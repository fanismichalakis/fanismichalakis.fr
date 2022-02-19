---
title: "Peeling the Onion"
date: 2022-02-17T09:00:00+01:00
cover:
    image: "../images/shrek-onions.gif"
    alt: "shrek and onions"
    caption: "<text>"
    relative: false
draft: false
---

`This article is the second (out of two) concerning Onion Routing. Therefore, it is recommended to read the first {{<newtabref href="https://fanismichalakis.fr/posts/onion-routing" title="article">}} before this one`

In a previous {{<newtabref href="https://fanismichalakis.fr/posts/onion-routing" title="article">}} I went into some details as to how Onion Routing allows payments to be processed accross the Lightning Network in a quite privacy preserving manner. More precisely, we saw how the identities of the emitter and the receiver of a payment are hidden via the use of successive layers of encryption in the messages that nodes exchange about a payment. But there are still some blind spots we'll want to shed some light on. Namely, we don't know what the messages are exactly and how they refer to HTLCs, nor do we know which keys are used for encryption. I find the latter question particularly interesting: we know the sender can't use their public key because it would completely undermine the privacy enabled by Onion Routing, but at the same time they need to coordinate with the intermediary nodes and give them some kind of public key. How does one do that? To find out, let's peel this mysterious onion!

## What's inside the Onion Packets?

The term "Onion Packet" refers to the message that each node in the route sends to the next one, starting from the sender, up to the final recipient of the payment. In this article, we will once again use our 5-nodes example where Alice pays Eve 20,000 sats, and where the payment passes throught Bob's, Carol's and Daniel's nodes to finally reach Eve.

```md
+-----+        +-----+        +-----+        +-----+        +-----+
|     |        |     |        |     |        |     |        |     |
|  A  |<------>|  B  |<------>|  C  |<------>|  D  |<------>|  E  |
|     |        |     |        |     |        |     |        |     |
+-----+        +-----+        +-----+        +-----+        +-----+
Emitter      Routing Node   Routing Node   Routing Node    Recipient
```

The Onion Packet itself is comprised of several parts, and can be brought down to this structure:
- a version byte, currently set to `0`, which will allow nodes to indicate which version of the protocol they use, should they be new ways to encode and transfer data in Onion Packets in the future,
- a session key, which we will cover in more details in the [section](#which-keys-does-onion-routing-uses) devoted to the cryptography of Onion Routing. Let's just say this is this session key that allows cryptographic coordination between Alice and each hop,
- the Onion Payload, which contains the useful data for each hop, as well as the encrypted data for the next hops,
- a checksum, which allows each hop to check the integrity of the Onion Payload (eg. that the data has not been corrupted or tampered with).

```md
|Version|Session Key|Onion Payload|Checksum|
```

This section concerns itself with the Onion Payload, what data it contains and how this relates to HTLCs.

### Onion Payload for Intermediary Nodes

What does a hop in the route needs to know in order to successfully forward the payment? First, the identity of the node it is supposed to forward the packet to. Second, the amount it must send to this next hop. This seems to be the bare minimum. But there is one additionnal field, called `outgoing_cltv_value`, which has to do with the sequential expiration of HTLCs (or PTLCs) along the route. Therefore, the structure of the Onion Payload for an intermediray node is:

```
short_channel_id: the channel along which to forward the payment
amt_to_forward: the amount to forward in this channel
outgoing_cltv_value: the block height at which the conditionnal payment should expire
```

#### Amount to Forward

The `amt_to_forward` field is pretty straight forward. The only thing worth mentionning at this point is that it is expressed in millisatoshis (the native currency unit of the Lightning Network). Let's focus on the two other fields.

#### Short Channel ID

The `short_channel_id` is a unique identifier for each channel. Per {{<newtabref href="https://github.com/lightning/bolts/blob/master/07-routing-gossip.md#definition-of-short_channel_id" title="BOLT 7">}}, it is defined as the concatenation of:
- the block height in which the funding transaction was included,
- the funding transaction index within the block,
- the index of the output of the funding transaction that actually funds the channel.

And structured like:

`block_height`x`tx_index`x`output_index`

In other words, the `short_channel_id` uniquely identifies the Bitcoin output corresponding to the channel, which is equivalent to uniquely identifying the channel. For example, a channel which funding transaction was confirmed in block 723,881, while the transaction was the 120th in the block (including the coinbase transaction, which has index 0) and the output actually funding the channel was the second one (eg its index is equal to 1) would have a `short_channel_id` of `723881x119x1`.

#### Outgoing CLTV Value

The `outgoing_cltv_value` also needs some explanations. I think it would be worth a whole article to fully explain the role *time* plays in Lightning, but for now we'll focus on what we need in order to understand Onion Routing.

CLTV stands for "Check Lock Time Verify" and it's a special kind of Bitcoin OP code providing timelock functionnalities. In other worlds, a Bitcoin transaction output with CLTV cannot be spent until some point in the future, referenced either as a UNIX timestamp or as a block height. In Lightning, conditionnal payments such as HTLCs or PTLCs have a timelock set using CLTV. If the channel is closed while a payment is still in-flight and the conditionnal payment commitment transaction gets published on-chain, this will prevent the funds from being spent for some time, allowing their rightful owner to claim them on-chain.

As we saw in the {{<newtabref href="https://fanismichalakis.fr/posts/ptlcs" title="PTLCs">}} article, conditionnal payments are either fulfilled or expire. Should the latter occur, it is necessary that the conditionnal payments along a route expire in a precise sequential order, starting from the recipient and moving up the route back to the sender. Else, intermediary nodes could find themselves in a situation where their own conditionnal payment has been claimed by the next node, but they are unable to claim the conditionnal payment from the previous node because it has already expired.

To ensure this ordered chain of expirations, when Alice builds the Onion Payload, she ensures that each routing node sets the block height at which its HTLC will expire at a bigger value than the one after them on the route. A simple way to do so would be to fetch the current block height, then tell the last routing node to set the expiration height of its HTLC to `current_block_height + 10` (for example), tell the penultimate routing node to set theirs at `current_block_height + 20`, and so on. But it is the intermediary routing nodes' funds that are at play here, not Alice's. Therefore, it is appropriate to allow intermediary nodes to set this delay themselves.

This is achieved by having nodes advertise a per channel parameter called `Time Lock Delta`. If you head over any Lightning explorer (such as {{<newtabref href="https://1ml.com" title="1ml.com">}} or {{<newtabref href="https://amboss.space" title="amboss.space">}} for example), you'll see that each public channel has a `Time Lock Delta` value, along with base fee, feerate and other parameters. This value can be set by the node owner, although it is often set to the default value of 40 blocks. When she constructs the route, Alice looks for this value for each node, just like she looks for the node's fees. For example, let's consider that:
- Daniel has a 40 blocks `Time Lock Delta` on his channel with Eve.
- Carol has a 20 blocks `Time Lock Delta` on her channel with Daniel,
- Bob has a 50 blocks `Time Lock Delta` on his channel with Carol,

Let's say that Alice tells Daniel to put the CLTV timelock on his conditionnal payment to Eve at block height `H =  723,900`. Hence:
- because Daniel has a delta of 40 blocks, he expects his incoming conditionnal payment from Carol to expire at block 723,940 (`H + 40`),
- because Carol has a delta of 20 blocks, she expects her incoming conditionnal payment from Bob to expire at block 723,960 (`H + 40 + 20`),
- because Bob has a delay of 50 blocks, he expects his incoming conditionnal payment from Alice to expire at block 724,010 (`H + 40 + 20 + 50`).

This way, conditionnal payments expire in the desired order, and node operators can manage their risk themselves by adjusting their `Time Lock Delta` value at will (just like they're able to do with their fees).

### Onion Payload for the Final Recipient

The Onion Payload for the recipient of the payment (Eve) is a bit different from the one for the intermediary nodes, because she doesn't need to forward the payment to anyone (and she must at the same time be able to link the payment she receives to the invoice she generated earlier). Eve's Onion Payload is therefore comprised of 3 fields:

```
amt_to_forward: the amount of the payment. Despite the name, Eve knows she does not need to forward it
outgoing_cltv_value: at what date will Daniel conditionnal payment to Eve expire
payment_secret: a secret Eve sent to Alice in the invoice. Not to be confused with the preimage s or its hash r. Only Alice and Eve know this secret.
```

Notice that the main difference with respect to the payload of intermediary nodes is the absence of a `short_channel_id` field, as Eve has nowhere to send the payment further. It is "replaced" with the `payment_secret` field, which helps Eve determine to which invoice this payment corresponds (notably if she has sent several invoices for the same amount around the same time). It also serves the purpose of protecting Eve from probing by intermediary nodes.

### Wrap Up

Let's sum it up a bit. First, we'll want to put the information available to Alice when she builds the Onion Packet on our diagram (where the base fee is in sats, and the Time Lock Delta in blocks):

```md
+-----+          +-----+          +-----+          +-----+          +-----+
|     |          |     |          |     |          |     |          |     |
|  A  |<-------->|  B  |<-------->|  C  |<-------->|  D  |<-------->|  E  |
|     |          |     |          |     |          |     |          |     |
+-----+          +-----+          +-----+          +-----+          +-----+
Emitter        Routing Node     Routing Node     Routing Node      Recipient
              Base Fee: 1k      Base Fee: 1k     Base Fee: 1k     Base Fee: 1k
               Feerate: 0%       Feerate: 0%      Feerate: 0%     Feerate: 0%
                Delta: 50         Delta: 20        Delta: 40   
```

Alice then buils the Onion Payload, which acts as instructions for the intermediary nodes:

```md
+---------------------------------+
| +-----------------------------+ |
| |           For BOB           | | Bob sends a HTLC to Carol
| |short_channel_id: 651034x98x0| | on their shared channel 651034x98x0
| |amt_to_forward: 22k sats     | | for an amount of 22,000 sats
| |outgoing_cltv_value: 724,010 | | with an expiration set at block 724,010
| +-----------------------------+ |
|                                 |
| +-----------------------------+ |
| |          For CAROL          | | Carol sends a HTLC to Daniel
| |short_channel_id: 672987x23x1| | on their shared channel 672987x23x1
| |amt_to_forward: 21k sats     | | for an amount of 21,000 sats
| |outgoing_cltv_value: 723,960 | | with an expiration set at block 723,960
| +-----------------------------+ | 
|                                 |
| +-----------------------------+ |
| |         For DANIEL          | | Daniel sends a HTLC to Eve
| |short_channel_id: 621340x12x0| | on their shared channel 621340x12x0
| |amt_to_forward: 20k sats     | | for an amount of 20,000 sats
| |outgoing_cltv_value: 723,940 | | with an expiration set at block 723,940
| +-----------------------------+ |
|                                 |
| +-----------------------------+ |
| |          For EVE            | | Eve receives her payment
| |amt_to_forward: 20k sats     | | of 20,000 sats (which she asked for in the invoice)
| |outgoing_cltv_value: 723,900 | | she has until block 723,900 to claim it
| |payment secret: ef45...b6    | | and it concerns the payment ef45...b6
| +-----------------------------+ |
+---------------------------------+
```

### What about the preimage?

An attentive reader who is already familiar with the inner workings of the Lightning Network may wonder how the payment preimage's hash `r` is passed between the nodes in the route, as it doesn't seem to be included in the Onion Payload.

When Alice sends the Onion Packet to Bob, she actually sends in a *message* called `update_add_htlc`. In this message, Alice tells Bob that she's sending him an HTLC, for a given amount, with a given expiry time, and for a given hash value `r`. The message actually looks like this:

```
channel_id: the id of the channel on which Alice sends the HTLC
id: the id of the HTLC, in case there are many (starts at 0)
amount_msat: the amount in the HTLC in millisatoshis
payment_hash: that's the hash r of our preimage. Yaï!
cltv_expiry: block at which the HTLC expires.
onion_routing_packet: that's our Onion Packet.
```

Bob, who wants to claim this HTLC, then takes a look at the Onion Packet to learn where he must in turn send a HTLC. He can send construct his own `update_add_htlc` message and send it to the next node in the route, because he learnt all the useful information in the payload. Here is the the message Bob builds, using `short_channel_id`, `amt_to_forward` and `outgoing_cltv_value` from his Onion Payload.

```xml
channel_id: short_channel_id
id: set by Bob depending on the presence of other HTLCs in the channel
amount_msat: amt_to_forward
payment_hash: the same as the one Bob received in the message from Alice
cltv_expiry: the cltv_expiry value in Alice message minus outgoing_cltv_value
onion_routing_packet: the new Onion Packet
```

And so does each node along the route. Now, let's take a look at how we do all of this, but with privacy!

## Which Keys does Onion Routing use?

The whole goal of Onion Routing is to hide who the sender and recipient of a payment are. Hence, when Alice sends a payment, she can't just use her node's public key to provide for the encryption and integrity of the Onion packet she constructs. Instead, Alice will use a one-time session public and private key for each hop in the route. The combination of this session key pair with the hop's public key will allow here to generate a shared secret, which the aforementioned hop will also be able to compute simply by knowing Alice's public session key (and, of course, its own private key). This way, the message intended for that hop can be encrypted so that only this node will be able to read it ; while at the same time the intermediary node will be able to tell that the data in the message has not been tampered with and was indeed put there by Alice (data integrity). Let's see how this works!

### Let's share a secret

Alice starts by creating a session private key for this payment and the associated public key, thus not revealing her node's public key. She sends the public session key in clear to Bob in the Onion Packet, so that both of them can compute an identical shared secret. In what follows, we will denote Alice's session private key as `a` and the corresponding public key as `A = a*G`, where `G` is the generator point on the elliptic curve, which we introduced in this article about {{<newtabref href="https://fanismichalakis.fr/posts/ptlcs" title="PTLCs">}}. On the other hand, `B` will be Bob's node public key, with `b` being the associated private key.

- Alice can compute a secret `s = a*B`, because she knows `a` (which she just generated) and `B` (it's Bob's node public key, so this data is available to all, and especially to Alice who chose to route her payment through this node).
- Bob can compute a secret `s' = b*A`, because he knows `b` (it's his own node's private key) and `A` (Alice's session public key, which she just sent to him in the Onion Packet).

Now, what if I told you that `s` and `s'` are actually the same? Indeed, if we use some parentheses to highlight the breakdown of public keys into private keys times `G`, as well as some interesting properties of elliptic curves multiplication, we can see that:

`s = a*B = a*(b*G) = (a*b)*G = (b*a)*G = b*(a*G) = b*A = s'`

We just demonstrated that `s` and `s'` are equal. We will therefore call them the *shared secret* between Alice and Bob, denoted `ss`.

That was for Bob, the first hop on the route. Now, Alice needs to do the same for each hop. Moreover, she needs to do it with a different session key for each hop, or else it could be easier for an attacker to deanonymize her. One simple, naive way of doing so would be by generating a distinct session key for each hop and sending each hop the key it is concerned with in its Onion Payload. But this would increase the size of the Onion more than necessary, and the people who designed the Onion Routing protocol in use in the Lightning Network[^1] actually came up with a much smarter way.

Once Alice has generated a session key for the first hop (Bob), she will deterministically alter it for the other nodes so that each hop has a different session key. To do so, she uses this simple formula:

`session_key_i = session_key_{i-1} * SHA-256(node_pubkey_{i-1} || shared_secret_{i-1})`

where `||` means a concatenation.

So the message Alice sends to Bob looks something like this:

```md
|Version|Session Key|Onion Payload|Checksum|
```

We'll soon cover into more details how Bob verifies the checksum and decrypts the Onion payload, but let's look at the session key first. With it, Bob can generate the shared secret on his end simply by performing an elliptic curve multiplication of the session key `SK` (caps because it is a public key) with his own private key:

`ss = b * SK`

With this shared secret, he is now able to derive some keys that will be useful for him to check the integrity of the payload (checksum), as well as decipher it to access the data addressed to him, as we'll see in the next [section](#and-derive-some-keys).

Once Bob has read his part in the Onion Payload, he removes it and adds some filler at the end of the payload so that it still weights the same as before (1300 bytes). Then, he computes a new session key for Carol, with the formula we saw earlier:

`session_key_carol = session_key_bob * SHA-256(node_pubkey_bob || shared_secret_bob)`

and appends this new session key before the Onion. From the part of the payload he deciphered and removed, Bob also extracts a checksum for Carol, which he puts after the payload. He then adds the version byte at the beginning and, tada!, Carol's message is ready to be sent:

```md
|Version|Session Key Carol|Onion Payload|Checksum|
```

This way, Carol receives from Bob a message with exactly the same structure as the one Bob received from Alice. Therefore, she can't tell wether Bob was the emitter of just an intermediary node. Conversely, when Bob received the first message from Alice, he couldn't tell wether she was a hop in the route or indeed the sender of the payment.

Each hop along the route repeats the same process, until the message reaches the final node:
1. Generate shared secret from the multiplication of the session key with their own private key.
2. Derive various keys from shared secret to:
    - check integrity
    - decypher the Onion Payload
3. Extract from the Onion Payload the part that is readable to them. The rest isn't intelligible because it is encrypted with the public keys of other nodes.
4. Add some filler in replacement so that the Onion Payload still weights the same.
5. Extract the checksum for the next hop from their own part of the payload (which they just extracted in step 3) and append it after the Onion Payload.
6. Compute the session key for the next hop by applying the formula to their own session key, public key and share secret. Append this new session key before the Onion Payload.
7. Add the version number (just `0` for now) before the rest.
8. Send this new message to the next hop.

### And derive some keys

We've seen in what preceeds how each hop in the route is able to generate a shared secret, which besides themselves is only known to Alice. Each node in the route will then use this shared secret to derive 4 different keys:
- *rho* used for the encrypting of the Onion Payload,
- *mu* used for the integrity verification (checksum),
- *um* used for error reporting (more on that later),
- *pad* used by Alice in the beginning to generate initial padding.

One crucial aspect of this key generation is that, for each hop, Alice and the hop are able to generate the same keys, but anyone else just can't. This is because only Alice and the hop can generate the same shared secret (Alice with the private session key corresponding to this hop and the hop's public key ; the hop with the public session key and its own private key).

We saw in the beginning of this article how Alice builds the Onion Payload. It is now time to see how she does so while also adding several layers of encryption.

1. Alice starts by generating 1,300 bytes of random data (using the *pad* key), reprensented as Fs (stands for *filler*). That's her Onion Payload at the beginning.

```md
|FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF|
```

2. She takes the last hop payload (eg the payload of the recipient Eve), and adds 32 bytes of 0s at the end of it. Those 0s act as the "checksum" over Eve's payload, and it being all zeroes indicates to Eve that she is indeed the final node in the route.

3. She adds Eve's payload and its checksum to the left end of the Onion Payload and remove the same amount of filler from the right end, so that the Onion Payload still has a length of 1,300 bytes at all time.

```md
|PayloadECheckFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF|
```

4. Alice uses the *rho_eve* key[^2] and a specific algorithm to generate a 1,300 bytes stream. What is important to note at this point is that anyone with the same key and using the same algorithm would generate the exact same 1,300 bytes. Then, Alice applies the XOR operation between the Onion Payload and the bytes generated with the *rho_eve* key. There is no need to know what XOR does exactly, apart from the fact that this function has the nice property that, if applied twice on an object, it returns the object itself ; but if applied once, it returns something completely different (it's bit like a light switch). After the XOR operation, the whole Onion Payload looks like some random byte stream.

```md
|ac7f98b6eec079f9e2d9c9d243255f40e25ba26107ee8dff3d97c5b2d88f13d3f|
```

5. Alice uses the *mu_eve* key to compute the checksum of the whole Onion Payload. 

6. Alice then takes Daniel's payload, put it with the checksum she just computed (step 5) and append all of it at the left end of the Onion Payload. Just like in step 3, she also removes the same amount of data from the filler (right end of the Onion Payload) that she just added, so that the Onion Payload still is 1,300 bytes long.

```md
|PayloadDCheckac7f98b6eec079f9e2d9c9d243255f40e25ba26107ee8dff3d97|
```

7. Then, she obfuscates the Onion Payload as she did in step 4, but this time using the *rho_daniel* key she shares with Daniel.

```md
|4bcf430964f7b4156aca1b1321f77a61c5af86dbf5876a2b320287e007a70bf2a|
```

8. Using the *mu_daniel* key, she computes the checksum of the whole Onion Payload.

9. Alice then takes Carol's payload and the checksum she generated in step 8, and add them at the left end of the Onion Payload. Once again, she removes the excess filler from the right side of the Onion Payload so that it still measures 1,300 bytes.

```md
|PayloadCCheck4bcf430964f7b4156aca1b1321f77a61c5af86dbf5876a2b3202|
```

10. Then, she encrypts the whole Onion Payload using the *rho_carol* key.

```md
|afbe2be5df68754ae81c8c4a1ea83791b72a60a4f1ae26c7bc9e999cc31e267e2|
```

11. Like in step 8, she computes the checksum over the whole Onion Payload, this time using the key she shares with Carol *mu_carol*.

12. She appends Bob's payload followed by the checksum to the left of the Onion Payload, and trims the excess filler from the right side.

```md
|PayloadBCheckafbe2be5df68754ae81c8c4a1ea83791b72a60a4f1ae26c7bc9e|
```

13. She encrypts the whole Onion Payload using the *rho_bob* key she shares with Bob.

```md
|817026b954c63094a08fd6e694cd5fe72690a7e919122786314843de2ceb9575f|
```

14. With *mu_bob*, she computes the checksum over the whole Onion Payload. She puts it after (right side) the Onion Payload.

```md
|817026b954c63094a08fd6e694cd5fe72690a7e919122786314843de2ceb9575f|Checksum|
```

15. Now, all Alice has to do is add the version byte and the session key before (left side) the Onion Payload, to conclude the Onion Packet.

```md
|0|Session Key|817026b954c63094a08fd6e694cd5fe72690a7e919122786314843de2ceb9575f|Checksum|
```

The Onion Packet is ready to be sent to Bob! 🥳

### Peeling the Onion

Now, the nodes in the route will receive the Onion Packet from the node before them, extract their own payload plus the next hop's checksum from it, add some **deterministic** filler so that the Onion Payload still weights the same after they removed their part, replace the checksum at the end of the Packet with the one they just extracted, and pass the Onion Packet along. Let's see in more details what happens sequentially:

1. Bob receives the Onion Packet from Alice. The first thing he does is check the checksum against the whole, still encrypted, Onion Payload.

```md
|0|Session Key|817026b954c63094a08fd6e694cd5fe72690a7e919122786314843de2ceb9575f|Checksum|
                                              ^                                      |
                                              |                                      |
                                              +----------------- ? ------------------+
```

2. If the check is successful (meaning the data hasn't been altered), he decrypts the Onion Payload. To do so:
    - he generates a 1,300 bytes stream with the *rho_bob* key and the same algorithm that Alice used. Hence, he obtains the same 1,300 bytes as Alice in step 13.
    - he applies the XOR operation between the 1,300 bytes he generated and the Onion Payload. As stated before, applying XOR twice is like doing nothing. Hence, after using XOR, Bob obtains the Onion Payload as it was before Alice herself used XOR on it in step 13. In other words, he decrypted his payload!

```md
|PayloadBCheckafbe2be5df68754ae81c8c4a1ea83791b72a60a4f1ae26c7bc9e|
```

3. Bob extracts his payload `PayloadB` and the checksum `Check` from the Onion Payload. The rest of the payload is still encrypted. Reading `PayloadB`, Bob knows what amount to transfer in a conditionnal payment, to whom, and with what expiry date.

4. Now that Bob has extracted `PayloadB` and `Check`, the Onion Payload is shorter. To fix this, Bob uses a *padding_key* he derives from the *pad* key to generate enough filler at the end. This allows him to generate the same filler as the one Alice created, and he hence obtains the same Onion Payload as Alice in step 10. This is necessary for the checksum `Check` to still be valid, as it was computed for Carol's whole encrypted payload.[^3] Bob adds the checksum for Carol after the Onion Payload

```md
|afbe2be5df68754ae81c8c4a1ea83791b72a60a4f1ae26c7bc9e999cc31e267e2|Check|
```

🚧 Note that this deterministic filler generation is still something I feel I don't completely grasp. I may have made some mistake or oversimplification. For instance, my understanding of the specification goes again what is written in _Mastering the Lightning Network_ by Antonopoulos, Osuntokun and Pickhardt, and I would doubt myself before doubting the three of them. **The important part is that filler was generated to keep the lenght of the Onion Payload at 1,300 bytes, and the checksum is still valid for the next hop.** 🚧

5. For the Onion Packet to be complete and for him to be able to send it to Carol, Bob must still add the version byte and the session key. The version is still set to `0`. For the session key, Bob uses what we saw in ["Let's share a secret"](#lets-share-a-secret) to transform the session key he received from Alice into a new session key. Note that this process is deterministic, that's how Alice herself generated the four session keys (one for each hop, incl. Eve) and the associated *shared secret*. Hence, with this "new" session key, Carol will indeed be able to generate the appropiate shared secret and therefore *rho_carol*, *mu_carol*, and so on.

Bob has now constructed the whole new Onion Packet and he can send it to Carol.

```md
|0|Session Key Carol|afbe2be5df68754ae81c8c4a1ea83791b72a60a4f1ae26c7bc9e999cc31e267e2|Check|
```

6. Once Carol receives the Packet from Bob, she does the same things that he did in steps 1 to 5. She uses the session key to create her keys *rho_carol* and *mu_carol*, uses *mu_carol* to check the cheksum against the Onion Payload, uses *rho_carol* to decrypt the Onion Payload, extrat her own payload from it, generate *deterministic* filler to replace what she extracted, add the checksum for Daniel at the end and compute Daniel's session key.

Then, she sends the new Onion Packet to Daniel.

```md
|0|Session Key Daniel|4bcf430964f7b4156aca1b1321f77a61c5af86dbf5876a2b320287e007a70bf2a|Check|
```

7. Once he receives the Packet from Carol, Daniel does the same things. He ends up with the following Onion Packet, ready to be sent to Eve.

```md
|0|Session Key Eve|ac7f98b6eec079f9e2d9c9d243255f40e25ba26107ee8dff3d97c5b2d88f13d3f|Check|
```

8. Eve finally receives the Onion Packet from Daniel. She uses the session key to generate the various keys, checks the checksum, and decrypt the Onion Payload, which is now nothing but her own payload and filler. She reads in her payload the information about the payment.

That's it, folks! Using outstanding cryptography and some smart ass optimizations (session key randomization for the win!), the Onion Packet was moved from Alice to Eve while retaining privacy at all time.

## TL;DR

The Onion Packet contains several, layered, encrypted Onion Payloads which indicates to each node the parameters of the HTLC (or PTLC) it must create to forward the payment. This includes the amount to forward, to who, as well as what expiration delta to maintain between HTLCs. In order to avoid using its node public key, the original sender of the payment uses a one-time session key, different for each hop in the route. The sender builds the payload and applies successive layers of encryption on said payload, using said keys. As the Onion Packets moves along the route, each node checks the integrity of the packet and extract its own payload, before sending it to next node in the route.

## Ressources
-  {{<newtabref href="https://github.com/lnbook/lnbook/blob/develop/10_onion_routing.asciidoc" title="Chapter 10">}} of Mastering the Lightning Network
- BOLTs {{<newtabref href="https://github.com/lightning/bolts/blob/master/04-onion-routing.md" title="4">}} and {{<newtabref href="https://github.com/lightning/bolts/blob/master/07-routing-gossip.md#definition-of-short_channel_id" title="7">}}. 

[^1]: It's called SPHINX and was designed by George Danezis and Ian Goldberg. Here is their {{<newtabref href="https://www.cypherpunks.ca/~iang/pubs/Sphinx_Oakland09.pdf" title="paper">}} if you're into it.

[^2]: *rho_eve* refers to the *rho* key derived from the shared secret between Alice and Eve. I'll use the same notation for other keys and other nodes.

[^3]: Note that in sequential order, the padding actually happens before the decryption of the payload. More details can be found in {{<newtabref href="https://github.com/lightning/bolts/blob/master/04-onion-routing.md#filler-generation" title="Bolt 4">}} and in the implementations' {{<newtabref href="https://github.com/lightningnetwork/lightning-onion/blob/master/packetfiller.go" title="code">}} (LND here).
---
title: "What Are PTLCs"
date: 2022-01-15T12:00:00+01:00
cover:
    image: "../images/storm.jpg"
    alt: "storm"
    caption: "<text>"
    relative: false
tags: ["lightning", "bitcoin"]
categories: ["articles"]
draft: false
---

If the Lightning Network is so useful today, it is in great part thanks to the fact that payments can be **routed** inside the network: if Alice wants to pay Bob, it isn't necessary that she has a direct channel with him. Instead, she can have a channel with Carol and, if Carol has a channel with Bob, use Carol's channel to reach Bob.

With this mechanism arises a new question: how can such payments, that rely on the benevolence of third parties such as Carol, be achieved in a trustless way? For a long time, HTLCs (for Hash Time Locked Contracts, a special kind of conditional Bitcoin transactions) have been the answer. But they in turn induce a few drawbacks, notably in terms of privacy.

That's why a new savior was crafted: PTLCs (Point Time Locked Contracts), which deliver the same benefits as HTLCs but in a privacy preserving manner.

## HTLCs?

Hash Time Locked Contracts are key to the way Lightning works today, because they allow payments to be trustlessly routed across the network. This way, it is possible to send a payment to someone with which I have no direct channel, as long as there exist a route between us within the network.

The trustlessness is achieved in the same way as it is often achieved on Lightning: by crafting and signing specifically designed Bitcoin transactions, that we don't publish unless there is a problem, in which case we can recover our funds on-chain.

I've published a {{<newtabref href="https://www.youtube.com/watch?v=-JC4mkq7H48" title="video">}} explaining how HTLCs work, which has recently been enriched with French and English subtitles. Feel free to watch it if this format is more appealing to you. In the following lines, I'll try to summarize how HTLCs work anyway.

The life of a Lightning payment begins with the person being paid (Bob) creating an invoice. This invoice contains various information such as Bob's public key (his "address" on the network), the amount he wants to be paid (for example 40,000 sats), etc. It also includes a number, often denoted as *r*. This number is the hash of a secret, denoted *s* and called the **preimage**, that Bob randomly created for this specific payment. Bob then sends the invoice to the person he wants to be paid by (Alice).

```md
Asking for a payment:
1. Randomly generate a preimage s
2. Compute r = hash(s)
3. Create invoice with `amount`, `pubKey`, `r`, etc.
4. Send invoice to Alice.
```

When she receives the invoice, Alice starts by trying to find a route to Bob's node. Ideally, she would have a direct channel with Bob, but often she has to pass through other nodes in the network. In this case for example, she selects a route that goes through Susie's node.

```md
+-----+        +-----+        +-----+
|     |        |     |        |     |
|Alice|<------>|Susie|<------>| Bob |
|     |        |     |        |     |
+-----+        +-----+        +-----+
```

She then crafts a conditionnal payment, an HTLC, which she sends to Susie. This HTLC says: "here are 40,000 sats. If you want to claim them, you need to give me a secret *s'* such as the hash of *s'* is equal to *r* ". In the rest of this article, we will use the notation `HTLC(r)` to represent such a HTLC[^1]. It also tells Susie that a good way for her to learn the secret is to ask Bob. So Susie in turn crafts her own HTLC(r), sending 40,000 sats with the same condition of revealing a secret *s'* which hash equals r, and sends it to Bob.

Now all Bob has to do to unlock the conditionnal payment and claim the 40,000 sats, is reveal some secret number which hash equals *r*. He has just that in stock as, per construction, `r = hash(s)`. Bob therefore reveals the preimage *s* to Susie, which allows him to "unlock" the conditionnal payment and claim the 40,000 sats. Now that Susie knows *s*, she can in turn reveal it to Alice and hence satisfy the condition of Alice's HTLC to her. Once the two HTLCs are resolved, the payment is completed: Alice has 40,000 sats less than before, Bob 40,000 more, and Susie's balance hasn't change. To move 40,000 sats from Alice to Bob, 40k sats were moved between Alice and Susie from Alice's side of their channel to Susie's, and 40k sats were moved between Susie and Bob from Susie's side of their channel to Bob's, all of this atomically[^2].

Should the payment involve two intermediary nodes (Susie and Tim), there is just one additionnal HTLC between Susie and Tim. Each intermediary node is only aware of the node before them and the node after them: Susie knows that she must send a HTLC to Tim if she wants to learn the secret, but she has no idea wether Tim is the final recipient or not. She doesn't know if Alice is the original sender or another hop in the route either. It's called Onion Routing, and it brings some level of privacy to payments on the Lightning Network.

```md
+-----+        +-----+        +-----+        +-----+
|     |        |     |        |     |        |     |
|Alice|<------>|Susie|<------>| Tim |<------>| Bob |
|     |        |     |        |     |        |     |
+-----+        +-----+        +-----+        +-----+
```

For example, in the four nodes example, the whole procedure would look something like:

```md
1. Bob randomly generates a preimage s, computes r = hash(s) and send r to Alice in the invoice
2. Alice selects a route to Bob that passes through Susie and Tim
3. She sends a HTLC(r) to Susie.
4. Susie only knows that she received a HTLC(r) from Alice, and that she can get the corresponding secret by asking Tim. She sends a HTLC(r) to Tim to learn the secret.
5. Tim only knows that he received a HTLC(r) from Susie, and that he can get the corresponding secret by asking Bob. He sends a HTLC(r) to Bob to learn the secret.
6. Bob reveals the preimage (secret) s to Tim, which unlocks Tim's HTLC and sends the funds from Tim to Bob.
7. Tim reveals the preimage he just learnt to Susie, which unlocks Susie's HTLC and sends the funds from Susie to Tim.
8. Susie reveals the preimage she just learnt to Alice, which unlocks Alice's HTLC and sends the funds from Alice to Susie.
9. Tada! 🎉 Payment completed!
```

HTLCs allow the payment to be trustlessly completed even if it involves multiple third parties. Onion Routing apppears to protect privacy by concealing who the sender and the recipient are to intermediary nodes on the route. So, why replace HTLCs with something new?

## HTLC Bad?

One of the issues with HTLCs is that the same preimage is used along the whole route. Additionnaly, given the fact that the preimage is randomly generated by the recipient of the payment, there are very little chances that two different payments use the same preimage. Because of this, if an entity (individual, company, etc.) controls multiple nodes along the route of a payment, it can effectively recognize that what came in in some place and came out in some other are in fact the same overall transaction. Then, using some heuristics (regarding route length or node types for example), it can then try to guess which node in the route is the emitter of the payment, and which is the recipient. All the gains in terms of privacy provided by Onion Routing are then lost. Bad!

Let's consider a simple example with 5 nodes: Alice, Bob, Carol, Daniel and Eve. Alice sends a payment to Eve but, because she has no direct channel with her, she must find a route in the network. She chooses to use the route that goes through Bob, Carol and Daniel. What she doesn't know though, is that Bob's and Daniel's nodes actually belong to the same entity (let's say it's {{<newtabref href="https://fanismichalakis.fr/posts/chainalysis-to-launch-lightning-network-support/" title="Chainalysis">}}).

```md
+-----+        +-----+        +-----+        +-----+        +-----+
|     |        |     |        |     |        |     |        |     |
|  A  |<------>|  B  |<------>|  C  |<------>|  D  |<------>|  E  |
|     |        |     |        |     |        |     |        |     |
+-----+        +-----+        +-----+        +-----+        +-----+
Emitter         Spook       Honest Node       Spook        Recipient
```

Because the HTLCs all use the same preimage *s* (with *r* being the hash of this preimage), the attacker controlling Bob et Daniel nodes knows it is the same payment. Bob's node knows that he received an HTLC(r) from Alice and sent an HTLC(r) to Carol. Daniel's node knows that he received an HTLC(r) from Carol and sent an HTLC(r) to Eve.

With this information, the attacker can already establish with certainty that Carol is just an intermediary node. If there were any other hops between Bob et Daniel, the attacker doesn't necessarily know about them, but he knows that whatever happens between Bob and Daniel is just hops along intermediary nodes.

Yet, the attacker doesn't know for sure that Alice is the emitter of the payment. In fact, there could be another node before Alice, and Alice could be just another intermediary. Same goes for Eve. **But** we know that a payment's reliability decreases with the length of a the route: a node can be offline, the liquidity in a channel can be on the on the other side than the one we need it to be, etc. ; and with each node the probabilities that something goes wrong compound. The attacker can therefore consider that it is unlikely for a route to have more than 3 intermediaries[^3]. The attacker could also know that Alice and Eve are mobile nodes (because they are often offline and their IP address often changes), which usually don't route payments and are only emitters and receivers. Using this kind of heuristics, the attacker could therefore consider it is likely that Alice is the emitter of the payment and Eve the recipient. They could say something like "our investigation led us to believe that Alice is the sender and Eve the recipient with a 90% confidence interval".

If an attacker had a few very well connected nodes, with competitive fees, they could very well become *de facto* hubs of the network and find themselves quite often in a situation where they can successfully "break" Onion Routing's privacy and reconstruct the origin and destination of a payment. Is Lightning privacy doomed?

## PTLCs *à la rescousse*

The main problem here regarding privacy is that we reuse the same preimage along all the hops in the route. More precisely, each HTLC in the route must be unlocked by revealing the same preimage[^4]. Is there an other way to do it? What we need is:
- the emitter (Alice) must be able to provide some proof of payment to the payee (Bob) once the payment is completed,
- each hop in the route must be able to unlock the conditionnal payment sent by the previous node by revealing some secret *s*,
- to be able to learn this secret *s*, each hop must send a conditionnal payment to the next node in the route requiring the revealing of a secret *s'* that can then be used to find the secret *s*.

One "easy" way to check all three conditions is to reuse the same secret *s* along the whole route. That's what we do with HTLCs. But it isn't the only way, as it not *required* that *s* and *s'* are equal. The only requirement is that secrets are built in such a way that, upon learning *s'*, a node can deterministically know what *s* is. Enter PTLCs.

With HTLCs, the payee (Bob) initially creates a payment secret, the preimage. With PTLCs, the payee will do something very similar but with a private key. Both the preimage and the private key are just random numbers, the difference is what we use them for.

To understand what follows, we also need some very basic understanding of how elliptic curve cryptography works, and especially elliptic curve point multiplication. An elliptic curve is a very specific curve that yields interesting properties. The point of this article is not to dwelve to deep into this, hence we will only introduce what is useful to us here.
- We define an addition operation, denoted `+`, between points on the elliptic curve. The sum `R` of two points `P` and `Q` of the curve is also a point of the curve, but it's location on the curve cannot be directly linked to the one of `P` and `Q`.
- We define a multiplication operation, denoted `*`, which represents successive additions of the same point to itself. In other words, if `k` is a number and `P` a point on the curve, `k*P = P + P + ... + P`, k times. Because we add `P` to itself over and over again, `k*P` can basically be anywhere on the curve. In other words, if I know `P` and `k*P` (which are 2 points on the elliptic curve), I can't find `k`.
- The `*` operand has some additional interesting properties, such as the distributive property: `a*P + b*P = (a+b)*P`.

We apply these properties of elliptic curves in cryptography as follows:
- A private key `s` is just a very long number.
- The public key associated with the private key `s` is `s*G`, where `G` is a specific point on the curve, called the base point, or the generator. In other worlds, `G` is a point on the curve and a constant.
- Even if someone knows the public key `s*G`, they can't guess the private key `s`, even if they know `G`.

Another thing worth nothing, which doesn't concern elliptic points additions but classic numbers addition, even if trivial, is that knowing `a + b` is very different from knowing `a` or `b`. And that even if I know `a + b + c` and `a`, I am far from knowing either `b` or `c`.

Now that we are equipped with all these concepts, let's take again our 5 nodes example, where Alice pays Eve *via* Bob, Carol and Daniel ; and where Bob and Daniel are actually an attacker trying to deanonymize the transaction.

```md
+-----+        +-----+        +-----+        +-----+        +-----+
|     |        |     |        |     |        |     |        |     |
|  A  |<------>|  B  |<------>|  C  |<------>|  D  |<------>|  E  |
|     |        |     |        |     |        |     |        |     |
+-----+        +-----+        +-----+        +-----+        +-----+
Emitter         Spook       Honest Node       Spook        Recipient
```

The flow of the payment would be something like:

1. Eve has a secret private key `s` and gives the public key `s*G` to Alice in an invoice, just like she did with the hash of the preimage when we used HTLCs.
2. Alice looks for a route and select one that goes through 3 hops: Bob, Carol and Daniel.
3. Alice generates 4 random numbers `a`, `b`, `c` and `d`. She sends `b` to Bob, `c` to Carol and `d` to Daniel. She also sends `(a + b + c + d)` to Eve (the sum, not `a`, `b`, `c` and `d` separately).
4. Alice sends to Bob a conditionnal payment where the condition is that Bob reveals the private key associated with `(a + s)*G`, which is `(a + s)` by definition. Bob is also told (in the onion packet) that Carol knows the private key associated with `(a + s)*G + b*G`, which is just `(a + b + s)`.
5. Bob realizes that, if he knew `(a + b + s)`, he could then compute `a + s = a + b + s - b` and reveal it to Alice to claim his payment, as he already knows `b` which Alice sent to him in step 3. He therefore sends a conditionnal payment to Carol, requiring that she sends him the private key associated with `( a + b + s)*G`.
6. When Carol receives the conditionnal payment from Bob, she's also told that Daniel knows the private key associated with `(a + b + s)*G + c*G`, which is `(a + b + c + s)`. Knowing `a + b + c + s` and `c`, Carol could then compute `a + b + s` by substraction. She sends a conditionnal payment to Daniel, with the condition that he reveals the private key associated with `(a + b + c + s)*G`.
7. When Daniel receives the conditionnal payment from Carol, he's also told that Eve knows the private key associated with `(a + b + c + s)*G + d*G`, which is `(a + b + c + d + s)`. Knowing `a + b + c + d + s` and `d`, he could then compute `a + b + c + s` by substraction and unlock Carol's conditionnal payment. To learn `a + b + c + d + s`, he sends a conditionnal payment to Eve requiring her to reveal the private key associated with `(a + b + c + d + s)*G`.
8. Eve already knows `s` because it's the secret the generated in the first place. She's also aware of `(a + b + c + d)` because Alice sent it to her in step 3. This way, she's able to reveal `a + b + c + d + s` to Daniel and claim his payment.
9. Now that he knows `a + b + c + d + s`, Daniel can compute `a + b + c + s` and reveal it to Carol, claiming her payment.
10. Now that she knows `a + b + c + s`, Carol can compute `a + b + s` and reveal it to Bob, claiming his payment.
11. Now that he knows `a + b + s`, Bob can compute `a + s` and reveal it to Alice, claiming her payment.
12. Alice now knows `a + s`. As she already knew `a`, she's able to quickly compute `s` by substraction. The secret `s` is Alice's proof of payment, which she can use to prove to Eve that she paid the invoice.

```md
+-----+                    +-----+                    +-----+                    +-----+                    +-----+
|     |                    |     |                    |     |                    |     |                    |     |
|  A  |-----PTLC(a+s)----->|  B  |----PTLC(a+b+s)---->|  C  |---PTLC(a+b+c+s)--->|  D  |--PTLC(a+b+c+d+s)-->|  E  |
|     |                    |     |                    |     |                    |     |                    |     |
+-----+                    +-----+                    +-----+                    +-----+                    +-----+
```

Using this construction, each hop in route is aware of a different secret. Even if they work together, Bob and Daniel don't know enough information to tell wether they're part of the same payment or not:
- once the payment is completed, Bob only knows `a + b + s`, `b` and `a + s`
- once the payment is completed, Daniel only knows `a + b + c + d + s`, `d` and `a + b + c + s`.

Even when they put all those information in common, they can't guess wether they were part of the same payment or not. We can see, from our omniscient point of view, that they can compute `c` with `c = a + b + c + d + s - d - (a + b + s)`[^5]. But it doesn't really mean anything to them, and they would be able to find some random number even if they were not part of the same payment. They just don't know enough to compute the only common denominator of this payment, which is `s`.

Of course, they still know when two consecutive nodes they control are part of the same payment, as each routing node learns the next hop in its onion packet. But it would require the attackers to control Bob, Carol and Daniel nodes in order to be able to use the same heuristics that we've seen before (eg. the route is "probably" not longer than 3 hops). In other words, PTLCs are defeated only when the attacker controls all the nodes in the route. And even then, the attacker still can't they for sure wether Alice is the emitter and Eve the sender, as they rely on the same heuristics as before.

## TL;DR

Because they reuse the same secret along the whole route of a payment, HTLCs can seriously downgrade the pricacy aquired (at the cost of some significant inefficiencies) thanks to Onion Routing. PTLCs, on the other hand, use a different secret for each hop in the route. This way, the privacy enabled by Onion Routing is preserved.

## Additional ressources

In this article, we focused solely on the privacy aspect of PTLCs. However, they have many other implications, detailed in this series of articles by {{<newtabref href="https://suredbits.com/payment-points-part-1/" title="Suredbits">}}.


[^1]: We omit the amount part because it is not really relevant for this specific article. Of course, a more detailed notation could be `HTLC(40000, r)` for a HTLC paying 40,000 sats on condition that the recepient reveals a secret s' such that hash(s') = r.

[^2]: We omit the routing fees that Susie may take for the sake of simplicity.

[^3]: Of course, a payment with 4 hops (and therefore 4 intermediaries) can be successful. The point is we can attach probabilities, based on statistics, to such events.

[^4]: Note that this design doesn't only impact privacy. In our 5 nodes configuration example where Bob and Daniel are actually the same person, Daniel can send the preimage to Bob as soon as he learns it from Eve, bypassing Carol. Bob can then reveal the preimage to Alice: to everyone but Carol, the payment appears to be completed. For Carol, it appears as still pending, until her HTLC eventually times out. But in the meantime, Bob and Daniel have been able to collect Carol's fees in her place.

[^5]: It is also worth mentionning that they can learn `c` only once the payment is settled. It contrasts with HTLCs, where Daniel was able to trasmit the preimage directly to Bob and bypass Carol. This kind of fee-stealing attacks are not possible anymore with PTLCs. 
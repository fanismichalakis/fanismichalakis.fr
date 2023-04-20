---
title: "Latest Strikes 28"
date: 2023-03-22T18:30:00+01:00
block: "781992"
cover:
    image: "../images/WanderingInCyberspace.jpg"
    alt: "A robot seems to be emerging from a gigantic motherboard."
    caption: "\"Wandering In Cyberspace\". Generated with Stable Diffusion."
    relative: "false"
tags: ["bitcoin", "lightning"]
categories: ["strikes"]
draft: false
---

Hello Strikers! Welcome to this 28th issue of Latest Strikes, your weekly dose of the hottest news and updates from the Lightning Network ecosystem. Whether you're a seasoned Bitcoin veteran or a curious newcomer, we try our best to make this newsletter as useful and approachable as possible, and make it your go-to source for all things Lightning-related. Last week, we've had some drama again with Core Lightning's Descriptiongate, a legal hassle, and a novel proposition for off-chain resizing of Lightning channels. And on top of that, of course, builders kept on building!

## Ecosystem

### First Wolf Pack Announced

Wolf, a New York City based incubator for Lightning startups (which we discovered first in {{<newtabref href="https://fanismichalakis.fr/posts/latest-strikes-8/#wolf-accelerator" title="October 2022">}}) has {{<newtabref href="https://wolfnyc.com/news-wolfpack-1" title="announced">}} its first cohort of projects. This first "wolfpack" is comprised of 8 teams, working and building on top of Bitcoin and the Lightning Network. Wolf didn't share exactly which startups entered the program, but gave some details as to what their main topics are.

Some of the projects aim to improve current systems and infrastructure with Lightning (for example by creating a "Lightning-monetized content delivery infrastructure", integrating payments into esport tournaments or facilitating payments and remittances in MENA (Middle East and North Africa) markets), while others focus on building better tools for users and node operators (such as automated node management, Lightning infrastructure and non-custodial wallets). Finally, a team is working on a "WeChat-style super app" (e.g. an app that includes a wide range of functionalities, such as chat, payments, online shopping, food delivery, travel booking, etc., all from a single app) taking advantage of nostr and Lightning ; while another startup will develop self-custodial trading on Lightning using DLCs (should remind you of {{<newtabref href="https://fanismichalakis.fr/posts/latest-strikes-22/#10101s-roodmap" title="something">}}).

Wolf also announced that applications for the incubator's second cohort are {{<newtabref href="https://wolfnyc.com/apply" title="open">}} until April 7th 2023.

### On Custodial Services For Merchants

Onboarding businesses to accept Bitcoin can be hard sometimes, and onboarding them to accept Bitcoin in a self-custodial way is even harder. A tremendous collective effort is underway to bring more and more easy self-custodial solutions to merchants (from light mobile nodes to plug-and-play full node distributions with easy installation of tools such as BTCPay Server), but they often aren't just there yet in terms of ease-of-use, not having to spend to much time on maintenance, or being fully compliant with local regulation (in terms of editing receipts than your accountant will be happy with, for example). While self-custodial point of sale solutions should be the end goal, in the meantime I believe we can settle for another class of products: custodial services with very frequent automatic withdrawals.

For example, {{<newtabref href="https://swiss-bitcoin-pay.ch/" title="Swisspay">}} allows a brick-and-mortar business to easily accept payments on-chain and with Lightning (including LN NFC cards, with a {{<newtabref href="https://nitter.lacontrevoie.fr/SwissBitcoinPay/status/1637746047471480833" title="double factor authorization">}} for the customer), with every member of staff being able to receive payments with a smartphone but only the manager being able to send. Additionally the funds are automatically withdrawn to the company's own wallet (either on-chain or Lightning), so that at any time what is at risk is "only" the revenues of the day.

Another similar service {{<newtabref href="https://nitter.lacontrevoie.fr/utxo_one/status/1636543980023185408" title="launched">}} last week. Called {{<newtabref href="https://nodeless.io/" title="Nodeless">}}, it's more focused on the e-commerce side (with a WooCommerce integration) but similarly performs automatic withdrawals to the merchants self-custodial wallet, on an even short period of time (currently every {{<newtabref href="https://support.nodeless.io/support/solutions/articles/151000052796-how-do-i-withdraw-to-my-on-chain-bitcoin-address-" title="4 hours">}}).

As I said above, while I think (and hope) this kind of solutions are only a temporary patch until end-to-end self-custodial ones are mature enough, is great to see them popping everywhere, as they help merchants get accustomed to the idea of self-custody without having to immediately go for the full self-sovereign merchant pack.

### Will Lightning LAbs TARO Protocol Need To Change Its Name?

The American justice system invited itself to the Lightning party last week with a temporary injunction preventing Lightning Labs from "making external updates to its
TARO protocol, from merging its internal updates with its public-facing open-source code for the TARO protocol, and from announcing or otherwise “launching” the next stage or “milestone” of the TARO protocol"[^1].

This injunction is the result of a lawsuit brought by blockchain startup Tari Labs (developing the Tari protocol) against Lightning Labs (developing the Taro protocol) over a trademark infringement. Tari Lab's claim is that both protocol cover similar use cases (the issuing of digital assets) and have similar enough names to constitute such an infringement. This lawsuit and the subsequent injunction prompted some backlash on social media (with for example BitMEX Research account calling it a {{<newtabref href="https://nitter.lacontrevoie.fr/BitMEXResearch/status/1636010708998471683" title="\"pretty bad ruling\"">}}).

Now, I'm going to be a little contrarian here. I dislike trademarks, I dislike copyright (every post I write and publish online is licensed under {{<newtabref href="https://creativecommons.org/licenses/by-sa/4.0/" title="CC BY-SA">}}). Maybe trademark laws can be useful in some contexts (for example to prevent scams), but it remains to be demonstrated whether the utility they bring exceeds the costs associated with how badly written or applied they often are.

For example, in a lot of jurisdictions, not taking steps to protect one's trademark from infringement equates to abandoning the right to do so later, which is a compelling argument for taking action every time, as Tari Labs's co-founder Riccardo Spagni {{<newtabref href="https://nitter.lacontrevoie.fr/fluffypony/status/1636104416817192960" title="explained">}}. In other words, if you don't go to court over something that someone might consider a trademark infringement, you open the door to other abuses which may be far worse and actually lead to confusion and scams. And, still according to {{<newtabref href="https://nitter.lacontrevoie.fr/fluffypony/status/1636241835730300929" title="Spagni">}}, going to court was Tari Labs solution of last resort after proposing to Lightning Labs to find a new good, catchy name for their Taro protocol at Tari Labs's expense.

To put it in a nutshell, while I agree that all this is a real shame, I'm not sure Tari Labs should bear the blame. As I'm definitely not a lawyer, I'm not sure whether Tari Labs could have had taken other steps to avoid the litigation ; and as I'm not aware of the exact substance of the discussions between Tari Labs et Lightning Labs, I can't really say anything for sure. All I wanted to do with this section is highlight that the issue at hand here is not as simple as "evil Tari suing Lightning Labs over nonsense". Hopefully the situation evolves positively quickly and doesn't hinder to much on the development of the Taro protocol, whatever its future name might be.

### Pay Directly From Your Lightning Wallet In VIDA

VIDA's founder Lyle Pratt shared a {{<newtabref href="https://nitter.lacontrevoie.fr/lylepratt/status/1637189324612554758" title="sneak peek">}} of the integration of {{<newtabref href="https://webln.dev/#/" title="webln">}} into the platform. This would enable users to pay directly from an external wallet, instead of having to deposit funds into their account first.

{{<newtabref href="https://vida.live/" title="VIDA">}} is a platform where content producers of all kind can monetize their audience directly. For example, you can pay around $17 to jump on a 30-minutes call with {{<newtabref href="https://vida.live/jack" title="jack">}}, or 10 cents to send {{<newtabref href="https://vida.live/fanismichalakis" title="me">}} a message. On top of that, creators can also stream to their audience, with listeners streaming sats as they watch or interact[^2].

### Breez SDK Implemented Into Satimoto Amidst Bank Shut Down

Satimoto is an app for electric vehicle charging which allows you to pay for charging non-custodially with Lightning and respects your privacy. We already covered the news here when they {{<newtabref href="https://fanismichalakis.fr/posts/latest-strikes-13/#you-can-now-charge-your-ev-with-sats-in-europe" title="launched">}} in Europe, or when they started looking into the {{<newtabref href="https://fanismichalakis.fr/posts/latest-strikes25/#breez-sdk-in-the-wild" title="Breez SDK">}}. Last week they announced two things which, combined, are a bit of the essence of the period we're living in:
- first, they {{<newtabref href="https://nitter.lacontrevoie.fr/SatimotoApp/status/1636101745309802497" title="announced">}} that they finished integrating the Breez SDK into their app, which will probably make it easier for them to provide a good user experience while remaining non-custodial and KYC-free ;
- second, they {{<newtabref href="https://nitter.lacontrevoie.fr/SatimotoApp/status/1637777052777553921" title="posted">}} that the bank they were using was due to shut down in May[^3].

As non-custodial Lightning wallets and Lightning-enabled apps blossom and banks wilt, it seems like the world is closer than ever from getting struck by Lightning!

## Wallets & Tools

### LNBits

The LNBits team {{<newtabref href="https://nitter.lacontrevoie.fr/arcbtc/status/1635998858655178753" title="showcased">}} 3 new extensions last week, which can work together to enable even more sophisticated use cases.

One of them is the {{<newtabref href="https://github.com/lnbits/nostr-relay-extension" title="Nostr Relay">}} extension, which as the name suggests allows you to easily spin-up one or many nostr relays and configure them with a graphical user interface. You can for example decide that joining your relay would cost a few sats, or even charge users for storage on a per-megabyte basis.

Another one is the {{<newtabref href="https://github.com/lnbits/nostrclient" title="Nostr Client">}} extension, which is an always-on nostr client that can also serve as a proxy to which other clients can be connected. For example, you can connect the extension to a bunch of relays, and then connect your mobile nostr client to the extension's endpoint as if it was a relay: on the mobile app, you're only connected to one relay (the extension), but you're actually pulling and pushing data from and to a bunch of different relays through the extension's proxy, thus saving bandwidth. Another interesting use case of this extension is that you can connect other extensions to it in order to make them nostr-aware. This opens the way to many resilient, censorship-resistant use cases were any DNS-based communication could be held on nostr instead.

The third extension, called {{<newtabref href="https://github.com/lnbits/nostrmarket" title="Nostr Market">}}, is the merge between nostr and the Dragon Alley protocol we already mentioned back in {{<newtabref href="https://fanismichalakis.fr/posts/latest-strikes-18/#lnbits-new-market-extension" title="January">}}. The idea is simple: from the extension, a merchant can create new product offerings, which will be published to nostr using the merchant's key. Everyone can then see the products and buy them over nostr. Orders themselves are placed via encrypted nostr direct messages between customers and the merchant, which returns invoices via nostr as well. If the LNBits instance of the merchant is taken down, they can quickly create another one under the same identity (provided they were holding their private key in a safe place, which things such as the {{<newtabref href="https://lnbits.github.io/nostr-signing-device/installer/" title="Nostr Signing Device">}} are paving the way for). As Ben Arc {{<newtabref href="https://www.youtube.com/live/lqV0XkOlcCs?feature=share&t=775" title="puts it">}} (paraphrasing a bit): "nostr enables moveable [digital] market stalls".

LNBits also {{<newtabref href="https://stacker.news/items/152429" title="updated">}} their LNURL-Pay extension: you can now create a unique Lightning Address for every LNURL-Pay link that you create. Awesome!

### Easy Migration From BlueWallet To Alby

The Alby team wrote a {{<newtabref href="https://blog.getalby.com/bluewallet-alby-how-to-switch-lndhub/" title="guide">}} on how to migrate your funds from BlueWallet to an Alby account. As a reminder, BlueWallet will {{<newtabref href="https://fanismichalakis.fr/posts/latest-strikes25/#bluewallet-sunsetting-their-custodial-lightning-offering" title="shut down">}} their Lightning custodial offering on April 30th, so user are urged to send funds they might have there to another wallet.

Alby's blog post also details how to check whether one of the accounts you use in your Alby extension is a BlueWallet account, and explains how one can connect their BlueWallet app to Alby's LndHub backend. In other world, if your Alby browser extension is using a BlueWallet account as a backend, you should withdraw that money elsewhere. And, if you still want to use the Lightning wallet in BlueWallet, you can use an Alby account as the backend[^4]. That's because both Alby and BlueWallet use the same underlying open-source Lightning interface and accounting system called LndHub. Kinda cool.

## Spec & Implems

### The Great Description Debacle

Last week was once again the set for some heated[^5] discussions in the Lightning community, which were quickly settled. The heat initially came from an announced change coming into effect in Core Lightning that had adverse consequences for users of the LNURL protocol.

The modification in question concerned the description field in invoices, and was merged into the code since December 2022. However, Core Lightning can run with a `allow-deprecated-apis` option which defaults to true and gives users of Core Lightning a grace period during which certain changes in the behavior of Core Lightning do not take effect. The recent {{<newtabref href="https://fanismichalakis.fr/posts/latest-strikes26/#core-lightning-v2302" title="update">}} of Core Lightning brought the grace period for this change to an end, thus revealing potential problems that were ignored until then.

Let's dive into the actual issue and its consequences. A Lightning invoice can contain a short description (for example "thank you for the coffee") or (exclusive) a description hash, which is useful when the description of the payment is too big but we still want to commit to it. In that case, only the description hash is included in the invoice, and the long description itself is expected to be sent to the sender via another mechanism, per the Lightning specification (Bolt 11). The issue is that the same specification {{<newtabref href="https://github.com/lightning/bolts/blob/master/11-payment-encoding.md?plain=1#L215" title="states">}} just a few lines below that if the invoice contains a description hash, then it is the responsibility of the Lightning implementation to check that the hash does match with the actual description that was provided out-of-band.

See the problem yet? We have a specification that is both quite evasive on how a long description is supposed to be passed around, but states that the receiver (which crafts the invoice) {{<newtabref href="https://github.com/lightning/bolts/blob/master/11-payment-encoding.md?plain=1#L174" title="must">}} make it available to the sender, which in turn **must** ensure that the description and its hash match.

But what about LNURL? In LNURL-Pay, the wallet of the issuer of a payment starts by sending a query to the LNURL server. For example, when trying to pay to the Lightning Address {{<newtabref href="lightning:fanis@lnmarkets.com" title="fanis@lnmarkets.com">}}, my wallet will send a request to `https://lnmarkets.com/.well-known/lnurlp/fanis` and get a JSON in return. This JSON contains (among other things) a metadata string with things such as a short description and an image, which my wallet will display to me. The JSON also contains some parameters, such as the minimum and maximum amounts that I'm allowed to pay as the sender, and a callback endpoint. So my wallet shows me the metadata's image and description, and asks me how much I'd like to send within the boundaries set by the LNURL server. Once I've defined my amount and pressed "send", my wallet will send a request to the callback endpoint, asking for an invoice for the amount I just submitted. The LNURL server will then answer with such an invoice, which also contains a description hash: the hash of the metadata we've seen in the previous step.

What you'd expect at this point is for my wallet to pass the metadata to my Lightning node along wit invoice so that it can check that the description hash in the invoice matches the metadata. After all, this is what the Lightning specification requests. Yet, until last week, no Lightning implementation really bothered to check that the out-of-band description and its hash matched before paying an invoice, and thus when implementing LNURL-Pay many wallets didn't bother to pass the description to the underlying Lightning implementation along with the to-be-paid invoice so that the Lightning node could check they matched. Instead, wallets implementing LNURL-Pay checked the match between description hash and metadata at the app level, as the LNURL-Pay {{<newtabref href="https://github.com/lnurl/luds/blob/luds/06.md?plain=1#L108" title="specification">}} dictates. In other words, wallets perform this check themselves, and hence don't send the description to the Lightning node when paying the invoice.

Until last week, it worked. But Core Lightning's change meant that Core Lightning nodes would begin to check the description and its hash matched, in accordance with Bolt 11. When asked to pay an invoice containing a description hash but without being provided any actual description, the Lightning node would therefore refuse to pay. This broke many (most? all?) LNURL-Pay implementations. However, after some discussions on Twitter, the Core Lightning team decided to revert the change in {{<newtabref href="https://github.com/ElementsProject/lightning/releases/tag/v23.02.2" title="v23.02.2">}} which was published last week.

The question is now: what will the next steps be? As Rusty Russel {{<newtabref href="https://github.com/ElementsProject/lightning/pull/6092#issuecomment-1467043503" title="points out">}}, there's a good reason for the specification to state that the Lightning node must check concordance between a description and its hash. There are a lot of use cases where it is paramount for the node to ensure that it is indeed signing what it is supposed to, especially in contexts where HSM are involved. On the other hand, this would mean rewriting many LNURL implementations to pass the description down to the Lightning node. Another way would be to loosen the specification a bit and transform a few MUSTs into SHOULDs: Lightning nodes could sign without checking the description hash when operating in a "reckless" mode, while always checking it in normal operation. This would accommodate all use cases while causing the least pain, but requires everyone sitting around the table to agree on this (which might be a good idea if we want to prevent this mishap from happening again).

### Resizing Lightning Channels Offchain

John Law sent {{<newtabref href="https://lists.linuxfoundation.org/pipermail/lightning-dev/2023-March/003886.html" title="published">}} a proposal on the Lightning-Dev mailing list on how to resize Lightning channels off-chain using what they call "hierarchical channels".

One way to think of this proposal is as if channel factories and circular rebalancing had a child. The core idea is to have channels of channels, and route payments across the Lightning Network to dynamically resize regular channels that are "inside" a "mother channel" (called a "hierarchical channel").

As an example, consider 4 Lightning nodes A, B, C and D. A and B can work together to create digital signatures for a common entity denoted AB. Similarly, C and D can be coordinated inside an entity called CD. Individual nodes being able to work with one another to produce digital signatures means that AB and CD are able to "own" Bitcoin UTXOs. We can therefore create a channel between entities AB and CD by sending funds to a 2-of-2 multisignature output. From this output, we can create off-chain transactions (transactions that are not meant to be spent unless we wish to close the channel, called *commitment transactions* in the context of Lightning) that spend to primarly two outputs: one that is a 2-of-2 multisignature between A and B, and one that is a 2-of-2 multisignature between C and D. Those 2 outputs are hence Lightning channels themselves that are not directly backed by any on-chain UTXO, but rather 2 off-chain "virtual" UTXOs that only exist inside commitment transactions of the big channel between AB and CD. However, this channels are fully functional, and can be used to send payments just like any regular Lightning channel. Even more interesting, the "mother channel" between AB and CD can also be used to perform payments: the main difference with regular Lightning channels is that it requires updating the commitment transactions of fours nodes instead of two, and thus exchanging 6 signatures (some of which actually involve two nodes) where a regular channel only requires 2.

Among other things, Law describes how this setup can be used to resize Lightning channels entirely off-chain. To do so, all you need is a closed loop of channels that start and end at the same node. Consider again our example with nodes A, B, C and D. Let's add a fifth node E which is connected to D and A with a channel to each. We hence have multiples channels that can form a closed loop when combined in the right order: AB-CD (the channel between entities AB and CD), D-E and E-A. For the rest of the network, the channel AB-CD can be treated as any regular channel, and what we see hence looks like a regular circular rebalancing where A sends funds to itself along a cyclic route to displace liquidity. Locally, inside the AB-CD channel, entity AB pushes liquidity to entity CD, just like a regular node would push liquidity to the other side of a channel. Here however, entity AB and CD are channels, so the transfer from AB to CD means that the channel A-B decreases in size while the channel C-D increases. We have resized the two "sub-channels", and the funds went from A to D. Now, D forwards the payment to E, so they don't actually gain any fund (apart from potential fees), but the size of the channel between A and B decreased while the one between C and D increased. The sizes of all the channels that are backed by an actual on-chain UTXO stayed the same, but we resized the channels backed by off-chain UTXOs, without ever touching the chain.

*As you can see in this example, the capacity of channel A-B went from 500 to 400, while the capacity of channel C-D went from 200 to 300. Potential routing fees are ignored for simplicity.*

Of course, the current Lightning protocol doesn't allow the creation of such setups, but it is good food for thoughts nonetheless. Notably, one of the advantages of hierarchical channels compared to other methods such as channel factories is that you have access to the whole network liquidity for your resizing needs, whereas in channel factories you are constrained by the liquidity inside the factory you're a part of.

### LDK Roadmap

The Lightning Dev Kit (LDK) team {{<newtabref href="https://nitter.lacontrevoie.fr/lightningdevkit/status/1635392924463804417" title="shared">}} their roadmap for the next 12 months, and it's fair to say it's appealing! The roadmap includes:
- a ready to go mobile node implementation built with the LDK and the Bitcoin Dev Kit (BDK) for the on-chain component ;
- {{<newtabref href="https://fanismichalakis.fr/posts/latest-strikes-4/#asynchronous--offline-payments-in-eclair" title="async payments">}}, allowing users to pay each other while being offline ;
- {{<newtabref href="https://fanismichalakis.fr/posts/ptlcs/" title="PTLCs">}}, bringing more privacy to Lightning and improving the protocol in many ways ;
- {{<newtabref href="https://fanismichalakis.fr/posts/latest-strikes27/#splicing" title="Splicing">}}, for dynamic resizing of channels ;
- {{<newtabref href="https://fanismichalakis.fr/posts/anchor-outputs/" title="Anchor Outputs">}}, for safe fee-bumping of channel closing transactions
- a versioned storage service for encrypted cloud backup of channels state and the possibility to share a same node across multiple devices (the *versioned* part making sure that users don't shoot themselves in the foot with deprecated states).

That's definitely an appetizing roadmap, so we'll probably have our eyes on LDK in the coming months!

## CLosing Bit

C'est comme un puits sans fond qui s'écoule en lui-même\
Et m'entraîne à sa suite à travers le modem\
M'attire et me consume, me disperse à tout va,\
Fait de moi, malgré moi, un cyborg sans état.

---

Want to receive Latest Strikes straight to your inbox every week? Couldn't be easier: subscribe to {{<newtabref href="https://blog.lnmarkets.com" title="LN Markets Ghost blog">}} and you're all set (remember to confirm your subscription by clicking the link sent via email).

---

If you enjoyed this recap, you can show your appreciation by throwing a few coins to *fanis @ lnmarkets.com*, by scanning or clicking the QR code.

Thank you!

{{<figure align=center src="../../images/lnm_lnurl.png" link="lightning:fanis@lnmarkets.com">}}


[^1]: https://storage.courtlistener.com/recap/gov.uscourts.cand.404957/gov.uscourts.cand.404957.57.0.pdf

[^2]: While it can remind us of the way Podcasting2.0 works, a big difference here is that the creator chooses which rates to apply (for example, whether a stream is free of costs 10 cents per minute). In Podcasting2.0, everything is free by default and listeners can choose to tip a certain amount to the creator.

[^3]: An astute reader will have remarked that the bank thing actually happened this week, but I just couldn't let such a coincidence slip. Or is it really a coincidence?

[^4]: Of course, if BlueWallet updates its wallet to completely remove the ability to use a custodial account (even one that's not operated by them) this won't work anymore.

[^5]: Lightning people are very nice so it was more of a lukewarm discussion than a really heated debate, but that doesn't sell as much paper, does it?
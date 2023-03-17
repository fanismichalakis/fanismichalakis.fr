---
title: "Latest Strikes 19"
date: 2023-01-17T18:00:00+01:00
block: "772409"
cover:
    image: "../images/DALL·E 2023-01-17.min.png"
    alt: "A cubist and colorful representation of a mother breastfeeding a child."
    caption: "\"Motherbase\". Generated with DALL·E."
    relative: "false"
tags: ["bitcoin", "lightning"]
categories: ["strikes"]
draft: false
---

## Ecosystem

### Lightningcon Vietnam

The {{<newtabref href="https://lightningcon.org/" title="LightningCon Vietnam">}} conference will happen in March 23-24, and tickets are for sale! Prices will go {{<newtabref href="https://nitter.net/BitcoinBeachVN/status/1612984100163555328" title="up">}} on February 1st, so if you plan to attend, now might be a good time to book!

### Lightning Addresses In Bottlepay

Bottlepay users can now have their own {{<newtabref href="https://nitter.lacontrevoie.fr/bottlepay/status/1612880235514720256" title="Lightning Address">}}! Users can claim their `user@bottlepay.me` Lightning Address by updating the app and heading to the settings.

### Lightning Movie

Speaking of cool stuff, this {{<newtabref href="https://nitter.net/smolgrrr/status/1612345030961958913" title="one">}} litterally had me smiling at the UI. {{<newtabref href="https://lightning.movie" title="Lightning.Movie">}} lets you watch a film by paying a 1000 sats invoice: just scan the QR code that shows up when hovering on a movie's cover, pay the invoice and you're good to go! A very pleasant 0-click user experience (if the movie of your choice is on the first page).

Needless to say this website is probably illegal in most jurisdictions anyway, so I'm absolutely not inviting you to use it. Just wanted to share because I found it cool, both on the use case (micro-payment to buy a digital copy of a movie) and the delivery (very nice user interface!).

### Remember The Chicken? Now There're Cats

If you've been in Lightning for some time, you'll probably remember the good ol' chicken from {{<newtabref href="https://pollofeed.com/" title="PolloFeed">}}. It is a website where you can see a livestream of real chicken joyfulluy grazing somewhere in the world, and pay some sats to trigger the delivery of some food from an automatic dispenser. The project went down at some point, but is back online since September 2022, with a revamped look for even more fun!

Well, you can now {{<newtabref href="https://lightningcats.org/" title="feed">}} two magnificient cats (but there's a timer between two feedings, to ensure they don't grow fat). Feeding remote animals is probably still the best way to demonstrate the power of Lightning. People on {{<newtabref href="https://stacker.news/items/121710" title="StackerNews">}} seem to agree!

### Lightsats Tip Cards Are Here

In {{<newtabref href="../latest-strikes-17/#hand-out-lightning-tips-to-friends-family--strangers-if-you-want-to" title="Latest Strikes 17">}}, we mentionned two different ways of gifting Bitcoin on Lightning to friends, colleagues or family, as a way to get them their first bitcoins and show them how it works. For Christmas, Lightsats had rolled out a nice feature where you could print your tip (eg. the QR code leading to the gift's URL) on a gift card, to be able to place it beneath the Christmas tree. It is {{<newtabref href="https://stacker.news/items/120792" title="now">}} a permanent feature, with the ability to personalize your card simply by pasting the URL of an image.

On top of it being an intuitive way to hand out sats, this new physical gift card feature comes with an additionnal perk: because the recipient has a printed version of the claim URL, Lightsats doesn't need them to register to save their session anymore, as they will be able to reaccess it using the QR on the card.

### Instant Withdrawals In MinatoPay

Building easy to use self-custodial services on Lightning can be hard sometimes, and depending on the use case it might be a reasonable tradeoff to give up some custody in exchange of usability and easy onboarding - but only **temporarily**. Lightning offers great possibilities in terms of reducing the amount of time during which funds are at risk in the hands of a custodian, and we're seeing an increasing number of projects adding automatic/fast withdrawal features.

The latest is {{<newtabref href="https://minatopay.com/" title="MinatoPay">}}, a payment processor that lets you receive Lightning payments with ease, with the downside of being custodial. This tradeoff is now mitigated with the addition of the new {{<newtabref href="https://stacker.news/items/122437" title="instant withdrawals">}} feature, where users can withdraw funds as soon as they're received in their MinatoPay account, thanks to LNURL-Pay.

If I understand how this new feature works, it should in theory be possible to completely remove the custodial part of Minato for merchants who have access to a LNURL enabled wallet/node. It would work roughly like {{<newtabref href="https://lnproxy.org" title="lnproxy">}} or {{<newtabref href="../latest-strikes-16/#make-your-geyser-donations-flow-to-your-own-wallet" title="Geyser">}}:


1. Customer hits "Pay" on checkout page
2. Minato gets an invoice for the required amount + Minato fees from the merchants self-custodial wallet using LNURL-Pay
3. Minato crafts an invoice for the required amount and with the same payment hash as the invoice in step 2., and shows it to customer.
4. When customers pays invoice of step 3., Minato pays the initial invoice of step 2. in order to get the preimage, then can settle the customer-facing invoice (the one created in step 3.) using said preimage.

I asked if this would work in the comments of Minato's StackerNews announcement post. Let's see if it's doable!

## Wallets & Tools

### Motherbase Shut Down

Heads up to {{<newtabref href="https://sbw.app" title="Simple Bitcoin Wallet">}} users: Motherbase, the Lightning node that provided the {{<newtabref href="../what-are-hosted-channels/" title="hosted channels">}} by default in the app will be {{<newtabref href="https://nitter.lacontrevoie.fr/SimpleBtcWallet/status/1613698688844529667" title="shutting down">}} on Janurary 21st - 23rd. If you have a hosted channel there with funds on your side, withdraw them before this date.

### Blixt Update

The version 0.6.2 of Blixt is {{<newtabref href="https://nitter.net/BlixtWallet/status/1614654406297018368" title="out">}}! Among some bug fixes and added support for the Croatian language, a notable modification is that LND's strict channel graph pruning (where LND aggressively removes channel from its graph, and hence its database, when they seem to be unusable) is now disabled by default. This leads to a moderatly higher memory footprint for the app, but should improve pathfinding, as this (maybe a bit too aggressive) graph pruning seemed to cause routing failures.

### Torq v0.16.3

A new Torq {{<newtabref href="https://nitter.lacontrevoie.fr/LN_Capital/status/1613608029131243520" title="release">}} is available, with some nice stuff! You can for example add tags to channels or nodes, for example labelling them as "sink" (a node that tends to receive more than they send), "exchange", etc. This release comes with some preconfigured tags, but you can add your own to better match your node's environments and needs.

As always, get the full release notes {{<newtabref href="https://github.com/lncapital/torq/releases/tag/v0.16.6" title="here">}}.

### Alby v1.23.0

Alby v1.23.0 is {{<newtabref href="https://nitter.net/getAlby/status/1613240315699159068" title="out">}}, with some nice enhancements. Notably, the team has improved the mobile experience with Alby, making it easier than ever to use Lightning (and Nostr) in the browser, even on mobile devices!

Other notable {{<newtabref href="https://github.com/getAlby/lightning-browser-extension/releases/tag/v1.23.0" title="changes">}} include a new connector to access your {{<newtabref href="https://kollider.xyz" title="Kollider">}} account directly in Alby, BIP21's {{<newtabref href="https://bitcoinqr.dev" title="Unified QR">}} support (we already spoke about it when Zeus {{<newtabref href="../latest-strikes-10/#bip21-unified-qrs-coming-to-zeus" title="rolled it out">}}), as well as support for a new {{<newtabref href="../latest-strikes-16/#alby-extension-for-developers" title="API request">}} allowing websites to request the extension to create a new invoice (which greatly facilitates flows where the website wants to send you money).

### Lightning Firewall CircuitBreaker Now Has A Web UI

{{<newtabref href="https://github.com/lightningequipment/circuitbreaker" title="Circuit Breaker">}} is a "Lightning Firewall" that allows you to set the maximum number of in-flight HTLCs on a per channel basis. For example, you can set a high limit for the node of a friend, while keeping a lower limit for a new channel where you don't know yet if the peer is trustworthy. This helps mitigate DoS attacks (such as certain types of channel jamming), as well as the inconvenience that can be caused by other people probing your channel.

The tool just received an {{<newtabref href="https://nitter.lacontrevoie.fr/joostjgr/status/1612511153950711830" title="update">}} and now ships with a web user interface, allowing you to visualize what's going on in your channels in terms of HTLC traffic, as well as apply limits (per channel) if needed (for example, if you see a channel with an anormaly high number of failed HTLCs).

If you already have Docker on your machine, you can run a demo with litterally one command:

`docker run -p 9235:9235 ghcr.io/lightningequipment/circuitbreaker:latest --httplisten 0.0.0.0:9235 --stub`

Then head to http://127.0.0.1:9235/ to see the demo web interface with fake data.

### All Time Stats In Amboss

A {{<newtabref href="https://nitter.net/ambosstech/status/1612483411343716352" title="new">}} network-wide "All Time Metrics" statistics {{<newtabref href="https://amboss.space/stats" title="page">}} is available on Amboss. You can see the evolution of the total public capacity or the number of announced channels since the inception of the Lightning Network, and with data from three different sources ( {{<newtabref href="https://amboss.space" title="Amboss">}}, {{<newtabref href="https://bitcoinvisuals.com/" title="Bitcoin Visuals">}} and {{<newtabref href="https://mempool.space" title="Mempool">}}).

As you can see, Bitcoin Visuals seems to be experimenting some problems with their Lightning data. But it's funny to see that even Amboss and Mempool, which have quite similar numbers for total capacity, differ by almost 10% when it comes to the number of channels (probably because Mempool doesn't count a bunch of small channels that Amboss takes into account). Very cool tool and visualizer for the stats nerds!

## Spec & Implems

### Async Payments Proof-of-Payment

{{<newtabref href="../latest-strikes-4/#asynchronous--offline-payments-in-eclair" title="Async Payments">}} are currently one of the priorities in Lightning development, allowing recipients to receive payments while they're offline (kinda). Last week saw some discussions on the mailing list as to how proofs of payments could be implemented for async payments.

With standard Lightning invoices, each payment comes with its own payment hash, which is the hash of a secret (often called the *preimage*). When they receive the payment, the recipient reveals the preimage, which unlocks the funds and settles the payment. By showing the preimage, the sender can then "prove" that they sent the funds[^1].

In the context of async payments, the issue arises from the fact that the receiver is presumably offline, and thus incapable of creating a new invoice with a dedicated preimage. An option could be to let the receiver's LSP handle invoice creation, but that requires trusting said LSP. Another method would be to rely on payments to static identifiers, such as keysend or Atomic Multi Path payments (AMP)[^2].

In this context, PTLCs were once envisioned to be a convenient solution, but it appears that while PTLCs are useful for regular invoices proof of payments, they are of little help for recurring payments to the same identifier (for example the public key). Hence the {{<newtabref href="https://lists.linuxfoundation.org/pipermail/lightning-dev/2023-January/003820.html" title="message">}} sent on the mailing list by Valentine Wallace, asking for ideas.

Async payments are among the next great improvements toward Lightning usability. Their envisioned implementation relies on Trampoline Routing to handle the payment while the recipient is offline, and it seems Trampoline is being {{<newtabref href="https://nitter.lacontrevoie.fr/moneyball/status/1613277882029346819" title="prioritized">}} in LDK development (and is already here in Eclair). Neat!

### Staking Credentials Architecture

In November 2022, the search for a mitigation against channel jamming attacks saw the publication of a {{<newtabref href="../latest-strikes-10/#unjamming-channels" title="paper">}}, that in turn led Antoine Riard to {{<newtabref href="../latest-strikes-12/#more-on-channel-jamming" title="propose">}} a certificates-based mechanism, where the sender of a payment must attach certificates to their HTLC for each hop that their payment goes through ; certificates which would have been previously bought from each routing node involved in the route, providing a protection against channel jamming attacks, where an attacker can completely disrupt channels at no cost.

Last week, Riard {{<newtabref href="https://lists.linuxfoundation.org/pipermail/lightning-dev/2023-January/003822.html" title="announced">}} in the mailing list that he had started working on specifying the {{<newtabref href="https://github.com/ariard/lightning-rfc/blob/2022-11-reputation-credentials/60-staking-credentials-archi.md" title="architecture">}} of his proposition. There is nothing fundamentally new with regard to what we covered back in November, but the whole mechanism has been further abstracted in order to be useful for a wider range of applications than just channel jamming mitigation, and credential issuance and credential redemption phases are now more clearly separated.

The aforementioned document is quite clear and concise, so I'd invite the reader to read it in full, but here is a quick summary and example, in the context of a node sending a payment in Lightning, through an intermediate routing node. First, the sender must obtain some certificates for this routing node. It does so by generating blinded certificates and asking the routing node to sign them in exchange for an off-chain payment or a proof of utxo-ownership. Then, it performs the payment with certificates attached, and if there are enough certificates with respect to the routed amount, the routing node forwards the HTLC. The certificates are burnt, they will not be accepted again by the routing node, but if the payment goes well, the routing node may decide to give some certificates back to the sender, potentially more than the sender initially pledged.

### Closing Bit

Le signal a sonné - corne de brume!\
Des montagnes, le brouillard est tombé\
Epaisse nappe recouvrant les vallées\
D'un tissu blanc coton aux allures d'écume.

La table est mise - on entend le fracas\
Des géants qui s'asseyent pour leur premier repas.

---

Want to receive Latest Strikes straight to your inbox every week? Couldn't be easier: subscribe to {{<newtabref href="https://blog.lnmarkets.com" title="LN Markets Ghost blog">}} and you're all set (remember to confirm your subscription by clicking the link sent via email).

---

If you enjoyed this recap, you can show your appreciation by throwing a few coins to *fanis @ lnmarkets.com*, by scanning or clicking the QR code.

Thank you!

{{<figure align=center src="../../images/lnm_lnurl.png" link="lightning:fanis@lnmarkets.com">}}

[^1]: Well, actually, not really. The way HTLCs work, any node that took part in the payment (eg. the sender, the recipient and any intermediate routing node) knows the preimage once it is settled. So a routing node that didn't *sent* the funds but rather took part in *routing* them across the network can still show the preimage to the recipient: that doesn't mean they made the payment. If anything, revealing the preimage proves that the payment was settled and hence received, but it doesn't say anything as to who actually paid. Depending on your definition of a *proof of payment* and what your specific needs are, this might be enough.

[^2]: Things like LNURL-Pay wouldn't really work here, as they are just a proxy to an actual invoice and require the receiving node to be online to generate invoices on demand.
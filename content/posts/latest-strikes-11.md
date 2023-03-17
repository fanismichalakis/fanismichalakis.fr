---
title: "Latest Strikes 11"
date: 2022-11-21T12:00:00+01:00
block: "764126"
cover:
    image: "../images/DALL·E 2022-11-21.png"
    alt: "A Caspar David Friedrich style paiting of a landscape during a storm, with thunder, digital art"
    caption: "'A Caspar David Friedrich style paiting of a landscape during a storm, with thunder, digital art'. Generated with DALL·E."
    relative: "false"
tags: ["bitcoin", "lightning"]
categories: ["strikes"]
draft: false
---

## Ecosystem

### Grant

BitMEX {{<newtabref href="https://nitter.net/BitMEXResearch/status/1592093654814175232" title="renewed">}} Rene Pickhardt's grant, extending it for 6 additional months. Rene's work has been quite influential on how we envision liquidity on the Lightning Network, from a novel routing algorithm (Pickhardt Payment) to better models for liquidity management (why would the optimal state for all channels be a 50/50 repartition of funds?) and their consequences (for example, {{<newtabref href="../latest-strikes-3/#controling-flows-in-lightning-with-valves" title="flow control">}}).

### Adopting Bitcoin

That was quick! The Adopting Bitcoin team already {{<newtabref href="https://www.youtube.com/@adoptingbitcoin/videos" title="published">}} lots of replays (all of them?) from the conference. I don't know about you, but I know what I'll be doing of my free time this week. Replays are divided in 4 playlists, one for each stage and day: {{<newtabref href="https://www.youtube.com/watch?v=mECOICo9Aho&list=PLN2-dhqIYoj-VQ5b1NxJqlIlLgdxxdnW2" title="Bitfinex Stage Day 1">}}, {{<newtabref href="https://www.youtube.com/watch?v=Lzyv5heylDg&list=PLN2-dhqIYoj-lQMCggtrvbY5-y6Ak6O_W" title="Day 2">}}, {{<newtabref href="https://www.youtube.com/watch?v=5ckIrGXLTa0&list=PLN2-dhqIYoj-e3NwSpBRz9IodY6ZgDioa" title="Galoy Stage Day 1">}}, {{<newtabref href="https://www.youtube.com/watch?v=iJDgpoJSquI&list=PLN2-dhqIYoj_XZ4eZIbiHBWb_b9ipqk2x" title="Day 2">}}.

### Stats

The latest {{<newtabref href="https://nitter.lacontrevoie.fr/LN_Capital/status/1593761676578406400" title="LightningReport">}} by {{<newtabref href="https://ln.capital" title="LNCapital">}} further cements the observation that big nodes (eg. from exchanges, wallets, services and large businesses) are eating the network in terms of capacity. However, half of the network capacity is still contributed by routing nodes, while the rest of the nodes contribution to the overall capacity is down to around 10%.

Galoy {{<newtabref href="https://nitter.net/GaloyMoney/status/1593252426370277378" title="published">}} a cool {{<newtabref href="https://ab22-dashboard.vercel.app/" title="dashboard">}} showing how and where Bitcoin was spent over Lightning during Adopting Bitcoin.

### Lightning Communities

Blockstream {{<newtabref href="https://nitter.lacontrevoie.fr/Blockstream/status/1593351477246001152" title="lauched">}} Build on L2 ({{<newtabref href="https://www.buildonl2.com/" title="BOL2">}}), a community for engineers, designers and contributors who are working (or want to work) on Lightning. The aim of the initiative is to foster collaborations in all forms, from joined projects to hackathons to physical events and more!

On the same week, node management tool {{<newtabref href="https://bolt.observer/" title="BoltObserver">}} and studio {{<newtabref href="https://peakshift.com/" title="PeakShift">}} released the {{<newtabref href="https://www.lightning-landscape.net/projects" title="Lightning Landscape">}}, a searchable data platform for the Lightning ecosystem with more than 1400 projects and companies listed so far. Entries can be filtered by categories and tags, allowing you to quickly find the project you're looking for even if you don't know its name. I'd love to have features such as community tagging, or signaling features for projects allowing them to display that they're looking for talents or investors, for example. But the brand new platform is already, as it is, impressively complete and enjoyable to use.

### SatsCrap

The ScarceCity team launched a new marketplace called {{<newtabref href="https://satscrap.com/" title="SatsCrap">}} where people can sell and buy stuff directly with Bitcoin. A good way to stack more sats directly, or to get your hands on some great deals. There's no signup required, and SatsCrap pays itself with a 10% commission on sells. Regarding customer protection, sellers are required to pay a listing deposit equalling 10% of the item's price, which will be refunded if everything goes well. On the other side, buyers are required to video record the item's unboxing.

### Wallet of Satoshi <> BTC Map

{{<newtabref href="https://www.walletofsatoshi.com/" title="Wallet of Satoshi">}} (WoS) {{<newtabref href="https://nitter.net/BTCMapDotOrg/status/1592955842185289728" title="integrated">}} {{<newtabref href="https://btcmap.org" title="BTC Map">}} directly in their wallet app, which comes in handy with the new Pay Button merchants can display on their profile on the map.

WoS has also become a sponsor of the open source project.

## Wallets & Tools

### Routing Node Extracted Value (RNEV)

MidnightOrange {{<newtabref href="https://stacker.news/items/95480" title="announced">}} a tool called {{<newtabref href="https://github.com/dark-ln/preimage-stealer" title="preimage-stealer">}}, which does pretty much what its name says: it steals preimages.

Lightning currently uses {{<newtabref href="https://www.youtube.com/watch?v=-JC4mkq7H48" title="HTLCs">}} to trustlessly route payments accross the network. HTLCs are conditional payments, which the receiver can unlock to get the funds by revealing a secret, commonly called the *preimage*. When a payment goes through multiples nodes to reach its final destination, what happens behind the scenes is that every node sends an HTLC to the next. All of this HTLCs use the same secret preimage and are then resolved *en cascade* starting from the final node.

The reason all this HTLCs use the same preimage is because the hash of said preimage was placed in the payment's invoice by the receiver. There is hence one preimage per payment/invoice and, once a payment is settled, every node involved in this payment has learnt the corresponding preimage. It means that if someone later tries to fulfill the same payment (for example, using an invoice posted on Twitter), any node that was part of the previous payment as well doesn't need to forward the HTLC to the next, as they already know the preimage, and can instead claim the payment for themselves as if they were the final recipient.

The preimage-stealer tool does just that: when a new HTLC enters your node, it checks whether it already knows the corresponding preimage or not. If not, it forwards the HTLC as usual. Else, it stops forwarding and either steal the funds or just increment a counter of how many funds it could have stolen (that's the watch-only mode).

Preimage stealing isn't a new idea, and I'm honestly quite surpised there wasn't a tool to do that before. This kind of attack will be addresses when we switch from HTLCs to {{<newtabref href="../ptlcs/" title="PTLCs">}}, but in the meantime can be mitigated by avoiding to pay publicly posted invoices (which shouldn't exist in the first place, as it carries a privacy risk for the receiver).

### LiquidOps

{{<newtabref href="https://bolt.observer" title="BoltObserver">}} released the beta of a new tool called {{<newtabref href="https://nitter.lacontrevoie.fr/BoltObserver/status/1592895461995970560" title="LiquidOps">}} that helps you get valuable and actionnable insights for your node. The tool connects to your node either via read-only macaroons or an open source agent, and then sends data to BoltObserver, allowing you to display channel data in dashboards and, more importantly, automatically receive custom alerts when certain thresolds are hit (balance depleted on a given channel, new channel, unavailable node, etc.).

### New Alby Release

Alby {{<newtabref href="https://nitter.net/getAlby/status/1592584723981041664" title="published">}} their latest {{<newtabref href="https://github.com/getAlby/lightning-browser-extension/releases/tag/v1.19.0" title="release">}}, which notably brings Core Lightning support to the browser extension, thanks to the commando plugin. Alby now supports all major immplementations, and this new Core Lightning integration already shows its power with the ability to open dual-funded channels {{<newtabref href="https://nitter.lacontrevoie.fr/getAlby/status/1593266388528922626" title="in the browser">}}. Impressive!

## Closing Bit

La foudre en frappant éveille une étincelle\
Qui s'élève, aspirée, virevolte et explose\
En un millier de petits, petits fragments d'étoile\
Qui retombent sur la terre avec les giboulées.

---

If you enjoyed this recap, you can show your appreciation by throwing a few coins to *fanis @ lnmarkets.com*, by scanning or clicking the QR code.

Thank you!

{{<figure align=center src="../../images/lnm_lnurl.png" link="lightning:fanis@lnmarkets.com">}}
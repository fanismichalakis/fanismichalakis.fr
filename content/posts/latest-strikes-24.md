---
title: "Latest Strikes 24"
date: 2023-02-21T19:00:00+01:00
block: "777681"
cover:
    image: "../images/card_players_in_a_drawing_room.min.jpeg"
    alt: "The painting \"Card Players in a Drawing Room\"."
    caption: "\"Card Players in a Drawing Room\" by Pierre-Louis Dumesnil (date unknown). Part of The Metropolitan Museum of Art Open Access Collection. Bequest of Harry G. Sperling, 1971."
    relative: "false"
tags: ["bitcoin", "lightning"]
categories: ["strikes"]
draft: false
---

Howdy! The Lightning-Dev mailing list was quite busy last week, with very interesting discussions! But that's not it: there were also tons of releases, as well as very good news in the education and adoption fronts. Let's find out more together!

## Ecosystem

### Zion

Zion {{<newtabref href="https://www.zion.fyi/blog/zion-the-category-defining-web5-social-network-releases-v2-app-with-updated-white-paper-and-announces-6m-in-funding" title="announced">}} a six million dollars raise and launched the V2 of its "Web 5" app that aims to provide a decentralized social network building upon DIDs and leveraging Lightning for payments.

Seems like there are many alternative visions of what a p2p society and economy might look like on the technical side of things. Nostr clearly wins the award for simplicity with its minimalistic design, while other approaches such as the TBD and Zion's {{<newtabref href="https://developer.tbd.website/projects/web5/" title="Web5">}} or Keet and Synonym's {{<newtabref href="https://docs.holepunch.to/" title="Holepunch Ecosystem">}} aim at building more sophisticated notions of identity and data management. Definitely an interesting game to watch, where there might very well be more than one winner. And what's even more interesting is to see how they all use the same, interoperable network for payment!

### The lnbook is now free

The book {{<newtabref href="https://github.com/lnbook/lnbook" title="Mastering the Lightning Network">}}, co-authored by {{<newtabref href="https://nitter.lacontrevoie.fr/aantonop" title="Andreas Antonopoulos">}}, {{<newtabref href="https://nitter.lacontrevoie.fr/roasbeef" title="Olaoluwa Osuntokun">}} and {{<newtabref href="https://nitter.lacontrevoie.fr/renepickhardt" title="Rene Pickhardt">}} is {{<newtabref href="https://nitter.lacontrevoie.fr/renepickhardt/status/1625869869198544896" title="now">}} free! It was already available for free on GitHub for personal use, but it is now freed on the licensing side as well. This tremendous work is indeed placed under the Creative Commons CC BY-SA license, granting anyone the right to redistribute, reuse, remix the material, both for commercial and non-commercial ends. There are only three rules to be observed: the original authors must be credited, it must be clearly stated when changes have been made, and the result of this rework must be licensed under the same license.

This speaks to the great values of both the authors and the editor O'Reilly, and will probably spark a number of adaptations, as well as enabling the original content to be more widely distributed. Hats off!

### Paying You Bus Trip With Lightning?

Is paying for public transportation with Bitcoin now a thing in Sweden? According to this {{<newtabref href="https://nitter.lacontrevoie.fr/Stromens/status/1625457745628475392" title="report">}} by Oliver Koblížek, it was briefly the case. Oliver was indeed able to buy a bus ticket on the public transportation service web app using BlueWallet: got a real invoice, paid it, and got his ticket in exchange.

Oliver then {{<newtabref href="https://nitter.lacontrevoie.fr/Stromens/status/1625544948714962944" title="contacted">}} Swish (standard mobile payment system in Sweden) and the bus company to know more about this new feature. It sadly disappeared a few hours after, leading many to believe that it was just a new feature not meant to be announced yet that somehow found its way into production. Quite interesting still, especially in a country like Sweden where cash usage is {{<newtabref href="https://www.statista.com/statistics/674315/cash-usage-in-sweden-by-payment-size/" title="dropping">}} significantly year after year, to the point that it even prompted the World Economic Forum to {{<newtabref href="https://www.weforum.org/agenda/2018/11/sweden-cashless-society-is-no-longer-a-utopia/" title="call">}} for the introduction of a Swedish CBDC in 2018, to counter the private sector's extension in the realm of payment and ensure the State keeps the influential position in day-to-day payments that cash brings. In this context, Bitcoin and Lightning could very well pave the way for a third approach: an open monetary and payment network where both public and private entities can deliver their services.

### Strike Send API

Jack Mallers {{<newtabref href="https://nitter.lacontrevoie.fr/jackmallers/status/1625629528977469441" title="announced">}} that the Strike Sending API {{<newtabref href="https://docs.strike.me/walkthrough/sending-payments" title="documentation">}} is now public. This allows developers to build new apps where the user can send money from their Strike account, using Lightning rails to reach their recipient.

### Support For NIP57

We (quite extensively) talked about Zaps (also knows as NIP57) in a couple of the previous Latest Strikes. This new standard has since been {{<newtabref href="https://github.com/nostr-protocol/nips/blob/master/57.md" title="merged">}} to the nostr specification, and we're already seeing huge usage in the wild. Supporting nostr clients include Damus (on iOS and MacOS), Amethyst (on Android) and Iris (cross platform).

On the other side, Zaps require the LNURL server (which provides the Lightning Address to the user) to implement some additional logic, notably creating and publishing the "zap note" that indicates funds have been received ; as well as adding a few new fields that can be consumed by nostr clients. Many wallets and Lightning Addresses providers have already implemented support for Zaps, notably {{<newtabref href="https://stacker.news/items/136477" title="StackerNews">}}, {{<newtabref href="https://nitter.lacontrevoie.fr/lylepratt/status/1625616337429995524" title="Vida">}}, {{<newtabref href="https://nitter.lacontrevoie.fr/nicolasburtey/status/1626971982339182594" title="Bitcoin Beach Wallet">}} (which also wins the "best meme" award), {{<newtabref href="https://nitter.lacontrevoie.fr/callebtc/status/1626244031981277184" title="LightningTipBot">}} and Wallet of Satoshi.

## Wallets & Tools

### Zeus Update & Point Of Sale Documentation

The beta version of Zeus next release is {{<newtabref href="https://nitter.lacontrevoie.fr/ZeusLN/status/1625508707856486402" title="available">}} for testing! Notable changes include the display of pending and closed channels (as opposed to displaying only currently opened channels, which is the current behaviour), as well as a timer for on-going force closes which shows approximately when the timelock will expire. On the user experience side, it is now possible to import QR code images from the gallery (very useful for example when trying to pay an invoice that someone sent you a picture of) and to login using biometrics.

Following the {{<newtabref href="https://fanismichalakis.fr/posts/latest-strikes-21/#more-lightning-payments-in-brick-and-mortar-businesses" title="release">}} of the Point Of Sale mode in Zeus compatible with Square POS devices (and only them at the moment), the Zeus team also published {{<newtabref href="https://docs.zeusln.app/pos/setup/" title="documentation">}} detailing how to set it up.

### Accounts in Lightning Terminal

A new alpha {{<newtabref href="https://github.com/lightninglabs/lightning-terminal/releases/tag/v0.8.6-alpha" title="release">}} of Lightning Terminal was published last week, that brings custodial accounts and finer granularity when setting up Lightning Node Connect authorizations from the graphical interface.

*Accounts* are a way to give access to a portion of your node's funds to someone else (for example a friend) without them being able to access anything besides what you grant them access to. Each account has its own macaroon and spending rules (for example spending limits or an expiration date). Like other accounting systems built on top of Lightning nodes (such as LNBits or LndHub), there is no certainty for the users of such custodial accounts that the sum of all accounts is below or equals the total available in the node. Account users are hence engaged in a trust relationship with the account issuer.

Such accounts, however, can cover a variety of use cases where trust is acceptable: sending a few bucks to a {{<newtabref href="https://nitter.lacontrevoie.fr/roasbeef/status/1626720335302377472" title="friend">}} who doesn't have their own Lightning wallet yet ; or making some money available for the kids to shop on their own during a specific afternoon (taking advantage of the expiration and spending limits features).

### Support For Core Lightning In BoltObserver

BoltObserver {{<newtabref href="https://nitter.lacontrevoie.fr/BoltObserver/status/1625525523534299140" title="launched">}} support for Core Lightning in their node and liquidity management {{<newtabref href="https://fanismichalakis.fr/posts/latest-strikes-11/#liquidops" title="offering">}}. Very cool to see a second implementation supported, especially since Core Lightning's "market share" as a Lightning implementation seem to have considerably grown in the last year or so.

### BTCPay Server Releases

The BTCPay team got busy in the last two weeks. We covered the release of {{<newtabref href="https://github.com/btcpayserver/btcpayserver/releases/tag/v1.7.6" title="v1.7.6">}} in the last issue of Latest Strikes, but we're now at {{<newtabref href="https://github.com/btcpayserver/btcpayserver/releases/tag/v1.7.12" title="v1.7.12">}}!

Among all the fixes and improvements, I found two changes particularly worth mentioning:
- a {{<newtabref href="https://github.com/btcpayserver/btcpayserver/blob/v1.7.8/docs/db-migration.md" title="migration">}} path from SQLite and MySql to Postgres. BTCPay historically supported this three databases, but maintaining support for them all proved to be "very challenging". Therefore, while SQLite and MySql will still work in the coming years, the team won't be providing support nor fix bugs in them, apart from migration to Postgres for impacted instances ;
- more fixes to cross-site scripting vulnerabilities (which the vulnerabilities mentioned in v1.7.6 were also about).

### Other Releases

Alby {{<newtabref href="https://github.com/getAlby/lightning-browser-extension/releases/tag/v1.27.0" title="v1.27.0">}} and Blixt {{<newtabref href="https://github.com/hsjoberg/blixt-wallet/releases/tag/v0.6.4" title="v0.6.4">}} were published last week!

## Spec & Implems

### Local Reputation to Mitigate Slow Jamming

Clara Shikhelman and Carla Kirk-Cohen {{<newtabref href="https://lists.linuxfoundation.org/pipermail/lightning-dev/2023-February/003857.html" title="published">}} an updated mechanism to prevent *slow* channel jamming attacks (where the jamming transaction takes a long time to resolve) using a local reputation score.

As a reminder, channel jamming attacks consist in an attacker taking up most of a channel's liquidity by submitting fake payments, for free. Two categories can be distinguished: *quick* jamming where the attacker's payments fail quickly but are resent every few seconds ; and *slow* jamming where they take hours to expire and fail. We already covered mitigation proposition in two previous issues of Latest Strikes ({{<newtabref href="https://fanismichalakis.fr/posts/latest-strikes-10/#unjamming-channels" title="here">}} and {{<newtabref href="https://fanismichalakis.fr/posts/latest-strikes-12/#more-on-channel-jamming" title="here">}}), but the main idea is that *quick* jamming can be mitigated with unconditional, upfront fees ; while *slow* jamming would be addressed with a reputation system.

The proposition put forward last week deals with the particular design this reputation system could have, and how reputation could be computed. As we've seen before, due to the very nature of Lightning, a local reputation system where each node maintains its own reputation score for other nodes makes the most sense. Here:
- each node gives a binary score (0 or 1) to each of its channel partners. This score starts at 0, and becomes 1 for "good peers", e.g. peers which lately paid more fees than the damage they could inflict now[^1] ;
- when a channel partner forwards a payment to my node, they can attach a message signalling whether they endorse this payment or not. If the endorsing peer has a reputation of 1, the payment can use the full liquidity available in the channel ; else, it can only use part of the available liquidity, and will hence be rejected if it requires forwarding more than the portion it is allowed to use.

Thanks to the endorsement signal passed between nodes, locally issued reputation scores can "travel" along the chain of a payment (for example, a forwarding node could enforce a payment only if it comes from a peer with a good reputation). When everything is fine, every payment can go through normally, even if they don't have access to the full liquidity of a channel (but, say, only to half of it). When a channel is under attack, only peers that established themselves a good reputation can still use it, which allows the node to keep most of its routing activity and revenue (since the good reputation itself was awarded based on the revenue this peer brought in the past).

One of the most apparent downsides of only devolving half of the channel available liquidity to low reputation peers is that it will probably make pathfinding, an already non-trivial task, even more difficult, as the sender of a payment would have to take into account that not only the liquidity could be on the other side of the channel, but it could also be unavailable because of low-reputation peers. On the other hand, payment paths going through high-reputation peers will have access to more liquidity, hence fail more rarely, and therefore be preferred in future pathfindings, thus provide more revenue which benefits their reputation score, and so on. This of course depends on a lot of parameters (such as channel capacity, payment sizes, as well as the sizes of the slots the channel is compartmented into and the exact configuration of pathfinding algorithms), but this could in my opinion lead to less variance in route selection, where as senders tend to favour more and more the same nodes, it digs an inescapable rut against which other routing nodes can't really compete, even with lower fees.

Nonetheless, it is crucial to find good countermeasures against channel jamming if we expect Lightning to be censorship resistant and to withstand attacks of all kinds. Good design is hard, and we will probably need to fine tune a lot of things (pathfinding algorithms, reputation systems, etc.) to reach our goal.

### Highly Available Lightning Channels

There were also very interesting {{<newtabref href="https://lists.linuxfoundation.org/pipermail/lightning-dev/2023-February/003842.html" title="discussions">}} on the mailing list regarding a related topic, where Joost Jager proposed adding the option for nodes to signal "high availability" for each of their channels, in the same way that they currently advertise their routing fees (e.g. using the `channel_update` messages). This data would be gathered by nodes and used in pathfinding algorithms alongside other data such as fees. When looking for a route, a sending node could decide to favour a channel signalling high availability but, should the payment fail, it would more heavily favour other channels (or even nodes) in the future. The discussion is quite dense and touches several sensitive points in the development on Lightning, such as arbitraging between payment reliability and centralization pressures.

As any summary, what follows probably misses some of the nuances of the debate, but here a few key elements that were put forth by participants:
- we lack a clear definition of "high availability", as it could mean different things in different sending contexts. Someone paying for its coffee would require very quick settlement, while someone sending money back to their country for remittance would favour cheaper fees, even it means trying a few routes to find one that works. Moreover, and due to the same lack of definition, having nodes define on their own if their channel is "high available" or not could lead to a quite *noisy* signal which wouldn't help sending nodes that much ;
- under some definitions of "high availability", notably the intuitive one of a high speed, very reliable channel, one could fear that it would incentivize routing nodes to perform just-in-time 0-conf splice-ins, as a way to adapt their channel's size on the go. This would enable both high availability and very efficient capital management. However, it comes at the cost of turning Lightning into a credit-based network, which is something we should probably avoid (or at least try to minimize, e.g. not incentivize through design decisions) ;
- reputation systems are notoriously hard to get write, and it seems quite difficult to build one that actually works while not being easily gameable. In this regard, I'd tend to think that a very local reputation system, such as the one put forth by Shikhelman and Kirk-Cohen in the context of channel jamming, could arguably work because data is by definition as accurate and frequently polled as it gets.

In the end, one way to look at Jager's proposal would be that:
1. Nodes can advertise "high availability" for some channels.
2. If I'm in a hurry, I might as a sender decide to use a "highly available" channel, even if it comes with a higher fee.

A specific situation where this comes in handy is if I'm trying to pay a node sitting in a remote area of the Lightning Network for which I don't have much data myself, because I've not done any payment there yet. The "high availability" signal just provides me with some additional information I can plug into my pathfinding algorithm to try to find the best route as possible in as few trials as possible.

### Closing Bit

Tout sonne comme un départ !\
Et ton oeil fatigué de tout voir sans rien croire\
S'habituera bientôt à ne plus regarder\
Que le morne spectacle qu'on donne sans le brader.

Mon âme à moi espère\
Et aspire à plus grand !\
Elle engloberait bien, avec le firmament\
La promesse qui vient, de loin, dessus le vent\

Et qu'on entend venir\
De loin en loin, écho\
Murmurée par des coeurs\
Qu'on sait pareils au nôtre.

---

Want to receive Latest Strikes straight to your inbox every week? Couldn't be easier: subscribe to {{<newtabref href="https://blog.lnmarkets.com" title="LN Markets Ghost blog">}} and you're all set (remember to confirm your subscription by clicking the link sent via email).

---

If you enjoyed this recap, you can show your appreciation by throwing a few coins to *fanis @ lnmarkets.com*, by scanning or clicking the QR code.

Thank you!

{{<figure align=center src="../../images/lnm_lnurl.png" link="lightning:fanis@lnmarkets.com">}}

[^1]: the calculation takes into account the maximum time `S` a HTLC can remain unresolved in one of my node's channels, and the routing revenue `M` I'm expecting in this period `S`, based on past performances. I would assign a channel partner a good reputation score if the revenue accrued by forwarding their payments over 10 times the aforementioned period `S` is equals `M`. This is quite similar to attributing a good reputation to a peer if they contributed at least 10% of my routing revenue over the last period of time, but with the subtle twist that we measure the income they provided over a larger period of time, thus favouring long term relationships with reliable peers in our reputation score.

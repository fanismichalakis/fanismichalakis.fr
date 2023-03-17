---
title: "Latest Strikes 18"
date: 2023-01-10T18:30:00+01:00
block: "771310"
cover:
    image: "../images/dancing_bolt.min.png"
    alt: "A synthwave city during a stormy night."
    caption: "\"Dancing Bolt\". Generated with DALL·E."
    relative: "false"
tags: ["bitcoin", "lightning"]
categories: ["strikes"]
draft: false
---

Last week was *electric*, with some fascinating discussions around inbound fees in Lightning, some cool releases and a new promising LNBits extension. Can you stand the voltage?

## Ecosystem

### Alby Pays Peertube Bounty

Alby {{<newtabref href="https://nitter.net/getAlby/status/1612104273390669825" title="paid">}} the 400,000 sats bounty (funded by German podcast and community {{<newtabref href="https://einundzwanzig.space/" title="Einundzwanzig">}} and an anonymous donor) that was on air for anyone creating a PeerTube plugin allowing viewers to tip content creators.

This new {{<newtabref href="https://github.com/dhk2/peertube-plugin-lightning" title="plugin">}} let's you send a one-time payment or stream sats by the minute, straight to the creator's Lightning Address, with the click of a button[^1]. Neat!

### Emeralize

Remember {{<newtabref href="../latest-strikes-14/#emeralize" title="Emeralize">}}? It's a new online learning platform, using Bitcoin and Lightning as a payment rail to make courses more widely accessible and easier to monetize, and it just went {{<newtabref href="https://nitter.lacontrevoie.fr/emeralizeapp/status/1610335201225506817" title="live">}}. We are of course still quite early, but there are already two courses available (one free by Zebedee, the other partly paid, by pleblab). For every course, it is possible to tip the creator (or even several creators thanks to {{<newtabref href="https://nitter.lacontrevoie.fr/emeralizeapp/status/1611587445702942720" title="payment splitting">}}) to support their work.

To put it in a nutshell, it's Udemy meeting the Value 4 Value model. And sats could even flow the other way, which could be useful to incentivize learners to go to the end of things.

### Fountain Release

Speaking of Value 4 Value, one of the very cool things (in my opinion) that this new model enables is some form of curation signal, where instead of sending likes and favs, users actually send sats. By tracking where sats flow, one may have a better idea of which content is valuable (the signal), and which might not be that interesting after all (the noise). A good example of that is {{<newtabref href="https://stacker.news/r/FanisMichalakis" title="StackerNews">}} (referral link), where upvotes are actually sats.

But you don't necessarily care about the opinion (and curation) of everyone. Money doesn't mean everything and if a rich douch really likes the weird content of a bald human trafficker and throw sats at it, it doesn't necessarily mean that you'll like this content too. In other words, what would be really useful for content curation would be to be able to see where your friends and the people you follow throw their sats at. Enters the latest Fountain {{<newtabref href="https://fountainpodcasts.substack.com/p/0-6-0" title="release">}}.

This new version of the podcasting 2.0 app comes with a lot of things, but what really caught my eye in this new feature called "Activity Feed". It allows you to see boosts, comments and likes that the people you follow left on podcasts, as well as the clips they produced.

Among the other things packed in this release, Fountain also changed their Lightning provider (for, I assume, Zebedee), so you'll need to upgrade to v0.6.0 to be able to interact with the Lightning part of the app (eg. deposit, withdraw, earn and tip).

## Wallets & Tools

### Zeus Release

Zeus v0.7.1 is now {{<newtabref href="https://nitter.lacontrevoie.fr/ZeusLN/status/1610636469227638784" title="available">}}, with a few notable changes:
- when sending a Lighting payment, users can now specify the maximum fee they're ready to pay as a percentage of the paid amount (or they can still input an absolute amount that the fee should not exceed, as was previously possible),
- it's now possible to display your node's nickname in the keypad and balance views, which is quite useful if you use Zeus to connect to several different nodes ; or if you connect to one node through various methods (for example, Tor and Tailscale for Umbrel users),
- Zeus now supports {{<newtabref href="https://github.com/lnurl/luds/blob/luds/17.md" title="LUD17">}}, which is a breaking change in the LNURL specification, with the introduction of new protocol prefixes (`lnurp://`, `lnurlw://`, `keyauth://`, etc.) instead of the `lightning:` prefix that is currently in use, as well as the dropping of bech32 encoding. Because it is a breaking change, this new specification isn't considered final yet, and won't be until all implementing wallets agree to consider it as such.

### LNURL-Auth Support In Wallet Of Satoshi

Speaking of LNURL, Wallet of Satoshi just {{<newtabref href="https://nitter.lacontrevoie.fr/walletofsatoshi/status/1611254595078230016" title="announced">}} the support of LNURL-Auth in their wallet app. It's not available yet, but it's definetely interesting to see a custodial wallet implement this kind of solutions.

### LNBits New Market Extension

A new LNBits extension {{<newtabref href="https://stacker.news/items/117788" title="dropped">}}! Called "Market", it allows you to create your own store and sell products throughout the world, either via your own instance or through someone else's one. The process to set up a store is quite easy: you just need to enable the extension in your LNBits wallet, and then you can define shipping zones (each with its own customizable shipping fee), stalls and products. Once you have at least one shipping zone, one stall and one product, you can create and publish your first marketplace, with one or several stalls, and for each stall one or several products. See my {{<newtabref href="https://legend.lnbits.com/market/market/VhEUcp9JeFfNwHjqprQM69" title="demo marketplace">}} to get an idea of what it looks like.

Cherry on top, Market will soon use nostr, with the merchant, market and buyer all having keys, and the data being sent through nostr relays. We're still early but this paves the way for a quite resilient and distributed archipelago of markets of various sizes that can't really be shut down as long as the seller is able to run a LNBits instance and access nostr relays.

### Ride The Lightning Hotfix

In Latest Strikes 16, I {{<newtabref href="../latest-strikes-16/#other-releases-lndhub-go-btcpay-server--ride-the-lightning" title="covered">}} the version 0.13.3 of Ride the Lightning. The software just received a {{<newtabref href="https://github.com/Ride-The-Lightning/RTL/releases/tag/v0.13.4" title="hotfix">}} to address an issue with 2FA.

## Specs & Implems

### New LND Doc

Lightning Labs' documentation {{<newtabref href="https://docs.lightning.engineering/" title="website">}} got a nice {{<newtabref href="https://nitter.lacontrevoie.fr/positiveblue2/status/1611035430949879816" title="update">}}! You can get an overview of how Lightning works, as well as the documentation of all Lightning Labs products, in one well-ordered place. Very nice!

### Discussions Around Inbound Fees

Last week we saw some (heated) discussions around the topic of inbound fees (for example, {{<newtabref href="https://nitter.net/TheBlueMatt/status/1611925676344619010" title="here">}} and {{<newtabref href="https://nitter.lacontrevoie.fr/roasbeef/status/1612318798446743553" title="here">}}).

When you send money on Lightning to someone to which you're not directly connected with a channel, your payment must go through other people's channels in order to reach its final destination. To do so, you effectively move funds around in these channels, from one side of each channel to the other. Routing your payment across the network hence requires other people to
- have liquidity ready in the right place for you to take advantage of,
- from time to time, maybe *rebalance* or close their channels as the current repartition in the channel, which is a consequence of previous payments going through, isn't necessarily exploitable anymore for routing payments, given the network topology around the channel.

Rebalancing or closing channels has a cost (in terms of fees paid, either on-chain or to other Lightning nodes), while the simple action of making funds available in a channel also incurs an *opportunity* cost (the node operator cannot use those coins elsewhere while they're in the channel). For this reason, when a payment goes through a channel, it is sensible that the two nodes sharing the channel get some compensation. However, right now, in a given channel, only the peer that moves liquidity from their side of the channel to the other is compensated. Of course, nobody routes payment for free, and the peer that is on the other side will still move the liquidity on their side in the next channel on the route, and charge sats there. Hurray, everybody gets paid!

Yet, it could be useful for various reasons to be able to set fees both as the node sending liquidity to the other side of the channel (outbound fees, the ones currently in place) as well as as the node receiving liquidity from the other side (inbound fees, the ones discussed here). This would for example allow node operators to shape the incoming flow to their node by applying different inbound fees on different channels.

There are primarily two ways of doing that[^2]:
- adding a new dedicated `inbound_fee` field in the messages that node regularly exchange, where they announce their fees to the rest of the network,
- having each node ask their peer to include their current inbound fee in the `outbound_fee` they announce to the network.

The reason for the heat last week is that Lightning Labs decided to go for the first version in LND, while there still seems to be some discussions in the broader specification process around which solution is best. Indeed, when one compares the two propositions side by side, there are a number of areas where they differ sensibly:

| Dedicated Field | Peer-based |
| -------- | -------- |
| Uses a new field in `channel_update` messages to advertise the inbound fee that must be paid by the sender. | As a node, ask my peer to incorparate the inbound fee I want into their advertized outbound fee, but then pass the sats to me instead of keeping them. |
| Kind of backward-compatible: the inbound fee must be negative (eg. an inbound discount), so that nodes that are not aware of this new feature can still route their payments through my node (they will just overpay in fees in comparison to up-to-date nodes that know there's a discount). The inbound discount can be compensated by setting higher outbound fees, so that the total fee is still positive. | Backward-compatible, as it doesn't require anything new to the network level: it's only a matter of peers agreeing one to one on the fees share. |
| Each node can independently announce their inbound fees. | Rely on peers to announce and enforce one's inbound fees (but 1. a node can still close channel if peer misbehave, 2. it isn't necessarily in the best interest of a peer to misbehave).
| Would not really be possible to set positive inbound fees from the get go. | Would be possible to set positive and (marginally) negative inbound fees from the get go.|

It is important to note that, from what I read, LND will first ship a version where the inbound fee must be negative, thus making this update backward-compatible. Legacy nodes have an incentive to upgrade in order to understand the new `inbound_fee` field and be able to benefit from the discount offered. If this catches on, and inbound fees do provide some utility in terms of flow control, when a sufficient part of the network supports inbound fees, it might then be possible to do positive inbound fees as well.

From what I understand, this is mostly a first step to try the idea of inbound fees in the wild and gather feedbacks ; and LND going for one solutions doesn't really prevent other implementations to explore the other one (but I might be missing something here).

It is also worth noting that on top of discussions around which implementation of inbound fees to use, there is still some disagreement among the community on whether inbound fees altogether are beneficial to the network. Some routing node operators are quite vocal on why this feature would help them manage their liquidity more efficiently, while some developers (see Rusty's {{<newtabref href="https://nitter.net/rusty_twit/status/1611932190388150272" title="tweet">}} or Thomas Huet's {{<newtabref href="https://lists.linuxfoundation.org/pipermail/lightning-dev/2022-July/003647.html" title="message">}} on the mailing list) and {{<newtabref href="https://nitter.lacontrevoie.fr/renepickhardt/status/1612004642593857539" title="researchers">}} seem doubtful on whether inbound fees would be useful at all.

In any case, this is really a fascinating topic, which we'll probably revisit in the next issue of Latest Strikes, as things mature.

Additional Ressources:
- this great {{<newtabref href="https://nitter.net/WitDeJesse/status/1612018040626896897" title="Twitter thread">}} by Jesse de Wit,
- the bLIPS {{<newtabref href="https://github.com/lightning/blips/pull/18" title="pull request">}} for the first solution, and this {{<newtabref href="https://github.com/lightning/blips/pull/22" title="one">}} for the other,
- the BOLTs {{<newtabref href="https://github.com/lightning/bolts/issues/835" title="pull request">}},
- the LND {{<newtabref href="https://github.com/lightningnetwork/lnd/pull/6703" title="pull request">}}.

## Closing Bit

La nuit n'en finissait plus d'avancer\
Le train s'y engouffra.\
Soudain le monde ne fut plus que ténèbres\
Et les ombres n'existaient plus.

---

Want to receive Latest Strikes straight to your inbox every week? Couldn't be easier: subscribe to {{<newtabref href="https://blog.lnmarkets.com" title="LN Markets Ghost blog">}} and you're all set (remember to confirm your subscription by clicking the link sent via email).

---

If you enjoyed this recap, you can show your appreciation by throwing a few coins to *fanis @ lnmarkets.com*, by scanning or clicking the QR code.

Thank you!

{{<figure align=center src="../../images/lnm_lnurl.png" link="lightning:fanis@lnmarkets.com">}}

[^1]: For the best experience, it is recommended to use a webln compatible wallet such as Alby. Else, it will be required to scan a QR code every time a payment is to be sent.

[^2]: At least, there were two ways primarily discussed last week.
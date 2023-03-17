---
title: "Latest Strikes 10 - Nov 13th"
date: 2022-11-14T16:00:00+01:00
block: "763155"
cover:
    image: "../images/DALL·E 2022-11-14.png"
    alt: "A portrait of a donkey in the style of the Mona Lisa painting"
    caption: "'A portrait of a donkey in the style of the Mona Lisa painting'. Generated with DALL·E."
    relative: "false"
tags: ["bitcoin", "lightning"]
categories: ["strikes"]
draft: false
---

## Ecosystem

### Automatic Withdrawals in LN Markets

{{<newtabref href="https://lnmarkets.com" title="LN Markets">}} released a new {{<newtabref href="https://twitter.com/LNMarkets/status/1590687798226751489" title="feature">}} called "Automatic Withdrawal". It leverages Lightning Addresses to automatically send the proceeds of a trade to the user's own wallet when some trading events (takeprofit, stoploss or option exercise) are triggered. On top of instant deposits and withdrawals, this helps users make sure not to leave their funds on the platform any longer than the trade itself.

### Zero Fee Post Mortem

lightningnetwork+ {{<newtabref href="https://lightningnetwork.plus/posts/335" title="interviewed">}} now {{<newtabref href="../latest-strikes-8/#zero-fee-routing-shuts-down-operations" title="retired">}} Zero Fee Routing regarding his experience as one of the biggest node in the network. I recommend reading the whole piece, but if there was only one advice to keep, I'd say it's this one:

> It's crucial to be aware of the cost for rebalancing, otherwise you're just subsidizing other people's routing.

I learned this costly lesson myself while {{<newtabref href="https://www.citadel21.com/lightning-chronicles" title="running a node">}} with a bunch of friends. If you don't set your fees with your rebalancing cost in mind, you'll end up being used by others to rebalance their own channels for cheap.

## Wallets & Tools

### Mutiny Web

Remember {{<newtabref href="../latest-strikes-1/#mutiny" title="Mutiny">}}? The team is working on a web version of the wallet, as part of BoltFun's {{<newtabref href="https://makers.bolt.fun/tournaments/1/overview" title="LegendsOfLightning tournament">}}. The end goal is to be able to run a privacy preserving Lightning wallet directly in the browser, which isn't the easiest thing to do!

Just like the original Mutiny wallet, the idea is to spin up a new child node for every payment, hence never reusing the same "identity" for two different payments. The web version still uses LDK to try to achieve that, but must also work around browser limitations at the same time. Currently, the {{<newtabref href="https://reckless.mutinywallet.com/tests" title="demo">}} is able to create a new node, perform on-chain receive and send (using BDK), and connect to remote peers through a websocket proxy.

Feel free to follow their journey on their BoltFun {{<newtabref href="https://makers.bolt.fun/project/mutiny" title="profile">}}!

### First Mainnet Vortex Coinjoin

Speaking of Lightning privacy, {{<newtabref href="https://twitter.com/benthecarman" title="Ben Carman">}} (who is also part of the Mutiny team) and {{<newtabref href="https://twitter.com/deregs_" title="Dereg">}} performed the {{<newtabref href="https://twitter.com/benthecarman/status/1590886577940889600" title="first mainnet 'Vortex CoinJoin'">}}, opening new Lightning channels through a Taproot-enabled CoinJoin.

{{<newtabref href="https://lnvortex.com/docs/ProtocolDocumentation" title="Vortex">}} builds upon ZeroLink, with slight modifications to accomodate for the specific needs of Lightning (such as the 10 minutes window to broadcast the channel funding transaction after negociating the channel details with one's peer).

The Lightning-related considerations mean it's probably easier to disrupt Vortex coinjoins than regular ones, so anti-DoS rules will have to be fine-tuned in this regard, and this first example of a mainnet Vortex Coinjoin doesn't actually provide much {{<newtabref href="https://kycp.org/#/5027541d328c2bab61e12c0db6df87f8a9f16dc10084042e4f4c962bdcbeb6fa" title="entropy">}}, but it's a good step in the right direction. Looking forward!

### BIP21 Unified QRs Coming To Zeus

{{<newtabref href="https://bitcoinqr.dev/" title="BIP21 Unified QR Codes">}} are {{<newtabref href="https://twitter.com/evankaloudis/status/1590575278287253504" title="coming">}} to Zeus! Such payment codes contain both an on-chain address and a Lightning invoice, allowing the sending wallet to decide which one to use on their own and simplifying user experience.

### LN+ App Available In Umbrel

The title says it all: Umbrel users will {{<newtabref href="https://lightningnetwork.plus/posts/334" title="now">}} be able to take part in LightningNetwork+ swaps from the comfort of their nodes. Swaps consist in multiple nodes (typically 3 or 5 for example) opening channels between themselves, creating local network topologies such as triangles or pentagons which help keep channels balanced by performing free circular rebalancing between the partipating nodes.

The Umbrel version of the app eases the user experience, with features such as automatic sign-in and one-click channel open, making it even easier to take part in swaps.

## Specs & Implems

### Dual Funding Between Core Lightning And Eclair Nodes Soon?

As Lisa Neigut {{<newtabref href="https://twitter.com/Core_LN/status/1589561144817352705" title="explains">}}, right now you can use dual funding to open a channel with money on both sides from the get go if you're running either Core Lightning or Eclair and your peer runs the same implementation as you do. Work is being done at Core Lightning to make their implementation of dual funding compatible with Eclair's, which means we'll soon be able to open dual funded channels accross two different implementations. Kinda cool.


### Unjamming Channels

A proposition to address the issue of {{<newtabref href="https://blog.bitmex.com/preventing-channel-jamming/" title="Channel Jamming">}} in Lightning has been {{<newtabref href="https://github.com/s-tikhomirov/ln-jamming-simulator/blob/master/unjamming-lightning.pdf" title="published">}} by Clara Shikhelman and Sergei Tikhomirov, and {{<newtabref href="https://lists.linuxfoundation.org/pipermail/lightning-dev/2022-November/003740.html" title="announced">}} on the Lightning-Dev Mailing List, where it sparked some interesting comments from Antoine Riard (who, among other things, created this {{<newtabref href="https://jamming-dev.github.io/book/about.html" title="ressource">}} on the subject with Gleb Naumenko) and Thomas Huet (from Acinq).

For readers unfamiliar with the concept, Channel Jamming is a current attack vector on Lightning that arises from the fact that failed payments are free: if you're making a payment and it fails somewhere along the route, you get all your funds back. While great on the user experience front, this property also opens the door to attackers spamming the network with payments failed on purpose, thus blocking liquidity in channels for various amounts of time. Today, this attack isn't really done at any scale, but it could be a powerful weapon in the Node Wars that we'll not fail to see if Lightning catches on[^1].

The solution put forward by Shikhelman and Tikhomirov aims to fix both "quick" (payments fail quickly but are resent every few seconds) and "slow" (payments remain in-flight for hours) jamming, while being generic enough to be potentially applied, with some twists, to a wide range of similar issues in other "Bitcoin "decentralized financial networks'", as Riard writes in his comment.

The solution in itself can be divided into two components:
- unconditional fees: users must pay a small fee even for failed payments. Simulation ran by the researchers tend to show that the overall fee paid by a user for failed payments remains low, even with high rates of failure (such as 50%). This is quite effective at preventing quick jamming, as each failed payment (on purpose or not) comes at a cost[^2], but not so much for slow jamming, where one malicious payment can keep funds stuck for hours.
- reputation: nodes keep track of their peers' past behavior, and perform distinct liquidity allocations to "low-risk" peers (peers that have behave correctly in the past) and "high-risk" ones. An attacker could hence not eat the whole liquidity of the node, because part of it is reserved for low-risk peers.

I still have to take some time to really dig deep in what is a whole rabbit hole by itself. The idea of having to pay for failed payments isn't, of course, very appealing, but I don't really see any way around. The whole challenge would then be to minimize those fees for honest participants of the network, notably by keeping failure rates to a minimum.

## Closing Bit

Un âne paissant dans un pré jaune d'été\
Se trouva malgré lui dans un curieux émoi\
Quand d'un côté il vit, courant à perdre pied\
La tignasse bouclée d'un trader en pourvoi.

A ses trousses la foule hurlant à perdre voix\
L'éclaira quelque peu sur ce dérangement.\
Il y était question de gens qu'on atermoie\
Après s'être servi longtemps de leur argent.

Pensant, réfléchissant, à perdre ses neurones\
L'âne se dit qu'enfin, il fallait réguler !\
Et que la solution au vol dont on s'étonne\
Ne saurait se trouver qu'au Château des Marais.

Ce faisant le mulet néglige cependant\
Que ses lois, supplantées, n'ont guère plus d'effet,\
Qu'aujourd'hui on les a pour beaucoup remplacées\
Par leur pendant plus fiable et désintéressé.

---

If you enjoyed this recap, you can show your appreciation by throwing a few coins to *fanis @ lnmarkets.com*, by scanning or clicking the QR code.

Thank you!

{{<figure align=center src="../../images/lnm_lnurl.png" link="lightning:fanis@lnmarkets.com">}}

[^1]: For example, Lightning Service Providers could attack each other in order to gain market shares.

[^2]: With the added benefit of compensating the victim, thanks to this fee.
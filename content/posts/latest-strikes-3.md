---
title: "Latest Strikes 3 - Sept 26th 2022"
date: 2022-09-26T12:00:00+02:00
block: "755771"
cover:
    image: "../images/Lightning_water_knight_6add169d-d61d-462b-9e01-71afbb1b28f9.png"
    alt: "Lightning water knight"
    caption: "'Lightning water knight' Generated with Midjourney."
    relative: "false"
tags: ["bitcoin", "lightning"]
categories: ["strikes"]
paybuttonlink: "https://btcpay.fanismichalakis.fr/apps/2dTq39Qoj9oJrFdBTQNTXu2MjbMh/pos"
draft: false
---

Sup! Welcome to this new edition of Latests Strikes, your weekly recap of what the cool kids talk about when they discuss the Lightning Network. Fasten your seatbelt and put on your helmet as we drive irresponsibly fast into the storm!

## Ecosystem

### BitGo goes long on Lightning

Crypto custodian {{<newtabref href="https://www.bitgo.com" title="BitGo">}} {{<newtabref href="https://scribe.rip/bitgo-unveils-custodial-lightning-898554d3b749" title="unveiled">}} the integration of Lightning into their custody products. Basically, BitGo will take care of everything on behalf of their customer, which can replace all the Lightning stuff with API calls.

### StackerNews Release

Stacker News latest {{<newtabref href="https://stacker.news/items/72602" title="release">}} introduces downvotes to the forum. Each downvote costs 1 sat and effectively lower the rank of the downvoted item. If enough downvotes are cast on an item, this item will be outlawed and removed from view. At the same time, a new *Wild West Mode* is available, which allows users to opt-out from this new feature and wander in the website as they did before, without any effect from downvotes. Sounds like moderation done right!

### New THNDR game drop

A new {{<newtabref href="https://thndr.games" title="THNDR">}} game dropped, and it's already decimating the productivity of Lightning enthousiasts at large! *Club Bitcoin: Solitaire* reinterprets the iconic Solitaire game, with a Lightning topping and sprinkles of sats everywhere. You can download the game with my {{<newtabref href="https://solitaire.thndr.games/r/bWyb" title="link">}} (super cool and free way of supporting the content you're reading) or {{<newtabref href="https://www.thndr.games/bitcoin-games/bitcoin-solitaire" title="without">}} (still cool, love ya). <mark>(productivity notice: higly addictive!)</mark>

### BoltFun Tournament Announced

Book October 12th, for this will be the start date of BoltFun's first {{<newtabref href="https://nitter.net/boltfun_btc/status/1572251737120964613" title="Tournament">}}! From October 12th to November 28th makers will buidl, accelerate their project through development, design and Lightning integration mentorships, take part in both IRL and online meetups, and try to be one of the true Legends and get a share of a 3BTC pool!

### Fountain Release

Podcasting2.0 app {{<newtabref href="https://fountain.fm" title="Fountain">}} published an {{<newtabref href="https://nitter.net/fountain_app/status/1572330786715582464" title="update">}}, with a more simple earning mechanism (you can earn sats during your first hour of podcast listening, with a random rate, everyday), a new refferal system, and comments for non-Lightning enabled podcasts (Lightning-enabled ones already have boosts). Speaking of refferal, here's my {{<newtabref href="https://fountain.fm/skyfan?code=1d14a24961" title="link">}}, feel free to use it!

## Papers

### Controling flows in Lightning with valves

{{<newtabref href="https://nitter.net/renepickhardt" title="Rene Pickhardt">}} published a new {{<newtabref href="https://blog.bitmex.com/the-power-of-htlc_maximum_msat-as-a-control-valve-for-better-flow-control-improved-reliability-and-lower-expected-payment-failure-rates-on-the-lightning-network" title="research article">}} with BitMEX Research, evaluating how the use of *valves* on Lightning channels could reduce the number of payment failures, improve the overral reliability of the network and keep channels balanced.

Valves are typically used in hydraulic (or other fluids) systems to manage the flow of water. Pickhardt's idea is to use the `htlc_maximum_msat` parameters of each channel to offset the draining effect that occurs when the volume of payments flows asymmetrically between the two sides of a channel.

Let's take an example. Imagine a channel between Alice and Bob where, for some reason, Alice forwards twice as much sats to Bob than Bob forwards to Alice. This could be, for example, because Bob is connected to an online store which receives a lot of payments. The result is that over time the liquidity on Alice's side of the channel will be depleted, and everything will be on Bob's side. When this happens, node operators usually *rebalance* the channel, either with swaps between Lightning and on-chain, or with circular rebalancing. Both methods are quite costly, can take some time when the Bitcoin chain is involved, etc. Hence the idea of using *valves* to direct and modulate the flow of payments.

Each node operator can set the `htlc_maximum_msat` parameter for each of their channel independently, and the change is broadcast to the rest of the network via the gossip protocol (just like channel announcements, fees, etc.). This parameter indicates the size (in terms of millisatoshis, 0.001 satoshi) of the biggest HTLC that the node operator is willing to forward on this channel. For example, a `htlc_maximum_msat` of 50 million means that the node operator will only accept to forward HTLCs of 50,000 sats or less. Any bigger HTLC will not be forwarded by the node operator on this specific channel. This information can (and should) be used by senders when looking for routes, to only consider channels that accept big enough HTLCs.

Each channel hence has two `htlc_maximum_msat` parameters, one for each side/direction of the channel, and unless the flow in the channel is perfectly symmetrical, they have no reason to be equal. This parameter is already actively used by some node operators (such as {{<newtabref href="https://zerofeerouting.com" title="zerofeerouting">}}) to indicate when liquidity is depleted on their side of a channel. Pickhardt's proposition takes it even further: assuming some kind of stationnary state (for example, Alice steadily forwards two times more sats to Bob over time, than Bob forwards to Alice), the peers of a channel could find a pair of optimal `htlc_maximum_msat` values for this channel which would balance the asymmetry of flow.

Under this assumption, Pickhardt finds that payment failure rates can be brought down to around 3%, even if the asymmetry of flow between the nodes is big (up to around 1 for 9, eg Alice forwards nine times more than Bob on this channel). The next big step is to test these predictions against reality, where the flow of funds between nodes can often be non-stationnary.

*You can join side with BitMEX and support Rene's work {{<newtabref href="https://donate.ln.rene-pickhardt.de" title="here">}}.*

## Wallets & Tools

### ZeroLogin

{{<newtabref href="https://nitter.net/dolu_Web" title="Dolu">}} released an {{<newtabref href="https://nitter.net/zerologin_co/status/1573333782760931328" title="update">}} of their {{<newtabref href="https://zerologin.co" title="Zerologin">}} project. Zerologin is a passwordless authentication server using LNURL-auth in the backgroud that's meant to be easy to deploy, or to be used by plugging your system into someone else's instance. This open source tool is still in development (dont't use in production, you freak!), but you can check out the {{<newtabref href="https://zerologin.co/login" title="demo">}} to see the magic happen!

Feel free to reach out to Dolu to sned some {{<newtabref href="https://twitter.com/Dolu_Web/status/1573944312450228224" title="feedback">}}! <mark>(privacy notice: this is a Twitter link)</mark>

### Tor <> Clearnet Bridges in sats4.me

{{<newtabref href="https://nitter.net/AaronDewes" title="Aaron Dewes">}} and {{<newtabref href="https://nitter.net/dtvelectronics" title="DTV Electronics">}} {{<newtabref href="https://nitter.net/AaronDewes/status/1573714612012417027" title="released">}} an hosted Tor to Clearnet bridge. The goal is to make it easier for people running nodes behind Tor (for example using Umbrel, Raspiblitz or Citadel) to make them accessible from the rest of the web.

The service is part of {{<newtabref href="https://sats4.me" title="sats4.me">}}, is still in beta and currently free (although it will probably become a paid feature in the future).

### Remote signing with VLS

In *Latest Stikes #2* I briefly wrote about {{<newtabref href="../latest-strikes-2/#remote-signing-in-lnd" title="remote signing">}}. Here is an {{<newtabref href="https://nitter.net/sphinx_chat/status/1571974701098074112" title="example">}} of {{<newtabref href="https://sphinx.chat" title="Sphinx.chat">}} using the {{<newtabref href="https://nitter.net/VLSProject" title="Validating Lightning Signer">}} to keep their private keys at home while the node itself is running in the cloud. Impressive!

### LN Bits Release

LN Bits latest {{<newtabref href="https://github.com/lnbits/lnbits/releases/tag/0.9.4" title="release">}} includes several important fixes as well as some new extensions, including support for Hardware Wallets ({{<newtabref href="https://lnbits.github.io/hardware-wallet/installer/" title="build your own">}}, use it with LnBits) and a Boltcard Extension to create and manage LNURL NFC cards.

### Flutter webln package

{{<newtabref href="https://nitter.net/Anipy1" title="Aniket Ambore">}} {{<newtabref href="https://nitter.net/Anipy1/status/1571495893043654656" title="published">}} a WebLN Flutter {{<newtabref href="https://flutterawesome.com/a-webln-interface-for-creating-bitcoin-lightning-powered-web-applications/" title="package">}}. WebLN enables seamless interactions with Lightning in the browser, and already powers a lot of webapps or browser extensions such as {{<newtabref href="https://getalby.com" title="Alby">}}. Having a Flutter package fot that will probably prove immensely useful for app builders. Thank you Aniket!

## Closing Bit

{{<blockquote>}}
Ton visage est un trou\
D'eau dans la banquise\
Qu'un vent continu vient\
Sans cesse rider

Si l'on y plonge\
C'est l'intensité glaciale\
De ton regard\
Qui nous étreint.
{{</blockquote>}}

---

If you enjoyed this recap, you can show your appreciation by throwing a few coins in one of the jars. The BTC Pay jar opens in a new tab, while the LN Address jar is a one-click button (with Alby) to send sats to *fanis @ lnmarkets.com*.

Thank you!

<div style="display: inline-grid;grid-template-columns: 50% 50%;align-items: center;width: 100%">
    <div>
        {{<paybutton text=" 🎩 BTC Pay 🏦" color="#51b13e">}}
    </div>
    <div>
        {{<paybutton text="✉️ LN Address 🐝" color="#f5ac11" link="lightning:fanis@lnmarkets.com">}}
    </div>
</div>
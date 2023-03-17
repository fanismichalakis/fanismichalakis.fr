---
title: "Latest Strikes 4 - Oct 2nd 2022"
date: 2022-10-02T23:30:00+02:00
block: "756770"
cover:
    image: "../images/DALL·E_lightning-strike-hits-rod-top-of-mountain.png"
    alt: "a lightning strike hitting a lightning rod at the top of a mountain, digital art"
    caption: "'a lightning strike hitting a lightning rod at the top of a mountain, digital art' Generated with DALL·E."
    relative: "false"
tags: ["bitcoin", "lightning"]
categories: ["strikes"]
paybuttonlink: "https://btcpay.fanismichalakis.fr/apps/2dTq39Qoj9oJrFdBTQNTXu2MjbMh/pos"
draft: false
---

Yo! Welcome to this 4th edition of Latest Strikes, your weekly recap of Lightning news. Grab a drink, and let's dive in!

## Ecosystem

### Some Numbers for the Nerds

{{<newtabref href="https://nitter.net/kerooke" title="Kevin Rooke">}} opened the ball of statistics this week with an interesting {{<newtabref href="https://nitter.net/kerooke/status/1575312721192574977" title="comparison">}} of exchange nodes capacity and its evolution over the last 30 days. We can see that the 13 exchanges considered in this analysis saw a collective increase of their public capacity of 349 BTC, which is a 20% increase! This major surge has been mostly carried by River and Kraken, with respectively a 56% and a 32% increase, while all other exchanges fall under the mean evolution of 20%.

Still, one should remain cautious when analyzying these raw numbers, as they don't tell wether this increase comes from exchanges deploying liquidity, or other people (customers, other services and platforms, routing nodes, etc.) connecting to them. Some on-chain analysis could help us draw a clearer picture, but it is a work that remains to be done.

On the network-wide aspect, it also seems like we just broke {{<newtabref href="https://nitter.net/kerooke/status/1575490303720820739" title="4,900 bitcoins">}} deployed in public channels!

On a more local scale, we at {{<newtabref href="https://lnmarkets.com" title="LN Markets">}} just celebrated {{<newtabref href="https://nitter.net/LNMarkets/status/1575499961860784128" title="140 BTC routed in Q3 2022">}} alone. Numbers definitely going up in this regard!

### Strike Raises 80 million

Looks like Strike just {{<newtabref href="https://fortune.com/crypto/2022/09/27/bitcoin-rapid-payment-service-strike-raises-90m-takes-aim-at-visa/" title="raised">}} 80 million dollars in a Series B led by {{<newtabref href="https://ten31.vc/content/strike" title="Ten31">}}. 🚀

### Bitcoin Exchange Bitnob Now Live in Kenya

People in Kenya can now use {{<newtabref href="https://nitter.net/Bitnob_official/status/1574360926148562950" title="Bitnob">}} to buy, sell, receive and send Bitcoin, including over Lightning. As Bernard Parah {{<newtabref href="https://nitter.net/i/status/1574493492000309248" title="highlights">}}, this is a huge deal in a country where the Bitcoin market is increasing at great speed, but where remittances are still vastly carried out by Western Union and the like which impose their oligopolistic fees and conditions. Thanks to Lightning, Kenyans can now receive Bitcoin from anywhere in the world, instantly, and easily thanks to the support of Lightning Addresses by Bitnob.

### First TARO Release

Lightning Labs just {{<newtabref href="https://nitter.net/lightning/status/1575152781899415554" title="released">}} an alpha version of the Taro daemon {{<newtabref href="https://github.com/lightninglabs/taro/" title="tarod">}} to issue, send and receive assets on Bitcoin using the TARO protocol. I must confess I'm impressed because, even if the feature set is still limited today, I expected the development of this first alpha version to take more time, in spite of the amazing 70 million dollars raised a few months ago (money doesn't provide everything, right?). Well done team!

## Spec & Implems

### Asynchronous / offline payments in Eclair

One of the main remaining friction points in the world of Lightning today is the ability to receive payments while being offline. Today, it is mostly impossible to do so in a non-custodial setup, because your node needs to be online to sign the commitment transaction when you receive funds. It works in a fully custodial environment, because your custodian receives the funds (and hence, signs) on your behalf, but we all want Lightning to succeed in having the best user experience without any sovereignty and privacy tradeoffs (or, more realistically, with as few tradeoffs as possible).

Work is being done today to improve Lightning so that users can receive funds to their own node even when said node is offline. This is especially useful for mobile nodes (such as Phoenix or Breez nodes), which spend most of their time being offline. A solution to this problem relies on two main improvements: trampoline routing and onion messages.

Onion messages allow nodes to send messages to each other through the network, and are being implemented across implementations as we speak[^1].

The second part is trampoline routing. To put it in a nutshell, trampoline routing can be very useful for mobile nodes by enabling them to only be aware of a subset of the network (for example, their immediate neighborhood plus a few nodes in the more distant network). To do so, some intermediate nodes, called trampoline nodes, will be in charge of computing some parts of the route. For example, when I make a payment to some recipient that is so far from me than I'm not able to compute a route to them with my contrived view of the network, my mobile node could select two trampolines node I am aware of and use them as a route. My node would need to find a route to the first trampoline node (as usual), and tell this node to forward the payment to the second trampoline node. The first trampoline node would then compute the route toward the second one themselves. Once the second trampoline node receives the payment, they read their instructions and discover they must forward the payment to the recipient. They will therefore compute the route themselves and send the payment along it. This way, our mobile node was able to reach a distant node without knowing a route to it, simply by sending the packet to a set of trampoline nodes[^2].

With onion messages and trampoline, nodes can now effectively send to an offline recipient: the payment would be held by the first trampoline node (which could for example be the sender's Lightning Service Provider) until the recipient comes online and indicates so. A crucial step has been made in this direction recently, with the addition of {{<newtabref href="https://github.com/ACINQ/eclair/pull/2435" title="initial support for asyncronous payments to offline nodes">}} in Eclair. Achieving asynchronous payment this way, where the payment is held very early in the route, is paramount to avoid having too many channels jammed with in-flights HTLCs when recipients are offline.

Too dive deeper in this subject, you can give a listen to this {{<newtabref href="https://stephanlivera.com/episode/386/" title="discussion">}} (starting from 32:53) between Roy Sheinfeld and Stephan Livera, which my introductory explanation was partly paraphrasing, or take a look to the corresponding {{<newtabref href="https://github.com/lightning/bolts/pull/989" title="BOLT proposal">}}.

### Getting Rid of Legacy Lightning Onion Format

Ir's time to let the {{<newtabref href="https://nitter.net/rusty_twit/status/1575322179897475073" title="legacy Lightning onion format">}} go. After months of careful monitoring of the usage of the legacy format across the network, its usage is finally steadily low enough to {{<newtabref href="https://github.com/lightning/bolts/pull/962" title="deprecate it">}}. The BOLTs now only mention the more flexible Type-Length-Value (TLV) onion format, which was almost the only one being used anyway.

So, if you're one of the few that was still using the old, fixed-length onion format, now is probably a good time to switch to TLV, as other nodes will start rejecting your payments.
 

## Wallet & Tools

### BTCPay Server Release

Version 1.16.11 of BTCPay Server is {{<newtabref href="https://github.com/btcpayserver/btcpayserver/releases/tag/v1.6.11" title="out">}}! It packages a lot of improvements and bug fixes, as well as a few new features. This includes, for example, the refactor of the PoS and Crowdfunding apps to handle them as plugins, instead of having them bundled in the core system ; and the use of {{<newtabref href="https://mempool.space" title="mempool.space">}} as the default block explorer.


### The Eye of Satoshi Release

{{<newtabref href="https://nitter.net/sr_gi/status/1575121262011191305" title="Sergi Delgado announced">}} the {{<newtabref href="https://github.com/talaia-labs/rust-teos/releases/tag/v0.1.2" title="latest version">}} of The Eye of Satoshi (rust-teos), a Lightning watchtower written in Rust. This update notably includes additionnal commands as well as Tor support for the Core Lightning plugin, and a set of more general improvements, such as persitence of the Tor private key (ie, the onion service id will not change on restart anymore).

### ItchySats Coming to Desktop

The {{<newtabref href="https://nitter.net/itchysats/status/1576034065383190530" title="new version">}} of {{<newtabref href="https://www.itchysats.network" title="ItchySats">}} brings it to desktop: with the addition of Windows and MacOS (both Intel and M1) support, you can now run ItchySats pretty much anywhere you want, except on mobile (soon?).

The {{<newtabref href="https://github.com/itchysats/itchysats/releases/tag/0.7.0" title="release">}} also includes a bunch of fixes, improvements and breaking changes, so be sure to check it out if you're using the software.

## Closing Bit

{{<blockquote>}}
De ce trou sortent toutes les merveilles du monde\
Des merveilles que le monde ne connaît pas encore\
Des merveilles d'un autre monde.

C'est à nous qu'il appartient de les extraire\
Infatiguables cueilleurs de ces fruits défendus\
Dont le sucre et les graines ont-le pouvoir, dit-on

De semer la révolte dans toute la plantation.
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

[^1]: They will be very useful for BOLT12's "offers".

[^2]: The use of several trampoline nodes is key to achieve any semblance of privacy.
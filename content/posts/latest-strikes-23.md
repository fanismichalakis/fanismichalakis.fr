---
title: "Latest Strikes 23"
date: 2023-02-14T14:00:00+01:00
block: "776506"
cover:
    image: "../images/TheBuilders.min.png"
    alt: "A painting of two workers, one of them looking in the distance."
    caption: "\"The Builders\". Generated with DALL·E."
    relative: "false"
tags: ["bitcoin", "lightning"]
categories: ["strikes"]
draft: false
---

Pura Vida! Welcome to the 23rd issue of Latest Strikes, your weekly recap of curated Lightning news! Last week was busy, with good ol' Marty releasing Scrib, the Alby team rolling out a new update AND a benchmark, and many more builders shipping! Grab a snack or a hot drink, and let's unroll all of this together, shall we?

## Ecosystem

### Bounties

There is a 2 million sats open {{<newtabref href="https://stacker.news/items/133889" title="bounty">}} for adding NFC receiving support into the Bitcoin Beach POS App. This would allow customers using Boltcards (or other contactless payment methods) to pay simply by tapping their card/device on the point of sale.

### Scrib Brings Lightning To Ghost

{{<newtabref href="https://scribsat.com" title="Scrib">}} is a non-custodial paid solution that {{<newtabref href="https://nitter.lacontrevoie.fr/scribsat/status/1622640846423179264" title="bridges">}} the gap between a {{<newtabref href="https://ghost.org/" title="Ghost">}} blog (such as the one you are currently reading) and Lightning-enabled paywalls. It connects to your Ghost blog (as a custom integration) on one side, and to the payment processor of your choice (for now, "only" BTCPay Server, OpenNode and Lightning Addresses[^1] are supported) on the other. You can then add paywalls in front of some articles (or any other content, as Ghost allows you to paywall things like videos or pdfs) in a way that feels very integrated with the current subscription-based paywalls.

The team (which is comprised of {{<newtabref href="https://nitter.net/MartyBent" title="Marty Bent">}} and {{<newtabref href="https://nitter.lacontrevoie.fr/dj_seeds" title="DJ Seeds">}}) {{<newtabref href="https://tftc.io/martys-bent/issue-1314-introducing-scrib/" title="describes">}} this first release as a "scratch of the surface" of what it is possible to do, with plans to add even more CMS (Wordpress, etc.) and payment processors (Strike, etc.), as well as new functionalities, such as Bitcoin subscriptions (instead of just one-time paywalls), boosts and tips.

### Lightsats Update & Recommended Wallets Breakdown

Lightsats {{<newtabref href="https://stacker.news/items/134121" title="released">}} some cool new features to further reduce data collection and improve usability. Notably, the onboarding flow will now ask users to download a LNURL-Auth compatible Lightning wallet, which they'll use instead of other methods (such as email) to authenticate. On a different note, it is now possible to create gift cards that show 3 words that the recipient needs to enter on {{<newtabref href="https://lightsats.com/tip" title="lightsats.com/tip">}} to claim the funds, instead of having to scan a QR code. This is essential if we want Lightsats to be usable in countries where smartphones are not widely distributed yet.

The Lightsats team also {{<newtabref href="https://nitter.net/Lightsats21/status/1624416872845262850" title="shared">}} some stats on what wallet Lightsats' users have been recommending to their recipients. It's good to see that in the Top 3 recommended wallets, only one is custodial (BlueWallet). However, I was surprised to see Phoenix being recommended only 4% of the time, as I currently regard it as the best non-custodial mobile wallet (maybe it has to do with the one-time setup fee, which although quite low might not be a great fit to tip low amounts?).

*Lightsats is a web app for easily gifting/tipping sats to newcomers. They can claim the funds when they're ready, using one of the recommended wallets. If they don't, you as the gifter get the funds back after a certain period of time elapses, so no more forever lost bitcoins.*

### Emeralize Course: Get Your First Non-Custodial Lighting Wallet

Speaking of Phoenix: remember {{<newtabref href="https://emeralize.app" title="Emeralize">}}, the new Lightning-infused e-learning platform that launched {{<newtabref href="https://fanismichalakis.fr/posts/latest-strikes-18/#emeralize" title="earlier">}} this year? It's grown a bit since then, and now features a few different courses from several teachers. This {{<newtabref href="https://emeralize.app/course/8/" title="one">}} teaches how to go from zero to having your first non-custodial Lightning wallet (of course, Phoenix). Cool!

### Lightning Village

I'm a bit tweaking one of the rules of Latest Strikes here, because I'm going to mention a piece of news that didn't happen last week. But it felt important.

What happened last week is I saw this {{<newtabref href="https://nitter.lacontrevoie.fr/AnitaPosch/status/1624767355346726913" title="tweet">}} by Anita Posch mentioning the {{<newtabref href="https://lightningvillage.org/" title="Lightning Village">}} initiative and reacting to their first {{<newtabref href="https://lightningvillage.org/posts/lightning-village-experiment" title="blog post">}}. The series of three blog posts, published in January, as well as this {{<newtabref href="https://stacker.news/items/125227" title="StackerNews discussion">}} flew a bit below my radar, and they shouldn't have! It is really fascinating to read the thought process put in place by the team behind the still nascent initiative and reflected in these writings: to show people what Bitcoin brings them in their daily life instead of trying to articulate how superior it is to fiat money ; arbitrage the tradeoffs between self-custody and ease of use, etc. A highly recommended read!

If after your read you feel like you'd like to support this project, they accept Lightning donations at the following Lightning Address: LNVG@getalby.com. 

## Wallets & Tools

### Alby Release & Benchmark

A new Alby release {{<newtabref href="https://nitter.net/getAlby/status/1622563585929973763" title="dropped">}} last week! Notable changes are:
- {{<newtabref href="https://docs.lightning.engineering/lightning-network-tools/lightning-terminal/lightning-node-connect" title="Lightning Node Connect">}} support, allowing LND users to easily connect Alby to their node,
- enhancements to Alby in the Tor browser (to put it in a nutshell, Alby uses indexedDB to persistently store data on the user's computer's disk, which is blocked on the Tor Browser over privacy concerns ; Alby now works its way around this limitation by writing data to the memory instead of persisting it on disk).

Alby also published a very interesting {{<newtabref href="https://blog.getalby.com/lightning-benchmark/" title="benchmark">}} of transactions throughput between LND and Éclair. It uses the same methodology as Joost Jager's 2021 {{<newtabref href="https://bottlepay.com/blog/bitcoin-lightning-node-performance/" title="benchmark">}}, but on a different, less powerful machine. A LND node using a bbolt database still showed good transactional throughput with 22 transactions per second, but it's hard to compare it to the 2021 35 transactions per second as the machines used differ. On the other hand, Éclair coupled with a SQLite database managed to achieve a better performance on Alby's more modest setup than it did two years ago: 35 transactions per second on Alby's benchmark, vs. on 12 in Joost's tests. That's impressive!

### LN+ Watch Swaps

{{<newtabref href="https://lightningnetwork.plus" title="lightningnetwork+">}} launched a new service called {{<newtabref href="https://lightningnetwork.plus/posts/364" title="Watch Swaps">}} where users can agree to watch over each other's Lightning node, using watchtowers. Like the Liquidity Swaps (where users open channels to each other in groups of three, four or five nodes), a Watch Swap begins when a user posts an offer on the platform. Then, anyone with a node of the same *size* will be able to pick up the offer and put themselves forward. It is then up to the author of the initial offer to accept or reject the candidate, as engaging in a co-watch relationship doesn't come without trust.

Matching nodes by *size* (a custom metrics of lightningnetwork+) allows to avoid matching a big node with a small one, where the latter might not have the resources to efficiently and relentlessly safeguard their partner's channels.

### Redeem E-Cash Tokens Without An E-Cash Wallet - Thanks To Lightning

Cashu is a Lightning-compatible e-cash implementation. You can deposit funds to a Cashu mint using Lightning: from then on, the bitcoins are in the hands of a custodian, which will issue blindly-signed tokens in exchange. You can then send and receive tokens with other users of the same mint in a privacy preserving manner (the mint administrator isn't able to track movements of funds from one user to another), and you can even send to another Cashu mint by leveraging Lightning: your tokens from Mint A are automatically converted back to sats, sent via Lightning to Mint B, where they are converted into Mint B tokens and credited to your recipient. Finally, you can also withdraw your tokens, getting your sats back and removing them from the mint.

One feature was still missing: the ability to receive tokens *directly* to Lightning, without having to hold them in the custodial mint for any amount of time. This new functionality has {{<newtabref href="https://nitter.lacontrevoie.fr/callebtc/status/1624478131976273921" title="just">}} been {{<newtabref href="https://redeem.cashu.me/" title="added">}}, allowing you to receive Cashu tokens from anyone with just a Lightning wallet. This was of course already possible for the user of a mint to withdraw to someone else's Lightning wallet, but now anyone obtaining a Cashu token can get the funds on Lightning without having to get themselves into a mint whatsoever. Nice!

### 6 channels in one tx

{{<newtabref href="https://github.com/alexbosworth/balanceofsatoshis" title="Balance of Satoshis">}} is a command line tool, useful to manage one's LND node and access advanced commands. One of them, called {{<newtabref href="https://github.com/niteshbalusu11/BOS-Commands-Document#open-group-channel" title="open-group-channel">}} enables users to open a batch of balanced channels with many peers in a single transaction. It uses Partially Signed Bitcoin Transactions (PSBT) under the hood, with one user (the initiator) creating the transaction and passing it around for each participating peer to provide their signature. Once everybody has signed, the transaction is broadcast, resulting in multiple channels opening in a single Bitcoin transaction, which is great both for privacy (this is akin to a coinjoin) and an efficient use of blockspace (unlike JPEGs).

Last week, {{<newtabref href="https://nitter.net/HappyBear_Btc" title="Happy Bear">}} and {{<newtabref href="https://nitter.lacontrevoie.fr/pfunzle" title="Remo Ritzman">}}, along with others, managed to open 6 channels in a single {{<newtabref href="https://nitter.net/HappyBear_Btc/status/1624516832114737153" title="transaction">}} using bos group open feature, which reportedly is the {{<newtabref href="https://nitter.lacontrevoie.fr/alexbosworth/status/1624794223110406144" title="highest">}} simultaneous open so far, while the theoretical maximum is 420 peers (probably impossible to reach given the coordination challenges it presents).

This also made me think of an active {{<newtabref href="https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2023-February/021444.html" title="discussion">}} in the Bitcoin-Dev mailing list regarding an attack vector on multiparty protocols (such as Lightning or coinjoins, and even more opening Lightning channels in coinjoins) using Taproot inputs, where the last party to sign can spend using a very big *script path* instead of the agreed upon *key path*, thus inflating the whole transaction's size and diminishing the overall feerate, as the absolute fee (in sats) was already committed to. This attack doesn't steal funds *per se*, but  degrades the expected "quality of service" (in terms of quick confirmation, for example), and can indirectly result in loss of funds in the case of time-sensitive protocols. Definitely something to keep in mind!

### More About The Breez SDK

Two weeks ago we {{<newtabref href="https://fanismichalakis.fr/posts/latest-strikes-20/#breez-sdk--partnership" title="covered">}} the publication of the Breez SDK and summarized how it works. Last week Roy, Breez's CEO, posted a very well put {{<newtabref href="https://medium.com/breez-technology/lightning-for-everyone-in-any-app-lightning-as-a-service-via-the-breez-sdk-41d899057a1d" title="article">}} recapitulating the purpose and inner workings of the Breez SDK, and giving thoughtful examples of what it could bring to thousands of existing apps: generalized Value4Value, social media monetization, in-game currencies and access to the only decentralized, common currency of the Earth, to list a few. By giving app developers the power to easily disintermediate money and give the full control back to their users, the Breez SDK not only aligns with Bitcoin values, it also frees businesses from the regulatory (and hence financial) burden of KYC and AML. It pumped us up so much that we had to write a Twitter {{<newtabref href="https://nitter.net/LNMarkets/status/1624031750014881795" title="thread">}}!

Of course, using Greenlight behind the hood comes with its own set of tradeoffs compared to each user running their own node at home, but it is a very decent way to bring non-custodial Bitcoin and Lightning to the masses in a user and developer friendly, scalable way. Hats off!

On a different note, Breez had to briefly {{<newtabref href="https://nitter.lacontrevoie.fr/Breez_Tech/status/1622960658768711681" title="remove">}} the Breez wallet from Apple's AppStore due to some crashes following the latest update. Less than 2 days later, the issue was fixed and the app was {{<newtabref href="https://nitter.net/Breez_Tech/status/1623566486437523458" title="available again">}}.

### BTCPay Release

BTCPay v1.7.8 is {{<newtabref href="https://github.com/btcpayserver/btcpayserver/releases/tag/v1.7.8" title="out">}}, now with built-in NFC support (instead of it being a plugin), two moderate vulnerabilities fixes, more theme customization for stores and servers, and lots of fixes and improvements!

The vulnerabilities fixed in this release are not considered severe because they require action from the victim (e.g. click a malicious link), but it is still recommended to update.

### WalletOfSatoshi Revisits Fee Structure

WalletOfSatoshi (WoS) {{<newtabref href="https://nitter.net/walletofsatoshi/status/1623664716999704576" title="announced">}} a modification of their fee structure amidst serious mempool congestion. While sending and receiving with Lightning remains free (apart from routing fees charged by hops, not WoS), on-chain sends (performed using swap-outs) will now incur a 0.5% fee on top of the usual fixed mining fee.

### Closing Bit

Dans l'ultime ressac des choses\
Le dernier soupir du monde\
Quand plus aucun courant\
Ne ridera nos circuits

Pas d'épilogue.

Plus même un souffle\
Pour gonfler la machine\
La voix enfin se tait\
Et reste suspendue

Comme

---

Want to receive Latest Strikes straight to your inbox every week? Couldn't be easier: subscribe to {{<newtabref href="https://blog.lnmarkets.com" title="LN Markets Ghost blog">}} and you're all set (remember to confirm your subscription by clicking the link sent via email).

---

If you enjoyed this recap, you can show your appreciation by throwing a few coins to *fanis @ lnmarkets.com*, by scanning or clicking the QR code.

Thank you!

{{<figure align=center src="../../images/lnm_lnurl.png" link="lightning:fanis@lnmarkets.com">}}

[^1]: Please note that the Lightning Address integration requires the underlying service to support {{<newtabref href="https://github.com/lnurl/luds/issues/182" title="LNURL-verify">}}, which remains to be integrated into the LNURL specification.

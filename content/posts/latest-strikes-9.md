---
title: "Latest Strikes 9 - Nov 6th"
date: 2022-11-07T10:10:00+01:00
block: "762103"
cover:
    image: "../images/DALL·E 2022-11-07.png"
    alt: "Spongebob's cockroach eating a burger while everything burns around him"
    caption: "'Spongebob's cockroach eating a burger while everything burns around him'. Generated with DALL·E."
    relative: "false"
tags: ["bitcoin", "lightning"]
categories: ["strikes"]
draft: false
---
## Wallets & Tools

### Blixt Wallet v0.6.0

Hampus Sjöberg {{<newtabref href="https://nitter.lacontrevoie.fr/hampus_s/status/1587821919390269442" title="released">}} the {{<newtabref href="https://github.com/hsjoberg/blixt-wallet/releases/tag/v0.6.0" title="version 0.6.0">}} of the {{<newtabref href="https://blixtwallet.com" title="Blixt Lightning Wallet">}}! This new version ports the wallet to MacOS, which makes it one of the few Lightning wallets available on desktop.

The release also features a number of improvements, such as the "sats" unit being the default, the ability to connect to nodes running behind onion v3 addresses, support for receiving to Taproot addresses or a welcomed change in connection flow: users can now change the Bitcoin node Blixt connects to before creating or restoring their wallet. Note that the node needs to support {{<newtabref href="https://bips.xyz/157" title="BIP157">}}, as Blixt is built upon a {{<newtabref href="https://github.com/lightninglabs/neutrino" title="Neutrino">}} privacy-preserving light client.

### Stats for Value4Value creators

{{<newtabref href="https://nitter.lacontrevoie.fr/conshax" title="Conshax">}} {{<newtabref href="https://stacker.news/items/87899" title="announced">}} their Value4Value {{<newtabref href="https://conshax.app/" title="dashboard">}}, aimed at helping creators get a grasp of what their audience likes, watches and listens the most. It leverages one of the unique characteristics of Value4Value, where people streaming down content can stream up sats to the content creator in return *while they're consuming the content*.

This means that simply by observing {{<newtabref href="https://conshax.app/analytics" title="statistics">}} about sats tipped over time, content creators can litterally view which parts of the show their audience listened to the most, or which part really appreciated because it led to more tips being sent in the form of boostagrams.

### Tor Support in Cashu

In the last issue of Latest Strikes, we {{<newtabref href="../latest-strikes-8/#grants" title="mentionned">}} the awarding of the OpenSats' "E-Cash" grant to {{<newtabref href="https://nitter.lacontrevoie.fr/CashuBTC" title="Cashu">}}, a Lightning-enabled Chaumian ecash implementation.

The project was only awarded half the grant, because the mint administrator was still able to learn their users' IP addresses. This pricacy consideration is now addressed, as Cashu wallets now {{<newtabref href="https://nitter.lacontrevoie.fr/CashuBTC/status/1587809906035507200" title="run with Tor by default">}}.

## Ecosystem

### Some Routing Stats For Major Nodes

{{<newtabref href="https://nitter.lacontrevoie.fr/kerooke/" title="Kevin Rooke">}} shared some quite interesting {{<newtabref href="https://nitter.lacontrevoie.fr/kerooke/status/1587176076559745027" title="statistics">}} about routing volumes for some of the top Lightning nodes.

The chart compares the (self reported) amount of BTC routed by River, Zero Fee Routing, LNMarkets, Kollider, LQwD and Cold Sats, as well as what this absolute number represents relative to each of this node's public capacity. For example, River is number 1 by far in absolute number of bitcoins with around 640 BTC routed in September, but it "only" represented 1.4 times their public capacity ; whereas Zero Fee Routing "only" routed slightly more than half this amount, but in their case this volume represented 4 times their public capacity.

What is cool to is that a few other quite influencial Lightning nodes reported their stats in the tweet's comments, including {{<newtabref href="https://nitter.lacontrevoie.fr/c_otto83/status/1587195089868161030" title="Carsten Otto">}} and {{<newtabref href="https://nitter.lacontrevoie.fr/dannydiekroeger/status/1587217355741884416" title="Deezy">}}.

Another graph caught my eye this week, from LN Capital's {{<newtabref href="https://drive.google.com/file/d/1PUKvqmOs1AZcPnxia4D7YObDs5sDgIVG/view" title="Lightning Report">}}: the median cost of a 1 million sats payment in September vs now (page 8 of the report). It's interesting to see this number go up (NGU tech innit?), while staying in the realm of the acceptable: from 655 msats to around 1000msats (ie 1 satoshi) for a 3 hops payment. A more resilient and dependable network surely comes at a cost.

Regarding the methodology, my guess is that Leonardo and Henrik from {{<newtabref href="https://ln.capital/" title="LN Capital">}} looked at all the announced base fee and fee rates in public channels, constructed all possible routes, computed the cost for each route by adding the costs of each channel, and then found the median for each subset of routes, classified by number of hops. In the end, because announced fee rate is expressed in parts per million (ppm), this gives us exactly what we're looking at: the median cost of a 1 million sats payment depending on the number of hops on the route.

### A Major South African Retailer Accepts Bitcoin via Lightning

You can now pay for your groceries with Lightning in South Africa, thanks to the integration of {{<newtabref href="https://www.cryptoconvert.co.za/" title="CryptoConvert">}}'s solution in {{<newtabref href="https://en.wikipedia.org/wiki/Pick_n_Pay_Stores" title="Pick n Pay stores">}}.

Lightning Labs developer Elle Mouton gave it a {{<newtabref href="https://nitter.lacontrevoie.fr/ElleMouton/status/1587872199960141826" title="try">}} and, if you look closely at the video, you can see a few interesting things.

First, that the overall experience seems to be quite seamless. Of course, paying with Lightning with your phone still takes more time than just opening ApplePay and touching the point of sale device with your phone (as my lovely and absolutely never contrarian girlfriend observed when I show her the video), but that's still pretty impressive!

Second, that the wallet used by Elle is the non-custodial Zeus Wallet, and not some custodial nightmare where you're not even sure of whether you're really interacting with Lightning or not. That was of course expected from a Lightning dev, but still refreshing to see.

Third, did you notice what happened at the very beginning, when Elle scanned the point of sale's QR Code? No? Play it again. Here, see? She scan the code with another app, which then automatically opens her lightning wallet. So what's going on?

No need to go scouting to far, as always a cool bitcoiner is already in the comments asking the good questions. This time it's {{<newtabref href="https://nitter.lacontrevoie.fr/callebtc/status/1588091133174943744" title="Calle">}}, getting {{<newtabref href="https://nitter.lacontrevoie.fr/carelvwyk/status/1588100254800306176" title="answers">}} from the founder of CryptoConvert himself. Turns out the QR code displayed on the point of sale ins't an actual Lightning invoice, as one could have originally thought. It is instead a "CryptoConvert QR code" that can be read by the "CryptoConvert app" on the customer's phone. This app must be set up before payment, and linked to an existing Lightning wallet with a test transaction. This ensures that when the customer arrives at the checkout, they already have a wallet ready with enough funds to perform the payment.

When Elle scans the QR code with the app, it generates an invoice corresponding to the amount to pay and pass it to the wallet linked at setup, here Zeus. Of course, introducing an intermediary app comes with tradeoffs, but I personnaly think it's quite useful and necessary during the transition period from outdated payment systems to Bitcoin and Lightning.

### Betting Contest Einundswanzig x LN Markets x Bitcoin Ekasi

Speaking of South Africa, {{<newtabref href="https://einundzwanzig.space/" title="Einundzwansig">}} and {{<newtabref href="https://lnmarkets.com" title="LN Markets">}} are organizing a {{<newtabref href="https://nitter.lacontrevoie.fr/LNMarkets/status/1585587592237617155" title="betting competition">}} for the Football (soccer, ya know?) World Cup with a 6 million sats reward. Registration to the contest costs 50,000 sats, all of which will be sent to {{<newtabref href="https://bitcoinekasi.com/" title="Bitcoin Ekasi">}} to support their work on the ground!

I know some of you, including myself, might be reluctant to celebrate the FIFA World Cup given where it takes place, but this "betting 4 good" contest is a good opportunity to turn it into something better.

### Orange-Pill with Lightning

In the {{<newtabref href="../latest-strikes-5/#onboarding-nocoiners-to-bitcoin--lightning" title="5th issue">}} of Latest Strike, I wrote about a cool project hat was just starting for BoltFun's {{<newtabref href="https://makers.bolt.fun/tournaments/1/overview" title="LegendsOfLightning">}} tournament. The goal of the then-unnamed project was to build a cool webapp where bitcoiners could  create tips (in sats), and then give the link to the tip page to someone they are orange-pilling. This person could then, back home, go to the website and claim the gift.

This makes it easier to gift sats without having the recipient install this or that app while sitting in a noisy pub, and avoids funds that are lost forever because the recipient just forgot about them.

In just a few weeks, the team behind the project has made impressive progress, with a cool name and even cooler {{<newtabref href="https://lightsats.com/" title="webapp">}}. The user experience is really smooth, and it is fairly easy to create gift cards as a bitcoiner, or claim one as a nocoiner, with a spot on tutotial on how to install a good Lightning wallet to receive the funds.

If you want to give it a try, you can click {{<newtabref href="https://lightsats.com//tips/cla6k7jov004ufjf63g5rr4s5/claim" title="here">}} or {{<newtabref href="https://lightsats.com//tips/cla6kahum004vfjf6498eh5hs/claim" title="here">}}. First-come, first-served, but feel free to pass it along by creating another tip and sharing it as well!

## Specs & Implems

### Yet Another Bug Triggered By Burak

A few weeks after triggering a wire-related {{<newtabref href="../latest-strikes-6/#da-bug-do-not-eat-it" title="bug">}} in btcd (and hence LND) with a 998-of-999 multisignature transaction, Burak {{<newtabref href="https://nitter.lacontrevoie.fr/brqgoo/status/1587397646125260802" title="recidivated">}}. This time, they published a transaction carefully designed to exloit a consensus discrepency between btcd and Bitcoin (Core).

In Bicoin, there are consensus rules governing things such as the stack size or the number of elements in the stack. However, Taproot introduced the `OP_SUCCESSx` opcodes (there are 87 `OP_SUCCESS` opcodes, each with its own numbered suffix to differentiate between them), which basically tells a node to consider the script as valid and stop there. Hence, even if there was to be any kind of weird things breaking a consensus rule positioned in the stack after an `OP_SUCCESS`, a transaction should still be considered as valid, as nodes should exit the script and consider it valid as soon as they encounter the `OP_SUCCESS`.

This rule is specifically stated in {{<newtabref href="https://bips.xyz/342" title="BIP342">}} (emphasis mine:)

> If the initial stack as defined in BIP341 (i.e., the witness stack after removing both the optional annex and the two last stack elements after that) violates any resource limits (stack size, and size of the elements in the stack; see "Resource Limits" below), fail. **Note that this check can be bypassed using OP_SUCCESSx**.

This is precisely what btcd did wrong: it didn't really stop at the `OP_SUCCESS` and still performed checks it shouldn't have done. The check that failed and hence marked the transaction as invalid for nodes running btcd was the one on the maximum number of witness items per input, which was limited to 500,000 (more on that later). With 500,001 empty `PUSH` items in the witness data, btcd logically considered the transaction as invalid, and hence the block. All nodes running btcd fell out of sync with the rest of the network.

There are two "funny" things about this bug:
- the transaction that triggered it was valid but non standard. Standardness defines whether nodes on the network will relay a transaction. It means that to have the transaction mined, Burak probably contacted the miner offband to submit the transaction (and its lucrative fee) to them ;
- even before Taproot and `OP_SUCCESS`, it was already possible to trigger a similar consensus bug in btcd, at the exact same spot. Indeed, as Peter Wuille obserbed, btcd was always checking this 500,000 items limit, although it shouldn't if the version byte is 1 to 16. Such a transaction would be non standard as well.

The bug has been quickly {{<newtabref href="https://github.com/btcsuite/btcd/pull/1907" title="fixed">}} by Elle Mouton (in French we'd say *"encore Elle ?"*), by increasing the maximum items per input from 500,000 to 4 million, which is an upper bound that shouldn't be triggered anymore given the blocksize limit itself is 4 million bytes. LND, which depends on btcd, quickly {{<newtabref href="https://github.com/lightningnetwork/lnd/releases/tag/v0.15.4-beta" title="released">}} the fix. It is strongly advised to update asap.

This move by Burak attracted a lot of criticism (for example {{<newtabref href="https://nitter.lacontrevoie.fr/KLoaec/status/1587441654730031105" title="here">}} or {{<newtabref href="https://nitter.lacontrevoie.fr/Snyke/status/1587464627260121089" title="here">}}), given the fact that it doesn't follow any form of responsible disclosure. The bug itself was detected and {{<newtabref href="https://nitter.lacontrevoie.fr/_chjj/status/1588399431191101440" title="disclosed">}} by {{<newtabref href="https://nitter.net/ajtowns" title="Anthony Towns">}} a few weeks prior to the events, but it isn't as easy as "let's push the fix" in the open source world. Given that the change required to fix the bug is very small, it would have been noticed if btcd/LND developers had fixed it right away, and could hence have been exploited on nodes that didn't make the upgrade quickly enough. Hence, while developers were aware of the bug, their {{<newtabref href="https://nitter.lacontrevoie.fr/roasbeef/status/1587478619131023360" title="approach">}} was to bundle the fix with an incoming release to avoid raising suspicions. This decision was also encouraged by the fact that the offending transaction had to be non standard, thus lowering the chances of an exploit happening in the meantime.

Some {{<newtabref href="https://nitter.net/lightningdevkit/status/1587939344530145280" title="versions">}} of rust-bitcoin seem to have been impacted by a similar bug, in turn impacting LDK and {{<newtabref href="https://github.com/romanz/electrs/issues/783" title="Electrs">}} which depend on it.

### Hosted Channels Improvement Proposal Merged in the blips Repo

The {{<newtabref href="../what-are-hosted-channels/" title="Hosted Channels">}} improvement proposal was {{<newtabref href="https://nitter.lacontrevoie.fr/fiatjaf/status/1587133582161711104" title="merged">}} into the {{<newtabref href="https://github.com/lightning/blips/blob/master/blip-0017.md" title="bLIPs">}} (Bitcoin Lightning Improvement Proposals). While BOLTs specify features that are intended to be universally implemented accross Lightning implementations, bLIPs can be seen as specifications for features that don't need such a strong level of deployment accross the network, although community consensus is still required for a proposal to be merged to the bLIPs repository.

## Closing Bit

-- Quelle est cette langue nouvelle que vous parlez ?\
Vient-elle des Amériques ?\
-- Non, ma bonne dame, répondis-je.\
Elle vient d'un espace bien au-delà des mers\
Où toutes sortes de choses sont possibles.

---

If you enjoyed this recap, you can show your appreciation by throwing a few coins to *fanis @ lnmarkets.com*, by scanning or clicking the QR code.

Thank you!

{{<figure align=center src="../../images/lnm_lnurl.png" link="lightning:fanis@lnmarkets.com">}}
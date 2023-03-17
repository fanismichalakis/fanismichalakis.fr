---
title: "Latest Strikes 14"
date: 2022-12-13T13:30:00+01:00
block: "767207"
cover:
    image: "../images/EfficientJusticeHypothesis.min.png"
    alt: "A giant is lifting up one plate of a scale of justice, distorting the judgment of the souls placed in it"
    caption: "'Efficient Justice Hypothesis' (FR: 'Justice Libre et Parfaite'). Generated with DALL·E."
    relative: "false"
tags: ["bitcoin", "lightning"]
categories: ["strikes"]
draft: false
---

A new point of sale app linked to Bitcoin Beach Wallet, the winners of the LegendsOfLightning tournament announced, faster, easier and cheaper remittances ... This week in Lightning was, as usual, busy and well-filled. Read further to find out more, and remember: if you want to receive your weekly recap in your inbox before anyone else, all you have to do is subscribe {{<newtabref href="https://blog.lnmarkets.com" title="here">}}. Ready? Let's dive in!

## Wallets & Tools

### Cashu In LNBits

Everyone can {{<newtabref href="https://nitter.net/callebtc/status/1600926923554971648" title="now">}} easily be their own Chaumian Ecash mint with the integration of {{<newtabref href="https://fanismichalakis.fr/posts/latest-strikes-2/#cashu" title="Cashu">}} into {{<newtabref href="https://lnbits.com/" title="LNBits">}}.

Having the ability to run a mint inside an LNBits instance makes a lot of sense: the way LNBits works is already custodial, where the money sent to a LNBits instance is *actually* sent to the Lightning node on top of which the instance runs. LNBits is "just" a toolkit to make it easy for anyone to run their own instance, and provide some Lightning services to others, be they clients, friends, neighbours or family.

With the {{<newtabref href="https://cashu.space" title="Cashu">}} plugin, it is now possible to provide an additional service: the added privacy of chaumian e-cash, supercharged by the ability to send funds between mints through the Lightning Network, without any additional risk or trust assumption than those that arise when using someone else's LNBits instance.

It makes even more sense to have Cashu in LNBits, as that means that any mint created on an LNBits instance will natively be connected to Lightning through the instance's channels, thus strengthening the case for cross-mint interoperability through Lightning.

### Phoenix Release

Eclair published {{<newtabref href="https://github.com/ACINQ/phoenix/releases/tag/android-legacy-v1.4.24" title="version 1.4.24">}} of their {{<newtabref href="https://phoenix.acinq.co" title="Phoenix">}} wallet, which brings the wallet in compliance with the LNURL specification when it comes to authentication. Indeed, {{<newtabref href="https://github.com/lnurl/luds/blob/luds/04.md" title="LUD4">}} specifies that the whole domain of the authentication endpoint must be taken into account for key derivation, while Phoenix used to consider only the main domain. For example: `lnmarkets.com` instead of `api.lnmarkets.com`.

To ensure backward compatibility (eg. users still being able to login to their accounts on various services), Phoenix will still use the main domain instead of the whole domain for a {{<newtabref href="https://github.com/ACINQ/phoenix/compare/android-legacy-v1.4.23...android-legacy-v1.4.24#diff-524c60b96f4f0b4c0f9441bd7c35210370d06a86b608697bc450db41c28a7b8bR168" title="few">}} impacted websites.

*What role does the domain name play in LNURL-Auth? One of the great things about LNURL-Auth is that it doesn't directly use one's Lightning node pubkey for authentication, but rather derives a new key for each service. This way, two different services will know the same node/wallet as two completely different entities, and won't be able to tell that it's actually the same person. On the other hand, we want users to be able to login using the same key everytime they connect to the same service, in order to access their account. Hence the logical choice to use the service's domain to derive a child key from the node's seed.*

### Alby Release

The Alby team {{<newtabref href="https://github.com/getAlby/lightning-browser-extension/releases/tag/v1.20.0" title="shipped">}} a new release, which adds support for encrypted messages on Nostr, fixes some bugs (I'm looking at you, {{<newtabref href="https://github.com/getAlby/lightning-browser-extension/issues/1790" title="YouTube handles">}}) and paves the way for the next release, which is set to be a big one.

### Lightning Cash Register By Galoy

{{<newtabref href="https://galoy.io" title="Galoy">}} published a {{<newtabref href="https://nitter.lacontrevoie.fr/GaloyMoney/status/1600187125642600448" title="blog post">}} announcing a new tool for merchants called the Lightning Cash Register. It allows merchants to easily create a web page from which their staff can create invoices and accept Lightning payments - and nothing more. Thus, the manager can trustlessly let the staff handle the receiving of Lightning payments without fear that a mistake (or something more nefarious) ends up removing money from their account.

The Lightning Cash Register works together with Bitcoin Beach Wallet: the manager can get their register's link from their wallet's settings, and then open it in any browser. Many employees can use the same link at once, and the money will automatically be sent right to the manager's wallet - from which only them can spend.

## Ecosystem

### BoltFun Finals

The LegendsOfLightning tournament by {{<newtabref href="https://bolt.fun" title="BoltFun">}} is {{<newtabref href="https://nitter.lacontrevoie.fr/boltfun_btc/status/1600585864060755968" title="over">}}! The first place was awarded to {{<newtabref href="https://lightsats.com/" title="Lightsats">}}, followed by {{<newtabref href="https://makers.bolt.fun/project/agrimint" title="Agrimint">}} and {{<newtabref href="reckless.mutinywallet.com" title="Mutiny">}} (we already covered this projects in Latest Strikes: {{<newtabref href="../latest-strikes-5/#onboarding-nocoiners-to-bitcoin--lightning" title="here">}}, {{<newtabref href="../latest-strikes-8/#designathon-results" title="here">}} and {{<newtabref href="../latest-strikes-12/#who-needs-a-lightning-wallet-when-you-have-a-browser" title="here">}}). Then comes {{<newtabref href="https://lnvpn.net/" title="LNVPN">}}, a very cool VPN provider that only accepts Lightning, and {{<newtabref href="https://nolooking.chaincase.app" title="Nolooking">}} at the fifth position ('member {{<newtabref href="../latest-strikes-8/#lightning-payjoins" title="them">}}?). {{<newtabref href="https://bitpayroll.vercel.app/" title="BitPayRoll">}} (payroll platform for companies paying their employees in Bitcoin) and {{<newtabref href="https://makers.bolt.fun/project/saving-satoshi" title="Saving Satoshi">}} (a cool sci-fi game to learn about Bitcoin coding) complete the podium.

Congratulations to the winners and to all the other projects and builders. I must say it was really inspiring for me to follow along the tournament, and I'm really looking forward to what happens in the BoltFun community in 2023.

### Emeralize

Santos Hernandez {{<newtabref href="https://nitter.lacontrevoie.fr/5antoshernandez/status/1601962552975581187" title="announced">}} Emeralize, an online learning platform using Lightning as its payment rails, and payments to compensate creators and reward learners. We don't know much yet about what Emeralize will look like when it's out, but you can already check out Santos' vision and what problems he aims to solve.

### Strike x Bitnob

Strike and Bitnob {{<newtabref href="https://www.businesswire.com/news/home/20221206005453/en/Strike-Launches-Lightning-Fast-Money-Transfers-to-Africa" title="announced">}} their partnership, which aims at greatly reducing the cost of remittance to African countries such as Nigeria, Ghana and Kenya (those are the countries concerned, for now).

It was always possible to send money from Strike to Bitnob, so the news left me a bit wondering at first. But the truth is, it's wasn't that easy yet for a Nigerian to instantly receive money in their own currency (Naira), even so in their bank or mobile money account. It's precisely this last steps that this partnership aims to solve: someone in America can send dollars to their familiy in Africa, and the money will arrive straight to their bank account. The payment goes through the Lightning Network at the speed of light, and Strike and Bitnod handle currency conversions and interconnection with local financial entities (bank, mobile money or Strike/Bitnob account).

### List Of Altruistic Watchtowers

Looking for a watchtower to connect to? A {{<newtabref href="https://nitter.net/SwissRouting/status/1599857943263858689" title="list">}} of altrustic watchtowers is being built {{<newtabref href="https://github.com/talaia-labs/rust-teos/discussions/158" title="here">}}.

*What is a watchtower? In Lightning, your node must always be online in order to be able to watch the chain and detect when one of your channels is closed. This way, if the close is fraudulent (eg. your peer tries to get on-chain more than their fair share by publishing an old, revoked state), your node can punish them by publishing a Justice Transaction, effectively claiming all the funds in the channel for yourself. A watchtower is a service to which you can externalise this "watch and strike" activity so that, if your node was to go offline for any reason, your funds would still be safe.*

## Closing Bit

*(continued from {{<newtabref href="../latest-strikes-10/#closing-bit" title="Latest Strikes 10">}})*

Vous souvient-il de l'âne dont nous causions tantôt?\
Il lui est arrivé quelque étrange accident\
Il se sentait fort bien, drappé d'un bel égo\
Quand survint une affaire au terme embarassant.

Il paissait tranquillement, comme à son habitude\
Ecarquillait les yeux et brayait de concert\
Quand il fut annoncé qu'un ami, un confrère,\
Avait par trop reçu de bons de gratitude.

Bien sûr l'âne à tout va crie son étonnement\
Assure que l'âne noir est un cas isolé\
Qu'en aucun cas ne faut en généraliser\
Une règle commune à toutes les juments.

La foule est apaisée : justice sera rendue !\
Et de cette âpre épreuve notre âne ressort plus sûr\
Que l'on peut bien prêcher sans être convaincu,\
Recevoir le tribut sans les éclaboussures.

---

Want to receive Latest Strikes straight to your inbox every week? Couldn't be easier: subscribe to {{<newtabref href="https://blog.lnmarkets.com" title="LN Markets Ghost blog">}} and you're all set (remember to confirm your subscription by clicking the link sent via email).

---

If you enjoyed this recap, you can show your appreciation by throwing a few coins to *fanis @ lnmarkets.com*, by scanning or clicking the QR code.

Thank you!

{{<figure align=center src="../../images/lnm_lnurl.png" link="lightning:fanis@lnmarkets.com">}}
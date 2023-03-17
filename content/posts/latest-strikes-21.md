---
title: "Latest Strikes 21"
date: 2023-01-31T17:30:00+01:00
block: "774472"
cover:
    image: "../images/TheEndlessRace.min.png"
    alt: "A colorful illustration of Mario running on a Moebius loop."
    caption: "\"The Endless Race\". Generated with DALL·E."
    relative: "false"
tags: ["bitcoin", "lightning"]
categories: ["strikes"]
draft: false
---

Hello it's a me! Welcome to the 21st edition of Latest Strikes, your weekly recap in the turmoils of the Lightning world. Last week was a bit like a Super Mario level: full of exciting stuff and with plenty of Goombas to smash!

## Ecosystem

### Lightning 🤝 Nostr

If you've been following up with the Bitcoin ecosystem lately, there are good chances that you've heard about nostr, a novel yet simple protocol for exchanging signed text messages in a decentralized fashion. I'm quite a nostr fan myself and, even if I try to keep Latest Strikes as Lightning-focused as possible, I realized crawling back in the archives that I mentioned it a few times already - the earliest mention being in {{<newtabref href="../latest-strikes-5/#alby-release-and-nostr-soon" title="October 2022">}}.

This week was, like many others before, a great illustration of the synergies between Lightning and Nostr:
- River {{<newtabref href="https://nitter.lacontrevoie.fr/River/status/1618991159568924673" title="showcased">}} how seamless it is to send sats to someone on Damus, an iOS (and MacOS) nostr client, using the River app. This also works with a variety of Lightning wallets, including Strike, CashApp, Phoenix, Breez, Zeus, Blixt, and many more. You'll have to choose which one to use the first time, but can setup a default for ease of use as shown in the video ;
- speaking of Lightning wallets, Breez's CEO Roy is {{<newtabref href="https://stacker.news/items/126488" title="calling">}} for Flutter devs who want to implement some nostr functionalities into Breez, such as a login method (a bit like LNURL-Auth, but with nostr keys), podcast comments or even a full nostr client ;
- Kollider {{<newtabref href="https://nitter.net/kollider_trade/status/1618280777124573189" title="showed">}} how nostr can be used as a notification mechanism, here to let you know privately when you've received a payment on your account ;
- one of the great use cases of Lightning (microtransactions and tipping) comes in very handy when integrated into social media apps. We already saw a few lines above how seamless it can be thanks to wallets integrations and deep links, but some devs want to bring it a step further with {{<newtabref href="https://nitter.lacontrevoie.fr/jb55/status/1618023666134167554" title="Zaps">}}, a new nostr note type representing a Lightning invoice receipt that is sent by the receiving node once the payment settles. This allows for various use cases, such as:
    - displaying sats tipped to a specific post or profile,
    - showing whether an invoice has already been paid or not (pretty useful to prevent {{<newtabref href="../latest-strikes-11/#routing-node-extracted-value-rnev" title="preimage stealing">}}),
    - commerce over nostr,
    - etc.

Edward Snowden seems to agree, as he {{<newtabref href="https://iris.to/#/post/note1scags6u8fre3rhyc9h457wdrhu0r2c0h4t4e4d4nrwsjj6mcg2qqc2k7am" title="stated">}} on nostr that he had never seen Bitcoin "feel as powerful as it does on Nostr". And Snowden to add:

> The instant, effectively-free transactions that spring from having so many people on Lightning Addresses is like arriving on a different planet. 

I couldn't agree more. By the way, in case you hadn't guessed already, you can find me on nostr at npub1fanjsgy7jghu7d3l5hfq79a3c9kt959x638d5qhjmeeseyr7xp2qert4f0.

### More Lightning Payments In Brick And Mortar Businesses

Lightning is a payment technology. We should hence celebrate every piece of Lightning adoption in real-life commerce, and last week saw some good improvements in this regard.

Strike just {{<newtabref href="https://nitter.net/jackmallers/status/1618731420998049798" title="announced">}} the beginning of a 90-days open pilote in partnership with Clover. Clover sells Point-of-Sale (POS) hardware and software, and Strike's integration into their terminals allows for any merchant using Clover's system to receive Lightning payments, from any wallet (e.g., not just Strike wallets).

During the 90 days trial, voluntary merchants can contact Strike to be onboarded to the Strike integration ; while the speed, cost and ease of payment, as well as actual customer demand for Lightning payment, will be closely monitored by Clover and Strike in order to assess whether Strike could join Clover's {{<newtabref href="https://www.clover.com/appmarket" title="apps marketplace">}}, or even be directly integrated into Clover's products.

👉 More on this in {{<newtabref href="https://bitcoinmagazine.com/business/clover-integrates-bitcoin-lightning-with-strike" title="Bitcoin Magazine">}}.

On a slightly smaller scale, I was happy to see that Bitcoin-themed NYC bar PubKey {{<newtabref href="https://nitter.lacontrevoie.fr/PubKey_NYC/status/1619033489114021888" title="finally">}} accepts Bitcoin, thanks to Zeus' POS software, and that people already {{<newtabref href="https://nitter.net/TryggBTC/status/1619818315161165827" title="use it">}}. Neat! 

### Bitcoin In Super Mario On NES

Christian Moss literally put {{<newtabref href="https://nitter.lacontrevoie.fr/MandelDuck/status/1617929446157320193" title="Bitcoin into the NES">}}: each time you collect a coin in Super Mario, it instantly sends you 10 sats over Lightning. Very cool, and I can't wait to see what this enables for conferences, venues or even esport tournaments.

## Wallets & Tools

### Channels Of Prominent Wallet Vanish Into The Blue

Seems like BlueWallet faced some trouble with their Lightning node last week. The situation isn't clear because BlueWallet didn't make any public statement and even deleted their tweet in response to {{<newtabref href="https://nitter.net/hi__im__dave/status/1619680373314813953" title="this node runner">}} experiencing forced channel closures.

Taking a look at gossip data (for example on {{<newtabref href="https://amboss.space/node/02c3be1b43f90f089fddeff84014dca38fd0f6ab4224dbf6c18a5e36d55d7917cc" title="Amboss">}}), we can see that both channel count and capacity heavily dropped on January 29th, and are now starting to increase again.

The now deleted tweet stated that this channel force closes were due to BlueWallet's LND node crashing. What's certain is that a public announcement would be welcomed, as many node runners might have some funds in limbo right now.

### LNBits Release

LNBits shipped version {{<newtabref href="https://github.com/lnbits/lnbits/releases/tag/0.9.6.1" title="0.9.6.1">}} and the subsequent version {{<newtabref href="https://github.com/lnbits/lnbits/releases/tag/0.9.7" title="0.9.7">}} (which was a minor release updating Docker images and dependencies version). This brought some bug fixes and improvements to LNBits core components, as well as some new extensions, such as the new Gerty app that connects to this very cute {{<newtabref href="https://shop.lnbits.com/product/gerty-a-bitcoin-assistant" title="hardware">}} to display information about Bitcoin and Lightning networks (such as block height, network wide Lightning announced capacity, blocks until next difficulty adjustment, etc.).

One day after the new version release, a very cool pull request was {{<newtabref href="https://nitter.lacontrevoie.fr/lnbits/status/1618655492884287488" title="merged">}} that will separate extensions from LNBits' core. The LNBits team will still maintain a list of vetted extensions, but users will be able to create their own collections, and all extensions will now live in their own code repository, from where they can be pulled and are more easily and independently maintainable.

### Eye Of Satoshi v0.2.0 Pre-Release

Talaia Labs published a first {{<newtabref href="https://github.com/talaia-labs/rust-teos/releases/tag/v0.2.0-rc1" title="release candidate">}} for the v0.2.0 of their Lightning Watchtower software. This update brings improvements to both the daemon and the client, a notable one being the ability to run the daemon on top of a pruned bitcoind node (no need to keep the entire chain, most of which is useless).

This is a pre-release version, so feedback from testers is welcomed!

### BTCPay Smol Release & Plugin Docs

Version 1.7.5 of BTCPay Server was {{<newtabref href="https://github.com/btcpayserver/btcpayserver/releases/tag/v1.7.5" title="released">}}, with several bug fixes and improvements, as well as a new Greenfield API to manage Lightning Addresses.

The project also published a new documentation {{<newtabref href="https://docs.btcpayserver.org/Development/Plugins/" title="page">}} detailing how to setup, but also how to code and deploy a plugin for BTCPay. Plugins for the win!

### Zap Revival

When it comes to using your own Lightning node to send and receive sats from your phone, the best wallet in my opinion is currently {{<newtabref href="https://zeusln.app/" title="Zeus">}}. But back in the days, I was also a huge fan of Zap, a very nice wallet connected to your own node, that stopped being maintained last year - or so I thought!

As far as I know, the Zap wallet was first developed by Strike, which halted it's development to focus on Strike's main business and solutions. It seems like former Zap developer Michael Wünsch took it upon himself to bring Zap back in the race, with a few new {{<newtabref href="https://github.com/LN-Zap/zap-android/releases/tag/v0.5.7-beta" title="features">}} and {{<newtabref href="https://github.com/LN-Zap/zap-android/releases/tag/v0.5.8-beta" title="fixes">}}. Let's see how this goes!

## Spec & Implems

### Monthly TARO Update

Interested in Taro? There's a public Taro development update call by Lightning Labs every month, and January's call took place last week! It was brilliantly summed up {{<newtabref href="https://nitter.net/GuerillaV2/status/1618676640883818497" title="here">}} by my friend Guillaume, so be sure to give it a read!

### anyprevout.xyz Is Out

The anyprevout.xyz domain has expired, and fiatjaf (who owned it) {{<newtabref href="https://nitter.lacontrevoie.fr/fiatjaf/status/1618035008694030342" title="announced">}} that they do not intent on renewing it. Its one page content, advocating for the soft fork and (notably) what it brings to Lightning (Eltoo for the win!) is still visible on this {{<newtabref href="https://archive.is/9obRm" title="archive">}}.

### Security Review of Validating Lightning Signer

Antoine Riard conducted a third party audit of the {{<newtabref href="https://vls.tech/" title="Validating Lightning Signer">}}, a project that aims at improving Lightning operational security by handling the signing operations in a separate device, where additional security checks can be performed (kind of like an {{<newtabref href="https://fr.wikipedia.org/wiki/Hardware_Security_Module" title="HSM">}}).

Overall, Riard found several vulnerabilities in the verifications performed by the Signer that could lead to theft/loss of funds in attacks of various complexity.

For example, the Signer accepts to open channels with the legacy `option_anchor_outputs` type, which is considered unsafe (or at least way less safe than `option_anchors_zero_fee_htlc_tx`) as it opens the way for fee siphoning attacks, where the peer can claim for themselves money that was supposed to pay for the channel commitment transaction fees[^1].

Another example is the exposition to time-sensitive attacks, where money can be stolen in-flight because the Signer doesn't no enforce safe practices in the difference between two consecutive routing hops timelocks.

Other attacks involve an attacker with low hashrate capabilities, where an attacking peer and miner can steal part of the channel value.

Riard's {{<newtabref href="https://lists.linuxfoundation.org/pipermail/lightning-dev/2023-January/003829.html" title="email">}} also describes other attack vectors and the link to the full {{<newtabref href="https://github.com/ariard/validating-lightning-signer/blob/main/VLS-audit-v0.2.pdf" title="audit report">}}. A huge and necessary work!

### Lightning Address Login

Last week Keyan from StackerNews made an interesting {{<newtabref href="https://github.com/lnurl/luds/issues/196" title="proposal">}} in the LUDs repository. LUDs are the "LNURL Documents", in other words the *specifications* of the LNURL protocols.

Keyan's proposal consists in using Lightning Addresses to initiate a LNURL-Auth login, in a similar way that they are used today as a proxy to LNURL-Pay payments. The major difference is that, unlike receiving a payment, authenticating to a service would require interaction from the user owning the Lightning Address (else, anybody with knowledge of your address could connect to services on your behalf, which is obviously not expected). Still, this could be preferable to the current LNURL-Auth mechanism (with a QR to scan or a string to copy/paste) in a variety of situations. For example, if the user runs their Lightning wallet on a separate computer with no camera, they might find it more convenient to input their (short) Lightning Address on the website and accept the authentication from the machine running the Lightning wallet when prompted for confirmation, with the click of a button.

## Closing Bit

Soudain l'air s'empourpre !\
Le vent a levé un banc de sable\
Pour que nous puissions nous y assoir.

---

Want to receive Latest Strikes straight to your inbox every week? Couldn't be easier: subscribe to {{<newtabref href="https://blog.lnmarkets.com" title="LN Markets Ghost blog">}} and you're all set (remember to confirm your subscription by clicking the link sent via email).

---

If you enjoyed this recap, you can show your appreciation by throwing a few coins to *fanis @ lnmarkets.com*, by scanning or clicking the QR code.

Thank you!

{{<figure align=center src="../../images/lnm_lnurl.png" link="lightning:fanis@lnmarkets.com">}}

[^1]: The way the attack works is that the peer can ask you to put higher fees with an `update_fee` message (which your node might accept, depending on its configuration). Those fees are deducted from the HTLC outputs, but the attacker is able to attach a new output to their commitment transaction that spends said fees to an address they control. This ability to non-cooperatively add ouputs to a commitment transaction is useful as a fee control mechanism (see this {{<newtabref href="../anchor-outputs/" title="article">}} on Anchor Outputs), but is used here as an attack vector. This attack is mitigated today by using another channel type called `option_zero_htlc_tx_fee` (the safe one), but that's a topic for another article.
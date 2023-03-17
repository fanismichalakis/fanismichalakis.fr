---
title: "Latest Strikes 27"
date: 2023-03-16T12:50:00+01:00
block: "781052"
cover:
    image: "../images/SplicingChannels.min.jpeg"
    alt: "A painting of farmers tending to irrigation paths, seen from above, as an allegory of Lightning Channel Splicing."
    caption: "\"Splicing Channels\". Generated with DALL·E."
    relative: "false"
tags: ["bitcoin", "lightning"]
categories: ["strikes"]
draft: false
---

How you doin'? Last week was a bit less tumultuous than the previous one, but there was still a lot happening. Let's unfold it together, shall we?

## Ecosystem

### Lightning Prisms

Gigi {{<newtabref href="https://nitter.lacontrevoie.fr/dergigi/status/1634905644154093569" title="published">}} an interesting article defining a novel payment flow called Lightning Prisms. The idea, initially brought up by Andrew Camilleri (aka {{<newtabref href="https://nostr.directory/p/MrKukks" title="MrKukks">}}) is to programmatically split the payments sent to an identifier (for example a Lightning Address) between other identifiers, which can be the final recipient of this split or yet another split to another set of identifiers, and so on.

The idea resembles what is currently done in the Podcasting2.0 ecosystem with *splits*, where the host of a show can fill in several Lightning public keys and attribute to each of them a percentage of the revenue share. A compatible podcast player will then automatically split any payment sent while listening to the episode between the various recipients[^1]. But it requires the host to change the episode metadata when they want to change the split, which works for the specific use case of podcasting but might not work so well for others.

With *prisms*, the "owner" of a prism can change the underlying value distribution as they see fit in order to reflect a change in the entity structure. For example, consider organisms such as {{<newtabref href="https://brink.dev/" title="Brink">}} or the HRF's {{<newtabref href="https://hrf.org/devfund" title="Bitcoin Development Fund">}}. Their job is to gather donations from the public and redistribute them among selected grantees. With *prisms*, they could set up an identifier that would automatically split any donation between the current grantees of a given program.

This, however, raises the question of transparency. In the aforementioned context of donations, senders would probably like to be able to see and verify that their money was indeed sent to the publicized grantees. On the other hand, other use cases will probably require more privacy regarding how the funds are split. Any implementation of *prisms* that aims at covering this variety of situations should have built-in mechanisms to enable custom levels of transparency.

While it is possible today to emulate *prisms* by using multiple LNBits extensions, a real implementation of the idea remains to be built. As Gigi highlights, the best way to have this would be at the protocol level (maybe using Botl12), but in the meantime having such schemes set up at the application level would allow for very welcomed explorations.

### New BoltFun Tournament

A new BoltFun {{<newtabref href="https://makers.bolt.fun/tournaments/2/overview" title="tournament">}} has begun! Projects building at the intersection of nostr and Bitcoin/Lightning can enter the competition until it ends on March 24th. At the time of writing, there are already 37 projects registered, from established Lightning open source initiatives developing nostr integrations (such as a new, nostr-enabled "Contacts" feature in {{<newtabref href="https://makers.bolt.fun/project/zeus" title="Zeus">}} wallet) to new ideas (such as a nostr-based marketplaces for {{<newtabref href="https://makers.bolt.fun/project/satsbounty" title="bounties">}} and {{<newtabref href="https://makers.bolt.fun/project/thegoodstr" title="goods">}} leveraging Lightning for payments).

Really looking forward to what will come out from this tournament! We will of course be looking into it when the contest ends, so be sure to {{<newtabref href="https://blog.lnmarkets.com/" title="subscribe">}} to the {{<newtabref href="https://lnmarkets.com" title="LN Markets">}} newsletter if you don't want to miss it!

### New THNDR Game

Lightning-native studio {{<newtabref href="https://www.thndr.games/" title="THNDR">}} came out with a new mobile {{<newtabref href="https://nitter.lacontrevoie.fr/THNDRGAMES/status/1633860310934142979" title="game">}} last week. Called "Bitcoin Blocks", it is a bit of a crossover between Tetris and Sudoku. This is the 6th game put forth by the studio, implementing the same earning mechanism as its predecessors: while playing, a user collects tickets that are automatically entered into an hourly draft. The more (and the better) the user plays, the more tickets they collect and the higher their chances of winning sats-denominated prizes. Sats won in game can then be withdrawn instantly and for free to an external Lightning wallet.

Wanna play? You can download the game {{<newtabref href="https://www.thndr.games/bitcoin-games/bitcoin-blocks" title="here">}} (or using this referral {{<newtabref href="https://blocks.thndr.games/r/s9iL" title="link">}} if you want to).

### LNRoom (Cool Education Project)

Last week I stumbled upon this cool educational {{<newtabref href="https://lnroom.live/" title="website">}} while browsing {{<newtabref href="https://nitter.lacontrevoie.fr/tonyaldon/status/1633144809442406401" title="Twitter">}}. LNROOM references 9 videos showcasing how to use Core Lightning from the command line, accompanied by extensive text resources. Very handy if you're beginning your journey with Blockstream's implementation of the Lightning Network!

### Blinded Paths Explanation

In the last issues of Latest Strikes I've been mentioning Blinded Paths every now and then without taking the time to give an in-depth explanation of how it works. Thankfully, Voltage got us covered and published an outstanding blog {{<newtabref href="https://voltage.cloud/blog/lightning-network-faq/what-are-blinded-paths-and-how-do-they-work/" title="article">}} dealing with the details of how Blinded Paths work and how it improves upon what we currently have in Lightning. Thank you guys!

### Arthur Hayes Reinvents Stablesats/Synthetic USD With A Twist

In a recent {{<newtabref href="https://entrepreneurshandbook.co/dust-on-crust-300d4b5cf3ec" title="post">}}, Arthur Hayes detailed how synthetic US dollars could be created using inverse perpetual swaps. If the idea sounds familiar, that's because it is: this is what {{<newtabref href="https://galoy.io/" title="Galoy">}} has been doing with {{<newtabref href="https://stablesats.com/" title="Stablesats">}} since more than a year, and what we're doing at {{<newtabref href="https://lnmarkets.com/en" title="LN Markets">}} with our {{<newtabref href="../latest-strikes-12/#synthetic-usd-in-ln-markets" title="Synthetic USD">}}. If it doesn't, let me explain how it works in a sentence: the idea is to both long (by holding it) and short (by opening a short position on a derivatives exchange) bitcoin at the same time. This way, whatever direction the price of bitcoin goes to, you win on one side what you lose on the other, thus resulting in a stable position when denominated in dollars.

Hayes' post describes how a DAO (Decentralized Autonomous Organization) could manage the "stablecoin", for example by defining which derivatives exchanges would be used, but in my opinion missed a crucial point: transferability. The great thing with Stablesats and its equivalents is that they are built on top of Lightning (e.g. using Lightning-native derivatives exchanges such as {{<newtabref href="https://lnmarkets.com/en" title="LN Markets">}} or {{<newtabref href="https://kollider.xyz/" title="Kollider">}}), meaning everything can happen without ever touching the Bitcoin chain. You send sats to a compatible wallet using Lightning, mint stablesats (eg. use sats to enter a derivatives position) and, should you want to transfer them, you can just exit the position and send the sats elsewhere. Because at any point no other token than sats was involved, stablesats inherit the marvelous transferability of sats themselves on Lightning[^2].

Finally, I must admit the title of this section was a bit *clickbaity*: Hayes didn't "reinvent" derivatives-based synthetic US dollars in 2023, he invented them back in {{<newtabref href="https://blog.bitmex.com/in-depth-creating-synthetic-usd/" title="2015">}}!

### c= Lightning Node Spotted

Remember the new c= Lightning entity TBD launched last week, with the announced intent to bring liquidity into the Lightning Network? Well, here is their Lightning {{<newtabref href="https://amboss.space/node/027100442c3b79f606f80f322d98d499eefcb060599efc5d4ecb00209c2cb54190" title="node">}}: after a little less than two weeks they already have 9 bitcoins of capacity, and seem to be accepting channels of any size.

### Lightning Conference In Norway

A Lightning {{<newtabref href="https://kongerik.et/" title="conference">}} will take place in Norway this week-end. On top of an intimate conference, the organizers also pulled a {{<newtabref href="https://bitcoinmagazine.com/industry-events/wild-at-northern-lightning-conference" title="rave">}}, with the goal to attract nocoiners who will have to use Lightning to pay for beers. Provided the onboarding is smooth enough, this might actually be a very good orange-pilling vector!

## Wallets & Tools

### Igor From BlueWallet On The Recent Events

{{<newtabref href="https://www.nostr.directory/p/raw_avocado" title="Alex Waltz">}} had the opportunity to {{<newtabref href="https://stacker.news/items/149049/r/FanisMichalakis" title="interview">}} BlueWallet's founder Igor Korsakov about the recent developments around the wallet, which we covered in {{<newtabref href="../latest-strikes25/#bluewallet-sunsetting-their-custodial-lightning-offering" title="Latest Strikes #25">}}.

Igor confirmed what we previously mentioned: a LDK node can already be found in the BlueWallet app, but you'll need to tap a few times at the right spot to enable it while the feature is still in beta, a bit like enabling developer mode on Android phones. Interestingly, what the BlueWallet team is currently busy figuring out is the LSP part: how to scale it up to thousand of users, how to price it so that it can be sustained in the long run, etc. This echoes nicely with Breez's Open LSP model we covered {{<newtabref href="../latest-strikes26/#the-breez-open-lsp-model" title="last week">}}!

### Zeus Release

The version 0.7.3 of Zeus is {{<newtabref href="https://nitter.lacontrevoie.fr/ZeusLN/status/1633834571019223045" title="out">}} of beta! On top of the new features we already described in {{<newtabref href="../latest-strikes-24/#zeus-update--point-of-sale-documentation" title="Latest Strikes 24">}} (importing QR Codes from the phone's gallery, display of pending and closed channels and a timer for on-going force closes, etc.), a notable improvement is a compatibility mode for LNURL-Auth when using Zeus with a LndHub backend.

LNURL-Auth is a protocol to authenticate to services online using one's Lightning wallet. For each service, identified by its domain (for example, https://lnmarkets.com) the wallet derives a new key from the root private key, and uses it to sign the authentication challenge submitted by the service. This means that for two different websites I will appear as two completely different users, even though I use the same wallet to authenticate into both. On the other hand, every time I use the same wallet to authenticate to the same website, it should log me into the same account. That's where things can get a bit tricky sometimes: a subtle variation in the way the LNURL-Auth protocol is implemented between two wallets can lead a user to access two completely different accounts when login in with LNURL-Auth in spite of using the same Lightning node (and hence the same root private key) in the backend. This, for example, happened when using a LndHub backend: using it through Zeus, BlueWallet or Alby wouldn't grant access to the same account. To solve this issue, the Zeus team created a {{<newtabref href="https://github.com/ZeusLN/zeus/pull/1305" title="compatibility mode">}}, where the user selects which "flavor" of LNURL-Auth they want to use depending on what account they're trying to access (e.g. which wallet they initially used when connecting to said account for the first time). And look which website they used to test their solution 👀.

### Alby Release

Version 1.28.0 of Alby is {{<newtabref href="https://github.com/getAlby/lightning-browser-extension/releases/tag/v1.28.0" title="out">}}.This new release ships a lot of improvements, of which a few are:
- {{<newtabref href="https://github.com/getAlby/lightning-browser-extension/pull/2000" title="detecting">}} the author Lightning Address in Substack posts and profiles, allowing for easy tipping (like is already the case in Medium or YouTube for example),
- a {{<newtabref href="https://github.com/getAlby/lightning-browser-extension/pull/2190" title="clearer">}} interface for setting up a connection through Tor to the node backend (useful for example when connecting Alby to an Umbrel node),
- an {{<newtabref href="https://github.com/getAlby/lightning-browser-extension/pull/2152" title="improved">}} experience when sending sats with LNURL, by taking into account the recipient's LNURL parameters (such as minimum and maximum sendable amounts).

### Some V4V Stats

The Podcast Index shared some {{<newtabref href="https://stats.podcastindex.org/v4v" title="stats">}} on the flow of sats inside the Value4Value podcasting ecosystem. The Podcast Index is an open, categorized directory of podcasts than any podcasting app can use.

This data only counts Value4Value payments where the Podcast Index is part of the split. Indeed, many podcasting apps such as Breez or Fountain attribute 1% of the split to the Podcast Index, which supports their action and enables them to draw those kind of statistics. It is hence a lower bound of the actual amounts, but still quite representative in my opinion as most Podcasting2.0 apps seem to include this voluntary 1% split to the Podcast Index.

That's some very nice figures, which Kevin Rooke {{<newtabref href="https://stacker.news/items/150534/r/FanisMichalakis" title="rearranged">}} to show them as an histogram over the last month. This ecosystem is definitely growing, and it's nice to see that there is a floor of users relentlessly sending value back to creators.

*In case the concept of Value4Value is new to you, I encourage you to read this awesome {{<newtabref href="https://dergigi.com/2021/12/30/the-freedom-of-value/" title="piece">}}.*

## Spec & Implems

### Splicing

Dusty Daemon's {{<newtabref href="https://github.com/ElementsProject/lightning/pull/5675" title="pull request">}} adding *splicing* to Core Lightning entered into the review phase. Splicing is a protocol update that will enable users to resize their channels on the go. Currently, the only way to change the size of a channel is to close it and reopen a bigger or smaller one, which means two on-chain transactions and some channel downtime. With splicing, it becomes possible to add or remove liquidity to or from a channel with only one on-chain transaction and without ever stopping the channel for more than a few seconds. On top of that, it is possible to batch multiple splicings, potentially from multiple nodes across the network, into only one Bitcoin transaction, thus saving even more blockspace and fees.

Splicing would also allow a wallet to only show one balance to the user, which is all inside a Lightning channel, and splice out whenever they need to send funds on-chain. In other words, you get to enjoy the instant settlement of Lightning as the default, but can still use on-chain whenever required without having to close your channel (and without any additional transaction than the one you'd already make given that you want to transact on-chain).

All those great features of splicing are especially useful for Lightning Service Providers (LSPs), which need to manage their liquidity across all the channels they have opened with their clients. For example, if you're using Phoenix today, the wallet will open a new channel whenever the amount you're trying to receive exceeds the current inbound liquidity of your channel(s). With splicing, it could dynamically adapt the size of the one and only channel they have with you, and potentially batch this resizing with others.

At the same time, wallets/LSPs that rely on submarine swaps to present their user with a unified balance while maintaining both Lightning and on-chain capabilities at the same time could use splicing instead, saving on fees and simplifying their liquidity management.

It seems that Eclair is also actively {{<newtabref href="https://github.com/ACINQ/eclair/commits/splices-20230303" title="working">}} on splicing. If you wish to go a little deeper into this rabbit hole, you can give Dusty's {{<newtabref href="https://www.youtube.com/watch?v=WxNlQflXhKo" title="presentation">}} at Adopting Bitcoin a watch.

### Closing Bit

Le bois craque, appelle, chante, pleure\
Il nous dit : tenez-vous prêts.\
J'annonce le printemps qui vient, le dégel\
La terre se réveille enfin.

---

Want to receive Latest Strikes straight to your inbox every week? Couldn't be easier: subscribe to {{<newtabref href="https://blog.lnmarkets.com" title="LN Markets Ghost blog">}} and you're all set (remember to confirm your subscription by clicking the link sent via email).

---

If you enjoyed this recap, you can show your appreciation by throwing a few coins to *fanis @ lnmarkets.com*, by scanning or clicking the QR code.

Thank you!

{{<figure align=center src="../../images/lnm_lnurl.png" link="lightning:fanis@lnmarkets.com">}}

[^1]: What actually happens is that the player app makes multiple payments automatically. It leverages *keysend*, which allows to send sats directly to a Lightning node without the need for an invoice.

[^2]: With the additional round of having to exit the derivatives position, but that's where having Lightning-native derivatives exchanges comes in handy.
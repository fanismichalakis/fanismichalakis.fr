---
title: "Latest Strikes 13 - December 4th"
date: 2022-12-06T00:50:00+01:00
block: "766066"
cover:
    image: "../images/DALL·E 2022-12-06min.png"
    alt: "Cyberpunk pirate space ship with orange solar sails, in the neighborhood of a moon, dark stellar background, digital art"
    caption: "'Cyberpunk pirate space ship with orange solar sails, in the neighborhood of a moon, dark stellar background, digital art'. Generated with DALL·E."
    relative: "false"
tags: ["bitcoin", "lightning"]
categories: ["strikes"]
draft: false
---

## Ecosystem

### Lightning (And Email) Addresses In Vida

Lightning Addresses are {{<newtabref href="https://nitter.net/lylepratt/status/1599056998783295488" title="now">}} a thing in {{<newtabref href="https://vida.page" title="Vida">}}, and every user gets one (it's basically \<your-username\>@vida.page, so for example mine is fanismichalakis@vida.page). But where it gets really interesting is that each Lightning Address is also a paywalled email address. To reach you via email, someone would therefore have to pay the same amount as the one for a one minute call.

I really like the idea of merging Lightning and Email addresses (although it won't make dealing with mailto: and lightning: prefixes easier). The only thing that is a bit frustrating here is that the sender is required to setup a Vida account in order to pay and get the mail to your inbox, rather than being able to simply scan a QR Code or copy-paste an invoice.

*By the way, this feels like a good opportunity to let you know I have a Vida {{<newtabref href="https://vida.page/fanismichalakis" title="page">}} myself. I'll always answer Twitter DMs anyway, but if you which to reach me more quickly or just support my work, this might be a good way (wink wink).*

### BoltFun Finalists Announced

BoltFun announced the finalists of the Legends of Lightning tournaments, with 2 categories ({{<newtabref href="https://nitter.lacontrevoie.fr/boltfun_btc/status/1597302886803070977" title="Building for Africa">}} and {{<newtabref href="https://nitter.net/boltfun_btc/status/1597303111319982080" title="Global Adoption">}}) and 8 projects selected for each. Among the finalists are some projects that we already met in Latest Strikes, such as {{<newtabref href="https://btcmap.org" title="BTC Map">}}, {{<newtabref href="https://lightsats.com/" title="Lightsats">}}, {{<newtabref href="https://reckless.mutinywallet.com/" title="Mutiny Web">}} or {{<newtabref href="https://nolooking.chaincase.app/" title="nolooking">}}. We also met {{<newtabref href="https://makers.bolt.fun/project/agrimint" title="AgriMint">}} from the "Building for Africa" track when it won the {{<newtabref href="../latest-strikes-8/#designathon-results" title="Designathon">}} back in October.

I'll let you check out all the finalists by yourself, but I must confess I remain amazed by how much talent and creativity bitcoiners have. From {{<newtabref href="https://makers.bolt.fun/project/afromnemonics" title="Afromnemonics">}} (BIP39 wordlist in Swahili -- 200 million speakers worldwide!) to {{<newtabref href="https://makers.bolt.fun/project/sats2data" title="Sats2Data">}} (it's in the name: turn sats into mobile data and airtime), all the projecs are really inspiring!

Don't forget to {{<newtabref href="https://nitter.net/boltfun_btc/status/1599824882233413632" title="tune in">}} tomorrow for the finals, starting at 14:45 UTC.

### SlashTag Authentication In Some Places

{{<newtabref href="https://slashtags.to/" title="Slashtags">}} are a new kind of "identity" that allow you to create passwordless accounts, send and receive money from and to "contacts", subscribe to personnalized data feeds, and so on. They are currently only supported by the {{<newtabref href="" title="BitKit">}} wallet, and authenticating via Slashtag is {{<newtabref href="https://nitter.net/LNMarkets/status/1598282839946317824" title="now">}} supported on {{<newtabref href="https://auth.starbackr.com/" title="Starbackr">}} and {{<newtabref href="https://lnmarkets.com/en/register" title="LN Markets">}}, alongside LNURL-Auth.

### You Can Now Charge Your EV With Sats In Europe

{{<newtabref href="https://satimoto.com" title="Satimoto">}} launched in Europe, with more than 20,000 locations covered in many countries. If you manage to get on the early access (or to wait a bit), Satimoto will allow you to charge your electric vehicle with sats, without any registration, KYC nor custody of funds. Some bitcoiners are already tring it {{<newtabref href="https://nitter.lacontrevoie.fr/jokoono/status/1597931132896550914" title="in the wild">}}. ⚡

Btw, pretty cool privacy policy on the website.

### StackerNews: Sats Now Affect Ranking

You may have thought (like me) that it was already the case, but sats {{<newtabref href="https://stacker.news/items/98002" title="now">}} affect ranking on StackerNews. The release post gets into more details as to how exactly sats impact ranking, but the key things to remember are other parameters (such as trust) still influence ranking, and that the effect of sats is logarithmic (ten times more sats only raises the ranking score by 1). Also, StackerNews will now take 10% of every tip in order to prevent sybil attacks, where someone could propel themselves to the top for free by simply tipping themselves with a secondary account.

I'm not yet sure sats tipped are the best way to measure the quality of content, but it's definitely worth giving a try!

## Wallets & Tools

### Anonsats

{{<newtabref href="https://hackmd.io/@anonsats/SJDzzRR4i" title="Anonsats">}} is a "Chaumian ecash payment and settlement system" that leverages Bitcoin, Lightning, LNBits and {{<newtabref href="../latest-strikes-2/#cashu" title="Cashu">}} to enable users to send and receive money with increased privacy, with the notable drawback of giving up the self-custody of their funds.

Users can create a new wallet on a custodial instance (*a la* LNBits) and send sats to this new wallet, for example using the included Lightning Address. They can then send the funds anywhere, or convert them to Cashu tokens. Cashu tokens can then be sent natively between users of the same mint (eg, server), or even sent to a different mint, through Lightning.

A cool feature, derived from the custodiality of this setup, is that users can access their wallet from anywhere as long as they have an internet connection (for example, from a {{<newtabref href="https://nitter.net/anonsats/status/1598661711732555776" title="demo machine in an Apple store">}}). On the privacy front, users profit from the strong privacy guarantees of Cashu and Chaumian e-cash. But all that requires trusting the central server.

You can give it a try {{<newtabref href="https://asats.io/anonsats/docs" title="here">}}, but keep in mind it's still alpha software, so only send tiny amounts you're prepared to lose.

### Zeus Prerelease

Testers wanted! Zeus v0.7.0-alpha1 is {{<newtabref href="https://nitter.lacontrevoie.fr/ZeusLN/status/1598715539777536002" title="out">}}, with some cool new feature such as {{<newtabref href="https://lightning.engineering/posts/2021-11-30-lightning-node-connect-deep-dive/" title="Lightning Node Connect">}} and {{<newtabref href="https://bitcoinqr.dev" title="Unified QR Codes">}}. The prerelease also includes UX enhancements and bug fixes.

## Specs & Implems

### New Minor LND Release

LND vO.15.5-beta is {{<newtabref href="https://nitter.net/roasbeef/status/1598480763808542720" title="here">}}, with a bunch of bug fixes. Notably:
- a bug in Taproot key tweaking that affected remote signing setups,
- an unnecessary CPU activity when waiting for a peer's `funding_locked` message, before announcing the channel to the rest of the network (fix consists in waiting 1 second between each check of whether we received the peer's message or not),
- the wallet birthday wasn't correctly taken into account when creating a watch-only wallet, prompting the wallet to rescan the whole chain instead of just the useful portion from the wallet's birthday to now.

### Core Lightning v.22.11

With this new release, Core Lightning changes its versioning scheme for a date-based one (22.11 stands for November 2022) but keeps its very funny naming policy. Core Lightning v22.11, named "Alameda Yield Generator", comes with a number of new features, bug fixes and enhancements.

This {{<newtabref href="https://blog.blockstream.com/core-lightning-v22-11-alameda-yield-generator/" title="blog post">}} goes into some details for a few of them, and is very pleasant to read. To put it in a nutshell:
- a new standalone pluging manager called "reckless" comes into town, allowing node operators to install and start new plugins with one command (no more git cloning and config editing),
- the autoclean tool has become more powerful, helping operators keep their node strong and fast.

You can scroll through the full {{<newtabref href="https://github.com/ElementsProject/lightning/blob/master/CHANGELOG.md#2211---2022-11-30-alameda-yield-generator" title="release notes">}} to see all the changes. You'll see for example that, following its {{<newtabref href="../latest-strikes-4/#getting-rid-of-legacy-lightning-onion-format" title="eradication">}} from the BOLTs, the legacy onion format is also bowing out from Core Lightning.

### Eclair v0.8.0

A new release of Eclair has {{<newtabref href="https://github.com/ACINQ/eclair/blob/master/docs/release-notes/eclair-v0.8.0.md" title="landed">}}! Version 0.8.0 includes three new features, a breaking change, and lots of improvements and bug fixes:
- make "private" (I mean, unannounced) channels even more private. With channels aliases, you can give channels arbitrary identifiers, as long as your peer supports them as well. This way, you don't have to leak the underlying UTXOs of your unannounced channels in routing hints anymore. Great for privacy!
- in the midst of the Full-RBF debate, zero-conf channels make their apparition in Eclair. They allow users to consider a channel as usable as soon as the funding transaction is published, without having to wait for confirmations. Because of the trust implications of zero-conf channels, they are disabled by default and can only be enabled on a peer-by-peer basis, allowing you to activate them only with peers you trust (enough),
- experimental support for dual-funding: if your peer supports it and you enabled this opt-in feature, your channel open will automatically use dual-funding, where both peers can contribute funds to the channel funding and the funding transaction can be fee bumped with RBF. However, note that in this first version, the "dual" aspect only concerns fee-bumping, as it is not yet possible for the non-initiator to contribute funds to the channel (soon™),
- Eclair v0.8.0 requires Bitcoin Core v23 or higher, dropping support for earlier versions (that's the breaking change). Note that you may need to change your Bitcoin Core configuration if not done already, so that Core only generates SegWit addresses, notably for change.

## Research & Papers

### A New Website For Lightning Privacy

Tony Giorgio, {{<newtabref href="https://nitter.lacontrevoie.fr/futurepaul" title="futurepaul">}}, {{<newtabref href="https://nitter.net/benthecarman" title="Ben Carman">}}, {{<newtabref href="https://nitter.lacontrevoie.fr/evankaloudis" title="Evan Kaloudis">}} and {{<newtabref href="https://nitter.net/HillebrandMax" title="Max Hillebrand">}} published a new {{<newtabref href="https://lightningprivacy.com/en/introduction" title="resource">}} on Lightning privacy, covering on-chain privacy "contagion", routing analysis and what {{<newtabref href="https://fanismichalakis.fr/posts/latest-strikes-2/#blinded-routes-in-eclair" title="Blinded Paths">}} and Trampoline Routing bring to the table.

Together with this {{<newtabref href="https://abytesjourney.com/lightning-privacy/" title="piece">}} by Toni Giorgio, and this {{<newtabref href="https://github.com/t-bast/lightning-docs/blob/master/lightning-privacy.md" title="one">}} by Bastien Teinturier, this new website is a highly recommended read!

### DLCs On Lightning (On Mainnet)

{{<newtabref href="https://cryptogarage.co.jp/" title="Crypto Garage">}} announced that they successfully opened and closed the {{<newtabref href="https://medium.com/crypto-garage/dlc-on-lightning-cb5d191f6e64" title="first mainnet Lightning channel embedding a DLC">}}.

A DLC is a channel between two peers (kind of like a Lightning channels) where the repartition of funds in the end depends on a specific result, provided by a well-determined oracle. With DLCs, one can take part in sophisticated "contracts" (betting, trading, etc.) without giving up the custody of their coins.

However, DLCs on-chain don't scale very well, as each new contract (for example, betting on the price of Bitcoin tomorrow) requires setting a new DLC (one on-chain transaction) and resolving it at due date (another on-chain transaction). By putting them inside Lightning channels, one can create and settle HTLCs off-chain, and even renew contracts without closing them (very useful for applications such as {{<newtabref href="https://comit.network/blog/2022/01/11/cfd-protocol-explained/#perpetual-cfds" title="perpetual CFDs">}}).

Of course, doing so requires some decent engineering, to properly split the funds inside the channel between those involved in the DLC and those that remain available for routing[^1], ensure contracts can be safely and trustlessly renewed, and everything can be brought back on-chain if needed.

With this building block, the possibilities offered by channels on top of Bitcoin start to become quite mesmerizing. Remember the {{<newtabref href="../latest-strikes-12/#synthetic-usd-in-ln-markets" title="Synthetic Dollar">}} in Bitcoin Beach, Kollider or LN Markets? You could very well set them up directy in your own Lightning channel by creating a DLC with your peer where you short Bitcoin's price, allowing your channel's balance to stay approximately the same in dollars term, in spite of Bitcoin's volatility, which could be quite useful for day-to-day spending.

However, as the Crypto Garage team emphasizes, it is not yet possible to route DLC's accross the Lightning Network, so it's too early to speak about Bitcoin-native "stablecoins". No big deal: stablechannels is cool too, isn't it?

## Closing Bit

Que de ténèbres alentours!\
L'hiver est venu dans un bruissement.

Il fait noir avant que n'entrent en gare\
Les trains partis tôt mais venant de loin\
Qui, de nuit en nuit,\
S'en vont toujours vers de nouveaux départs.

---

Want to receive Latest Strikes straight to your inbox every week? Couldn't be easier: subscribe to {{<newtabref href="https://blog.lnmarkets.com" title="LN Markets Ghost blog">}} and you're all set (remember to confirm your subscription by clicking the link sent via email).

---

If you enjoyed this recap, you can show your appreciation by throwing a few coins to *fanis @ lnmarkets.com*, by scanning or clicking the QR code.

Thank you!

{{<figure align=center src="../../images/lnm_lnurl.png" link="lightning:fanis@lnmarkets.com">}}

[^1]: Else, we would need to update the (potentially numerous) DLC's Contract Execution Transactions every time a Lightning transaction is routed in the node.
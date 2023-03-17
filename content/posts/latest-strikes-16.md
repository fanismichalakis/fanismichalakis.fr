---
title: "Latest Strikes 16"
date: 2022-12-27T12:00:00+01:00
block: "769099"
cover:
    image: "../images/ZeussHolidays.min.png"
    alt: "A cartoony illustration of the Greek God Zeus surfing."
    caption: "\"Zeus' Holidays\". Generated with DALL·E."
    relative: "false"
tags: ["bitcoin", "lightning"]
categories: ["strikes"]
draft: false
---

## Ecosystem

### Plug Any Vending Machine To Lightning

René Aaron {{<newtabref href="https://nitter.net/_reneaaron/status/1606026340523659264" title="shared">}} the impressive stuff he's been working on in the last months: connect any vending machine to the Lightning Network. To do so, he designed a small, easily plugable module that comes with its own screen and can be used by the vending machine to generate a Lightning invoice and display it as a QR code.

The product is currently being tested by a bunch of merchants in Europe, but given its plug-and-playiness and the benefits of using Lightning in this types of machines (you get the best money in the world sent directly to your remote BTCPay Server, no need to come around get the bills and coins or to pay payment processors their astounding fees), I'd say I'm quite bullish on this!

### Make Your Geyser Donations Flow To Your Own Wallet

A bit more than a week ago, Geyser rolled out a very neat {{<newtabref href="https://nitter.lacontrevoie.fr/geyserfund/status/1603783875125301249" title="feature">}} that I missed, so here it is: you can now as a project creator receive donations directly to your own wallet, through a Lightning Address. This allows you to receive the funds straight to the wallet of your choice (ideally non-custodial), without them ever sitting on Geyser's node.

So, how does it work? Much like {{<newtabref href="https://lnproxy.org/" title="lnproxy">}}, this new feature leverages "hodl invoices": when someone wants to send you money, the first thing Geyser does is requesting an invoice from the Lightning Address you provided. It then extracts the payment hash from this invoice and uses it to create a new invoice that it presents to the sender. When the sender pays this invoice, Geyser puts this first payment on hold while it pays your original invoice. Then, once this payment is settled and Geyser hence has the preimage, it can settle the invoice that was still on hold by providing the preimage to the sender.

This flow allows payees to receive money straight to their wallet in a privacy preserving manner (because the recipient's node is hidden from the sender), while Geyser remains a simple messenger and has no control over the funds at any moment.

### Mash Gets A Lifting

{{<newtabref href="https://www.getmash.com/" title="Mash">}} got a small {{<newtabref href="https://nitter.net/getmash/status/1606333823909646336" title="lifting">}} to better suit creators and what they want to do with their content.

Mash is a service that allows content creators to monetize what they create in a user friendly way. It just got easier to use, with more customization available (themes, Mash button placement, Boost button placement, etc.). Cherry on top: what previously required copy-pasting multiple snippets to make the Mash magic work on a custom website now requires only one code snippet. Cool!

Please keep in mind that the funds you receive originally end up in a custodial Mash account, from which they can be withdrawn at any time through Lightning.

### Alby Extension For Developers

Remember last week's Alby {{<newtabref href="../latest-strikes-15/#alby" title="sneak peek">}} from Bumi? Alby officially {{<newtabref href="https://nitter.lacontrevoie.fr/getAlby/status/1606554703172608000" title="launched">}} support for the webln {{<newtabref href="https://www.webln.guide/building-lightning-apps/webln-reference/webln.request" title="request">}} method, allowing users and developers to do more things through Alby, such as opening channels, getting statistics, and so on.

Basically, the `webln.request()` method allows websites you connect to through Alby to use your node's underlaying API (different depending on whether you use LND, Core Lightning or Eclair for example) to perform anything you'd do with said API, from listing channels to opening new ones to extracting useful data from past forwards -- you name it!

If you combine this with some universal API wrapper on the node's side (such as the still in progress {{<newtabref href="https://github.com/blc-org/una/tree/master" title="UNA">}}), you end up with some cool stuff where you don't even need to know the underlaying Lightning implementation of a node to interact with it in a meaningful way from a web browser.

### Sats Streaming in Podverse (cont'd)

In last week's {{<newtabref href="../latest-strikes-15/#sats-streaming-now-avaible-in-podverse-beta" title="Latest Strikes">}}, I covered the new Value For Value feature in the Podverse podcast streaming app. Doing so, I incorrectly stated that it was currently only possible to do one-time donations, and not directly stream sats per minute of listening as we can do in other podcasting apps such as {{<newtabref href="https://breez.technology/mobile/" title="Breez">}} or {{<newtabref href="https://fountain.fm/" title="Fountain">}}. It was indeed already possible to also stream sats by the minute in Podverse last week, only not in the F-Droid version which I use.

However, the sats streaming feature is now available in all versions, including the F-Droid one. If, like me, you like your podcast player Google/Apple-free, but still want to be able to support podcasters with Value For Value, this new feature in Podverse is a very nice addition to the current landscape[^1]!

### Lightning Auditability Or Lightning Surveillance?

Layers (formerly Exponential Layers) {{<newtabref href="https://nitter.net/Exp_Layers/status/1605638406821842967" title="announced">}} their new audit platform, meant to help assess whether claims by some entity (for example, an exchange or a LSP) hold up when confronted to publicly accessible data. To do so, Layers continuously listens to the gossip on the network and monitors the Bitcoin chain to detect channels open and close. This provides some upper and lower bound, and allows the public to verify that the data provided by the audited entity checks out.

The announcement {{<newtabref href="https://stacker.news/items/109300/r/FanisMichalakis" title="sparked">}} some interesting discussions on the frontier between audit and surveillance. What is certain is that this kind of tool highlights how much data Lightning's gossip protocol lets through. We're definetely on a slippery slope here, and if we don't mind how much soap we use to remove friction and enhance reliability, we might end up far lower than expected.

{{<figure align=center src="../../images/monkey-fight-ln-reliability-vs-privacy.jpg" caption="The perfect meme to sum up the situation, by the great <a href=\"https://stacker.news/DarthCoin\">Darthcoin</a>." alt="The monkey fight meme depicting how hard it can be to balance between privacy and reliability when building or using Lightning.">}}

## Wallets & Tools

### Zeus Release

Zeus v0.7.0 is {{<newtabref href="https://github.com/ZeusLN/zeus/releases/tag/v0.7.0" title="here">}} for real (not a {{<newtabref href="../latest-strikes-13/#zeus-prerelease" title="prerelease">}}, this is not a drill). The good stuff includes:
- connect to your LND node through {{<newtabref href="https://docs.lightning.engineering/lightning-network-tools/lightning-terminal/lightning-node-connect" title="Lightning Node Connect">}}, very handy if you're currently connecting to your node through Tor (it's way faster),
- a new default home screen, ready for you to input the amount you want to request or send (instead of the wallet displaying your whole balance (or weird characters if you have Lurker mode set up) from the get go),
- new themes (if you love red as much as I do, be sure to check the new {{<newtabref href="https://github.com/ZeusLN/zeus/pull/1183" title="Dealpool">}} theme out),
- support for BTCPay's {{<newtabref href="https://docs.btcpayserver.org/LNbank/" title="LNbank accounts">}}, a bit like LndHub accounts but without on-chain receiving support,
- {{<newtabref href="https://bitcoinqr.dev" title="BIP21 Unified QRs">}} by default (but you can still switch to Lightning-only or on-chain-only for each payment you want to receive),
- and much more!

Feel free to check out the {{<newtabref href="https://nitter.net/ZeusLN/status/1605566054130147328" title="Twitter announcement thread">}} or the {{<newtabref href="https://github.com/ZeusLN/zeus/releases/tag/v0.7.0" title="release notes">}} to see what more there is!

### RaspiBlitz v1.9.0 Around The Corner

Testers needed! The first release candidate for RaspiBlitz v1.9.0 is {{<newtabref href="https://nitter.lacontrevoie.fr/rootzoll/status/1606316410371710977" title="available">}} for testing. This new {{<newtabref href="https://github.com/rootzoll/raspiblitz/blob/8d5f42ff2e3681f7f92a67684513f246bfdb3cb1/CHANGES.md#whats-new-in-version-190-of-raspiblitz" title="version">}} brings new apps (notably The Eye of Satoshi watchtower Core Lightning plugin) and updates.

Remember this version of RaspiBlitz is still at the release candidate stage, and should not be considered production ready.

### Advanced Settings UI In Umbrel

In its latest release, Umbrel {{<newtabref href="https://nitter.lacontrevoie.fr/umbrel/status/1605906942555148288" title="added">}} a nice UI for users willing to change the Bitcoin Core configuration of their node without having to manually edit the configuration file. Available settings include control over Tor and I2P connections, toggling the "listening node" mode on and off, pruning and Full-RBF. The nice addition here on top of ease of use is the small text accompaniying each settings, so that users can grasp what each parameter does before changing it.

### Other Releases: LndHub Go, BTCPay Server & Ride The Lightning

Last week was also the week for a bunch of smaller releases that I found worth mentionning:
- LndHub.Go (LndHub compatible wrapper written in Go) got some nice {{<newtabref href="https://github.com/getAlby/lndhub.go/releases/tag/0.12.0" title="enhancements">}}, including an API endpoint to send a keysend payment to multiple nodes in only one API call (useful for things such as payment splitting in Podcasting 2.0 apps, for example),
- the version {{<newtabref href="https://github.com/btcpayserver/btcpayserver/releases/tag/v1.7.3" title="1.7.3">}} of BTCPay Server brings some bug fixes and enhancements to the table,
- and the version {{<newtabref href="https://github.com/Ride-The-Lightning/RTL/releases/tag/v0.13.3" title="0.13.3-beta">}} of Ride The Lightning fixes some bugs with Eclair (notably some breaking changes to adapt to the updates in Eclair's API introduced in {{<newtabref href="https://github.com/ACINQ/eclair/blob/master/docs/release-notes/eclair-v0.8.0.md#api-changes" title="v0.8.0">}}).

## Specs & Implems

### Lightning Channels On Top Of Statechains

Last week {{<newtabref href="https://nitter.net/brian_trollz" title="Shinobi">}} published an {{<newtabref href="https://bitcoinmagazine.com/technical/statechain-lightning-combined-in-bitcoin" title="article">}} in Bitcoin Magazine detailing how Lightning channels could be built out of statechain coins.

A statechain is a server-based construct allowing users to exchange UTXOs without moving them on-chain. A user (Alice) can deposit a UTXO to a statechain by sending it to a Bitcoin address for which she only knows part of the private key, and the statechain entity (eg. the central server) knows the other part. Before doing this deposit, Alice and the statechain entity signed a backup transaction spending the funds from the statechain address to Alice with a locktime, so that Alice can still recover her funds should the statechain entity disappear (she just needs to wait for the locktime to expire). At any time, if Alice wants to exit the statechain, she can request the statechain entity to sign with her a peg-out transaction that sends the UTXO on-chain to her address.

When Alice wants to send the statechain to another user (Bob), she collaborates with the statechain entity to sign a new backup transaction spending from the statechain address to Bob's address, with a timelock that expires earlier that Alice's, so that Bob can claim the coin (that now belongs to him) before Alice does. The statechain entity then deletes its half of the key it shared with Alice and creates a new pair of "half keys" with Bob in the same way it did with Alice in the beginning, thus rendering Alice's half useless and effectively transferring the "ownership" of the coin to Bob, without the coin actually moving on-chain.[^2]

While statechains are useful for scalability and privacy, they also have some drawbacks. Not only do you need to trust the statechain entity not to collude with the person who sends you money, but it is also only possible to send the exact amount of a given UTXO, as creating change would require another on-chain transaction. To circumvent that, the sender (Alice), the statechain entity and the recipient (Bob) can collaborate to turn the statechain into a Lightning channel: instead of the new peg-out transaction sending all the funds to Bob, it opens a channel by sending the funds to a 2-of-2 multisig between Alice and Bob. This creates a new "virtual" Lightning channel, in the sense that it is not (yet) backed by a real on-chain funding transaction. Provided that other Lightning nodes accept it, this channel could even be announced and used in the Lightning Network, as it only requires Alice and Bob update their respective balance in the channel each time a transaction occurs, in the exact same way as in a regular Lightning channel[^3].

This allows Alice and Bob to perform any split of funds they wish through the classic Lightning mechanism with commitment transactions, and they can even subsequently use the Lightning channel, thus rendering the statechain far more convenient to use while Alice and Bob are interacting together. Once they're done and all the funds are on one side of the channel, they can even close it without going on-chain by signing a new peg-out transaction with the statechain entity and sending the statechain to a new recipient.

The only thing that remains a bit unclear to me right now is whether the statechain entity needs to take part in the signing of commitment transactions once the channel is open, or if Alice and Bob can live their life on their own. If you know, feel free to add a comment or reach out!

## Closing Bit

Un seul phare brille dans la tempête, arqué,\
Il irradie, révèle, éclate de lumière\
Il brille si fort, et sur un ton si fier\
Que bien des capitaines s'en détournent, amers\
Et vont se fracasser sur les dents des rochers.

---

Want to receive Latest Strikes straight to your inbox every week? Couldn't be easier: subscribe to {{<newtabref href="https://blog.lnmarkets.com" title="LN Markets Ghost blog">}} and you're all set (remember to confirm your subscription by clicking the link sent via email).

---

If you enjoyed this recap, you can show your appreciation by throwing a few coins to *fanis @ lnmarkets.com*, by scanning or clicking the QR code.

Thank you!

{{<figure align=center src="../../images/lnm_lnurl.png" link="lightning:fanis@lnmarkets.com">}}

[^1]: As far as I know, there are now only two FOSS podcasting apps available in F-Droid or through APK that support Value For Value and don't require Google Services to work: Breez and Podverse. Please hit me up if you're aware of any other!

[^2]: This is a crucial aspect of the way Mercury statechains work: the key generation is so that for the same private key (corresponding to the actual on-chain UTXO), there are different pairs of "half keys" (called keyshares) that produce the same private key when combined. This is what allows transfer of ownership: the statechain entity has a different keyshare with each new owner and immediately deletes the keyshare corresponding to the previous owner when a transfer occurs. For a more detailed explanation of statechains, how they work and how Mercury statechains differ from the statechains envisioned by Ruben Somsen (which require eltoo and are hence impossible to do as of now), see the first half of this {{<newtabref href="https://bitcoinmagazine.com/technical/a-new-privacy-tool-for-bitcoin" title="article">}} by Shinobi.

[^3]: In other words, there is no question that this channel would work. The only remaning question, which is one of the reason why the team behind Mercury is writing a {{<newtabref href="https://github.com/commerceblock/blip-XXXX/blob/main/blip-XXXX.md" title="bLIP">}} (Bitcoin and Lightning Improvement Proposal), is whether other nodes will consider the channel announcement as valid in spite of there not being an on-chain funding transaction. This is of importance only if Alice and Bob wish to announce this channel.
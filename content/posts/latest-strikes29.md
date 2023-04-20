---
title: "Latest Strikes 29"
date: 2023-03-30T12:30:00+02:00
block: "783163"
cover:
    image: "../images/LightningNetworkAccountant.min.jpeg"
    alt: "A man wearing a suit, doing some accounting with an abstract holographic abacus "
    caption: "\"The Lightning Network Accountant\". Generated with Stable Diffusion."
    relative: "false"
tags: ["bitcoin", "lightning"]
categories: ["strikes"]
draft: false
---

Buongiorno! Welcome to the 29th issue of Latest Strikes, published from Tuscany, Italy, where we're attending the Tuscany Lightning Summit. But more on that next week. For now, let's wrap up last week together, from lightning accounting to privacy-preserving LNURL servers!

## Ecosystem

### Lightning Accounting

BoltObserver published a blog {{<newtabref href="https://boltobserver.substack.com/p/lightning-network-financial-statements" title="post">}} on Lightning Accounting, more precisely dealing with what a Lightning node's balance sheet might look like. I think it's a really interesting exercise, as proper accounting seems to be kind of a blind spot for node operators, both professional and *amateurs*. Or, to put it differently, while I'm sure many companies running nodes perform some kind of accounting (if only to be sure that they actually win money), to my knowledge we still lack accounting software able to produce financial statements (or assist accountants in doing so), and not just a glimpse of the node's financial situation. So I'd say it's definitely a space to watch, especially for companies and professionally-run nodes. In a not so distant future, liquidity marketplaces might allow nodes to publish such statements to display their financial and operational health, since so much is kept private by design in the Lightning Network.

Speaking of accounting, I also {{<newtabref href="https://stacker.news/items/155532/r/FanisMichalakis" title="stumbled upon">}} a tutorial showing how to connect your Lightning node to {{<newtabref href="https://www.gnucash.org/" title="GnuCash">}}, a free and open accounting software. The idea here is not to generate financial statements, but rather track income and expenses, for your personal use or for a small business (for example a merchant accepting Lightning payments). It relies on a tool called {{<newtabref href="https://github.com/drmartinberger/FueliFinTS/" title="LN-FinTS">}}, which basically creates an open banking interface on top of LNBits. GnuCash can then be connected to this interface to fetch and display data in the accounting software.

### 10101 Launches Beta

{{<newtabref href="https://fanismichalakis.fr/posts/latest-strikes-22/#10101s-roodmap" title="10101">}} are making some progress and {{<newtabref href="https://nitter.lacontrevoie.fr/get10101/status/1639160117470851077" title="announced">}} that they will be launching their closed beta soon, right on track with their projected {{<newtabref href="https://10101.substack.com/p/10101-roadmap" title="roadmap">}}, although it depends on whether it's a small "soon" or a big one.

According to their latest blog {{<newtabref href="https://10101.substack.com/p/10101-coming-soon" title="post">}}, the closed beta will be a MVP of the core feature of the app: a non-custodial Lightning wallet where user can also place a non-custodial Futures market order (thanks to {{<newtabref href="https://fanismichalakis.fr/posts/latest-strikes-13/#dlcs-on-lightning-on-mainnet" title="Lightning DLCs">}}).

### Efficient Self-custodial Asset Exchanges On Lightning

Lukas Bahrenberg published a Medium {{<newtabref href="https://medium.com/@lukasbahrenberg/efficient-self-custodial-asset-exchanges-on-lightning-off-chain-swaps-and-a-central-order-book-f3ea6f9fd40b" title="post">}} on an efficient, self-custodial way to exchange Taproot-based assets (for example, RGB or Taro assets) off-chain using atomic swaps. The idea is to mix the swapability of Taproot-based assets with Bitcoin and between themselves with a centralized order book to enable trading of assets in a self-custodial, yet efficient manner.

Parties willing to trade interact only with the centralized exchange, which is in charge of matching orders it receives by being the counterparty of both sides. For example, if Alice wants to sell 10 LNM tokens for 0.1 BTC, and Bob wants to buy 10 LNM tokens for 0.1 BTC, the exchange will perform 2 swaps, one with Alice and one with Bob, thus allowing each of them to perform the trade they wished to do while staying in a neutral position.

1. Alice connects to exchange and states her intention to sell 10 LNM tokens for 0.1 BTC.
2. The exchange creates a preimage, hashes it, and sends the hash to Alice.
3. Alice creates an invoice for 0.1 BTC with the hash and sends it to the exchange.
4. The exchange pays the invoice, but Alice can't claim the HTLC yet, as she doesn't know the preimage.
5. The exchange creates and invoice for 10 LNM tokens with the hash and sends it to Alice.
6. Alice pays the invoice. The exchange can claim the corresponding HTLC at any time by revealing the preimage. When it does, Alice learns the preimage and can in turn claim her HTLC. But the exchange doesn't claim the HTLC just yet, and holds on the invoice ...
7. Bob connects to the exchange and states his intention to buy 10 LNM tokens for 0.1 BTC.
8. The exchange creates another preimage, hashes it, and sends the hash to Bob.
9. Bob creates an invoice for 10 LNM tokens with the hash and sends it to the exchange.
10. The exchange pays the invoice, but Bob can't claim the HTLC yet, as he doesn't know the preimage.
11. The exchange creates an invoice for 0.1 BTC and sends it to Bob.
12. Bob pays the invoice. The invoice, which sees the match with Alice's ongoing swap, claims the invoice right away with the preimage. At the same time, it claims Alice's HTLC, revealing her the second preimage. Alice and Bob now know the preimage of their respective swaps, and can in turn claim their HTLC.
13. The swap is complete!

What we've just described could very well happen with two on-chain transactions, but where it really shines is with the ability to do it off-chain, directly inside Lightning payment channels. The required tech isn't completely here yet - notably we still need Taproot channels - but it's coming very soon™ (2 weeks?).

Of course, the above design is only one possibility among others. What is interesting is that users benefit from the capital efficiency of a centralized exchange while retaining full-custody of their funds at any time. We could even automate the matching part with nostr and a specifically designed client: limit orders would be published publicly, along with a hash. When creating a new order, the client would check if it matches an already existing order. If so, it would directly initiate a swap by sending an invoice to the nostr pubkey of the counterparty via an encrypted message. The counterparty, if it's still willing to partake in the trade, would pay the invoice and send another invoice, still with an encrypted message. Once the counterparty reveals the preimage, both HTLCs can be claimed and the swap is complete. The counterparty can then submit a deletion event to remove the limit order from the public order book, since it has been paid. And to mitigate DoS issues, users could decide to interact only with orders published to paid relays.

Lukas is currently working on a {{<newtabref href="https://l2.auction/" title="prototype">}} for such a centralized, yet non-custodial exchange. Definitely an interesting topic, maybe not completely new, but worth revisiting now that nostr is proving to be a more and more robust communication medium. Also, kudos to Rsync for spotting this and {{<newtabref href="https://stacker.news/items/155531/r/FanisMichalakis" title="posting">}} the link to StackerNews!

## Wallets & Tools

### Lightning Addresses Without A Server

One of the biggest concerns around Zaps (and Lightning Addresses in general) in the community and outside is that it can favor custodial solutions. Of course, in theory, anyone can run the whole stack to be able to use a Lightning Address in a sovereign way, but it might be a bit more challenging in practice. This shows in the statistics of Zaps, which are by definition publicly available accross nostr relays. Ben Carman collected and arranged them in nice {{<newtabref href="https://nitter.lacontrevoie.fr/benthecarman/status/1638006709741289474" title="graphs">}}, and the results are stunning: 90% of Zaps are received on custodial wallets, with Wallet of Sathoshi grabing the lion's share with two-third of the volume received!

To address this issue, Ben Carman developed a tool called {{<newtabref href="https://github.com/benthecarman/zap-tunnel" title="zap-tunnel">}}. It essentially borrows from the same idea behind {{<newtabref href="https://lnproxy.org/about.html" title="lnproxy">}}, but with different trust assumptions. In lnproxy, you never need to trust the proxy because you're the one passing around invoices and wrapped invoices[^1]. In Zap-Tunnel, it must work without any intervention from the receiver. To address this, Zap-Tunnel stores some pre-generated, amountless invoices from your node, and uses them when someone tries to pay your Lightning Address. You don't have to run your own web server, and all you need is an online Lightning node (since the tunnel needs to pay your initial invoice). However, this comes at a hefty price: you need to trust the tunnel not to give its own invoices instead of yours. If it did, it would be able to siphon payments that were meant to reach you. If done at a reasonable scale, it could easily go unnoticed.

This tradeoff is not new. Indeed, similar solutions where you only need an always-on Lightning node have been around since the middle of 2021. For example, you can connect your node to a {{<newtabref href="https://github.com/nbd-wtf/satdress" title="Satdress">}} server in order to get a Lightning Address that pays directly to your node (try it out {{<newtabref href="https://lnsat.me" title="here">}}). If you already have a domain name but don't want or can't run a server, you can rely on a {{<newtabref href="https://bridgeaddr.fiatjaf.com" title="bridgeaddr">}} server. In both cases, you still need to trust the server not to give its own invoices instead of yours.

If you have a domain name and are feeling like running your own LNURL server, there is {{<newtabref href="https://github.com/dolu89/ligess" title="Ligess">}}, which supports Zaps since a few weeks. Running your own LNURL server is currently the only way to ensure payments sent to you aren't being hijacked. We briefly {{<newtabref href="https://fanismichalakis.fr/posts/latest-strikes26/#the-lnurl-vs-bolt12-debate-rages-again" title="mentioned">}} a proposal made by Evan Kaloudis to mitigate this by commiting to the receiving node's public key in the Lightning Address itself, but it comes at a privacy cost, and I'm not sure it is an arbitrage I am willing to make.

Speaking of privacy, one of the interesing things with Ben Carman's zap-tunnel is that the receiver's node is hidden from the sender, since the server also wraps the invoices *à la* lnproxy. While it currently relies on storing invoices, it could also connect directly to your node and fetch a new invoice every time it needs one, wrap it, present the wrapped invoice to the sender and pay your original invoice once the sender makes the payment. If so, I'd say it has the same tradeoffs as Satdress and Bridgeadd but with the additionnal privacy benefits.

Finally, all this solutions still require you to have an online Lighting node. Hampus from Blixt Wallet {{<newtabref href="https://fanismichalakis.fr/posts/latest-strikes26/#lightning-addresses-coming-soon-to-blixt" title="proposed">}} a way to also serve offline wallets, but it requires the service taking custody of the funds while the wallet is offline.

### BoltCard Wallet

We've got a {{<newtabref href="https://stacker.news/items/154795/r/FanisMichalakis" title="new">}} wallet in town! The {{<newtabref href="https://boltcardwallet.com/" title="Bolt Card Wallet">}} is a fork of BlueWallet, without the on-chain part, and where the custodial Lightning wallet has been modified to accomodate NFC cards *à la* {{<newtabref href="https://www.boltcard.org/" title="BoltCard">}}. On the backend, the wallet connects to a fork of LndHub called {{<newtabref href="https://github.com/boltcard/boltcard-lndhub" title="Boltcard-LndHub">}}, which has all the stuff needed to support NFC cards connections.

The app makes it easy to link a NFC card to a wallet, and you can have many wallets as you wish inside the app. As a user, you can either rely on someone else's Boltcard-LndHub instance, or run your own (and maybe let your friends and family use it as their backend).

Speaking of BoltCards, those {{<newtabref href="https://stacker.news/items/154665/r/FanisMichalakis" title="ones">}} lit up when you tap them!

### RGB Coming To Lightning?

The Bitfinex team working on RGB {{<newtabref href="https://nitter.lacontrevoie.fr/iris_wallet/status/1639189676845047808" title="released">}} a RGB-enabled Lightning {{<newtabref href="https://github.com/RGB-Tools/rgb-lightning-sample" title="node">}} based on the LDK (Lightning Dev Kit) sample node implementation and a fork of rust-lightning (a Rust library maintained by the LDK team). This node implementation is still at the prototype stage, but it allows to issue RGB assets, deploy them into Lightning channels and send them offchain. Assets can even be routed along channels, provided they have sufficient liquidity in the requested asset.

I've seen it in action yesterday during the Tuscany Lightning Summit, and the least I can say is I'm quite bullish on RGB.

### And Lightning Coming To Blockstream Green

Seems like Lightning is {{<newtabref href="https://nitter.lacontrevoie.fr/Blockstream/status/1638671142570594305" title="coming">}} to the Blockstream Green Wallet. There isn't much details as to when this new feature will drop, or how it works, but I'd guess it uses {{<newtabref href="https://blockstream.com/lightning/greenlight/" title="Greenlight">}} under the hood. Cool!

### Automation In Torq

{{<newtabref href="https://ln.capital/" title="LN Capital">}} dropped a banger for their liquidity management tool {{<newtabref href="https://github.com/lncapital/torq" title="Torq">}}: automation. As shown in this {{<newtabref href="https://nitter.net/LN_Capital/status/1639671343116599297#m" title="demo">}}, this tool allows you to create automated workflows using a drag-and-drop interface (think {{<newtabref href="https://en.wikipedia.org/wiki/Scratch_(programming_language" title="Scratch">}}), but for Lightning). For example, you can ask Torq to automatically rebalance a channel everytime its balance drops below a certain level, or rebalance all channels in need of rebalancing every hour. You can automatically tag channels based on many conditions, and so on. A very powerful tool, made even more powerful by its accessibility for all kinds of public, even non-developers. There will probably be a bit of a learning curve to fully understand the grammar of this automation tool and be able to use at its full extent, but I really believe this is a huge step forward better node and liquidity management accessible to all Lightning node operators.

### Split Extension In LNBits

Remember the {{<newtabref href="https://fanismichalakis.fr/posts/latest-strikes27/#lightning-prisms" title="Lightning Prisms">}} we spoke about a few weeks ago? There is now a detailed {{<newtabref href="https://bitkarrot.substack.com/p/lightning-prisms-with-lnbits" title="guide">}} on how to setup this kind of payment-splitting mechanism, and all you need is LNBits with the {{<newtabref href="https://github.com/lnbits/lnurlp" title="LNURLp">}} and {{<newtabref href="https://github.com/lnbits/splitpayments" title="SplitPayments">}} extensions!

## Closing Bit

L'heure fut soudain là\
Un claquement, l'aiguille se fige\
Bondit soudain, enjambe le corps\
De ce temps déjà tué.

Ce temps ne nous appartient pas\
Qu'importe ? Tic, toc\
Voici déjà venu le prochain bloc.

---

Want to receive Latest Strikes straight to your inbox every week? Couldn't be easier: subscribe to {{<newtabref href="https://blog.lnmarkets.com" title="LN Markets Ghost blog">}} and you're all set (remember to confirm your subscription by clicking the link sent via email).

---

If you enjoyed this recap, you can show your appreciation by throwing a few coins to *fanis @ lnmarkets.com*, by scanning or clicking the QR code.

Thank you!

{{<figure align=center src="../../images/lnm_lnurl.png" link="lightning:fanis@lnmarkets.com">}}

[^1]: The idea behind lnproxy is the following: first, you send the proxy an invoice. Then, the proxy creates an invoice for themselves, for the same amount and using the same payment hash. It presents this invoice to the sender. When the sender pays, the proxy can't claim the payment because they don't know the preimage behind the payment hash. The only way for them to learn this preimage is by paying your initial invoice. This way the proxy can never get hold of your funds, since it needs to first pay you before it can receive the payment from the original sender.

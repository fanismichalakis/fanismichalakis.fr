---
title: "Latest Strikes 32"
date: 2023-04-19T19:00:00+02:00
block: "786134"
cover:
    image: "../images/FreeMerchantRidingMetaOstrich.jpg"
    alt: "An orientalist science-fiction painting of a merchant riding a cyborg ostrich."
    caption: "\"A Free Merchant Goes Nowhere Without Their Meta-Ostrich\". Generated with Stable Diffusion."
    relative: "false"
tags: ["bitcoin", "lightning"]
categories: ["strikes"]
draft: false
---

Last week was quite THE week for decentralized trading over Lightning and Nostr. Between Civ Kit, n3xb, Mostro and the Nostr Marketplace specification being merged, it seems like there is a big arc developing and further fueling the synergies between Nostr and Lightning. Let's get into this, and see what other amazing events last week had for us.

## Ecosystem

### Awesome LDK

Peak Shift published an extensive {{<newtabref href="https://github.com/peakshift/awesome-ldk/" title="list">}} of projects using the {{<newtabref href="https://lightningdevkit.org/introduction/" title="Lightning Dev Kit">}} (LDK) under the hood. Mobile wallets, nodes, watchtowers, smart contracts platforms, analysis tools, and the list goes on, and the variety of use cases the LDK allows to fulfill is impressive. This versatility comes from the high flexibility and modularity of the LDK, and seeing it in action in so many different projects is quite dizzying!

### Lightspark

Lightspark ignited last week! The platform, launched by David Marcus (former Head of now discontinued Facebook's Crypto Wallet project Novi, former President of PayPal, etc.), had already made the news through its {{<newtabref href="https://fanismichalakis.fr/posts/latest-strikes26/#first-bank-to-join-the-lightning-network" title="partnership">}} with Xapo Bank, where Lightspark provided the Lightning infrastructure for the bank to join the network.

This partnership was part of Lightspark's closed beta program, but the company has now officially launched its offering. It is comprised of three interconnected products:

- Lightspark Connect which, as the name suggests, connects you to the Lightning Network through Lightspark's infrastructure,
- Lightspark Predict, which supposedly uses Artificial Intelligence to optimize the routing nodes Lightspark connects its clients too, as well as the flow of payments going through those connections,
- Lightspark SDK for easy integration of Lightspark's services in an existing system.

To use Lightspark, one has to be a company, and the pricing seems to target companies that already expect a decent volume of transactions. For example, the first plan starts at $1,500 a month, and covers up to $300,000 of monthly Lightning transactions. That's a pretty low 0.5% fee in comparison to legacy payment rails, and higher plans are even lower, but that's supposing the business reaches the aforementioned volume. In other words, Lightspark seems to be built for businesses of a quite decent size already, given that Lightning's adoption is still small. My intuition is the market isn't there yet, and Lightspark positioned itself at this end of the scale out of expectation that Lightning usage and adoption will grow substantially, and especially that established businesses will need to get on the Lightning rails quickly to process millions of dollars of Lightning payments monthly. Only time will tell if that was a crazy bet or a decisive move.

Regarding Predict, which is the most exotic part of the offering, it's difficult to assess exactly how it works. Lightspark co-founder Christian Catalini {{<newtabref href="https://nitter.lacontrevoie.fr/ccatalini/status/1645850361046114304" title="shared">}} some insights on Twitter and in this {{<newtabref href="https://www.lightspark.com/learn/lightspark-insights/harnessing-the-power-of-prediction-to-scale-lightning" title="blog post">}}, mostly indicating that Lightspark developed its own metric called *conductivity* which measures the ability of a Lightning node to "effectively transfer value across the network". This definition, of course, is a bit vague, and so is the actual role of an AI model in the equation. But still, that's an interesting direction, since capital management is paramount in Lightning, and efficiently deploying liquidity where it's needed is a decisive advantage.

Regarding custody of the funds, Lightspark seems to work quite like {{<newtabref href="https://voltage.cloud/" title="Voltage">}}. Indeed, custody is a more sophisticated question on Lightning than it is on-chain, because on Lightning even receiving funds requires the node to access the private key in order to sign the new state of the channel. That's why when relying on a hosting provider for your Lightning node, you have to accept that the private key of your node will be on the machine's memory[^1]. When they store sensible things (such as macaroons or keys) for backup, they always store encrypted versions of them, with the encryption happening on the client side. Lightspark also has a {{<newtabref href="https://www.lightspark.com/recovery-kit#important-notes" title="recovery kit">}}, updated after every Lightning payment, and which contains presigned Bitcoin transactions closing all channels and sending the funds to an address the user specified during the setup process ; while Voltage lets users export their node's data and backups at will.

The big difference between Lightspark and Voltage seems to lie in the privacy of the transactions happening on the node. While Voltage clearly details in this {{<newtabref href="https://voltage.cloud/blog/lightning-infrastructure-providers/how-voltage-works/" title="article">}} what data they can and can't see, I could not find such information for Lightspark. On the contrary, Lightspark's pricing itself suggests that they can see everything going on, since they charge customers depending on their transactions volume. So does their {{<newtabref href="https://www.lightspark.com/privacy-policy" title="privacy policy">}}. Voltage, on the other hand, sees none of that:

> We can’t see your node’s public key, peers, channels, balance, or transactions. We don’t have the credentials to your node, so there’s no way for us to get this information. All peer-to-peer traffic is routed through Tor. This means we can only see your node connecting to Tor entry nodes, not your actual peers. (...) Since your Lightning nodes are hooked up to our Bitcoin full nodes, it’s possible we could see some of your on-chain activity. To be very clear, we do not track this information and never will.[^2]

Overall, I think it's a great signal for Lightning adoption to see such an offering. Of course, we'd have preferred something more privacy-oriented, more open (I'd love to know how conductivity is computed), but I guess that doesn't necessarily fit to the market that Lightspark is aiming for. Let's see where this goes 👀

### Olympus

A new LSP is about to enter the game. Zeus just {{<newtabref href="https://nitter.lacontrevoie.fr/ZeusLN/status/1645385547827802114" title="announced">}} {{<newtabref href="https://olympusln.com/" title="Olympus">}}, its very own LSP which will probably be available in the Zeus {{<newtabref href="https://zeusln.app/" title="wallet">}}. You can already join the waitlist (either by email or nostr identifier), and fill a short survey to help the Zeus team better identify users expectations.

Having an LSP in the Zeus app is a natural step toward more Lightning adoption. I also think it's the perfect opportunity to finally have many LSPs available in a single wallet, with a nice interface displaying the features and cost of each. But it of course requires some {{<newtabref href="https://github.com/BitcoinAndLightningLayerSpecs/lsp" title="standardization">}} across LSPs to spare the Zeus team from writing a new interface for each. So we'll probably see an Olympus-only Zeus app first, and a multiple-LSPs version later. In any case, looking forward to this!

### Censorship-Resistant Permissionless Lightning Exchanges On Nostr

A very interesting {{<newtabref href="https://github.com/civkit/paper/blob/main/civ_kit_paper.pdf" title="whitepaper">}} {{<newtabref href="https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2023-April/021556.html" title="dropped">}} into the Bitcoin-Dev mailing list last week. The idea behind Civ Kit is to use Nostr and Bitcoin/Lightning together to create a "censorship-resistant and permissionless global trading" system that everyone can access. The whitepaper is very well written, with clear yet concise explanations of the various technological pieces involved, as well as the potential pitfalls of such a system and how they can be mitigated. Well worth a read, but here's a quick summary anyway.

A maker who wishes to partake in a certain trade (for example, exchange 0.1 BTC against 10,000 {{<newtabref href="https://en.wikipedia.org/wiki/Dofus" title="Kamas">}}) creates a Lightning {{<newtabref href="https://thebitcoinmanual.com/articles/lightning-offers-bolt12/" title="Offer">}} containing all the details of the trade (amounts, expiry period, oracle, escrow, etc.) and sends it to one or many *bulletin board(s)* via Lightning Onion Messages. Bulletin boards are also Nostr relays and, when one receives a trade offer, it broadcasts it to all the subscribed clients. Among those clients, if one of them finds the offer interesting and wants to take it, they do so by sending a specifically-crafted HTLC to the maker's blinded endpoint, which they specified in their Offer. From then on, the taker is committed to the trade, and either the maker is still interested and the trade happens, or the maker just lets the HTLC expire and the taker gets their funds back.

Already sounds a bit too complicated? Here's an even simpler explanation. **Someone wants to trade, they send the details of the trade they're looking to make to a Nostr relay, which broadcasts the trade offer to everyone listening. Among the listeners, someone interested can then directly initiate the trade.** That's it. The rest of the explanation only describes which communication medium is used where and why, to ensure both privacy for the participants and resiliency for the bulletin boards.

For example, using Lightning Onion Messages to send the trade offer from the maker to the bulletin board in the form of an Offer helps protect bulletin boards from DoS attacks, as they can enable rate-limiting based on amounts deployed in direct channels, while protecting the maker's privacy at the same time. On the other hands, Nostr totally makes sense as a publication network. Finally, complex Bitcoin contracts (for example involving escrows using multisignature schemes) can be used to perform the trade itself, either on-chain or off-chain, where such contracts can even be routed across the Lightning Network.

Of course, we are at the very beginning of the specification process of this idea, but it feels really powerful. Part of this feeling I think comes from the apparent simplicity of the system, while it will require many more building blocks to make it actually resilient and censorship-resistant, such as privacy-preserving stake certificates (a bit like the ones {{<newtabref href="https://fanismichalakis.fr/posts/latest-strikes-12/#more-on-channel-jamming" title="proposed">}} by Riard to solve channel jamming) to enable participants to assess whether a trade counterparty is "trustworthy" or not.

At this point, I really hope you're as pumped as me. This is really an exciting subject, as the number of similar projects being built right now demonstrates.

For example Francisco Calderón {{<newtabref href="https://nitter.lacontrevoie.fr/negrunch/status/1646385935930490880" title="shared">}} their advancement on Mostro (which we briefly covered {{<newtabref href="https://fanismichalakis.fr/posts/latest-strikes-15/#mostro" title="here">}}) last week. The core functionality is operational, and the team is working on orders cancellation, dispute logic and a reputation system. Mostro works quite like Civ Kit in the sense that a maker sends a trade offer to a relay (a Mostro instance) which broadcasts it to listeners. Big differences are that all communications (order publishing, order taking, reputation scores) happen on Nostr, and that Mostro instances serve as escrows to settle trades between users (whereas on Civ Kit the bulletin board's role stops at broadcasting the offers it receives). The team is looking for contributors, so feel free to check out their {{<newtabref href="https://mostro.network/" title="website">}}.

Another alternative proposal is {{<newtabref href="https://github.com/nobu-maeda/n3xb" title="n3xb">}}, which stands for "Naive Nostr No-KYC Exchange". As the name suggests n3xb focuses on simplicity, in a stance not to dissimilar to the one that underpinned Nostr's design itself. All communication happens on Nostr, using a special kind even for trade offers and relays to broadcast them to the public. When a taker wants to partake in the trade, they send a Nostr DM to the maker to notify them and send the finalized details of the contract, which initiates the trade if the maker accepts.

All this various proposals are very cool. Some are more complex because they try to address complicated problems such as DoS mitigation from the get go, while others focus more on simplicity. Really looking forward what builders will come with in the coming months!

### Cool New Lightning Faucet

1of21mil {{<newtabref href="https://nitter.lacontrevoie.fr/1of21mil/status/1645556690547507200" title="made">}} a nice Lightning {{<newtabref href="https://lnscratch.com/" title="faucet/game">}} last week. It's a simple scratch game, where you login using LNURL and get 3 cards a day. If scratching your card reveals 4 check marks in a row, you win (usually 21 sats). Nicely done, and a great little demo of the power of Lightning!

### Zebedee & Strike Further Expand In Africa Thanks To Bitnob

After its {{<newtabref href="https://fanismichalakis.fr/posts/latest-strikes30/#zebedee" title="partnership">}} with Brazilian Bipa and Philipinno Pouch, Zebedee is coming to some African countries thanks to an {{<newtabref href="https://nitter.lacontrevoie.fr/zebedeeio/status/1645805787183484929" title="integration">}} with Bitnob. Bitnob already worked with Strike as part of its Send Globally program, and recently expanded the number of countries {{<newtabref href="https://nitter.lacontrevoie.fr/Strike/status/1645898120998404097" title="available">}}, which means people living in Nigeria, Kenya, Ghana, Rwanda, Benin, Senegal, Cote d'Ivoire and Togo can now receive money both from Strike and Zebedee, and have it credited directly in their local currency if they so wish. Open Banking on Lightning 🔥

## Wallets & Tools

### Lightning In Mercury

In the {{<newtabref href="https://fanismichalakis.fr/posts/latest-strikes-2/#lightning-support-in-mercury" title="second issue">}} of Latest Strikes, back in September 2022, we mentioned the upcoming support of Lightning into {{<newtabref href="https://mercurywallet.com/" title="Mercury Wallet">}}, a "Layer 2" Bitcoin wallet. Right now, Mercury only supports {{<newtabref href="https://fanismichalakis.fr/posts/latest-strikes-16/#lightning-channels-on-top-of-statechains" title="statechains">}}, a server-based construct where participants can send UTXOs without actually moving them on-chain. The wallet is now closer than ever to adding another string to its bow with Lightning support. Indeed, the team behind the project {{<newtabref href="https://nitter.lacontrevoie.fr/mercury_wallet/status/1646893804899692548" title="released">}} their lightweight Lightning node implementation called *mercury-node* and based off the LDK. The node implementation is currently behind polished, and will soon make it into the actual Mercury Wallet. Very cool!

### NIP5 & Lightning Addresses In Voltage

Voltage continues to pave the way with the {{<newtabref href="https://nitter.lacontrevoie.fr/voltage_cloud/status/1646545761461497861" title="release">}} of the {{<newtabref href="https://voltage.cloud/blog/news/non-custodial-nostr-zaps-nip05-ln-addresses/" title="Nostr Toolkit">}}. It allows Voltage users to get an `@vlt.ge` NIP5 identifier, as well as to receive Zaps directly to their Voltage node. Cherry on top: you can also connect the Lightning Address to your own node at home, if you'd rather not rely on Voltage's infrastructure.

### BTCPay Release

A new major BTCPay server release {{<newtabref href="https://nitter.lacontrevoie.fr/BtcpayServer/status/1646514087105560581" title="dropped">}}. In version {{<newtabref href="https://blog.btcpayserver.org/btcpay-server-1-9-0/" title="1.9.0">}}, you can start connecting your BTCPay server to exchanges (only Kraken is supported so far) through a dedicated plugin. For example, this allows BTCPay users to convert 20% of each payment to fiat to pay taxes. It's cool to see this land in BTCPay, as it is one of the main features that set custodial payment processing solutions apart. Many merchants still need to go back to fiat, at least partially.

The update also includes a number of new features and improvements, such as:

- further enhancements to the new checkout page they {{<newtabref href="https://fanismichalakis.fr/posts/latest-strikes-12/#new-btcpay-server-release" title="rolled out">}} a few months ago,
- stores preset (retail (e.g. physical store) and online mode), to get you started with your new store with a sensible default configuration,
- wallet labels export using {{<newtabref href="https://bips.xyz/329" title="BIP329">}}. When you move to another wallet, you can now take your labels with you automatically,
- and much more enhancements (NFC, receipts, labels management, invoices metadata, etc.).

The BTCPay Server team is also seeking to phase out support for MySQL and SQLite, as they announced in {{<newtabref href="https://fanismichalakis.fr/posts/latest-strikes-24/#btcpay-server-releases" title="February">}}. Trying to start a BTCPay server with MySQL or SQLite database outside of the migration context will hence fail, unless the user inputs the `--deprecated` flag. Time to migrate folks!

### BoltObserver Release

BoltObserver {{<newtabref href="https://nitter.lacontrevoie.fr/BoltObserver/status/1646523595005501444" title="added">}} three new alerts to their {{<newtabref href="https://fanismichalakis.fr/posts/latest-strikes-11/#liquidops" title="LiquidOps">}} product: on-chain funds level, sync to graph, and sync to chain.

You'll get a warning when:

- your available on-chain funds get depleted (which allows you to deploy new liquidity in time, to use for example to open new channels, perform swaps, or even bump channel closing using {{<newtabref href="https://fanismichalakis.fr/posts/anchor-outputs/" title="anchor outputs">}}) ;
- your node loses sync to the graph, which is the set of nodes and channels your node is aware of, and it uses to find the optimal route for payments. An out-of-sync node can mean costlier or less reliable payments (or even both!)[^3] ;
- your node loses sync to the chain, which means it can't see new channels opening or channels closing, and your funds could even be stolen by a malicious actor if you don't have a working watchtower.

### Zeus Release

Last week was the {{<newtabref href="https://nitter.lacontrevoie.fr/ZeusLN/status/1646577364543979520" title="release">}} of the alpha of {{<newtabref href="https://github.com/ZeusLN/zeus/releases/tag/v0.7.5-alpha1" title="version 0.7.5">}} of Zeus wallet. There's some really good stuff coming:

- payment path {{<newtabref href="https://github.com/ZeusLN/zeus/pull/1426" title="visualization">}}, where you can see a beautiful breakdown of the routing nodes your payment went through, with the fee perceived by each node in the route,
- better handling of in-flight payment, which are {{<newtabref href="https://github.com/ZeusLN/zeus/pull/1408" title="now">}} displayed as such,
- a fix to LNURL-Withdraw handling,
- various bug fixes, display enhancements and more.

Feel free try this alpha version out and send your feedback to the Zeus team!

### Nostr Marketplaces NIP Merged

Remember the Nostr Market plugin for LNBits we {{<newtabref href="https://fanismichalakis.fr/posts/latest-strikes28/#lnbits" title="covered">}} a few weeks ago? The corresponding {{<newtabref href="https://github.com/nostr-protocol/nips/blob/master/15.md" title="specification">}} has been {{<newtabref href="https://nitter.lacontrevoie.fr/arcbtc/status/1646463215503659011" title="merged">}}. This echoes with the permissionless, censorship-resistant P2P trading protocols we covered above, but with a focus on goods and services.

Now that the specification is ironed out, we can expect more and more clients to implement it, as there seems to be {{<newtabref href="https://i.imgur.com/cYnlr1C.png" title="demand">}} for it!

### Closing Bit

Les effluves iodées de la mer paresseuse
Montaient discrètement vers la ville assoupie
Croulant sous un soleil aux mutiques furies
Etrangère aux terreurs, fidèle et prometteuse.

Ainsi qu'un chat lové au creux d'un édredon
Elle ronronne entourée de pics et de vallons
Son sang ce sont les hommes et femmes qui l'arpentent
Et pulsent dans ses rues de leur cadence lente.

---

Want to receive Latest Strikes straight to your inbox every week? Couldn't be easier: subscribe to {{<newtabref href="https://blog.lnmarkets.com" title="LN Markets Ghost blog">}} and you're all set (remember to confirm your subscription by clicking the link sent via email).

---

If you enjoyed this recap, you can show your appreciation by throwing a few coins to *fanis @ lnmarkets.com*, by scanning or clicking the QR code.

Thank you!

{{<figure align=center src="../../images/lnm_lnurl.png" link="lightning:fanis@lnmarkets.com">}}

[^1]: An exception to this is Blockstream's {{<newtabref href="https://blog.blockstream.com/en-greenlight-by-blockstream-lightning-made-easy/" title="Greenlight">}}, where even if the node runs in the cloud, the private key never leaves the user's device. When the node needs to perform any kind of operation (either sending, receiving or routing funds) it thus needs to ask the user's device to sign. The user must hence be online to be able to receive funds, for example.

[^2]: As on-chain activity includes opening and closing channels, this means Voltage could theoretically try to infer who you have channels with. What's clear, however, is they can't see the Lightning transactions themselves.

[^3]: As there is no "the mempool" for the Bitcoin network, but rather many mempools that converge to approximately the same state, there is no "the graph" on Lightning. Rather, each node has its own view of the network, depending on its needs and capabilities, but they tend to be quite the same (although I'd expect more discrepancies between two Lightning graphs than between two mempools). This feature probably compares your node's graph to BoltObserver's to detect sync drops.

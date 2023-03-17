---
title: "Latest Strikes 26"
date: 2023-03-09T19:10:00+01:00
block: "780041"
cover:
    image: "../images/BuildersOfLightning.min.jpeg"
    alt: "An abstract representation of someone building on the Lightning Network."
    caption: "\"Builders Of Lightning\". Generated with DALL·E."
    relative: "false"
tags: ["bitcoin", "lightning"]
categories: ["strikes"]
draft: false
---

Live long and prosper 🖖 Welcome to the 26th issue of Latest Strikes! That's right, 26. At the yet unbroken pace of one issue per week, this means that it has been half a year since we started covering the amazing work of Lightning builders all around the world in this columns. Let's celebrate this half-anniversary in style with the thrilling developments of last week!

# Ecosystem

### Qala 🤝 BoltObserver 🤝 Nodl

Qala {{<newtabref href="https://blog.qala.dev/educating-the-next-wave-of-bitcoin-lightning-developers-across-africa/" title="announced">}} a partnership with {{<newtabref href="https://bolt.observer/" title="BoltObserver">}} and {{<newtabref href="https://www.nodl.eu/" title="nodl">}}, which aims to share and foster good node infrastructure and management practices with Qala's fellows.

{{<newtabref href="https://qala.dev" title="Qala">}} is an education program for experienced developers, helping them transition to a Bitcoin/Lightning career through a 3-months fully-funded fellowship. Out of the first cohort of 13 fellows in 2022, 12 graduated and are now working for Bitcoin/Lightning companies or have received open source grants. This partnership with BoltObserver (a node and liquidity management tool) and nodl (a Bitcoin/Lightning infrastructure provider) will give the fellows of the new cohort additional insights in how to efficiently and securely manage a Lightning node.

I really love to see this kind of synergies between high level education camps and Lightning companies, especially in Africa, where Bitcoin has a huge potential in terms of empowerment, financial inclusion and autonomy, while the current Lightning solutions are still not always perfectly tailored for the local context.

### First Bank To Join The Lightning Network

{{<newtabref href="https://www.xapobank.com/" title="Xapo">}} is the first bank worldwide to {{<newtabref href="https://nitter.lacontrevoie.fr/xapoprivatebank/status/1631293433057878019" title="join">}} the Lightning Network. Of course, Bitcoin and Lightning's essence is to make banks obsolete in the long term - or at least, to make them evolve into something so different that it can't really be compared to today's banks - but in the meantime it's good to see it being adopted by some of them.

Xapo, based in Gibraltar, describes itself as a crypto private bank, and already supported Bitcoin on-chain as well as some stablecoins. Bitcoin deposits and withdrawals can now be quicker than ever thanks to the integration of Lightning, through a {{<newtabref href="https://nitter.lacontrevoie.fr/davidmarcus/status/1631302716977815554" title="partnership">}} with David Marcus' {{<newtabref href="https://www.lightspark.com/" title="Lightspark">}}. The partnership consists in Xapo participating in Lightspark's closed beta for their yet to be revealed product, as this blog {{<newtabref href="https://www.lightspark.com/news/lightspark-powers-xapo-bank-lightning-payments" title="article">}} highlights. While the exact nature of Lightspark's offering isn't known to date, they seem to have developed a complete offering for businesses eager to join the Lightning network, from node provisioning, to node and liquidity management, as well as clients and SDKs to ease the integration into other apps.

### The Breez Open LSP Model

Roy from {{<newtabref href="https://breez.technology" title="Breez">}} wrote an excellent {{<newtabref href="https://medium.com/breez-technology/the-breez-open-lsp-model-scaling-lightning-by-sharing-roi-with-3rd-party-lsps-e2ef6e31562e" title="piece">}} describing the second pillar of the Breez's approach to scaling Lightning: money. Indeed, in his previous posts, Roy described the way the {{<newtabref href="../latest-strikes-23/#more-about-the-breez-sdk" title="Breez SDK">}} works, allowing developers to quickly and easily plug their apps to Lightning, while users retain the custody of their funds.

The second piece of the puzzle is deploying capital for users to use. Indeed, Lightning is known for its chicken-and-eggish problem of *inbound liquidity* where in order to receive payments a user either needs someone else to open a channel to them, or must first spend money themselves before they can receive. Part of the solution to this somewhat counterintuitive piece of user experience comes from Lightning Service Providers (LSPs) such as Breez or Acinq. In exchange for a fee, a LSP will open a direct channel to you with funds on their end of the channel, allowing you to receive money on Lightning. Users retain control of their funds because there is a real Lightning channel between them and their LSP(s).

To accelerate the emergence of new LSPs (which is paramount to getting more users on Lightning and triggering a virtuous cycle), Breez is therefore launching the "Breez LSP package", which provides new LSPs with downstream users (useful to bootstrap their service offering), a direct channel to the Breez node, as well as software to run their operation (e.g. opening channels to users, etc.). As Roy highlights, new LSPs only need to bring their own, always online Lightning node and their capital.

As I mentioned above, LSPs are a decisive part of the solution to Lightning adoption, alongside other improvements, both technical (dual-funding, liquidity ads, etc.) and social. I don't have a crystal ball, but I'm pretty sure they will continue to play a big role in the future, if only to serve mobile users. Non-custodial and with clear tradeoffs[^1], they are in my opinion one of the best shot we have at bringing Lightning to the masses while staying aligned with Bitcoin's core values. That's why I'm really pumped to see Breez dedication to opening the LSP game, to everyone's benefit. 

### Jack Dorsey's TBD Launches c=

Speaking of LSP, Jack Dorsey founded TBD just {{<newtabref href="https://nitter.lacontrevoie.fr/c_equals/status/1631324148499660803" title="launched">}} a new entity called {{<newtabref href="https://cequals.xyz/" title="c=">}} (pronounced "c equals"), which will bring liquidity to the network through a new LSP in order to make Lightning payments even more reliable and dependable.

Everything is still kinda blurry, but given the announced ambition to "help connect the next billion people to the Lightning Network", this new entity will likely deploy some substantial amount of capital into the network. Eager to see where this goes!

### LNP2P Bot Hacked

{{<newtabref href="https://lnp2pbot.com/" title="lnp2pBot">}}, a Telegram bot for trading bitcoin over Lightning with no KYC, suffered an attack where the database was deleted but no funds were stolen. Ongoing payments have been resolved manually, and the service is now {{<newtabref href="https://nitter.lacontrevoie.fr/lnp2pBot/status/1632288099798491138" title="back up">}} with a new {{<newtabref href="https://amboss.space/node/0380c5536d70b81137cb72fc71c262f50a3ec5a6fa9e517ef3637d889fb0b7e3db" title="node">}}.

### Ghost Checkout In Mash

Remember {{<newtabref href="https://www.mash.com/" title="Mash">}}? We covered the news in {{<newtabref href="../latest-strikes-16/#mash-gets-a-lifting" title="Latest Strikes">}} when this monetization service got a lifting back in December 2022. Until last week, it was required to have a Mash account in order to be able to spends sats on a Mash-enabled website. But this time is gone! It is {{<newtabref href="https://nitter.lacontrevoie.fr/getmash/status/1630191485999017984" title="now">}} possible to send sats to your favorite content producer straight from your own Lightning wallet.

Using a Mash account still brings some benefits, such as one-click payments and automatic contributions. The team behind Mash is working on bringing more Lightning-native functionalities, which won't require an account. Until hopefully, someday, the whole Mash experience is non-custodial?

### Where Are We At With Micropayments?

Speaking of Mash, its CEO Jared Nusinoff wrote an in-depth {{<newtabref href="https://bitcoinmagazine.com/culture/with-bitcoin-micropayments-can-work" title="article">}} rebutting the pontificated 1999 {{<newtabref href="https://nakamotoinstitute.org/static/docs/micropayments-and-mental-transaction-costs.pdf" title="paper">}} by Nick Szabo that established the truism that micropayments can't work (which Szabo himself {{<newtabref href="https://unenumerated.blogspot.com/2007/05/micropayments-redux.html" title="nuanced">}} in 2007).

The article (a recommended read, in case that wasn't clear) sheds light on common misconceptions around what Szabo meant when writing that micropayments would never work back in 1999 (basically, that you wouldn't see people paying nano tiny amounts every time they use a service or a product, unlike what's showed in the Black Mirror episode {{<newtabref href="https://en.wikipedia.org/wiki/Fifteen_Million_Merits" title="Fifteen Million Merits">}}, where the hero makes a transaction to buy a dab of toothpaste every time he brushes his teeth). I think we can all agree this would be pretty dystopian. But Szabo's micropayments are often conflated with today's micropayments, which have a complete different meaning: buying a news article, buying a sub on Twitch, etc. Micropayments happen all the time on the internet, and technology such as Lightning only bring even further down the floor of the minimum amount.

On the other hand, Szabo is right that the mental cost of a transaction is the final frontier. With technologies such as Lightning, most of the actual cost of doing a transaction is mental: what am I getting in exchange of this 100 sats? Is is worth it? This burden can be - actually, is - lightened with clever engineering and UI. In Podcasting2.0, sats are streamed automatically without further intervention from the listener, who can still drop an occasional *boost* if they hear something they particularly enjoy. Wallets/apps such as Mash or Alby allow users to set up a budget ({{<newtabref href="https://nitter.lacontrevoie.fr/getAlby/status/1630574178129649666" title="here">}} in action on nostr for example), so that all it takes to send sats is one click.

I'm already having a mental transaction cost when deciding to hit the "thumb up" button under a post or a video. And yet I leave a trail of *likes* and *favs* behind me in the dark forest of cyberspace. If anything, having the ability to do microtransactions as simply as that will only bring more light by financing good, meaningful content, helping all the Little Thumblings of the internet to find their way back home.

### BuildOnL2 Is Live

Blockstream opened its "Build On L2" community platform, announced a few months ago. The {{<newtabref href="https://community.corelightning.org/home" title="Core Lightning">}} community aims at gathering people building on the Lightning implementation or using it, with general discussions, guides and events. We're still at the beginning, but I'm really looking forward to what happens there!

### Make The Good Apparel Happen

Do you like cool Lightning apparel? I do! The very talented NoGood launched a crowdfunding campaign on {{<newtabref href="https://geyser.fund/project/nogood" title="Geyser">}} to collect enough money to launch a new collection! The first milestone was reached quite quickly, allowing NoGood to send the T-shirts design to production, but there's still more to come.

I really love NoGood's work, including this amazing {{<newtabref href="https://www.youtube.com/watch?v=h69snvlGLXU" title="LoFi Radio Station">}} that often accompanies the writing of this newsletter, so it felt right to give this campaign a little shout out here.

## Wallets & Tools

### Breez Updates Fees

Breez {{<newtabref href="https://nitter.lacontrevoie.fr/Breez_Tech/status/1630280532306059265" title="increased">}} their channel opening fees, from 0.4% to 0.75%. The minimum fee remains the same: 2000 sats. After Wallet Of Satoshi's fee {{<newtabref href="../latest-strikes-23/#walletofsatoshi-revisits-fee-structure" title="increase">}} a few weeks ago, it's interesting to see how the new fee environment propelled by the Inscriptions craze can affect Lightning wallets.

### BTCPay 1.8.0

BTCPay Server v1.8.0 is {{<newtabref href="https://nitter.lacontrevoie.fr/BtcpayServer/status/1630976919305846804" title="out">}}. This huge release bundles and builds upon a lot of the improvements we've seen in the past month. It notably includes a revamped checkout interface, with custom checkout forms: you can now collect any information you see fit from your customers (special instructions, a message to write on a card, a nostr public key for delivery notification, you name it!).

### LNBits Update

The new LNBits {{<newtabref href="https://github.com/lnbits/lnbits/releases/tag/0.10" title="release">}} brings the big modification we already covered back in {{<newtabref href="../latest-strikes-21/#lnbits-release" title="January">}}: extensions are no longer part of LNBits core, and will instead live in separate repositories, where they can be more easily maintained. Admins will be able to install and manage extensions from a dedicated interface, and the LNBits team will also maintain a list of vetted extensions.

This release paves the way for an even richer extensions ecosystem in LNBits, if that was possible. Promising!

### Lightning Addresses Coming Soon To Blixt

Hampus {{<newtabref href="https://nitter.lacontrevoie.fr/hampus_s/status/1630219164265619456" title="shared">}} a new incoming feature for {{<newtabref href="https://blixtwallet.github.io/" title="Blixt">}} which will allow users of the mobile wallet to receive funds to a Lightning Address in a *trust minimized* fashion. The idea is to have an always online service called *Lightning Box* that is in charge of receiving the payment on behalf of the user and notify the wallet/user, which will then automatically withdraw the funds the next it comes back online.

Alternatively, if the wallet is already online, the *Lightning Box* does not take custody of the funds. Instead, it will directly ask the wallet for an invoice, and then forward it to the sender. This way, the sender pays the wallet directly, and the box only acts as a trusted proxy. This is something that could be done by LSPs: upon receiving a payment, sending a push notification to wake up the wallet on the user's phone, and transfer the payment without taking custody of the funds. Of course, this is harder than it looks, and greatly depends on how much phones constrain apps while they're not in the foreground.

However, it is important to keep in mind that, as for any similar setup, the *Lightning Box* could be rogue and respond to requests from people trying to pay a user with its own invoices, thus undetectably stealing money that was supposed to be for the end user. It could do so with small amounts to reduce the chances of being detected, and steal a substantial amount of money in the long run. Definitely something to keep in mind (DarthCoin wrote a {{<newtabref href="https://stacker.news/items/147230/r/FanisMichalakis" title="guide">}} on that topic, although I don't agree with everything in there and I would definitely avoid trusting someone I don't know personally, be it the mighty fiatjaf!).

### Handling Lightning Unpredictable Fees In eCash

The team behind {{<newtabref href="../latest-strikes-2/#cashu" title="Cashu">}} published an interesting {{<newtabref href="https://nitter.lacontrevoie.fr/callebtc/status/1629776855573168129" title="solution">}} to the problem of unpredictable fees in Lightning in the context of e-cash mints. The issue arises from the fact that:

1. The fees of a Lightning payment cannot really be guessed beforehand, and you only learn them while doing the actual payment[^2]. The user of a mint thus needs to pay an upfront fee, which must be equal or superior to the actual fee paid by the mint when sending the payment over Lightning.
2. E-cash tokens are not divisible, so there's no concept of "change" *per se*, where the mint could simply send the excess fee back to the user.

The solution put forward is the following: the user sends to the mint the amount they want to transfer on Lightning plus the maximum fee for this amount (called the *fee reserve* and publicly available, it is the maximum fee the mint is ready to pay to send said amount on Lightning). Alongside with the tokens, the users also sends a few blinded messages (a bit like when asking the mint for new tokens, except there is no value on this messages yet). The mint then sends the Lightning payments, uses the provided reserve to pay the fees, and returns any remains by adding amounts to the messages and signing them, thus creating new e-cash tokens. There's a granularity issue here, because e-cash tokens are denominated in powers of 2 (1 sat, 2 sats, 4 sats, etc.), so depending on the amount to be returned and the number of blinded messages provided, the mint may or not be able to return the whole fee excess. Still, this mechanism does the job, and it's always possible to use more blinded messages to get more granularity.

I found this particularly interesting because unpredictable Lightning fees can be a tiring beast sometimes. For example, they make it harder for a service to allow you to withdraw your full balance in only one Lightning payment, because the service needs to reserve part of your balance for the fees but isn't sure how much. Here, the struggle is a bit different (not so much being able to withdraw an exact amount, but being able to get the excess fee back to your wallet) due to the nature of e-cash mints, but the solution is quite interesting.

The only shortcomings I see are that:
- this "change" mechanism doesn't work out of the box for third-party Lightning gateways (e.g. entities connected to a mint that will accept e-cash tokens and perform the payment on Lightning) as they don't have minting capabilities, requiring an additional round of communication (between the gateway and the mint server) that can ultimately be denied by the mint server, which would therefore be the only Lightning gateway on said mint able to return fee excess to users ;
- as far as I understand, there is no way for the user to know what fee the mint actually paid to send the funds on Lightning, so the mint can very much pocket anything it wants. Still, we're in a better position than before: from "the mint can't return any change" to "the mint can return change if it wants to".

Also, this shortcomings are in my opinion quite quintessential to the trusted nature of e-cash mints, so I'm not sure there's much we can do to alleviate them.

## Spec & Implems

### Core Lightning v23.0.2

Core Lightning is back with a terrific release and its hilarious name! {{<newtabref href="https://github.com/ElementsProject/lightning/releases/tag/v23.02" title="Core Lightning v23.02 \"CBDC Backing Layer\"">}} brings tons of bug fixes and performance improvements (notably for large nodes), new commands for end users, compatibility improvements and some new, experimental features.

The compatibility improvements touch a wide range of the Lightning protocols, but the two big ones that I spotted are {{<newtabref href="https://github.com/ElementsProject/lightning/pull/5892" title="Blinded Paths">}} and {{<newtabref href="https://github.com/ElementsProject/lightning/pull/5956" title="Dual-Funding">}} compatibility with Eclair. Blinded Paths allow a receiving node to hide its identity when getting paid, by computing the end of the path instead of letting the sender node do it ; while Dual-Funding enables nodes to natively open channels where both nodes contribute to the funding, and where the channel is hence created with liquidity on both side. As the reader can see, this two new protocol improvements of course require careful engineering so that all implementations are compatible with one another, which is closer than ever to be the case for Core Lightning and Eclair! However, if you're a Core Lightning user of this features, note that while this release brings compatibility with Eclair, it breaks compatibility with older versions of Core Lightning (but you can't make an omelette without breaking eggs, can you?).

On the experimental features side, this release brings a new interesting functionality called "Peer Storage" where a node can distribute its encrypted backup to its peers, from where it can later be recovered in case of complete data loss. Note that the term "peer" refers to another node you're communicating with, not necessarily a channel partner. Cool idea!

### The LNURL vs BOLT12 Debate Rages Again

Last week also saw a comeback of the never-ending debate opposing LNURL Pay and Bolt12. The debate went around the privacy, censorship resistance and custodianship aspects. To put it in a nutshell, LNURL relies on the existing internet infrastructure (that is, DNS and web servers) to enable LNURL-Pay links (such as lnurl1dp68gurn8ghj7ctsdyhxcmndv9exket5wvhxxmmd9amrztmvde6hymp0wpshjtmjv4ch2etnwslku0f5vfnrvd35vy6rvdp4vd3nzetxye6kjepaxy6ngdr9893kxtfnxu6nwtf5vvckxttzvverxtfhx93nyctxxqmnvdpevgn8x6t8deshgatjv57kzvfj8pskvefkvvmrsvnyx3nx2epevg6nyv35v5urqwtyx5mk2dmrxp3ngvfexvexvcmzxgcnzctrvsuxzdrzvfjkvwryxdjnvd3exqfn44sl) and Lightning Addresses (such as fanis@lnmarkets.com) to resolve to an actual Lightning invoice. Bolt12, on the other hand, uses the Lightning communication network itself to resolve another kind of static identifiers called Offers (such as lno1pqqnyzsmx5cx6umpwssx6atvw35j6ut4v9h8g6t50ysx7enxv4epyrmjw4ehgcm0wfczucm0d5hxzag5qqtzzq3lxgva5qlw9xsjmeqs0ek9cdj0vpec9ur972l7mywa66u3q7dlhs).

First, let's address the elephant in the room: while we can compare LNURL Pay strings and Bolt12 Offers because they look quite the same at first glance (lengthy alphanumerical strings), Lightning Addresses are a different beast. You can send money to someone as simply as sending an email. And in fact, while Lightning Addresses are mostly used with LNURL today, you could easily make one resolve to a Bolt12 Offer instead. The downside of Lightning Addresses is that you rely heavily on existing, easily censorable internet infrastructure.

Same goes for LNURL itself. When optimizing for privacy and censorship resistance, Bolt12 (not only Offers, but also stuff that comes bundled with it such as Blinded Paths) is (will be) clearly superior. But that's not telling the whole story. LNURL is practical **today** in a wide range of contexts, from social media tipping to actual trade. While the receiver currently has to deal with the absolutely unsatisfactory trade-off between privacy and self-custody[^3], it will not necessarily always be the case (for example, Blinded Paths could benefit LNURL as much as Offers). LNURL is a client-server protocol, and using web servers and DNS carries its censorship risk, but at least it leverages an existing, well functioning network. Bolt12 are a bit of the opposite (although it's a stretch to say that): peer-to-peer, they use the rails of a very censorship-resistant, yet quite new and still "frail" network. This is impactful both for ease of use and ease of integration.

Like many, I strongly believe there is room for both LNURL and Offers, especially today. There use cases overlap, but not completely (at all). They both have their weaknesses, and talented people are exploring ways to address them. For example, Evan Kaloudis is currently working on a {{<newtabref href="https://github.com/lnurl/luds/pull/204" title="proposal">}} to address the stealing attacks of LNURL servers, although it is a bit hard to reconcile with privacy. Ultimately, once we have Blinded Paths, the right thing to do would be to run one's own LNURL server to get the better of both words, which developers have shown to be quite an {{<newtabref href="https://nitter.lacontrevoie.fr/hampus_s/status/1632769530207301632" title="easy">}} {{<newtabref href="https://nitter.lacontrevoie.fr/EricSirion/status/1632422391698579456" title="task">}} to achieve once someone is already running running a Lightning node (although it requires going through Tor).

Ultimately, users will see what fit their use case best, and if both protocols were to stay in usage, I suspect it would be for very different use cases.

### LNURL-Pay Over Nostr

Andrew Camilleri {{<newtabref href="https://github.com/lnurl/luds/pull/203" title="proposed">}} a way to use Nostr to offer LNURL endpoints without web servers! It really reminds me of Dan Gould's Serverless Payjoins {{<newtabref href="https://nitter.lacontrevoie.fr/bitgould/status/1620789534094131201" title="proposal">}} where he proposed a way to perform payjoins without servers by relying on untrusted relays to (rings a bell?) to pass the data around.

Here, we take advantage of the fact that nostr in based on public key cryptography at its core to send encrypted messages between a sender and a receiver. Nostr relays are responsible for transferring the data, as with any regular nostr notes. To put it in a nutshell, while in the regular LNURL flow the payer's wallet discusses with a web server, which in turn gets an invoice from the receiver's node, here the sender's wallet can discuss directly with the receiver's node over nostr. We don't need a web server in between any more, and we don't need to trust the relays because the data is encrypted with nostr keys, thus providing both privacy and tamper-resistance.

Reflecting on this proposal and this {{<newtabref href="https://nitter.lacontrevoie.fr/arcbtc/status/1631252194463830018" title="tweet">}} from Ben Arc, I believe I might have over-hyped Zaps a bit in the last newsletters. It echoes with the privacy and relevance aspects we covered last week, and overall I'm less and less convinced that they're such a good thing. They're fun but, in the end, they don't bring much value to the table and are trivially gameable. Or maybe I'm missing something.

## Closing Bit

Qu'importent les honneurs, la fortune et la gloire ?\
Si sans grand tremblement, d'un décret péremptoire\
Quelques hommes - des hommeaux - peuvent sans s'émouvoir\
Tout saisir, déchirer, répandre pour leur gloire!

Car enfin, s'il s'agissait de quelque choix commun\
D'un potlach nécessaire auquel on se soumet\
Il n'y aurait rien à dire, et rien à déplorer.\

Le problème, camarades, illustres compagnons\
C'est qu'ici bien souvent la main est aux mignons\
Qui s'arrangent très bien de saigner un chacun\
Pour apporter son eau à leur propre moulin.

---

Want to receive Latest Strikes straight to your inbox every week? Couldn't be easier: subscribe to {{<newtabref href="https://blog.lnmarkets.com" title="LN Markets Ghost blog">}} and you're all set (remember to confirm your subscription by clicking the link sent via email).

---

If you enjoyed this recap, you can show your appreciation by throwing a few coins to *fanis @ lnmarkets.com*, by scanning or clicking the QR code.

Thank you!

{{<figure align=center src="../../images/lnm_lnurl.png" link="lightning:fanis@lnmarkets.com">}}


[^1]: The most obvious tradeoff, which is common to all LSPs, is that if it suddenly ceases to operate or goes rogue, you can't use its channels anymore to send or receive on Lightning (but you can still get your funds back on-chain). This, along with other centralization risks, can be mitigated by using several LSPs, hence having multiple channels with inbound liquidity with different peers. That's one more reason why this ongoing effort toward openness and {{<newtabref href="https://github.com/BitcoinAndLightningLayerSpecs/lsp" title="standardization">}} is so important.

[^2]: This can be mitigated by probing the network before hand to get a better picture of what the fees will be for the actual payment. But this comes with its own challenges.

[^3]: The tradeoff is the following: if I'm self-hosting everything, then I'm inevitably leaking my node's address on the internet for everyone to see, and hence revealing that I own the UTXOs that this node uses to open channels. This is a very good introduction point to try to do some prospective and retrospective analysis and follow my funds on the bitcoin chain. On the other hand, if I'm using a custodial service, I get to hide my own node from the public but am exposed to theft or loss of my funds. Finally, if I'm connecting my own node to a trusted web server, I'm enjoying the **worst** of both worlds: poor privacy because I still leak my node address, and poor security because the server can easily substitute its own invoices to mine (although there are propositions to mitigate that, as the reader will see in a few moments).
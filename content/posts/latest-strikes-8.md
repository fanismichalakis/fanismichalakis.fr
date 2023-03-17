---
title: "Latest Strikes 8 - Oct 30th"
date: 2022-10-31T16:40:00+01:00
block: "761123"
cover:
    image: "../images/DALL·E_2022-10-31 16.18.50.png"
    alt: "A cyberpunk tesla coil spitting out electric arcs"
    caption: "'A cyberpunk tesla coil spitting out electric arcs'. Generated with DALL·E."
    relative: "false"
tags: ["bitcoin", "lightning"]
categories: ["strikes"]
draft: false
---

## Ecosystem

### Grants

The OpenSats initiative has {{<newtabref href="https://nitter.lacontrevoie.fr/gladstein/status/1586098031501447169" title="announced">}} two new grant attributions: {{<newtabref href="https://nitter.lacontrevoie.fr/jb55" title="William Casarin">}} received the "Tip Jar" grant for his work on {{<newtabref href="https://lnlink.app/" title="LNLink">}}, an iOS app to manage one's Core Lightning node ; while {{<newtabref href="https://nitter.lacontrevoie.fr/callebtc" title="Calle">}} was awarded the "E-Cash" bounty for his work on {{<newtabref href="https://nitter.lacontrevoie.fr/CashuBTC" title="Cashu">}}, a Lightning-enabled Chaumian ecash implementation.

The non profit {{<newtabref href="https://opensats.org/" title="OpenSats">}} initiative created 3 special Lighting {{<newtabref href="https://nitter.lacontrevoie.fr/gladstein/status/1472961294915432455" title="grants">}} back in December 2021, funded by the {{<newtabref href="https://hrf.org" title="Human Rights Foundation">}} (HRF) and {{<newtabref href="https://strike.me" title="Strike">}}, awarding bounties to open source projects building wallets and tools providing useful features for dissidents worldwide. The "Tip Jar" bounty was created to reward a non custodial wallet allowing users to receive Lightning payments to a BOLT12 static payment code, without revealing the public key or IP of the receiver. The "E-Cash" bounty was created to reward a wallet that would allow its users to use Chaumian e-cash and benefit from its privacy addons.

LnLink allows users to interact with a remote Core Lightning node (theirs, or someone else's in more contrived scenarii) by issuing commands through the Lightning Network itself, thanks to Core Lightning's *commando* plugin. The app notably allows generating BOLT12 Offers, thus qualifying for the 1 BTC "Tip Jar" grant.

Cashu allows user to deposit and withdraw funds to and from Chaumian e-cash mints, as well as transfering ecash tokens between users of the same mint ; while the central server of the mint cannot link the ecash tokens it issues to who it issues them to, nor track them when they're transferred. At the moment, Cashu only qualifies for half of the "E-Cash" bounty (0.5 BTC) because it is still possible for the mint administrator to track users' IP addresses, but work is already underway to add {{<newtabref href="https://nitter.lacontrevoie.fr/callebtc/status/1586519088494321664" title="Tor support">}} into Cashu.

### Zero Fee Routing Shuts Down Operations

Lightning Network OG Zero Fee Routing {{<newtabref href="https://nitter.lacontrevoie.fr/zerofeerouting/status/1586053522029936641" title="announced">}} the shutting down of their famous Lightning node, because of the upcoming release of a new little human in their family.

Zero Fee Routing, as the name entails, was famous for his zero-fee routing node: it would forward payments absolutely free of charge. The node quickly became one of the most connected on the network, as this {{<newtabref href="https://nitter.lacontrevoie.fr/zerofeerouting/status/1586401292473184256" title="snapshot">}} of the network's statistics, taken 24 hours after the shut down announcement, shows. 

Thank you very much for your service, and all the best for this new adventure!

### Wolf Accelerator

New York City is now the home of the {{<newtabref href="https://wolfnyc.com/the-program" title="Wolf Accelerator Program">}}. Focused solely on Lightning startups, {{<newtabref href="https://nitter.lacontrevoie.fr/_WolfNYC/status/1585270385934753792" title="Wolf">}} provides an 8 weeks in-person acceleration program, with free lodging and transportation to NYC, $250k guaranteed seed funding, mentoring investors and much more!

Applications are open, until 31st December for the first pack.

### CashApp

CashApp users can {{<newtabref href="https://nitter.lacontrevoie.fr/nobsbitcoin/status/1584954348370595840" title="now">}} receive Lightning payments! The 40 million users of CashApp were previously only able to send Lightning payments: they can now receive through a {{<newtabref href="https://bips.xyz/21" title="BIP21">}} Unified QR Code!

### Designathon Results

The Bitcoin Design Community {{<newtabref href="https://nitter.lacontrevoie.fr/bitcoin_design/status/1585309452499963905" title="announced">}} the winners of the {{<newtabref href="https://event.bitcoin.design/" title="Designathon">}}, some of which are participating in the ongoing LegendsOfLightning tournament by BoltFun.

- {{<newtabref href="https://makers.bolt.fun/project/BitKids-App" title="BitKid">}} is a cool wallet for kids to receive their first bitcoin and spend some using Lightning. The user interface is colorful, and illustrations are preferred to text. For example, the amount can be displayed with a schematic representation consisting in "dots" to be counted, instead of numbers.

- {{<newtabref href="https://makers.bolt.fun/project/agrimint" title="AgriMint">}} is a Lightning-enabled mint for rural communities in Sub-Saharan Africa which interconnects with USSD, enabling people to use Bitcoin without even an internet connection.

- {{<newtabref href="https://makers.bolt.fun/project/LNDg" title="LNDg.xyz GUI 2.0">}} is a new lightweight GUI for the Lightning node management automation tool.

### Apollosats

{{<newtabref href="https://heyapollo.com/" title="Apollo">}} allows you to post reviews of your favorite Bitcoin and Lightning products, and earn Bitcoin for every review you post, as well as every time someone finds your review useful. A bit more than a week after launch, Apollo already counts over {{<newtabref href="https://nitter.lacontrevoie.fr/sahil_21m/status/1584965901027188737" title="200 reviews">}} for a wide range of products.

### Some Lightning Gaming

A new Lightning-enabled gaming platform is {{<newtabref href="https://nitter.lacontrevoie.fr/lngamesapp/status/1584972860082122754" title="coming around the corner">}}, while THNDR Games proposes {{<newtabref href="https://nitter.lacontrevoie.fr/THNDRGAMES/status/1585275967261462528" title="new ways">}} of winning some sats in games.

I also stumbled into a {{<newtabref href="https://proofofword.thomasjohns1.repl.co/" title="Bitcoin WORDLE">}} while browsing on {{<newtabref href="https://stacker.news/items/87032" title="StackerNews">}}. Very fun, and the perspective of losing sats if you don't find the answer after 6 guesses adds for a unique spiciness! Please note, however, that there seems to be some problems for mobile browsers, so better play on desktop!

### Kollider Raises $2.4M

Kollider announced their {{<newtabref href="https://nitter.lacontrevoie.fr/kollider_trade/status/1585310681787944962" title="official launch">}} and their {{<newtabref href="https://nitter.lacontrevoie.fr/Lemniscap/status/1585420751317893122" title="$2.4 million fundraise">}}. Congrats!

### Satimoto Soon?

Seems like {{<newtabref href="https://satimoto.com/" title="Satimoto">}} is getting {{<newtabref href="https://nitter.lacontrevoie.fr/SatimotoApp/status/1583469266913091585" title="closer">}} and {{<newtabref href="https://nitter.lacontrevoie.fr/SatimotoApp/status/1585367962516852736" title="closer">}} from release! Soon you'll be able to charge your electric vehicle using the power of Lightning!

## Wallets & Tools

### Lightning PayJoins

The process of opening Lightning channels can be cumbersome, especially if you're spinning up a new node and need to open a few channels to begin with. Usually, you'd have to send funds on-chain from some of your pre-existing wallets to your new node. Then, once this deposit is confirmed, you'd need to open each new channel separately, requiring an additional Bitcoin on-chain transaction for each channel opening.

{{<newtabref href="https://nolooking.chaincase.app/" title="Nolooking">}} takes advantage of PayJoin (Pay-to-EndPoint) to achieve the same in only one transaction, saving users fees and adding some degree of privacy.

{{<figure src="../../images/LatestStrikes8-On_chain_footprint_Naive_vs_Nolooking.jpg">}}

The {{<newtabref href="https://chaincase.app/words/lightning-payjoin" title="key idea">}} is that instead of coordinating everyting on-chain through various transactions, the initial funding transaction performs a Pay-to-EndPoint transaction, the endpoint being provided by the Lightning node. In simple terms, what it means is that the initial wallet sends a message to the Lightning node, stating that they're willing to send a certain amount of bitcoin. The node then responds with a transaction that spends the same amount, but opens the channels instead of sending to a single address like a "regular" transaction would do. Because it spends the same amount as initially stated, the sending wallet accepts this proposition and proceeds to the spend.

You can already give it a try on this {{<newtabref href="https://nolooking.chaincase.app/pj/static/index.html" title="demo">}}, where the Nolooking app is connected to the the Nolooking team's Lightning node. It will hence open channel(s) between the team's node and the nodes you specify in the app. An {{<newtabref href="https://getumbrel.com" title="Umbrel">}} application already {{<newtabref href="https://nitter.lacontrevoie.fr/utxoclub/status/1585703047124389888" title="exists">}}, and is in the {{<newtabref href="https://github.com/getumbrel/umbrel-apps/pull/229" title="process">}} of being published in the Umbrel App Store, so soon every user running an Umbrel node should be able to open channels in their Lighntning node from any compatible, BIP78-enabled wallet (for example, {{<newtabref href="https://sparrowwallet.com/" title="Sparrow">}}).

### New Umbrel Release Brings Community App Stores

Speaking of Umbrel, the project {{<newtabref href="https://nitter.lacontrevoie.fr/umbrel/status/1584942522551631874" title="released">}} v0.5.2, which introduces Community App Stores. Anyone can now publish their own Umbrel App Store, and users can decide to pull from whichever store(s) they see fit. A very good news in terms of censorship resistance and ease of use, as it would for example allow users to use Bitcoin-stuff-only app stores if they're not interested in the rest, and vice versa.

### Zion V2

Zion {{<newtabref href="https://scribe.rip/announcing-zion-v2-a-web5-app-44ac7d66b1e1" title="shared">}} their vision for the V2 of their app, that leverages {{<newtabref href="https://developer.tbd.website/projects/web5/" title="TBD's Web5">}} to provide decentralized identity, messaging and data storage, while relying on the Lightning Network for payments.

I'm still unsure whether the {{<newtabref href="https://identity.foundation/" title="DIF">}}'s vision for decentralized identity (and everything that surrounds it) will be the one that prevails in the future, but it's still interesting to follow along as progresses are made.

### BitKit

On a slightly different note, {{<newtabref href="https://synonym.to" title="Synonym">}} released the first version of their wallet {{<newtabref href="https://synonym.to/products/bitkit" title="BitKit">}}, which stands for "Bitcoin Toolkit". The app integrates both on-chain and Lightning Bitcoin, with a nice UI to allocate funds from a savings account (on-chain) to a spending one (Lightning).

It also features a strong social/identity aspect using {{<newtabref href="https://slashtags.to/" title="Slashtags">}}, where user can create a profile, pay to their contacts' profiles, retrieve data from widgets, and so on. The list of possibilities enabled by this kind of constructs can be quite long, but here are two that I personnaly like a lot:
- pay using a contact's favorite receiving method automatically: no more need to send a message to someone asking if they prefer on-chain or Lightning, and requesting them to send an address or an invoice. You wallet will instead pull the data from your recipient's profile, see that their prefer to teceive via Lightning, and ask for an invoice.
- see and interact with funds on exchanges directly from your BitKit app, thanks to widgets. This is something that is already possible with things like {{<newtabref href="https://github.com/lnurl/luds/blob/luds/14.md" title="LNURL">}}, but not widely implemented yet. Imagine withdrawing from your custodian (*bad!*) account to your self-sovereign (*good!*) wallet, directly from the comfort of your wallet. Sweet, init?

### Amboss

Amboss {{<newtabref href="https://nitter.lacontrevoie.fr/ambosstech/status/1585290480769650690" title="published">}} a big release this week, with the ability for node operators to share some otherwise private data about their node and channels with the rest of the world. While everyone, including the Amboss team, understands the importance of privacy, it is true that the concealed nature of the repartition of funds inside channels has led to an increasing number of actors probing the network to try to guess where the liquidity is. Why not offer the possibility for node operators willing to do so to disclose how the funds are distributed inside channels? Of course, one could argue that this favors nodes willing to compromise on privacy, thus lowering the bar accross the network, but it was only a matter of time until such tools were built anyway.

The Amboss team built a connector inside Thunderhub that allows node opeators to publish their data to a single endpoint, and make them available to everyone on their Amboss page. The tools also enables user to specify whether they want this data to be vague (eg only say if roughly 0%, 25%, 50%, 75% or 100% of a channel liquidity is on the local/remote side) or precise (display the exact percentage). User can even connect their node to Amboss but keep this data private: data is still sent to Amboss, but only displayed for the node's owner.

For premium users, the release also comes with a new tool to visualize arbitraging opportunities where liquidity isn't priced correctly across the network. For those interested, Danny Diekroeger explained in details what this arbitrage techniques can look like in {{<newtabref href="https://bitcointv.com/w/nepbbrGt3WBSDV4DZKGx2p?start=26m37s" title="rip #370 of TFTC">}}.

Read the full announcement {{<newtabref href="https://scribe.rip/lightning-balance-sharing-and-network-statistics-32e687a4db25" title="here">}}.

## Vids & Pods

### A cool interview of Thaddeus

During {{<newtabref href="https://surfinbitcoin.com/" title="Surfin'Bitcoin">}} last summer in Biarritz, France, Grand Angle Crypto recorded a very cool {{<newtabref href="https://www.youtube.com/watch?v=1Q_uoID-BDY" title="interview">}} of Thaddeus Dryja, which they published this week.

## Specs & Implems

### Dual Funding: Who Signs First?

There was an interesting {{<newtabref href="https://github.com/lightning/bolts/pull/851#issuecomment-1290727242" title="discussion">}} on dual funding through liquidity ads, and whether the initiator or the liquidity provider should sign the dual funding transaction first.

Ordering is important because whomever signs first is locking up their funds involved in the transaction for some period of time. While their funds are not at risk, it remains an attack vector, which could be used by attackers looking at harming specific targets or causing denial of service, simply by waiting for their victim to sign and then not signing themselves.

The discussion seems to have converged on the default being "largets contribution goes last", eg. the node that contributes the least funds to the dual funding signs first, and only then does the one that contributes the most funds sign. It helps align incentives of participants with what is at stake, while ensuring an attacker must always have more funds on the balance than their victim. Additionnaly, nodes could signal that they're willing to take part in the dual funding process only if they sign last, with no consideration of whether they're the main contributor of funds or not. This is useful to protect large liquidity providers from DoS attacks, while ensuring new nodes can still batch channel opens when they join the network.

### A pragmatic, unsatisfying work-around for anchor outputs fee-bumping reserve requirements

Bastien Teinturier sent a {{<newtabref href="https://lists.linuxfoundation.org/pipermail/lightning-dev/2022-October/003729.html" title="proposal">}} for what he calls a "pragmatic, unsatisfying work-around for anchor outputs fee-bumping reserve requirements".

Since the addition of {{<newtabref href="../anchor-outputs/" title="Anchor Ouputs">}} to the Lightning protocol, Lightning nodes are faced with the necessity of maintaining a stash of available UTXOs to be used to fee-bump channel closing transactions if needed. This effectively locks up UTXOs that could be used elsewhere, hence the proposition to instead sign multiple commitment transactions each time the channel state changes, to account for different feerates. For example, peers of a channel could agree to sign 5 commitment transactions at each update, with feerates ranging from 1 sats/vBytes to 5 times the current fee rate at signature time, for example.

As Bastien himself highlights, this solution, while easy to implement, is pretty unsatisfying as it doesn't really allow for any kind of precise feerate tuning. Its main benefits are that it removes the necessity of keeping some UTXOs ready in the Lightning node's wallet, thus improving their security and/or allowing them to be used elsewhere.

## Closing Bit

Une feuille tombe\
L'aiguille recule\
Le chant du coq\
-- Un nouveau bloc.

---

If you enjoyed this recap, you can show your appreciation by throwing a few coins to *fanis @ lnmarkets.com*, by scanning or clicking the QR code.

Thank you!

{{<figure align=center src="../../images/lnm_lnurl.png" link="lightning:fanis@lnmarkets.com">}}
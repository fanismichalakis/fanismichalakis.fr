---
title: "Latest Strikes 12"
date: 2022-11-28T18:20:00+01:00
block: "765068"
cover:
    image: "../images/DALL·E 2022-11-28.png"
    alt: "The Tables of the Law hit by a lightning strike, digital art"
    caption: "'The Tables of the Law hit by a lightning strike, digital art'. Generated with DALL·E."
    relative: "false"
tags: ["bitcoin", "lightning"]
categories: ["strikes"]
draft: false
---
## Wallets & Tools

### Who Needs A Lightning Wallet When You Have A Browser?

Remember the Mutiny Web Wallet we discovered in {{<newtabref href="../latest-strikes-10/#mutiny-web" title="Lastest Stikes #10">}}? The team behind the project made some significant progress and the perfect {{<newtabref href="https://nitter.net/futurepaul/status/1595787240403501056" title="video announcement">}}. The web wallet now provides all the features you'd expect from a Lightning wallet: send and receive Bitcoin on-chain, open Lightning channels and transact on Lightning. For example, Ben Carman recorded a {{<newtabref href="https://nitter.lacontrevoie.fr/benthecarman/status/1595395624010190850" title="demo">}} of him using Munity Web to buy an OP_RETURN transaction on {{<newtabref href="https://opreturnbot.com" title="OP_RETURN bot">}}.

Behind the scenes, Mutiny Web leverages the {{<newtabref href="https://github.com/bitcoindevkit/bdk" title="BDK">}} and {{<newtabref href="https://lightningdevkit.org/" title="LDK">}} libraries inside a Lightning node written in Rust and compiled to Web Assembly so that it can be loaded in the frontend (written in React Typescript).

Needless to say that the ability to run a freakin' non-custodial Lighnting node in the browser is **huge**. Of course, there are still a lot a improvements to be made, and a browser wallet has inherent limitations, notably when it comes to being always online and dealing with persistent storage. But as the teams puts it:

> Of course, we don't have to stay in the web page. This could be a browser extension, it could be a mobile and desktop app, it could run on a server, etc. By getting a node to run in the most constrained environment, we're setting ourselves up to, ultimately, run anywhere (and even distributed).

So huge congrats to{{<newtabref href="https://nitter.net/futurepaul" title="futurepaul">}}, {{<newtabref href="https://nitter.lacontrevoie.fr/benthecarman" title="Ben Carman">}} and {{<newtabref href="https://github.com/TonyGiorgio" title="Tony Giorgio">}} for their amazing work. Can't wait for what they have next for us!

### New BTCPay Server Release

BTCPay Server v1.7.0 was {{<newtabref href="https://blog.btcpayserver.org/btcpay-server-1-7-0/" title="released">}}, and it's a big one! The team completely redesigned the checkout page, with a slick, more intuitive layout where the complexity is hidden by default, but can be revealed by users with the click of a button. You can even go one step further with {{<newtabref href="https://bitcoinqr.dev" title="BIP21 Unified QRs">}} that allow you to completely remove the "On-chain" and "Lightning" tabs: all the user sees on checkout is how much is due and a QR Code. The user's wallet will then, upon scanning the QR, choose whether to use on-chain or Lightning (or ask the user which one to use). And on top of all that, you can now customize your store and server appearance easier than ever. No more CSS stylesheet upload. Yaï!

There are a lot more things in this update (new Greenfield API functionnalities, forms on the checkout page, etc.), which you can check out in the {{<newtabref href="https://github.com/btcpayserver/btcpayserver/releases/tag/v1.7.0" title="release notes">}}.

If you which to support BTCPay Server's mission to enable every merchant and individual to self-sovereignly receive Bitcoin, you can donate on {{<newtabref href="https://opensats.org/projects/btcpayserver" title="OpenSats">}}.

### Torq & Nolooking On Umbrel

Two new Umbrel apps caught my eyes this week: {{<newtabref href="https://stacker.news/items/97454" title="Torq">}} (by {{<newtabref href="https://ln.capital" title="lncapital">}}) and {{<newtabref href="https://nitter.lacontrevoie.fr/chaincaseapp/status/1595066603447746560" title="nolooking">}} (by {{<newtabref href="https://chaincase.app/" title="Chaincase">}}).

{{<newtabref href="https://github.com/lncapital/torq" title="Torq">}} is an open source "capital management tool for routing nodes" which allows node runners to get (and visualize) a lot of actionnable data regarding their routing activity. With this data in mind, operators can then take educated decisions on where to (re)deploy their liquidity in the network.

{{<newtabref href="https://nolooking.chaincase.app/" title="nolooking">}} (about which we talked in {{<newtabref href="../latest-strikes-8/#lightning-payjoins" title="Latest Strikes #8">}}) is a privacy and efficiency tool that helps node operators open multiple channels at once using PayJoins. In only one transaction, you can go from having funds on some external wallet to having a bunch of channels opened on your Umbrel node!

### Standard Sats Wallet Rebrands To Valet

Ilya Evdokimov {{<newtabref href="https://makers.bolt.fun/story/introducing-valet--421" title="announced">}} the rebranding of the {{<newtabref href="https://github.com/standardsats/wallet" title="Standard Sats SBW Wallet">}} to Valet.

Valet looks really much like {{<newtabref href="https://sbw.app" title="SBW">}}, with support for on-chain and both regular and {{<newtabref href="../what-are-hosted-channels/" title="hosted">}} Lightning channels, but with an additionnal twist: {{<newtabref href="https://github.com/standardsats/fiat-channels-rfc" title="fiat channels">}}. Fiat channels are basically hosted channels but with a stable balance in fiat (for example, dollars or euros). It does this by adding a dedicated "fiat rate" field to each channel, which is changed by the host every time the user sends or receive a payment, so that the balance stays flat in fiat terms, plus or minus the incoming/outgoing payment.

### Voltage Surge

Voltage {{<newtabref href="https://nitter.net/voltage_cloud/status/1595064121082486784" title="launched">}} a new monitoring tool for node runners called {{<newtabref href="https://voltage.cloud/surge/" title="Surge">}} (no, it's not the name of an Ethereum roadmap step).

Surge allows node operators to visualize their node's uptime, receive alerts, detect bad peers and issues, analyze traffic and transactions, perform static channel backups on remote servers, and so on. It's free (for now) and accessible through a waiting list.

### Indra

Speaking of Lightning nodes in the cloud, Azz from {{<newtabref href="https://valera.co/" title="Valera">}} recently {{<newtabref href="https://nitter.lacontrevoie.fr/617a7a/status/1594696672973570048" title="shared">}} what they've been working on "in the dark", and it's quite interesting to say the least.

The idea is to be able to run multiple Lightning nodes on the same server by leveraging the fact that only a few of them need to be online at the same time. You can therefore keep the nodes "shut down" while they're not used, and only bring them back online when needed. If you were to do this with a naive approach, you would need to boot up the node everytime you want to use it, getting the saved channel data of the "virtual node" into the real, actual one. And even if booting times are fast, they're not fast enough to bring a node back online at the exact moment it is needed to answer a request. Here comes Azz's innovative approach, which they compare to how a computer boots up: instead of having to boot it up, the node's state is stored in database in a format that can be pushed straight to memory, thus allowing to "revive" the node in 5 milliseconds, as Azz claims.

## Ecosystem

### Grant

Strike {{<newtabref href="https://nitter.lacontrevoie.fr/Strike/status/1595185069538349056" title="announced">}} a grant to {{<newtabref href="https://nitter.net/brian_trollz" title="Shinobi">}} for his work on Bitcoin and Lightning. Good to see Lighting company embracing fair criticism!

### Synthetic USD In LN Markets

{{<newtabref href="https://lnmarkets.com" title="LN Markets">}} released a new feature called {{<newtabref href="https://nitter.lacontrevoie.fr/LNMarkets/status/1595752739333718016" title="Synthetic USD">}}, which looks a lot like what {{<newtabref href="https://galoy.io/" title="Galoy">}} is offering with {{<newtabref href="https://stablesats.com/" title="Stablesats">}}. Basically, by holding Bitcoin and shorting its price against the US Dollar at the same time, it is possible to mimick a stable balance in dollars terms. It was hence always possible to create this kind of synthetic dollar on LN Markets by shorting Bitcoin on the platform (a possibility that wallets such as {{<newtabref href="../latest-strikes-5/#tao-wallet" title="Tao">}} exploited), but it is now easier than ever thanks to a dedicated interface and API, allowing users to swap sats for synthetic dollars, and vice-versa, without having to care about the hedging stuff (shorting), which is carried out by LN Markets.

### OpenNode Integration In Woocommerce

OpenNode is now {{<newtabref href="https://nitter.it/OpenNode/status/1594809893110050817" title="officially">}} a preferred payment processor for accepting Bitcoin in WooCommerce, thanks to OpenNode's plugin and their partership with WooCommerce.

### Buy Bitrefill Gift Cards In Zebedee

Zebedee {{<newtabref href="https://nitter.net/zebedeeio/status/1595084775038910464" title="partnered">}} with Bitrefill to enable users to buy gift cards directly from the Zebedee wallet app. This may seem a not so important news, but I personnaly find it huge: people who get their first sats through gaming (and there are more and more of them) are often confused as to how and where they can spend them. This integration will help solve this and further show that Bitcoin is for spending!

## Specs & Implems

### More On Channel Jamming

There was an update on the Channel Jamming front following Clara Shikhelman and Sergei Tikhomirov's {{<newtabref href="../latest-strikes-10/#unjamming-channels" title="proposal">}} made earlier this month. Antoine Riard {{<newtabref href="https://github.com/lightning/bolts/blob/80214c83190836c4f7699af9e8920769607f1a00/www-reputation-credentials-protocol.md" title="published">}} the first sketch of a reputation-based mechanism to prevent channel jamming. The idea is that, in order to have a payment forwarded through a routing node, the sender would need to join to the payment a certain amount of *certificates*, signed earlier by this specific routing node[^1]. If the payment goes well, the routing node will replace the sent certificates with new, freshly signed ones (and possibly a few additionnal certificates to reward the sender for their good behavior). It the payment fails, the certificates are burnt and no new certificates are signed for this payment. Certificates use blind signatures, which means that when a routing node signs a certificate, they don't know who they sign a certificate for, thus maintaning the privacy benefits of {{<newtabref href="../onion-routing/" title="Onion Routing">}}. This certificates-based mechanism hence allows routing nodes to assess of the reputation in which they hold the sender of the payment, without even having to identify the sender.

When it comes to bootstraping this new, still highly theoretical system, and issuing the first certificates, Riard proposes that they would be acquired by sending a dedicated payment to each node you want to receive certificates from.

If you are interested in the topic of channel jamming and its mitigations, make sure to {{<newtabref href="https://blog.lnmarkets.com" title="subscribe">}} to LNMarket's blog and newsletter, as I will cover this subject there in a more extensive format soon™. And if you like Latest Strikes and want to receive them by email, subscribing to this newsletter might be a good idea too 😉.

## Posts & Papers

### The Maturation Of Lightning

Roy from Breez pulished this fantastic {{<newtabref href="https://medium.com/breez-technology/the-maturation-of-lightning-growing-up-by-going-vertical-c5cffd0c98ea" title="piece">}}.

## Closing Bit

Le tonnerre frappe et tonne deux fois:\
Quand il s'abat,\
Et dans la ferveur de la voix\
De l'homme qui relate son fracas.

---

If you enjoyed this recap, you can show your appreciation by throwing a few coins to *fanis @ lnmarkets.com*, by scanning or clicking the QR code.

Thank you!

{{<figure align=center src="../../images/lnm_lnurl.png" link="lightning:fanis@lnmarkets.com">}}

[^1]: The number of certificates required by a node to route a certain amount of sats with a certain expiry period can be set by each node, at any time, and is gossiped through the network, much like regular payment fees.
---
title: "Latest Strikes 30"
date: 2023-04-07T18:15:00+02:00
block: "784368"
cover:
    image: "../images/IntroductionPoint.jpg"
    alt: "The drawing of a futuristic space ship at the crossing of multiple star paths."
    caption: "\"Introduction Point\". Generated with Stable Diffusion."
    relative: "false"
tags: ["bitcoin", "lightning"]
categories: ["strikes"]
draft: false
---

Friday it is! Never was a Latest Strikes issue published this late in the week, but here we are at last! With the release of a new major LND version, an innovative way of connecting nostr and Lightning, and Route Blinding finally making it into the specification, last week was another banger!

## Ecosystem

### Wavlake Makeover

Back in January this year we {{<newtabref href="https://fanismichalakis.fr/posts/latest-strikes-20/#wavlake-relaunch" title="covered">}} the relaunch of {{<newtabref href="https://www.wavlake.com/" title="Wavlake">}}, a Lightning-native music streaming platform based on the {{<newtabref href="https://dergigi.com/2021/12/30/the-freedom-of-value/" title="Value4Value">}} model. You can listen to the music uploaded by artists for free and, if you like what you hear, you can send back value to the creator in the form of sats. On top of that, each album is its own RSS feed, freely retrievable by any one, including other clients than Wavlake (for example, it is totally possible to import an album into a podcast player, since podcasts use RSS feeds too) ; and the RSS feed not only contains endpoints to retrieve the music files, but also all the information you need to send payments to the artist.

One of the "critiques" I formulated back then was that I found it annoying as a user to be forced to create an account and deposit funds in Wavlake in order to be able to tip artists. This is now a thing of the past, since last week's Wavlake release completely {{<newtabref href="https://iris.to/note1y7hyauslc25ufvkspk98ejh2qg39ha7hqs9tl7qn83vwkxy6kkvq7q0mf5" title="removed">}} this obligation. You can now boost tracks and tip artists without an account!

On top of that, the team also released a nice new feature called "Wavlake Radio". A bit like Spotify Radio, this creates a playlist of tracks, very useful if you want to discover new things.

### Zebedee

Lightning-infrastructure and wallet provider Zebedee partnered with Bipa and Pouch, operating respectively in Brazil and the Philippines, to enable Zebedee users to cash out in their local currencies. This partnership, a bit like the {{<newtabref href="https://fanismichalakis.fr/posts/latest-strikes-14/#strike-x-bitnob" title="one">}} between Bitnob and Strike back in December last year, highlights how impactful Lightning can be to move value around. As Pouch's founder and CEO Ethan Rose {{<newtabref href="https://nitter.lacontrevoie.fr/Pouch_PH/status/1640725904556011521" title="highlighted">}}, the level of native interoperability provided by the Lightning Network and LNURL protocols allows companies to interact without even having to specifically think about it. This enables some entities to specialize in worldwide Lightning infrastructure, while others can focus on local development and adoption.

### Lightning Cash

Hynek Jína created {{<newtabref href="https://stacker.news/items/157596/r/FanisMichalakis" title="Lotes">}}, physical Lightning cash than can be passed around just like bills and coins. It works a bit like the {{<newtabref href="https://www.boltcard.org/" title="BoltCard">}} in the sense that it works by writing a LNURL-Withdraw link to an NFC card or tag. The big difference lies in the projected usage: while the BoltCard's link is meant to be used by a merchant when I pay using the card, here the idea is that I'd transfer the bitcoins by handing out the card.

However, this doesn't come without tradeoffs: when you hand the card to someone as payment, they either trust that the required amount is deposited onto it, or check the amount by scanning the card with the Lotes {{<newtabref href="https://github.com/hynek-jina/lotes" title="app">}}. As the whole point of Lotes is to be able to move sats without touching a phone, this means that the expected behavior is to trust the person giving you a Lote, and maybe only check it later when you're at home. While I get the intention - the lack of physicality of Bitcoin/Lightning is one of the most mentioned turnoff for newbies - I can't help but to think that using this kind of systems at scale would lead to a lot of abuse. But still, an interesting idea to play with.

## Wallets & Tools

### Bolt12 Offers In Clams

{{<newtabref href="https://bolt12.org/" title="Bolt12">}} Offers are {{<newtabref href="https://nitter.lacontrevoie.fr/clamstech/status/1640810071725842432" title="available">}} in Clams! Clams is a web interface to interact with your Core Lightning node, using the {{<newtabref href="https://docs.corelightning.org/docs/commando" title="commando">}} plugin to issue commands to the node *via* the Lightning Network itself. Users can now pay Bolt12 offers or create their own to receive payments, all that with ease thanks to Clams intuitive user interface.

### Mempool's Lightning Explorer Now Open Source

The {{<newtabref href="https://github.com/mempool/mempool" title="Mempool">}} open source project {{<newtabref href="https://nitter.lacontrevoie.fr/mempool/status/1640715797097246723" title="released">}} a new version with all the latest features available on the mempool.space website, including Lightning-related ones. You can now display Mempool's Lightning {{<newtabref href="https://mempool.space/lightning" title="explorer">}}, as well as additional Lightning-related context on on-chain transactions (channel open and close) on your own instance.

A few days ago, Umbrel {{<newtabref href="https://nitter.lacontrevoie.fr/umbrel/status/1643639183142187009" title="ported">}} this update to their app store.

### Zeus 0.7.4

The Zeus team {{<newtabref href="https://github.com/ZeusLN/zeus/releases/tag/v0.7.4" title="released">}} a new version of the wallet, with a ton of bug fixes and improvements, new themes, fee {{<newtabref href="https://github.com/ZeusLN/zeus/pull/1368" title="bumping">}} (for regular on-chain transactions, but also to speed up channel opens and closes) and filtering in the channels and transactions display (for example to hide unpaid invoices).

### Bitcoin Beach Wallet Renames to Blink

The Bitcoin Beach Wallet {{<newtabref href="https://nitter.lacontrevoie.fr/blinkbtc/status/1642220765926834179" title="got">}} new features and a new name last week! "Bitcoin Beach Wallet" is long, while searching its acronym BBW on Google leads to interesting results, so changing the name totally makes sense. The team listed three reasons behind the new name on the announcement Twitter thread, but one that I like even more is "don't blink or you'll miss it", as Lightning payments settle at the speed of light.

New features include new languages and more than 30 display currencies (which was trickier than it sounds to achieve, since some currencies are lacking a consensual exchange rate, or in some cases the official exchange rate and the one available to people in practice are completely different).

### Nostr Wallet Connect

Alby and Amethyst just changed the Zap game, forever!

One of the cumbersome parts of zapping on mobile is that you need to leave the nostr app in order to open the wallet app and send the payment (unless a wallet is integrated into the nostr app, but this comes with different tradeoffs). What if you could instead connect your nostr app to an external Lightning wallet, and trigger payments directly from the nostr app?

This is what {{<newtabref href="https://github.com/getAlby/nips/blob/master/47.md" title="Nostr Wallet Connect">}} does. During an easy one-time setup, you create an authenticated link between your Lightning wallet and your nostr app, through a "Nostr Wallet Connect Service" . Then, every time you hit the "zap" button, the nostr app will send an ephemeral nostr note containing the corresponding invoice to the NWC Service, which will ask your Lightning wallet/node to pay and return the preimage to the nostr app in a different note once the payment is done.

All you need for this to work is:
- a NWC Service, e.g. an always-on nostr client, connected to
- an always-on Lightning wallet (either your own Lightning node, or a custodial solution) ;
- for the nostr app and the NWC Service to share at least one relay, so that they can receive each other's notes.

Wanna see it in action? See this blog {{<newtabref href="https://blog.getalby.com/native-zapping-in-amethyst/" title="post">}} by Alby, and connect your Amethyst app to Alby's NWC service at nwc.getalby.com. All you need to do is to link whatever Alby account you use (either custodial or non-custodial) to the service, scan a QR Code with your phone and open the link with Amethyst (which should be automatic thanks to the `nostrwalletconnect://` prefix).

I really believe this is quite a game changer in the synergies between nostr and Lightning, not only for zaps, but also for a wide range of use cases. Let's keep an eye on this 👀

## Spec & Implems

### LND v0.16.0 Released

Lightning Labs {{<newtabref href="https://lightning.engineering/posts/2023-03-29-lnd-0.16-launch/" title="released">}} the version 0.16 of LND! This major release - the first of the year - notably includes a revamped pathfinding logic, updates to watchtowers, and multiple enhancements to a variety of existing RPCs.

The pathfinding enhancements include the alternative bimodal estimator we already {{<newtabref href="https://fanismichalakis.fr/posts/latest-strikes25/#better-payment-flow-model-in-lnd" title="mentioned">}} in February, as well as the addition of a `capacity factor` in the computation of the probability of success in the existing `a priori` estimator. This factor is comprised between 1 and 0.5 and starts declining sharply when the ratio between the amount of the payment and the channel's capacity reaches a certain threshold called the `Capacity Fraction`. By default, the `Capacity Fraction` is set to the quite conservative value of 99.99%, which means that while the amount of your payment is below 99.99% of the channel's capacity, the `capacity factor` will not have a huge effect on the estimated probability of success (but still have some effect[^1]). If you want to give more influence to this parameter, you can lower the default value down to a minimum of 75% (e.g. the capacity factor, and hence the estimated probability of success, declines sharply when the amount is around 75% or more of the channel capacity).

On the watchtowers front, this new release brings significant improvements, such as "disk space savings of up to 93% in simulations and early-tester reports", less memory usage, better performance, as well as the ability to add and remove watchtowers without having to restart LND.

### Route Blinding Baby

After 3 years of hard work, route blinding has been {{<newtabref href="https://nitter.lacontrevoie.fr/realtbast/status/1640606307924291585" title="merged">}} into the Lightning Network specification! We've talked in details about route blinding in previous issues of Latest Strikes, and this paves the way for it being "interoperably" implemented across various implementations. Lightning Privacy isn't so great yet, especially for the receiver, but we're getting there!

If you're new here, route blinding is a way of hiding the final destination of a payment from the sender: instead of the sender computing the whole route between them and their recipient, both ends compute half of the route. This way, the sender only knows that there exists a route between the last node of the half it computed (called the *introduction point*) and the recipient. This route could even be comprised of unannounced channels the sender doesn't know about. Done right, this greatly enhances the privacy of the receiver.

## Closing Bit

A la croisée de toutes ces routes\
L'homme hésite.\
Une femme est assise là et le regarde\
Tranquille.

Il comprend, se départit de son fardeau\
Et le dépose à ses pieds.\
Elle sourit.

---

Want to receive Latest Strikes straight to your inbox every week? Couldn't be easier: subscribe to {{<newtabref href="https://blog.lnmarkets.com" title="LN Markets Ghost blog">}} and you're all set (remember to confirm your subscription by clicking the link sent via email).

---

If you enjoyed this recap, you can show your appreciation by throwing a few coins to *fanis @ lnmarkets.com*, by scanning or clicking the QR code.

Thank you!

{{<figure align=center src="../../images/lnm_lnurl.png" link="lightning:fanis@lnmarkets.com">}}

[^1]: As you can see on the {{<newtabref href="https://lightning.engineering/static/d868fae86841bdf71e0b1f2e825b1951/d61c2/capacity_factor.png" title="graph">}} in Lightning Labs' post, the effect kicks in when the value of the amount-to-capacity ratio is a bit below the `capacity fraction`. For example, even with a `capacity fraction` value of 99.99%, the `capacity factor` starts to fall when the ratio is around 90%.
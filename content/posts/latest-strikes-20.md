---
title: "Latest Strikes 20"
date: 2023-01-25T20:00:00+01:00
block: "773585"
cover:
    image: "../images/DragonAlleyStream.min.png"
    alt: "An impressionist and fantasmagoric representation of Harry Potter's Dragon Alley."
    caption: "\"Dragon Alley Stream\". Generated with DALL·E."
    relative: "false"
tags: ["bitcoin", "lightning"]
categories: ["strikes"]
draft: false
---

Last week was big - again. From Breez releasing its SDK to Wavlake launching a revamped Lightning-powered music streaming platform, there was no time left to get bored! Jump in the stream with us to see what you might have missed!

## Ecosystem

### Channel Ninja

There's a new channel recommendation tool in town, called {{<newtabref href="https://channel.ninja" title="channel.ninja">}}: give it your node's public key, and it will show you good nodes to connect to in exchange for 1,000 sats.

After taking a quick glimpse through the {{<newtabref href="https://github.com/channelninja/channel.ninja/blob/main/server/src/graph/graph.service.ts#L118" title="code">}}, it seems that the recommendation algorithm is still quite simple at the moment, and mostly uses the distance between your node and others (in terms of number of hops) as well as availability (channel updates frequency) to suggest nodes to connect to. This still gives a good first answer to the sempiternal question "which nodes should I connect to?", and I have no doubt the suggestion engine will be improved upon in further updates.

What's cool is that the website already supports {{<newtabref href="https://nitter.net/channel_ninja21/status/1616103743233359872" title="webln">}} to pass your node's public key from a browser extension (such as {{<newtabref href="https://getalby.com" title="Alby">}}) to the website without having to manually copy/paste it. As Bumi {{<newtabref href="https://nitter.lacontrevoie.fr/Bumi/status/1616129141648113671" title="notes">}}, webln support paves the way for even bigger UX improvements, such as being able to open new channels, based on recommendations from channel.ninja, simply by clicking an "Open Channel" button displayed in front of the suggestion.

### Minecraft Meets Lightning

Bitcoin just {{<newtabref href="https://nitter.net/PlaySatlantis/status/1616539590130798592" title="landed">}} in Minecraft! You can build you citadel and mine real sats, alone or with your friends, in Satlantis Minecraft server. The prize pool is sponsored by The Bitcoin Company, which has its own virtual store front in the game. Pretty cool, and kinda Second Lifey vibes with the potential for a real in-game economy thanks to Bitcoin and Lightning.

### New Games In Zebedee

Viker {{<newtabref href="https://nitter.net/zebedeeio/status/1616435601464791043" title="published">}} two new mobile games with Lightning rewards powered by Zebedee: a chess game and a scratch game. I've always been bullish on Lightning Gaming, both in terms of adoption (mobile gaming is huge) and stress testing (generates a huge load of microtransactions, sometimes literally thousands in a short time window), so it's cool to see two new games join Viker's stall.

Speaking of Lightning Gaming, seems like there's something {{<newtabref href="https://nitter.lacontrevoie.fr/THNDRGAMES/status/1617907580193456128" title="brewing">}} at THNDR GAMES 👀

### Full Lightning Experience On CashApp

Cash App {{<newtabref href="https://nitter.lacontrevoie.fr/CashApp/status/1616163862293917696" title="announced">}} last week that the "full Lightning experience" is now available on the app, which means Cash App users are now able to send to and receive from any other Lightning wallet, for free (presumably Cash App eats the routing fees for their users). I'm not entirely sure as to what was missing to call it the "full experience" when they rolled out Lighting receive support back in {{<newtabref href="../latest-strikes-8/#cashapp" title="October">}} last year, but still awesome to see!

### Lots Of Cool Domains For Your Lightning Address(es)

Always looking for a new cool Lightning Address to add to your list? Yves (probably) got you {{<newtabref href="https://nitter.net/ZLOK/status/1615717558304268292" title="covered">}}! On {{<newtabref href="https://lnsat.me/" title="LNsat.me">}} you can pick across almost 20 different domains (some of them political, other more memeical, but always sending a message), choose your username, and directly connect your new Address to your node.

Also a friendly reminder that, no, Lightning Address doesn't necessarily means custodial.

### Goodbye LNTXBOT

Speaking of custodial, seems like it's time to say {{<newtabref href="https://nitter.net/LightningTipB0t/status/1615084272691413012" title="goodbye">}} to LNTXBOT. The famous Telegram-based Lightning wallet has shut down operations, quite unexpectedly, with users having to {{<newtabref href="https://nitter.lacontrevoie.fr/jokoono/status/1615312431697506304" title="queue up">}} to get their sats back. Farewell good ol' bot, you'll be remembered.

Also a friendly[^1] reminder that in Lightning too, not your keys, not your coins.

### Wavlake Relaunch

Wavlake - the coolest online music player - {{<newtabref href="https://nitter.net/wavlake/status/1615428578413510657" title="relaunched">}} with a brand new interface and new mechanisms.

Previously, the platform relied on crodwsourced paywall to compensate artists: in order to play a song it needed to have at least one charge, and charges could be bought for a few sats. If you really liked a track and felt like the world needed to hear it, you could therefore buy many charges at once, allowing others to enjoy the music for free for a while.

Now, the remuneration model has turned into something closer to what currently exists in Podcasting 2.0: you can listen for free and, if you enjoy the music send some sats to the artist with a "Boost", along with a message if you so desire.

The new interface is very clean, and it is very cool (and principled) that users are able to listen to songs for free, but I must say I liked the old model too: buying charges for a song you liked so that others could experience it was fun and totally made sense. On a different note, what was really nice is that sending sats didn't require registration - just send them straight from your wallet - whereas now you need to create an account (no LNURL login) and fund it to be able to boost songs, which feels a bit like a regression.

Anyway, you can still listen to the tracks without an account, and you should: there are some real bangers out there!

### Bounties

I caught two Lightning-related bounties last week:
- Coinkite is {{<newtabref href="https://stacker.news/items/123317" title="offering">}} a 10 million sats bounty to implement SATSCARD support in Breez, which would allow sweeping the funds from the NFC card to the Breez balance,
- Francis Pouliot puts forth a 2 million sats {{<newtabref href="https://nitter.lacontrevoie.fr/francispouliot_/status/1617255454614118408" title="bounty">}} for adding LNURL-Pay and Lightning Addresses to the LNURL component of Cyphernode.

## Wallets & Tools

### LNBits Week

Last week was big for LNBits. The project got:
- a new {{<newtabref href="https://github.com/lnbits/lnbits/wiki" title="documentation">}} in the form of a GitHub wiki, thanks to {{<newtabref href="https://stacker.news/items/124858" title="Darthcoin and PlebTag">}},
- a v2 for the Boltz extension, allowing users to create recurring swaps where the Lightning balance is swapped to on-chain when a thresold is reached (as Calle {{<newtabref href="https://nitter.net/callebtc/status/1616008588975112193" title="points out">}} this comes very handy for a merchant who wants to empty the drawer after a day of hard work),
- an {{<newtabref href="https://nitter.net/arcbtc/status/1615763409097588758" title="update">}} to the Dragon Alley Protocol for resilient markertplaces to take advantage of nostr. This update in the protocol outline will then be integrated into the {{<newtabref href="../latest-strikes-18/#lnbits-new-market-extension" title="Market extension">}} (maybe we'll have more to say about this next week?).

### Breez SDK & Partnership

Last week was also huge for Breez, with the publication of the {{<newtabref href="https://nitter.lacontrevoie.fr/Breez_Tech/status/1617183343560335360" title="Breez SDK">}} and a new partnership with BoltObserver.

The {{<newtabref href="https://github.com/breez/breez-sdk" title="Breez SDK">}} aims to facilitate the integration of Bitcoin and Lightning payments by developers into their apps. Instead of having to reinvent the wheel, developers can now use the SDK to quickly and easily leverage the power of Lightning! The SDK comes in two parts:
- Blockstream's Greenlight API to handle the classical Bitcoin and Lightning stuff (talk with other nodes, perform transactions, etc.),
- Breez Server, which handles what we could call the "business logic" and runs the Lightning Service Provider (LSP, for example to provide users with channels and inbound liquidity), fiat currencies management (mostly to be able to display balance in local currencies) and notifications (to tell users when they receive money, for example).

On a different note, Breez also {{<newtabref href="https://nitter.lacontrevoie.fr/Breez_Tech/status/1615719849094774785" title="officialized">}} their partnership with {{<newtabref href="https://bolt.observer" title="bolt.observer">}}. bolt.observer provides ready to use tools to monitor your node's channels and liquidity allocation so that you don't have to build your own, with data vizualisation and custom alerting and notification (for example, receive a message in Slack when a channel's outbound liquidity drops below a certain threshold). Just like the Breez SDK helps developers integrate Lightning without recreating everything from scratch, Breez decided to let bolt.observer do what they do best (and better than anyone else), and focused on helping them create a service that would be useful for them when bolt.observer was developing their {{<newtabref href="../latest-strikes-11/#liquidops" title="LiquidOps">}} tools. Win-win!

### Releases (BTCPay & Blixt)

Last week, the version {{<newtabref href="https://github.com/btcpayserver/btcpayserver/releases/tag/v1.7.4" title="1.7.4">}} of BTCPay Server was released, as well as the version {{<newtabref href="https://github.com/hsjoberg/blixt-wallet/releases/tag/v0.6.3" title="0.6.3">}} of Blixt Wallet.

Both updates mostly ship bug fixes and improvements, with notably a fix in Blixt of the previous fix of LND's too aggressive channel pruning that we covered in {{<newtabref href="../latest-strikes-19/#blixt-update" title="Latest Strikes 19">}}.

## Specs & Implems

### Negative Fees Anyone?

Researchers have found a fast algorithm to find shortest paths in a graph where segments can have negative weights. This could prove pretty useful for {{<newtabref href="https://nitter.net/niftynei/status/1616110454396391424" title="Lightning">}} and payment routing, if we were to have negative fees 👀

### LN Spec Meeting

Lucas Ferreira published this awesome {{<newtabref href="https://nitter.lacontrevoie.fr/lucasdcf/status/1615413064148328448" title="recap">}} of last week's Lightning Spec Meeting.

## Closing Bit

Je crois te voir dans chaque visage\
Chaque paire de baskets blanches\
Dans l'odeur de thé qui traine au coin d'une rue...\
Là ! Froissement d'étoffe : c'est bien toi.

---

Want to receive Latest Strikes straight to your inbox every week? Couldn't be easier: subscribe to {{<newtabref href="https://blog.lnmarkets.com" title="LN Markets Ghost blog">}} and you're all set (remember to confirm your subscription by clicking the link sent via email).

---

If you enjoyed this recap, you can show your appreciation by throwing a few coins to *fanis @ lnmarkets.com*, by scanning or clicking the QR code.

Thank you!

{{<figure align=center src="../../images/lnm_lnurl.png" link="lightning:fanis@lnmarkets.com">}}

[^1]: Provided you didn't have too many sats on there, otherwise the "friendly" aspect might be a bit lost on you. But it still is a reminder, right? So you know what to do next.
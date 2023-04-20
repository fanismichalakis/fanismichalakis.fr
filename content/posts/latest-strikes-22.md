---
title: "Latest Strikes 22"
date: 2023-02-06T18:25:00+01:00
block: "775320"
cover:
    image: "../images/merlin.png"
    alt: "A mysterious wizard standing in a forest, seen from behind."
    caption: "\"Merlin's blows are strokes of fate.\" Generated with Midjourney by Koty Auditaure (https://koty.uwu.ai/)."
    relative: "false"
tags: ["bitcoin", "lightning"]
categories: ["strikes"]
draft: false
---

"Greeting, Lightning wanderer! I hear you're interested in discovering the latest developments in the mighty kingdgom of Lightning? Follow me, my young friend, as we descend into the valley."

You're a bit baffled by what just happened, but still decide to follow the strange man. "Do not worry, he tells you, looking over his shoulder. Last week was quite quiet, this will not be a long walk."

## Ecosystem

### THNDR GAMES Launches Leagues

THNDR GAMES {{<newtabref href="https://nitter.lacontrevoie.fr/dickerson_des/status/1621196042405306369" title="launched">}} a new feature called "Leagues" in their Solitaire game. Several times a day, you can compete (asynchronously) with other players in the same league as you. There are three 8 hours long rounds per day, and during each round you can play up to 3 games that will qualify for your league score. At the end of the day, depending on your ranking, you will either climb up to the next league, go down to the previous one or stay in the same.

### Moar Merchants

Remember Pick n Pay? This major South African retailer {{<newtabref href="https://fanismichalakis.fr/posts/latest-strikes-9/#a-major-south-african-retailer-accepts-bitcoin-via-lightning" title="made the news">}} in November last week when they started to accept Lightning payments in some of their stores. CryptoConverted, the company powering the stores system to accept such payments, just {{<newtabref href="https://nitter.net/CryptoConverted/status/1620745811582939136" title="announced">}} that you can now pay with Lightning in all PnP South African stores!

### 10101's Roodmap

10101 (it reads Ten-Ten-One), formerly known as Itchy Sats, just published their {{<newtabref href="https://10101.substack.com/p/10101-roadmap" title="roadmap">}} for their vision of self-custodial trading with {{<newtabref href="https://fanismichalakis.fr/posts/latest-strikes-13/#dlcs-on-lightning-on-mainnet" title="Lightning DLCs">}}. Itchy Sats already paved the way for self-custodial trading on-chain with DLCs, allowing users to engage in {{<newtabref href="https://en.wikipedia.org/wiki/Contract_for_difference" title="CFD">}} contracts without counterparty risk, a complete game-changer! No wonder they're now aiming at bringing those contracts to Lightning, which allows for instant settlement and facilitates contract renewing (essential for things such as {{<newtabref href="https://en.wikipedia.org/wiki/Perpetual_futures" title="perpetual futures">}}). Such contracts also enable the creation of synthetic fiat-denominated balances inside Lightning channels, which will be the first use case explored by the team.

### More Lightning x Nostr

Last week I couldn't refrain from talking about Lightning and Nostr synergies, and I don't really see why I should this week! On the Nostr front, Lightning news this week include:
- the opening of the {{<newtabref href="https://github.com/nostr-protocol/nips/pull/224" title="merge request">}} for Zaps, a new nostr note type representing paid Lightning invoices receipts (we already briefly talked about it {{<newtabref href="https://fanismichalakis.fr/posts/latest-strikes-21/#lightning--nostr" title="last week">}}). This spec proposition goes into more details around the specific flow of payments with Zaps:
    1. Sender gets the LNURL endpoint of the user they want to send money to from their nostr profile,
    2. Sender calls this endpoint, checks if it supports Zaps, and if so asks the endpoint to generate a Zap invoice by sending it a Zap request, which contains all the needed info to identify the user and/or the post for which money is sent. The endpoint asks the receiver's Lightning node to generate the invoice.
    3. The sender pays the Zap invoice once it receives it from the endpoint. Then, the receiving Lightning node creates, signs and sends a Zap note, which indicates that the invoice has been paid.
There are still on-going discussions around this new NIP (Nostr Improvements Proposals), dealing with questions such as whether to use LNURL at all, or use a new, dedicated endpoint.
- as nostr gains traction, so does spam on the network (real spam, I'm not talking about perfectly valid Bitcoin transactions that pay their share of fees). To address this (rapidly) growing issue, one of the explored mitigations is *paid relays*. The idea is quite simple: a nostr user will pay an upfront fee to be authorized by a specific relay to read and write data from it. If a user connects only to paid relays, they effectively only see content posted by paid users. Additionally, they can connect in write-only mode to "free" relays, so that the notes they publish can reach non-paying users. The latest {{<newtabref href="https://github.com/Cameri/nostream/releases/tag/v1.19.0" title="version">}} of Nostream, one of the most prominent nostr relay implementations, now allows relay runners to configure this admission fee on their instance. The relay must be connected to a payment processor to be able to generate invoices and track payments, which is an area where {{<newtabref href="https://andreneves.xyz/p/the-rise-of-paid-nostr-relays" title="Zebedee can help">}} if you're looking into setting up your own paid relay but don't want to go into running your own BTCPay Server or equivalent.

## Wallets & Tools

### Zeus

Zeus v0.7.2 is {{<newtabref href="https://github.com/ZeusLN/zeus/releases/tag/v0.7.2" title="out">}}! It notably includes a Point of Sale mode for Square devices (we saw it in action {{<newtabref href="https://fanismichalakis.fr/posts/latest-strikes-21/#more-lightning-payments-in-brick-and-mortar-businesses" title="last week">}}) and support for receiving payments via NFC (sending was already possible). This last bit means that anyone can now pay you simply by tapping their Boltcard (or equivalent) on your phone. Neat!

### Breez

Breez is rolling out a new {{<newtabref href="https://nitter.lacontrevoie.fr/Breez_Tech/status/1622226364408504327" title="update">}} with Tor support (Android-only) and neutrino sync over HTTP. From what I understand (and I'd like to thank my friend {{<newtabref href="https://nitter.net/JohnOnChain" title="John">}}) for guiding me here), it probably means that there is a shared HTTP cache somewhere and that Breez applications syncing using neutrino will be able to get some of the block headers directly from the cache, instead of having to ask Breez's Neutrino server every time.

Note that this new version is still labelled as pre-release on {{<newtabref href="https://github.com/breez/breezmobile/releases/tag/0.15.httpsync" title="GitHub">}}.

### Umbrel

Umbrel {{<newtabref href="https://nitter.lacontrevoie.fr/umbrel/status/1620459292565598208" title="released">}} a long awaited feature for the LND app: the ability for users to access some advanced parameters from the graphical user interface, instead of having to manually modify a configuration file and restart LND. Users can now easily change things such as their node's alias or colour, enable so-called *wumbo* channels (capacity greater than 0.16 BTC), configure channel acceptors, tweak their routing strategies, add watchtowers, and much more!

It's very cool to see this amount of customizability in the hands of end-users. One note though, and I think it explains why the Umbrel team waited so long before releasing this feature: be careful with what you're doing, and don't change a settings if you don't know what it does!

### BTCPay Vulnerability Disclosed And Patched

BTCPay Server went back on a serious {{<newtabref href="https://blog.btcpayserver.org/btcpay-server-cve-2022-32984/" title="vulnerability">}} that was responsibly disclosed by Antoine Riard in May 2022, and patched the same day in version 1.5.4 of the software. This vulnerability affects BTCPay Server versions 1.3.0 to v1.5.3, and allows a remote attacker to access sensitive information (such as xpub and Lightning credentials) from the web page of any publicly exposed Point of Sale app. The information could be obtained simply by looking at the web page HTML source, which is accessible from any regular browser.

If you're running one of the affected versions of BTCPay Server and exposing Point of Sale apps, it is highly recommended to upgrade immediately to at least v1.5.4.

## Specs & Implems

### LN Spec Meeting Recap

It's probably going to be a recurrent part of Latest Strikes: Lucas Ferreira wrote again a very nice and clear {{<newtabref href="https://nitter.net/lucasdcf/status/1620810765853954048" title="digest">}} of last week's LN Specification meeting[^1]. I'll let you read it yourself because it is already amazingly concise, but the main item I take out from this thread is {{<newtabref href="https://github.com/lightning/bolts/blob/6e3b97c5454b759053f611a3797320004fecd21c/proposals/route-blinding.md" title="route blinding">}} implementations in Core Lightning and Éclair being finally interoperable, although interoperability is still to be fully tested.

## Closing Bit

"Un nouveau peuple est arrivé\
Qui érige partout des statues\
Et nos belles vallées\
Autrefois si bien tenues\
S'en trouvent bien défigurées."

Je regarde l'homme d'un oeil mauvais\
Le tonnerre est dans mes lèvres:

"Qui es-tu, toi, pour appeler ces vallées tiennes ?\
Les terrasses que tu ériges sont utiles à ton agriculture\
Alors tu en quadrilles la terre. Vaurien !

Ce nouveau peuple n'a cure de tes cultures - il a la sienne\
Et dans mille ans encore on en verra l'étain."

---

Want to receive Latest Strikes straight to your inbox every week? Couldn't be easier: subscribe to {{<newtabref href="https://blog.lnmarkets.com" title="LN Markets Ghost blog">}} and you're all set (remember to confirm your subscription by clicking the link sent via email).

---

If you enjoyed this recap, you can show your appreciation by throwing a few coins to *fanis @ lnmarkets.com*, by scanning or clicking the QR code.

Thank you!

{{<figure align=center src="../../images/lnm_lnurl.png" link="lightning:fanis@lnmarkets.com">}}

[^1]: LN Spec Meeting are public meetings between developers of all the Lightning Network implementations, held over an IRC chat and a Jitsi conference call. They aim at syncing the different teams' progress and priorities, as well as discussing modifications or additions to the common Lightning specification.

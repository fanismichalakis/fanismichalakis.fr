---
title: "Latest Strikes 7 - Oct 23rd"
date: 2022-10-23T21:30:00+02:00
block: "760007"
cover:
    image: "../images/DALL·E 2022-10-23.png"
    alt: "Realist painting of a greek agora, crowded, with people pointing their fingers toward a guilty man, digital art"
    caption: "'Realist painting of a greek agora, crowded, with people pointing their fingers toward a guilty man, digital art' Generated with DALL·E."
    relative: "false"
tags: ["bitcoin", "lightning"]
categories: ["strikes"]
draft: false
---

## Ecosystem

### Developer Grants

This week we saw two new grants going to Lightning builders!
- {{<newtabref href="https://www.superlunar.com/" title="Superlunar">}} issued a {{<newtabref href="https://nitter.net/dusty_daemon/status/1582426374979358721" title="grant">}} to {{<newtabref href="https://nitter.net/dusty_daemon" title="Dusty Daemin">}} to support his work on Lightning, and notably splicing.
- {{<newtabref href="https://okcoin.com" title="Okcoin">}} is now {{<newtabref href="https://nitter.net/Okcoin/status/1582174627085910016" title="sponsoring">}} Johns Beharry's work of promoting Lightning projects and experiments through {{<newtabref href="https://bolt.fun/" title="BoltFun">}}.


### Legends Of Lightning Update

Speaking of BoltFun, I thought it would be interesting to see how the {{<newtabref href="https://makers.bolt.fun/tournaments/1/overview" title="LegendsOfLightning tournament">}} has evolved since we last took a look. There are now 25 different {{<newtabref href="https://makers.bolt.fun/tournaments/1/projects" title="projects">}} competing, and each of them is sharing their story along the way! Go take a look!

### TabConf 2022

Seems like TabConf was lit! 🔥

{{<tweet user="roasbeef" id="1582162098754187265">}}

André Neves gave the {{<newtabref href="https://nitter.net/andreneves/status/1583078776178503680" title="keynote">}}, detailing how Bitcoin can thrive through developer education, mainstream adoption and open source software, and what they're doing at Zebedee and NBD.

There was also a cool {{<newtabref href="https://nitter.net/theinstagibbs/status/1581444240847949824" title="presentation">}} on where we're at with Eltoo.

## Wallet & Tools

### Echo

Zeus {{<newtabref href="https://nitter.net/ZeusLN/status/1582353192066908160" title="released">}} {{<newtabref href="https://echoln.com/" title="Echo">}}, a Podcasting2.0 web player leveraging Lightning Lab's Lightning Node Connect to enable you to stream sats to your favorite podcasters while listening to their shows.

### Impervious Browser Is Live

Impervious Browser is {{<newtabref href="https://nitter.net/ImperviousAi/status/1582806296255864832" title="live">}}! The browser features encrypted messaging, peer-to-peer group video calls, collaboration features and native support for Lightning.

### And Keet Now Supports Lightning

You can {{<newtabref href="https://nitter.net/keet_io/status/1584198778747162625" title="now">}} send and receive sats in a Keet Meeting. In the settings, you can now configure your wallet by connecting to an existing node backend (either LND, Eclair or Core Lightning). Once it's done, you'll be able to transfer value P2P with other people in meetings.

### Alby 🤝 Nostr

It was a bit teased in {{<newtabref href="../latest-strikes-5/#alby-release-and-nostr-soon" title="Latest Strikes #5">}}, but here it is: {{<newtabref href="https://blog.getalby.com/nostr-in-the-alby-extension/" title="Nostr integration in Alby">}}. Users can easily generate new keys from the extension, and said keys are then managed by the extension itself. It will allow users to sign messages on web Nostr clients with the click of a button (no more copy-pasting of private keys!).

### Centrality in BoltObserver

BoltObserver {{<newtabref href="https://nitter.net/BoltObserver/status/1583487524550459396" title="added">}} 3 centrality measures to their {{<newtabref href="https://bolt.observer/explorer/" title="explorer">}}: betweeness, closeness and eigenvector centrality.

{{<newtabref href="https://en.wikipedia.org/wiki/Betweenness_centrality" title="Betweeness">}} and {{<newtabref href="https://en.wikipedia.org/wiki/Closeness_centrality" title="closeness">}} centralities are both based on the analysis of shortest paths between two nodes on a graph. The betweeness centrality of a given node takes all the shortests paths that exist between all nodes in the network and count those where the studied node is on the path. The closeness centrality of a node is the multiplicative inverse of the sum of the lengths of the shortest paths between this node and and all other nodes.

On the other hand, {{<newtabref href="https://en.wikipedia.org/wiki/Eigenvector_centrality" title="eigenvector">}} centrality is a measure of how powerful your direct neighborhood is: your own score is proportionnal to the sum of all the scores of your neighbours (eg, of the peers you share a channel with).

### Bitcoin Ring

After NFC cards, it didn't took long for us to be blessed with the first Lightning-enabled {{<newtabref href="https://nitter.net/bitcoin_ring/status/1581966568631988224" title="ring">}}! It works basically just like the cards, but the NFC tag is hidden inside the ring. Very useful (and beautiful) for when you leave home without a phone or wallet (as the latter increasingly tend to be included in the former).

Regarding security, while it is easier to protect a NFC card (simply by keeping it in a NFC/RFID blocking card holder), one could imagine an equally secure ring where you have to actively press a small button on the ring to close the electrical circuit and allow the NFC tag to be read from.

## Spec & Implems

### Error Attribution Upon Payment Failure

Joost Jager sent a {{<newtabref href="https://lists.linuxfoundation.org/pipermail/lightning-dev/2022-October/003723.html" title="proposition">}} in the Lightning-Dev mailing list aiming to improve how nodes can pinpoint where a payment failure comes from on the route.

Currently, when a payment fails, the hop where it fails is responsible for writing the appropriate error message and propagate it (from hop to hop) back to the sender. The issue is that the error source (the hop where the failure happened) could simply write random data, and the sender would have no way of telling either what the error was, or who wrote the random data. Indeed, in the current form, only the error source commits to the error message via an HMAC, which means that any node on the route can replace the error message with any gibber they want.

Unable to determine where the error comes from, the sender would then penalize (in terms of internal reputation score) either no one or the whole route, which frustrates the whole point of propagating error messages back to the sender.

The idea is to instead have every hop of the route authenticate the message via an HMAC as well. This way, if the error message is corrupted, the sender can always pinpoint a pair of nodes where the corruption happened and be sure that one of them is responsible.

The issue is that, in order to preserve the privacy guarantees that Lightning's Onion Routing provides, each node on the route must provide several HMACs, one for each potential position it is sitting in on the route, from 27th hop (the highest possible number of hops) to 1st hop[^1]. Even with some optimizations, this still leads to an error packet of 12KB. However, Jager notes, this should not be so problematic if the frequency of errors do decrease as expected, and this size could be brought down by setting the maximum number of hops in a route to a lower amount.

## Closing Bit

Entourée de ténèbres aveugles,\
Peuplée de moines-bâtisseurs ayant fait voeu de silence,\
Et parcourue par la douleur sourde des innocents qui en trouvent la porte\
C'est une bien étrange cathédrale.

Elle scintille là où il n'y a pas encore de lumière\
Et les photons diffus semblent jaillir de ses vitraux-mêmes\
Comme s'ils étaient l'émanation d'une explosion ancienne et singulière\
Dont l'onde, en passant, cadancerait les ères.

C'est une chose à voir que ce scintillement!\
Prêtes-y un regard, voyageur inconscient\
Tandis que tu glisses, sans bruit et sans tourment\
Vers le prochain lieu de ton asservissement.

[^1]: Or, to put it another way, as we want hops to ignore where they are on the route, or even how long the route is, for privacy reasons, we have them provide an HMAC for any position they could be in.

---

If you enjoyed this recap, you can show your appreciation by throwing a few coins to *fanis @ lnmarkets.com*, by scanning or clicking the QR code.

Thank you!

{{<figure align=center src="../../images/lnm_lnurl.png" link="lightning:fanis@lnmarkets.com">}}
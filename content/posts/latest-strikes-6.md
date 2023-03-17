---
title: "Latest Strikes 6 - Oct 16th"
date: 2022-10-16T19:00:00+02:00
block: "759103"
cover:
    image: "../images/DALL·E 2022-10-17 09.43.07.png"
    alt: "A set of interconnected pressure release valves surrounded by an electric power transformation station, sky in the background during civil twilight"
    caption: "'A set of interconnected pressure release valves surrounded by an electric power transformation station, sky in the background during civil twilight' Generated with DALL·E."
    relative: "false"
tags: ["bitcoin", "lightning"]
categories: ["strikes"]
draft: false
---

## Specs & Implems

### Da Bug (do not eat it)

This week was the scene of a fun (and overall not so harmful) bug in LND. The bug came from {{<newtabref href="https://github.com/btcsuite/btcd" title="btcd">}}, a Bitcoin library on which LND relies to parse new blocks. The library still had a reminiscence of SegWit V0, in the form of a check on the witness size (eg size of signatures, although it's not strictly equivalent) of Bitcoin transactions.

This check, that was happening at the wire protocol level, triggered a bug when {{<newtabref href="https://nitter.net/brqgoo" title="@brqgoo">}} published a 998-of-999 multi-signature {{<newtabref href="https://mempool.space/tx/7393096d97bfee8660f4100ffd61874d62f9a65de9fb6acf740c4c386990ef73" title="transaction">}}, thus exceeding the size limit on witness data still enforced by btcd. Hence, LND nodes didn't accept this new block, and fell out of sync.

The fix, promptly released by {{<newtabref href="https://nitter.net/roasbeef" title="Olaoluwa Osuntokun">}}, was nothing more than {{<newtabref href="https://github.com/btcsuite/btcd/pull/1896/files#diff-d90adfff2befe29fa72ab522be237f2565daf0abf0dc1069beff4563b13119fe" title="changing the variable">}} constraining the size of witness data from the previous 11,000 bytes to 4,000,000 bytes (the maximum size of a Bitcoin block). The consequence of the bug for LND nodes was the inability to open new channels, due to being out-of-sync, as well as being exposed to potential theft.

Indeed, if a transaction closing one of your channels was in the same block as @brqgoo's transaction, your node wouldn't have been able to catch it, allowing an indelicate peer to get more than their fair share of the funds. It is hence strongly advised to update to {{<newtabref href="https://github.com/lightningnetwork/lnd/releases/tag/v0.15.2-beta" title="v0.15.2-beta">}} asap.

### Proposal: Forwadable Peerswaps

ZmnSCPxj {{<newtabref href="https://lists.linuxfoundation.org/pipermail/lightning-dev/2022-October/003710.html" title="proposed">}} a variation of {{<newtabref href="https://www.peerswap.dev/" title="PeerSwaps">}} called Forwadable PeerSwaps, where a swap can happen between nodes that don't share a direct channel.

PeerSwaps allow two peers sharing a channel to perform a swap between on-chain and off-chain (Lightning) funds, in order to rebalance a channel between them. For example, if Alice has 90% of the capacity on her side of her channel with Bob, it might be of interest for both of them to rebalance the channel to better suit the flow of payments (and hence earn additionnl routing revenue). With PeerSwap, Alice pushes some funds to Bob on the channel, effectively moving the liquidity from the crammed side of the channel to the depleted one, while Bob sends the same amount of money to Alice, but on-chain. The swap can be performed in a trusless manner thanks to the use of HTLCs: Alice's transaction to Bob is a classic Lightning transaction (thus with an HTLC), while Bob's on-chain transaction to Alice has an HTLC output, from which Alice spends to claim the funds. The swap is hence *atomic*, as either both transactions are successful, or they both fail.

PeerSwap can currently only be performed by peers (nodes that share a direct channel), hence the name. This limitation comes from the fact that multi-hops swaps would inherently be less reliable and harder to coordinate.

ZmnSCPxj's Forwadable PeerSwaps aims to address this limitation. Instead of sending the funds on-chain to Alice, Bob could see that another of his channels is unbalanced (say a channel with Carol), with him having too much liquidity on his side. Bob would then forward the swap to Carol on Lightning, and Carol would send the funds to Alice's address (without even knowing Alice's existence). To Alice and Carol, it appears as if they both conducted independent swaps with Bob, but in reality it was only one swap with Bob acting as a trustless middleman. A key benefit is that now, instead of only rebalancing one channel, we rebalanced two, with the same amount of on-chain transactions. And of course, Carol could very well decide to forward the swap to Dave, and so on.

As the number of hops in the swap increases, so does the probability of something going wrong somewhere. We trade efficiency (in terms of number of channels rebalanced per on-chain transactions) for reliability. However, the reliability tradeoff can be mitigated by the fact that every node in the swap knows if their peers are online or not, and how the liquidity is spread on their channels.

A careful reader will have noted that, unlike regular Lightning payments, Forwadable PeerSwaps are packet-routed, not source-routed. This means that each hop decides whether to forward the swap further or to settle it there (by sending the on-chain funds), and that they decide where to forward it (if they do forward it). To benefit from the rebalacing effect, they will forward it on a unbalanced channel and, from one to the next, the swap will be forwarded until it reaches a balanced node. This very much reminded me of {{<newtabref href="https://en.wikipedia.org/wiki/Gradient_descent" title="gradient descent">}}, and likewise it theoretically leads to a stable local state where channels are balanced across the network.

## Wallets & Tools

### LNsploit

Tony Giorgio {{<newtabref href="https://stacker.news/items/80134" title="announced">}} {{<newtabref href="https://www.nakamoto.codes/BitcoinDevShop/LNsploit" title="LNsploit">}}, a Lightning Network toolkit built on top of LDK. It can be plugged to a bitcoind instance with funds available to launch and manage a handful of Lightning nodes, from which to perform various possible exploits. Attacks include channel jamming, publishing old commitment transactions, balance probing, and even an exploit of the latest {{<newtabref href="../latest-strikes-6/#da-bug-do-not-eat-it" title="btcd/LND bug">}}, where you can craft and publish a big enough Bitcoin transaction to prevent your target from reading the block this transaction is in. If this transaction is a closing transaction, or if you put a closing transaction in the same block, you can cheat on your out-of-date peers, granted they don't use any watchtower.

### No Big Deal

Zebedee {{<newtabref href="https://blog.zebedee.io/announcing-nbd/" title="launched">}} No Big Deal (NBD), an open source initiative that already has given a lot of very cool and useful lines of code to the world. The very prolific {{<newtabref href="https://nitter.net/fiatjaf" title="fiatjaf">}} is the main contributor, with a variety of project, including a Lightning wallet, a Core-Lightning plugin or a Lightning library, all of them centered aroung the support for {{<newtabref href="../what-are-hosted-channels/" title="hosted channels">}}.

The fact that Zebedee only publicly talks about NBD now, with a lot of things already released, instead of having made an announcement of an announcement, speaks to the dedication and focus of the team. I am personnaly really looking forward to all the software the {{<newtabref href="https://nbd.wtf/" title="NBD">}} team will release in the future - it'll probably be a pretty big deal.

## Ecosystem

### River Lightning Services

{{<newtabref href="https://river.com" title="River Financial">}} {{<newtabref href="https://nitter.net/River/status/1579851931207360515" title="announced">}} their Lightning infrastructure service, named River Lightning Services ({{<newtabref href="https://rls.dev" title="RLS">}}). River has been quite early among financial institutions in adopting Lightning, and in the process gathered a real expertise in how to manage Lightning nodes at scale. They will now be providing this service to other entities (exchanges, financial institutions, payment processors, etc.), abstracting all the Lightning complexity, as they already have for the Chivo wallet for the past year.

### Lightning Halloween

The first edition of {{<newtabref href="https://bolt.fun/hackathons/lightning-halloween/" title="Lightning Halloween">}}, sponsored by {{<newtabref href="https://fulgur.ventures" title="Fulgur Ventures">}}, will take place in Italy right after the {{<newtabref href="https://planb.lugano.ch/planb-forum/" title="Plan B Forum">}} in Lugano. It aims at gathering people and builders of the Lightning community, with talks and workshops. Everyone is welcome, but be aware that the discussions will be of technical nature, and the number of available spots is limited.

## Research & Papers

### River Floats A New Report Downhill

River Financial published a very cool {{<newtabref href="https://nitter.net/SDWouters/status/1579895854273814529" title="report">}} based on their experience as industrial-grade node runners. The piece is very well written, so I encourage people to read it in full, but here are a few points worth highlighting:
- capacity is not paramount, and a well-managed node can be a better peer than a not so well managed node that has more capacity,
- channel count is a more interesting metric as it signals some established relationship with part of the network,
- the frequency of Lightning payment failures tends to decrease over time (River now processes payments with a 98.7% success rate). On their nodes, the River team observed that the biggest contributor (~60%) to failures is still timeouts when looking for a route, while the absence of a route roughly makes for the rest of the failures,
- while developing their Lightning infrastructure, the River team incidentally generated a 1.15% APY through routing fees.

## Free Ziya

It isn't directly Lightning-related, but I couldn't imagine staying silent on this: in 2 days, it will be a month since Bitcoin educator {{<newtabref href="https://nitter.net/gladstein/status/1579166976995635200" title="Ziya Sadr">}} was arrested by Iranian Security Forces. The {{<newtabref href="https://nitter.net/LaurentMT/status/1580663610803908608" title="latest news">}} aren't encouraging. We must be his voice and relentlessly ask for his liberation.

## Closing Bit

{{<blockquote>}}
Un frisson court sur l'échine du train,\
Immense bête harnachée.\
Partout les voyageurs fourmillent\
-- C'est le jour du grand départ.
{{</blockquote>}}

---

If you enjoyed this recap, you can show your appreciation by throwing a few coins to *fanis @ lnmarkets.com*, by scanning or clicking the QR code.

Thank you!

{{<figure align=center src="../../images/lnm_lnurl.png" link="lightning:fanis@lnmarkets.com">}}
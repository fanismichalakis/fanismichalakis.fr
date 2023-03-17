---
title: "Latest Strikes 17"
date: 2023-01-02T19:00:00+01:00
block: "770063"
cover:
    image: "../images/PikachusMeditation.min.png"
    alt: "A 3D render of Pikachu meditating, in levitation, at peace."
    caption: "\"Pikachu's Meditation\". Generated with DALL·E."
    relative: "false"
tags: ["bitcoin", "lightning"]
categories: ["strikes"]
draft: false
---

Happy New Year! And welcome for the 17th edition of Latest Strikes, your weekly recap of Lightning news. As you can imagine, last week wasn't the busiest of the year, but here we are. Take a sit and a cup of coffee or tea, and let's start this new year together, shall we?

## Ecosystem

### 2022 Rewinds

The first days of January are for rewinds! Here are a few of them, but I surely didn't catch them all, so feel free to drop the ones I missed in the comments.

{{<newtabref href="https://geyser.fund/entry/529" title="Geyser">}} will turn one in January 2023 and definitely demonstrated the power of Lightning for crowdfunding, while {{<newtabref href="https://nitter.at/RoboSats/status/1609207997993041925" title="Robosats">}} just celebrated their first year on December 31st, as well as over 90 BTC transacted in total!

Stephan Livera {{<newtabref href="https://stephanlivera.com/episode/447/" title="sat down">}} with k3tan for a roundup of 2022, and the Standard Sats team {{<newtabref href="https://stacker.news/items/115710" title="went back">}} on the impact of the Russian invasion of Ukraine on the development of some Lightning wallets and tools.

Finally, if you're a user of Fountain, they published some {{<newtabref href="https://nitter.at/fountain_app/status/1608813946223616002" title="statistics">}} for last year (over 2 bitcoins earned by podcasters through Value 4 Value!) as well as a cool tool to see (and share) your 2022 stats (simply head to `https://fountain.fm/<your_username>/2022`).

### Bounties

Looking for cool open source Lightning projects to contribute to? Eric Sirion {{<newtabref href="https://nitter.lacontrevoie.fr/EricSirion/status/1608517985161076737" title="is offering">}} a 5 million sats bounty for an alternative pay plugin for Core Lightning, written in Rust using {{<newtabref href="https://lightningdevkit.org/" title="LDK">}}, and implementing optimized payment pathfinding algorithms (such as *Pickhardt payments*) with enhanced payment splitting and route ranking compared to the current algorithm used in Core Lightning.

Fiatjaf {{<newtabref href="https://gist.github.com/elsirion/8c1453fe3120dc3f7ba843a6a062dc9e?permalink_comment_id=4418160#gistcomment-4418160" title="followed suit">}} and added 1 million sats to the bounty. If you're interested, you can see the details of the bounty {{<newtabref href="https://gist.github.com/elsirion/8c1453fe3120dc3f7ba843a6a062dc9e" title="here">}}.

On a slightly different note, RoboSats has a very cool {{<newtabref href="https://github.com/users/Reckless-Satoshi/projects/2" title="Developer Rewards Panel">}}, with various eligible tasks and rewards ranging from 50,000 sats to 5 million sats. Go check it out!

### Strike Commerce Update

Strike CEO Jack Mallers {{<newtabref href="https://nitter.at/jackmallers/status/1608980987383537665" title="shared">}} some update regarding Strike Commerce and the announcements that were made in Miami during Bitcoin 2022.

Back then, Jack had announced a few partnerships with entities such as Shopify (e-commerce platform for online stores), Blackhawk (gift/prepaid cards) and NCR (point of sale devices). Since then however, these announcements have been slow to materialize. In his {{<newtabref href="https://scribe.rip/strike-commerce-update-1554f37f9b4b" title="post">}}, Jack addressed the various delays and his earlier over-optimistic statements while reassuring that:
- the announced integrations are still underway (the Shopify one being already live, and expected to be officially featured in Shopify's plugin marketplace in Q1 2023),
- a partner integrating Strike actually integrates the Lightning Network, only through the use of Strike's services. In other words, customers of a business using Blackhawk or NCR should be able to pay in bitcoin through Lightning with any Lightning wallet, not just Strike[^1] (which is, if I'm being honest, quite expected but still nice to have).

## Wallets & Tools

### More Swapping Tools

We all love transacting on Lightning, but sometimes you still need to go back on-chain, to pay a large amount or to put funds to rest in cold storage. There are tools to do so that allow you to perform swaps between Lightning and on-chain bitcoin. One of them is Boltz, which uses {{<newtabref href="https://docs.lightning.engineering/the-lightning-network/multihop-payments/understanding-submarine-swaps" title="submarine swaps">}} to perform atomic and trustless swaps.

Last week {{<newtabref href="https://www.diamondhands.community/" title="DiamondHands">}}, a Bitcoin and Lightning community in Japan, {{<newtabref href="https://nitter.lacontrevoie.fr/DiamondHandsLN/status/1608138146872721409" title="opened">}} their own Boltz instance to the public. Swapouts (where a user converts Lightning funds to on-chain) comes with a 0.2% service fee (slightly less than the main Boltz {{<newtabref href="https://boltz.exchange/" title="instance">}}) and swapins (on-chain to Lightning) are rewarded uo to 0.15% by DiamondHands, to attract liquidity to their node.

On the same week, open source developper {{<newtabref href="https://github.com/dni" title="dni">}}, known for their work on LNBits and Boltz, {{<newtabref href="https://nitter.lacontrevoie.fr/dnilabs/status/1607117088094842881" title="released">}} a Python package that can be used as a CLI client to perform swaps on Boltz.

Very cool to see more swapping solutions, so kudos to the Boltz team for making their solution open source, allowing other people to create their own instance of Boltz and further decentralizing the liquidity bridges between Lightning and the Bitcoin chain.

### Hand Out Lightning Tips To Friends, Family (& Strangers If You Want To)

It is now possible to create {{<newtabref href="https://stacker.news/items/114700" title="several tips">}} at the same time using {{<newtabref href="https://lightsats.com" title="Lightsats">}}. This update comes with the nice touch of still being able to contextualize the message that the recipient will see with their name (or something else) using a `name` variable. Quite handy for family meetings!

Since Christmas, Lightsats also offers the possibility to print your tips on a gift card, a bit like {{<newtabref href="https://tipcards.io/" title="Lightning Tip Cards">}} does.

## Specs & Imples

### Full Taproot Support in LND?

Lightning Labs developer Olaoluwa Osuntokun wrapped up the year with the {{<newtabref href="https://nitter.lacontrevoie.fr/roasbeef/status/1609010773845737473" title="exhibit">}} of "taprooty level 1" Lightning channels on testnet. To put it in a nutshell, LND users will soon™ be able to open and close channels using Musig2, thus rendering their channel opening/closing transactions indistinguishable from "regular", single-signature transactions (and saving some fees in the process, as well as bandwidth for channel announcements).

*Musig2 is a protocol for multiple users to safely[^2] aggregate public keys and signatures, so that `n` keys out of `n` are required to sign a transaction, while the transaction on-chain looks like a standard single-signature transaction. This is achieved thanks to Schnorr signatures and their property that a signature for the sum of two public keys is the sum of the signatures for the two public keys.*

*Musig2 improves upon Musig, notably by requiring less interactivity between signers, with only two interactive steps in the signing process, making it far more usable in practice (for example to open Lightning channels).*

## Closing Bit

La clé était là, sur la table\
Personne ne l'a prise\
Cette porte n'en valait pas la peine.

---

Want to receive Latest Strikes straight to your inbox every week? Couldn't be easier: subscribe to {{<newtabref href="https://blog.lnmarkets.com" title="LN Markets Ghost blog">}} and you're all set (remember to confirm your subscription by clicking the link sent via email).

---

If you enjoyed this recap, you can show your appreciation by throwing a few coins to *fanis @ lnmarkets.com*, by scanning or clicking the QR code.

Thank you!

{{<figure align=center src="../../images/lnm_lnurl.png" link="lightning:fanis@lnmarkets.com">}}

[^1]: Weirdly enough, Jack's blog post makes it abundantly clear for Blackhawk, but not so much for NCR. Let's wait and see, I guess.

[^2]: For example, Musig2 ensures that it is not possible for one party to craft keys or nonces in a way that would allow them to signle-handedly sign transactions by themselves.
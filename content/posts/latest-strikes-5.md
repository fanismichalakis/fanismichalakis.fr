---
title: "Latest Strikes 5 - Oct 9th 2022"
date: 2022-10-09T15:00:00+02:00
block: "757871"
cover:
    image: "../images/dalle_high-quality-photo-of-a-man-standing-on-a-cliff-during-a-storm-looking-at-the-ocean-beneath-him-digital-art.png"
    alt: "High quality photo of a man standing on a cliff during a storm, looking at the ocean beneath him, digital art"
    caption: "'High quality photo of a man standing on a cliff during a storm, looking at the ocean beneath him, digital art' Generated with DALL·E."
    relative: "false"
tags: ["bitcoin", "lightning"]
categories: ["strikes"]
draft: false
---

Geia sas! Welcome to this 5th issue of Latest Strikes, your weekly recap of what's new in the Lightning realm. Zip up your jacket, tuck your chin into the collar, and enter the storm with me!

## Wallets & Tools

### Alby Release (and Nostr soon)

The Alby team landed a new {{<newtabref href="https://github.com/getAlby/lightning-browser-extension/releases/tag/v1.17.0" title="release">}}, which improves the LNBits integration and allows users to connect from their own LNDHub instance (or the instance of a friend), and not just your BlueWallet Lightning account.

Additionnaly, Rene Aaron showed during {{<newtabref href="https://nitter.net/_reneaaron/status/1578003866351812608" title="Alby's Community Call">}} a first version of a Nostr integration in Alby. This feature will allow users to sign Nostr messages in the browser using the Alby extension, with a user experience that is very similar to sending a Lightning payment (you click a button on a website and Alby pops up).

In my opinion, this integration enables a lot of very cool and promising synergies between Lightning and Nostr in the web, with a very nice user experience!

### Tao Wallet

Danny Diekroeger {{<newtabref href="https://nitter.it/dannydiekroeger/status/1578148272555716611" title="launched">}} a new project: {{<newtabref href="https://github.com/dannydeezy/tao-wallet" title="Tao">}}, an opensource BTC and USD digital wallet with support for on-chain and Lightning. The project is still in the early phase, but I find the idea quite interesting: let users choose what backend they want to use and let Tao interface with that. An experienced Bitcoin user could connect Tao to their own self-sovereign Bitcoin/Lightning node, while less tech savy users could connect Tao to their custodial account. Of course, the range of features will not be the same depending on the backend, and you could even have one Tao wallet connected to different backends, for different use cases.

Right now, Tao uses {{<newtabref href="https://lnmarkets.com" title="LN Markets">}} as the backend, which enables users to perform `BTC<-->USD` swaps on top of more classic wallet features (send & receive funds).

Danny is currently looking for people to join him on this journey, so feel free to reach out!

## Implems & Specs

### Impact of Full-RBF on zero-conf channels

There's been some {{<newtabref href="https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2022-October/020980.html" title="discussions">}} this week around the impact that the new {{<newtabref href="../fullrbf/" title="Full-RBF">}} policy would have on Lightning wallets and services that provide zero-conf channels (aka {{<newtabref href="../turbo-channels/" title="Turbo Channels">}}).

When opening a zero-conf channel to a user, wallets such as Muun, Breez or Phoenix assume a temporary risk while the on-chain deposit transaction is unconfirmed: the user could spend the funds from the channel, and then cancel the initial deposit transaction using RBF while it's still in the mempool.

However, the Full-RBF policy will be merged into Bitcoin Core only as an opt-in feature. By default, nodes running Bitcoin Core will stick to the current policy (e.g. {{<newtabref href="https://bips.xyz/125" title="BIP0125">}}). Yet, the fact that a Full-RBF policy will now be activatable simply by modifying Bitcoin Core's configuration file arguably makes it easier for node operators to enable than it was before, which increases the risk associated with accepting zero-conf transactions (including for opening channels).

I think relay policies are an interesting discussion, because they concern rules that each node operator can define and choose for themselves. Some nodes already follow a Full-RBF policy, and it was always possible to do so. The only thing Bitcoin Core 24.0 will bring is more uncertainty, which should be factored in by wallets enabling zero-conf channels.

## Ecosystem

### BoltObserver - The Path to Reliability

In this {{<newtabref href="https://boltobserver.substack.com/p/the-path-to-reliability" title="blog post">}}, Alexandre Bussutil from {{<newtabref href="https://bolt.observer" title="Bolt Observer">}} addresses the question of reliability in the Lightning Network, and how to use observability to improve your node's reliability, as well as check the reliability of a potential new peer.

Three areas of improvement are covered in the article: reachability, latency and connectivity. An actionable reachability improvement consists in having monitoring set up to check that your node is always reachable, and send an alert if it's not. This way, you can detect quickly if something is wrong, and fix it.

Regarding latency, a good idea is to inspect the latency of a node before considering connecting to it. Many Tor nodes suffer from high levels of latency (several seconds), which impacts payment reliability a great deal.

Finally the idea behind connectivity is that the more nodes there are in the route of a payment, the more the chances that something goes wrong somewhere and the payment fails. {{<newtabref href="https://bolt.observer/explorer" title="Bolt Observer's explorer">}} provides a nice tooling to see how far potential peers are from you in terms of network topology and help you decide whether or not to connect to them.

### Onboarding nocoiners to Bitcoin & Lightning

Remember the {{<newtabref href="https://makers.bolt.fun/tournaments/1/overview" title="Legends of Lightning">}} contest I wrote about in the {{<newtabref href="../latest-strikes-3/#boltfun-tournament-announced" title="last edition of September">}}? Juan is working on a cool {{<newtabref href="https://makers.bolt.fun/story/looking-for-a-team-to-tackle-this-project--141" title="project">}} to onboard nocoiners and is looking for teammates for the tournament.

The idea is simple: a webapp where a bitcoiner orange-pilling someone can deposit sats, which can then be redeemed by the orange-pilled nocoiner later on, simply by scanning a QR code. This helps circumvent the classic problem of having someone install a wallet in a noisy pub. Additonnaly, an expiration period is set up so that, if the nocoiner isn't that much orange-pilled after all and doesn't claim the sats, the funds automatically go back to the bitcoiner's wallet.


### Some Stats

We reached 5,000 bitcoins deployed on Lightning!

{{< tweet user="mempool" id="1578056916693024768" >}}

{{<newtabref href="https://ln.capital" title="LN.capital">}} published the 4th issue of their {{<newtabref href="https://nitter.net/LN_Capital/status/1578461781026279426" title="Lightning Report">}}. Take a look at it, because it's clear and concise as always! Of particular interest for me was the 6 months comparison (now vs March) of big industrial nodes capacity, including wallets, exchanges and swap services. What we see is a global increase everywhere. On the wallet front, ACINQ remains unchallenged in absolute capacity, but custodial Wallet of Satoshi made some tangible gains.

In the swap services jungle, {{<newtabref href="https://deezy.io/" title="deezy">}} (from the same {{<newtabref href="https://nitter.net/dannydiekroeger" title="Danny Diekroeger">}} who is building {{<newtabref href="../latest-strikes-3/#tao-wallet" title="Tao">}}) made an outstanding 900% increase in capacity, from rougly 10 BTC capacity back in March to 90 BTC today. The service now surpasses LOOP and Boltz in terms of capacity! Impressive.

### Lightning Adoption in the Fiatest Venues in Europe

Seems like the merchant adoption in Europe is also coming from places where you didn't expect it. McDonald's (in {{<newtabref href="https://tether.to/en/plan-b-foundation-rolls-out-large-scale-crypto-payments-in-lugano-onboards-mcdonalds-and-more/" title="Lugano, Switzerland">}}) and Subway (in {{<newtabref href="https://nitter.net/jokoono/status/1577993640600821761" title="Berlin, Germany">}}) seem to be accepting Bitcoin and Lightning payments. One can only wonder whether the (forced?) adoption of Bitcoin in El Salvador played a role in global companies acceptance of Bitcoin. In Lugano's case, the adoption is fueled by the Plan B Foundation (a joint initiative between the City of Lugano and Tether).

In Berlin, a Subway restaurant uses {{<newtabref href="https://getlipa.com/en" title="Lipa for businesses">}}, which is quite refreshing as Lipa wallets are non custodial (I hear the new slang is *unhosted*?).

### And More Merchant Mapping

The {{<newtabref href="https://btcmap.org" title="BTCMap">}} project pushed a new {{<newtabref href="https://nitter.net/BTCMapDotOrg/status/1578813296903217153" title="feature">}}: you can now tip the person who properly tagged a place in OpenStreetMap to thank them!

## Closing Bit

{{<blockquote>}}
Un météore s'est écrasé\
Près du Golfe du Mexique.

A l'intérieur :\
Un ordinateur.

A l'intérieur :\
Une clé privée.

256 bits magiques\
Echos distants du commencement.
{{</blockquote>}}

---

If you enjoyed this recap, you can show your appreciation by throwing a few coins[^1] to *fanis @ lnmarkets.com*, by scanning or clicking the QR code.

Thank you!

{{<figure align=center src="../../images/lnm_lnurl.png" link="lightning:fanis@lnmarkets.com">}}

[^1]: Minimum is 1000 sats, as it is the minimum deposit size on {{<newtabref href="https://lnmarkets.com" title="LN Markets">}}.
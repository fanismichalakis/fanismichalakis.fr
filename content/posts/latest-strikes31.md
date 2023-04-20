---
title: "Latest Strikes 31"
date: 2023-04-14T20:20:00+02:00
block: "785390"
cover:
    image: "../images/PiratesOfLightning.jpg"
    alt: "A pirate two-masted ship in the middle of an electric storm, with a bit of synthwave atmosphere."
    caption: "\"The Pirates of Lightning\". Generated with Stable Diffusion."
    relative: "false"
tags: ["bitcoin", "lightning"]
categories: ["strikes"]
draft: false
---

Annnnd it's Friday again! We'll try to not make an habit out of it and come back to a more regular schedule, but I'm hearing later is better that never. Anyway, what did the Lightning world cook for us last week? Mutiny raised funds to develop their privacy focused Lightning wallet, the Price of Anarchy paper got released, and splicing discussions kept the Lightning-Dev mailing list busy. Let's dive in, shall we?

## Ecosystem

### Some Stats

Let's begin our wrap up with some Lightning stats. Kevin Rooke produced some awesome visualizations again last week, showcasing how Wallet of Satoshi processed an All Time High {{<newtabref href="https://nitter.lacontrevoie.fr/kerooke/status/1642141494944358401" title="905,000 Lightning payments">}} in March, of which around 190,000 came from THNDR games withdrawals alone. Indeed, the Lightning-gaming company set its own new record with more than {{<newtabref href="https://nitter.lacontrevoie.fr/kerooke/status/1641768276211408898" title="300,000 payments">}} in March alone, of which {{<newtabref href="https://nitter.lacontrevoie.fr/kerooke/status/1644409881192005632" title="two third">}} went to Wallet of Satoshi.

Of course, we'd like to see more withdrawals going to non-custodial wallets, but the cost incurred to open one's first channel on wallets such as Breez or Phoenix makes it unpracticable for withdrawing from THNDR games, where accrued rewards over a few days rarely surpass a few thousand sats[^1].

The crowdfunding platform Geyser was also {{<newtabref href="https://nitter.lacontrevoie.fr/kerooke/status/1642511682055307267" title="on fire">}} last week, doubling their previous February ATH with more than 2.5 bitcoins collect by the various project on the platform during the month.

On a different note, Amboss {{<newtabref href="https://nitter.lacontrevoie.fr/ambosstech/status/1642474097249492994" title="shared">}} that the Magma marketplace surpassed 100 BTC of channel capacity deployed, accruing a total of around a third of a bitcoin to the liquidity providers on the platform. The Magma platform will turn 1 year old in a few weeks, and allows Lightning node operators to "lend" liquidity to other operators on a marketplace, by offering to open a channel for a fee. The side providing liquidity also commits to keeping the channel open for a minimum amount of time (typically 90 days), and can also collect fees on the channel as is normally the case in Lightning. Overall, the average APR for channel lenders has been around 3%[^2], which is an impressive number considering it is risk-free, self-custodial yield.

We've got some happy metrics to {{<newtabref href="https://nitter.lacontrevoie.fr/LNMarkets/status/1646796051121053696" title="share">}} ourselves at {{<newtabref href="https://lnmarkets.com" title="LN Markets">}}, with a new trading volume ATH set in March with 1,850 BTC!

### Bounties

Zeus wallet opened two new {{<newtabref href="https://www.nobsbitcoin.com/zeus-wallet-opened-two-new-bounties/" title="bounties">}}, one for the addition of the {{<newtabref href="https://lightning.readthedocs.io/lightning-commando.7.html" title="commando">}} and {{<newtabref href="https://github.com/aaronbarnardsound/lnmessage" title="lnmessage">}} connection methods to pair one's Core Lightning node, and the other to integrate Zeus Point of Sale to Clover terminals.

Commando enables Core Lightning users to connect and issue commands to their node through the Lightning Network itself, while lnmessage uses websockets and commando to achieve the same.

The Zeus Pos is already {{<newtabref href="https://fanismichalakis.fr/posts/latest-strikes-24/#zeus-update--point-of-sale-documentation" title="available">}} for Square terminals, and porting it to Clover ones would further expand its usage, as Clover has quite a strong market share.

### Zaprite

This one was a "aha" moment for me. {{<newtabref href="https://zaprite.com" title="Zaprite">}} is a Bitcoin-native invoicing tool that helps you create invoices and get paid with Bitcoin, either on-chain or Lightning. There's no KYC, and it's non-custodial. It literally took me 5 minutes to create an account and link my Umbrel node sitting behind Tor at home. From then on, I was able to create invoices (as in commercial invoice, aka a bill, not a Lightning invoice), send them to my customers (myself, for the sake of the demo), and they were able to pay by following a link or scanning a QR.

Zaprite was just {{<newtabref href="https://nitter.lacontrevoie.fr/ZapriteApp/status/1643943598579171328" title="rebuilt">}}, and I really like the result! I think it's already a very useful and intuitive tool for someone running a small business, with all you need to create legally valid invoices. On top of connecting your own node, you can also link your Zaprite account to a variety of other solutions, including custodial ones such as Strike and Zebedee.

So while the Bitcoiner ethos pushes us toward self-hosting everything and using solutions such as {{<newtabref href="https://btcpayserver.org/" title="BTCPay Server">}} for invoicing, Zaprite feels like a really good middle-ground solution for people who aren't there yet on their journey, but still want to easily and safely receive Bitcoin in exchange of their work in a non-custodial fashion. Impressive!

### Lightning-powered ASIC Marketplace

Blockware {{<newtabref href="https://nitter.lacontrevoie.fr/voltage_cloud/status/1642908013831782403" title="integrated">}} Lightning into their Bitcoin ASICs marketplace, with the help of Voltage. An interesting use case, which might even pave the way for things such as Lightning payouts for miners contributing work to the Blockware Pool. We'll see, I guess?

### RGB Is Going Places

RGB - an off-chain smart contracts protocol built on top of Bitcoin and with Lightning capabilities - is coming along quite nicely recently, with the efforts of the past years bearing visible fruits. But all those fruits and efforts would be nothing without public awareness, so I was pumped to the see the LNP/BP Standards Association, which is at the core of RGB development, put together a new educational {{<newtabref href="https://rgb.tech/" title="website">}}.

On the tech-side, the latest RGB {{<newtabref href="https://rgb.tech/blog/release-v0-10/" title="release">}} finally brought stability to the core protocol, as well as very cool tooling such as the almighty {{<newtabref href="https://rgb.tech/install/#cmd" title="rgb">}} command line tool) which was showcased during the latest {{<newtabref href="https://nitter.lacontrevoie.fr/lnp_bp/status/1645854903045177344" title="demo">}}. The overall sentiment toward RGB is also a lot warmer than it used to be in the last years, and we'll probably be covering it more and more in Latest Strikes (but focused on Lightning and how RGB interfaces with the network, we swear!).

## Wallets & Tools

### Mutiny Is For Real Now

The Mutiny Wallet team {{<newtabref href="https://blog.mutinywallet.com/introducing-mutiny/" title="announced">}} that they successfully raised $300k during a pre-seed funding round, and will now work full-time on this project. The Mutiny Wallet will be a privacy-first lightweight wallet, capable of running anywhere, supported by a tailored LSP and with synthetic dollars built inside with DLCs. That's a hell of a program!

All 3 founders already have extensive expertise in the various areas that need to work together to make this happen, and can also leverage past projects (such as {{<newtabref href="https://fanismichalakis.fr/posts/latest-strikes-10/#first-mainnet-vortex-coinjoin" title="Vortex">}} coinjoins), as well as the work they've already put into {{<newtabref href="https://fanismichalakis.fr/posts/latest-strikes-12/#who-needs-a-lightning-wallet-when-you-have-a-browser" title="Mutiny">}} itself.

I'm really looking forward to what those three beasts will achieve with Mutiny, and we'll of course cover all this in the next issues of Latest Strikes.

### Blixt & Phoenix (iOS) Updates

Phoenix {{<newtabref href="https://www.nobsbitcoin.com/phoenix-wallet-v1-6-0-ios/" title="released">}} Tor support for the iOS version for their app, while Blixt {{<newtabref href="https://www.nobsbitcoin.com/blixt-wallet-v0-6-6/" title="updated">}} to the {{<newtabref href="https://lightning.engineering/posts/2023-03-29-lnd-0.16-launch/" title="latest version of LND">}}, with support for the alternative bimodal pathfinding estimator in the settings.

### PoS In WoS

Wallet of Satoshi is working on a {{<newtabref href="https://stacker.news/items/162458/r/FanisMichalakis" title="Point of Sale">}} mode, which they showcased in a short video {{<newtabref href="https://nitter.lacontrevoie.fr/walletofsatoshi/status/1644873345056518144" title="demo">}} with a BoltCard. Looks cool!

### lnproxy In Robosats

Peer-to-peer Bitcoin exchange Robosats {{<newtabref href="https://nitter.lacontrevoie.fr/RoboSats/status/1644151666617221120" title="integrated">}} {{<newtabref href="https://lnproxy.org/" title="lnproxy">}} into their trading flow with a built-in interface. Instead of having to copy-paste invoices to and from the lnproxy website, Robosats users can now enjoy the added privacy without leaving Robosats.

## Spec & Implems

### Splicing

The Lightning-Dev newsletter saw extensive discussions around Splicing last week, as the draft specification gathers more and more feedback. Now, one of the good things about being a bit late publishing Latest Strikes is that the Bitcoin Optech team has already brilliantly covered the subject in their latest {{<newtabref href="https://bitcoinops.org/en/newsletters/2023/04/12/" title="newsletter">}}, so I don't need to!

I invite the reader to take a look at the Bitcoin Optech newsletter, but to sum it up the discussions were quite technical, for example regarding commitment transactions signature exchange (where some redundant signatures can be exchanged in the current specification proposal) ; or discussion on using relative amounts to communicate if a splicing is *in* (adding on-chain funds to the channel) or *out* (removing funds from the channel).

## Research & Papers

## The Cost Of Anarchy

Sebastian Alscher {{<newtabref href="https://medium.com/@sebulino/i-analyzed-the-price-of-anarchy-in-the-lightning-network-bde4da59e02" title="published">}} his {{<newtabref href="https://github.com/sebulino/ThesisSimulation/raw/e477ed11852a70f988ea93326717feebbdc0f28f/Price_of_Anarchy_in_the_Lightning_Network_Sebastian_Alscher_20230320.pdf" title="master thesis">}} quantifying the "Price of Anarchy" on the Lightning Network.

The price of anarchy is defined as "the ratio of the failure rates of the optimal selfish strategy for participants and the failure rate when participants follow a cooperative strategy". To put it differently, it is the cost the network has to bear (in terms of payment failures) due to the fact that nodes don't share data, compared to a theoretical Lightning Network where all payment success and failure data are pooled together. Of course, such a network is not desirable from a privacy and censorship-resistance standpoint, but it's a baseline against which we can compare failure rates in the actual Lightning Network.

I have yet to digest the full thesis, but a few takeaways (notably highlighted by René Pickhardt {{<newtabref href="https://nitter.lacontrevoie.fr/renepickhardt/status/1643579862530113537" title="here">}}) are that LSPs can gather a lot of data and thus exert less pressure on the network (in terms of payment failures), and that probability-based pathfinding algorithms seem to lead to less failure than fee-based ones. The research also restates the importance of {{<newtabref href="https://en.wikipedia.org/wiki/Betweenness_centrality" title="betweenness centrality">}} when it comes to predicting payment failures.

## Closing Bit

Une trainée dans le ciel\
Ton sourire\
Tout un chambardement\
La ville entière gronde.

Bergère tu fais face au loup\
Qui ne recule pas\
Alors ce sont tes brebis\
Qui montrent les dents.

---

Want to receive Latest Strikes straight to your inbox every week? Couldn't be easier: subscribe to {{<newtabref href="https://blog.lnmarkets.com" title="LN Markets Ghost blog">}} and you're all set (remember to confirm your subscription by clicking the link sent via email).

---

If you enjoyed this recap, you can show your appreciation by throwing a few coins to *fanis @ lnmarkets.com*, by scanning or clicking the QR code.

Thank you!

{{<figure align=center src="../../images/lnm_lnurl.png" link="lightning:fanis@lnmarkets.com">}}

[^1]: For example, it currently costs a minimum of 3,000 sats to receive for the first time using Phoenix, since the wallet's LSP Acinq needs to open a new channel for the user (which comes at a price, since an on-chain transaction is necessarily involved). Since rewards from games disappear after a week if they're not claimed and barely exceeds this amount over this period, Phoenix isn't a good fit at all for new Lightning users getting their first sats from playing THNDR games. Them turning to custodial solutions such as Wallet of Satoshi makes perfect sense from this point of view, and one can only hope that through education and awareness this newcomers learn the limitations of custodial wallets and turn to non-custodial ones when their Lightning stash begins to grow.

[^2]: One may think this 3% APR is not in line with the aforementioned statistic of 100 BTC deployed generating 0.33 BTC in fees over roughly a year of the marketplace existence, but it's simply due to the fact that all 100 BTC were not deployed on the platform's inception. Rather, capital slowly flowed to the platform, and funds are only "locked" and generating yield while they're deployed in a channel.
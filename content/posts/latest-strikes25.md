---
title: "Latest Strikes 25"
date: 2023-02-28T16:50:00+01:00
block: "778673"
cover:
    image: "../images/georgia_pines.jpg"
    alt: "The painting \"Georgia Pines\"."
    caption: "\"Georgia Pines\", George Inness. From The Smithsonian Open Access collection."
    relative: "false"
tags: ["bitcoin", "lightning"]
categories: ["strikes"]
draft: false
---

Welcome to the 25th edition of Latest Strikes, your weekly dose of Lightning stuff! Last week saw BlueWallet sunsetting their custodial Lightning offering, some developments in the synergies between Lightning and Nostr, as well as some research on payment reliability and wallets usability. Let's dive in together!

## Ecosystem

### Check Splitting App "Settle Up" Adds Lightning Support

Settle Up is an app which, as its name conveys, allows you to easily settle debt between friends, roommates or colleagues. Take a trip to the countryside with a bunch of friends: everyone records what they pay for the group in the app, and in the end you see how to settle everything in only a handful of transactions.

The app {{<newtabref href="https://nitter.lacontrevoie.fr/settle_up/status/1628508627450355713" title="now">}} supports Lightning for settling debt, which is a bit meta, as a commonly used allegory when describing Lightning is precisely this kind of "debt settling" apps.

### Geyser Grants Round 2

The winners of the second round of Geyser Grants have been {{<newtabref href="https://nitter.lacontrevoie.fr/geyserfund/status/1628842072802312193" title="announced">}}! Out of the 90 applications it received, the board, comprised of 9 top notch bitcoiners, selected 30 projects which share the 1 bitcoin prize. All the awarded projects aim at augmenting Bitcoin adoption through education, either by translating content into local languages, creating stunning visual art to convey Bitcoin ideals, or creating vibrant communities on the field.

Congrats to all the winners! Go check them out!

### More On Zaps

I know it's starting to become a recurring topic at this point, but we're going to talk about Zaps again! As a reminder, Zaps are a new way of sending Lightning payments in nostr, where the receiver can publish a special kind of note upon reception of the funds. This allows nostr clients to display how many sats were tipped for a specific post, or sent to a user.

Jack gave the perfect one sentence {{<newtabref href="https://nitter.lacontrevoie.fr/nicolasburtey/status/1627402762886553608" title="explanation">}} of why this matters:

> Relevance algorithms have their place, but they are best informed by a truly costly action.

Basing relevance and recommendation algorithms on metrics such as likes and engagement seems like a fair approach, but a truly costly form of engagement - tipping - makes for a more precise signal. You can already experience this on websites like {{<newtabref href="https://stacker.news" title="StackerNews">}}, and I'm very curious to see recommendation algorithm built into nostr clients, taking advantage of the transparency brought by Zaps.

Speaking of transparency, I also very much appreciate the stance taken by Toni Giorgio in this {{<newtabref href="https://snort.social/e/note1v376krvvv3ra29n8smwzcq09mskhng8p0868hhdzvfeajqyhtc3q4hkeat" title="note">}}. Sure, Zaps are pretty cool, but at the same time they come by design with a privacy tradeoff. In this regard, I am very much looking forward to Bolt 12 and Path Blinding, which will solve all the privacy aspects that are linked with publicly posting a Lightning Address to receive payments or donations. The last hit on privacy that Zaps bring is that everyone can now see how many sats you got tipped, but that's the whole point. Maybe there's space for Zap notes where the amount paid is not revealed, thus acting more like a tips counter rather than displaying the full detail of the amounts tipped.

This privacy consideration is highlighted, although indirectly, by very cool websites just as {{<newtabref href="https://zaplife.lol/" title="Zaplife">}}, which counts and display all the Zaps sent in the last 4 hours. I really shows how public this data is, which is cool if users are fully aware of what it means for them and for their financial privacy.

Finally, to get back to the topic of using Zaps as a powerful metric for relevance algorithm, I'm still a bit unconvinced as to whether it will resist manipulation. It seems fairly easy to just setup a bunch of wallets to tip yourself from, and I'm not sure I see a way for clients to differentiate between real tips and fake ones.

On a different note, Fountain added support for {{<newtabref href="https://nitter.lacontrevoie.fr/MerryOscar/status/1628759537099456513" title="Zaps">}}, and some nostr-clients even turned {{<newtabref href="https://nitter.lacontrevoie.fr/GetCurrent_io/status/1627186789537521664" title="\"Zap-only\"">}} when it comes to handling Lightning payments.

Last but not least: I really like the SovrnBitcoiner community stance on Lightning: they are very critic, even sceptics sometimes, but that's good criticism. Highlighting what is not done so good today in Lightning (custody and privacy, mainly) is a duty. That's why I was really pumped to see this very good {{<newtabref href="https://sovrnbitcoiner.com/receiving-self-sovereign-zaps/" title="guide">}} they published on how to receive Zaps in a self-sovereign manner.

### HRF Donates 20 bitcoins to various projects

The {{<newtabref href="https://hrf.org/" title="Human Rights Foundation">}} is spending {{<newtabref href="https://nitter.lacontrevoie.fr/gladstein/status/1628048614391173121" title="20 bitcoins">}} to support 10 projects worldwide, with a focus on core development, education, and the strengthening of Bitcoin's core value proposition as censorship resistant money.

On the Lighting front, there are many education/community projects among the grantees, such as Qala, the Africa Bitcoin Conference, or Anita Posch's "Bitcoin for Fairness". Ekenimoh Elyan
also received a grant for her work on Lightning-enabled payment solution {{<newtabref href="https://www.easepay.io/" title="EasePay">}}, operating in Nigeria.

### Voltage Release

Voltage {{<newtabref href="https://nitter.lacontrevoie.fr/gkrizek/status/1628440689456615424" title="released">}} a new non-custodial Lightning Service Provider focused on "just-in-time liquidity". Flow 2.0 - that's its name - takes advantage of zero-conf channels to provide the receiver with a channel with inbound liquidity right when they need it. It's very much like wallets such as Acinq's {{<newtabref href="https://phoenix.acinq.co" title="Phoenix">}} operate, except Voltage brings this functionality to a wider audience.

The LSP is only deployed on testnet yet, and is intended to be interacted with mainly with API. In the future, a merchant could for example connect its BTCPay Server to Flow 2.0 via API, and not have to worry about having enough inbound liquidity anymore. Game changer!

## Wallets & Tools

### BlueWallet Sunsetting Their Custodial Lightning Offering

BlueWallet {{<newtabref href="https://nitter.lacontrevoie.fr/bluewalletio/status/1628733798438281216" title="announced">}} that they will no longer provide their Lightning custodial service. Users have until the end of April to withdraw any funds they might have on a BlueWallet Lightning account to another wallet.

The reasons behind the shutdown are a matter of speculation, but remembering that BlueWallet's node LndHub.io suffered some {{<newtabref href="../latest-strikes-21/#channels-of-prominent-wallet-vanish-into-the-blue" title="crashes">}} a few weeks ago, one can only conjecture that the main reason for sunsetting the custodial service is of a technical nature. Indeed LndHub, the technology that BlueWallet uses to *compartment* their Lightning node into accounts for their clients, doesn't seem to scale very well when there is a huge number of clients to serve.

On the other hand, it seems like BlueWallet is working on non-custodial Lightning, with a hidden beta inside the app of a full LDK (Lightning Dev Kit) node. LDK is considered today as the forth major Lightning implementation, with an emphasis on modularity and being able to run even in very resource-contrived environments - such as mobile devices.

It therefore seems like BlueWallet had already been working on a non-custodial Lightning node inside BlueWallet, but that the recent issues with their LndHub instance forced them to halt their custodial service sooner than they had planned. Hence why BlueWallet's communication focuses on the sunsetting of the custodial service without mentioning the new, incoming, non-custodial one: it's just not 100% ready yet.

Overall, this seems like a very good news for Lightning: a custodial service disappears (with a public announcement and a 2 months long grace period), and a non-custodial one is waiting in the backstage for the second act to begin.

### How Does The Typical Lightning Wallet Perform With Slow Internet?

In the meantime, BlueWallet users might be wondering which wallet to use in place of Blue. The wallet that I {{<newtabref href="https://stacker.news/items/143612/r/FanisMichalakis" title="recommend">}} is usually {{<newtabref href="https://phoenix.acinq.co/" title="Phoenix">}}, although of course the "best wallet" depends on the user's context. Anita Posch conducted a very interesting {{<newtabref href="https://nitter.lacontrevoie.fr/AnitaPosch/status/1628423145689387012" title="experiment">}} to evaluate how different wallets behave in a slow internet environment.

Her conclusion is that Phoenix was the best wallet overall, due to its non-custodial nature and the fact that it just works even with poor internet connection. Anita also wrote what I find to be a very thoughtful explanation of why non-custodial is the way to go **especially** for low income individuals:

> The usual recommendation to use only a small amount of funds [in custodial wallets], because of the custodianship, cannot be applied to lower-income users. A loss of $2 can be huge for them.

### Breez SDK In The Wild

In Latest Strikes {{<newtabref href="../latest-strikes-20/#breez-sdk--partnership" title="#20">}} and {{<newtabref href="../latest-strikes-23/#more-about-the-breez-sdk" title="23">}} we covered the new Breez SDK that enables any developer to *effortlessly* bring Lightning payments into their app.

Last week we got to see it {{<newtabref href="https://nitter.lacontrevoie.fr/SatimotoApp/status/1627441297874206721" title="used">}} in the wild by the dev behind {{<newtabref href="https://satimoto.com/" title="Satimoto">}} (Lightning native EV charging app we've already seen {{<newtabref href="../latest-strikes-13/#you-can-now-charge-your-ev-with-sats-in-europe" title="here">}}). Looks powerful!


## Spec & Implems

### Better payment flow model in lnd

LND {{<newtabref href="https://github.com/lightningnetwork/lnd/pull/6815" title="added">}} a new pathfinding probability estimator (the piece of software responsible for trying to find a route that will work well for a given payment). The current *a priori* estimator will still be the default, but users can now use a new opt-in one, called the *bimodal* estimator. This new estimator is notably based on {{<newtabref href="https://arxiv.org/abs/2103.08576" title="work">}} by Rene Pickhardt and others, and differs in that it takes into account both the assumed liquidity distribution inside channels and previous learnings from past payments.

### anyprevout.xyz Is Back

In January this year, fiatjaf {{<newtabref href="../latest-strikes-21/#anyprevoutxyz-is-out" title="announced">}} that he would no renew the {{<newtabref href="https://anyprevout.xyz" title="anyprevout.xyz">}} domain he used to educate around this *soft fork* proposal, because they were feeling it had come to a dead end.

Last week, they {{<newtabref href="https://nitter.lacontrevoie.fr/fiatjaf/status/1628791795437178881" title="reversed course">}} since Anyprevout moves two steps closer to activation. Cool!

### Redundant Overpayments

During the discussion around *Highly Available* channels that we documented {{<newtabref href="../latest-strikes-24/#highly-available-lightning-channels" title="last week">}}, another way to solve payment reliability was reiterated: redundant overpayments. The idea behind overpayments is not new, and quite simple in its essence. Instead of trying several routes sequentially to try to send a 1 million sats payment, why not try to send 10,000 chunks of 1,000 sats each, amounting for a total of 10 million sats (ten times what I want to send), but where in the end we only settle 1 million sats (the amount we actually want to send). We can indeed ensure that the receiver is only able to claim up to 1 million sats (for more details, this this 2020 {{<newtabref href="https://berkeley-defi.github.io/assets/material/1910.01834.pdf" title="paper">}}, but basically the idea is that if the receiver tries to claim more than he ought, the sender can cancel the whole transfer).

Last week, Rene Pickhardt {{<newtabref href="https://nitter.lacontrevoie.fr/renepickhardt/status/1629559701745614849/photo/1" title="showed">}} some early results, responding to a tweet from Matt Corallo. As we can see, the maximum amount sendable between the two considered nodes in only one attempt (eg we want the payment to succeed immediately, not try different routes sequentially until it does) is around 2,750,000 sats, and requires sending around 5 million sats in total (summing all the small chunks). As {{<newtabref href="https://nitter.lacontrevoie.fr/renepickhardt/status/1629075405587066880" title="expected">}}, we also see that the amount that can be delivered in one attempt starts to decline sharply after its maximum, even if we were to send more sats overall. It just doesn't matter how much we try, the payment is just too big.

### Closing Bit

Une fleur est tombée sur la terre défaite\
Sans un bruit, sans émoi, sans troubler la cueillette.\
Pourtant une fleur qui choit autrement que par l'âge\
-- Pas fânée, pas séchée, encore fière sous l'orage

C'est un gâchis si grand qu'on en verse une larme.

---

Want to receive Latest Strikes straight to your inbox every week? Couldn't be easier: subscribe to {{<newtabref href="https://blog.lnmarkets.com" title="LN Markets Ghost blog">}} and you're all set (remember to confirm your subscription by clicking the link sent via email).

---

If you enjoyed this recap, you can show your appreciation by throwing a few coins to *fanis @ lnmarkets.com*, by scanning or clicking the QR code.

Thank you!

{{<figure align=center src="../../images/lnm_lnurl.png" link="lightning:fanis@lnmarkets.com">}}
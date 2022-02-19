---
title: "What Are Turbo Channels"
date: 2021-12-04T17:26:13+01:00
cover:
    image: "../images/turbo_amusement-park-g36f09113e_1920.jpg"
    alt: "attraction park"
    caption: "<text>"
    relative: false # To use relative path for cover image, used in hugo Page-bundles
tags: ["lightning", "bitcoin"]
categories: ["articles"]
draft: false
---

Turbo channels have been around since at least 2 years now, but they remain quite largely misunderstood among the community. Information about them are available but a bit scattered. The purpose of this post is to bring them together and provide a comprehensive view on this subject.

## 0-conf channels

Turbo channels are basically 0-confirmation channels, which means the channel can be used before the channel opening transaction get mined in a Bitcoin block. Usually, a Lightning channel isn't considered as usable by both parties before its opening transaction[^1] has (typically) 3 confirmations. This is great in regard to security, as it protects users against double-spending attacks, but it has the drawback of adding several tens of minutes between the moment a user opens a channel and the moment they are able to use it.

## Why can't people just wait?

Generally speaking, you're right. There are tons of cases where you're not in any particular hurry to see your channel confirmed. If you're a patient, forward-looking, low-time preference person, you usually open Lightning channels before you need them.

But not everybody is like that, and not everybody even opens its own channels. I know, sounds crazy. But hey, there's demand for managed Lightning solutions, so there is an offer. We can divide managed Lightning wallets into two main categories:
- fully custodial wallets. Users don't have their own private keys, and users don't have their own channels. Those are the bad ones. Avoid them at all cost. [^2]
- non-custodial, trust minimized wallets. You are in control of your private keys and you have your own channels (linked to said private keys), usually between a light Lightning node on the app on your phone and the node of the wallet provider. There is some trust involved, but the amount of trust required is usually kept to a minimum. Those wallets are the way to go if you don't want to bear the hussle of maintaining your own node and your own channels by yourself but still are a sensible human being.

The first kind of managed Lightning wallet (the bad ones) can very easily make the onboarding to Lightning a seamless experience for the user:
1. User sends bitcoins on-chain to wallet provider
2. Wallet provider shows corresponding balance in the Lightning wallet

It's fast and quite cheap (modulo the mining fee to send the bitcoins), but those bitcoins on Lightning are really just an IOU the user can never enforce because he doesn't have the appropriate key to do so. Gotta trust the wallet provider.

For the second kind of managed Lightning wallet (the good ones), having the same UX is a bit more difficult. When a user wants to start using Lightning, the wallet provider must open their first Lightning channel:
1. User sends bitcoins on-chain to wallet provider
2. Wallet provider publishes a channel opening transaction for the corresponding amount (modulo fees) or more
3. User waits for the 1st confirmation
4. User waits for the 2nd confirmation
5. User waits for the 3rd confirmation
6. User can finally use their new channel and access the Lightning network!

As you can see, the classical UX of the Lightning Network, where users must wait 3 confirmations before a channel is usable, isn't necessarily appropriate for non-custodial managed wallets. That's especially true when the user wants to use Lightning to pay **now**, and can therefore not wait for so long. Moreover, having this kind of delays can repulse users and move them to custodial Lightning wallets. The bad ones!

This is why non-custodial managed Lightning wallets have pretty much all implemented Turbo Channels in various ways.

## How it's done today

Non custodial managed Lightning wallet such as {{< newtabref  href="https://breez.technology" title="Breez" >}}, {{< newtabref  href="https://muun.com" title="Muun" >}}, {{< newtabref  href="https://phoenix.acinq.co" title="Phoenix" >}} all use Turbo Channels in various ways.

For example, Muun leaves it to the appreciation of the user to decide wether or not they want to use Turbo Channels: the option is activated by default but users can choose to opt out.

Regarding the general flow, the idea is pretty much the same for all implementation:
1. User sends bitcoins on-chain to wallet provider
2. Wallet provider publishes a channel opening transaction for the corresponding amount (modulo fees) or more
3. Both ends of the channel (the wallet provider's node and the user's light node) immediately regard the channel as usuable even if unconfirmed or with less than three confirmations.

One important thing to note is that the wallet provider is the one actually opening the channel. This means that, by default, the funds in the channel will be on their side in the beginning. But those are the user's funds, as the user sent them on-chain to the wallet provider. The wallet provider must therefore push some funds to the user's side of the channel. The general flow is:
1. User sends bitcoins on-chain to wallet provider
2. Wallet provider publishes a channel opening transaction for some amount (at least the amount sent by the user on-chain, but often more)
3. Wallet provider pushes the amount the user sent in 1. (modulo wallet fees) to the user's side of the channel
4. Both ends of the channel (the wallet provider's node and the user's light node) immediately regard the channel as usuable even if unconfirmed or with less than three confirmations
5. Because there are some funds on their side of the channel, user can start to send bitcoin on Lightning right away. Usually, the wallet provider opens a channel bigger than the amount sent in 1., which means there are funds on the wallet provider's side of the channel as well and the user can start receiving payments too.

Regarding the specific details as to how this is processed by wallets and Lightning implementations, today it is up to the wallet provider. The process of specifying (eg writing the specification) how Turbo Channels should work at the protocol level has begun through this {{< newtabref href="https://lists.linuxfoundation.org/pipermail/lightning-dev/2021-June/003074.html" title="Lightning Dev mailing list message" >}}.

## What are the tradeoffs?

Using Turbo Channels, non custodial managed Lightning wallet can achieve a user experience comparable to the one provided by the custodial ones. Of course, as always, there are tradeoffs regarding trust and security that must be <mark>highlighted<mark>.

While the channel opening transaction is still unconfirmed, there is nothing on-chain that enforces the existence of the channel. If the wallet provider goes rogue and cancels the transaction in the mempool[^3], the user formally loses all the funds they didn't send while the channel was *open*:
- if the user didn't use the channel before the wallet provider cancelled it, then they lose the exact amount they sent on-chain in the beginning
- if the user used some part of the funds in the channel (for example, they paid a 50,000 sats invoice to a merchant), then they lose what they sent on-chain minus the 50,000 sats.

In the "best case scenario", the user sent all their local balance before the wallet provider's attack and are short nothing, except Bitcoin mining fees for the on-chain transaction and the wallet provider's processing fees.

Once the channel opening transaction has 1 confirmation, it is much harder for the wallet provider to execute the same attack, as it would require a reorganization of the blockchain (short: reorg). A reorg of depth 1 is still quite feasible (and even happens spontaneously) but any double spend occuring would be detected and scrutinized by the Bitcoin network's constituents.

That's where reputation comes in play. Any attempt from the wallet provider to fool the user would require the publication of a Bitcoin transaction[^4]. Even when replacing a transaction in the mempool, even if the original transaction isn't mined yet, it is known to a large portion of the network. Therefore, the wallet's provider malice can't go unnoticed, especially if the user complains on a public space where benevolent bitcoiners can hear them. Sure, the user's funds are gone, but so is the wallet provider's reputation. A reputation any ot the aforementioned non custodial wallet providers has spent years to build.

[^1]: A channel opening transaction is a Bitcoin transaction that sends funds to a multisignature address controlled by both parties of the channel. To move the funds from this address, the signature of both parties is required. In a sense, this address is the on-chain representation of the corresponding Lightning channel.
[^2]: This should be taken with some salt. I have a huge respect for wallets such as BlueWallet (non custodial on-chain, custodial for Lightning for the managed part).
[^3]: While is has not been included in a block, a Bitcoin transaction may be cancelled by spending the same UTXO(s) in another transaction that pays more fees.
[^4]: It would of course be possible to trick the user in other ways. For example, the wallet provider's app could be malicious and display false things to the user. But that can't happen with open source software, right?
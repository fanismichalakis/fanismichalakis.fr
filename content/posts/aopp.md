---
title: "AOPP: regulators getting cheesy?"
date: 2022-01-28T08:00:00+01:00
cover:
    image: "../images/aopp_meme.jfif"
    alt: "meme"
    caption: "Credits: @Loic_Psyduck"
    relative: false
tags: ["bitcoin", "regulators"]
categories: ["articles"]
draft: false
---

A (heated) discussion on a specific piece of regulation and its application has quickly spread through Bitcoin Twitter in the last hours, following a tweet by 
shaquille o'atmeal (@crypt0e):

{{< tweet user="crypt0e" id="1486782623930150913" >}}

I found the topic interesting enough to wrap up my thoughts on the matter in a short article. I hope it will also help the reader quickly get grasp of what is at stake here.

## Some Context

In some countries (Switzerland and the Netherlands), regulated exchanges and alike (often referred to as VASP in the jargon, for Virtual Asset Service Provider) are required to collect proof of *ownership* of the addresse(s) their users withdraw their funds to. This is achieved by asking the user to sign a custom message (something like "I, Fanis Michalakis, hereby confirm the ownership of address bc1...") with the private key associated with the address they want to withdraw their funds to.

The official justification for this curious (to say the least) piece of regulation is that VASP must verify the identity of the person controlling the address they send funds to, in order to curb terrorism financing and money laundering. Of course, just as KYC, this measure does absolutely nothing against both mischiefs, but efficiently paves the way for even more mass surveillance and State overreach. One could also point out that this particular measure doesn't prove anything regarding address *ownership*, as it is fairly easy for anyone withdrawing to the address of a third party to ask said third party to sign whatever message regulators may come with ; but a law's ineffectiveness is no excuse for its enactment.

## AOPP

Considering that the friction added by this requirement can drive away users from self custody, because they don't want to take this additionnal step (or don't know how to), {{<newtabref href="https://www.21analytics.ch/" title="21analytics">}}, a Swiss crypto-compliance software company, initiated the {{<newtabref href="https://aopp.group" title="AOPP">}}: Address Ownership Proof Protocol.

The goal is to enable wallets to provide a quick, easy way for users to provide the required proof of *ownership* to their VASP. If a user's wallet and their VASP both implement AOPP, all the user has to do is click a link on the VASP website or app. It will automatically open the wallet, sign the appropriate message with the appropriate private key, and send it to the VASP. From one burdensome process of copy-pasting a message and signing it with the right private key (something non tech savy users might find difficult), we now have a one-click verification mechanism.

```kd
+------+                        +---------+                          +----------+
|      |-- clicks one button -->|  VASP's |-- message and address -->|  User's  |
| User |                        | Website |                          |  Wallet  |
|      |<--------- OK ----------|         |<-- message signed with --|          |
+------+                        +---------+    corresp. priv. key    +----------+
```

For this protocol to work, it is necessary that at least some wallets implement it. Some of them do: software wallets such as BlueWallet or Sparrow, and hardware wallets such as Trezor as well. Swiss and Dutch exchanges (like Relai for example) can also implement the protocol to provide easy, one-click verification to their customers.

## Why is it a problem?

All this protocol does is making the application of law easier. The law being applied wether it is easy or not, implementing it could seem to be a good idea, as it would reduce the friction on the path to self-custody for users. Besides, I do think that it is what led to this protocol being crafted, and then adopted by many well-known platforms and wallets.

Yet, this law and its application materialize the anti-Bitcoin idea that self-custody requires permission, and permission is the first step to denial. Therefore, instead of being facilitated, this law should be fought against. If users are ready to make this compromise, so be it, but software and hardware self-custody solutions should stay absolutely neutral. This stance is very well detailed by Samourai in this thread:

{{< tweet user="SamouraiWallet" id="1486771410949357571" >}}

Since then, {{<newtabref href="https://twitter.com/SparrowWallet/status/1486785866739728386" title="Sparrow">}} and {{<newtabref href="https://twitter.com/bluewalletio/status/1486805550608392194" title="BlueWallet">}} have withdrawn themselves from the initiative, and will remove the AOPP functionnality from their software in their next release.

[EDIT at B720786]: Trezor has also {{<newtabref href="https://twitter.com/Trezor/status/1487091879883722755" title="announced">}} the removal of AOPP from their products.

## Post-Scriptum

I feel like I should explain the joke in the title a bit, or else face the unpleasant fate of it going unnnoticed. I know, if I have to explain a joke, maybe I'd be better off by just not writing it. But as a great man once said during his Golden Globes speech: I don't care.

In French, AOP stands for Appellation d'Origine Protégée: Protected designation of origin. It can be used to label many awesome products, but cheese makes for a great part of such culinary wonders.
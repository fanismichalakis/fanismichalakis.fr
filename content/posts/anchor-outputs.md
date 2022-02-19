---
title: "What Are Anchor Outputs"
date: 2022-01-03T22:00:00+01:00
cover:
    image: "../images/ropes.jpg"
    alt: "ropes"
    caption: "<text>"
    relative: false
tags: ["lightning", "bitcoin"]
categories: ["articles"]
draft: false
---

The last two "long" articles of this blog were dedicated to special kinds of Lightning channels that seek,  {{<newtabref href="https://fanismichalakis.fr/posts/turbo-channels/" title="each">}} in their {{<newtabref href="https://fanismichalakis.fr/posts/what-are-hosted-channels/" title="own">}} way, to enhance the user experience on the Lightning Network. This week, we will dive into anchor outputs, which aim to ensure channel closings are settled quicly, even in the case of a force close. This article will go into details as to how Lightning works in this regard, what are the issues and how anchor outputs can solve them. Finally, we'll take a look at how the rollout of this new mechanism can affect users.

## Closing Lightning Channels

On the Lightning Network, the state of a channel (eg, the distribution of funds between the two ends of the channel) is kept in the form of {{<newtabref href="https://www.youtube.com/watch?v=aPqI34tpypM" title="commitment transactions">}}. Those Bitcoin transactions are signed by the two parties of the channel, but not published on the blockchain until one of the two peers needs to close the channel. If the state of the channel changes (because funds moved from one end of the channel to the other), the previous commitment transaction is revoked and a new commitment transaction is crafted and signed (but not published) to account for the new distribution of funds.

In the case of a cooperative close (also known as mutual close), both peers agree on closing the channel and work together to build a closing transaction that sends the funds of the channel on-chain to each peer **proportionnaly** to what they own in the channel. During the construction of the closing transaction, the two peers notably discuss the amount of fees they want to spend on this on-chain transaction. Once the transaction is built, both peers sign it and it is then published to the Bitcoin network by the closing peer. This is better than simply publishing the last commitment transaction because fees can be adjusted to the network congestion.

In the case of a force close, by definition both peers do not agree on closing the channel and can therefore not build a closing transaction together. Instead, the peer that wants to close the channel publishes the latest commitment transaction they are aware of[^1]. This commitment transaction was built cooperatively by the two peers the last time funds moved in the channel. At that time, the peers had to decide on the fees to apply to this transaction, which is tricky because they have no idea as to when -- if ever -- this transaction will need to be published.

Because the fees can't be changed without rebuilding the transaction and both peers signing the new transaction, you have to make sure the fees will be enough when the transaction is published so that it confirms in a timely manner[^2]. Which is impossible because you don't know when the transaction will be published. And even if you did, you don't know what the transaction fees will be like on Bitcoin at that time (unless it is in the very close future). To circumvent that, Lightning implementations usually use a fee that is several times higher than the current fee at the moment of building the transaction.

## Why can't we just use small fees and bump them later?

Once a transaction is signed, its fees cannot be changed (because changing the fees changes the transaction, and the signature therefore does not match anymore). Moreover, once it is published, the whole network is aware of the transaction. But there are still ways through which one can increase (or "bump") the fees of a transaction:
- by crafting, signing and publishing a new transaction that spends the same outputs as the original one but pays higher fees. This is called Replaced-By-Fee (RBF).
- by spending one of multiple output(s) from the yet unconfirmed transaction in *child* transactions that pay higher fees. This is called Child-Pay-For-Parent and should incentivize miners to include the original transaction in their block so that they can also include its descendants.

So, why can't we use either RBF or CPFP to bump commitment transactions? This would allow Lightning nodes to craft their commitment transactions with minimal fees and bump them later if network conditions require it.

Well, we can. But there's a catch.

## Protecting the network from DoS attacks

When RBF and CPFP were implemented into Bitcoin, some protections were also put in place to prevent malicious actors from using this new features to perform Denial of Service (DoS) attacks on the network. Such attacks consist in deliberatly exhausting the ressources (CPU, memory, etc.) of the computers constituting the network to slow it down or even bring it to an halt.

For RBF, one of the rules that the replacement transaction must follow is that it "pays an absolute fee of at least the sum paid by the original transactions"[^3]. This serves two purposes. First, it effectively incentivizes miners to pick the replacement transaction. Secondly, it prevents people from spamming the network with replacement transactions at no cost. Indeed, if it was not necessary for the replacement transaction to have a greater fee, an attacker could broadcast replacement transactions that would be relayed through the nodes of the network (actively consumming relay bandwidth) but would have litteraly no chance of being added to a block, hence costing nothing to the attacker.

For CPFP, the risk is to see an attacker take advantage of how the mempool works to exhaust the computational ressources of nodes. For effiency reasons, every transaction in the mempool also references all its ancestors (parents, grand-parents, etc.) and descendants (children, grand-children, etc.) that are in the mempool too. This notably helps miners select transactions that pay higher fees overall, reject transactions that pay too little, and so on. One downside is that it makes the action of removing one transaction from the mempool more ressource-consumming, especially if this transaction has a lot of descendants that must be removed too. Same goes for adding a transaction that has a lot of ascendants. Therefore, a limit has been set to avoid DoS attacks using this vector: a given transaction in the mempool cannot have more than 25 descendants (including itself), or a total size of descendants bigger than 101 KvB (once again, including itself). Same goes for ascendants.

## Transaction Pinning

Those two limits are absolutely essential to prevent DoS attacks via abusing RBF or CPFP mechanisms. But they come with a drawback: they can in turn be used as an attack vector when a users try to fee bump a LN commitment transaction. Such an attack is called **transaction pinning** and occurs when two entities (or more) can bump the same transaction.

The idea is quite simple: one of the two peers of the channel could deliberately bump the fee of the original commitment transaction so that it reaches the anti-DoS limit (of either RBF or CPFP), and the other peer can't bump it any further. This way, the attacker effectively imposes its own version of the transaction (and its own fees) to the other peer and prevents them from being able to bump the fee like they want to.

For example, abusing the RBF anti-DoS protection could consist in attaching a transaction that is huge in size but with a small fee-rate to the original transaction. Because the rule requires the replacing transaction to pay higher fees (not higher fee-rate) than the original transaction **and** its descendants, it would require the other peer to pay a huge amount in fees to bump the transaction using RBF.

CPFP's anti-DoS rule can also be used to pin a transaction, simply by attaching 24 descendants to it (or reaching the size limit). The other peer can then not use CPFP to bump the fees of the original commitment transaction.

Attackers can hence use anti-DoS policies of RBF and CPFP to delay the confirmation of commitment transaction when the Bitcoin network is under heavy load and fees are high. Such an attack, if properly orchestrated, could allow the attackers to steal funds from honest Lightning users. It is therefore critical to find some tweak around those rules so that we can safely bump Lightning commitment transactions.

## Carve Out and Anchor Outputs

The CPFP carve out policy is one of those tweaks. It allows to add a 25th descendant to a transaction, if and only if this descendant transaction weights no more than 1,000 vB and has only one unconfirmed ancestor. Or, to put it differently, even if an unconfirmed transaction already has 24 descendants[^4], carve out allows the addition of one direct child to this transaction, with the condition than this child must not weight more than 1k vB.

But carve out alone doesn't solve our problem. We must also make sure that, just after the commitment transaction is published, each party can only spend from one (and only one) output. Indeed, consider the case where the commitment transaction has 3 ouputs. Let's say that, out of this 3 outputs, Alice can spend from one (output #1) and Bob from two (outputs #2 and #3). Bob could still pin the commitment transaction by attaching 24 descendants to output #2 and one child to output #3. He is allowed to do this thanks to carve out but, because he has done it, Alice cannot add any new child to the transaction because it would then exceed the limit granted by carve out.

If the commitment transaction only has 2 outputs and each party can spend from one only of them, the situation is very different. Bob can at most attach 24 descendants to his ouput and, by definition, he can't attach any to Alice's output. He can't attach a 25th descendant to his output either, because carve out policy only allows it if the 25th descendant is a direct child from the original transaction. Here, the 25th descendant would instead be the grandson of a grandson of a grandson of ... etc. On the other hand, thanks to carve out, Alice is allowed to add one child transaction to her own output[^5]. The commitment transaction then slightly exceeds the 25 descendants rule, but stays within the boudaries set by carve out. This way, even if Bob tries his best to pin the transaction, Alice can still bump the fees using CPFP on her own output.

The last question we must answer is how to make sure that each party has at most one output to spend from in the commitment transaction. After all, commitment transaction can very easily have more than two outputs, for example when there are in-flight HTLCs in the channel.

The secret sauce is we don't need the commitment transaction to have only one output per party *in absolute*. We only need the commitment transaction to have at most one output **spendable** per party right after it is published. This is *precisely* what **anchor outputs** do: every output of the commitment transaction is encumbered with a {{<newtabref href="https://en.bitcoin.it/wiki/CheckSequenceVerify" title="CSV">}} condition (some kind of timelock) that prevents it from being spent for at least one block, and two new outputs are added to the transaction, one for each party. Those outputs sole purpose is to be used by either of the parties to bump the fees of the commitment transaction with CPFP, using them as anchors on which to attach one or more descendants while the other outputs are still timelocked.

TL;DR: Anchor outputs are two outputs (one for each party of the channel) that are added to a commitment transaction so that the transaction fees can safely be increased without the risk of transaction pinning. This way, both peers have a chance to set the fees they want for the closing transaction.

## Wrap Up

Commitment transactions as essential to the security model of the Lightning Network because they allow for unilateral closure of channels. However, there can often be a delay between the moment they are crafted and the moment they are published, which can lead to them being stuck in the mempool because transaction fees are set at craft time. The naive solution consisting in deliberately overpaying fees when crafting the transaction is not very adequate, because on-chain fees when the transaction is published can very well be way more, leading to the transaction being stuck anyway.

Anti-DoS policies of fee bumping techniques such as RBF or CPFP made their use inadequate in the case of Lightning, where two parties can increase the fees of the same transaction. This issue was addressed for CPFP with the introduction of the CPFP carve out policy. Leveraging this policy, each party of a channel can bump the fees of an unconfirmed commitment transaction by spending from one dedicated output called **anchor output** and using Child-Pay-For-Parent.

## How does it affect end users?

From what I know, all 3 major Lightning implementations now support anchor outputs. For example, in lnd they are now the default and commitment transactions are crafted with dedicated anchor outputs in them and 1-block CSV on all the non-anchor outputs. But doing this is useless if the user doesn't keep at least some sats to add children to anchors and bump the commitment transaction's fee with CPFP. That's why lnd has started to enforce an implementation specific rule requiring that a user keeps at least 10,000 sats per open channel in their on-chain balance, up to 100,000 sats in total. This is why users might find, sometimes to their surprise, that they might be unable to open a 150,000 sats channel even though they have 200,000 sats available. That's actually what led me to research the subject and write this article: my own perplexity.

## Some ressources

Bitcoin Optech made a great job covering {{<newtabref href="https://bitcoinops.org/en/topics/anchor-outputs/" title="anchor outputs">}}, {{<newtabref href="https://bitcoinops.org/en/topics/transaction-pinning/" title="transaction pinning">}} and {{<newtabref href="https://bitcoinops.org/en/topics/cpfp-carve-out/" title="CPFP carve out">}}.

The Bitcoin and Lightning dev mailing lists are also a great source of information. For example, see Matt Corallo's {{<newtabref href="https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2018-November/016518.html" title="initial proposition">}}.

[^1]: This is what commitment transactions are useful for: closing the channel alone even if the other peer doesn't agree to the closing (or is offline).

[^2]: Which is of extreme importance because part of the security model on Lightning relies on the use of timelocks.

[^3]: Per {{<newtabref href="https://github.com/bitcoin/bips/blob/master/bip-0125.mediawiki#implementation-details" title="BIP 125">}}. The term "original transactions" refers to the intial transaction and any other unconfirmed transaction that spends from it (its descendants).

[^4]: 25 including itself.

[^5]: With the (quite manageable) condition that this transaction must not exceed 1,000 vB.
---
title: "A Few More Thoughts on PoW And PoS"
date: 2022-09-05T18:55:25+02:00
draft: true
---

It's been a few months since I posted a first article regarding the irreconciliable differences between Proof of Work (PoW) and Proof of Stake (PoS). Since then, a ot of discussions happend, notably in the Ethereum community, as they gather in ORDRE DE BATAILLE for the long-awaited Merge. Every argument I developed still stands true, but I wanted to see how the recent actuality echoes with them. This second article will also present additionnal arguments as to why PoW and PoS are absolutely not comparable.

I feel like now might be a good time to put this new piece together, as the temporal coincidence of Ethereum's switch to PoS and the ongoing energy crisis put us all in very prolific conditions for Proof of Work deniers of all kinds. I sincerely hope this piece, in line with the previous one, will help the reader make up their own, educated opinion.

## TL;DR

I'd like to begin with the conclusion, so that the reader undestands where I want to go. My thesis (which I belive is rather factual than opinionated) can be summarized in a few points:
1. Bitcoin's true value and usefulness is censorship resitance. Every other property of Bitcoin derives from it.
2. Censorship resistance is only achievable with Proof of Work. Proof of stake is not censorship resistant.
3. Proof of Work is a necessary condition to reach censorship resistance, but not a sufficient condition.

## Prerequisite: Why PoW is Censorship Resistant and PoS Is Not

My previous piece described why, even from a concetpual standpoint, PoS cannot be censorship-resistant in the same way that PoW is. I invite the reader to read the piece in full, but what it entail can be summarized in a few sentences.

Consider a situation where an entity seized a majority of the network's means of block production (eg hashrate in PoW and tokens in PoS). Once this happens, this entity is effectively able to censor the network by:
1. Refusing to include some "illicit" transactions in the blocks it produces
2. Refusing to build blocks on top of a chain that contains said "illicit" transactions, even if this chain was *bigger*[^1] than its own.

Because the censor controls the majority of the resource (eg 51% of the hahsrate in PoW), its chain will eventually be the longer one, and the rest of the network will converge to it and accept it as the *true* chain. The only way to resist this censorship is to dispute the hegemony of the censor over the means of block production.

In PoW, it can be done by pluging in new hashing machines, until the hashrate of the honest nodes outperforms the hashrate of the censor. The censored transaction can then eventually be mined and included in the chain. If the censor persevers in their strategy, they will not be producing the longest chain, and thefore will not be able to censor transations. They can then either stop the attack, or carry on with a slightly different statégy, where they refuse to add "illicit" transactions into their own blocks but still build on top of other blocks that do.

In PoS, once the censor as gathered the majority of the token, it is impossible to overtake them without changing the rules of the protocol. Indeed, because the means of block production are the tokens, and said tokens can only be produced by creating new blocks, the censor is the only one able to create new tokens and stake them. We'll see in a next paragraph how the Ethereum community seems to be willing to overcome this fragility, but for now what is important to understant is that **because Proof of Work uses an extragenous resource (energy) as the mean for block production, a PoW network can eventually overcome a censor ; whereas because PoS uses an intragenous resouces (tokens), a PoS network is inherently doomed once an entity has gather enough tokens**.

[^1]: In PoW, bigger means "with more work". In PoS, it means "with the higher number of blocks". The disctinction will be very important in a later part of this article.
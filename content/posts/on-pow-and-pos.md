---
title: "No, Proof of Work Is Not Some \"Costly Mistake\""
date: 2022-03-30T09:55:00+02:00
block: "729667"
cover:
    image: "../images/nuns_at_work-min.jpg"
    alt: "Nuns at work painting by a follower of Alessandro Magnasco"
    caption: "Nuns at work - Follower of Alessandro Magnasco <br> Open Access - MET Museum."
    relative: false
paybuttonlink: "https://donate.fanismichalakis.fr/api/v1/invoices?storeId=EqjDottuNfgWVwvJPnmMGTdHnqhFJeadqyQ9WiTaqok1&orderId=onpowandpos&checkoutDesc=test&price=1000&currency=SATS"
tags: ["bitcoin"]
categories: ["articles"]
draft: false
---

The desire to write this article came to me from the recent publication of two papers[^1] by {{<newtabref href="https://lejournal.cnrs.fr/auteurs/jean-paul-delahaye" title="Pr. Jean-Paul Delahaye">}}, professor emeritus at the University of Lille 1 and researcher at the Centre de recherche en informatique, signal et automatique of Lille (CNRS/Centrale Lille Institut/University of Lille). However, I hesitated for a long time before deciding to do it. Indeed, I had the impression that counter-arguments to those of Pr. Delahaye already existed in profusion, freely accessible for those who would take the trouble to look for them. So I felt I had little to add to the debate. Moreover, since Pr. Delahaye comes from the world of academics and research, I was afraid that my answer, although genuine, could be interpreted as just another opposition between the two spheres, unfortunately so little overlapping these days, that are the academic world and the Bitcoin community[^2]. My name, in fact, is not that of an eminent CNRS researcher.

This is not an anti-academic rant or, it seems to me, the verbatim of a blind Bitcoiner. This is an honest and well-reasoned answer to the opinion developed by Pr. Delahaye, whose texts I found rather well constructed[^3]. This text is intended to be even more general in scope, even if it takes that opinion as its basis and foundation. It is intended as a reminder of the usefulness of Bitcoin and its Proof of Work.

I will not respond in detail to each of Pr. Delahaye's arguments one by one, because I feel that I have found the crux of our differences of opinion, and so it is this crux that I want to address first. After a short preamble, necessary for the use of common definitions, I will explain why Proof of Work and Proof of Stake are not comparable. This will at the same time address many of the points developed by Pr. Delahaye, which stem from this misunderstanding. For the remaining points, I will address them at the end of the article.

## Preamble

Before going any further, it is useful to set out some definitions and recall some established facts. This preamble is thus composed of two sub-sections: the first one briefly recalls the difference between validation and confirmation of transactions within a distributed network; the second one defines the terms Proof of Work and Proof of Stake.

### Validation & Confirmation

The Bitcoin network is composed of machines, called "nodes", which can perform different functions depending on their type:
- full nodes store the entire ledger. When a new block is proposed, they verify its validity, which includes making sure that all the transactions it contains are valid (i.e. that they follow the protocol rules), that the block is properly formed, and that the associated proof of work is also valid,
- the miners gather the pending transactions into blocks that they attempt to have accepted by the entire network. Each miner works on a block, which may be different (i.e., contain different transactions) from that of his neighbor. To be able to propose his block to the rest of the network, a miner must be the first (among all the miners) to find a number satisfying a specific condition. Without going into the technical details, it is enough to imagine that this mechanism is very similar to a lottery: the only way to find this number is to try many of them, at random, hoping to find the right one. It is precisely this process that consumes large amounts of energy when thousands of miners are engaged in it.

Once a miner has found a number that satisfies the condition, he adds it to his block and publishes it. All other nodes (miners or full nodes) then check the validity of the number. In particular, if the number found satisfies the required condition, it is the proof that the miner has spent energy to find it: the famous proof of work. From then on (and provided that everything else in the block is also valid), all nodes accept this block as the new page of the registry and add it to their own local version. Then the miners resume work on a new block.

It may be interesting to note, and Pr. Delahaye does so, that the validation process itself is very fast and energy efficient. It is the process of selecting the next miner authorized to propose his block that is energy intensive. However, the term "validators" is often used to refer to miners or their "equivalent" in Proof-of-Stake blockchains. Of course, miners validate transactions before adding them to their block, but only to protect themselves from adding some transaction that is illegal with respect to the rules of the protocol, which would cause their block to be rejected if they were lucky enough to win the lottery. The validation of transactions does not distinguish miners from other nodes, nor does it distinguish their Proof of Stake counterpart from the complete nodes of PoS[^4] networks.

Now, when a transaction is added to a block and that block is accepted, it is customary to say that it has been confirmed; or that it has "received confirmation". Then, each block that is added in the chain above that block adds to the transaction an additional confirmation. Thus, because it is a name that seems consistent, and which does emphasize the distinctive role of miners and their Proof-of-Stake counterparts, we will refer to the nodes responsible for creating and publishing new blocks as "confirmers" (or simply "miners" in the case of Bitcoin and Proof-of-Work blockchains).

### Work and Stake

The difference between Proof of Work and Proof of Stake lies primarily in the criteria for selecting the confirmer adding the next block.

- In Proof of Work, it is the miner who first finds a number that satisfies the required condition. Since the only way to do this is to try as many numbers as possible until you find one, the chances of a miner winning the race are proportional to its computing power.
- In Proof of Stake, it is a randomly selected confirmer from the set of confirmers. However, there is not one ticket per confirmer: the probability of a confirmer being drawn is proportional to the number of cryptocurrency tokens he has pledged.

## PoW and PoS are not comparable

Pr. Delahaye's main argument is that, since the Proof of Work (PoW) and the Proof of Stake (PoS) reach the same result, it is moral to prefer the second one, which is more energy-efficient, to the first one. Presented this way, the statement seems not very debatable. However, PoW and PoS are not so easily comparable, as they do not fulfill the same objectives and do not exhibit the same properties.

### Protection against Sybil attacks

The common role of Proof of Work and Proof of Stake is to protect the network from Sybil attacks. A Sybil attack consists of a malicious actor running many nodes in order to simulate a multitude of different actors and take advantage of them. For example, imagine that the probability of a confirmer being chosen is not proportional to its computational power or its pledged wealth, but that each confirmer has the same chance as all the others. For example, each confirmer has a lottery ticket, and a winner is drawn at random. Since the marginal cost of setting up a new node is small (and decreasing), malicious actors could run thousands of nodes, getting thousands of times more chances to be selected. This is why pure randomness, without any other consideration, is not a good tool against the Sybil threat. Hence the usefulness of Proof of Work and Stake.

Pr. Delahaye, and it is there an essential element of his thesis, claims that the Proof of Work and the Proof of Stake manage as well one as the other to ensure the protection against the Sybil attacks. We will admit this point for the moment, before discussing it further later in this article. Indeed, there is a much more crucial aspect that needs to be raised.

What Pr. Delahaye also says, albeit implicitly, is that the only function of PoW and PoS is protection against Sybil attacks. While this is true in a first approximation, it ignores certain effects that follow from good protection against Sybil, and on which PoW and PoS are not equivalent.

### Censorship Resistance

One such effect, of monumental importance, is censorship resistance. This term refers to the ability of a network to sustainably resist an arbitrary takeover that would censor or filter certain transactions. This decision-making power is already held by certain entities (state or private) within traditional, centralized payment systems. It is crucial for distributed networks that whoever succeeds in grasping this power for a certain period of time, is quickly removed from it. In other words, these networks must be resilient, and if an attacker were to gain a position in the network that would allow him to censor transactions in practice, it should be impossible for htem to maintain their position. However, as Eric Voskuil demonstrated in his {{<newtabref href="https://github.com/libbitcoin/libbitcoin-system/wiki/Proof-of-Stake-Fallacy" title="Proof of Stake Fallacy">}}:

{{<blockquote>}}
Censorship resistance depends on people paying miners to overpower the censor. Overcoming censorship is not possible in a PoS system, as the censor has acquired majority stake and cannot be unseated. As such PoS systems are not censorship-resistant and the theory is therefore invalid.
{{</blockquote>}}

Once an actor has amassed enough wealth to be assured of being chosen so often to offer his block that he is able to censor transactions, there is no going back: he will not give up cryptocurrency units to others; and the only way to get new ones, via confirmation rewards, he has appropriated for himself alone.

This is in stark contrast to Proof of Work, where such a tyrant can be overthrown by plugging in new machines. The only way for the attacker to maintain themselves would be to further increase their computing power (and thus their power consumption). In the long run, they would be forced to invest in new machines, new energy infrastructure, etc. Because the parameter determining the probability of offering the next block is exogenous and expensive, the network is protected from censorship.

Moreover, Pr. Delahaye himself points this out very well, believing he has an argument against Proof of Work:

{{<blockquote>}}
The POW is a POS that confiscates bids! (...) The POS does as well as the POW (fighting Sybil attacks) without forcing a validator to a large expense.
{{</blockquote>}}

What Pr. Delahaye takes to be a flaw (the forfeiture of bids and the subsequent cost to the confirmer) is actually one of the key elements to making Bitcoin censorship-resistant. Without this ongoing cost expressed in an external unit (energy), the censor can maintain itself indefinitely. With the external cost (in energy and investment), the censor can be overturned at any time.[^5]

A relevant question to ask at this point is whether Proof of Stake has another mechanism enabling censorship-resistance. Surprisingly, the answer is no. Some argue that as an actor buys cryptocurrency units in the market to build up capital to control a significant portion of the currency, the price rises accordingly, making it difficult, if not impossible. I fear that this is unfortunately a misjudgment of the threat model. An actor wishing to censor a distributed network would in all likelihood have tools at his disposal that would allow them to acquire the required amounts at a reasonable cost: seizures or injunctions to the large platforms that do not fail to form in Proof-of-Stake environments, money printing, etc.

### Conclusion

The main mistake that Pr. Delahaye makes is to consider PoW and PoS only through the prism of protection against Sybil attacks. However, as we have shown, this framework of analysis is too reductive. Censorship resistance is the fundamental property of Bitcoin, necessary for the expression of its other properties. It is therefore non-negotiable, and only Proof of Work can ensure its existence and conservation today. This is its primary use.

Bitcoin's detractors may argue that such a censorship-resistant system is not necessary, or even desirable. This is an opinion they can have and defend, but it remains an opinion. Similarly, my belief that such a system is absolutely necessary for a free society remains an opinion (though one that I believe is increasingly supported, as recent events in Canada, for example, have shown).

The debate about the usefulness of Bitcoin and its Proof of Work is therefore a philosophical discussion about the kind of society one wants to live in. It is not the technical controversy to which Pr. Delahaye wanted to reduce it, as I believe this first part has just demonstrated.

{{<paybutton text=" 💪 Support my Work " color="#1da1f2">}}

## Other considerations

In this second part, I will attempt to deal with the points raised by Pr. Delahaye that are not already addressed in the first part. This treatment is not intended to be exhaustive, and I refer the reader to the table in the appendix to this article if he or she wishes to have a quick overview, point by point, of the counter-arguments made to Pr. Delahaye's assertions.

### Decentralization

Anyone who has ever looked at Bitcoin's mining process has noticed a certain concentration of computing power in just a few mining pools. This was generally expressed by the idiomatic "everything is centralized in a few miners in China" that some people repeated over and over again before the Exodus.

This remark calls for two comments: the first concerning the meaning to be placed behind the notion of *decentralization*; the second concerning the nature of the above-mentioned mining cooperatives.

The notion of decentralization in distributed money networks is not easy to grasp, and it is easy to misunderstand. What exactly are we seeking to decentralize? One possible answer is that we are looking to decentralize the executive power of transaction ordering. Indeed, in the Bitcoin whitepaper, Satoshi Nakamoto writes that the Proof of Work allows for the establishment of a peer-to-peer *distributed timestamp server*. This distributed server replaces the traditional centralized servers that were used until now and that acted as a source of truth regarding the order of transactions.

If we consider decentralization through this single prism, then the centralization of mining among a few cooperatives can be a legitimate source of concern. A mining cooperative is the result of several miners coordinating to work together and share any rewards they may earn, in order to gain certain benefits such as reduced variance in earnings or the {{<newtabref href="https://github.com/libbitcoin/libbitcoin-system/wiki/Proximity-Premium-Flaw" title="Proximity Premium">}}. Such a cooperative typically operates with a coordinator who distributes work and rewards to members. However, even if miners are, in theory, individually free to change cooperatives at any time, or even to mine alone, it is not obvious that they would make this choice, even in the case of a takeover of the cooperative by an entity, if their economic interest is to remain there[^6].

A crude analysis may lead one to believe that Proof of Stake is exempt from this concentration problem, and that it is therefore more decentralized than the Proof of Work. This pitfall is related to a misjudgment of the reasons why miners associate in cooperatives. I have already mentioned two of these reasons (reduction of variance and proximity premium), to which we can add, for example, possible economies of scale, or greater resilience to market variations. However, all these reasons are still present in a Proof of Stake system. Even worse, new concentration pressures (i.e. new reasons to form cooperatives) may arise in the latter, such as when a minimum amount is required to participate in transaction confirmation, prompting small holders to federate to exceed this limit.

The concentration pressures do not differ between Proof of Work and Proof of Stake in their nature, but (possibly) in their degree. It is thus admissible that economies of scale are less important in a PoS system than in a PoW system, although this depends strongly on the minimal characteristics required to operate a confirmer node in a given PoS system.

Moreover, it can be argued that the incentive structure of Proof of Stake makes confiscation, and thus takeover, easier. Indeed, the same concentration pressures that drive some participants to pool their tokens in a PoS system also drive them to entrust these tokens to trusted intermediaries, such as exchange platforms for example, in order to benefit from better returns (often due to lower fees). This is evidenced by the distribution of Ethereum 2.0 validators (under test), with nearly 10% of staked ethers being stored by a single platform (Kraken). [^7].

While it is not certain that miners would leave their cooperative if it became hostile to a certain conception of the general interest, it would be much easier for them to do so than for their Proof of Stake counterparts who had deposited their funds with a third party. Indeed, all the miners would have to do is redirect their computing power elsewhere - a simple configuration change on their machine - while the token holders would be firmly told that withdrawals are suspended.

Thus, if we judge that Proof of Work presents a significant risk of centralization because of the pressures of concentration that are exerted there, we must rigorously apply the same reasoning to Proof of Stake, to see that the same pressures exist there, and that their effects are potentially harder to moderate.

### Environmental and societal impact

The other criticism so often levelled at Proof of Work is its environmental impact. A detailed response would certainly be the subject of a full article, or even a meta-article. A more condensed answer can be found in a few considerations:

1. All human activity has an environmental and societal impact. When you take the bus. When you brush your teeth. When you watch Netflix while waiting for the clothes dryer to finish. This impact must always be weighed against the benefits of the activity.

2. Bitcoin's utility is to provide an open, permissionless, fair and censorship-resistant monetary and payment protocol.

3. Bitcoin's consumption is often compared to that of a country like Sweden. To keep in mind an equally meaningless order of magnitude, it is amusing to note that this corresponds, for example, to the annual consumption of one third of the clothes dryers in the United States.

If the reader agrees with proposition 1., the question is whether he recognizes that proposition 2. justifies the energy consumption presented in 3. To fuel this reflection, I advise the reader the excellent {{<newtabref href="https://medium.com/@AlexStach/manual-of-survival-in-the-jungle-of-poncifs-anti-bitcoin-long-version-523e381745ff" title="manual-of-survival">}} written by Alexander Stachtchenko (in French). Once again, this is a philosophical and ethical reflection, both personal and a real social debate. In no case a purely technical question, as we had already underlined in conclusion of the first part.

Finally, there is a real question to be asked about the alleged environmental safety of Proof of Stake protocols. This will surely be the subject of a future article, but in view of the multiplication of these projects, some of them of dubious ethics, during the recent market euphoria, the question of a possible "Rebound Effect" arises.

## Appendix - Summary Table

This table allows the reader who would like to weigh Pr. Delahaye's arguments to find, for each argument, numbered according to Pr. Delahaye's nomenclature, my possible observations. My hope is that these remarks will enrich the debate and provide food for thought for everyone.

| Argument | Summary | Observations |
|--|------------|------------|
|A | Pow and PoS do the same thing, but PoS does it in a more economical/ecological way	 | Already addresses in the first [part](#pow-and-pos-are-not-comparable). |
|B1|Mining prompts electricity theft|Stealing electricity is indeed reprehensible, no matter what use is made of that energy afterwards. As it did with *ransomware*, although to a lesser extent Bitcoin makes it easier to make a profit from an activity that existed before it anyway. So it's just a matter of criminals adopting better tools, which it would be pointless to make illegal, since criminals, by definition, are already acting illegally. So the solution is not to ban Bitcoin or PoW, but to strengthen the security of the electricity supply, just as the IT world has become aware of the cyber threat.|
|B2|Mining encourages the theft of computing power|Same answer as for B1.|
|B3|"POW contributes to the shortage of electronic components" |No more so than other industries. Again, it is a matter of understanding the utility of PoW, highlighted in Part 1. Moreover, it should be noted that, contrary to what Pr. Delahaye says, many PoS networks require powerful, dedicated machines for the confirming nodes[^8].|
|B4|"Validators have to sell part of their earnings to pay the costs of mining," which negatively influences the price by creating selling pressure.|Buying pressure is more than enough to absorb these sales, when they occur. Moreover, the dynamics in this regard seem to have changed considerably, with miners selling less and less mined bitcoins now that they have access to other sources of funding. Argument not supported by facts.|
|B5|As the price rises, mining Bitcoin becomes more profitable (apart from *halving*) and the total computing power of the network increases accordingly. But since this is only possible to a certain extent, the growth of the Bitcoin price is limited.|Yes. It does not seem absurd to me that money, in a finite world, is constrained by the physics of that world. This is unfortunately a reality from which fiat currencies have distanced us.|
|B6|PoW, by focusing attention on the 51% attack, tends to hide the other risks.|Subjective and not established by facts.|
|C1|Just because Bitcoin mining uses renewable energy doesn't mean it doesn't pollute.|Correct, all energy produced is pollution, to be weighed against its benefits. It should also be noted that Bitcoin also uses an increasing amount of wasted energy, which costs nothing to consume, economically or environmentally speaking.|
|C2|Some players are turning away from PoW in favor of PoS, because of the pollution generated by the former.| *Ad verecundiam* fallacy.|
|C3|Mining may have created power outages.|It is quite possible that mining is involved in certain disorders on electrical networks. However, mining can also be very useful in stabilizing the latter. Hence the importance of dialogue and joint work between energy producers and miners, as for any electro-intensive industry.|
|C4|"Mining plants create unrest in their immediate environment."|Some of the examples cited here have been debunked. For example, Pr. Delahaye indicates that certain installations have led to "heating the water of certain lakes in the United States", pointing to an article in the Figaro newspaper which states that the water of the lake in question has remained at seasonal norms. Which a simple reasoning on the orders of magnitude could have taught us.|
|C5|In some areas, mining may have led to higher prices.|Unfortunately, this argument is supported by only one source. If true, the answer is similar to that in C3.|
|C6|PoS allows much better decentralization than PoW because it does not require the purchase of expensive machines.|This point deserves an answer in several phases. First, the decentralization of a network is measured not only by the decentralization of its confirming nodes, but also by that of its validating nodes. The figure of 15,000 Bitcoin nodes presented by Pr. Delahaye refers to a subset of the validator nodes, not to the confirming nodes (improperly referred to as "validators" by Pr. Delahaye). The actual number of Bitcoin validator nodes is estimated to be over 15,000, making Bitcoin by far the most decentralized network. Moreover, it is abusive to claim that PoS allows for greater decentralization of confirming nodes, especially when one considers, depending on the network, the amount of funds to be pledged or the characteristics of the required hardware.|
|D1|The equivalent of billions of dollars are on PoS networks like Solana or Cardano, proving their security. |In times of market euphoria, the capitalization achieved by some projects does not allow one to deduce anything about their technical underpinning. Moreover, in many of these projects, a good part of the money supply is under the control of a few entities closely or remotely linked to the development team. Finally, new research papers regularly highlight flaws in leading PoS protocols[^9].|
|D2|"New blockchains never use PoW"|Not factual and not demonstrating anything. PoS is to this market cycle what ICOs were to the previous one: a simple way to distribute an initially worthless token, and to generate an ersatz network effect at low cost.|
|D3|Ethereum will move to PoS.|*Ad verecundiam* fallacy. And skeptics will also be allowed to doubt whether Ethereum will move to Proof of Stake in 2022.|
|E1|Some PoW proponents would claim that, "The massive electrical expenditure of the POW secures against 51% attacks and therefore provides perfect protection in the case of the Bitcoin network."|I have never heard anyone say that.|
|E2|Some PoW proponents would argue that: "It is normal for security to have a cost. The lack of such a significant cost for securing POS networks shows that they are less well protected than POW networks."|I have heard or read sophistries similar to this one. Pr. Delahaye is right to point it out. But this is not an argument in favor of PoS, nor even against PoW... This is bordering on an *ad auditores* fallacy. I do not insist!|
|E3|The PoW may use surplus electricity, but it is not virtuous because all energy produced is polluting. It would be better to do away with surpluses. |I agree with Pr. Delahaye that in a perfect world, there would be no electrical surplus, energy would be available at the right time, in the right place and in the right quantity. However, in practice, it is necessary to deal with physics, and therefore very often to oversize facilities to cope with peaks in consumption, or because we anticipate a population increase, etc. It is also important not to project the French or European power grid as a universal truth: many grids around the world benefit from the stabilizing effect of the controllable demand of Bitcoin miners.|

\
Found this article interesting? Share it! And if you feel so inclined, don't hesitate to toss a coin in the hat.

{{<paybutton text=" 🎩 Hats Off! " color="#1da1f2">}}

[^1]: This long {{<newtabref href="https://institut-rousseau.fr/les-arguments-en-faveur-de-la-preuve-denjeu-pos-et-contre-la-preuve-de-travail-pow-pour-les-chaines-de-bloc/" title="paper">}} (in French) published by the Institut Rousseau, and this  {{<newtabref href="https://lejournal.cnrs.fr/billets/le-reseau-bitcoin-une-erreur-follement-couteuse" title="opinion piece">}} (in French too) published in Libération and the CNRS Journal.

[^2]: If the reader finds this subject interesting, I recommend giving the analysis formalized by Phylisophy Professor {{<newtabref href="https://twitter.com/thetrocro" title="Troy Cross">}} in {{<newtabref href="https://anchor.fm/daniel-prince6/episodes/thetrocro---A-Philosopher-Talks-Bitcoin--234-e1ec98b" title="Daniel Prince">}}'s podcast.

[^3]: In any case, they show a good understanding of the technical functioning of Proof of Work, although some of the arguments seem questionable to me, while others do not add anything to the debate.

[^4]: If they exist.

[^5]: It is quite possible that it will be difficult to override the computational power of the censor, if it is very large. The crucial point to understand here is that, in a PoS system, once the censor is in place, it is impossible to oust **in theory and in practice** while keeping the pre-existing consensus rules intact, because it receives all the new tokens that players wishing to overthrow it would need to override it. With PoW, the censor may receive the block rewards as well, but this is of no use to him to maintain his power since the cost taken into account in the allocation of chances to confirm a block (energy) is external to the system.

[^6]: See {{<newtabref href="https://github.com/libbitcoin/libbitcoin-system/wiki/Cockroach-Fallacy" title="Cockroach Fallacy">}}.

[^7]: It is also worth noting that a significant part of the money supply remains concentrated among a few players, while the part of the money supply represented by premined ethers still represents more than 50% of the total. An advantage that, while benign in a PoW system, suddenly takes on a very different light in a PoS network.

[^8]: See for example Solana's {{<newtabref href="https://docs.solana.com/running-validator/validator-reqs" title="documentation">}}.

[^9]: See for example the latest {{<newtabref href="https://arxiv.org/abs/2203.01315" title="paper">}}, published in the beginning of March 2022.
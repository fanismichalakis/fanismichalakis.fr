---
title: "Chainalysis to Launch Lightning Network Support"
date: 2021-12-10T22:40:13+01:00
tags: ["lightning", "bitcoin"]
categories: ["logs"]
draft: false
---

Chainalysis {{< newtabref  href="https://blog.chainalysis.com/reports/lightning-network-support/" title="announced" >}}  today that they are going to lauch support for Lightning Network transaction monitoring. This new feature would be integrated into KYT (Know Your Transaction), one of the main products of Chainalysis that supposedly helps businesses and services stay in line with regulation by providing them with transaction monitoring and traceability tools.

In its blog post, the company didn't detail how they plan on monitoring transactions on the Lightning Network. One can only suppose it would be a combination of both on-chain data monitoring, channels probing and acting as a payment hub to try to get their hands on some data. 

The first one (on-chain data) can give them interesting results, but nothing more that what was highlighted by Anthony Ronning[^1] and Bastien Teinturier[^2][^3] in their articles on Lightning Privacy. The one example the firm gives in their blog post is actually quite revealing in my opinion of the limited knowledge on-chain analysis can bring regarding what is happening on Lightning (regarding actual Lightning transactions)[^4].

The second and third methods (probing and acting as a hub) both require other nodes in the Lightning Network to actually open channels with Chainalysis nodes. Although I think no sensible human being would ever do this on purpose, it could be achieved either via deceit or coercion:
- there are tons of big hubs on Lightning that nobody really knows who is behind. LNBIG is one good example of that,
- regulators could force companies accepting Lightning payment to have channels only with Chainalysis nodes. This way, Chainalysis would act as a *de facto* payment processor really similar to Visa or Mastercard.

I am not so worried about the latter. But the hub one is definitely a bit scary. If hubs appear that are so big and well connected that the hub owner can consider with a certain level of confidence that, for any payment, the previous hop is the actual sender of the payment and the next hop the actual recipient, then they can in fact have a pretty good understanding of where payments flow, at least locally. But the existing hubs today are nowhere near this stage in my opinion, and there are tons of ways through which we can circumvent that. Yes, moar decentralization.

## Final thoughts

Seems like the Lightning Network is so little used that Chainalysis can't help but add it to its monitored networks.

[^1]: {{< newtabref  href="https://abytesjourney.com/lightning-privacy/" title="Anthony's not so recent but still very accurate article" >}} 

[^2]: {{< newtabref  href="https://github.com/t-bast/lightning-docs/blob/master/lightning-privacy.md" title="Bastien's very recent and very accurate article" >}} 

[^3]: {{< newtabref  href="https://bitcointv.com/w/2pXyaypeMThT5tM3MUWcgN" title="Bastien's presentation on Lightning Privacy at Adopting Bitcoin in El Salvador" >}}. Did I mention how recent and accurate it is? 

[^4]: The example they give is being able to tell (with a good probability) wether a channel was actually used or not by seeing if the channel close transaction has one or two outputs.

---
title: "Bitwage Announces First Salary Paid Through Lightning"
date: 2021-12-07T20:21:36+01:00
tags: ["lightning", "bitcoin"]
categories: ["logs"]
draft: false
---

Bitwage announced today that it conducted the first ever salary payment over the Lightning Network.

{{< tweet user="Bitwage" id="1467874344026230799" >}}

I personnaly found the news quite interesting, because the idea of getting paid, not only in Bitcoin, but also on the Lightning Network, opens for some *intriguing* considerations.

Getting paid in Bitcoin is nice. It's catchy, fun to say at family meetings, and protects against inflation and censorship. It may have its (short term) drawbacks, especially when everything around you is still priced in good ol' FED bucks. But it's nice.

Now, as more and more people start getting paid in Bitcoin, we might start to see a bit of a traffic on the Bitcoin chain at the end of the month. Every company sends its employees their salary pretty much at the same time, be it monthly or weekly. Queue, delay, overloaded mempool. Bad. The sole idea of having to wait for the mempool to clear to be able to receive your salary is *weird*. Enters Lightning.

With Lightning, you can receive your salary off-chain and independtly of the chain conditions (eg, wether the mempool is crowded or not) as long as there's a route between you and your employer, and that this route has enough liquidity in the right direction (eg, flowing from your employer to you).

Moreover, we can even imagine using the same channel each month, over and over again:
1. Employee receives salary. After this, the inbound capacity of their channel is deplenished: they can't receive much.
2. Employee pays expenses throughout the month. Each spend takes from the outbound capacity (what they can send) and pushes to the inbound capacity of the channel (what they can receive). Therefore, with each spend, the employee's ability to receive increases.

This way, it would **theoretically** be possible to use Bitcoin over Lightning without ever touching the chain again, receiving one's salary with the same channel every month, and spending from this same channel during the month. It works as long as there's enough inbound capacity every month for the salary to be paid[^1]. For example, if the employee spends exactly what they receive each month, this can work endlessly.

Now, two things come to my mind:
- this doesn't leave much space for savings, and we love savings
- what about the fees?

Regarding savings, there are several possibilities.

For example, the channel the employee uses to receive their salary could be big enough so that it takes ten years for the inbound capacity to be totally drained, given the employee's saving habits. But it sounds like a pretty inefficient capital allocation.

Or liquidity could ne *naturally* driven to the inbound via routing.

Or the employee could use some *Lightning <--> on-chain atomic swap* to save in Bitcoin while keeping enough inbound liquidity to get their next salary:
1. Employee receives salary.
2. Employee spends part of the salary to pay for expenses.
3. Employee sends the remnant to a swap service and receives on-chain BTC for long-term savings in exchange. This way, the liquidity in the channel will be on the good side to receive the next salary.

Bitcoin over Lightning salaries could even be a significant moving force in the emergence of P2P swap services and marketplaces, where users with excess funds on Lightning willing to exchange them for on-chain funds (the savers) would trade with users wishing to increase their Lightning Network bandwith (the spenders).

Finally, another interesting aspect in getting paid in Lightning is that it has the potential to redefine the timesccale at which it occurs. Why wait a whole month to receive your salary? Why not every day? Or every hour? With Lightning, we can do this without the risk of overcrowding the blockchain. And if the payment flows in a direct channel between the employer and the employee[^2], it comes at no additional cost (apart from admnistrative costs).

If I had to make a guess, I'd say we've barely scratched the surface of what getting paid over Lightning implies, both in terms of innovation and challenges.

[^1]: Of course, everything gets more complicated when there're additionnal hops between the employer and the employee, has each hop must also have its liquidity well-positioned for this to work.

[^2]: Is this a good idea? It would mean zero fees, but it would also mean the employee would have to go through the employer's node to spends their salary.
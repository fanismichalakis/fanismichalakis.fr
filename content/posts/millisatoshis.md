---
title: "Millisatoshis"
date: 2021-12-16T15:59:38+01:00
tags: ["lightning", "bitcoin"]
categories: ["logs"]
draft: false
---

Today's post was inspired by this very good question from {{< newtabref href="https://twitter.com/antwar" title="@antward">}} on Twitter:

{{< tweet user="antward" id="1471242670777511942" >}}

As you can see, I tried to give him a synthetic answer, but then {{< newtabref  href="https://www.youtube.com/watch?v=CWzrABouyeE&t=27s" title="I thought to myself" >}}: why not devote today's short piece to this question? So here we are.

## 1 millisat = 0.001 sat

That's the shortest answer one could give. 1 millisatoshi equals 0.001 satoshi, in the same way that a millimeter is 0.001 meter. So 1 bitcoin is 100 million sats, and one sat is 1000 millisats, which means that 1 bitcoin is 100 billion millisats.

```md
100,000,000.000
^         ^   ^
|         |   |
bitcoin   sat millisat
```

## So the satoshi isn't the smallest Bitcoin unit?

Yes and no.

The Bitcoin protocol (and hence the Bitcoin network) considers coins as integers. We call them "satohis" *in memoriam* of Satoshi Nakamoto, but in the source code they are referred to as coins. Alice may say she has 6.15 bitcoins, but what the code would say if it could speak is that Alice has six hundred and fifteen million (615,000,000) coins. And when it comes to coins, the Bitcoin protocol doesn't know what decimals are. That's why we say the satoshi is the smallest accounting unit of Bitcoin.

Now, it doesn't mean we can't come with a subunit of our own and use it for our accounting. Take gas prices in gas stations for example. They usually display 3 decimals, even though you end up paying with a precision of only two decimals. That's because it is useful to account for the price of the gallon of gas with three decimal places, because decimals add up as you fill your tank.

The same goes for millisatoshis. They are a useful unit of account. We use them on the Lightning Network because it allows us to do very small transactions[^1], and because there is no real reason not to do it.

## What happens when I close my channel?

One of the great things about the Lightning Network is that it is backed by the real Bitcoin network. You can always close your channels and get you funds back on-chain. But what about those millisatoshis that aren't recognized by the Bitcoin protocol?

Upon closure, the amount of funds you own in a channel is rounded to the nearest satoshi. Got 100,011.430 sats? That's 100,011 sats when you go back on-chain. Where did the 430 millisats go? They were simply pocketed by your peer on this channel, because his amount was something like 36500.570 sats, which is rounded up to 36501 sats in the channel closing transaction[^2].

## What about bits?

There are still people claiming that satoshis are too small in value today, and that another unit makes more sense : the bit. 1 bit is equal to 100 sats. This way, 1 bitcoin is 1 million bits. And one sat is 0.01 bit. They also claim it's nice and good looking because we are accustomed to prices with tho decimal places with the fiat system.

```md
1,000,000.00
^       ^  ^
|       |  |
bitcoin bit sat
```

To be honest, I kinda like the idea behind bits. I don't consider myself as a bit supporter, but I must confess I do find the bit-based representation clearer. And yet, it is undeniable that the sats gang won. They had the upper ground, and their unit denomination was backed by the fact that, at the protocol level, sats are equivalent to coins and therefore the smallest unit of account on Bitcoin.

But sats supporters were (and are) wrong too.

**For years, the right choice has always been to stop this nonsense, and finally call the smallest fraction of money on the Bitcoin network a bitcoin.**

[^1]: Even if it's quite rare to see transactions below 1 satoshi, the millisatoshi is still super useful to calculate network fees. For example, if you were to route a 1000 sats payment through a node that has a zero base fee and a 1 ppm (0.0001%) feerate, the fees charged by this node would be equal to 0.001 satoshis, or 1 millisatoshi.
Also notice that if the amount was below that, the collected fee would drop below 1 millisatoshi and therefore be rounded to zero! That's right, a small amount, no base fee and a small feerate mean zero fee. Literally.

[^2]: Notice how no satoshi was created nor destroyed in the process.
---
title: "Bitcoin and Mesh Networking"
date: 2021-12-17T21:53:31+01:00
tags: ["bitcoin", "mesh"]
categories: ["logs"]
draft: false
---

I am increasingly convinced that the future of Bitcoin (at least, its short term future) lies in mesh networking.

## Intro

Mesh networks are networks were nodes connect to one another dynamically and without any hierarchy. There is no central authority, every node is connected to other nodes with which it exchanges data.

Bitcoin already looks a lot like a mesh network at the protocol level. Consider transactions or blocks propagation for example. When a node becomes aware of a new transaction or a new block, it transmits this information to its neighbors, which in turn pass it along to their neighbors, and so on. This way, information quicly reaches the whole network.

But at the transport level, Bitcoin still largely relies, in practice, on a non-mesh TCP/IP layer[^1]. I believe that, as the pushback against Bitcoin increases in some jurisdictions, Bitcoin related traffic might start being censored. At least, in any adversarial thinking oriented planning of the future, this is a possibility that should be accounted for by any rationnal Bitcoiner.

There are a few ways bitcoiners can circumvent that. Here are three I thought about, feel free to reach out if you see others that might play out:
- create Bitcoin-friendly ISPs ("ISP for Bitcoiners, by Bitcoiners"),
- build mesh networks between Bitcoiners homes,
- satellite communications for long-distance data transfers.

In my opinion, the best solution is a combination of the three. A Bitcoin-friendly ISP could be able to delay the application of anti-Bitcoin laws and regulations, at least to some extent. When this bastion falls, a mesh network comprised of hundreds of antennas should be able to ensure a stable communication between nodes that are geographically close to one another. This works especially well for cities, but could be a bit more challenging in the countryside. Finally, satellite communication would allow Bitcoiners living in an anti-Bitcoin country to reach their peers outside of this jurisdiction.

## An example

I always like to give this example when trying to explain how I see mesh networking and Bitcoin working together.

{{< tweet user="Marketsbylili" id="1413185925128069121" >}}

It doesn't fully encapsulates what I have in mind, because in this example mesh is used ponctually to route a transaction to the closest node with internet access, whereas I envision a stable mesh network. But it's defintely a good place to start.

## Plan ahead

Of course, Bitcoiners should not wait for the moment they need them to start building mesh networks. There are some initiatives such as {{< newtabref href="https://txtenna.com/" title="TxTenna">}} or {{< newtabref href="https://locha.io/" title="Locha Mesh">}}, but we're not there yet. Maybe we should.

[^1]: Although TCP/IP doesn't care how data packets are communicated, non-mesh networking is quite the standard todays, with centralized Internet Service Providers (ISP) giving access to the internet to their client. This is true for Bitcoin too: even if the communication between you and your peers is peer-to-peer at the Bitcoin protocol level, you often still rely on your ISP to send and receive data to and from your peers.
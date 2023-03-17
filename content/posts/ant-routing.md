---
title: "Ant Routing"
date: 2022-04-03T20:00:00+01:00
draft: true
---

In a previous article, we covered in length the inner workings of Onion Routing on the Lightning Network. As we outlined, Onion Routing enables a decent level of privacy for Lightning transactions by concealing the identities of the emitter and the recipient of a payment to the intermediary nodes that take part to its delivery. However, this scheme comes at cost, which consists mainly in inefficiencies, the (computationnal) complexity of pathfinding and the need for at least some part of the network's topology to be public (eg shared and stored).

In today's post, we will take a look at an alernative routing mechanism for the Lightning Network which completely takes par with the concept of *public network topology* that is so crucial for Onion Routing. This design would allow the network to scale without the (natural) apparition of concentration points acting as beacon nodes.

## The Onion Concentration Problem

In Onion Routing, the emitter of a payment is in charge of calculating the whole route between them and their recipient. Picture a railroad network: many train stations, interconnected through rail roads of various dimensions. Depending on its width, a railroad line will only be available to trains that do not exceed a certain span and weight. Bigger trains would have to go through a different, wider track, if such a track exists. As the administrator of a train station, your role is to find the best route for each train departing from your station.

To do so, you must be aware of where the railroad tracks are. Additionnaly, for each portion, you must know its width so that you only send trains of acceptable dimensions along them. But that's not all: the physics of our imaginary world is a bit messed up, and each time a train goes through a track in a given direction, it temporarily *weakens* the track, which cannot accept trains as big as its width would normaly allow, until the track is repaired or a train takes it in the other direction.

To be a good train station administrator, you must therefore have a detailed knowledge of the map of the network: where are the tracks and, for each track, what its width it. Ideally, you would also like to know when a train goes through a track, so that you can account for the temporary weakening of this specific line and avoid sending too heavy trains on there. But train companies value the privacy of their operations a lot, and there is no way they're sending this data to you[^1]. Your only alternative is therefore to guess what the state of a track is at a given moment, knowing that if a track's width originally allowed it to support 400 tons, it as more chances to be able to host your 200 tons train than if it could originally only handle 250 tons.

So not only do you have to keep a detailed map of the network and modify it every time a track is closed or a new one opens, but you must also often make educated guesses about which route is better for a given train, depending on its size. More than once will you send a train on an apparently practical road, only to discover after a few steps that the middle portion of the journey has been damaged and your train must reverse course to try another route altogether. The only ways for you to mitigate this are:
- to have a very good map of the network to begin with (the more tracks you are aware of, the better),
- to have a lot of train departing from your station, because each you send a train on a route that reveals itself to be infructuous, you at least learn some information about the state of weakness of a specific track at a given time, and can use this information to make even more educated guesses in the future.

And, of course, the more stations and tracks on the network, the harder it generally is to go from one arbitrary point to another. A bigger Lightning Network means a higher number of available channels. The size of the "map" of the network grows with the network, to the point that fewer and fewer nodes are able to store a detailed view of the network (and keep it up-to-date). But that would still be doable, if not for the very dynamic aspect of liquidity depletion (the track weakening) that forces you to make educated guesses all the time and favors nodes with a lot of traffic, such as Lightning Service Providers (LSP: wallets, Lightning-enabled platforms, etc.). This creates a concentration pressure around a few nodes that have a thoroug knowledge of the network and are well connected. Over time, these nodes tend to become *de facto* hubs of the network, and it is increasingly difficult to reach a destination without going through them, unless appropriate measures are adopted. These measures tend to go against the natural tendency of the network to concentrate around efficient nodes, which means it might not be a good idea to rely solely on them.

## Ants To The Rescue

Fortunately, there is a lot of research going on regarding how to mitigate the concentration pressures induced by Onion Routing. Some of them aim at making the pathfinding algorithm more efficient while keeping the Onion Routing design. For example, Rene Pickhardt's algorithm could greatly reduce the failure rate of payments, thus downsizing the benefits big entities get from their high transaction volume. Others try to remove the necessity of having to maintain big maps of the network, and therefore focus on novel payment routing mechanisms. Ant Routing, as the name indicates, is one of them.

As we saw, the big problem with today's Onion Routing is that you don't know for sure if a payment will be able to go through a certain route before you actually try it, because you don't know the exact repartion of liquidity inside a channel you don't belong to. Ant Routing's design flips this problem on its head. Instead of relying on a hardly up-to-date map, the nodes concerned with a payment (the sender and the receiver) propagate information about said payment to their neighbours, who will respond regarding the feasibility of the payment on their channels. With these fresh information, the sender can then choose a route that will work on the first attemp. And, icing on the cake: everything is done in a privacy preserving manner for the payer, the payee, and even the intermediary nodes, thanks to a mechanism inspired of ants' pheromone-based communication and path-marking.

### General idea

The general idea of how Ant Routing works can be summed up in a few sentences. Considering a given transaction, the first step is for the payer and the payee to agree on a pair of numbers called *pheromone seeds*, one for the payer and one for the payee, which are different but very similar (in a way that it is easily recognizable for anyone that they share the same root). Then, the payer sends his pheromone seed to all of his direct neighbours, while the payee does the same with their own pheromone seed.

Upon receiving a pheromone seed, each node keeps it in memory and sends it forward to all of its own neighbours. This way, some nodes in the network will eventually have received both pheromone seeds. When it happens, it means that there exist a path between the payer and the payee that goes through said node. This node then crafts a *matched pheromone* and sends it to the neighbour from which they received the pheromone seed. From node to node, *matched pheromones* make they way back to the emitter and the receiver. The emitter collects them and, once they have enough, can decide through which path they want to go and proceed with the actual payment.

### Down the Anthill

At this point, I belive it is useful to dive into some technical details, which will help the reader grasp the mechanism of Ant Routing. Let's take an example where Alice wants to send a 10,000 sats payment to Bob, and the network around them like this at the given time:

IMG

1. Alice and Bob agree on a random number R, big enough to avoid collisions.
2. Alice crafts her own number S(0), which is equal to R preceded by 0 (ie S(0) = 0⁀R, where ⁀ is the concatenation operator).
3. Bob crafts his own number S(1), which is equal to R preceded by 1 (ie S(1) = 1⁀R).

This way, Alice and Bob have different numbers, but it is trivial for anyone to link both numbers to the same root number R. S(0) and S(1) are called *pheromone seeds*.

4. Alice sends her number S(0) to all of her neighbors[^2]. Likewise, Bob sends S(1) to all of his neighbors.
5. Each of their neighbors then forwards the number they received to their own neighbours, and so on.
6. Eventually, some nodes will have received both numbers at some point. In our example, Cléante receives S(0) and S(1) in the figure number XX[^3]. This means that there exists a path between Alice and Bob and going through Cléante.
7. Upon receiving both numbers, Cléante crafts a pair of numbers M(0) and M(1) (called *matched seeds*), so that M(0) = 1⁀S(0) and M(1) = 0⁀S(1). Then, Cléante sends M(0) back in the direction from which he received S(0) (in our case, he therefore sends M(0) to Béline) and sends M(1) back in the direction from which he received S(1) (here, to Damis).
8. Béline proceeds to send M(0) in the direction from which she received S(0), and hence sends it to Alice. Likewise Damis sends M(1) in the direction from which he received S(1), and hence sends it to Bob.
9. Once she received M(0), Alice creates yet another number C = 0⁀M(0), called the *confirmed seed*, and sends it back to Béline. The *confirmed seed* C is sent from node to node until it reaches Bob, who then aknowledged reception by sending a p2p message to Alice. The path between them is now confirmed.
10. Alice sends the payment along the path, and nodes forward it as usual.

### But what about the amount?

The astute reader will have noticed that, according to what we've depicted, some useful details seem to be missing from the *pheromones* nodes send to each other. For instance, a given node needs to be aware of the amount of the payment, so that he only forwards the *pheromone seed* to his neighbours with which he has channels in which there is enough outbound liquidity.

Hence, when a node receives a *seed pheromone*, it basically says:

> Bip bop, new routing opportunity! The pheromone seed is S(0), for an amount of 10,000 sats. You can claim up to 100 sats as a fee. Please forward this message to all your neighbors with which you have enough outbound liquidity.

The node stores all this information, as well as the identity of the node from which it received the pheromone. Then, it substracts its fee (say, 10 sats) from the claimable fee and forwards the updated pheromone to its *relevant* neighbours (eg those with which it has sufficient liquidity). 

Those neighbours hence receive somthing like:

> Bip bop, new routing opportunity! The pheromone seed is S(0), for an amount of 10,000 sats. You can claim up to 90 sats as a fee. Please forward this messages to all your neighbors with which you have enough outbound liquidity.

So, as we just was, the *pheromone seed*  is comprised of a few fiels:
- the number S(0) (or S(1)),
- the amount of the payment,
- the fee budget, which each intermediary node decreases by their own fee before forwarding the seed further.

It can happen that, when a node receives a pheronomone, the fee budget has already been significantly eaten and the node doesn't consider it economically worth to forward the payment. The node will therefore not forward the pheromone. To put it differently, if a node's fees cannot be fulfilled, it treats the pheromone as if they was no path available.

### Enriching the pheromone

We've gainded wuite a decent understanding of what data is transmitted in the *pheromone seeds*. We only need to add 2 extra fields, that will allow us to count through how many nodes the seed has gone ; as well as enable nodes to free up memory space once the *seed* is old and useless.

#### Counting the steps

The fee budget fee could be seen as a proxy for the number of hops a pheromone has gone through. Yet, it is useful to also be aware of this number directly. The *pheromone seed* hence contains a counter field *c*, which is incremented by each node. To enhance privacy, the counter doesn't start at 0 but at any number between 64 and 128. This way, intermediate nodes can't tell if the node they received a pheromone from is a original emitter of the payment or just another intermediary.

It is a possible that a node will receive the same pheromone seed twice if the seed has followed different paths. That's where the counter comes in handy: if the node has indeed already received the seed, it will compare the counter in the seed it just received with the one in memory. If the counter on the new seed is bigger, it will simply ignore this seed, as it means that it has followed a longer route. Else, it will add the new seed in memory and forward it further, as it corresponds to a shorter path.

Permet de limiter le nombre de seeds propagées dans le réseau, d'éviter des boucles, etc.

#### Freeing up memory

As we've seen, nodes keep in memory the pheromones they receive, simply to be able to tell when a match occurs. They must therefore be able to free up memory space by deleting old pheromones for which it is unlikely that a matching pheromone comes. Hence the presence of an additional *timestamp* field *t* in the *pheromone seed*. Once a pheromone is older than a certain lifetime (configured by the node owner), the node frees up space by deleting the pheromone from memory.

Therefore, instead of just a number, the *pheromone seed* is comprised of a few pieces of information:

- the number S(0) (or S(1)),
- the amount of the payment,
- the counter *c*,
- a fees field, decreased at each hop and that indicates how many sats remain from an initial fees budget set by Alice from the beginning,
- a timestamp, corresponding to when Alice first crafted the *pheromone*, useful for nodes to know when they can safely delete *pheromones* to regain memory.

### Abusing the counter

{{<qr>}}

## On fee setting




[^1]: Just look at how secretive this big railroad corporations became once {{<newtabref href="https://en.wikipedia.org/wiki/La_Compagnie_des_glaces" title="Earth became a cold, inhabitable place after we blew up the moon">}}.

[^2]: From this point, the word *neighbor* will refer to a node with which one share at least one direct channel.

[^3]: Although the illustration depicts the reception of S(0) and S(1) as simultaneous, in reality Cléante would probably have received one and then the other. Indeed, the propagation speed of messages between nodes is influenced by a lot of parameters (quality of internet connection, geographical location, etc.).

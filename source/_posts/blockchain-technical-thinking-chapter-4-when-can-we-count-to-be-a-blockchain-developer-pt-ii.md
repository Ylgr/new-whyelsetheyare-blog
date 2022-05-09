---
layout: blog
title: "Blockchain Technical Thinking: Chapter 4 - When can we count to be a
  Blockchain developer? Pt. II"
date: 2022-05-08T18:32:02.901Z
top_image: /images/uploads/82028519_p0.png
tags:
  - blockchain
  - technical
categories:
  - blockchain
---
The sky is full of star like how the Blockchain is going. If we can count a Blockchain like a star, do you want to make one?

On this post, there will be an upper level of Blockchain development that require skill of above levels.

Do you want to know about it? Let's start.

<!-- more -->

# 1. Level 3 - Chain developer

At this point, many of you may think that if we can make one, it is so glorious.

Well, like how to develop an app, there are some framework that help us to make thing simply. There are some of them that I would like to talk about is:

![](https://i0.wp.com/coinyuppie.com/wp-content/uploads/2022/04/1649651900175615.png)

The first thing that I want to share about is Cosmos or Cosmos SDK. It is based on Tendermint and integrates some more feature like: DPoS consensus, Slashing, Governance, ...

It is the first thing exist of 3 Blockchain framework that I like to talk about. It's architect is Hub and Zones where each Blockchain using it may become a Zone. Each Zone can talk to each other by Inter‐Blockchain Communication Protocol (IBC) so it makes them more easier to have a Brige to others and that is main point of this architect. So if you want to build a chain that can easily have a Brige to some existed chain using Cosmos SDK like: Terra, Kava, ... Then this is the best choice for that. This thing using Golang.

Next, we have one of the most success Blockchain in 2021, Polkadot with its framework: Substrate. Its using Rust for programming.

Substrate is used for building chain and Polkadot is a place that connect all Blockchain using Substrate by architect: Relay - Parachain. In that architect, Polkadot has role to be Relay chain and protect and validate other parachain on it by it own validators. So main topic to using this framework that you can build your own blockchain that don't really need a bunch of validators to protect it, you just need many DOT to win the auction and Polkadot will maintain and protect your Blockchain for you. Expect of above reason, Web3 is foundation of those things (Polkadot and Substrate), so more than technology, that is the fame of people who developed Ethereum.

Finally, we have Avalanche - a new rising star, using Golang for development. By default, Avalanche exist 3 type of chain: X chain for exchange and create token in that exchange, C chain for contract development, P chain for protocol and operation. So I want to talk about P chain for chain development.

In Avalanche, we have some set of validators, each set is called a Subnet. A Subnet can choose what chain build on P chain to validate. It mean if they believe on your future of your chain, they will join to maintain and protect chain for you. The special of this model is number of validators. If two above has limit of number validator, then this architect can scale to very large or maybe infinity number of validator can join to maintain network.

# 4. Level 4 - Hardcore chain developer

Yep, still a chain developer, but it is godlike level.

Just image if you use those 3 framework to build a chain, but need to chain the core how it work, it will be more than just adding features. Or maybe even harder that you don't based on anything, just grab every part like Cryptography, consensus, p2p network, ... just to building a new one.

Okay, so we now all know the path of a Blockchain developer or to be true, just my opinion about some level that a Blockchain developer may take part in. So, what next.







---
layout: blog
title: "Open the world of Blockchain development - Chapter 6 (final): The rest
  and the dark sides"
date: 2022-11-09T18:14:29.875Z
top_image: /images/uploads/konachan.com-347516-sample.jpg
tags:
  - blockchain
  - crypto
  - EIP
categories:
  - blockchain
---
This chapter is the last concept you need to know about Blockchain technical world so let's talk about the rest of it. Inside the rest there is a dark side as Blockchain is still a new place in the end so it will be vulnerable to some kind of user activity.

<!-- more -->

# Genesis

Everything has its own starting point, so does Blockchain. Genesis can be a Block with index 0, can be a base feature like EVM to help develop ecosystem, can be initialing setting like a number of node address, block time, consensus config or anything else.

![](https://www.researchgate.net/publication/339901454/figure/fig1/AS:991835447107585@1613483406049/An-example-of-BlockChain-of-a-genesis-block-followed-by-two-blocks-Block-1-and-Block-2.jpg)

Well, there are nothing much to talk about this topic. Bitcoin may start with only one validator and 1 million of BTC for Satoshi Nakamoto. Now Bitcoin like 1 million miners and 19 million Bitcoin was mined.

From its genesis, the Blockchain would have been vulnerable, but probably not many people were interested in attacking it at that time. Because who know what kind of that thing can be so value in the future.

# Block lifecycle

Block start its live by the info of last block, it is Block initial phrase. Then it open for verified transaction can put into. After reach block time, it would be closed to change to block product phrase. Finally, it will be verified by Blockchain network in phrase Block finality. It will be put in a trie data structure to generate root hash for verify with others node, then store it in some kind of NoSQL database like LevelDB or RockDB.

# Mempool

This is placed to put pending transaction, then miner will try searching for best fee transaction inside to verify it and put it in to Block. Mempool is darkest place in Blockchain because it can be taken advantage by MEV.

# Maximal extractable value (MEV)

![](https://blog.chainalysis.com/wp-content/uploads/2022/08/Episode-17-Website-Graphic-1170x508.png)

There is a dark forest in Blockchain, its location is mempool. 

A story told about Dan Robinson accident find out an amount of token be stuck in one smart contract that can be withdraw the value of its around $12,000, and he know that dark forest is exist, so he needs to be careful when he trying to do that. He plans with his friend about this topic, then they trying to withdraw that stuck token but end up with a failed transaction. A transaction willing to pay more fee than them a little bit in the same Block is the one which withdraw success that asset.

## How MEV works

![](https://blog.chain.link/wp-content/uploads/2021/05/MEV-Diagram_V2.png)

MEV work by two participants:

\-﻿ Searcher: Who trying to search MEV opportunity and willing to pay a higher transaction fee to get profit more than fee used.

\-﻿ Miner: responsibility to priority the higher fee transaction, then make it be verified faster than the originals.

## How many types of MEV

Detail in the image below:

![](https://pbs.twimg.com/media/Fbvb9RhUIAIqIZ_?format=jpg&name=large)
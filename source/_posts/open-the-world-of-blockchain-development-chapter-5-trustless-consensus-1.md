---
layout: blog
title: "Open the world of Blockchain development - Chapter 5: Trustless (consensus)"
date: 2022-11-08T03:41:07.553Z
top_image: /images/uploads/77643899_p0.png
tags:
  - blockchain
  - crypto
  - EIP
categories:
  - blockchain
---
Can you completely trust someone even though they are with you? Want but cannot, right? We are living in the world that most of situation is grey color, anyone or anything is your comrade today may turn in to your enemy tomorrow. Blockchain is a large system which was built by the community, how to make sure the last information set in Block is the truth?

<!-- more -->

# Byzantine fault tolerance

This is a traditional topic to check if a server can be inconsistently. In its simplest form, a number of generals are attacking a fortress and they must decide as a group whether to attack or retreat. Some generals may prefer to attack, while others prefer to retreat. The important thing is that all generals agree on a common decision, for a halfhearted attack by a few generals would become a [Rout](https://en.wikipedia.org/wiki/Rout "Rout"), and would be worse than either a coordinated attack or a coordinated retreat.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/f/fc/Byzantine_Generals.png/1920px-Byzantine_Generals.png)

In computer science field, we will make an election by using [ECC](https://en.whyelsetheyare.tk/2022/10/30/open-the-world-of-blockchain-development-chapter-1-how-blockchain-can-protect-your-value-cryptography/) to make unique signed vote of each general that can be easy verify (hard to fake).

The strategy is: First, we need to choose a decision is attack or retreat. For example we would choosing attack, then make a election with others generals. If number of vote that have same result as attack more than 2/3+1 vote, then attack is a final decision. Otherwise the election is stuck there so they will do nothing and continue the siege.

# The proof

## Proof of work

## Proof of stake

## Delegated proof of stake

## Proof of history
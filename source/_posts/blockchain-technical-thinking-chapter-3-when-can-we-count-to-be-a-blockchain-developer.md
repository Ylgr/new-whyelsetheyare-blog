---
layout: blog
title: "Blockchain Technical Thinking: Chapter 3 - When can we count to be a
  Blockchain developer?"
date: 2022-05-03T07:49:51.220Z
top_image: /images/uploads/82028519_p0.png
tags:
  - blockchain
  - technical
categories:
  - blockchain
---
Developers, in some ways can have a chance to working with Blockchain industry. Some of those may want to be a Blockchain developer but still not sure that to be count or not?

In this post, I will share my opinion about the level of Blockchain developer in development way. Of course it will not relative with experience, just some kind of work help you know where you are in the way of Blockchain developer.

<!-- more -->

Overview picture would see like this:


# 1. Level 1 - still not be a Blockchain developer: Interacting with Blockchain

There are several of application just to interact with Blockchain. They may be a Blockchain explorer, a app to swap token, a crypto wallet, an IDO project, ...

![](/images/uploads/pna.png)

It's may split to some smaller level depend on what knowledge of Blockchain they need to interact:

- Explorer: This application just want to look something might happen in Blockchain network through api or socket, for example: an exchange may only need to scan Blockchain to detect a deposit order (of course exchange would be more complex than that).

- Dapp: Do you know pancake swap? That is this kind of application and to developing this kind you need to know how to interact with a Blockchain and its Smart contract.

- Wallet: Trust wallet may be the best kind of this type at this time. You need both of two requirement of those two type above and cryptography.

Technical stack:

It depends on what Blockchain you develop on, of course. For example: In EVM environment (Ethereum, BSC, Matic) you need to use Web3, in Solana it maybe spl library.

About Cryptography, there are several things, but it may around some technologies like: Bip39, Elastic curve (Ed25519, Secp256k1, ...), One way hash (SHA256, KECCAK256, ...), Serializable (Hex, Base58, Base64).

# 2. Level 2 - Smart contract developer

When you call someone with title Blockchain developer, most of them may work in this level.

![](/images/uploads/eth-ada-sol.png)

There are several options for Smart Contract builder based on function and trust of each Blockchain. At the time of this post, I choose 3 different architect of Blockchain to explain how it works.

Firstly, we have the origin of the concept Smart contract: Ethereum.

Ethereum and some of it clone (BSC, Matic, Fantom, ...) using EVM for Smart contract development, its mean that you need to use Solidity or Viper to write Smart contracts in it. 

Here are some tool of that ecosystem:

![](/images/uploads/evm-tool.png)

About the way of thinking how to dev, the development will be around State. State is a variable that only can be changed by transactions.

The same age as Ethereum, we have Cardano or ADA for short. Cardano using traditional transaction type called UTXOs with a little modify it. If you want to build something on it, you need to thinking based on how UTXOs work.

Finally, we have a rising star called Solana. Solana does not use work Smart contracts like others. It uses word Program to refer that concept. Yep, it is not like EVM Smart contracts at any point. You need to thinking based on Program Derived Address (PDA). 

It means when you deploy a program to network, to use that program, you need to pick up a new key pair and use it to make a PDA of that program for example that program is spl token program. After create a token by that way, each user need other key pair that is managed by other account of System program. 

Agree that it may be complex, but at the end it makes easier when it comes to scale and that is thing make transaction fee of Solana very cheap and fast.

We still have other two levels. See you there.

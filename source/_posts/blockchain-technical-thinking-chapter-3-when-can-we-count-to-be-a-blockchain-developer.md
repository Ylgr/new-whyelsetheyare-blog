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

About Cryptography, there are several things but it may around some technologies like: Bip39, Elastic curve (Ed25519, Secp256k1, ...), One way hash (SHA256, KECCAK256, ...), Serializable (Hex, Base58, Base64).


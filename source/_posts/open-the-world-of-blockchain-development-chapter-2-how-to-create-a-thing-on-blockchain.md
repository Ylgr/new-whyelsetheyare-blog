---
layout: blog
title: "Open the world of Blockchain development - Chapter 2: How to create a
  thing on Blockchain"
date: 2022-10-24T17:24:01.943Z
top_image: /images/uploads/81634385_p0.png
tags:
  - blockchain
  - crypto
  - EIP
categories:
  - blockchain
---
Have you ever heard about the overwhelm of "Smart Contract" or "Blockchain not Bitcoin" for quite a time in the past or even now? This is the topic that we will talk about in this chapter.

<!-- more -->

# Meaning of smart contract

In the last chapter, we learned that Blockchain data is state. Are you interested in what kind of data the state can be and how it can change?

Basically, you can assume a default state of Blockchain is the native token. But it is more than that, in 2nd generation of Blockchain, the concept of Smart Contract started and it make much more optional to working around with it like store value in token, save some important information of your life like your wedding time in the Blockchain or just create some fun game with fair mechanism.

![](https://app.builtin.com/cdn-cgi/image/quality=80,width=752,height=435/https://builtin.com/sites/www.builtin.com/files/styles/byline_image/public/2022-02/blockchain-nfts.png)

There are so much option for you to do that. All you need is to prepare a solution knowledge that is possible if you choose to use other types of Smart Contracts.

# The solution of smart contract

## E﻿VM

T﻿he first type I want to talking about is most popular concept of the Smart contract: EVM or Ethereum Virtual Machine.

![](https://images.viblo.asia/b37b5437-ee0e-4639-8041-d2a45d0c8cac.jpg)

EVM is like a CPU that computes your logic to output the result to save it in the Blockchain.

A﻿nd there are few concept you need to know to working with it, it is:

![](https://wilkinson.graphics/img/portfolio/vyper/existing-logos.png)

* Solidity: A specific programming language you want to know to work with the EVM. Most of Blockchain developer know how to use it.
* V﻿yper: Other programming language for someone who more familiar with Python.
* W﻿hispers: Decentralize messaging to help you save log for searching in the future. The disadvantage of it is Blockchain itself cannot read this information.
* S﻿warms: Decentralize storage to keep your data as state.

## S﻿olana program

T﻿he problem of EVM is a state that may be bigger in the future be like you need to spread every stuff in your yard, it always need your time and effort to get things right. Solana program has other architect that it not called itself is Smart contract, it called Program.

![](https://coinexpress.net/wp-content/uploads/2021/11/solana-hits-new-all-time-high-overtaking-ripple-s-capitalization.jpg)

I﻿n Solana you need to prepare a fixed size for your data, if you know you may need more than it, you need to use another space to keep it. This mechanism called PDA.

P﻿DA mean when you store data, you need to rent an account to keep it with size fixed so you may need more size in the future if you want to store more. If you don't want to keep an account data anymore you can release it to receipt back some of your rent fee.

It's like building an apartment. Finish a program meaning you finish foundation. Then you can build more higher depend on your architect that you wire before by rent more type of account to storage data.

T﻿he advantage of this solution is you have a high speed Blockchain, save money on transaction fee so you can make much more transaction to enjoy feature running on Blockchain. The addition of Solana that you can make many type of transaction at once, each small transaction called instruction.

T﻿o working with this technology, you need to be able to use Rust.

## S﻿ystem program

T﻿he Blockchain maybe an decentralize application itself. Some of them born to do something like Ethereum 2.0 has Stake mechanism that using goverment, stake, pool reward System contract to management.

![](https://ethereum.org/static/ddb9a22d53fdaaae70c0a0d94577f2aa/52295/eth.png)

S﻿ystem contract only be created before Blockchain genesis so you need to build a Blockchain that we will talk in another topic.

## S﻿ubstrate Ink!

![](https://www.shawntabrizi.com/substrate-contracts-workshop/media/substrate-ink.png)

A﻿n advantage type of Smart contract that can communicate with System contract when you building with Substrate framework.

J﻿ust imagine: you have some feature to call in future scheduled time. The problem of other type of Smart contract that you need 3rd system that has cronjob to support you do this action. Solution can be solve in different way in this case that you can write a Ink Smart contract that call to Schedule System contract of Substrate to schedule.

I﻿n Substrate Ink! You need to know how to use Rust to working around.

## O﻿ther type

T﻿here are some other type of Smart contract that maybe popular but concept itself maybe outdated (like UTXO concept) or not so much different with EVM concept but change programming language. Some of them are:

\-﻿ Cardano: The UTXO concept to build Smart contract.

\-﻿ Near protocol: Rust smart contract but not so different with EVM concept of state.

\-﻿ EOS: C++ contract with zero fee on transaction but you need CPU and RAM (from stake EOS) to use it.
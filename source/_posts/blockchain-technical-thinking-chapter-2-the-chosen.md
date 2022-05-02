---
layout: blog
title: "Blockchain Technical Thinking: Chapter 2 - The chosen"
date: 2022-03-18T11:53:07.530Z
top_image: /images/uploads/82028519_p0.png
tags:
  - blockchain
  - technical
categories:
  - blockchain
---

"For success, choice is more important than action".

This chapter will be the overview of what is happening in our Blockchain world. Of course at the time this post is writing.

<!-- more -->

# 1. What do I do on Blockchain?

This is what you can deal with Blockchain was I sorted by difficultly.

## 1.1. Live a protected life

I am talk about the way that most of Dapps follow. This way you just strange use an existed Blockchain platform to build your world.

Firstly, you need pick a good platform that most suitable for your business requirements.

We have some kind of good platform today:

- Ethereum / Binance smart chain / Matic (EVM): A familiar platform with most Blockchain developer because the popular of Solidity and Openzeppelin. For some still don't know what they are: Solidity is a programming language (must like be a Library because it is too small to be called language), Openzeppelin is the biggest library that coded in Solidity. By using Openzeppelin, you can easily create a token contract with only 4-5 lines of code and so more.

- Solana: Not so familiar with most Developer because of using Rust. So it will be more difficult to find Developers. In terms of application, it will help you have a better experience in both of speed and transaction fees. You can easily create a Token with SPL but for another specify business, it will be more difficultly. By the way, not like EVM, most time you don't need to deploy new logic to networks, you can just using some existed program that has logic you want and create a PDA of it to use it. Not only that, on this platform you will have other type of transactions that make you can group many child transaction (called instructions) at once to active it. Just image you create a token and an application on Solana, then you can create a frontend to use application and at the same time, you collect transaction fee, pay Sol for network fee instead of user, make user interact with application.

Here is a comparison table of platforms (Price example: ETH - 500$, BNB - 2$, MATIC - 3$, SOL - 200$):

|             | Ethereum    | Binance Smart Chain | Matic | Solana |
| ----------- | ----------- | --------------------| ------| -------|
| Speed      | 15s - some days | 3s - 30s        |  1s - 12s |  0.5s - 6s |
| Fee   | 2-3$        | 0.05 - 0.2$           | 0.002 - 0.005$ | 0.0005$ - 0.002$|
| Fee create acccount| 0 | 0 | 0 |0.4$|
| Platform | EVM | EVM | EVM | Solana program|
| Programming language| Solidity | Solidity | Solidity | Rust|
| Most popular library| Openzeppelin | Openzeppelin | Openzeppelin | SPL |
| Popular wallet | Metamask | Metamask | Metamask | Phantom |

Talk about the wallet, if you build a mobile app, most like you will need to implement a local wallet on your app that handle it. In this case, you need to have some knowledge about Cryptography like: Bip39, Ed25519, Keccak256, ...

## 1.2. Newcomer? You are welcome

If you are familiar with Crypto Exchange about deposit and withdraw, so this is one of those type. Some others type of those is: Cross chain / Bridge, some type of listen event services.

Why I choose to grouping them. All of them need a system has responsibility to scan Block and notify some kind of event. If conditions are satisfied, services will trigger some action that necessary.

This ofter to be the easiest way to help non-blockchain user getting started.

In Exchange architect, you always listen the events of Blockchain to make sure that you don't miss something (so annoying if a customer need supporter services to solve his/her problem because of that). You even don't need to write anything to deploy on Blockchain in this case.

Talking about Cross chain, on the other hand you may need to know about it. Cross chain mean you do some action in a chain and emit some others action that match with it.

In conclusion, in this way, may be you don't need to put anything to the Blockchain network but in my opinion it will be harder because of security. There are many ways to fake information that was read, so it may have some effect with how business run in other way that called your system is hacked.

# 2. Layer 3 application

If you still don't know, all the description I was written above is called Blockchain Layer 3.

We still have two others layer to archive: Layer 2 - Side chain and Layer 1 - Main chain.

The lower of number layer, the harder and more dangerous you need to face. Be patient for it.

Alright, see you in next chapter.

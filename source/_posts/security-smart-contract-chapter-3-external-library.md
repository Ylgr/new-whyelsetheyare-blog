---
layout: blog
title: "Security smart contract - Chapter 3: External library"
date: 2023-04-05T11:14:19.662Z
top_image: /images/uploads/76405513_p0.jpg
tags:
  - smartcontractsecurity
categories:
  - Smart contract
---
OpenZeppelin is a popular library of smart contract templates and tools that can help you build secure and reliable contracts more easily. While these resources can be valuable, it's important to use them in a way that follows the KISS principle and keeps your code simple and easy to understand.

<!-- more -->

# Appling access control mechanism

Basically, each contract function \`public\` or \`external\` can be call by anyone in the Blockchain network. Because of that, some function should only be called by some specify people (like withdrawMoney) that need some advance design to approach it. Luckily, OpenZeppelin already prepare some for us to implement.

## Ownable pattern

The most basic and gas-saving pattern. By using Ownable library, contract implement now has an address be count as Owner. By using onlyOwner() mark a function to make sure function only be call by address owner.

This pattern supports some use case to manage owner:

\-﻿ Transfer owner: by using this feature, executive address gives up ownership (if has) to another address.

\-﻿ Renounce ownership: this feature makes executive address give up ownership to address zero, meaning give up ownership permanently.

The advance of this library is 2StepOwnerable, it needs one more step on address be transfer ownership to confirm. Meaning before address be transfer ownership confirm, transferring address still has ownership on Smart Contract.
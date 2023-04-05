---
layout: blog
title: "Security smart contract - Chapter 3: External library"
date: 2023-04-05T11:14:19.662Z
top_image: /images/uploads/76405513_p0.jpg
tags:
  - smart-contract-security
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

## Role-based access control

In order to reduce centralize of ownable pattern, OpenZeppelin also product a library help control multi role in multi authority setting.

Now use case for smart contract more width. For example, for a Token smart contract can have a minter role for some authority person important for market maker and a pauser role to help maintainer stop network if needed.

The advance library is EnumAccessControl. It not only province roles but also safe them on-chain to easier re-track number of people control role or how many roles exists. Using in case does not care much about gas fee and need better solution to manage authority.

## Muli-signature wallet

The final solution on this type is setting up a wallet be control by a number of other wallets. This is the most decentralize solutions, trade-off by require people confirm each other's to execute something. This solution suitable for asset management like charity, make it more trustless.

# Emergency stop

Not like we can make everything perfect from started, OpenZeppelin province a stable solution that is we can emergency pause all execute of functions.

Using an emergency stop functionality provides an effective stopgap for dealing with serious vulnerabilities in your smart contract. However, it increases the need for users to trust developers not to activate it for self-serving reasons. To this end, decentralizing control of the emergency stop either by subjecting it to an on-chain voting mechanism, timelock, or approval from a multisig wallet are possible solutions.

# Upgradeable

We will talk more about this solution in other series. It is a mechanism help you update Smart contract code without change current execute address and contract data by a layer to store data and a layer to execute logic.

# Governance

## Timelock

The transaction will be safer if it be executed later. Remember, you need to wait around 10 minutes to has a produce block, this mechanism help we has more time to getting everything on control be for really execute it.

## Voting

A combo go together with timelock. Like bitcoin network using PoW to choosing which node would produce next block after a set of time. Another way to archive this by province "voting weight" to make people invest more has more power to control the safety of network.

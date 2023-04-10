---
layout: blog
title: "Security smart contract - Chapter 4: Maintain"
date: 2023-04-10T13:28:42.321Z
top_image: /images/uploads/104835805_p0.jpg
tags:
  - smart-contract-security
categories:
  - Smart contract
---
After development phrase is go production time. Like other system development, maintainer is needed to make sure everything working smoothly in control. Actually, you don't want to be exploit your bussiness by some MEV and don't have any menthod to revert it. This chapter, we will find out some way to make it.

<!-- more -->

# OpenZeppelin Defender

First reason to use it, it is free ... for some feature can be used. Its still a good feature for both of maintainers and users. Here is these five: Admin, Relay, Autotasks, Sentinel and Logging. The best benefit of using OpenZeppelin Defender is they can combine to each other to optimize use case.

## Admin

Mostly, this feature will be used by maintainers and developers, it helps them manage ownership and execute authority's rights of Smart contract (for execute some sensitive function for example).

To using all supported features of this components you need to use OpenZeppelin library like governance, access control or upgradeable proxy.

Talk about upgradable, this may be the sensitive part of Smart contract when it like a knife, both protect smart contract from vulnerability and make it become vulnerability. When combine it with relay feature, it helps the upgrade ability now will be distribute between maintainers and even advance user when they can propose upgrade code version. This ensures that the upgrading process is more transparent and less susceptible to a single point of failure or misuse.

## Relay

We told about it above and this time we will clear how it's working. Each transaction will contain some extra payments called fee; relay response collects all transaction to execute at one to reduce gas fee.

If you still feel it's not good enough here may is the thing you care, zero fee! Zero fee meaning for some specify transactions in batch transaction, you can config it mean zero fee, this is new user-friendly feature if you not recognize.

By implementing the Relay feature, smart contract developers can create a more user-friendly experience, especially for those who are new to blockchain or have limited access to cryptocurrency for paying gas fees. It can also help increase user adoption and engagement with smart contracts since users won't be discouraged by the costs associated with interacting with the  contract.

## Autotasks

Do you want to execute some feature in a specify time of month to reward user or collect money each time it reach a threshold, just using a vps and setup cronjob for it .... or using autotasks feature in Defender.

T﻿o be clear, autotasks is automatic scripts that can be triggered by different events or executed on a predefined schedule. These autotasks enable developers to automate various processes within their smart contracts. The three main types of autotasks are Schedule, Webhook, and Sentinel-based.

**Schedule**, to be easy it like cronjob. You prepare some code and schedule time to call it, it will trigger when time come whenever every days, every hours or even every minutes. The main use case of it can be:

* Distributing rewards or dividends to token holders at specific intervals.
* Fetching off-chain data periodically and updating the smart contract with the latest information.
* Rebalancing a decentralized finance (DeFi) portfolio or updating liquidity pools at predefined intervals.

**Webhook** is external trigger help you call scripts from other platform like chat, app or something else. Some examples of webhook-based autotask use cases include:

2. Some examples of webhook-based autotask use cases include:

* Triggering smart contract actions based on user interactions with a web application or DApp, such as voting, staking, or withdrawing funds.
* Responding to external API events, such as price updates, real-time data changes, or social media activity.
* Integrating with third-party services, like oracles or data providers, to update the smart contract based on external events.
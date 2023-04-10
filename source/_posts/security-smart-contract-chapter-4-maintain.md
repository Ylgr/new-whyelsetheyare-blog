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

* Triggering smart contract actions based on user interactions with a web application or DApp, such as voting, staking, or withdrawing funds.
* Responding to external API events, such as price updates, real-time data changes, or social media activity.
* Integrating with third-party services, like oracles or data providers, to update the smart contract based on external events.

**Sentinel** is next component we will mention, in this scenario we only need to know it is a script be triggered by event on-chain. Some examples of Sentinel-based autotask use cases include:

* Monitoring and responding to specific smart contract events, such as token transfers, contract interactions, or function calls.
* Reacting to on-chain conditions, like price fluctuations, token balances, or liquidity pool changes, by triggering actions like liquidations or rebalancing.
* Implementing automated security measures, such as pausing the contract, notifying developers, or rolling back transactions if suspicious activity or vulnerabilities are detected.

## Sentinel

When thinking about maintainers, the things be most people thinking about is notification, right? This role be responsibility by Sentinel.

There are three type of Sentinel that is: 

* Contract Sentinels use on-chain data to monitor smart contract activity and trigger alerts or actions based on specific events or conditions. Some use cases for Contract Sentinels include:

  * Detecting and alerting developers to unusual or potentially malicious activity, such as large token transfers, repeated failed transactions, or unauthorized function calls.
  * Triggering automated responses to specific events or conditions, like pausing the contract, rolling back transactions, or executing corrective actions.
  * Monitoring key performance indicators (KPIs) and providing insights into the contract's usage, such as user growth, transaction volume, or token distribution.
* Forta Sentinels use off-chain data, such as transaction data, logs, events, and external data sources, to analyze and detect anomalies, vulnerabilities, or suspicious activity in smart contracts. Some use cases for Forta Sentinels include:

  * Identifying and alerting developers to potential vulnerabilities, such as reentrancy attacks, front-running, or price oracle manipulation.
  * Analyzing historical transaction data to detect patterns or trends that could indicate issues, like excessive gas usage, spam transactions, or address concentration.
  * Integrating with third-party services, like oracles, data providers, or security scanners, to enhance the security analysis and threat detection capabilities.
* Forta Local Mode Sentinels create a simulated environment for developers to run and test Forta Sentinels during the development process, allowing them to identify and fix potential security and performance issues before deployment.  Some use cases for Forta Local Mode Sentinels include:

  * Running security checks and vulnerability scans during the development process to catch potential issues early.
  * Testing the smart contract against known attack vectors and edge cases to ensure it behaves as expected and is resistant to common threats.
  * Analyzing the smart contract's performance and gas usage to optimize its efficiency and reduce deployment costs.

## Logging

The last thing I want to mention by I need, it is Logging - a premium feature.

Every execute of above components: Admin, Relay, Autotasks and Sentinel has logs and it will be stored here. The main feature of this component is forward all these logs to another destination to analyst like Slunk or Datadog. Or just use it directly.

With Logging, you can:

* Store logs of all executed actions in the Defender components for audit and analysis purposes.
* Forward logs to external platforms like Splunk or Datadog for more advanced analytics, visualization, and monitoring capabilities.
* Identify patterns and trends in smart contract usage, performance, and security to inform future development and business strategies.
* Diagnose issues, vulnerabilities, or anomalies in smart contract behavior by analyzing historical logs and events.
* Ensure compliance with regulations and industry best practices by maintaining a comprehensive audit trail of all smart contract activities.

In summary, the Logging feature in OpenZeppelin Defender provides a comprehensive overview of all past activities within the platform. It enables developers and maintainers to analyze and optimize their smart contracts, enhance security, and make data-driven decisions to support their project's growth and success.
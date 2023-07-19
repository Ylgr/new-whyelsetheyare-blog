---
layout: blog
title: "Security smart contract - Chapter 5: Simulator"
date: 2023-04-11T13:36:49.063Z
top_image: /images/uploads/103449029_p0.jpg
tags:
  - smart-contract-security
categories:
  - Smart contract
---
There are several of hacks making millions of dollars lost in this Blockchain world. The reason come from the mistake of development. According to [Rekt](https://rekt.news/), we may know how that accident happen in overview way but for engineer, you must truly understand step by step how it's going. This chapter, we will explore a useful tool to help us do that and so more.

<!-- more -->

Its name **Tenderly**.

Same mission for maintaining Smart contract (like OpenZeppelin Defender that we explored in last chapter) but focusing on different way. Well, by overall, Tenderly is more focused on monitoring and debugging, while OpenZeppelin Defender is more focused on managing and securing smart contracts.

To understand how Tenderly support us, let's learn about benefit of each component from it.

# Devnets

If you concern that Ganache is good enough why we should use this thing, the answer is if you want easy and quick, just using Ganache. Tenderly devnet is a public Ethereum test network that is designed to closely mimic the behavior of the Ethereum mainnet. It is a reliable and stable environment for testing and deploying smart contracts, and it provides advanced features such as gas profiling, transaction tracking, and contract debugging. Additionally, Tenderly devnet has built-in support for MEV (Miner Extractable Value) analysis and allows developers to fork the network at specific block heights for testing purposes.

Devnets not good enough? Go next component!

# Simulations

Just image you have any Private key in this world running on Ethereum network. Simulation will help you do that without needing to know or have access to its private key.

Tenderly Simulations uses a technique called "mocking" to simulate the behavior of Ethereum addresses and contracts. Mocking involves creating a simulated version of an address or contract in the simulation environment that behaves in the same way as the real address or contract would on the live network.

For example, if you want to simulate a token transfer from one address to another, you can create a mock version of the sending address and the receiving address in the simulation environment. You can then simulate the token transfer between these mock addresses as if it were happening on the live Ethereum network.

This allows you to test and debug your smart contracts in a simulated environment without needing to worry about the security risks or complexities of using real Ethereum addresses and private keys. It also makes it easier to set up complex testing scenarios involving multiple addresses and contracts.

***We can fork network too.***

Now we can turn back time, revert hack and make another one before its happen. Using fork choose starting point before it happen and trying to realize the scenario. 

Are you understand why it happen? 

Good! Don't make that mistake on your production.

Dry runs, refers to a simulation of a transaction without actually executing it on the live network. Essentially, it allows you to test a transaction and see what its effects would be without incurring any gas fees or actually changing the state of the blockchain.

Tenderly supports dry runs in its simulation environment, allowing developers to test and optimize their transactions and smart contracts before deploying them on the live network. The dry-run feature in Tenderly can also be used in combination with other features, such as gas profiling or contract debugging, to provide a powerful toolset for Ethereum developers.

# Monitoring

Lets see, you are watching a mempool then discovering your customers being "sandwich" and they don't know it. Okay first, do you know how to go into that situation? Deploy a node and writing some query code to do that, right? You can use Tenderly Monitoring to do that.

Tenderly Monitoring is primarily focused on providing real-time monitoring and analysis of smart contract execution on the Ethereum network. It helps developers to track and optimize the performance and security of their smart contracts and dApps.

If you don't want to watch how it happens all the time. Let's using Alerts.

# Alerts

Tenderly Alerts is simple ... alert. There are many things you can setup an alert like successful transaction, failed transaction, event emitted, transaction value, blocklisted callers, state change, ... Then you can receive it through Slack, Sentry or Email.

# Debugger

If you are too lazy to fork and using simulation, Tenderly give you an extension that you can use it to debug and transaction that exist on Etherscan, that mean even the hack one. You want to wear ... a hat with color? Then this is solution for you, just install it and go directly to the hack transaction and explore it!

With Tenderly Debugger, developers can:

1. Step through smart contract code line-by-line: The Tenderly Debugger allows developers to step through their smart contract code line-by-line, making it easy to identify where errors or unexpected behavior are occurring.
2. Monitor contract state: The Tenderly Debugger provides real-time monitoring of contract state, making it easy to see how contract state changes during execution.
3. View detailed transaction information: The Tenderly Debugger provides detailed information about each transaction, including gas usage, gas costs, and the events emitted during execution.
4. Set breakpoints: The Tenderly Debugger allows developers to set breakpoints in their smart contract code, making it easy to pause execution at specific points in the code.
5. Optimize gas usage: The Tenderly Debugger provides detailed gas profiling information, allowing developers to optimize gas usage and reduce transaction costs.

***Bonus***: Tenderly War Room Aid Kit.

The War Room Aid Kit includes a range of services and tools, including:

1. Rapid incident response: The War Room Aid Kit provides a rapid response service that allows developers to quickly deploy a new version of their smart contract in the event of a security incident or other emergency.
2. On-demand security review: The War Room Aid Kit includes an on-demand security review service that provides a detailed analysis of a smart contract's security vulnerabilities and recommendations for improvements.
3. Customized incident response plans: The War Room Aid Kit provides customized incident response plans tailored to the specific needs of a dApp or smart contract. These plans include detailed procedures for responding to incidents, identifying vulnerabilities, and mitigating risks.
4. Dedicated support team: The War Room Aid Kit includes a dedicated support team of Ethereum experts who are available 24/7 to help developers respond to critical incidents or emergencies.

Overall, the Tenderly War Room Aid Kit provides a comprehensive set of tools and services designed to help Ethereum developers respond to critical incidents or emergencies related to their dApps or smart contracts. By using the War Room Aid Kit, developers can be better prepared to handle security incidents or other emergencies and mitigate the risks associated with these events.
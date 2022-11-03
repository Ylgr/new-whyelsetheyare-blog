---
layout: blog
title: "Open the world of Blockchain development - Chapter 4: The unique (of
  transaction)"
date: 2022-11-01T18:15:26.545Z
top_image: /images/uploads/konachan.com-258963-sample.jpg
tags:
  - blockchain
  - crypto
  - EIP
categories:
  - blockchain
---
Decentralized means having many of the same things: Same in data, same in program, ... How about input from the client, which can be accidentally sent to the server multiple times? This problem even many centralized systems need to find a way to solve. It may be more difficult in decentralize environment, right? Yep, but it has some solution for this problem in decentralize way that we will find out in this topic.

<!-- more -->

# First solution UTXO

In the first generation of Blockchain, beside of Bitcoin, we have many other Blockchains that follow by this solution rule: UTXO (stand for Unspent transaction output).

The information that UTXO have is: input, output, timestamp, hash, nonce.

Typically, that type of Blockchain don't save your balance to query, so you need to get sum number of your UTXO in your account to get the number.

This mechanism worked based on money flow. UTXO created from mining, it is block reward and sum of transaction fees on that block. It is then splitted and reduced by some as a fee in transaction, so it means money from whoever had it initially.

![](https://www.researchgate.net/publication/352182532/figure/fig2/AS:1032055378935812@1623072585707/The-example-of-Bitcoin-UTXO-transaction-model.png)

UTXO can be splitted or grouped. When you create a transaction send coin to another address, you need to collect one or more UTXO in input that enough for both of send amount and transaction fee, then create new UTXO in output at least one for destination address, and another one for yourself if have any amount left.

If there are two transaction with same valid input that send to the network at the same time, the transaction executed first will reject another one. The priority to execute transaction depending on fee pay for each transaction data so more fee and less data meaning transaction will be executed faster. So if you create a transaction by accident, you can still revert it if it still not in Block by create another one same input then change it destination and add some more fee to it.

![](https://coinsutra.com/wp-content/uploads/2017/06/Bitcoin-Confirmations-e1498718174774.jpg)

So never have double spending on Blockchain when network still be in protect.

# The nonce

Another strategy to prevent double spending is using nonce. It is like versioning on management on software development. Nonce is a number of each account typically start from 0 and increase by one through each transaction (there are some exception of nonce start from another number).

This nonce is different with Block nonce, it is exist on each address, using to fill to transaction to detect the different of each transaction.

![](https://i.stack.imgur.com/OItKD.png)

By using this solution, the Blockchain can save the balance of each address as state, so it will be more client friendly.

Now, the question is how you can revert a valid transaction that you created by accident? Just using the same nonce number, add some more fee, then send it to the network as soon as possible because typically, this type of Blockchain is more effetely on Block verify.

# The speed aka the timestamp

In some situation, the problem about speed is raise so some type of Blockchain follow this architect to solve this problem.

The most powerful point of this architect is it available to execute transaction of same address async.

Below is an image that explain well how this solution works:

![](https://cryptopotato.com/wp-content/uploads/2021/10/img1_solana.jpg)

If you want a Blockchain that have best TPS for your business, go for this type.
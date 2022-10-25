---
layout: blog
title: "Open the world of Blockchain development - Chapter 1: How Blockchain
  works technically"
date: 2022-10-23T18:22:08.083Z
top_image: /images/uploads/98902426_p0.jpg
tags:
  - blockchain
  - crypto
  - EIP
categories:
  - blockchain
---
You are a developer and have some questions about how Blockchain technically works and why it is better than a traditional database in some situations that make people feel overwhelmed about that about that?

I﻿f your answer is yes, it mean this series is suitable for you.

<!-- more -->

# The principle

## How data are stored

Let's talk about how a database works. It stores some kind of value that you can read, create, update or delete a record inside if you have permission. When you read the record, it doesn't affect the value inside but if you want to create, update or delete a record, you need to do a transaction to change it. How Blockchain stores data in the same way, but more specifically as a record called state and transactions are stored as a log in the Block. Like this:

![](https://ethereum.org/static/85d784391401f89209d3bcc51e0ea677/302a4/tx-block.png)

The difference is that Blockchain's database is secured by many maintainers called Node. So it's much harder than a traditional database if you want to hide something that makes your value stored differently from what it really is.

## Private Blockchain vs Public Blockchain

T﻿here are two main types of Blockchain in this world, namely: Private Blockchain and Public Blockchain.

![](https://www.ifourtechnolab.com/pics/Public-blockchain-Private-blockchain.webp)

### Private Blockchain

One scenario is that your company is running a business and you need other companies involved in the process but you don't know if you can trust their information.nd there is still some sensitive information that needs to be moderated for some participants, others can be made public to anyone. Private Blockchain was created to solve this problem. 

Private Blockchain has mechanism called authority. Each organization participating in the system has a different role with the system, since the database is distributed internally by the organizations, information can be trusted because of that.

There are some popular framework to build this:

![](https://dreamzchain.com/wp-content/uploads/2019/04/blockchain-and-corda-4.jpg)

### P﻿ublic Blockchain

On the other hand, if you don't have any sensitive information. Public Blockchain will be the better choice.

Typically, the Public Blockchain is maintained by the community and its own organization. So it needs some mechanism to protect it from spamming, the solution is transaction fees.

T﻿here are some useful framework created by big technology company in this field to support you build one.

![](https://sp-ao.shortpixel.ai/client/to_webp,q_glossy,ret_img/https://www.analyticsinsight.net/wp-content/uploads/2022/03/Terra-Cosmos-Avalanche-Polkadot-and-EverGrow-Coin-Altcoins-Lead-the-Crypto-Surge-in-March-2022-1440x564_c.jpg)

# Can all types of data be stored on the Blockchain?

T﻿he short answer is **Yes**, the full answer is **It's depend**.

## The problem of being decentralize

Choosing to be decentralized means that data needs to be synchronized to be the same at each node.A large file stored in the Blockchain means that all nodes have to download it and that's the problem because it may stuck in many node cause network be suspended.

Normally you need to store that file somewhere and save its path to Blockchain but the problem is what if the file in that direction can be changed? So there are several solutions to this problem.

## I﻿PFS

![](https://icommunity.io/wp-content/uploads/2020/08/IPFS.jpg)

I﻿PFS or InterPlanetary File System is a decentralize storage. Storing data at there you will have an unique path that cannot be change data in it direction.

B﻿ut, it is decentralize, right? So it's still have same problem with Blockchain.

W﻿ell, it is not store your data directly. It is only pinning that your file exist somewhere and you need that pinning to keep your url still working. So there are some services that help you do that. Google it, okay?

## A﻿rweare

![](https://img.capital.com/imgs/articles/1200x627x1/shutterstock_2016039677.jpg)

N﻿ormal Blockchain does't but special Blockchain does. Arweare is a specifically Blockchain using for store big file and created an unique url that cannot be changed data inside. You need to pay AR depend on your file size.

# W﻿hat's next?

 ﻿Blockchain not only store database, but also store logic to calculator data to store. Next chapter we will learn about how to store logic and how far logic can be store in Blockchain.
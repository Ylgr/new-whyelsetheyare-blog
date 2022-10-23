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
# 1﻿. The principle

Let's talk about how a database works. It store some kind of value and you can read, create, update or delete a record inside if you have permission. When you read, it doesn't affect the value inside but if you want to create, update or delete a record, you need to do a transaction to change it. How Blockchain stores data in the same way, but more specifically as a record called state and transactions are stored as a log in the Block. Like this:

![](https://ethereum.org/static/85d784391401f89209d3bcc51e0ea677/302a4/tx-block.png)

The difference is that Blockchain's database is secured by many maintainers called Node. So it's much harder than a traditional database if you want to hide something that makes your value stored differently from what it really is
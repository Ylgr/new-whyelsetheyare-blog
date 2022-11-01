---
layout: blog
title: Open the world of Blockchain development - Chapter 1:Understand the math
  inside Cryptography
date: 2022-10-30T15:05:59.781Z
top_image: /images/uploads/101934929_p0.jpg
tags:
  - blockchain
  - crypto
  - EIP
categories:
  - blockchain
---
Being a store of worth thing meaning it must be strong to protect itself. This chapter we will get close to cryptography. The way they deal with sensitive information, and still keeping it public that everyone can verify it. Let's go!

<!-- more -->

# How you can keep the secret

On Blockchain or any other field that uses Cryptography or can be called Digital Signatures, there are two types of keys that go together, that is Private key and Public key.

Before Cryptography, we usually using fingerprint or written signature because we know only that person can make it (although it could be fake). In digital world, it still the same. If a message have a signature that you know it's Public key. You know the person created that without knowing the value of their Private key.

More than it, the scenario addition that you can send a secret message to owner of Public key by using that key to encrypt your message, then only it's owner can decrypt and read that message.

![](https://www.simplilearn.com/ice9/free_resources_article_thumb/alice.PNG)

It like Alice using Bob locker to lock her message on the box then send it to Bob. Then Box using his key to unlock that box and read message inside, no one else can read that message even Alice but why do she need it?

# Go deeper

Let's talk about a little bit about mathematical, the cryptography that stand behind of the mechanism above is Elliptic Curve Cryptography (ECC). It is a way of one-way math problem, easy to solve it one way, the other way is intractable. For example if you have a question about how 23144*12343, the answer will be easy one on calculator, it is 285666392. Then how to you revert from 285666392 to 23144 multiply by 12343? Impossible, right. 

ECC is not working exactly like that, for the easy one we could use the form:

> y2 = x3 + ax + b

This formula mean a straight line can only catch the curve line at most 3 point. We have P point then Q point on the line of curve, you will have R point like this:

![](https://matt-rickard.ghost.io/content/images/2022/03/Screen-Shot-2022-03-26-at-10.20.33-AM.png)

Then you drop R to other side of curve line to have R' like this:

![](https://matt-rickard.ghost.io/content/images/2022/03/Screen-Shot-2022-03-26-at-10.20.40-AM.png)

Now we connect two point P and R', it will create another straight line that can cross will curve line in new point that called S, then make S' and loop it over and over again then stop at a number of unknown time.

We have P . Q -> R then P . R' -> S then over and over again.

In this case we have P as public one n time of dot is private one so it will be challenge to find Q point if you only know the result.

And of cause, this formula has some limit time if it cause on special case.

![](https://matt-rickard.ghost.io/content/images/2022/03/Screen-Shot-2022-03-26-at-10.20.58-AM.png)

# Back to the Blockchain, where is it?

﻿Based on HD wallet architect, there are many wallet follow this rule:

![](/images/uploads/hd-wallet.drawio.png)

Here it is, can you see ECDSA? It stand for Elliptic Curve Digital Signature Algorithm and that is where we are using ECC.
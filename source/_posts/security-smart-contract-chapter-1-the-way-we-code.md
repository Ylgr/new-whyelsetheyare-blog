---
layout: blog
title: "Security smart contract - Chapter 1: The way we code"
date: 2023-04-03T14:21:41.397Z
top_image: /images/uploads/105230873_p0.jpg
tags:
  - smartcontractsecurity
categories:
  - Smart contract
---
In the past, we have warned about the perils of the dark forest and the risk of losing one's hard-earned money in the unpredictable world of crypto. However, it's not just your finances that are in danger - navigating the realm of crypto development can be equally treacherous. In this series, we will explore ways to safely traverse this mystical terrain and avoid the dangers that lurk in the shadows.

<﻿!-- more -->

# Do it in the code

## Error handling

![](https://storage.potatomedia.co/articles/potato_1a628609-4e8d-461f-9451-91ad9d899023_d720abe8065c56ddd4b96c552997a881ce9d79b1.png)

One of the most fundamental ways to prevent exceptions in your code is to use error handling, which can be accomplished through the use of the require(), assert(), and revert() functions. While all three of these functions can be used in various situations, there are some best practices that should be followed to ensure that your code is robust and error-free.

Firstly, the require() function is best used for checking input data, such as function parameters. For example, you could use it to check if a user has enough balance to complete a transaction, like so:

```
require(balanceOf(this) > transferAmount, "You don't have enough balance");
```

Secondly, the assert() function should only be used to verify the final result and should be reserved for handling internal errors. For example, you could use it to check if the balance of an address has been updated correctly after a transaction:

```
assert(address(this).balance == balanceBeforeTransfer - msg.value / 2);
```

Lastly, the revert() function should be used to throw exceptions and prevent execution of certain logic. For instance, you could use it to prevent a certain action from being taken if a system is not active:

```
if(isActive) {
 doSomething();
} else {
 revert("System has not been active")
```

By using these functions properly, you can ensure that your code is resilient to errors and operates smoothly under various circumstances.

\#﻿# Test

![](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTC0hXh-1042D6OZaRH6shEjSs_s7nSUfLtL28tsAy0DacEhLWJ-mStbEKA0aLIKi6HCOE&usqp=CAU)

When it comes to checking the correctness of your Solidity code, there are two common approaches: static testing and unit testing.

Static testing is an approach that is already built into the Solidity compiler. When you compile your Solidity code, the compiler will automatically check for errors and warnings in your code. If it finds any issues, it will provide you with detailed error messages and help you identify the source of the problem.

On the other hand, unit testing is a technique that allows you to simulate how your code will run in a controlled development environment. In unit testing, you write automated tests that verify that individual units of your code are functioning correctly. These tests can be run repeatedly, making it easier to catch errors and ensure that your code is robust and reliable.

Both static testing and unit testing are important tools for ensuring the correctness of your Solidity code. While static testing is helpful for catching errors early on in the development process, unit testing allows you to test your code in a more realistic environment and catch issues that might not be caught by static testing alone. Together, these approaches can help you build solid, reliable smart contracts that work as intended.
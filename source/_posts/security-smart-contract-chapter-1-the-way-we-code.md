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

# Error handling

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

# Test

![](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTC0hXh-1042D6OZaRH6shEjSs_s7nSUfLtL28tsAy0DacEhLWJ-mStbEKA0aLIKi6HCOE&usqp=CAU)

When it comes to checking the correctness of your Solidity code, there are two common approaches: static testing and unit testing.

Static testing is an approach that is already built into the Solidity compiler. When you compile your Solidity code, the compiler will automatically check for errors and warnings in your code. If it finds any issues, it will provide you with detailed error messages and help you identify the source of the problem.

On the other hand, unit testing is a technique that allows you to simulate how your code will run in a controlled development environment. In unit testing, you write automated tests that verify that individual units of your code are functioning correctly. These tests can be run repeatedly, making it easier to catch errors and ensure that your code is robust and reliable.

Both static testing and unit testing are important tools for ensuring the correctness of your Solidity code. While static testing is helpful for catching errors early on in the development process, unit testing allows you to test your code in a more realistic environment and catch issues that might not be caught by static testing alone. Together, these approaches can help you build solid, reliable smart contracts that work as intended.

# Managing

## Version control

Git is indeed a valuable tool for any developer, as it allows for efficient version control and collaboration on projects. One important practice when using Git is to create clear and informative pull requests. Pull requests should include a detailed description of the changes being made, the reasons for those changes, and any relevant context. This can help other team members understand the changes you are proposing and make the review process smoother.

Another important practice when using Git is to have at least one other reviewer to double check your work. This can help catch any logic bugs or other issues that may have been overlooked during the development process. Additionally, having multiple reviewers can help ensure that the code is consistent with the team's standards and best practices.

## Development environment

There are indeed many development frameworks available that can help make the development process smoother and more efficient. Some popular frameworks for developing smart contracts include:

* Truffle: Truffle is a development framework for Ethereum that provides tools for building, testing, and deploying smart contracts. It includes a suite of tools for managing your development workflow, as well as a testing framework that can help you ensure your contracts are functioning as intended.
* Hardhat: Hardhat is another popular development framework for Ethereum that provides similar tools to Truffle, as well as support for testing and debugging smart contracts. It also includes a plugin system that allows you to extend its capabilities with additional tools and features.
* Foundry: Foundry is a Rust-based smart contract development framework that provides a high-level, developer-friendly API for building smart contracts. It includes features like built-in testing and debugging tools, as well as support for multiple blockchain platforms.
* Vyper: Vyper is a smart contract development framework for Ethereum that is designed to be more secure and auditable than traditional smart contract languages like Solidity. It uses a simplified syntax and restricts certain features to reduce the risk of security vulnerabilities.

Ultimately, the choice of development framework will depend on a variety of factors, including your familiarity with the language and platform, the features and tools you need, and the specific requirements of your project. It's a good idea to evaluate several options and choose the one that best meets your needs and preferences.

## Documents

Documentation is an important part of the development process, as it helps to ensure that your code is understandable and maintainable over time. One way to document your Solidity code is through the use of comments, which can provide additional context and explanations for the code you are writing.

Solidity includes support for NatSpec, which is a natural language specification format that allows you to write comments in a standardized format. NatSpec comments can be used to provide descriptions of functions and their parameters, as well as other types of documentation.

To use NatSpec comments in your Solidity code, you can start your comment with a triple slash (`///`) and then write your documentation in a structured format. For example, you could document a function like this:

/

```
/// @dev Calculate the sum of two numbers
/// @param a The first number
/// @param b The second number
/// @return The sum of a and b
function add(uint256 a, uint256 b) public pure returns (uint256) {
    return a + b;
}

```

In this example, the `@dev` tag provides a description of the function, while the `@param` and `@return` tags describe the function's parameters and return value.

By using NatSpec comments to document your Solidity code, you can make your code more readable and understandable for other developers, as well as for your future self.

# Event monitor

Solidity provides an Event feature that allows you to emit events from your smart contract. Events are a way to signal to external applications that something has happened in the contract, and can be used to control the flow of logic and detect issues.

When you emit an event from your contract, you are essentially broadcasting a message to the outside world. This message can include information about what happened in the contract, such as the values of certain variables or the occurrence of a specific event.

One common use case for events is to track changes to the state of a contract. For example, you might emit an event whenever a user's balance is updated or a new token is minted. By doing so, you can provide a way for external applications to stay up to date with the state of the contract and react accordingly.

Another use case for events is to detect issues and debug your contract. By emitting events at key points in your code, you can track the flow of logic and identify potential issues or errors. You can then use these events to diagnose and fix problems, helping to ensure that your contract is functioning as intended.

Overall, events are a powerful feature in Solidity that can help you control the flow of logic and detect issues in your smart contract. By using events effectively, you can build more robust and reliable contracts that are better equipped to handle real-world scenarios.

# R﻿educe complex

One important principle to keep in mind when writing Solidity code (or any code, for that matter) is to keep it simple. This is often referred to as the KISS principle, which stands for "Keep it simple, stupid."

The idea behind the KISS principle is that simpler code is often easier to read, understand, and maintain than more complex code. By keeping your code simple, you can make it more approachable for other developers, reduce the risk of errors or bugs, and make it easier to modify or update in the future.

There are several ways to follow the KISS principle when writing Solidity code. One approach is to break down your code into smaller, more manageable functions, rather than trying to do everything in one large function. This can help make your code more modular and easier to read.

Another approach is to avoid unnecessary complexity in your code, such as using overly complicated data structures or algorithms. Instead, focus on writing code that is straightforward and easy to understand, even if it means sacrificing a bit of performance or efficiency.

Ultimately, following the KISS principle can help you build better Solidity code that is more reliable, maintainable, and effective in achieving its goals.
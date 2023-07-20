---
layout: blog
title: "Security smart contract - Chapter 6: Advance techniques"
date: 2023-07-20T05:30:02.878Z
top_image: /images/uploads/82092662_p0.jpg
tags:
  - smart-contract-security
categories:
  - Smart contract
---
To make sure your smart contract is security enough, its should be break test to check if its strong enough, throw it to the water to make sure security from wet and burn it in the fire for heat-resistant. This topic will show you how to make it by using some advance techniques like static analysis, fuzz testing and symbolic execution.

<!-- more -->

# Static analysis

In the past, many [rekt](https://rekt.news/) events happened because of the smart contract code is not security enough. For example before [The Dao](https://en.wikipedia.org/wiki/The_DAO_(organization)) hack, people never know about reentrancy attack. Then many other vulnerabilities like denial of service, integer overflow, etc. were exploited. To prevent this, we need to check the code before deploying it to the mainnet. And static analysis is solution for this.

Static analysis is a technique that scanning code to find vulnerable or not optimize code without executing it. One of the most popular tool for this is [Slither](https://github.com/crytic/slither).

![](https://raw.githubusercontent.com/crytic/slither/master/logo.png)

Overall, this kind of technique only detect the vulnerability that follow some example patterns. Its sound like advance, it's the most dumbly way to check the code. Here is the better way to check the code.

# Fuzz testing

Fuzz testing is a technique that generate random input to test the code. It's like a monkey that randomly press the keyboard to test the code. This technique is very popular in the software development. For example, [Google](https://www.google.com/) use this technique to test their [Chrome](https://www.google.com/chrome/) browser. And [Ethereum](https://ethereum.org/en/) use this technique to test their [Ethereum 2.0](https://ethereum.org/en/eth2/) client. Here is one of the real life related to fuzz testing:
- I go to the store to buy a new phone with 0 ETH.
- I go to the store to buy a new phone with 100 ETH get discount 10% become 110 ETH.
- I go to the store to buy a new phone with Max uint256 ETH get discount 10% become ... thanks god we are using 0.8.0 solidity compiler. So its detect the overflow and revert the transaction.
...

Fuzz testing in one of the main feature of Foundry make its become most powerful tool for smart contract security and development. The other tool for this is [Echidna](https://github.com/crytic/echidna).

![](https://raw.githubusercontent.com/crytic/echidna/master/echidna.png)

Well, fuzz testing not end here yet. There are two types of fuzz testing: stateless fuzz testing and stateful fuzz testing.

## Stateless fuzz testing

Stateless fuzz testing is a technique that generate random input to test the code and not care about the change that its make in the last execution. For example if I bring gun to the bank, its likely I will be arrested. But if I bring gun to the gun store, its likely I will be fine. Also, if I bring gun to the gun store then get certificated to keep it in the bank, its likely I will be fine too. This is the different between stateless fuzz testing and stateful fuzz testing.

## Stateful fuzz testing

Stateful fuzz testing is a technique that generate random input to test the code and care about the change that its make in the last execution. Here is the code example:

```solidity
pragma solidity ^0.8.0;

contract BasicFuzzy {
    uint256 public shouldAlwaysBeZero = 0;
    uint256 hiddenValue = 0;


    function doSomething(uint256 data) public {
        if(data == 0) {
            shouldAlwaysBeZero = 1;
        }
        if(hiddenValue == 7) {
            shouldAlwaysBeZero = 1;
        }
        hiddenValue = data;
    }
}
```

As you can see if `hiddenValue` is 7 then `shouldAlwaysBeZero` will be 1. So if we use stateless fuzz testing, we will never know about this. But if we use stateful fuzz testing, we will know about this and caught the bug.

# Formal verification and symbolic execution

Formal verification is a technique that prove the code is correct. You can understand its like fuzzy testing but instead of using random input, its using mathematic proof.

Symbolic execution is one of the technique that use in formal verification. Its a technique that execute the code with symbolic value.

![](https://www.researchgate.net/publication/314950910/figure/fig1/AS:701239067176962@1544199830648/Example-of-symbolic-execution-of-a-code.ppm)

Symbolic execution tools mostly using Z3 solver to solve the problem. Here is the example of symbolic execution:

```solidity
function safe_add(uint x, uint y) returns(uint z){
  z = x + y;
  require(z>=x);
  require(z>=y);
  return z;
}
```

If we use symbolic execution to execute this code, the test value will be in range `z = x + y AND (z >= x) AND (z=>y) AND (z < x OR z < y)`. So no value is in this range, the code will be safe. And its help us avoid the integer overflow.

Weakness of this technique is its take a lot of time to execute and its limited to smart contract that can check by computer. If you want to check the smart contract that can only check by human, you can't use this technique.



---
layout: blog
title: "Open the world of Blockchain development - Chapter 5: Trustless (consensus)"
date: 2022-11-08T03:41:07.553Z
top_image: /images/uploads/77643899_p0.png
tags:
  - blockchain
  - crypto
  - EIP
categories:
  - blockchain
---
Can you completely trust someone even though they are with you? Want but cannot, right? We are living in the world that most of situation is grey color, anyone or anything is your comrade today may turn in to your enemy tomorrow. Blockchain is a large system which was built by the community, how to make sure the last information set in Block is the truth?

<!-- more -->

# Byzantine fault tolerance

This is a traditional topic to check if a server can be inconsistently. In its simplest form, a number of generals are attacking a fortress and they must decide as a group whether to attack or retreat. Some generals may prefer to attack, while others prefer to retreat. The important thing is that all generals agree on a common decision, for a halfhearted attack by a few generals would become a [Rout](https://en.wikipedia.org/wiki/Rout "Rout"), and would be worse than either a coordinated attack or a coordinated retreat.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/f/fc/Byzantine_Generals.png/1920px-Byzantine_Generals.png)

In computer science field, we will make an election by using [ECC](https://en.whyelsetheyare.tk/2022/10/30/open-the-world-of-blockchain-development-chapter-1-how-blockchain-can-protect-your-value-cryptography/) to make unique signed vote of each general that can be easy verify (hard to fake).

The strategy is: First, we need to choose a decision is attack or retreat. For example we would choosing attack, then make a election with others generals. If number of vote that have same result as attack more than 2/3+1 vote, then attack is a final decision. Otherwise the election is stuck there so they will do nothing and continue the siege.

# The proof

Beside of BFT, we have others mechanism to keep the network trustless. They are: Proof of work (Bitcoin, 1st Blockchain generation), Proof of stake (Ethereum, 2nd generation), Delegated proof of stake (EOS, 3rd generation) and Proof of history (Solana).

## Proof of work

Blockchain's most known consensus is Proof of Work. An overview of how it works in the image below:

![](https://capital.com/files/glossary/-infographics-Proof-of-Work-PoW-.png)

The unique of PoW is miners need computer calculator power to find a hash for closing Block as soon as possible. This is requirement to have Block reward and transaction fee of that Block, complexity of find nonce to close Block hash has been updated once each two weeks to make sure miners sill took time to verify Block be close with block time.

The different thing with BFT is transaction only need 51% of approved network power to mark as success, if any Block that not follow mechanism of Blockchain, they will be fork to another Blockchain. So this solution problem is be forked many time because it is not be okay with fault node within.

## Proof of stake

Because required much power on calculating the nonce to close the Block, PoW be criticism because of power washing or non-environment friendly. Proof of Stake or PoS is a solution for this problem.

![](https://capital.com/files/glossary/-infographics-Proof-of-Stake-PoS-.png)

The main different between PoW and PoS is miner now need to stake their native token to have chance to be selected as Block's validator to get Block reward and transaction fees of that Block.

Now the game is changed, instead of calculating power race now become staking power race so it still keep the network safe as PoW and now reduce the cost of maintain network, is it? Not really, because of not requiring calculating power mean less people willing to run a Node. But we still have trade off for this problem is the network can be smother than PoW and it have more applicability to practice than PoW

## Delegated proof of stake

## Proof of history
+++
math = false 
meta = false
toc = false
author = "Royce"
title = "An Intro to Layer 2"
date = "2022-03-10"
category = "blockchain"
description = "Explaining the basics of Layer 2 chains"

+++

If you've been diving into blockchain development, you've likely been hearing about Layer 2s. If you've been confused, don't worry, it isn't as complicated as it seems. In this guide, we will explore the basics of Layer 2 and what it means for your applications and users.

<!--more-->

# What is Layer 2?

Layer 2 (L2) is a general term that refers to various solutions to scale Ethereum. Usually, this works by offloading transaction execution to the L2 protocol while regularly committing proof of the L2 transactions back to Ethereum (the Layer 1 or L1). Instead of lots of transactions being submitted individually, L2s “rollup” their transactions and submit them as a bundle to Ethereum. 

In this way, L2s compress thousands of transactions into just a few on an L1. This saves on gas fees and improves transaction speeds, all while leveraging Ethereum's security and decentralization.

L2s get around a key bottleneck of blockchain design. The gas costs of using Ethereum are socialized by all users of the L2. This means that as more people use the L2, it becomes cheaper to use for everyone. Compare this to Ethereum where more usage means higher fees and you can see why L2s are appealing.

L2s are the current plan for scaling Ethereum. Eventually, they will allow Ethereum to move from processing 10s of transactions per second to 1000s of transactions per second.

# Why develop on a Layer 2?

As a developer, there are plenty of reasons you might want to deploy on Layer 2 instead of the Ethereum main chain.

## You want cheaper transactions for you and your users

Transactions are much cheaper on an L2. This means your users will pay less in fees to use your application. For example, swaps on Ethereum can regularly be more than $10, [while on the L2s](https://l2fees.info/) they are around $1. Cheaper transactions also mean that you pay a lot less to deploy and run your contracts.

## You want a faster experience

L2 transactions are much faster to confirm than ones on Ethereum. This means that they can be better for apps that need to be fast or have high transaction throughput. Typical confirmation times for transactions on L2s are close to instant.

## You want to leverage more compute

Since transactions per second are higher and costs are lower, L2s are better for applications that will require more computing resources. For example, on-chain games or graphics are possible on L2s but would be prohibitively expensive on Ethereum.


# What are the types of Ethereum L2s?

There are various solutions available for developers looking to launch on an L2 network. Each has tradeoffs on security, speed, and user experience, so it is worth knowing the differences. 

There are two main types of Ethereum L2s: optimistic rollups and zero-knowledge rollups.


## Optimistic rollups

Optimistic rollups work by committing the signed call data of the L2 transactions back to Ethereum. Their name comes because transactions posted to an optimistic rollup are assumed valid. To stop fraud, anyone can submit proof of bad transactions and claim a reward from the network. If a validator commits fraud they are penalized by the network.

With this game theory of punishing committing fraud and rewarding proving fraud, optimistic rollups incentivize honest transactions.

One downside to optimistic rollups is that you need to wait longer for secure confirmations. Since transactions can be challenged well after submission, there are longer wait times to confirm transactions and withdraw from the rollup.

[Optimism](https://www.optimism.io/) and [Arbitrum](https://arbitrum.io/) are both optimistic rollups and among the most popular Ethereum L2s.


## Zero-knowledge rollups

Zero-knowledge rollups work by committing a proof of L2 transactions to Ethereum. With the L2 protocol, transactions are bundled together and the resulting changes to state are run through some fancy math to generate a validity proof. These proofs are then verified by a smart contract and committed to Ethereum.

Since many transactions can be included in a single validity proof, zero-knowledge rollups can save lots of gas and process a high number of transactions. Zero-knowledge rollups also have fast confirmation times because transactions are finalized as soon as the proof is submitted on Ethereum.

However, zero-knowledge rollups are not always directly compatible with the Ethereum Virtual Machine (EVM) and may require specialized languages or compilers to develop smart contracts.
[Polygon Hermez](https://hermez.io/) and [zkSync](https://zksync.io/) are both zero-knowledge rollups that have production networks running and are open for developers.

## Hybrid rollups, sidechains, and alternative L1s

While outside the scope of this article, there are plenty of other solutions that improve on the speed and scale of Ethereum and have different tradeoffs.

As the name suggests, hybrid L2s combine aspects of different rollup technologies.

Sidechains like [Polygon](https://polygon.technology/) run separate blockchains but are tied to Ethereum with a two-way peg of assets. These can be faster, but may not inherit all of the security of the main chain.

Alternative L1s run completely separate from Ethereum but often have bridge connections to move assets between chains. While other L1s often aim to be faster and cheaper than Ethereum, they may trade off on security and decentralization. The good news is that many [are EVM compatible](/writing/multichain-development/) making it very easy to use the smart contracts and developer tools from Ethereum to deploy on other L1s.

# How to choose an L2?

With all of the options, it can be a bit hard to decide which L2 would be the best fit for you to develop on. Here are some things you should consider:

## Will you need EVM compatibility?

Using an L2 that is EVM compatible can reduce development time and lets you reuse previous work on Ethereum. It also means you have access to a long list of development resources for EVM languages like Solidity or Vyper.

For example, Arbitrum is EVM compatible and you can directly reuse Ethereum contracts. Optimism is almost EVM compatible, but the OVM has slight differences and requires a specialized compiler to run Solidity code. ZkSync isn't yet EVM compatible and you have to write code in their language, Cairo, to develop smart contracts.

## Will you need fast withdrawals to the main net?

If your users need quick withdrawals from the L2 to mainnet, or your application requires quick finalization, you should consider your L2 carefully. For example, optimistic rollups have longer confirmation times and withdrawal periods than zero-knowledge rollups.

## Will your application use a lot of compute?

Very high numbers of transactions, the type of transaction and the amount of compute you will use can all factor into your choice of L2. Some rollups have advantages for speed, while others may be better for compute-heavy applications.

## What other applications do you need in the ecosystem?

One advantage of blockchain development is interoperability and the ability to use other applications running on the same chain. If you need other apps or money legos to run your application, you should consider this when choosing an L2. For example, Uniswap is currently deployed on the optimistic rollups Arbitrum and Optimism, but not yet available on the zero-knowledge rollups.

# Getting started developing on L2s

The various Layer 2 protocols have tried to make it as easy as possible for developers to start deploying contracts. The result is that you can leverage a lot of the tools used for developing on Ethereum.

For many L2s, a tool like Hardhat will let you test and deploy your contracts without hassle.
You can follow the Alchemy [tutorial](https://docs.alchemy.com/alchemy/tutorials/hello-world-smart-contract) on deploying a Hello World smart contract, and deploy to Arbitrum with just a few changes to your code.

In step 13, update your Hardhat configuration to include the Arbitrum network. Alchemy's free plan will give you an RPC node with archive mode and additional debug tools:

```
module.exports = {
  networks: {
    arbitrum: {
      url: 'https://arb-rinkeby.g.alchemy.com/v2/',
    }
  },
}
```

During step 16, deploy to the Arbitrum:

`npx hardhat run scripts/deploy.js --network arbitrum`

As you can see, it is pretty easy to get started with basic contracts on an L2. However, all L2s have slight differences, so it is important to understand these and plan for them in your development.

Hopefully, you now have a better understanding of what L2s are and some considerations for developing on them. You can take a look at [my tutorial on multichain development](/writing/multichain-development/) for more tips on using Hardhat and EVM developer tools for other chains. 

# More Reading
- [Ethereum.org Layer 2 Explainer](https://ethereum.org/en/developers/docs/scaling/layer-2-rollups/)
- [Vitalik’s Incomplete Guide to Rollups](https://vitalik.ca/general/2021/01/05/rollup.html)
- [Arbitrum Developer Documentation](https://developer.offchainlabs.com/docs/developer_quickstart)
- [Optimism Community Documentation Site](https://community.optimism.io/)


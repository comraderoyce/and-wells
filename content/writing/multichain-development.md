+++
math = false 
meta = false
toc = false
author = "Royce"
title = "Multichain Development with Hardhat and Remix"
date = "2021-11-19"
categories = ["blockchains"]
description = "How to use Hardhat and Remix to develop and test on Fantom and other EVM blockchains"
collections = ["blockchain"]
+++

Many blockchains are EVM compatible and you can deploy contracts written in Solidity to these chains. Here is how to do local development and testing for basic contracts on other chains using Hardhat and Remix.

<!--more-->

## Introduction

Most code for the Ethereum Virtual Machine (EVM) is written in Solidity. Beyond Ethereum, many other chains are essentially forks of `geth` and the EVM. This is useful for us as it makes it straightforward to use Solidity and similar build methods to write and deploy contracts on these chains. 

We will set up a local fork of the Fantom mainnet, write a short contract, and deploy it to our local fork for testing. 

## Set up hardhat

[Hardhat](https://hardhat.org/) is Solidity development tooling that makes it easy to develop, test, and deploy smart contracts. For our purposes, we will use the ability to do a local fork of a mainnet for development and testing.

The mainnet fork is a powerful feature of hardhat that lets you create an exact copy of the current chain state that lives locally on your machine. This lets you develop and test deployments of contracts before even going to a test net. It has other neat features like auto-funding testing accounts and forking from a given block height. Yet my favorite feature is the ability to easily fork the mainnets of other EVM-compatible chains. 

Since hardhat forking is based on pulling state from a running node, we can point the hardhat configuration to fork from any EVM compatible node. 

To do this in forking mode, set up your hardhat configuration as shown below. 

```json 
networks: {
    hardhat: {
      chainId: 1337,
      forking: {
        url: "https://rpc.ftm.tools/",
        chainId: 1337,
      }
    }
}
```

This example above is for Fantom, but this generalizes to other EVM chains with a remote RPC, a local node, or a node-as-a-service RPC like [Alchemy](alchemy.com).

```json
forking: {
  url: "https://polygon-mainnet.g.alchemy.com/v2/<apikey>",
  chainId: 137,
  blockNumber: 10000000,
}
```

Run the hardhat command to start a local fork: 

```sh
$ npx hardhat node
```

This will make an EVM instance with funded test accounts, all running on your local machine.

## Write a smart contract

Since many of the large protocols on other EVM chains are forks, it is often easy to move code over from one EVM chain to another. 

On Fantom, the two largest exchanges are [Spooky Swap](https://spookyswap.finance/) and [Spirit Swap](https://www.spiritswap.finance/). Since they are both forks of Uniswap, we can interact with their contracts on Fantom using many of the same Uniswap ABIs and interfaces. In this case, we will use one of the router contract functions to check the price of a swap from the exchange token to Fantom. We could use this later in an arbitrage or keeper bot. 

``` sol
// SPDX-License-Identifier: GPL-3.0

pragma solidity >=0.7.0 <0.9.0;

/** 
 * @title CheckPools
 * @dev Checks a swap from BOO or SPIRIT to FTM for a given amount
 */

interface IRouter {
    function getAmountsOut(uint amountIn, address[] memory path) external view returns (uint[] memory amounts);
}

address constant wftmAddress = 0x21be370D5312f44cB42ce377BC9b8a0cEF1A4C83;
address constant booTokenAddress = 0x841FAD6EAe12c286d1Fd18d1d525DFfA75C7EFFE;
address constant spiritTokenAddress = 0x5Cc61A78F164885776AA610fb0FE1257df78E59B;
address constant booRouterAddress = 0xF491e7B69E4244ad4002BC14e878a34207E38c29;
address constant spiritRouterAddress = 0x16327E3FbDaCA3bcF7E38F5Af2599D2DDc33aE52;

contract checkPools {
    IRouter booRouter = IRouter(booRouterAddress);
    IRouter spiritRouter = IRouter(spiritRouterAddress);

    function fantomBoo(uint amount) public view returns (uint[] memory _amountOut) {
        uint _amount = amount;
        address[] memory path = new address[](2);
        path[0] = booTokenAddress; 
        path[1] = wftmAddress;
        _amountOut = booRouter.getAmountsOut(_amount, path);
        return (_amountOut[1]);
    }

    function fantomSpirit(uint amount) public view returns (uint[] memory _amountOut) {
        uint _amount = amount;
        address[] memory path = new address[](2);
        path[0] = spiritTokenAddress; 
        path[1] = wftmAddress;
        _amountOut = spiritRouter.getAmountsOut(_amount, path);
        return (_amountOut[1]);
    }
}   
```

The contract uses the `getAmountsOut` function from the [Uniswap Router interface](https://docs.uniswap.org/protocol/V2/reference/smart-contracts/library#getamountsout) to simulate a swap from one token to another. We have the relevant token addresses and the router contracts hard coded in to the contract. Then we have some basic logic to intialize the contract interfaces for Spooky and Spirit routers. Last are two functions that take unit numbers as inputs and output the expected amount of Fantom tokens. We return the second array entry, which is the expected tokens output from our amount. 

## Deploy to a mainnet fork with Remix

Remix is a browser-based IDE for developing smart contracts. While hardhat has a powerful setup, Remix has an easy UI and is a quick way for beginners to write and deploy contracts. With Remix, you can write and compile your contracts from your browser.

To set up Remix with your local forked node, go to the Deploy & Run Transactions tab, change the Environment to Web3 Provider, then input the local RPC server URL; by default, this will be `http://127.0.0.1:8545/`. 

Remix will connect to your node and load up the funded test wallets.

Deploying is as easy as selecting your funded account, choosing your contract, and clicking deploy. 


## Test your smart contracts on a mainnet fork

Once the contract is deployed to your local mainnet fork, you can query it or submit transactions to test functionality. 

Remix provides a simple UI to query your contracts once they are deployed.

We can also use any other suite of EVM compatible toolsets to test our contracts. I like [dapptools](/writing/dapptools-m1/) for their command-line interface `seth`. 

With `seth` we can query our deployed contract. The address you can copy from the Remix deploy panel. 

```sh
$ export address=
$ seth call $address 'fantomBoo(uint)(uint[])' $(seth --from-wei 1)
```

Keep in mind that the queries for the contract above are against your local fork and so could be a bit out of date. Restart your hardhat fork to get the latest data.

## Other notes

- Developing in Solidity and deploying to other chains is a much cheaper practice for devs than trying to work on Ethereum. For example, it is only a few cents to deploy a simple contract to Fantom. 
- Most large protocols have direct forks or are deployed on multiple chains at this point, so you can work similar bot and arbitrage strategies across chains. 
- The underlying `geth` is usually the same, but chains have subtle differences in execution that you sometimes have to work around.
- I've been able to develop working contracts with just a remote RPC and the mainnet fork setup described above. All of the workflows are improved with a local node instead of a remote RPC.
- Most of the "newer" EVMs and associated tooling have functionality for a mainnet fork.
    - `ganache-cli --fork https://rpc.ftm.tools/`
- Using an archive node with hardhat gives you debug_traceTransaction that you can use in the step-through debugger in Remix.
- Running a node gets you some extra features for transactions not available from an RPC connection. For example, you can [submit lower gas transactions](https://github.com/Fantom-foundation/go-opera/blob/10ca669279e26d21133c1d95db26ea41a6479360/evmcore/tx_pool.go#L587) and [add more transactions to the pool](https://github.com/Fantom-foundation/go-opera/blob/10ca669279e26d21133c1d95db26ea41a6479360/evmcore/tx_pool.go#L1304).
- You can set a custom RPC in MetaMask with the information from your mainnet fork. Then import one of the funded test wallets. This lets you interact with other dapps and contracts from MetaMask. You can also use the injected Webe3 provider from MetaMask for your Remix environment.

## Useful links

- [Hardhat mainnet forking documentation](https://hardhat.org/hardhat-network/guides/mainnet-forking.html)
- [Remix deploy & run documentation](https://remix-ide.readthedocs.io/en/latest/run.html)


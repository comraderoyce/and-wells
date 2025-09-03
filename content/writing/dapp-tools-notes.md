+++
math = false 
meta = false
toc = false
author = "Royce"
title = "dapptools notes"
date = "2021-09-16"
categories = ["notes"]
description = "Notes on working with dapptools"
draft = true
collections = ["blockchain"]

+++

Notes on working with dapptools, particularly how to use `seth`, the command-line utility for interacting with blockchains. 

<!--more-->



## How to use seth with different chains

You can use `seth` to interact with other EVM based blockchains by changing the RPC URL. For example, to change the network to query the chain and send transactions on Fantom:

```sh
# use seth with Fantom
export ETH_RPC_URL=https://rpcapi.fantom.network
```

## Helper commands

The `--from-wei` and the `--to-wei` utilities are quite useful when dealing with the large number conversions usually necessary for interacting with contracts. Combine this with nested queries and you get useful results.    For example, to check current gas prices in gwei:

```sh
seth --from-wei $(seth gas-price) gwei
```
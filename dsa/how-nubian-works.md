---
description: Get an overview of the whole Nubian ecosystem in a jiffy.
---

# How Nubian Works

Nubian Finance is a Decentralized Finance \(DeFi\) aggregator, it leverages different DeFi protocols to give the average crypto user a simple DeFi experience. It is currently deployed on the Binance Smart Chain and makes extensive use of DeFi Smart Accounts \(DSA\) _\*\*_simply called a smart account.

## **DeFi Smart Accounts**

To start interacting with Nubian Finance, each user will have to create a smart account. The smart account acts as a middle man between the user's wallet and the rest of the Nubian Ecosystem. The smart account holds the users crypto assets and is used to interact with different DeFi protocols. It's like a bank account but with all the features of decentralization and is completely controlled by only the user.

## Extensions

The smart accounts themselves are proxy contracts, they make use of other contracts called extensions \(implementations\) to execute every functionality. These extensions are separate contracts that contain the actual implementation code. They can be added to every smart account using the [NbnImplementations](dsa-introduction/core/nbnimplementations.md) contract. The contract records all available extensions and helps the smart account to select the right extension to execute a function call.

## Connectors

For the smart account to interact with DeFi protocols it uses an extension that in turn interacts with separate contracts called connectors. Connectors are smart contracts that allow smart accounts to interact with various DeFi protocols. [NbnImplementationsM1](dsa-introduction/implementations/nbndefaultimplementation.md) is the extension that extends the smart accounts to support the use of connectors. Each call to a protocol done using NbnImplementationsM1 is called a **spell** and multiple spells can be combined to be **cast** \(execute a spell\) in a single transaction. This allows for very simple actions and even complex actions can be done using different DeFi protocols. These connectors are built for each DeFi protocol and implement specific functions needed to interact with a DeFi protocol. So connecting smart accounts to a new DeFi protocol simply just involves adding a new connector for that protocol.

## The flow of a simple swap on Pancakeswap

{% hint style="info" %}
Every call to a DeFi protocol follows the same process below.
{% endhint %}

1. The user creates a smart account if he doesn't have one already.
2. The smart account is funded with the token to be swapped if it isn't there already.
3. The user enters the amount of the token he wants to swap and other necessary parameters and calls `cast` on the smart account.
4. The smart account finds the extension that implements `cast`  \([NbnImplementationsM1](dsa-introduction/implementations/nbnimplementationm1.md)\) and passes the data to it.
5. NbnImplementationsM1 finds the Pancakeswap connector and casts the swap spell using the connector.
6. The Pancakceswap connector interacts with Pancakeswap and completes the swap spell.

We offer an **SDK** that handles all the blockchain connections and leaves you to just cast spells from your browser or node backend. It helps you concentrate on just the user interface and to deliver a nice user experience to your users.


---
description: Get an overview of the whole Nubian ecosystem in a jiffy.
---

# How Nubian Works

Nubian Finance is a Decentralized Finance (DeFi) aggregator, it leverages different DeFi protocols to give the average crypto user a simple DeFi experience. It is currently deployed on the Binance Smart Chain.

Nubian Finance uses a proxy contract called a **wizard** and a group of contracts called **connectors** to route transactions across different protocols, each connector is protocol specific. The wizard receives the transaction from your address, the transaction will contain one or more calls to each connector, each call is called a **spell. **The wizard casts each spell by sending it to the specified connector which in turn interacts with its protocol.

This mechanism allows Nubian to execute various strategies by interacting with different protocols in a single transaction.

{% hint style="info" %}
Nubian still lets users use their addresses to interact directly with some protocols that require external wallet addresses to interact directly with them.
{% endhint %}

### Wizard

This is a proxy contract that receives the transaction sent from the Nubian frontend. It receives the transaction from the user and casts all the spells in the transaction using different connectors. The Wizard casts each spell using a `delegatecall` to the spells connector.

### Connectors

This is a group of contracts that hold the logic the wizard uses in connecting with various protocols. Each protocol has its own connector. Each connector has a function that interacts with the DeFi protocol to perform each major function of the protocol. The connector also formats the inputs it receives before it sends them to the protocol.

## The flow of a simple token swap on Pancakeswap

{% hint style="info" %}
Every call to a DeFi protocol follows the same process below.
{% endhint %}

1. The user interacts with the Nubian frontend which sends a transaction containing a deposit swap and withdrawal spells to the wizard.
2. The wizard casts the deposit spell by delegate calling the deposit connector which transfers the token to itself. It must already be approved to spend the amount to be swapped.
3. It casts the swap spell by delegate calling the Pancakeswap connector which in turn calls the Pancakeswap router and completes the swap spell with the token it got as a deposit.
4. It casts the withdraw spell by delegate calling the withdraw connector which sends the token swapped from the Wizards balance to the user.

The process above is done for almost every protocol that Nubian interacts with. To interact with multiple protocols in one spell, multiple spells that interact with each of those protocols are sent in their sequential order of interaction to the wizard.

We offer an **SDK** that handles all the blockchain connections and leaves you to just cast spells from your browser or node backend. It helps you concentrate on just the user interface and to deliver a nice user experience to your users.

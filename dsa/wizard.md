---
description: Welcome let us show you how we cast spells here at Nubian.
---

# 🧙♂ Wizard

The wizard is the main contract that users interact with almost every time they do a transaction on Nubian. It is a proxy contract that directs each call to a DeFi protocol to a connector which formats inputs and sends them to its DeFi protocol.&#x20;

Like every wizard, the Nubian wizard casts spells. Each spell is a call to a DeFi protocol. These spells are achieved using connectors which are separate contracts that interact with a DeFi protocol. Almost every protocol that Nubian interacts with has its own connector.&#x20;

## Address

The Wizard contract is deployed on [mainnet](https://bscscan.com/address/0x9B1240399e9E23e4C31520fc5C00FA83dc451819).

## Events

### LogCast

```solidity
    event LogCast(
        address indexed origin,
        address indexed sender,
        uint256 value,
        string[] targetsNames,
        address[] targets,
        string[] eventNames,
        bytes[] eventParams
    );
```

This emits all the events from all the connectors involved in casting the spells in a cast transaction.

## Code

[main.sol](https://github.com/NestcoinCo/Nubian-coven/blob/main/contracts/wizard.sol)

## Read-only-methods

### Connectors

```solidity
address public immutable connectors;
```

Returns the address of the contract that holds the list of approved connectors.

Spe

---
description: Start performing simple to complex DeFi transactions using Javascript.
---

# Cast

The SDK allows developers to interact with Nubian smart contracts easily from their node backend or from the frontend. The SDK just receives the function parameters and handles the rest, from instantiating the Nubian contracts to calling them and returning the output received or error raised. &#x20;

### Casting Spells

**Spells** denote a sequence of connector functions that will achieve a given use case. Spells can comprise any number of functions across any number of connectors. The spells are cast by the Nubian **Wizard** contract.

The wizard contract receives the spells from the Externally Owned Account (EOA) calls their respective connectors which in turn interact with the DeFi protocol it is associated with. All these are done in a single transaction.&#x20;

With this SDK, performing DeFi operations on your dapp consists of creating a `spells` instance to add transactions. Here is where you can initiate complex transactions amongst different protocols.

Create an instance:

```javascript
let spells = nub.Spell()
```

Add **spells** that you want to execute. Think of any action, and by just adding new **spells**, you can wonderfully **cast** transactions across protocols. Let's swap USDC TO BUSD on Pancakeswap using the SDK. This will involve three steps:

1. Deposit USDC in the wizard contract.
2. Swap USDC to BUSD on Pancakeswap using the Wizard.
3. Withdraw BUSD from the wizard contract.

{% hint style="warning" %}
Here are a few important things to note about using the SDK:

1. The Wizard acts as a middleman between the EOA and the protocols so it is required that the Wizard has the funds to be used in casting the spells else the transaction will fail. **Deposit spell(s)** that send the funds for all the spells should start the spells. The wizard contract should already have the approval to spend the EOAs funds before the Deposit spell is cast.
2. **Withdrawal spell(s)** should always be called to remove all the funds received by the wizard in the transaction to prevent the loss of funds. It is recommended to always use the max value of uint256 type in Solidity to remove the complete balance of the Wizard. E.g since Pancakeswap sees the Wizard contract as the caller of the transaction, it sends the swapped funds to it. A withdrawal spell on the Deposit connector should remove these funds.
3. Some Protocols like Autofarm use **`msg.sender`** to keep a record of account deposits. If the Wizard contract is used it would be recorded as the depositor instead of the original account owner. For protocols like this, the EOA is required to interact directly with these protocols. The SDK provides functions that cover this.
{% endhint %}

```javascript
let spells = nub.Spell()

// the Wizard is a middleman between you and the protocol
// it has to have been approved to spend the amount you are depositing

// approve Wizard to spend USDT [Check utilities on how to use approve]
await nub.erc20.approve("0x55d398326f99059ff775485246999027b3197955");

// passing this value as the amount in any connector input uses the maximum balance
const max = "0xffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff";

// Send USDT to Wizard
spells.add({
  connector: "BASIC-A",
  method: "deposit",
  args: [
    "0x55d398326f99059ff775485246999027b3197955", // USDT address
    "1000000000000000000", // 1 USDT (10^18 wei)
    0,
    0
  ]
})

// swap USDT for BUSD on Pancakeswap
spells.add({
  connector: "PancakeV2",
  method: "sell",
  args: [
    "0xe9e7cea3dedca5984780bafc599bd69add087d56", // BUSD address
    "0x55d398326f99059ff775485246999027b3197955", // USDT address
    "1000000000000000000", // USDT sent to Wizard
    1, // indicates slippage
    0,
    0
  ]
})

// withdraw BUSD from Wizard
spells.add({
  connector: "BASIC-A",
  method: "withdraw",
  args: [
    "0xe9e7cea3dedca5984780bafc599bd69add087d56",
    max, // max BUSD sent to Wizard from swap spell
    "0x0", // address to receive BUSD
    0,
    0
  ]
})
```

At last, cast your spell using `cast()` method.

```javascript
// in async functions
let transactionReceipt = await spells.cast()

// or
spells.cast().then(console.log) // returns a transaction receipt
```

You can pass an object to send **optional** parameters like sending ETH along with the transaction.

```javascript
spells.cast({
  gasPrice: web3.utils.toWei(gasPrice, 'gwei'), // in gwei, used in node implementation.
  value: '1000000000000000000', // sending 1 BNB along with the transaction.
  nonce: nonce,
})
```

Here are the optional parameters.

| **Parameter (optional)** | **Type**        | **Description**                                                                                                                                                                |
| ------------------------ | --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| gasPrice                 | `string/number` | The gas price in gwei. It is required in Node environments to configure the transaction confirmation speed.                                                                    |
| value                    | `string/number` | Amount of BNB which you want to send along with the transaction (in wei). Used when you want to deposit BNB.                                                                   |
| nonce                    | `string/number` | Nonce of your sender account. Mostly used in Node implementation to send transaction with a particular nonce either to override unconfirmed transaction or some other purpose. |

This will send the transaction to blockchain in node implementation (or ask users to confirm the transaction on web3 wallets like Metamask).

## Connectors

| **Name**                                                                   | **Address**                                |
| -------------------------------------------------------------------------- | ------------------------------------------ |
| ****[**BASIC-A**](../connectors/available-connectors/basic.md)****         | 0xC2e1c0fc0A2c0126AD5222D6eB2453c6aEc1e637 |
| [**PancakeV2**](../connectors/available-connectors/pancakeswap.md)         | 0x546bde105B24147bbd34F3147a0FD68961515Feb |
| [**VenusV2**](../connectors/available-connectors/venus.md)                 | 0xB03308Fa6A1Ecb489ECC86B7e930491020ee2b96 |
| [**Nubian Staking**](../connectors/available-connectors/nubian-staking.md) | 0x0764C090a14E45Ae23F69732BeB28504f89D669A |

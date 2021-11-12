---
description: Start performing simple to complex DeFi transactions using Javascript.
---

# Cast

### Casting Spells

**Spells** denotes a sequence of connector functions that will achieve a given use case. Spells can comprise any number of functions across any number of connectors. The spells are cast by the Nubian **Wizard** contract.&#x20;

The wizard contract receives the spells from the Externally Owned Account (EOA) calls their respective connectors which in turn interact with the DeFi protocol it is associated with.&#x20;

{% hint style="warning" %}
Here are a few important things to note about using the SDK:

1. The Wizard acts as a middleman between the EOA and the protocols so it is required that the Wizard has the funds to be used in casting the spells else the transaction will fail. **Deposit spell(s)** that send the funds for all the spells should start the spells. The wizard contract should already have the approval to spend the EOAs funds before the Deposit spell is cast.
2. At the end of each transaction, **withdrawal spell(s)** should remove all the funds received by the wizard to prevent the loss of funds. It is recommended to always use **`uint(-1)`**, the max value of the uint256 type in Solidity to remove all the complete balance of the Wizard. E.g since Pancakeswap sees the Wizard contract as the caller of the transaction, it sends the swapped funds to it. A withdrawal spell on the Deposit connector should remove these funds.
3. Some Protocols like Autofarm use **`msg.sender`** to keep a record of account deposits. If the Wizard contract is used it would be recorded as the depositor instead of the original account owner. For protocols like this, the EOA is required to interact directly with these protocols. The SDK provides functions that cover this.
{% endhint %}

With this SDK, performing DeFi operations on your dapp consists of creating a `spells` instance to add transactions. Here is where you can initiate complex transactions amongst different protocols.

Create an instance:

```javascript
let spells = nub.Spell()
```

Add **spells** that you want to execute. Think of any action, and by just adding new SPELLS, you can wonderfully CAST transactions across protocols. Let's try to execute the following actions:

1. Deposit 1 USDC in the wizard contract.
2. Swap USDC to BUSD on Pancakeswap.
3. Withdraw BUSD from the wizard contract.

```javascript
let spells = nub.Spell()

//send USDT to Wizard
spells.add({
  connector: "BASIC-A",
  method: "deposit",
  args: [
    "0x55d398326f99059ff775485246999027b3197955", //USDT address
    "1000000000000000000", // 1 USDT (10^18 wei)
    0,
    0
  ]
})

//swap USDT for BUSD on Pancakeswap
spells.add({
  connector: "PancakeV2",
  method: "sell",
  args: [
    "0xe9e7cea3dedca5984780bafc599bd69add087d56", //BUSD address
    "0x55d398326f99059ff775485246999027b3197955", //USDT address
    "1000000000000000000", // USDT sent to Wizard
    1, //indicates slippage
    0,
    0
  ]
})

//withdraw BUSD from Wizard
spells.add({
  connector: "BASIC-A",
  method: "withdraw",
  args: [
    "0xe9e7cea3dedca5984780bafc599bd69add087d56",
    "0xffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff",
   //max BUSD sent to Wizard from swap spell
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
spells.cast().then(console.log) // returns transaction receipt
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
| gasPrice                 | `string/number` | The gas price in gwei. Mostly used in Node implementation to configure the transaction confirmation speed.                                                                     |
| value                    | `string/number` | Amount of BNB which you want to send along with the transaction (in wei). Used when you want to deposit BNB.                                                                   |
| nonce                    | `string/number` | Nonce of your sender account. Mostly used in Node implementation to send transaction with a particular nonce either to override unconfirmed transaction or some other purpose. |

This will send the transaction to blockchain in node implementation (or ask users to confirm the transaction on web3 wallets like Metamask).

### Transaction History

You can see the list of transactions by an address:

```javascript
nub.getAccountTransactions("0x00");
```

Replace `0x0` with the address of the EOA.

### Eth and token Transfer

You can transfer tokens using the transferToken function.

```javascript
nub.transferToken(_tokenAddress, _recipient, _amount);
```

for Eth transfers, make use of the transferEth function.

```javascript
nub.transferEth(_recipient, _amount);
```

### Approval

You can approve the wizard contract to spend tokens on behalf of the user by calling the approve or infiniteApprove functions.

```javascript
nub.infiniteApprove(_tokenAddress);
```

```js
nub.approve(_tokenAddress, _amount);
```

## Connectors

| **Name**                                                                   | **Address**                                |
| -------------------------------------------------------------------------- | ------------------------------------------ |
| ****[**BASIC-A**](../connectors/available-connectors/basic.md)****         | 0xC2e1c0fc0A2c0126AD5222D6eB2453c6aEc1e637 |
| [**PancakeV2**](../connectors/available-connectors/pancakeswap.md)         | 0x546bde105B24147bbd34F3147a0FD68961515Feb |
| [**VenusV2**](../connectors/available-connectors/venus.md)                 | 0xB03308Fa6A1Ecb489ECC86B7e930491020ee2b96 |
| [**AutofarmV2**](../connectors/available-connectors/autofarm.md)           | 0x82aB4bCD90E99f31a90201669AACC6867c9c3B77 |
| [**Nubian Staking**](../connectors/available-connectors/nubian-staking.md) | 0x0764C090a14E45Ae23F69732BeB28504f89D669A |

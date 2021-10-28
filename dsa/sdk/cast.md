---
description: Start performing simple to complex DeFi transactions using Javascript.
---

# Cast

### Casting Spells

**Spells** denotes a sequence of connector functions that will achieve a given use case. Spells can comprise any number of functions across any number of connectors.

With this SDK, performing DeFi operations on your dapp consists of creating a `spells` instance to add transactions. Here is where you can initiate complex transactions amongst different protocols.

Create an instance:

```javascript
let spells = dsa.Spell()
```

Add **spells** that you want to execute. Think of any action, and by just adding new SPELLS, you can wonderfully CAST transactions across protocols. Let's try to execute the following actions:

1. Deposit 1 BNB in the DSA.
2. Deposit 1 BNB in Venus protocol.
3. Borrow 100 USDC from Venus.
4. Deposit borrowed USDC in Venus.

```javascript
// Deposit BNB in DSA

spells.add({
  connector: "BASIC-A",
  method: "deposit",
  args: [
    "0xEeeeeEeeeEeEeeEeEeEeeEEEeeeeEeeeeeeeEEeE",
    "1000000000000000000", // 1 BNB (10^18 wei)
    0,
    0
  ]
})


// Deposit BNB in Venus

spells.add({
  connector: "VenusV2",
  method: "deposit",
  args: [
    "BNB-A",
    "1000000000000000000", // 1 BNB (10^18 wei)
    0,
    0
  ]
})

// Borrow USDC from Venus

spells.add({
  connector: "VenusV2",
  method: "borrow",
  args: [
    "USDC-A",
    "100000000000000000000", // 100 USDC (10^18 wei)
    0,
    0
  ]
})

// Deposit USDC in Venus

spells.add({
  connector: "VenusV2",
  method: "deposit",
  args: [
    "USDC-A",
    "100000000000000000000", // 100 USDC (10^18 wei)
    0,
    0
  ]
})
```

At last, cast your spell using `cast()` method.

```javascript
// in async functions
let transactionReceipt = await spells.cast({value: "1000000000000000000"})

// or
spells.cast().then(console.log) // returns transaction receipt
```

You can pass an object to send **optional** parameters like sending ETH along with the transaction as we did above to deposit in the DSA.

```javascript
spells.cast({
  gasPrice: web3.utils.toWei(gasPrice, 'gwei'), // in gwei, used in node implementation.
  value: '1000000000000000000', // sending 1 BNB along with the transaction.
  nonce: nonce,
})
```

Here are the optional parameters, they have the same defaults as their counterparts in `dsa.build()`.

| **Parameter (optional)** | **Type**        | **Description**                                                                                                                                                                |
| ------------------------ | --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| gasPrice                 | `string/number` | The gas price in gwei. Mostly used in Node implementation to configure the transaction confirmation speed.                                                                     |
| value                    | `string/number` | Amount of BNB which you want to send along with the transaction (in wei).                                                                                                      |
| nonce                    | `string/number` | Nonce of your sender account. Mostly used in Node implementation to send transaction with a particular nonce either to override unconfirmed transaction or some other purpose. |

This will send the transaction to blockchain in node implementation (or ask users to confirm the transaction on web3 wallets like Metamask).

## Connectors

| **Name**                                                                   | **Address**                                |
| -------------------------------------------------------------------------- | ------------------------------------------ |
| [**B**](../connectors/available-connectors/basic.md)**asic**               | 0xC2e1c0fc0A2c0126AD5222D6eB2453c6aEc1e637 |
| [**PancakeV2**](../connectors/available-connectors/pancakeswap.md)         | 0x546bde105B24147bbd34F3147a0FD68961515Feb |
| [**VenusV2**](../connectors/available-connectors/venus.md)                 | 0xB03308Fa6A1Ecb489ECC86B7e930491020ee2b96 |
| [**AutofarmV2**](../connectors/available-connectors/autofarm.md)           | 0x82aB4bCD90E99f31a90201669AACC6867c9c3B77 |
| [**Nubian Staking**](../connectors/available-connectors/nubian-staking.md) | 0x0764C090a14E45Ae23F69732BeB28504f89D669A |

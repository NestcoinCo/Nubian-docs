---
description: Start creating smart accounts with simple Javascript calls.
---

# Setup Account

Every user needs to create a Smart Account to interact with DeFi Protocols seamlessly; this allows developers to build extensible use-cases with maximum security and composability. You can also create multiple accounts for a single address.

To get started using the SDK, you must do one or all of the following:

* Create Smart Account - `build()`
* Fetch Smart Accounts - `getAccounts()`
* Set Smart Account - `setInstance()`

## build\(\)

This creates a uniquely numbered Smart Account which acts as a proxy to interact with verified DeFi protocols and each DSA has a unique ethereum address. If the account is already created, you can use the `setInstance` method to activate a paricular DSA account and start casting spells.

```javascript
// in async functions
await dsa.build()

// or
dsa.build().then(console.log)
```

The build method also accepts optional parameters as shown below:

```javascript
dsa.build({
  gasPrice: gasPrice // estimated gas price
  origin: origin,
  authority: authority,
})
```

> View this [Gist](https://gist.github.com/nonseodion/39f9c7a46b122131e8cec95ad4350cf0) for estimation of gas price

### Parameters

| **Parameter** | **Type** | **Description** | **Default** |
| :--- | :--- | :--- | :--- |
| gasPrice | `string/number` | The gas price in gwei. Mostly used in Node implementation to configure the transaction confirmation speed. | Not optional in Node and estimated in other modes. |
| origin | `address` | The address to track the origin of the transaction. Used for analytics and affiliates. | `0x0` |
| authority | `address` | The DSA authority. This is the address to be added as an authority. An authority has control over the DSA created. | Address of the connected wallet, private key address or public key in Browser, Node and Simulation modes respectively. |
| from | `address` | The account with which you want to create your DSA. This is helpful to create DSA for other addresses. | Same as the authority parameter. |
| nonce | `string/number` | Nonce of your sender account. Mostly used in Node implementation to send a transaction with a particular nonce either to override unconfirmed transaction or some other purpose. | Used only in Node. |
| version | `string/number` | The DSA version to create. | 2 |

### Returns

This function returns a promise that resolves to the transaction receipt when the transaction is mined.

## getAccounts\(\)

Fetch all the accounts owned by an ethereum address by calling `getAccounts()`.

```javascript
// in async functions
await dsa.getAccounts(address)

// or
dsa.getAccounts(address).then(console.log)
```

### Parameter

| **Parameter** | **Type** | **Description** |
| :--- | :--- | :--- |
| address | `address` | An ethereum address. |

### Returns

The method returns a Promise that resolves to an array of objects with all the DSA accounts where `address` is authorised. Here's how it looks:

```javascript
[
  {
      id: 52, // DSA ID
      address: "0x...", // DSA Address
      version: 2 // DSA version
  },
  ...
]
```

## setInstance\(\)

Be sure to configure global values by calling `setInstance()`. You can get the id of the DSA by calling `getAccounts()`. The configured account will be used for all subsequent calls.

```javascript
dsa.setInstance(dsaId) // DSA ID
```

### Parameter

| **Parameter** | **Type** | **Description** |
| :--- | :--- | :--- |
| dsaId | `Number` | DSA ID to be used for casting spells. |

### Returns

This method returns a promise that resolves to the newly set instance. Here's how it looks:

```javascript
  {
    id: 0, // DSA ID
    address: "0x...", // Address of DSA
    version: 2, // Version of DSA
    chainId: 56,
  }
```


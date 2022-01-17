# Utilities

The SDK also provides other methods to help developers interact with the blockchain easily and common transactions like ERC20 token and ETH transfers.

### Transaction History

You can see the list of transactions for an address:

```javascript
nub.getAccountTransactions(address);
```

It accepts an address as an argument.

### Token Transfer

You can transfer tokens using the erc20 transfer function. It receives an object as input. It returns a promise that resolves to a transaction object

```javascript
nub.erc20.transfer({token, amount, to});
```

| Object Parameters | Type   | Description                                                                                                            |
| ----------------- | ------ | ---------------------------------------------------------------------------------------------------------------------- |
| token             | String | The address of the ERC20 token you want to send.                                                                       |
| amount            | String | The amount of tokens you want to send. It must include the decimal places of the token. E.g `1*10**18` to send 1 WBNB. |
| to                | String | The address you want to send the token to.                                                                             |

### BNB Transfer

For BNB transfers, use the eth transfer function. It also receives an object as input. It returns a promise that resolves to a transaction object.

```javascript
nub.eth.transfer({amount, to});
```

| Object Parameters | Type   | Description                                                    |
| ----------------- | ------ | -------------------------------------------------------------- |
| amount            | String | The amount of BNB you want to send in wei (smallest BNB unit). |
| to                | String | The address you want to send the BNB.                          |

### Wrap BNB

BNB can be wrapped to BNB using the SDK.

```
nub.wbnb.wrap(amount)
```

The function takes in the amount of BNB you want to wrap.

### Estimate Wrap Gas

```
nub.wbnb.estimateWrapGas(amount)
```

The function takes in the amount of BNB you want to use in estimation.

### Unwrap BNB

WBNB can be unwrapped to BNB.

```
nub.wbnb.unwrap(amount)
```

The function takes in the amount of WBNB you want to unwrap. You must have this amount of WBNB already approved.

### Estimate Unwrap Gas

```
nub.wbnb.unwrap(amount)
```

The function takes in the amount of WBNB you want to use in estimation.

### Approval

You can approve addresses to spend the ERC20 token. It also receives an object as input and returns a promise that resolves to a transaction object.

```javascript
nub.erc20.approve({token [, amount ] [, to]});
```

| Object Parameters | Type   | Description                                                                                                                                                                     |
| ----------------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| token             | String | Address of the token you want to approve for a spender.                                                                                                                         |
| amount            | String | The amount of tokens to be approved for spending. If empty it defaults to an infinite approval. It must include the decimal places of the token. E.g `1*10**18` to send 1 WBNB. |
| to                | String | The address to be approved. It defaults to the Wizard address if not passed.                                                                                                    |

### Pancakeswap LpToken Price

You can get the price of a Pancakeswap Liquidity provider token (lptoken) in US dollars using this function. It returns a promise that resolves to a number and takes the address of the lp token as an input.

`nub.pancakeswap.getLpPrice(tokenAddress)`

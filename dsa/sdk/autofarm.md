---
description: These methods are provided by the SDK to interact with the AutoFarm Protocol
---

# AutoFarm

### Deposit

You can deposit in Autofarm pools using this method on the autofarm class of the SDK. You must have granted the AutoFarm protocol approval to spend the funds before calling it. Check [approval](utilities.md#approval) to find out how to approve contracts using the SDK. This function returns a promise that resolves to a transaction receipt.

```
nub.autofarm.deposit({poolId, amount});
```

| Parameter | Type   | Description                                                                                                                                                                                                           |
| --------- | ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| poold     | String | This is the pool of the liquidity provider (lp) token on Autofarm. Get the list of poolds [here](https://autofarm.gitbook.io/autofarm-network/how-tos/autofarm/withdraw-from-autofarm-vaults-using-a-block-explorer). |
| amount    | String | The amount of tokens you want to deposit. Passing the max value of `uint256` deposits the complete lptoken balance.                                                                                                   |

### Withdraw

Use this function to withdraw funds from AutoFarm pools.  It returns a promise that resolves to a transaction receipt.

```
nub.autofarm.withdraw({poolId, amount});
```

| Parameter | Type   | Description                                                                                                                                                                                                           |
| --------- | ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| poolId    | String | This is the pool of the liquidity provider (lp) token on Autofarm. Get the list of poolds [here](https://autofarm.gitbook.io/autofarm-network/how-tos/autofarm/withdraw-from-autofarm-vaults-using-a-block-explorer). |
| amount    | String | The amount of tokens you want to withdraw. Passing the max value of `uint256` withdraws the complete address balance.                                                                                                 |

### Harvest

You can collect rewards you have earned in AUTO tokens (the native token of the AutoFarm protocol) using this function. It returns a promise that resolves to a transaction receipt.

```
nub.autofarm.harvest({poolId});
```

| Parameter | Type   | Description                                                                                                                                                                              |
| --------- | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `poolId`  | String | Pool to harvest farming rewards from. Get the list of poolds [here](https://autofarm.gitbook.io/autofarm-network/how-tos/autofarm/withdraw-from-autofarm-vaults-using-a-block-explorer). |


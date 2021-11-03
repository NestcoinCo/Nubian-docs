# Venus

Provides functions to deposit, withdraw, borrow, payback and liquidate borrow positions. It provides raw functions that require the caller to provide a vToken and an underlying token address and normal functions that resolves the addresses from a provided tokenId. See the tokenIds with their corresponding tokens and vTokens in the TokenId [table](venus.md#TokenIds).

## Address

Venus Connector is deployed on [mainnet](https://bscscan.com/address/0x4ffcfd0f62352e33bb02710fd4c7d2049644b13d).

## Code

[main.sol](https://github.com/Open-Currency-Collective/Nubian-dsa-connectors/blob/master/contracts/connectors/venus/main.sol)

## Events

### LogDeposit

```text
event LogDeposit( address indexed token, address vToken, uint256 tokenAmt, uint256 getId, uint256 setId);
```

Emitted each time a deposit occurs with [Deposit](venus.md#Deposit) or [DepositRaw](venus.md#DepositRaw).

### LogWithdraw

```text
event LogWithdraw( address indexed token, address vToken, uint256 tokenAmt, uint256 getId, uint256 setId);
```

Emitted each time a withdrawal occurs with [Withdraw](venus.md#WithdrawRaw) or [WithdrawRaw](venus.md#WithdrawRaw)

### LogBorrow

```text
event LogBorrow( address indexed token, address vToken, uint256 tokenAmt, uint256 getId, uint256 setId);
```

Emitted each time a borrow occurs with [Borrow](venus.md#Borrow) or [BorrowRaw](venus.md#BorrowRaw)

### LogPayback

```text
event LogPayback( address indexed token, address vToken, uint256 tokenAmt, uint256 getId, uint256 setId);
```

Emitted each time a payback occurs with [Payback](venus.md#Payback) or [PaybackRaw](venus.md#PaybackRaw)

### LogDepositVToken

```text
event LogDepositVToken( address indexed token, address vToken, uint256 tokenAmt, uint256 vTokenAmt, uint256 getId, uint256 setId);
```

Emitted each time a deposit occurs with [DepositVToken](venus.md#DepositVToken) or [DepositVTokenRaw](venus.md#DepositVTokenRaw).

### LogWithdrawVToken

```text
event LogWithdrawVToken( address indexed token, address vToken, uint256 tokenAmt, uint256 vTokenAmt, uint256 getId, uint256 setId);
```

Emitted each time a withdrawal occurs with [WithdrawVToken](venus.md#WithdrawVToken) or [WithdrawVTokenRaw](venus.md#WithdrawVToken).

### LogLiquidate

```text
event LogLiquidate( address indexed borrower, address indexed tokenToPay, address indexed tokenInReturn, uint256 tokenAmt, uint256 getId, uint256 setId);
```

Emitted each time a liquidation occurs with [Liquidate](venus.md#Liquidate) or [LiquidateRaw](venus.md#LiquidateRaw).

## Read-only Method

### Name

```text
string public name = "Venus-v1";
```

Returns "Venus-v1" as the name of this function.

## State-changing Methods

### DepositRaw

```text
function depositRaw(
    address token,
    address vToken,
    uint256 amt,
    uint256 getId,
    uint256 setId
) public payable returns (string memory _eventName, bytes memory _eventParam);
```

Deposit token into Venus to earn interest. Depositor gets vTokens.

**DepositRaw Parameters**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| token | `address` | Address of token to deposit. Pass 0xEeeeeEeeeEeEeeEeEeEeeEEEeeeeEeeeeeeeEEeE to deposit BNB. |
| vToken | `address` | Address of token's corresponding vToken. |
| amt | `uint256` | Amount of tokens or BNB to be deposited. Pass `uint(-1)` to deposit the full DSA balance. |
| getId | `uint256` | ID to get amt. Pass 0 if unsure of its value. |
| setId | `uint256` | ID to store the amount deposited. Pass 0 if unsure of its value. |

#### Deposit <a id="Deposit"></a>

```text
function deposit(
    string calldata tokenId,
    uint256 amt,
    uint256 getId,
    uint256 setId
) external payable returns (string memory _eventName, bytes memory _eventParam);
```

Deposit token to Venus to earn interest. Depositor gets vTokens.

**Deposit Parameters**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| tokenId | `string` | The token id of the token to deposit. \(For eg: BUSD-A\) which is a representation of venus mapping. |
| amt | `uint256` | Amount of tokens or BNB to be deposited. Pass `uint(-1)` to deposit the full DSA balance. |
| getId | `uint256` | ID to get amt. Pass 0 if unsure of its value. |
| setId | `uint256` | ID to store the amount deposited. Pass 0 if unsure of its value. |

### WithdrawRaw

```text
function withdrawRaw(
    address token,
    address vToken,
    uint256 amt,
    uint256 getId,
    uint256 setId
) public payable returns (string memory _eventName, bytes memory _eventParam);
```

Withdraw tokens from Venus with interest earned. The account making the withdrawal must have the equivalent vTokens for amt in its balance.

**WithdrawRaw Parameters**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| token | `address` | Address of token to withdraw. Pass 0xEeeeeEeeeEeEeeEeEeEeeEEEeeeeEeeeeeeeEEeE to deposit BNB. |
| vToken | `address` | Address of token's corresponding vToken. |
| amt | `uint256` | Amount of underlying tokens to be withdrawn. Pass `uint(-1)` to withdraw the full DSA token or BNB balance. |
| getId | `uint256` | ID to get amt. Pass 0 if unsure of its value. |
| setId | `uint256` | ID to store the amount withdrawn. Pass 0 if unsure of its value. |

### Withdraw

```text
function withdraw(
    string calldata tokenId,
    uint256 amt,
    uint256 getId,
    uint256 setId
) external payable returns (string memory _eventName, bytes memory _eventParam);
```

Withdraw tokens from Venus with interest earned. The account making the withdrawal must have the equivalent vTokens for amt in its balance.

**Withdraw Parameters**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| tokenId | `string` | The token id of the token to withdraw. \(E.g.: BUSD-A\) which is a representation of venus mapping. |
| amt | `uint256` | Amount of underlying tokens to be withdrawn. Pass `uint(-1)` to withdraw the full DSA token or BNB balance. |
| getId | `uint256` | ID to get amt. Pass 0 if unsure of its value. |
| setId | `uint256` | ID to store the amount withdrawn. Pass 0 if unsure of its value. |

#### BorrowRaw <a id="BorrowRaw"></a>

```text
function borrowRaw(
    address token,
    address vToken,
    uint256 amt,
    uint256 getId,
    uint256 setId
) public payable returns (string memory _eventName, bytes memory _eventParam);
```

Borrow token from Venus. The amount borrowed must be less than the user's Account Liquidity and the market's available liquidity.

**BorrrowRaw Parameters**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| token | `address` | Address of token to borrow. Pass 0xEeeeeEeeeEeEeeEeEeEeeEEEeeeeEeeeeeeeEEeE to borrow BNB. |
| vToken | `address` | Address of  `token`'s corressponding vToken. |
| amt | `uint256` | Amount of underlying tokens to be borrowed. |
| getId | `uint256` | ID to get amt. Pass 0 if unsure of its value. |
| setId | `uint256` | ID to store the amount borrowed. Pass 0 if unsure of its value. |

### Borrow

```text
function borrow(
    string calldata tokenId,
    uint256 amt,
    uint256 getId,
    uint256 setId
) external payable returns (string memory _eventName, bytes memory _eventParam);
```

Borrow token from Venus. The amount borrowed must be less than the user's Account Liquidity and the market's available liquidity.

**Borrrow Parameters**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| tokenId | `string` | The token id of the token to borrow. \(For eg: BUSD-A\) which is a representation of venus mapping. |
| amt | `uint256` | Amount of underlying tokens to be borrowed. |
| getId | `uint256` | ID to get amt. Pass 0 if unsure of its value. |
| setId | `uint256` | ID to store the amount borrowed. Pass 0 if unsure of its value. |

### PaybackRaw

```text
function paybackRaw(
    address token,
    address vToken,
    uint256 amt,
    uint256 getId,
    uint256 setId
) public payable returns (string memory _eventName, bytes memory _eventParam);
```

Payback tokens borrowed from Venus.

**PaybackRaw Parameters**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| token | `address` | Address of token to payback. Pass 0xEeeeeEeeeEeEeeEeEeEeeEEEeeeeEeeeeeeeEEeE to payback BNB. |
| vToken | `address` | Address of token's corresponding vToken. |
| amt | `uint256` | Amount of underlying tokens to be borrowed. Pass `uint(-1)` to payback total amount borrowed with interest. |
| getId | `uint256` | ID to get amt. Pass 0 if unsure of its value. |
| setId | `uint256` | ID to store the amount payed back. Pass 0 if unsure of its value. |

### Payback

```text
function payback(
    string calldata tokenId,
    uint256 amt,
    uint256 getId,
    uint256 setId
) external payable returns (string memory _eventName, bytes memory _eventParam);
```

Payback tokens borrowed from Venus.

**Payback Parameters**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| tokenId | `string` | The token id of the token to payback. \(E.g.: BUSD-A\) which is a representation of venus mapping. |
| amt | `uint256` | Amount of underlying tokens to be borrowed. Pass `uint(-1)` to payback total amount borrowed with interest. |
| getId | `uint256` | ID to get amt. Pass 0 if unsure of its value. |
| setId | `uint256` | ID to store the amount payed back. Pass 0 if unsure of its value. |

### DepositVTokenRaw

```text
function depositVTokenRaw(
    address token,
    address vToken,
    uint256 amt,
    uint256 getId,
    uint256 setId
) public payable returns (string memory _eventName, bytes memory _eventParam);
```

Same as the [DepositRaw](venus.md) function except setId stores the number of vTokens received.

**DepositVTokenRaw Parameters**

Check [DepositRaw](venus.md) function for the other parameters.

| Parameter | Type | Description |
| :--- | :--- | :--- |
| setId | `uint256` | ID to store the amount of vTokens received. |

#### DepositVToken <a id="DepositVToken"></a>

```text
function depositVToken(
    string calldata tokenId,
    uint256 amt,
    uint256 getId,
    uint256 setId
) external payable returns (string memory _eventName, bytes memory _eventParam);
```

Same as the [Deposit](venus.md) function except setId stores the number of vTokens received.

**DepositVToken Parameters**

Check [Deposit](venus.md) function for the other parameters.

| Parameter | Type | Description |
| :--- | :--- | :--- |
| setId | `uint256` | ID to store the amount of vTokens received. |

### WithdrawVTokenRaw

```text
function withdrawVTokenRaw(
    address token,
    address vToken,
    uint256 vTokenAmt,
    uint256 getId,
    uint256 setId
) public payable returns (string memory _eventName, bytes memory _eventParam);
```

Same as the [WithdrawRaw](venus.md) function except for the following:

* GetId is used to retrieve vTokenAmt instead of amt.
* The amount of vTokens to redeem is passed instead of the amount of underlying tokens to withdraw.

**WithdrawVTokenRaw Parameters**

Check the [WithdrawRaw](venus.md) function for other parameters.

| Parameter | Type | Description |
| :--- | :--- | :--- |
| vTokenAmt | `uint256` | The amount of vTokens to redeem for the underlying token. |
| getId | `uint256` | ID to get the amount of vTokens to withdraw. |

#### WithdrawVToken <a id="WithdrawVToken"></a>

```text
function withdrawVToken(
    string calldata tokenId,
    uint256 vTokenAmt,
    uint256 getId,
    uint256 setId
) external payable returns (string memory _eventName, bytes memory _eventParam);
```

Same as the [Withdraw](venus.md) function except for the following:

* GetId is used to retrieve vTokenAmt instead of amt.
* The amount of vTokens to redeem is passed instead of the amount of underlying tokens to withdraw.

**WithdrawVToken Parameters**

Check the [Withdraw](venus.md) function for other parameters.

| Parameter | Type | Description |
| :--- | :--- | :--- |
| vTokenAmt | `uint256` | The amount of vTokens to redeem for the underlying token. |
| getId | `uint256` | ID to get the amount of vTokens to withdraw. |

### LiquidateRaw

```text
function liquidateRaw(
    address borrower,
    address tokenToPay,
    address vTokenPay,
    address tokenInReturn,
    address vTokenColl,
    uint256 amt,
    uint256 getId,
    uint256 setId
) public payable returns (string memory _eventName, bytes memory _eventParam);
```

Liquidate an accounts borrow position on Venus. The account's liquidity must be negative.

**LiquidateRaw Parameters**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| borrower | `address` | Address with negative liquidity. |
| tokenToPay | `address` | The token to be used as liquidation payment. Pass 0xEeeeeEeeeEeEeeEeEeEeeEEEeeeeEeeeeeeeEEeE for BNB. |
| vTokenPay | `address` | The corressponding vToken address of tokenToPay. |
| tokenInReturn | `address` | The address of the token to return for liquidation. |
| vTokenColl | `address` | The address of the corressponding vToken of tokenInReturn. |
| amt | `uint256` | Amount of tokenToPay to be used for liquidation. Pass `uint(-1)` to use the full balance. |
| getId | `uint256` | ID to get amt. Pass 0 if unsure of its value. |
| setId | `uint256` | ID to store the actual amount of tokenToPay used to pay for liquidation. Pass 0 if unsure of its value. |

### Liquidate

```text
function liquidateRaw(
    address borrower,
    string calldata tokenIdToPay,
    string calldata tokenIdInReturn,
    uint256 amt,
    uint256 getId,
    uint256 setId
) public payable returns (string memory _eventName, bytes memory _eventParam);
```

Liquidate an accounts borrow position on Venus. The account's liquidity must be negative.

**Liquidate Parameters**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| borrower | `address` | Address with negative liquidity. |
| tokenIdToPay | `string` | Token Id of token to pay for liquidation. |
| tokenIdInReturn | `string` | Token Id of token to return for liquidation. |
| amt | `uint256` | Amount of token to be used for liquidation. Pass `uint(-1)` to use the full balance. |
| getId | `uint256` | ID to get amt. Pass 0 if unsure of its value. |
| setId | `uint256` | ID to store the actual amount of token used to pay for liquidation. Pass 0 if unsure of its value. |

## TokenIds <a id="TokenIds"></a>

| TokenId | Token | vToken |
| :--- | :--- | :--- |
| BNB-A | 0xEeeeeEeeeEeEeeEeEeEeeEEEeeeeEeeeeeeeEEeE | 0xA07c5b74C9B40447a954e1466938b865b6BBea36 |
| BUSD-A | 0xe9e7CEA3DedcA5984780Bafc599bD69ADd087D56 | 0x95c78222B3D6e262426483D42CfA53685A67Ab9D |
| SXP-A | 0x47BEAd2563dCBf3bF2c9407fEa4dC236fAbA485A | 0x2fF3d0F6990a40261c66E1ff2017aCBc282EB6d0 |
| USDC-A | 0x8AC76a51cc950d9822D68b83fE1Ad97B32Cd580d | 0xecA88125a5ADbe82614ffC12D0DB554E2e2867C8 |
| USDT-A | 0x55d398326f99059fF775485246999027B3197955 | 0xfD5840Cd36d94D7229439859C0112a4185BC0255 |
| XVS-A | 0xcF6BB5389c92Bdda8a3747Ddb454cB7a64626C63 | 0x151B1e2635A717bcDc836ECd6FbB62B674FE3E1D |
| BTC-A | 0x7130d2A12B9BCbFAe4f2634d864A1Ee1Ce3Ead9c | 0x882C173bC7Ff3b7786CA16dfeD3DFFfb9Ee7847B |
| ETH-A | 0x2170Ed0880ac9A755fd29B2688956BD959F933F8 | 0xf508fCD89b8bd15579dc79A6827cB4686A3592c8 |
| LTC-A | 0x4338665CBB7B2485A8855A139b75D5e34AB0DB94 | 0x57A5297F2cB2c0AaC9D554660acd6D385Ab50c6B |
| XRP-A | 0x1D2F0da169ceB9fC7B3144628dB156f3F6c60dBE | 0xB248a295732e0225acd3337607cc01068e3b9c10 |


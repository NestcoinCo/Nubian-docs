# Basic

Basic handles user deposits and withdrawals on the DeFi Smart Account \(DSA\).

## Address

Basic Connector is deployed on [mainnet](https://bscscan.com/address/0xC2e1c0fc0A2c0126AD5222D6eB2453c6aEc1e637).

## Code

[main.sol](https://github.com/Open-Currency-Collective/Nubian-dsa-connectors/blob/master/contracts/connectors/basic/main.sol)

## Events

### LogDeposit

```text
event LogDeposit(address indexed erc20, uint256 tokenAmt, uint256 getId, uint256 setId);
```

Emitted when there is a deposit with [deposit](basic.md#Deposit).

### LogWithdraw

```text
event LogWithdraw(address indexed erc20, uint256 tokenAmt, address indexed to, uint256 getId uint256 setId);
```

Emitted when there is a withdrawal with [withdraw](basic.md#Withdraw).

## Methods

### Read-only methods.

#### Name

```text
string constant public name = "Basic-v1";
```

Returns connector name.

#### Deposit <a id="Deposit"></a>

```text
function deposit(
    address token,
    uint256 amt,
    uint256 getId,
    uint256 setId
) public payable returns (string memory _eventName, bytes memory _eventParam);
```

Deposits into DSA

**Deposit Parameters**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| token | `address` | Address of token to be deposited. Use `0xEeeeeEeeeEeEeeEeEeEeeEEEeeeeEeeeeeeeEEeE` for BNB. |
| amt | `uint256` | Amount of tokens to be deposited. Pass `uint(-1)` to deposit full depositor balance. `amt` must equal `msg.value` for ETH deposits. |
| getId | `uint256` | ID to get `amt`. Pass 0 if unsure of its value. |
| setId | `uint256` | ID to set amount deposited. Pass 0 if unsure of its value. |

#### Withdraw <a id="Withdraw"></a>

```text
function withdraw(
    address token,
    uint amt,
    address payable to,
    uint getId,
    uint setId
) public payable returns (string memory _eventName, bytes memory _eventParam);
```

Withdraws from DSA.

**Withdraw Parameters**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| token | `address` | Address of token to be withdrawn. Use 0xEeeeeEeeeEeEeeEeEeEeeEEEeeeeEeeeeeeeEEeE for BNB. |
| amt | `uint256` | Amount of tokens to be withdrawn. Pass `uint(-1)` to withdraw the full DSA balance of token or BNB. |
| getId | `uint256` | ID to get `amt`. Pass 0 if unsure of its value. |
| setId | `uint256` | ID to set amount withdrawn. Pass 0 if unsure of its value. |


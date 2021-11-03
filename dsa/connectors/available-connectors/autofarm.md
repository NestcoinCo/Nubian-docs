# Autofarm

Allows users to deposit and withdraw tokens in AutoFarm vaults in order to earn yield.

## Address

Autofarm connector is deployed on [mainnet](https://bscscan.com/address/0x82aB4bCD90E99f31a90201669AACC6867c9c3B77).

## Events

### LogDeposit

```text
event LogDeposit( address lpToken, uint256 amount, uint256 poolId, uint256 getId, uint256 setId);
```

Emitted when there is a deposit with [Deposit](autofarm.md#Deposit).

### LogWithdraw

```text
event LogWithdraw( uint256 amount, uint256 poolId, uint256 getId, uint256 setId);
```

Emitted when there is a withdrawal with [Withdraw](autofarm.md#Withdraw) or [Harvest](autofarm.md#Harvest).

## Code

[main.sol](https://github.com/Open-Currency-Collective/Nubian-dsa-connectors/blob/master/contracts/connectors/autofarm/main.sol)

## Read-only methods.

### Name

```text
string public name = "Autofarm-v1";
```

Returns the name of this connector.

## State-changing methods

### Deposit <a id="Deposit"></a>

```text
function deposit(
    address lpToken,
    uint256 amt,
    uint256 poolId,
    uint256 getId,
    uint256 setId
) public payable returns (string memory _eventName, bytes memory _eventParam);
```

Enables deposits into AutoFarm vaults.

#### Deposit Parameters

| Parameter | Type | Description |
| :--- | :--- | :--- |
| lpToken | `address` | Address of liquidity Provider \(lp\) token to be distributed. |
| amt | `uint256` | Amount of lp tokens to be deposited. Pass `uint(-1)` to deposit the full DSA lpToken balance. |
| poolId | `uint256` | Pool Id of the Autofarm lp vault. |
| getId | `uint256` | ID to get `amt`. Pass 0 if unsure of its value. |
| setId | `uint256` | Not used. Pass 0. |

### Withdraw <a id="Withdraw"></a>

```text
function withdraw(
    uint256 amt,
    uint256 poolId,
    uint256 getId,
    uint256 setId
) public payable returns (string memory _eventName, bytes memory _eventParam);
```

Enables withdrawals from AutoFarm vaults. Autofarm tokens \($AUTO\) and interest earned are withdrawn automatically.

#### Withdraw Parameters

| Parameter | Type | Description |
| :--- | :--- | :--- |
| amt | `uint256` | Amount of tokens to be deposited. Pass `uint(-1)` to withdraw complete user deposit. |
| poolId | `uint256` | Pool Id of Autofarm vault. |
| getId | `uint256` | ID to get `amt`. Pass 0 if unsure of its value. |
| setId | `uint256` | Not used. Pass 0. |

### Harvest <a id="Harvest"></a>

```text
function harvest(
    uint256 poolId,
    uint256 getId,
    uint256 setId
) public payable returns (string memory _eventName, bytes memory _eventParam);
```

Allows users to collect pending rewards on their deposits.

#### Harvest Parameters

| Parameter | Type | Description |
| :--- | :--- | :--- |
| poolId | `uint256` | Pool Id of Autofarm vault. |
| getId | `uint256` | Not used. Pass 0. |
| setId | `uint256` | Not used. Pass 0. |


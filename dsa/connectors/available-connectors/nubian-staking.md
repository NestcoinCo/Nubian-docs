# Nubian Staking

Allows a user to stake and unstake Nubian tokens.

## Address

Nubian staking Connector is deployed on [mainnet.](https://bscscan.com/address/0x0764C090a14E45Ae23F69732BeB28504f89D669A)

## Code

[main.sol](https://github.com/Open-Currency-Collective/Nubian-dsa-connectors/blob/master/contracts/connectors/nubian_staking/main.sol)

## Events

### LogDeposit

```text
event LogDeposit( uint256 recordId, uint256 amt, uint256 getId, uint256 setId);
```

Emitted each time a deposit occurs with [deposit](nubian-staking.md#deposit).

### LogWithdraw

```text
event LogWithdraw( address indexed user, uint256 recordId, uint256 amt, uint256 reward, uint256 getId, uint256 setId);
```

Emitted each time a withdrawal occurs with [withdraw](nubian-staking.md#withdraw).

## Read-only method

### Name

```text
string public name = "NubianStaking-v1";
```

Returns connector name.

## State-changing methods

### Deposit

```text
function deposit(
    uint256 amt,
    uint256 lockPeriod,
    uint256 getId,
    uint256 setId
) public payable returns (string memory _eventName, bytes memory _eventParam);
```

Stakes Nubian tokens for a certain period to earn nubian rewards. It logs the recordId associated with each stake.

**Deposit Parameters**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| amt | `uint256` | Amount of Nubian tokens to stake. |
| lockPeriod | `uint256` | Length of time in seconds the user wants to stake his Nubian tokens must be more than the `minLockPeriod`. Valid lockPeriods and minLockPeriod are retrievable from the nubian staking contract. |
| getId | `uint256` | ID to get `amt`. Pass 0 if unsure of its value. |
| setId | `uint256` | ID to set amount staked. Pass 0 if unsure of its value. |

### Withdraw

```text
function withdraw(
    uint256 recordId,
    uint256 getId,
    uint256 setId
) public payable returns (string memory _eventName, bytes memory _eventParam);
```

Withdraws all the Nubian tokens staked with a `recordId` and gives the user earned rewards. RecordIds are logged with each stake.

**Withdraw Parameters**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| recordId | `uint256` | ID to withdraw all staked tokens associated with it. |
| getId | `uint256` | Not used. Pass 0. |
| setId | `uint256` | Not used. Pass 0. |


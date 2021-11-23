---
description: Welcome let us show you how we cast spells here at Nubian.
---

# 🧙♂ Wizard

The wizard is the main contract that users interact with almost every time they do a transaction on Nubian. It is a proxy contract that directs each call to a DeFi protocol using a connector which formats inputs and sends them to the DeFi protocol.&#x20;

Like every wizard, the Nubian wizard casts spells. Each spell is a call to a DeFi protocol. These spells are achieved using connectors which are separate contracts that interact with a DeFi protocol. Almost every protocol that Nubian interacts with has its own connector. The spells can be combined in a single transaction to form complex strategies.

{% hint style="danger" %}
It is necessary to note that the Wizard contract is stateless and is not meant to hold any funds. If you send funds to the contract and fail to retrieve them in that same transaction, they can be taken by anyone.
{% endhint %}

## Address

The Wizard contract is deployed on [mainnet](https://bscscan.com/address/0x9B1240399e9E23e4C31520fc5C00FA83dc451819).

## Events

### LogCast

```solidity
    event LogCast(
        address indexed origin,
        address indexed sender,
        uint256 value,
        string[] targetsNames,
        address[] targets,
        string[] eventNames,
        bytes[] eventParams
    );
```

This emits all the events from all the connectors involved in casting the spells when the [cast](wizard.md#cast) function is called.

## Code

[main.sol](https://github.com/NestcoinCo/Nubian-coven/blob/main/contracts/wizard.sol)

## Read-only-methods

### Connectors

```solidity
address public immutable connectors;
```

Returns the address of the contract that holds the list of approved connectors.

## State-changing methods

### Spell

```solidity
function spell(
    address _target, 
    bytes memory _data
) internal returns (bytes memory response);
```

This function does the actual casting by calling the connector with the data it receives and returns the event so it can be cast.

| Parameter | Type      | Description                                                         |
| --------- | --------- | ------------------------------------------------------------------- |
| \_target  | `address` | The address of the connector to be used in the spell                |
| \_data    | `bytes`   | The abi encoded parameters which are to be passed to the connector. |

### Cast

```solidity
    function cast(
        string[] calldata _targetNames,
        bytes[] calldata _datas,
        address _origin
    ) external payable;
```

Receives the arrays of connectors (`_targetNames`) and the parameters (`_data`) to be passed to each of them. Each parameter in the parameters array is passed to the connector in the corresponding index of the connectors array. It checks for the validity of all the connectors before attempting to cast the spells.

| Parameter     | Type       | Description                                                                                                                                                                 |
| ------------- | ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| \_targetNames | `string[]` | The names of connectors to be used in casting spells. Their names are mapped to their addresses in the [connectors registry](connectors/connectors-registry.md#connectors). |
| \_datas       | `bytes[]`  | The abi encoded parameters passed to the corresponding connector in `_targetNames`.                                                                                         |
| origin        | `address`  | The address to track the origin of the transaction. Used for analytics and affiliates.                                                                                      |

### Connector Names

| Name                                                                            | Address                                        |
| ------------------------------------------------------------------------------- | ---------------------------------------------- |
| ****[**BASIC-A**](connectors/available-connectors/basic.md)****                 | 0xC2e1c0fc0A2c0126AD5222D6eB2453c6aEc1e637​​​​ |
| ****[**PancakeV2**](connectors/available-connectors/pancakeswap.md)****         | 0x546bde105B24147bbd34F3147a0FD68961515Feb     |
| ****[**VenusV2**](connectors/available-connectors/venus.md)****                 | 0xB03308Fa6A1Ecb489ECC86B7e930491020ee2b96     |
| ****[**AutoFarmV2**](broken-reference)****                                      | 0x82aB4bCD90E99f31a90201669AACC6867c9c3B77     |
| ****[**Nubian Staking**](connectors/available-connectors/nubian-staking.md)**** | 0x0764C090a14E45Ae23F69732BeB28504f89D669A     |

****

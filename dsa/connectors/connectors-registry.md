# Connectors Registry

This contract keeps a record of available connectors, it can also add, remove and update them.

## Address

Connectors Registry is deployed on [mainnet](https://bscscan.com/address/0x944930F20A6D9f17140B6F5ba69F83BFF95eb820).

## Code

[connectors.sol](https://github.com/Open-Currency-Collective/nubian-dsa-contracts/blob/master/contracts/v2/registry/connectors.sol)

## Events

### LogConnectorAdded

```
event LogConnectorAdded(string indexed connectorName, address indexed connector);
```

Emitted anytime a new connector is added with [`addConnector`](connectors-registry.md#addconnectors).

### LogConnectorUpdated

```
event LogConnectorUpdated(string indexed connectorName, address indexed oldConnector, address indexed newConnector);
```

Emitted anytime an existing connector is updated with [`updateConnector`](connectors-registry.md#updateconnectors).

### LogConnectorRemoved

```
event LogConnectorRemoved(string indexed connectorName, address indexed connector);
```

Emitted when an existing connector is removed with [`removeConnector`](connectors-registry.md#removeconnectors).

### LogController

```
event LogController(address indexed addr, bool indexed isChief);
```

Emitted when a chief is enabled or disabled (toggled) with [`toggleChief`](connectors-registry.md#togglechief).

## Read-only Methods

### Connectors

```
mapping(string => address) public connectors;
```

Maps connector names to their addresses and returns an address when given a connector name.

### IsConnectors

```
function isConnectors(string[] calldata _connectorNames) external view returns (bool isOk, address[] memory _connectors)
```

Checks if `_connectorNames` are connectors and returns their connector addresses.

**Parameters**

| Parameter        | Type       | Description              |
| ---------------- | ---------- | ------------------------ |
| \_connectorNames | `string[]` | Array of connector names |

**Returns**

| Parameter    | Type        | Description                                                             |
| ------------ | ----------- | ----------------------------------------------------------------------- |
| isOk         | `boolean`   | Is true if all _\_connectorNames_ are valid and false otherwise         |
| \_connectors | `address[]` | Addresses of _\_connectorNames_ . False connectors have a null address. |

## State-Changing Methods

### AddConnectors

```
function addConnectors(string[] calldata _connectorNames, address[] calldata _connectors) external isChief
```

Adds new connectors.

| Parameter        | Type        | Description                                                      |
| ---------------- | ----------- | ---------------------------------------------------------------- |
| \_connectorNames | `string[]`  | Array of connector names                                         |
| \_connectors     | `address[]` | Array of corresponding connector addresses to _\_connectorNames_ |

### RemoveConnectors

```
function removeConnectors(string[] calldata _connectorNames) external isChief
```

Removes already existing connectors.

**Parameter**

| Parameter        | Type       | Description              |
| ---------------- | ---------- | ------------------------ |
| \_connectorNames | `string[]` | Array of connector names |

### UpdateConnectors

```
function updateConnectors(string[] calldata _connectorNames, address[] calldata _connectors) external isChief
```

Updates already existing `_connectorNames` with new addresses.

**Parameter**

| Parameter        | Type        | Description                                                    |
| ---------------- | ----------- | -------------------------------------------------------------- |
| \_connectorNames | `string[]`  | Array of connector names                                       |
| \_connectors     | `address[]` | Array of connector addresses corresponding to \_connectorNames |

**Returns**

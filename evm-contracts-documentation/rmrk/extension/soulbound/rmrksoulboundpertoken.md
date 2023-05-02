# RMRKSoulboundPerToken

_RMRK team_

> RMRKSoulboundPerToken

Smart contract of the RMRK Soulbound module where the transfers are permitted or prohibited on a per-token basis.

## Methods

### VERSION

```solidity
function VERSION() external view returns (string)
```

Version of the @rmrk-team/evm-contracts package

#### Returns

| Name | Type   | Description |
| ---- | ------ | ----------- |
| \_0  | string | undefined   |

### isNonTransferable

```solidity
function isNonTransferable(uint256 tokenId) external view returns (bool)
```

Used to check whether the given token is non-transferable or not.

_If this function returns `true`, the transfer of the token MUST revert executionIf the tokenId does not exist, this method MUST revert execution_

#### Parameters

| Name    | Type    | Description                   |
| ------- | ------- | ----------------------------- |
| tokenId | uint256 | ID of the token being checked |

#### Returns

| Name | Type | Description                                                          |
| ---- | ---- | -------------------------------------------------------------------- |
| \_0  | bool | Boolean value indicating whether the given token is non-transferable |

### name

```solidity
function name() external view returns (string)
```

Used to retrieve the collection name.

#### Returns

| Name | Type   | Description            |
| ---- | ------ | ---------------------- |
| \_0  | string | Name of the collection |

### supportsInterface

```solidity
function supportsInterface(bytes4 interfaceId) external view returns (bool)
```

_Returns true if this contract implements the interface defined by `interfaceId`. See the corresponding https://eips.ethereum.org/EIPS/eip-165#how-interfaces-are-identified\[EIP section] to learn more about how these ids are created. This function call must use less than 30 000 gas._

#### Parameters

| Name        | Type   | Description |
| ----------- | ------ | ----------- |
| interfaceId | bytes4 | undefined   |

#### Returns

| Name | Type | Description |
| ---- | ---- | ----------- |
| \_0  | bool | undefined   |

### symbol

```solidity
function symbol() external view returns (string)
```

Used to retrieve the collection symbol.

#### Returns

| Name | Type   | Description              |
| ---- | ------ | ------------------------ |
| \_0  | string | Symbol of the collection |

## Events

### Soulbound

```solidity
event Soulbound(uint256 indexed tokenId, bool state)
```

Emitted when a token's soulbound state changes.

#### Parameters

| Name              | Type    | Description                                                                                       |
| ----------------- | ------- | ------------------------------------------------------------------------------------------------- |
| tokenId `indexed` | uint256 | ID of the token                                                                                   |
| state             | bool    | A boolean value signifying whether the token became soulbound (`true`) or transferrable (`false`) |

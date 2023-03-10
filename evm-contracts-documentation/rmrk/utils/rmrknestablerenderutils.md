# RMRKNestableRenderUtils

_RMRK team_

> RMRKNestableRenderUtils

Smart contract of the RMRK Nestable render utils module.

## Methods

### checkExpectedParent

```solidity
function checkExpectedParent(address childAddress, uint256 childId, address expectedParent, uint256 expectedParentId) external view
```

Check if the child is owned by the expected parent.

_Reverts if child token is not owned by an NFT.Reverts if child token is not owned by the expected parent._

#### Parameters

| Name             | Type    | Description                             |
| ---------------- | ------- | --------------------------------------- |
| childAddress     | address | Address of the child contract           |
| childId          | uint256 | ID of the child token                   |
| expectedParent   | address | Address of the expected parent contract |
| expectedParentId | uint256 | ID of the expected parent token         |

### getChildIndex

```solidity
function getChildIndex(address parentAddress, uint256 parentId, address childAddress, uint256 childId) external view returns (uint256)
```

Used to retrieve the given child's index in its parent's child tokens array.

#### Parameters

| Name          | Type    | Description                                             |
| ------------- | ------- | ------------------------------------------------------- |
| parentAddress | address | Address of the parent token's collection smart contract |
| parentId      | uint256 | ID of the parent token                                  |
| childAddress  | address | Address of the child token's colection smart contract   |
| childId       | uint256 | ID of the child token                                   |

#### Returns

| Name | Type    | Description                                                           |
| ---- | ------- | --------------------------------------------------------------------- |
| \_0  | uint256 | The index of the child token in the parent token's child tokens array |

### getParent

```solidity
function getParent(address childAddress, uint256 childId) external view returns (address parentAddress, uint256 parentId)
```

Used to retrieve the contract address and ID of the parent token of the specified child token.

_Reverts if child token is not owned by an NFT._

#### Parameters

| Name         | Type    | Description                                            |
| ------------ | ------- | ------------------------------------------------------ |
| childAddress | address | Address of the child token's collection smart contract |
| childId      | uint256 | ID of the child token                                  |

#### Returns

| Name          | Type    | Description                                             |
| ------------- | ------- | ------------------------------------------------------- |
| parentAddress | address | Address of the parent token's collection smart contract |
| parentId      | uint256 | ID of the parent token                                  |

## Errors

### RMRKChildNotFoundInParent

```solidity
error RMRKChildNotFoundInParent()
```

Attempting to find the index of a child token on a parent which does not own it.

### RMRKParentIsNotNFT

```solidity
error RMRKParentIsNotNFT()
```

Attempting an operation requiring the token being nested, while it is not

### RMRKUnexpectedParent

```solidity
error RMRKUnexpectedParent()
```

Attempting an operation expecting a parent to the token which is not the actual one

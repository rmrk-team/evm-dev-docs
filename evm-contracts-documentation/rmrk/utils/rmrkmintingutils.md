# RMRKMintingUtils

_RMRK team_

> RMRKMintingUtils

Smart contract of the RMRK minting utils module.

_This smart contract includes the top-level utilities for managing minting and implements OwnableLock by default.Max supply-related and pricing variables are immutable after deployment._

## Methods

### addContributor

```solidity
function addContributor(address contributor) external nonpayable
```

Adds a contributor to the smart contract.

_Can only be called by the owner._

#### Parameters

| Name        | Type    | Description                          |
| ----------- | ------- | ------------------------------------ |
| contributor | address | Address of the contributor's account |

### getLock

```solidity
function getLock() external view returns (bool)
```

Used to retrieve the status of a lockable smart contract.

#### Returns

| Name | Type | Description                                                                |
| ---- | ---- | -------------------------------------------------------------------------- |
| \_0  | bool | bool A boolean value signifying whether the smart contract has been locked |

### isContributor

```solidity
function isContributor(address contributor) external view returns (bool)
```

Used to check if the address is one of the contributors.

#### Parameters

| Name        | Type    | Description                                             |
| ----------- | ------- | ------------------------------------------------------- |
| contributor | address | Address of the contributor whose status we are checking |

#### Returns

| Name | Type | Description                                                          |
| ---- | ---- | -------------------------------------------------------------------- |
| \_0  | bool | Boolean value indicating whether the address is a contributor or not |

### maxSupply

```solidity
function maxSupply() external view returns (uint256)
```

Used to retrieve the maximum supply of the collection.

#### Returns

| Name | Type    | Description                                            |
| ---- | ------- | ------------------------------------------------------ |
| \_0  | uint256 | uint256 The maximum supply of tokens in the collection |

### owner

```solidity
function owner() external view returns (address)
```

Returns the address of the current owner.

#### Returns

| Name | Type    | Description |
| ---- | ------- | ----------- |
| \_0  | address | undefined   |

### pricePerMint

```solidity
function pricePerMint() external view returns (uint256)
```

Used to retrieve the price per mint.

#### Returns

| Name | Type    | Description                                                                                            |
| ---- | ------- | ------------------------------------------------------------------------------------------------------ |
| \_0  | uint256 | uint256 The price per mint of a single token expressed in the lowest denomination of a native currency |

### renounceOwnership

```solidity
function renounceOwnership() external nonpayable
```

Leaves the contract without owner. Functions using the `onlyOwner` modifier will be disabled.

_Can only be called by the current owner.Renouncing ownership will leave the contract without an owner, thereby removing any functionality that is only available to the owner._

### revokeContributor

```solidity
function revokeContributor(address contributor) external nonpayable
```

Removes a contributor from the smart contract.

_Can only be called by the owner._

#### Parameters

| Name        | Type    | Description                          |
| ----------- | ------- | ------------------------------------ |
| contributor | address | Address of the contributor's account |

### setLock

```solidity
function setLock() external nonpayable
```

Locks the operation.

_Once locked, functions using `notLocked` modifier cannot be executed._

### totalSupply

```solidity
function totalSupply() external view returns (uint256)
```

Used to retrieve the total supply of the tokens in a collection.

#### Returns

| Name | Type    | Description                                  |
| ---- | ------- | -------------------------------------------- |
| \_0  | uint256 | uint256 The number of tokens in a collection |

### transferOwnership

```solidity
function transferOwnership(address newOwner) external nonpayable
```

Transfers ownership of the contract to a new owner.

_Can only be called by the current owner._

#### Parameters

| Name     | Type    | Description                        |
| -------- | ------- | ---------------------------------- |
| newOwner | address | Address of the new owner's account |

### withdrawRaised

```solidity
function withdrawRaised(address to, uint256 amount) external nonpayable
```

Used to withdraw the minting proceedings to a specified address.

_This function can only be called by the owner._

#### Parameters

| Name   | Type    | Description                                                |
| ------ | ------- | ---------------------------------------------------------- |
| to     | address | Address to receive the given amount of minting proceedings |
| amount | uint256 | The amount to withdraw                                     |

## Events

### OwnershipTransferred

```solidity
event OwnershipTransferred(address indexed previousOwner, address indexed newOwner)
```

#### Parameters

| Name                    | Type    | Description |
| ----------------------- | ------- | ----------- |
| previousOwner `indexed` | address | undefined   |
| newOwner `indexed`      | address | undefined   |

## Errors

### RMRKNewContributorIsZeroAddress

```solidity
error RMRKNewContributorIsZeroAddress()
```

Attempting to assign a 0x0 address as a contributor

### RMRKNewOwnerIsZeroAddress

```solidity
error RMRKNewOwnerIsZeroAddress()
```

Attempting to transfer the ownership to the 0x0 address

### RMRKNotOwner

```solidity
error RMRKNotOwner()
```

Attempting to interact with a management function without being the smart contract's owner
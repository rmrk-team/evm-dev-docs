# OwnableLock

_RMRK team_

> OwnableLock

A minimal ownable lock smart contract.

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

### owner

```solidity
function owner() external view returns (address)
```

Returns the address of the current owner.

#### Returns

| Name | Type    | Description |
| ---- | ------- | ----------- |
| \_0  | address | undefined   |

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

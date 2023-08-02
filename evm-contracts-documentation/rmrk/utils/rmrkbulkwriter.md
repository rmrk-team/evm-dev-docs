# RMRKBulkWriter

_RMRK team_

> RMRKBulkWriter

Smart contract of the RMRK Bulk Writer module.

_Extra utility functions for RMRK contracts._

## Methods

### bulkEquip

```solidity
function bulkEquip(address collection, uint256 tokenId, RMRKBulkWriter.IntakeUnequip[] unequips, IERC6220.IntakeEquip[] equips) external nonpayable
```

#### Parameters

| Name       | Type                            | Description |
| ---------- | ------------------------------- | ----------- |
| collection | address                         | undefined   |
| tokenId    | uint256                         | undefined   |
| unequips   | RMRKBulkWriter.IntakeUnequip\[] | undefined   |
| equips     | IERC6220.IntakeEquip\[]         | undefined   |

### replaceEquip

```solidity
function replaceEquip(address collection, IERC6220.IntakeEquip data) external nonpayable
```

#### Parameters

| Name       | Type                 | Description |
| ---------- | -------------------- | ----------- |
| collection | address              | undefined   |
| data       | IERC6220.IntakeEquip | undefined   |

## Errors

### RMRKCanOnlyDoBulkOperationsOnOwnedTokens

```solidity
error RMRKCanOnlyDoBulkOperationsOnOwnedTokens()
```

Attempting to do a bulk operation on a token that is not owned by the caller

### RMRKCanOnlyDoBulkOperationsWithOneTokenAtATime

```solidity
error RMRKCanOnlyDoBulkOperationsWithOneTokenAtATime()
```

Attempting to do a bulk operation with multiple tokens at a time

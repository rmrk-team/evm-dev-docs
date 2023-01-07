# RMRKEquipRenderUtils

_RMRK team_

> RMRKEquipRenderUtils

Smart contract of the RMRK Equip render utils module.

_Extra utility functions for composing RMRK extended assets._

## Methods

### composeEquippables

```solidity
function composeEquippables(address target, uint256 tokenId, uint64 assetId) external view returns (string metadataURI, uint64 equippableGroupId, address catalogAddress, struct RMRKEquipRenderUtils.FixedPart[] fixedParts, struct RMRKEquipRenderUtils.EquippedSlotPart[] slotParts)
```

Used to compose the given equippables.

_The full `FixedPart` struct looks like this: \[ partId, z, metadataURI ]The full `EquippedSlotPart` struct looks like this: \[ partId, childAssetId, z, childAddress, childId, childAssetMetadata, partMetadata ]_

#### Parameters

| Name    | Type    | Description                                                    |
| ------- | ------- | -------------------------------------------------------------- |
| target  | address | Address of the smart contract of the given token               |
| tokenId | uint256 | ID of the token to compose the equipped items in the asset for |
| assetId | uint64  | ID of the asset being queried for equipped parts               |

#### Returns

| Name              | Type                                     | Description                                                                               |
| ----------------- | ---------------------------------------- | ----------------------------------------------------------------------------------------- |
| metadataURI       | string                                   | Metadata URI of the asset                                                                 |
| equippableGroupId | uint64                                   | Equippable group ID of the asset                                                          |
| catalogAddress    | address                                  | Address of the catalog to which the asset belongs to                                      |
| fixedParts        | RMRKEquipRenderUtils.FixedPart\[]        | An array of fixed parts respresented by the `FixedPart` structs present on the asset      |
| slotParts         | RMRKEquipRenderUtils.EquippedSlotPart\[] | An array of slot parts represented by the `EquippedSlotPart` structs present on the asset |

### getEquipped

```solidity
function getEquipped(address target, uint64 tokenId, uint64 assetId) external view returns (uint64[] slotPartIds, struct IRMRKEquippable.Equipment[] childrenEquipped)
```

Used to retrieve the equipped parts of the given token.

_NOTE: Some of the equipped children might be empty.The full `Equipment` struct looks like this: \[ assetId, childAssetId, childId, childEquippableAddress ]_

#### Parameters

| Name    | Type    | Description                                                     |
| ------- | ------- | --------------------------------------------------------------- |
| target  | address | Address of the smart contract of the given token                |
| tokenId | uint64  | ID of the token to retrieve the equipped items in the asset for |
| assetId | uint64  | ID of the asset being queried for equipped parts                |

#### Returns

| Name             | Type                         | Description                                                                 |
| ---------------- | ---------------------------- | --------------------------------------------------------------------------- |
| slotPartIds      | uint64\[]                    | An array of the IDs of the slot parts present in the given asset            |
| childrenEquipped | IRMRKEquippable.Equipment\[] | An array of `Equipment` structs containing info about the equipped children |

### getExtendedActiveAssets

```solidity
function getExtendedActiveAssets(address target, uint256 tokenId) external view returns (struct RMRKEquipRenderUtils.ExtendedActiveAsset[])
```

Used to get extended active assets of the given token.

_The full `ExtendedActiveAsset` looks like this: \[ ID, equippableGroupId, priority, catalogAddress, metadata, \[ fixedPartId0, fixedPartId1, fixedPartId2, slotPartId0, slotPartId1, slotPartId2 ] ]_

#### Parameters

| Name    | Type    | Description                                                |
| ------- | ------- | ---------------------------------------------------------- |
| target  | address | Address of the smart contract of the given token           |
| tokenId | uint256 | ID of the token to retrieve the extended active assets for |

#### Returns

| Name | Type                                        | Description                                                           |
| ---- | ------------------------------------------- | --------------------------------------------------------------------- |
| \_0  | RMRKEquipRenderUtils.ExtendedActiveAsset\[] | sturct\[] An array of ExtendedActiveAssets present on the given token |

### getExtendedPendingAssets

```solidity
function getExtendedPendingAssets(address target, uint256 tokenId) external view returns (struct RMRKEquipRenderUtils.ExtendedPendingAsset[])
```

Used to get the extended pending assets of the given token.

_The full `ExtendedPendingAsset` looks like this: \[ ID, equippableGroupId, acceptRejectIndex, replacesAssetWithId, catalogAddress, metadata, \[ fixedPartId0, fixedPartId1, fixedPartId2, slotPartId0, slotPartId1, slotPartId2 ] ]_

#### Parameters

| Name    | Type    | Description                                                 |
| ------- | ------- | ----------------------------------------------------------- |
| target  | address | Address of the smart contract of the given token            |
| tokenId | uint256 | ID of the token to retrieve the extended pending assets for |

#### Returns

| Name | Type                                         | Description                                                            |
| ---- | -------------------------------------------- | ---------------------------------------------------------------------- |
| \_0  | RMRKEquipRenderUtils.ExtendedPendingAsset\[] | sturct\[] An array of ExtendedPendingAssets present on the given token |

### splitSlotAndFixedParts

```solidity
function splitSlotAndFixedParts(uint64[] allPartIds, address catalogAddress) external view returns (uint64[] slotPartIds, uint64[] fixedPartIds)
```

Used to split slot and fixed parts.

#### Parameters

| Name           | Type      | Description                                                          |
| -------------- | --------- | -------------------------------------------------------------------- |
| allPartIds     | uint64\[] | \[] An array of `Part` IDs containing both, `Slot` and `Fixed` parts |
| catalogAddress | address   | An address of the catalog to which the given `Part`s belong to       |

#### Returns

| Name         | Type      | Description                                                       |
| ------------ | --------- | ----------------------------------------------------------------- |
| slotPartIds  | uint64\[] | An array of IDs of the `Slot` parts included in the `allPartIds`  |
| fixedPartIds | uint64\[] | An array of IDs of the `Fixed` parts included in the `allPartIds` |

## Errors

### RMRKNotComposableAsset

```solidity
error RMRKNotComposableAsset()
```

Attempting to compose an asset wihtout having an associated Catalog

### RMRKTokenHasNoAssets

```solidity
error RMRKTokenHasNoAssets()
```

Attempting to determine the asset with the top priority on a token without assets

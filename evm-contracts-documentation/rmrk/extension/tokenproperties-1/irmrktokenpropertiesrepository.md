# IRMRKTokenPropertiesRepository

_RMRK team_

> IRMRKTokenPropertiesRepository

Interface smart contract of the RMRK token properties extension.

## Methods

### getAddressTokenProperties

```solidity
function getAddressTokenProperties(address collection, uint256 tokenId, string[] addressKeys) external view returns (struct IRMRKTokenPropertiesRepository.AddressProperty[])
```

Used to get multiple address parameter values for a token.

_The `AddressProperty` struct contains the following fields: \[ string key, address value ]_

#### Parameters

| Name        | Type      | Description                                                  |
| ----------- | --------- | ------------------------------------------------------------ |
| collection  | address   | Address of the collection the token belongs to               |
| tokenId     | uint256   | ID of the token for which the properties are being retrieved |
| addressKeys | string\[] | An array of address keys to retrieve                         |

#### Returns

| Name | Type                                              | Description                           |
| ---- | ------------------------------------------------- | ------------------------------------- |
| \_0  | IRMRKTokenPropertiesRepository.AddressProperty\[] | An array of `AddressProperty` structs |

### getAddressTokenProperty

```solidity
function getAddressTokenProperty(address collection, uint256 tokenId, string key) external view returns (address)
```

Used to retrieve the address type token properties.

#### Parameters

| Name       | Type    | Description             |
| ---------- | ------- | ----------------------- |
| collection | address | The collection address  |
| tokenId    | uint256 | The token ID            |
| key        | string  | The key of the property |

#### Returns

| Name | Type    | Description                       |
| ---- | ------- | --------------------------------- |
| \_0  | address | The value of the address property |

### getBoolTokenProperties

```solidity
function getBoolTokenProperties(address collection, uint256 tokenId, string[] boolKeys) external view returns (struct IRMRKTokenPropertiesRepository.BoolProperty[])
```

Used to get multiple bool parameter values for a token.

_The `BoolProperty` struct contains the following fields: \[ string key, bool value ]_

#### Parameters

| Name       | Type      | Description                                                  |
| ---------- | --------- | ------------------------------------------------------------ |
| collection | address   | Address of the collection the token belongs to               |
| tokenId    | uint256   | ID of the token for which the properties are being retrieved |
| boolKeys   | string\[] | An array of bool keys to retrieve                            |

#### Returns

| Name | Type                                           | Description                        |
| ---- | ---------------------------------------------- | ---------------------------------- |
| \_0  | IRMRKTokenPropertiesRepository.BoolProperty\[] | An array of `BoolProperty` structs |

### getBoolTokenProperty

```solidity
function getBoolTokenProperty(address collection, uint256 tokenId, string key) external view returns (bool)
```

Used to retrieve the bool type token properties.

#### Parameters

| Name       | Type    | Description             |
| ---------- | ------- | ----------------------- |
| collection | address | The collection address  |
| tokenId    | uint256 | The token ID            |
| key        | string  | The key of the property |

#### Returns

| Name | Type | Description                    |
| ---- | ---- | ------------------------------ |
| \_0  | bool | The value of the bool property |

### getBytesTokenProperties

```solidity
function getBytesTokenProperties(address collection, uint256 tokenId, string[] bytesKeys) external view returns (struct IRMRKTokenPropertiesRepository.BytesProperty[])
```

Used to get multiple bytes parameter values for a token.

_The `BytesProperty` struct contains the following fields: \[ string key, bytes value ]_

#### Parameters

| Name       | Type      | Description                                                  |
| ---------- | --------- | ------------------------------------------------------------ |
| collection | address   | Address of the collection the token belongs to               |
| tokenId    | uint256   | ID of the token for which the properties are being retrieved |
| bytesKeys  | string\[] | An array of bytes keys to retrieve                           |

#### Returns

| Name | Type                                            | Description                         |
| ---- | ----------------------------------------------- | ----------------------------------- |
| \_0  | IRMRKTokenPropertiesRepository.BytesProperty\[] | An array of `BytesProperty` structs |

### getBytesTokenProperty

```solidity
function getBytesTokenProperty(address collection, uint256 tokenId, string key) external view returns (bytes)
```

Used to retrieve the bytes type token properties.

#### Parameters

| Name       | Type    | Description             |
| ---------- | ------- | ----------------------- |
| collection | address | The collection address  |
| tokenId    | uint256 | The token ID            |
| key        | string  | The key of the property |

#### Returns

| Name | Type  | Description                     |
| ---- | ----- | ------------------------------- |
| \_0  | bytes | The value of the bytes property |

### getStringTokenProperties

```solidity
function getStringTokenProperties(address collection, uint256 tokenId, string[] stringKeys) external view returns (struct IRMRKTokenPropertiesRepository.StringProperty[])
```

Used to get multiple sting parameter values for a token.

_The `StringProperty` struct contains the following fields: \[ string key, string value ]_

#### Parameters

| Name       | Type      | Description                                                  |
| ---------- | --------- | ------------------------------------------------------------ |
| collection | address   | Address of the collection the token belongs to               |
| tokenId    | uint256   | ID of the token for which the properties are being retrieved |
| stringKeys | string\[] | An array of string keys to retrieve                          |

#### Returns

| Name | Type                                             | Description                          |
| ---- | ------------------------------------------------ | ------------------------------------ |
| \_0  | IRMRKTokenPropertiesRepository.StringProperty\[] | An array of `StringProperty` structs |

### getStringTokenProperty

```solidity
function getStringTokenProperty(address collection, uint256 tokenId, string key) external view returns (string)
```

Used to retrieve the string type token properties.

#### Parameters

| Name       | Type    | Description             |
| ---------- | ------- | ----------------------- |
| collection | address | The collection address  |
| tokenId    | uint256 | The token ID            |
| key        | string  | The key of the property |

#### Returns

| Name | Type   | Description                      |
| ---- | ------ | -------------------------------- |
| \_0  | string | The value of the string property |

### getTokenProperties

```solidity
function getTokenProperties(address collection, uint256 tokenId, string[] stringKeys, string[] uintKeys, string[] boolKeys, string[] addressKeys, string[] bytesKeys) external view returns (struct IRMRKTokenPropertiesRepository.StringProperty[] stringProperties, struct IRMRKTokenPropertiesRepository.UintProperty[] uintProperties, struct IRMRKTokenPropertiesRepository.BoolProperty[] boolProperties, struct IRMRKTokenPropertiesRepository.AddressProperty[] addressProperties, struct IRMRKTokenPropertiesRepository.BytesProperty[] bytesProperties)
```

Used to retrieve multiple token properties of any type at once.

_The `StringProperty`, `UintProperty`, `BoolProperty`, `AddressProperty` and `BytesProperty` structs consists to the following fields (where `value` is of the appropriate type): \[ key, value, ]_

#### Parameters

| Name        | Type      | Description                                        |
| ----------- | --------- | -------------------------------------------------- |
| collection  | address   | The collection address                             |
| tokenId     | uint256   | The token ID                                       |
| stringKeys  | string\[] | An array of string type property keys to retrieve  |
| uintKeys    | string\[] | An array of uint type property keys to retrieve    |
| boolKeys    | string\[] | An array of bool type property keys to retrieve    |
| addressKeys | string\[] | An array of address type property keys to retrieve |
| bytesKeys   | string\[] | An array of bytes type property keys to retrieve   |

#### Returns

| Name              | Type                                              | Description                                                                  |
| ----------------- | ------------------------------------------------- | ---------------------------------------------------------------------------- |
| stringProperties  | IRMRKTokenPropertiesRepository.StringProperty\[]  | An array of `StringProperty` structs containing the string type properties   |
| uintProperties    | IRMRKTokenPropertiesRepository.UintProperty\[]    | An array of `UintProperty` structs containing the uint type properties       |
| boolProperties    | IRMRKTokenPropertiesRepository.BoolProperty\[]    | An array of `BoolProperty` structs containing the bool type properties       |
| addressProperties | IRMRKTokenPropertiesRepository.AddressProperty\[] | An array of `AddressProperty` structs containing the address type properties |
| bytesProperties   | IRMRKTokenPropertiesRepository.BytesProperty\[]   | An array of `BytesProperty` structs containing the bytes type properties     |

### getUintTokenProperties

```solidity
function getUintTokenProperties(address collection, uint256 tokenId, string[] uintKeys) external view returns (struct IRMRKTokenPropertiesRepository.UintProperty[])
```

Used to get multiple uint parameter values for a token.

_The `UintProperty` struct contains the following fields: \[ string key, uint value ]_

#### Parameters

| Name       | Type      | Description                                                  |
| ---------- | --------- | ------------------------------------------------------------ |
| collection | address   | Address of the collection the token belongs to               |
| tokenId    | uint256   | ID of the token for which the properties are being retrieved |
| uintKeys   | string\[] | An array of uint keys to retrieve                            |

#### Returns

| Name | Type                                           | Description                        |
| ---- | ---------------------------------------------- | ---------------------------------- |
| \_0  | IRMRKTokenPropertiesRepository.UintProperty\[] | An array of `UintProperty` structs |

### getUintTokenProperty

```solidity
function getUintTokenProperty(address collection, uint256 tokenId, string key) external view returns (uint256)
```

Used to retrieve the uint type token properties.

#### Parameters

| Name       | Type    | Description             |
| ---------- | ------- | ----------------------- |
| collection | address | The collection address  |
| tokenId    | uint256 | The token ID            |
| key        | string  | The key of the property |

#### Returns

| Name | Type    | Description                    |
| ---- | ------- | ------------------------------ |
| \_0  | uint256 | The value of the uint property |

### isCollaborator

```solidity
function isCollaborator(address collaborator, address collection) external view returns (bool)
```

Used to check if the specified address is listed as a collaborator of the given collection's parameter.

#### Parameters

| Name         | Type    | Description                |
| ------------ | ------- | -------------------------- |
| collaborator | address | Address to be checked.     |
| collection   | address | Address of the collection. |

#### Returns

| Name | Type | Description                                                                                                    |
| ---- | ---- | -------------------------------------------------------------------------------------------------------------- |
| \_0  | bool | Boolean value indicating if the address is a collaborator of the given collection's (`true`) or not (`false`). |

### isSpecificAddress

```solidity
function isSpecificAddress(address specificAddress, address collection, string key) external view returns (bool)
```

Used to check if the specified address is listed as a specific address of the given collection's parameter.

#### Parameters

| Name            | Type    | Description                |
| --------------- | ------- | -------------------------- |
| specificAddress | address | Address to be checked.     |
| collection      | address | Address of the collection. |
| key             | string  | The key of the property    |

#### Returns

| Name | Type | Description                                                                                                                  |
| ---- | ---- | ---------------------------------------------------------------------------------------------------------------------------- |
| \_0  | bool | Boolean value indicating if the address is a specific address of the given collection's parameter (`true`) or not (`false`). |

### manageAccessControl

```solidity
function manageAccessControl(address collection, string key, enum IRMRKTokenPropertiesRepository.AccessType accessType, address specificAddress) external nonpayable
```

Used to manage the access control settings for a specific parameter.

_Only the `issuer` of the collection can call this function.The possible `accessType` values are: \[ Issuer, Collaborator, IssuerOrCollaborator, TokenOwner, SpecificAddress, ]Emits an {AccessControlUpdated} event._

#### Parameters

| Name            | Type                                           | Description                                                                            |
| --------------- | ---------------------------------------------- | -------------------------------------------------------------------------------------- |
| collection      | address                                        | The address of the collection being managed.                                           |
| key             | string                                         | The key of the property                                                                |
| accessType      | enum IRMRKTokenPropertiesRepository.AccessType | The type of access control to be applied to the parameter.                             |
| specificAddress | address                                        | The address to be added as a specific addresses allowed to manage the given parameter. |

### manageCollaborators

```solidity
function manageCollaborators(address collection, address[] collaboratorAddresses, bool[] collaboratorAddressAccess) external nonpayable
```

Used to manage the collaborators of a collection.

_The `collaboratorAddresses` and `collaboratorAddressAccess` arrays must be of the same length.Emits a {CollaboratorUpdate} event._

#### Parameters

| Name                      | Type       | Description                                                                                                                 |
| ------------------------- | ---------- | --------------------------------------------------------------------------------------------------------------------------- |
| collection                | address    | The address of the collection                                                                                               |
| collaboratorAddresses     | address\[] | The array of collaborator addresses being managed                                                                           |
| collaboratorAddressAccess | bool\[]    | The array of boolean values indicating if the collaborator address should receive the permission (`true`) or not (`false`). |

### prepareMessageToPresignAddressProperty

```solidity
function prepareMessageToPresignAddressProperty(address collection, uint256 tokenId, string key, address value, uint256 deadline) external view returns (bytes32)
```

Used to retrieve the message to be signed for submitting a presigned address property change.

#### Parameters

| Name       | Type    | Description                                                                             |
| ---------- | ------- | --------------------------------------------------------------------------------------- |
| collection | address | The address of the collection smart contract of the token receiving the property        |
| tokenId    | uint256 | The ID of the token receiving the property                                              |
| key        | string  | The property key                                                                        |
| value      | address | The property value                                                                      |
| deadline   | uint256 | The deadline timestamp for the presigned transaction after which the message is invalid |

#### Returns

| Name | Type    | Description                                        |
| ---- | ------- | -------------------------------------------------- |
| \_0  | bytes32 | Raw message to be signed by the authorized account |

### prepareMessageToPresignBoolProperty

```solidity
function prepareMessageToPresignBoolProperty(address collection, uint256 tokenId, string key, bool value, uint256 deadline) external view returns (bytes32)
```

Used to retrieve the message to be signed for submitting a presigned bool property change.

#### Parameters

| Name       | Type    | Description                                                                             |
| ---------- | ------- | --------------------------------------------------------------------------------------- |
| collection | address | The address of the collection smart contract of the token receiving the property        |
| tokenId    | uint256 | The ID of the token receiving the property                                              |
| key        | string  | The property key                                                                        |
| value      | bool    | The property value                                                                      |
| deadline   | uint256 | The deadline timestamp for the presigned transaction after which the message is invalid |

#### Returns

| Name | Type    | Description                                        |
| ---- | ------- | -------------------------------------------------- |
| \_0  | bytes32 | Raw message to be signed by the authorized account |

### prepareMessageToPresignBytesProperty

```solidity
function prepareMessageToPresignBytesProperty(address collection, uint256 tokenId, string key, bytes value, uint256 deadline) external view returns (bytes32)
```

Used to retrieve the message to be signed for submitting a presigned bytes property change.

#### Parameters

| Name       | Type    | Description                                                                             |
| ---------- | ------- | --------------------------------------------------------------------------------------- |
| collection | address | The address of the collection smart contract of the token receiving the property        |
| tokenId    | uint256 | The ID of the token receiving the property                                              |
| key        | string  | The property key                                                                        |
| value      | bytes   | The property value                                                                      |
| deadline   | uint256 | The deadline timestamp for the presigned transaction after which the message is invalid |

#### Returns

| Name | Type    | Description                                        |
| ---- | ------- | -------------------------------------------------- |
| \_0  | bytes32 | Raw message to be signed by the authorized account |

### prepareMessageToPresignStringProperty

```solidity
function prepareMessageToPresignStringProperty(address collection, uint256 tokenId, string key, string value, uint256 deadline) external view returns (bytes32)
```

Used to retrieve the message to be signed for submitting a presigned string property change.

#### Parameters

| Name       | Type    | Description                                                                             |
| ---------- | ------- | --------------------------------------------------------------------------------------- |
| collection | address | The address of the collection smart contract of the token receiving the property        |
| tokenId    | uint256 | The ID of the token receiving the property                                              |
| key        | string  | The property key                                                                        |
| value      | string  | The property value                                                                      |
| deadline   | uint256 | The deadline timestamp for the presigned transaction after which the message is invalid |

#### Returns

| Name | Type    | Description                                        |
| ---- | ------- | -------------------------------------------------- |
| \_0  | bytes32 | Raw message to be signed by the authorized account |

### prepareMessageToPresignUintProperty

```solidity
function prepareMessageToPresignUintProperty(address collection, uint256 tokenId, string key, uint256 value, uint256 deadline) external view returns (bytes32)
```

Used to retrieve the message to be signed for submitting a presigned uint property change.

#### Parameters

| Name       | Type    | Description                                                                             |
| ---------- | ------- | --------------------------------------------------------------------------------------- |
| collection | address | The address of the collection smart contract of the token receiving the property        |
| tokenId    | uint256 | The ID of the token receiving the property                                              |
| key        | string  | The property key                                                                        |
| value      | uint256 | The property value                                                                      |
| deadline   | uint256 | The deadline timestamp for the presigned transaction after which the message is invalid |

#### Returns

| Name | Type    | Description                                        |
| ---- | ------- | -------------------------------------------------- |
| \_0  | bytes32 | Raw message to be signed by the authorized account |

### presignedSetAddressProperty

```solidity
function presignedSetAddressProperty(address setter, address collection, uint256 tokenId, string key, address value, uint256 deadline, uint8 v, bytes32 r, bytes32 s) external nonpayable
```

Used to set the address property on behalf of an authorized account.

_Emits a {AddressPropertyUpdated} event._

#### Parameters

| Name       | Type    | Description                                               |
| ---------- | ------- | --------------------------------------------------------- |
| setter     | address | Address of the account that presigned the property change |
| collection | address | Address of the collection receiving the property          |
| tokenId    | uint256 | The ID of the token receiving the property                |
| key        | string  | The property key                                          |
| value      | address | The property value                                        |
| deadline   | uint256 | The deadline timestamp for the presigned transaction      |
| v          | uint8   | `v` value of an ECDSA signature of the presigned message  |
| r          | bytes32 | `r` value of an ECDSA signature of the presigned message  |
| s          | bytes32 | `s` value of an ECDSA signature of the presigned message  |

### presignedSetBoolProperty

```solidity
function presignedSetBoolProperty(address setter, address collection, uint256 tokenId, string key, bool value, uint256 deadline, uint8 v, bytes32 r, bytes32 s) external nonpayable
```

Used to set the bool property on behalf of an authorized account.

_Emits a {BoolPropertyUpdated} event._

#### Parameters

| Name       | Type    | Description                                               |
| ---------- | ------- | --------------------------------------------------------- |
| setter     | address | Address of the account that presigned the property change |
| collection | address | Address of the collection receiving the property          |
| tokenId    | uint256 | The ID of the token receiving the property                |
| key        | string  | The property key                                          |
| value      | bool    | The property value                                        |
| deadline   | uint256 | The deadline timestamp for the presigned transaction      |
| v          | uint8   | `v` value of an ECDSA signature of the presigned message  |
| r          | bytes32 | `r` value of an ECDSA signature of the presigned message  |
| s          | bytes32 | `s` value of an ECDSA signature of the presigned message  |

### presignedSetBytesProperty

```solidity
function presignedSetBytesProperty(address setter, address collection, uint256 tokenId, string key, bytes value, uint256 deadline, uint8 v, bytes32 r, bytes32 s) external nonpayable
```

Used to set the bytes property on behalf of an authorized account.

_Emits a {BytesPropertyUpdated} event._

#### Parameters

| Name       | Type    | Description                                               |
| ---------- | ------- | --------------------------------------------------------- |
| setter     | address | Address of the account that presigned the property change |
| collection | address | Address of the collection receiving the property          |
| tokenId    | uint256 | The ID of the token receiving the property                |
| key        | string  | The property key                                          |
| value      | bytes   | The property value                                        |
| deadline   | uint256 | The deadline timestamp for the presigned transaction      |
| v          | uint8   | `v` value of an ECDSA signature of the presigned message  |
| r          | bytes32 | `r` value of an ECDSA signature of the presigned message  |
| s          | bytes32 | `s` value of an ECDSA signature of the presigned message  |

### presignedSetStringProperty

```solidity
function presignedSetStringProperty(address setter, address collection, uint256 tokenId, string key, string value, uint256 deadline, uint8 v, bytes32 r, bytes32 s) external nonpayable
```

Used to set the string property on behalf of an authorized account.

_Emits a {StringPropertyUpdated} event._

#### Parameters

| Name       | Type    | Description                                               |
| ---------- | ------- | --------------------------------------------------------- |
| setter     | address | Address of the account that presigned the property change |
| collection | address | Address of the collection receiving the property          |
| tokenId    | uint256 | The ID of the token receiving the property                |
| key        | string  | The property key                                          |
| value      | string  | The property value                                        |
| deadline   | uint256 | The deadline timestamp for the presigned transaction      |
| v          | uint8   | `v` value of an ECDSA signature of the presigned message  |
| r          | bytes32 | `r` value of an ECDSA signature of the presigned message  |
| s          | bytes32 | `s` value of an ECDSA signature of the presigned message  |

### presignedSetUintProperty

```solidity
function presignedSetUintProperty(address setter, address collection, uint256 tokenId, string key, uint256 value, uint256 deadline, uint8 v, bytes32 r, bytes32 s) external nonpayable
```

Used to set the uint property on behalf of an authorized account.

_Emits a {UintPropertyUpdated} event._

#### Parameters

| Name       | Type    | Description                                               |
| ---------- | ------- | --------------------------------------------------------- |
| setter     | address | Address of the account that presigned the property change |
| collection | address | Address of the collection receiving the property          |
| tokenId    | uint256 | The ID of the token receiving the property                |
| key        | string  | The property key                                          |
| value      | uint256 | The property value                                        |
| deadline   | uint256 | The deadline timestamp for the presigned transaction      |
| v          | uint8   | `v` value of an ECDSA signature of the presigned message  |
| r          | bytes32 | `r` value of an ECDSA signature of the presigned message  |
| s          | bytes32 | `s` value of an ECDSA signature of the presigned message  |

### registerAccessControl

```solidity
function registerAccessControl(address collection, address issuer, bool useOwnable) external nonpayable
```

Used to register a collection to use the RMRK token properties repository.

_If the collection does not implement the Ownable interface, the `useOwnable` value must be set to `false`.Emits an {AccessControlRegistration} event._

#### Parameters

| Name       | Type    | Description                                                                                                                                                                                                            |
| ---------- | ------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| collection | address | The address of the collection that will use the RMRK token properties repository.                                                                                                                                      |
| issuer     | address | The address of the issuer of the collection.                                                                                                                                                                           |
| useOwnable | bool    | The boolean value to indicate if the collection implements the Ownable interface and whether it should be used to validate that the caller is the issuer (`true`) or to use the manually set issuer address (`false`). |

### setAddressProperties

```solidity
function setAddressProperties(address collection, uint256 tokenId, IRMRKTokenPropertiesRepository.AddressProperty[] properties) external nonpayable
```

#### Parameters

| Name       | Type                                              | Description |
| ---------- | ------------------------------------------------- | ----------- |
| collection | address                                           | undefined   |
| tokenId    | uint256                                           | undefined   |
| properties | IRMRKTokenPropertiesRepository.AddressProperty\[] | undefined   |

### setAddressProperty

```solidity
function setAddressProperty(address collection, uint256 tokenId, string key, address value) external nonpayable
```

Used to set an address property.

_Emits a {AddressPropertyUpdated} event._

#### Parameters

| Name       | Type    | Description                                      |
| ---------- | ------- | ------------------------------------------------ |
| collection | address | Address of the collection receiving the property |
| tokenId    | uint256 | The token ID                                     |
| key        | string  | The property key                                 |
| value      | address | The property value                               |

### setBoolProperties

```solidity
function setBoolProperties(address collection, uint256 tokenId, IRMRKTokenPropertiesRepository.BoolProperty[] properties) external nonpayable
```

#### Parameters

| Name       | Type                                           | Description |
| ---------- | ---------------------------------------------- | ----------- |
| collection | address                                        | undefined   |
| tokenId    | uint256                                        | undefined   |
| properties | IRMRKTokenPropertiesRepository.BoolProperty\[] | undefined   |

### setBoolProperty

```solidity
function setBoolProperty(address collection, uint256 tokenId, string key, bool value) external nonpayable
```

Used to set a boolean property.

_Emits a {BoolPropertyUpdated} event._

#### Parameters

| Name       | Type    | Description                                      |
| ---------- | ------- | ------------------------------------------------ |
| collection | address | Address of the collection receiving the property |
| tokenId    | uint256 | The token ID                                     |
| key        | string  | The property key                                 |
| value      | bool    | The property value                               |

### setBytesProperties

```solidity
function setBytesProperties(address collection, uint256 tokenId, IRMRKTokenPropertiesRepository.BytesProperty[] properties) external nonpayable
```

#### Parameters

| Name       | Type                                            | Description |
| ---------- | ----------------------------------------------- | ----------- |
| collection | address                                         | undefined   |
| tokenId    | uint256                                         | undefined   |
| properties | IRMRKTokenPropertiesRepository.BytesProperty\[] | undefined   |

### setBytesProperty

```solidity
function setBytesProperty(address collection, uint256 tokenId, string key, bytes value) external nonpayable
```

Used to set an bytes property.

_Emits a {BytesPropertyUpdated} event._

#### Parameters

| Name       | Type    | Description                                      |
| ---------- | ------- | ------------------------------------------------ |
| collection | address | Address of the collection receiving the property |
| tokenId    | uint256 | The token ID                                     |
| key        | string  | The property key                                 |
| value      | bytes   | The property value                               |

### setStringProperties

```solidity
function setStringProperties(address collection, uint256 tokenId, IRMRKTokenPropertiesRepository.StringProperty[] properties) external nonpayable
```

#### Parameters

| Name       | Type                                             | Description |
| ---------- | ------------------------------------------------ | ----------- |
| collection | address                                          | undefined   |
| tokenId    | uint256                                          | undefined   |
| properties | IRMRKTokenPropertiesRepository.StringProperty\[] | undefined   |

### setStringProperty

```solidity
function setStringProperty(address collection, uint256 tokenId, string key, string value) external nonpayable
```

Used to set a string property.

_Emits a {StringPropertyUpdated} event._

#### Parameters

| Name       | Type    | Description                                      |
| ---------- | ------- | ------------------------------------------------ |
| collection | address | Address of the collection receiving the property |
| tokenId    | uint256 | The token ID                                     |
| key        | string  | The property key                                 |
| value      | string  | The property value                               |

### setTokenProperties

```solidity
function setTokenProperties(address collection, uint256 tokenId, IRMRKTokenPropertiesRepository.StringProperty[] stringProperties, IRMRKTokenPropertiesRepository.UintProperty[] uintProperties, IRMRKTokenPropertiesRepository.BoolProperty[] boolProperties, IRMRKTokenPropertiesRepository.AddressProperty[] addressProperties, IRMRKTokenPropertiesRepository.BytesProperty[] bytesProperties) external nonpayable
```

#### Parameters

| Name              | Type                                              | Description |
| ----------------- | ------------------------------------------------- | ----------- |
| collection        | address                                           | undefined   |
| tokenId           | uint256                                           | undefined   |
| stringProperties  | IRMRKTokenPropertiesRepository.StringProperty\[]  | undefined   |
| uintProperties    | IRMRKTokenPropertiesRepository.UintProperty\[]    | undefined   |
| boolProperties    | IRMRKTokenPropertiesRepository.BoolProperty\[]    | undefined   |
| addressProperties | IRMRKTokenPropertiesRepository.AddressProperty\[] | undefined   |
| bytesProperties   | IRMRKTokenPropertiesRepository.BytesProperty\[]   | undefined   |

### setUintProperties

```solidity
function setUintProperties(address collection, uint256 tokenId, IRMRKTokenPropertiesRepository.UintProperty[] properties) external nonpayable
```

#### Parameters

| Name       | Type                                           | Description |
| ---------- | ---------------------------------------------- | ----------- |
| collection | address                                        | undefined   |
| tokenId    | uint256                                        | undefined   |
| properties | IRMRKTokenPropertiesRepository.UintProperty\[] | undefined   |

### setUintProperty

```solidity
function setUintProperty(address collection, uint256 tokenId, string key, uint256 value) external nonpayable
```

Used to set a number property.

_Emits a {UintPropertyUpdated} event._

#### Parameters

| Name       | Type    | Description                                      |
| ---------- | ------- | ------------------------------------------------ |
| collection | address | Address of the collection receiving the property |
| tokenId    | uint256 | The token ID                                     |
| key        | string  | The property key                                 |
| value      | uint256 | The property value                               |

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

## Events

### AccessControlRegistration

```solidity
event AccessControlRegistration(address indexed collection, address indexed issuer, address indexed registeringAddress, bool useOwnable)
```

Used to notify listeners that a new collection has been registered to use the repository.

#### Parameters

| Name                         | Type    | Description                                                                                                                 |
| ---------------------------- | ------- | --------------------------------------------------------------------------------------------------------------------------- |
| collection `indexed`         | address | Address of the collection                                                                                                   |
| issuer `indexed`             | address | Address of the issuer of the collection; the addess authorized to manage the access control                                 |
| registeringAddress `indexed` | address | Address that registered the collection                                                                                      |
| useOwnable                   | bool    | A boolean value indicating whether the collection uses the Ownable extension to verify the issuer (`true`) or not (`false`) |

### AccessControlUpdate

```solidity
event AccessControlUpdate(address indexed collection, string key, enum IRMRKTokenPropertiesRepository.AccessType accessType, address specificAddress)
```

Used to notify listeners that the access control settings for a specific parameter have been updated.

#### Parameters

| Name                 | Type                                           | Description                                                                             |
| -------------------- | ---------------------------------------------- | --------------------------------------------------------------------------------------- |
| collection `indexed` | address                                        | Address of the collection                                                               |
| key                  | string                                         | The name of the parameter for which the access control settings have been updated       |
| accessType           | enum IRMRKTokenPropertiesRepository.AccessType | The AccessType of the parameter for which the access control settings have been updated |
| specificAddress      | address                                        | The specific addresses that has been updated                                            |

### AddressPropertyUpdated

```solidity
event AddressPropertyUpdated(address indexed collection, uint256 indexed tokenId, string key, address value)
```

Used to notify listeners that an address property has been updated.

#### Parameters

| Name                 | Type    | Description                   |
| -------------------- | ------- | ----------------------------- |
| collection `indexed` | address | The collection address        |
| tokenId `indexed`    | uint256 | The token ID                  |
| key                  | string  | The key of the property       |
| value                | address | The new value of the property |

### BoolPropertyUpdated

```solidity
event BoolPropertyUpdated(address indexed collection, uint256 indexed tokenId, string key, bool value)
```

Used to notify listeners that a boolean property has been updated.

#### Parameters

| Name                 | Type    | Description                   |
| -------------------- | ------- | ----------------------------- |
| collection `indexed` | address | The collection address        |
| tokenId `indexed`    | uint256 | The token ID                  |
| key                  | string  | The key of the property       |
| value                | bool    | The new value of the property |

### BytesPropertyUpdated

```solidity
event BytesPropertyUpdated(address indexed collection, uint256 indexed tokenId, string key, bytes value)
```

Used to notify listeners that a bytes property has been updated.

#### Parameters

| Name                 | Type    | Description                   |
| -------------------- | ------- | ----------------------------- |
| collection `indexed` | address | The collection address        |
| tokenId `indexed`    | uint256 | The token ID                  |
| key                  | string  | The key of the property       |
| value                | bytes   | The new value of the property |

### CollaboratorUpdate

```solidity
event CollaboratorUpdate(address indexed collection, address indexed collaborator, bool isCollaborator)
```

Used to notify listeners that a new collaborator has been added or removed.

#### Parameters

| Name                   | Type    | Description                                                                                      |
| ---------------------- | ------- | ------------------------------------------------------------------------------------------------ |
| collection `indexed`   | address | Address of the collection                                                                        |
| collaborator `indexed` | address | Address of the collaborator                                                                      |
| isCollaborator         | bool    | A boolean value indicating whether the collaborator has been added (`true`) or removed (`false`) |

### StringPropertyUpdated

```solidity
event StringPropertyUpdated(address indexed collection, uint256 indexed tokenId, string key, string value)
```

Used to notify listeners that a string property has been updated.

#### Parameters

| Name                 | Type    | Description                   |
| -------------------- | ------- | ----------------------------- |
| collection `indexed` | address | The collection address        |
| tokenId `indexed`    | uint256 | The token ID                  |
| key                  | string  | The key of the property       |
| value                | string  | The new value of the property |

### UintPropertyUpdated

```solidity
event UintPropertyUpdated(address indexed collection, uint256 indexed tokenId, string key, uint256 value)
```

Used to notify listeners that an uint property has been updated.

#### Parameters

| Name                 | Type    | Description                   |
| -------------------- | ------- | ----------------------------- |
| collection `indexed` | address | The collection address        |
| tokenId `indexed`    | uint256 | The token ID                  |
| key                  | string  | The key of the property       |
| value                | uint256 | The new value of the property |

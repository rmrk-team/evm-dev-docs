---
description: Specification of the expected metadata formatting
---

# Metadata formatting

RMRK standards expect the metadata to be structured according to [ERC-721 specification](https://eips.ethereum.org/EIPS/eip-721). Having multiple kinds of resources (assets, parts, and collections) means that there is some variation in the metadata of each:

## Metadata examples

Examples of metadata structures for all of the resources.

### Collection metadata

Here is an example of the metadata of the collection:

```json5
{
  "name": "Collection Name",
  "description": "The description of the collection",
  "mediaUri": "ipfs://mediaOfTheCollection",
  "externalUri": "https://uriToTheProjectWebsite",
  "license": "License name",
  "licenseUri": "https://uriToTheLicense",
  "tags": ["tags", "used", "to", "help", "marketplaces", "categorize", "the", "asset", "or", "token"],
}
```

### Asset metadata

Here is an example of the metadata of an [ERC-5773](https://eips.ethereum.org/EIPS/eip-5773) compliant asset:

```json5
{
  "name": "Asset Name",
  "description": "The description of the token or asset",
  "mediaUri": "ipfs://mediaOfTheAssetOrToken",
  "thumbnailUri": "ipfs://thumbnailOfTheAssetOrToken",
  "externalUri": "https://uriToTheProjectWebsite",
  "license": "License name",
  "licenseUri": "https://uriToTheLicense",
  "tags": ["tags", "used", "to", "help", "marketplaces", "categorize", "the", "asset", "or", "token"],
  "preferThumb": false, // A boolean flag indicating to UIs to prefer thumbnailUri instead of mediaUri wherever applicable
  "attributes": [
    {
      "label": "rarity",
      "type": "string",
      "value": "epic",
      // For backward compatibility
      "trait_type": "rarity"
    },
    {
      "label": "color",
      "type": "string",
      "value": "red",
      // For backward compatibility
      "trait_type": "color"
    },
    {
      "label": "height",
      "type": "float",
      "value": 192.4,
      // For backward compatibility
      "trait_type": "height",
      "display_type": "number"
    }
  ]
}
```

### Catalog part metadata

Here is an example of the metadata of an [ERC-6220](https://eips.ethereum.org/EIPS/eip-6220) compliant part:

```json5
{
  "name": "Kanaria headwear slot",
  "description": "This is a Kanaria headwear slot, you can equip nested NFTs with a compatible asset in it.",
  "mediaUri": "ipfs://ipfs/XXXX/headwear_slot_fallback.svg",
  "attributes": [
    {
      "label": "rarity",
      "type": "string",
      "value": "rare",
      // For Opensea backward compatibility
      "trait_type": "rarity"
    }
  ]
}
```

## &#x20;Metadata schema definition

The top-level metadata types supported are:

<table><thead><tr><th width="199">Base metadata field</th><th width="79">Type</th><th width="173">Description</th><th>Required</th></tr></thead><tbody><tr><td><code>name</code></td><td>string</td><td>Resource name.</td><td>✅</td></tr><tr><td><code>description</code></td><td>string</td><td>General notes, abstracts, or summaries about content.</td><td>❌</td></tr><tr><td><code>license</code></td><td>string</td><td>The name of the license appended to the resource.</td><td>❌</td></tr><tr><td><code>licenseUri</code></td><td>string</td><td>The URI linking to the license body.</td><td>❌</td></tr><tr><td><code>mediaUri</code></td><td>string</td><td>The URI to the main media file of the resource.</td><td>❌</td></tr><tr><td><code>thumbnailUri</code></td><td>string</td><td>The URI to be used in wallets and client applications, where a scaled-down image is needed in order to present the resource to the end user.</td><td>❌</td></tr><tr><td><code>tags</code></td><td>array</td><td>An array of string values used to help marketplaces categorize the resource.</td><td>❌</td></tr><tr><td><code>preferThumb</code></td><td>bool</td><td>The flag used to signal to UIs to prefer the <code>thumbnailUri</code> instead of <code>mediaUri</code> where applicable.</td><td>❌</td></tr><tr><td><code>attributes</code></td><td>array</td><td>An array of custom attributes specific to the resource it represents.</td><td>❌</td></tr></tbody></table>

### Supported attribute types

Attributes can be completely custom to cater to the resource they are describing. The supported attribute types are:

* `number`
* `float`
* `integer`
* `string`
* `date`
* `percentage`
* `boolean`

To observe how the attributes array is structured, you can refer to the [Asset metadata example](metadata-formatting.md#asset-metadata) above.

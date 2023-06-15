---
description: How to get your collection listed on Singular marketplace
---

# List collection on Singular

The [Singular marketplace](https://singular.app) is the most advanced NFT marketplace to date with support for [ERC-5773](https://eips.ethereum.org/EIPS/eip-5773), [ERC-6059](https://eips.ethereum.org/EIPS/eip-6059), [ERC-6220](https://eips.ethereum.org/EIPS/eip-6220), [ERC-6381](https://eips.ethereum.org/EIPS/eip-6381), and [ERC-6454](https://eips.ethereum.org/EIPS/eip-6454) in addition to the support for [ERC-721](https://eips.ethereum.org/EIPS/eip-721), [ERC-2981](https://eips.ethereum.org/EIPS/eip-2981), and other standard NFT-powering ERCs.

To ensure the best results when the collection is displayed, we prepared a list of suggested extensions to implement:

* [**Ownable**](https://github.com/rmrk-team/evm/blob/dev/contracts/RMRK/access/Ownable.sol) or [**OwnableLock**](https://github.com/rmrk-team/evm/blob/dev/contracts/RMRK/access/OwnableLock.sol): Used for access control or for access control with the ability to lock the operation of the smart contract
* [**RMRKCore**](https://github.com/rmrk-team/evm/blob/dev/contracts/RMRK/core/RMRKCore.sol): Used to set the `name` and `symbol` of the collection
* [**RMRKRoyalties**](https://github.com/rmrk-team/evm/blob/dev/contracts/RMRK/extension/RMRKRoyalties.sol): Used to configure secondary sale royalties compatible with ERC-2981
* [**RMRKCollectionMetadata**](https://github.com/rmrk-team/evm/blob/dev/contracts/RMRK/utils/RMRKCollectionMetadata.sol): Used to provide the collection metadata
* [**RMRKTokenURI**](https://github.com/rmrk-team/evm/blob/dev/contracts/RMRK/utils/RMRKTokenURI.sol): Used to provide token URI and power enumerable tokens
* [**RMRKMintingUtils**](https://github.com/rmrk-team/evm/blob/dev/contracts/RMRK/utils/RMRKMintingUtils.sol): Used to provide information about token supply and minting

In order to be eligible for your collection to be listed on the Singular marketplace, it **MUST** implement and contain the following:

* [Access control](list-collection-on-singular.md#access-control) with `owner` top-level entity
* [Collection information](list-collection-on-singular.md#collection-information), including `name` and `symbol`
* [RMRK lego](list-collection-on-singular.md#rmrk-lego)

#### Access control

We rely on the existence of the `owner` entity in order to verify the management operations done through the marketplace. This means the `owner` view function must be exposed in your collection.

As this is a common practice in all of the smart contracts implementing the _Ownable_ pattern, you should be compatible using any version of it. We suggest you use the [**Ownable**](https://github.com/rmrk-team/evm/blob/dev/contracts/RMRK/access/Ownable.sol) or [**OwnableLock**](https://github.com/rmrk-team/evm/blob/dev/contracts/RMRK/access/OwnableLock.sol) from [**@rmrk-team/evm-contracts**](https://www.npmjs.com/package/@rmrk-team/evm-contracts?activeTab=versions) as it provides an additional management role compatible with the Singular marketplace called `contributor`. This allows you to appoint additional users to help you manage your collection via the marketplace.

If you are wondering why we are providing custom **Ownable** implementation, you can refer to the [FAQ](../frequently-asked-questions/faq.md#why-do-we-implement-some-of-the-smart-contracts-that-are-already-provided-in-other-packages-like-ope) where we explain that.

#### Collection information

In order for the collection to be eligible to be presented in the Singular marketplace, it needs to have its `name` and `symbol` exposed so that the marketplace can pick it up. Most of the metadata extensions contain it, but we suggest using any of the RMRK lego smart contracts from [**@rmrk-team/evm-contracts**](https://www.npmjs.com/package/@rmrk-team/evm-contracts?activeTab=versions) as they import the [**RMRKCore**](https://github.com/rmrk-team/evm/blob/dev/contracts/RMRK/core/RMRKCore.sol) smart contract, which includes the `name` and `symbol` values.

Additionally, we suggest using [**RMRKCollectionMetadata**](https://github.com/rmrk-team/evm/blob/dev/contracts/RMRK/utils/RMRKCollectionMetadata.sol), which extends your collection by adding collection-wide metadata support.

#### RMRK lego

As the Singular marketplace is specially equipped to present the next generation of Non-Fungible Tokens, it is crucial that your collection meets other advanced collections listed on Singular. If your collection was built without the powers of NFT 2.0, you can still wrap the tokens in order to power them up to reach the functionality of NFTs 2.0.

If you are still deciding on which RMRK lego to use and don't want to implement all of the base logic yourself, we encourage you to explore [ready-to-use implementations](https://github.com/rmrk-team/evm/tree/dev/contracts/implementations) that are documented in the [Implementations](../evm-contracts-documentation/implementations/) section.

#### Additional notes

The [**@rmrk-team/evm-package**](https://www.npmjs.com/package/@rmrk-team/evm-contracts?activeTab=versions) offers many more powerful extensions to supercharge your collection. We invite you to explore them and build the best collection out there!

### Metadata

As there are more metadata-bearing resources when using NFTs 2.0, we prepared an overview of the expected metadata for each. You can refer to the structure of the metadata of collection, asset, and catalog part in the [Metadata formatting](metadata-formatting.md) section.

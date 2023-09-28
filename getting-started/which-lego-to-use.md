---
description: A page to help you decide which RMRK lego to use
---

# Which lego to use?

## How to decide which lego to use?

The decision on which RMRK lego implementation to use can be daunting as there is a lot to pick from, but the following questions might help. Additionally, you can refer to the [decision flowchart](which-lego-to-use.md#flowchart).

We provide minimal implementations of our standards as well as ready-to-use implementations. The former allow for more business logic customization but also require custom core logic implementation. The latter provide fully usable smart contracts that require little to no modifications but have less space for customization.

If you require minimal implementation in order to implement more custom business logic, you can refer to the [Minimal Implementation](which-lego-to-use.md#minimal-implementation) section.

If you require the ready-to-use implementation, you can refer to the [Ready-to-use Implementation](which-lego-to-use.md#ready-to-use-implementation) section.

### Minimal Implementation

There is a number of available minimal implementation smart contracts available:

#### RMRKNestable

`RMRKNestable` provides the minimal implementation of RMRK nestable lego, also known as [ERC-7401](https://eips.ethereum.org/EIPS/eip-7401). It allows the nesting of NFTs into one another.

* You can refer to the `RMRKNestable` documentation [here](../evm-contracts-documentation/rmrk/nestable/rmrknestable.md)
* You can refer to the `RMRKNestable` source code [here](https://github.com/rmrk-team/evm/blob/master/contracts/RMRK/nestable/RMRKNestable.sol)

In order to import the RMRKNestable into your smart contract, you can import it from `@rmrk-team/evm-contracts`:

```solidity
import "@rmrk-team/evm-contracts/contracts/RMRK/nestable/RMRKNestable.sol";
```

#### RMRKMultiAsset

`RMRKMultiAsset` provides the minimal implementation of RMRK multi-asset lego, also known as [ERC-5773](https://eips.ethereum.org/EIPS/eip-5773). It allows a single token to have multiple assets.

* You can refer to the `RMRKMultiAsset` documentation [here](broken-reference)
* You can refer to the `RMRKMultiAsset` source code [here](https://github.com/rmrk-team/evm/blob/master/contracts/RMRK/multiasset/RMRKMultiAsset.sol)

In order to import the `RMRKMultiAsset` into your smart contract, you can import it from `@rmrk-team/evm-contracts`:

```solidity
import "@rmrk-team/evm-contracts/contracts/RMRK/multiasset/RMRKMultiAsset.sol";
```

#### RMRKNestableMultiAsset

`RMRKNestableMultiAsset` provides the minimal implementation of joined RMRK nestable and multi-asset legos, also known as [ERC-7401](https://eips.ethereum.org/EIPS/eip-7401) and [ERC-5773](https://eips.ethereum.org/EIPS/eip-5773). It allows tokens to be nested into one another and every single token to have multiple assets.

* You can refer to the `RMRKNestableMultiAsset` documentation [here](../evm-contracts-documentation/rmrk/nestable/rmrknestablemultiasset.md)
* You can refer to the `RMRKNestableMultiAsset` source code [here](https://github.com/rmrk-team/evm/blob/master/contracts/RMRK/nestable/RMRKNestableMultiAsset.sol)

In order to import the `RMRKNestableMultiAsset` into your smart contract, you can import it from `@rmrk-team/evm-contracts`:

```solidity
import "@rmrk-team/evm-contracts/contracts/RMRK/nestable/RMRKNestableMultiAsset.sol";
```

#### RMRKEquippable

{% hint style="info" %}
The `RMRKEquippable` is considered the merged equippable RMRK lego composite as it uses two smart contracts (Equippable and Core) to provide the full Equippable capabilities. This means that there are fewer smart contracts to manage, but there is also very little space for customization.
{% endhint %}

`RMRKEquippable` provides the minimal implementation of RMRK equippable lego, also known as ERC-6220. It allows tokens to be equipped into other tokens. In addition to the Equippable smart contract, you also need to set up the RMRK catalog lego.

* You can refer to the `RMRKEquippable` documentation [here](../evm-contracts-documentation/implementations/erc-20-pay/rmrkequippablelazyminterc20.md)
* You can refer to the `RMRKEquippable` source code [here](https://github.com/rmrk-team/evm/blob/master/contracts/RMRK/equippable/RMRKEquippable.sol)

In order to import the `RMRKEquippable` into your smart contract, you can import it from `@rmrk-team/evm-contracts`:

```solidity
import "@rmrk-team/evm-contracts/contracts/RMRK/equippable/RMRKEquippable.sol";
```

* You can refer to the `RMRKCatalog` documentation [here](../evm-contracts-documentation/rmrk/catalog/rmrkcatalog.md)
* You can refer to the `RMRKCatalog` source code [here](https://github.com/rmrk-team/evm/blob/master/contracts/RMRK/catalog/RMRKCatalog.sol)

In order to import the RMRKCatalog into your smart contract, you can import it from `@rmrk-team/evm-contracts`:

```solidity
import "@rmrk-team/evm-contracts/contracts/RMRK/catalog/RMRKCatalog.sol";
```

#### RMRKMinifiedEquippable

{% hint style="info" %}
The `RMRKMinifiedEquippable` is considered the merged equippable RMRK lego composite as it uses two smart contracts (minified Equippable and Core) to provide the full Equippable capabilities. This means that there are fewer smart contracts to manage, but there is also not a lot of space for customization. However, the minified Equippable has more space for customization than `RMRKEquippable` since the redundant inherited functions have been manually removed.
{% endhint %}

`RMRKMinifiedEquippable` provides the minimal implementation of RMRK equippable lego composite, also known as ERC-6220. It allows tokens to be equipped into other tokens. In addition to the Equippable smart contract, you also need to set up the RMRK catalog lego.

* You can refer to the `RMRKMinifiedEquippable` documentation [here](../evm-contracts-documentation/rmrk/equippable-1/rmrkminifiedequippable.md)
* You can refer to the `RMRKMinifiedEquippable` source code [here](https://github.com/rmrk-team/evm/blob/master/contracts/RMRK/equippable/RMRKMinifiedEquippable.sol)

In order to import the `RMRKMinifiedEquippable` into your smart contract, you can import it from `@rmrk-team/evm-contracts`:

```solidity
import "@rmrk-team/evm-contracts/contracts/RMRK/equippable/RMRKMinifiedEquippable.sol";
```

* You can refer to the `RMRKCatalog` documentation [here](../evm-contracts-documentation/rmrk/catalog/rmrkcatalog.md)
* You can refer to the `RMRKCatalog` source code [here](https://github.com/rmrk-team/evm/blob/master/contracts/RMRK/catalog/RMRKCatalog.sol)

In order to import the RMRKCatalog into your smart contract, you can import it from `@rmrk-team/evm-contracts`:

```solidity
import "@rmrk-team/evm-contracts/contracts/RMRK/catalog/RMRKCatalog.sol";
```

### Ready-to-use Implementation

There is a number of ready-to-use implementation smart contracts available. Each of the implementations also has three variations:

* The lazy mint native implementations are designed around minting being paid by the native token of the chain to which the smart contract is deployed.
* The lazy mint ERC-20 implementations are designed to support paying for token minting using ERC-20 tokens.
* The premint implementations are designed for minting to be done by the issuer and distributed later.

#### Nestable

The `RMRKNestableLazyMintNative` provides a ready-to-use native token pay implementation of RMRK nestable lego, also known as the [ERC-7401](https://eips.ethereum.org/EIPS/eip-7401) allowing NFTs to be nested into other NFTs.

* You can refer to the `RMRKNestableLazyMintNative` documentation [here](../evm-contracts-documentation/implementations/native-token-pay/rmrknestablelazymintnative.md)
* You can refer to the `RMRKNestableLazyMintNative` source code [here](https://github.com/rmrk-team/evm/blob/master/contracts/implementations/lazyMintNative/RMRKNestableLazyMintNative.sol)

In order to import the `RMRKNestableImpl` into your smart contract, you can import it from `@rmrk-team/evm-contracts`:

```solidity
import "@rmrk-team/evm-contracts/contracts/implementations/lazyMintNative/RMRKNestableLazyMintNative.sol";
```

The `RMRKNestableLazyMintErc20` provides a ready-to-use ERC-20 pay implementation of RMRK nestable lego, also known as the [ERC-7401](https://eips.ethereum.org/EIPS/eip-7401) allowing NFTs to be nested into other NFTs.

* You can refer to the `RMRKNestableLazyMintErc20` documentation [here](../evm-contracts-documentation/implementations/erc-20-pay/rmrknestablelazyminterc20soulbound.md)
* You can refer to the `RMRKNestableLazyMintErc20` source code [here](https://github.com/rmrk-team/evm/blob/master/contracts/implementations/lazyMintErc20/RMRKNestableLazyMintErc20.sol)

In order to import the `RMRKNestablelazyMintErc20` into your smart contract, you can import it from `@rmrk-team/evm-contracts`:

```solidity
import "@rmrk-team/evm-contracts/contracts/implementations/lazyMintErc20/RMRKNestableLazyMintErc20.sol";
```

The `RMRKNestablePreMint` provides a ready-to-use premint implementation of RMRK nestable lego, also known as the [ERC-7401](https://eips.ethereum.org/EIPS/eip-7401) allowing NFTs to be nested into other NFTs.

* You can refer to the `RMRKNestablePreMint` documentation [here](../evm-contracts-documentation/implementations/premint/rmrknestablepremint.md)
* You can refer to the `RMRKNestablePreMint` source code [here](https://github.com/rmrk-team/evm/blob/master/contracts/implementations/premint/RMRKNestablePreMint.sol)

In order to import the `RMRKNestableImplPreMint` into your smart contract, you can import it from `@rmrk-team/evm-contracts`:

```solidity
import "@rmrk-team/evm-contracts/contracts/implementations/premint/RMRKNestablePreMint.sol";
```

#### MultiAsset

The `RMRKMultiAssetLazyMintNative` provides a ready-to-use native token pay implementation of RMRK multi-asset lego, also known as the [ERC-5773](https://eips.ethereum.org/EIPS/eip-5773) allowing NFTs to have multiple assets.

* You can refer to the `RMRKMultiAssetLazyMintNative` documentation [here](../evm-contracts-documentation/implementations/native-token-pay/rmrkmultiassetlazymintnative.md)
* You can refer to the `RMRKMultiAssetLazyMintNative` source code [here](https://github.com/rmrk-team/evm/blob/master/contracts/implementations/lazyMintNative/RMRKMultiAssetLazyMintNative.sol)

In order to import the `RMRKMultiAssetLazyMintNative` into your smart contract, you can import it from `@rmrk-team/evm-contracts`:

```solidity
import "@rmrk-team/evm-contracts/contracts/implementations/lazyMintNative/RMRKMultiAssetLazyMintNative.sol";
```

The `RMRKMultiAssetLazyMintErc20` provides a ready-to-use ERC-20 pay implementation of RMRK multi-asset lego, also known as the [ERC-5773](https://eips.ethereum.org/EIPS/eip-5773) allowing NFTs to have multiple assets.

* You can refer to the `RMRKMultiAssetLazyMintErc20` documentation [here](../evm-contracts-documentation/implementations/erc-20-pay/rmrkmultiassetlazyminterc20.md)
* You can refer to the `RMRKMultiAssetLazyMintErc20` source code [here](https://github.com/rmrk-team/evm/blob/master/contracts/implementations/lazyMintErc20/RMRKMultiAssetLazyMintErc20.sol)

In order to import the `RMRKMultiAssetLazyMintErc20` into your smart contract, you can import it from `@rmrk-team/evm-contracts`:

```solidity
import "@rmrk-team/evm-contracts/contracts/implementations/LazyMintErc20/RMRKMultiAssetLazyMintErc20.sol";
```

The `RMRKMultiAssetPreMint` provides a ready-to-use premint implementation of RMRK multi-asset lego, also known as the [ERC-5773](https://eips.ethereum.org/EIPS/eip-5773) allowing NFTs to have multiple assets.

* You can refer to the `RMRKMultiAssetPreMint` documentation [here](../evm-contracts-documentation/implementations/premint/rmrkmultiassetpremint.md)
* You can refer to the `RMRKMultiAssetPreMint` source code [here](https://github.com/rmrk-team/evm/blob/master/contracts/implementations/premint/RMRKMultiAssetPreMint.sol)

In order to import the `RMRKMultiAssetPreMint` into your smart contract, you can import it from `@rmrk-team/evm-contracts`:

```solidity
import "@rmrk-team/evm-contracts/contracts/implementations/premint/RMRKMultiAssetPreMint.sol";
```

#### Nestable with MultiAsset

The `RMRKNestableMultiAssetLazyMintNative` provides a ready-to-use native token pay implementation of RMRK nestable and multi-asset legos, also known as the [ERC-7401](https://eips.ethereum.org/EIPS/eip-7401) and [ERC-5773](https://eips.ethereum.org/EIPS/eip-5773) allowing NFTs to be nested into after other NFTs and to have multiple assets.

* You can refer to the `RMRKNestableMultiAssetLazyMintNative` documentation [here](../evm-contracts-documentation/implementations/native-token-pay/rmrknestablemultiassetlazymintnative.md)
* You can refer to the `RMRKNestableMultiAssetLazyMintNative` source code [here](https://github.com/rmrk-team/evm/blob/master/contracts/implementations/lazyMintNative/RMRKNestableMultiAssetLazyMintNative.sol)

In order to import the `RMRKNestableMultiAssetLazyMintNative` into your smart contract, you can import it from `@rmrk-team/evm-contracts`:

```solidity
import "@rmrk-team/evm-contracts/contracts/implementations/lazyMintNative/RMRKNestableMultiAssetLazyMintNative.sol";
```

The `RMRKNestableMultiAssetLazyMintErc20` provides a ready-to-use ERC-20 pay implementation of RMRK nestable and multi-asset legos, also known as the [ERC-7401](https://eips.ethereum.org/EIPS/eip-7401) and [ERC-5773](https://eips.ethereum.org/EIPS/eip-5773) allowing NFTs to be nested into after other NFTs and to have multiple assets.

* You can refer to the `RMRKNestableMultiAssetLazyMintErc20` documentation [here](../evm-contracts-documentation/implementations/erc-20-pay/rmrknestablemultiassetlazyminterc20.md)
* You can refer to the `RMRKNestableMultiAssetLazyMintErc20` source code [here](https://github.com/rmrk-team/evm/blob/master/contracts/implementations/lazyMintErc20/RMRKNestableMultiAssetLazyMintErc20.sol)

In order to import the `RMRKNestableMultiAssetLazyMintErc20` into your smart contract, you can import it from `@rmrk-team/evm-contracts`:

```solidity
import "@rmrk-team/evm-contracts/contracts/implementations/LazyMintErc20/RMRKNestableMultiAssetLazyMintErc20.sol";
```

The `RMRKNestableMultiAssetPreMint` provides a ready-to-use premint implementation of RMRK nestable and multi-asset legos, also known as the [ERC-7401](https://eips.ethereum.org/EIPS/eip-7401) and [ERC-5773](https://eips.ethereum.org/EIPS/eip-5773) allowing NFTs to be nested into after other NFTs and to have multiple assets.

* You can refer to the `RMRKNestableMultiAssetPreMint` documentation [here](../evm-contracts-documentation/implementations/premint/rmrknestablemultiassetpremint.md)
* You can refer to the `RMRKNestableMultiAssetPreMint` source code [here](https://github.com/rmrk-team/evm/blob/master/contracts/implementations/premint/RMRKNestableMultiAssetPreMint.sol)

In order to import the `RMRKNestableMultiAssetPreMint` into your smart contract, you can import it from `@rmrk-team/evm-contracts`:

```solidity
import "@rmrk-team/evm-contracts/contracts/implementations/premint/RMRKNestableMultiAssetPreMint.sol";
```

#### Equippable

The `RMRKEquippableLazyMintNative` provides a ready-to-use native token pay implementation of RMRK equippable lego, also known as the [ERC-6220](https://eips.ethereum.org/EIPS/eip-6220) allowing NFTs to be equipped into other NFTs.

* You can refer to the `RMRKEquippableLazyMintNative` documentation [here](../evm-contracts-documentation/implementations/native-token-pay/rmrkequippablelazymintnative.md)
* You can refer to the `RMRKEquippableLazyMintNative` source code [here](https://github.com/rmrk-team/evm/blob/master/contracts/implementations/lazyMintNative/RMRKEquippableLazyMintNative.sol)

In order to import the `RMRKEquippableLazyMintNative` into your smart contract, you can import it from `@rmrk-team/evm-contracts`:

```solidity
import "@rmrk-team/evm-contracts/contracts/implementations/lazyMintNative/RMRKEqippableLazyMintNative.sol";
```

The `RMRKEquippableLazyMintErc20` provides a ready-to-use ERC-20 pay implementation of RMRK equippable lego, also known as the [ERC-6220](https://eips.ethereum.org/EIPS/eip-6220) allowing NFTs to be equipped into other NFTs.

* You can refer to the `RMRKEquippableLazyMintErc20` documentation [here](../evm-contracts-documentation/implementations/erc-20-pay/rmrkequippablelazyminterc20.md)
* You can refer to the `RMRKEquippableLazyMintErc20` source code [here](https://github.com/rmrk-team/evm/blob/master/contracts/implementations/lazyMintErc20/RMRKEquippableLazyMintErc20.sol)

In order to import the `RMRKEquippableLazyMintErc20` into your smart contract, you can import it from `@rmrk-team/evm-contracts`:

```solidity
import "@rmrk-team/evm-contracts/contracts/implementations/lazyMintErc20/RMRKEquippableLazyMintErc20.sol";
```

The `RMRKEquippablePreMint` provides a ready-to-use premint implementation of RMRK equippable lego, also known as the [ERC-6220](https://eips.ethereum.org/EIPS/eip-6220) allowing NFTs to be equipped into other NFTs.

* You can refer to the `RMRKEquippablePreMint` documentation [here](../evm-contracts-documentation/implementations/premint/rmrkequippablepremint.md)
* You can refer to the `RMRKEquippablePreMint` source code [here](https://github.com/rmrk-team/evm/blob/master/contracts/implementations/premint/RMRKEquippablePreMint.sol)

In order to import the `RMRKEquippablePreMint` into your smart contract, you can import it from `@rmrk-team/evm-contracts`:

```solidity
import "@rmrk-team/evm-contracts/contracts/implementations/premint/RMRKEquippablePreMint.sol";
```

{% hint style="info" %}
Please remember that any implementation of Equippable lego requires Catalog as well.
{% endhint %}

* You can refer to the `RMRKCatalogImpl` documentation [here](../evm-contracts-documentation/implementations/rmrkcatalogimpl.md)
* You can refer to the `RMRKCatalogImpl` source code [here](https://github.com/rmrk-team/evm/blob/master/contracts/implementations/RMRKCatalogImpl.sol)

In order to import the `RMRKCatalogImpl` into your smart contract, you can import it from `@rmrk-team/evm-contracts`:

```solidity
import "@rmrk-team/evm-contracts/contracts/implementations/RMRKCatalogImpl.sol";l
```

## Flowchart

The following flowchart can help you decide which RMRK smart contract to use as the basis of your solution:

```mermaid
flowchart TD
    A(Do you want to use a\nready-to-use-implementation\nor a customizable version?) -->|Ready-to-use implementation| B(Use the smart contracts that end with 'Impl')
    A ----->|More customizable implemetation| C(Use the smart contract from the `RMRK`directory)
    B --> D(Do you want the ability to exclusively\nnest the tokens, exclusively use multi-asset,\nuse nestable and multi-asset,\nor to have equippable tokens)
    D -->|Exclusively nest the tokens| E(Use RMRKNestableImpl)
    D -->|Exclusively use multi-asset| F(Use RMRKMultiAssetImpl)
    D -->|Use nestable with multi-asset| G(Use RMRKNestableMultiAssetImpl)
    D -->|Use equippable| H(Use RMRK EquippableImpl)
    C --> I(Do you want the ability to exclusively\nnest the tokens, exclusively use multi-asset,\nuse nestable and multi-asset,\nor to have equippable tokens)
    I -->|Exclusively nest tokens| J(Use RMRKNestable)
    I -->|Exclusively use multi-asset| K(Use RMRKMultiAsset)
    I -->|Use nestable and multi-asset| L(Use RMRKNestableMultiAsset)
    I -->|Use equippable| M(Use RMRKEquippable and RMRKCatalog)
```

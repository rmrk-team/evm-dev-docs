---
description: Introduction to RMRK legos EVM examples.
---

# RMRK Solidity

A set of Solidity sample contracts using the RMRK standard implementation on EVM.

<figure><img src="../../.gitbook/assets/RMRK EVM Smart Contracts_rev3.png" alt=""><figcaption><p>Possible combinations of RMRK legos</p></figcaption></figure>

## Installation

You can start using the RMRK EVM implementation smart contracts by installing the dependency to your project:

```shell
npm install @rmrk-team/evm-contracts
```

Once you have installed the `@rmrk-team/evm-contracts` dependency, you can refer to one of the samples residing in this section's pages. The versions starting with `Simple` keyword are ready to use; you can simply extend those for your own contracts and pass fixed or variable parameters to the constructor. The examples starting with `Advanced` keyword showcase the implementation where you have more freedom in implementing custom business logic. The available internal functions when building it are outlined within the examples.

{% hint style="danger" %}
The usage examples of package **v2.0.0** are coming soon. The current examples are of the previous version.
{% endhint %}

## RMRK EVM implementation examples

This section contains the examples of using RMRK legos to build your own smart contracts. Every example uses the `@rmrk-team/evm-contracts` dependency in order to implement the examples. Adding it allows you to easily include them in your own smart contracts.

The examples included are:

1. [`MultiAsset`](multiasset.md)
2. [`Nestable`](nestable.md)
3. [`Nestable with MultiAsset`](nestable-with-multiasset.md)
4. [`MergedEquippable`](mergedequippable.md)
5. [`SplitEquippable`](splitequippable.md)

Additionally we have render util contracts. The reason these are separate is to save contract space. You can have a single deploy of those and use them on any number of contracts or even use the existing ones (we will provide them in the future):

1. `MultiAsset render utils` provides utilities to get asset objects from IDs, and accepted or pending asset objects for a given token. The MultiAsset lego provides only IDs for the latter.
2. `Equip render utils` provides the same shortcuts on extended assets (with equip information). This utility smart contract also has views to get information about what is currently equipped to a token and to compose equippables for a token asset.

To follow along using modifiable and runnable code, you can clone our examples repository:

{% embed url="https://github.com/rmrk-team/evm-sample-contracts" %}

{% hint style="info" %}
**NOTE: This is a living collection of examples, which will get updated as the RMRK EVM implementation evolves.**
{% endhint %}

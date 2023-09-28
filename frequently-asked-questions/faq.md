---
description: Answers to frequently asked questions.
---

# FAQ

{% hint style="info" %}
Do you have any feedback on your development experience with RMRK standards or any questions left unanswered? Let us know in our [feedback form](https://docs.google.com/forms/d/1jTHJsZ7GT\_umZol3HT6YghWCQRsWuQ382DWJRShx9EA)!
{% endhint %}

#### Are RMRK legos compatible with ERC-721?

Yes, we ensured that all our legos and extensions are backward compatible with ERC-721 and the existing tooling to build and interact with ERC-721-compatible smart contracts.

#### Does using RMRK smart contracts require xcRMRK?

The xcRMRK token is not necessary to use RMRK NFT 2.0 contracts in any way - the protocols and standards are open-source and free to use. However, adding utility to xcRMRK by integrating it meaningfully into your hackathon project might improve your score.

#### Where can we find a list of all the ERCs/EIPs that RMRK has published?

The list can be found in the [RMRK legos](../general-overview/rmrk-legos/) and [RMRK extensions](../general-overview/rmrk-extensions/) sections, but also here:

* [ERC-5773: Context-Dependent Multi-Asset Tokens](https://eips.ethereum.org/EIPS/eip-5773)
* [ERC-7401: Parent-Governed Non-Fungible Tokens Nesting](https://eips.ethereum.org/EIPS/eip-7401)
* [ERC-6220: Composable NFTs utilizing Equippable Parts](https://eips.ethereum.org/EIPS/eip-6220)
* [ERC-6381: Public Non-Fungible Token Emote Repository](https://eips.ethereum.org/EIPS/eip-6381)
* [ERC-6454: Minimal Transferable NFT detection interface](https://eips.ethereum.org/EIPS/eip-6454)
* [ERC-7508: Dynamic On-Chain Token Attributes Repository](https://eips.ethereum.org/EIPS/eip-7508)

#### What networks can be used to deploy the RMRK-powered smart contracts?

You can deploy the Solidity implementation of RMRK legos and the extensions to any EVM-compatible network. However, if you intend to utilize Singular, the next-generation marketplace already supporting RMRK primitives, we suggest you consider the currently supported networks.

#### Why do we implement some of the smart contracts that are already provided in other packages like OpenZeppelin's?

The decision to implement our own utility smart contracts is an optimization decision. Since RMRK standards are highly evolved, they take up a lot of smart contract space, and since the smart contract file sizes are limited, we had to optimize them.

One of the main space-saving steps taken is the use of predefined errors in favor of stringified errors and the unification of some management functions (i.e., instead of having a function to add a contributor and another to remove a contributor, we only have one function that either adds or removes them).

#### Where can we find the up-to-date notes on the changes of the `@rmrk-team/evm-contracts`?

All of the changes to the package are recorded in a congested way in the [CHANGELOG](https://github.com/rmrk-team/evm/blob/master/CHANGELOG.md) we are keeping.

{% embed url="https://github.com/rmrk-team/evm/blob/master/CHANGELOG.md" %}

Additionally, you can read all about the changes in the most recent version in our [blog](https://www.rmrk.app/blog) titled _Developer Notes_.

{% embed url="https://www.rmrk.app/blog/developer-notes-on-rmrk-team-evm-contracts-v2-0-0" %}

{% embed url="https://www.rmrk.app/blog/arcane-developer-notes-introduction-of-rmrk-wizard" %}

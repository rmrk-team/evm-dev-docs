---
description: Introduction of Catalog and Equippable RMRK legos
---

# Catalog and Equippable NFTs

A Catalog can be considered a _colleciton of parts_ from which an NFT can be composed. Parts can be either of the `slot` type or `fixed` type. Slots are intended for equippables.

{% hint style="info" %}
**NOTE: A catalog is referenced in an NFT as a separate** [**asset**](multiasset.md) **by specifying the catalog and cherry picking the list of parts from the catalog for that NFT instance.**
{% endhint %}

Catalogs can be of different media types.

The catalogs's type indicates what the final output of an NFT will be when this resource is being rendered. Supported types are PNG, SVG, audio, video, even mixed.

The most important concept to understand with regard to equippables is that the final output is not static. Equipping, e.g., a hat onto a rhino does not generate a new static image in place of an old one. Instead, the hat is dynamically rendered _inside_ the image of the rhino, and the image of the rhino has to be prepared for this functionality in advance.

This is what the Catalog system allows: minting collections with equippability in mind, regardless of type - audio files can be prepared with slots for audio stems, movie catalogs can be prepared with filter slots, but video files can also have a slot for subtitles, or even an alternative audio track, and more.

## EIP-6220: Composable NFTs utilizing Equippable Parts

We published an Ethereum Improvement Proposal detailing the specification of the Equippable RMRK lego. If you are interested, you can access it here:

{% embed url="https://eips.ethereum.org/EIPS/eip-6220" %}
EIP-6220: Composable NFTs utilizing Equippable Parts
{% endembed %}

---
description: What are RMRK legos?
---

# RMRK legos

RMRK is a set of NFT standards which compose several "NFT 2.0 lego" primitives. Putting these legos together allows a user to create NFT systems of arbitrary complexity.

There are various possibilities on how to combine these legos, all of which are ERC721 compatible:

1. MultiAsset ([Context-Dependent Multi-Asset Tokens](https://eips.ethereum.org/EIPS/eip-5773))
   * Only uses the MultiAsset RMRK lego
2. Nestable (Parent-Governed Nestable Non-Fungible Tokens)
   * Only uses the Nestable RMRK lego
3. Nestable with MultiAsset
   * Uses both Nestable and MultiAsset RMRK legos
4. Equippable MultiAsset with Nestable and Catalog
   * Merged equippable is a more compact RMRK lego composite that uses less smart contracts, but has less space for custom logic implementation
   * Split equippable is a more customisable RMRK lego composite that uses more smart contracts, but has more space for custom logic implementation

The first 3 use cases have stand alone versions with both minimal and ready to use implementations. The latter two, due to Solidity contract size constraints, MultiAsset and Equippable logic are included in a single smart contract, while Nestable and ownership are handled by either the same smart contract or a separate one. Catalog is also a separate smart contract for practical reasons, since one Catalog can be used by multiple tokens.

<figure><img src="../../.gitbook/assets/RMRK EVM Smart Contracts_rev3.png" alt=""><figcaption><p>Infographic of RMRK lego combinations</p></figcaption></figure>

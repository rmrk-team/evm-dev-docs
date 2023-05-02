---
description: Introduction of MultiAsset RMRK lego
---

# MultiAsset (ERC-5773)

The Multi-Asset RMRK lego allows for the construction of a new primitive: context-dependent output of information per single NFT.

The context-dependent output of information means that the asset in an appropriate format is displayed based on how the token is being accessed. I.e. if the token is being opened in an e-book reader, the PDF asset is displayed, if the token is opened in the marketplace, the PNG or the SVG asset is displayed, if the token is accessed from within a game, the 3D model asset is accessed and if the token is accessed by the (Internet of Things) IoT hub, the asset providing the necessary addressing and specification information is accessed.

An NFT can have multiple assets (outputs), which can be any kind of file to be served to the consumer, and orders them by priority. They do not have to match in mimetype or tokenURI, nor do they depend on one another. Assets are not standalone entities, but should be thought of as “namespaced tokenURIs” that can be ordered at will by the NFT owner, but only modified, updated, added, or removed if agreed on by both the owner of the token and the issuer of the token.

## ERC-5773: Context-Dependent Multi-Asset tokens

We published an Ethereum Improvement Proposal detailing the specification of the MultiAsset RMRK lego. If you are interested, you can access it here:

{% embed url="https://eips.ethereum.org/EIPS/eip-5773" %}
ERC-5773: Context-Dependent Multi-Asset Tokens
{% endembed %}

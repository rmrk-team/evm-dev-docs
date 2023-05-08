---
description: RMRK Soulbound extension
---

# Soulbound (ERC-6454)

Soulbound RMRK extension allows for a design of non-transferable tokens.

We provide implementations for multiple approaches to making a token non-transferable:

1. Tokens are non-transferable from when they are minted
2. Tokens become non-transferable after a specified block
3. Tokens become non-transferable after a predefined number of transactions
4. Tokens can be set as non-transferable on a per-token basis

Additionally, the Soulbound implementation supports limiting transferability based on the sending and receiving address.

## ERC-6454: Minimal Transferable NFT detection interface

We published an Ethereum Improvement Proposal detailing the specification of the Soulbound RMRK extension. If you are interested, you can access it here:

{% embed url="https://eips.ethereum.org/EIPS/eip-6454" %}
ERC-6454: Minimal Transferable NFT detection interface
{% endembed %}

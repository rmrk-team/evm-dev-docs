---
description: Example of Nestable & MultiAsset RMRK lego usage in zkSync.
---

# Using Nestable and MultiAsset RMRK legos in zkSync

This workshop examines the Nestable and MultiAsset RMRK legos in action and shows how they can be used to create a new next-generation NFT collection.

The easiest way of doing so, is by defining a use case utilizing both legos and then building a collection around it. So let's do just that!

## Use Case

The use case we will be implementing in this workshop is a music album. The album will be a collection of NFTs, each representing a song in the album. Each song can be represented by multiple assets, such as an audio file, a lyric sheet, etc. The album itself will also be represented by a single NFT, which will be the parent of all the songs. The album NFT will also contain multiple assets such as album artwork, metadata about the album, such as the artist, the release date, etc.

We will use a fictitious artist called _**"The RMRKables"**_ to demonstrate the use case. The album they released as NFTs is called _**"The RMRKables - Next Generation"**_. And it will contain the following songs:

* Into the Future
* My Utility
* Minbend

The album NFT will live in its own collection, while the songs will live in their own collection. The album NFT will contain the artwork to be displayed in the music applications and a json file containing the metadata about the album.

The song NFTs will contain the audio file, the lyric sheet, and the metadata about the song, such as the title, the artist, the duration, etc. They will be nested into the album NFT and form the whole.

## Setup

We've prepared a template repository for you to get started with. It includes a simple `Equippable` smart contract, tests, deploy script and network configuration. Our smart contract development package, `@rmrk-team/evm-contracts` is included as well. You can find it here: [https://github.com/rmrk-team/evm-template/tree/zksync](https://github.com/rmrk-team/evm-template/tree/zksync).

The easiest way to get started is to fork the template repository and clone it to your local machine. You can do so by clicking the "Use this template" button on the template repository page.

{% hint style="info" %}
**NOTE: If you intend to use the template repository with the ZKSync network, make sure to select the `Include all branches` option and use the `zksync` branch.**
{% endhint %}

Once you have the template repository cloned to your local machine, you can install the dependencies by running the following command:

```bash
yarn install
```

You can explore the template repository, compile the smart contract and run the tests by running the following commands:

```bash
yarn hardhat compile && yarn hardhat test
```

Once you are ready, you can remove the `Equippable` smart contract and the tests for it. You can also remove the `deploy.js` scrip as we will not be using them in this workshop:

```bash
rm contracts/SimpleEquippable.sol && rm test/equippable.ts && rm scripts/deploy.ts
```

## Building the smart contracts

Now that we have the template repository set up, we can start building the smart contracts.

### Album

We will start by creating a new smart contract for the Album NFT. We will call it `Album.sol` and place it in the `contracts` folder.

The skeleton of the smart contract will look like this:

```solidity
// SPDX-License-Identifier: Apache-2.0
pragma solidity ^0.8.18;

contract Album {

}
```

As the Album NFT will utilize the `Nestable` as well as `MultiAsset` lego, we will need to import them into the smart contract. In addition to the separate smart contracts for each lego, we also provide a unified smart contract that contains both. We will import the [`RMRKNestableMultiAsset.sol`](https://github.com/rmrk-team/evm/blob/master/contracts/RMRK/nestable/RMRKNestableMultiAsset.sol) smart contract:

```solidity
import "@rmrk-team/evm-contracts/contracts/RMRK/nestable/RMRKNestableMultiAsset.sol";
```

In addition to the `RMRKNestableMultiAsset` smart contract, we will also need to import the `Ownable` smart contract from OpenZeppelin. We will us it to provide simple access control to the smart contract:

```solidity
import "@openzeppelin/contracts/access/Ownable.sol";
```

Now that we have the required smart contracts imported, we can inherit from them in our `Album` smart contract:

```solidity
contract Album is RMRKNestableMultiAsset, Ownable {

}
```

To properly initialize the `RMRKNestableMultiAsset` smart contract, we need to pass the `name_` and `symbol_` parameters to the constructor. We will pass them, as constructor parameters:

```solidity
    constructor(
        string memory name_,
        string memory symbol_
    ) RMRKNestableMultiAsset(name_, symbol_) {}
```

#### Mint

We can now start implementing the functionality. We will start by implementing the `mint` function. The `mint` function will be used to mint the Album NFT. It will take the `to` address as a parameter and will mint the NFT to that address. It will also take the `amount` parameter, which will be an unsigned integer defining the amount of tokens to be minted at the same time.

In order to automatically increment the token IDs, we need to define a the total and maximum supply of the collection. To do so, we will define the `totalSupply` and `maxSupply` variables. We will make them public, so that we are able to use the auto-generated getters to retrieve their values:

```solidity
    uint256 public totalSupply;
    uint256 public maxSupply;
```

As the initial `totalSupply` will be `0`, we don't need to assign any value to it when deploying the smart contract. However, we will need to assign a value to the `maxSupply` variable. We will assign its value in the constructor using the `maxSupply_` parameter. The updated `constructor` should look like this:

```solidity
    constructor(
        string memory name_,
        string memory symbol_,
        uint256 maxSupply_
    ) RMRKNestableMultiAsset(name_, symbol_) {
        maxSupply = maxSupply_;
    }
```

The execution of the minting function should be reverted if attempting to mint `0` tokens, minting to `0x0` address or if minting the desired `amount` of tokens would exceed the `maxSupply` of the collection. If any of these conditions are met, the execution should be reverted with custom errors. To be able to use them, they need to be defined below the import statements:

```solidty
error MintOverMaxSupply();
error ZeroAddress();
error ZeroAmount();
```

The `_mint` function of the `RMRKNestableMultiAsset` accepts the minting destination, the ID of the token to be minted and the `data` field (to which we will pass an empty value). To properly mint the desired amount of tokens, we need to make sure that the IDs don't overlap and that the total and maximum supply values are kept up to date. To do so, we will define a `nextTokenId` variable, which will be used to keep track of the next token ID to be minted. We will also update the total supply and use it to keep track of how many more tokens we can mint.

We also need to make sure that only the owner is allowed to call the `mint` function, so we need to include the `onlyOwner` modifier as well.

The `mint` function will look like this:

```solidity
    function mint(address to, uint256 amount) public onlyOwner {
        if ( amount == 0 ) revert ZeroAmount();
        if ( to == address(0) ) revert ZeroAddress();
        if ( totalSupply + amount > maxSupply ) revert MintOverMaxSupply();

        uint256 nextTokenId = totalSupply + 1;
        unchecked {
            totalSupply += amount;
        }
        uint256 totalSupplyOffset = maxSupply + 1;

        for (uint256 i = nextTokenId; i < totalSupplyOffset; ){
            _safeMint(to, i, "");
            unchecked {
                i++;
            }
        }
    }
```

{% hint style="info" %}
**NOTE: You might have noticed that minting doesn't support token ID of `0`. This is because the RMRK legos don't allow the use of the ID `0`. This is a design decision allowing us to provide clean NFT nesting experience.**
{% endhint %}

As the Album NFTs won't be nested, but will act as parent tokens, we don't need to implement nest transfers for this collection. We do however need to implement the functions to add the asset entries and add them to the tokens.

#### Add asset entry

We will add `addAssetEntry` function, which will be used to add the asset entries to the smart contract. One asset can be assigned to multiple tokens, so asset management is more streamlined than adding assets on a per-token level.

The internal `_addAssetEntry` function we will be using accepts ID of the asset to be added and the metadata URI of the asset. In order to simplify the management of asset IDs we will add a global `numberOfAssets` variable. We will define its visibility as public, so that we are able to use the auto-generated getter to retrieve its value when interacting with the smart contract:

```solidity
    uint64 public numberOfAssets;
```

Our `addAssetEntry` function now needs to accept the metadata URI pointing to the metadata of the asset. We will also need to make sure that only the owner is allowed to call the `addAssetEntry` function, so we need to include the `onlyOwner` modifier as well.

Similarly to the token IDs, the asset ID can't be `0`, so we need to take this into account when adding the new asset entry.

The `addAssetEntry` function will look like this:

```solidity
    function addAssetEntry(string memory metadataURI) public onlyOwner {
        unchecked {
            numberOfAssets++;
        }
        _addAssetEntry(numberOfAssets, metadataURI);
    }
```

#### Add asset to token

Once the asset entry is added to the smart contract, it can be added to the tokens. The internal function `_addAssetToToken` accepts the ID of the token to which the asset will be added, the ID of the asset to be added and the asset ID of the asset to be replaced by the asset being added. The asset ID of the asset to be replaced can be `0`, which means that the asset will be added to the token, but won't replace an existing asset.

We will design `addAssetToTokens` in a way that accepts an array of token IDs that should receive the asset and the ID of the asset to be added. As we only intend to add assets to the tokens, we will hardcode the asset ID of the asset to be replaced to `0`.

Since the assets need to be accepted once they are added to a token, we will streamline the process by accepting the asset if the token is owned by the owner of the smart contract. This will allow us to add the assets to the tokens without the need to accept them manually.

To check whether the token receiving the asset is owned by the owner of the smart contract, we will use the `ownerOf` function. The `ownerOf` function returns the _**root owner**_ of the token, which means that if the token is nested, it will return the address of the owner of the parent token. This is the address we need to check against the owner of the smart contract. We can afford to make the assumption that the tokens aren't nested, as the Album NFTs won't be nested.

Another assumption we will be making is that the newly added asset resides in the last position of the pending array of the token. This is because the assets are added to the pending array in the order they are added to the token. This means that the asset being added will always be the last one in the pending array. An important distinction compared to token IDs to note is that the pending array is zero-indexed, so the last asset will have the index of `length - 1`.

Additionally only the owner should be allowed to call the `addAssetToTokens` function, so we will include the `onlyOwner` modifier as well.

The `addAssetToTokens` function will look like this:

```solidity
    function addAssetToTokens(uint256[] memory tokenIds, uint64 assetId) public onlyOwner {
        for (uint256 i = 0; i < tokenIds.length; ) {
            _addAssetToToken(tokenIds[i], assetId, 0);

            if ( ownerOf(tokenIds[i]) == msg.sender ) {
                uint256 assetIndex = getPendingAssets(tokenIds[i]).length - 1;
                acceptAsset(tokenIds[i], assetIndex, assetId);
            }

            unchecked {
                i++;
            }
        }
    }
```

<details>

<summary>Click to see the full code of the Album smart contract</summary>

```solidity
    // SPDX-License-Identifier: Apache-2.0
    pragma solidity ^0.8.18;

    import "@rmrk-team/evm-contracts/contracts/RMRK/nestable/RMRKNestableMultiAsset.sol";
    import "@openzeppelin/contracts/access/Ownable.sol";

    error MintOverMaxSupply();
    error ZeroAddress();
    error ZeroAmount();

    contract Album is RMRKNestableMultiAsset, Ownable {
        uint256 public totalSupply;
        uint256 public maxSupply;
        uint64 public numberOfAssets;

        constructor(
            string memory name_,
            string memory symbol_,
            uint256 maxSupply_
        ) RMRKNestableMultiAsset(name_, symbol_) {
            maxSupply = maxSupply_;
        }

        function mint(address to, uint256 amount) public onlyOwner {
            if (amount == 0) revert ZeroAmount();
            if (to == address(0)) revert ZeroAddress();
            if (totalSupply + amount > maxSupply) revert MintOverMaxSupply();

            uint256 nextTokenId = totalSupply + 1;
            unchecked {
                totalSupply += amount;
            }
            uint256 totalSupplyOffset = totalSupply + 1;

            for (uint256 i = nextTokenId; i < totalSupplyOffset; ) {
                _safeMint(to, i, "");
                unchecked {
                    i++;
                }
            }
        }

        function addAssetEntry(string memory metadataURI) public onlyOwner {
            unchecked {
                numberOfAssets++;
            }
            _addAssetEntry(numberOfAssets, metadataURI);
        }

        function addAssetToTokens(
            uint256[] memory tokenIds,
            uint64 assetId
        ) public onlyOwner {
            for (uint256 i = 0; i < tokenIds.length; ) {
                _addAssetToToken(tokenIds[i], assetId, 0);

                if (ownerOf(tokenIds[i]) == msg.sender) {
                    uint256 assetIndex = getPendingAssets(tokenIds[i]).length - 1;
                    acceptAsset(tokenIds[i], assetIndex, assetId);
                }

                unchecked {
                    i++;
                }
            }
        }
    }
```

</details>

With this, we have the minimum required functions to mint the Album NFTs. We can now move on to creating the Song NFTs smart contract.

### Song

The Song NFTs will contain songs that are part of the album. The Song NFTs will be nested into the Album NFTs. We will call the smart contract for them `Song.sol` and place it in the `contracts` folder.

The skeleton of the smart contract will look like this:

```solidity
// SPDX-License-Identifier: Apache-2.0
pragma solidity ^0.8.18;

contract Song {

}
```

Just like the [`Album.sol`](broken-reference), this smart contract will use the [`RMRKNestableMultiAsset.sol`](https://github.com/rmrk-team/evm/blob/master/contracts/RMRK/nestable/RMRKNestableMultiAsset.sol) to gain access to the functionality of the `Nestable` and `MultiAsset` legos and `Ownable` for access control. They both need to be imported and set to be inherited by our smart contract:

```solidity
import "@rmrk-team/evm-contracts/contracts/RMRK/nestable/RMRKNestableMultiAsset.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract Song is RMRKNestableMultiAsset, Ownable {

}
```

To properly initialize the `RMRKNestableMultiAsset` smart contract, we need to pass the `name_` and `symbol_` parameters to the constructor. We will pass them, as constructor parameters:

```solidity
    constructor(
        string memory name_,
        string memory symbol_
    ) RMRKNestableMultiAsset(name_, symbol_) {}
```

#### Nest mint

We can now start implementing the functionality. We will start by implementing the `nestMint` function. The `nestMint` function will be used to mint the Song NFTs directly into the Album NFTs. It will accept the `to` parameter, which will be the address of the Album NFT into which to mint the Song NFTs. It will also acccept the `destinationId` which will be the ID of the destination token and the `amount` which will represent the number of Song NFTs to mint into the Album NFT.

As the internal `_nestMint` function, which we will be using, accepts the ID of the token to be minted, we will define the `totalSupply` variable, to keep track of the number of the existing Song NFTs. We will define its visibility as public, so that we are able to use the auto-generated getter to retrieve its value when interacting with the smart contract. The Song NFTs won't have maximum supply defined, as we can mint as many Song NFTs as we want into the Album NFTs (maybe we could release additional songs as part of the album later on):

```solidity
    uint256 public totalSupply;
```

When using `nestMint`, we have to make sure the destination is not `0x0` address, that the `destinationId` is not `0` and that the `amount` is greater than `0`. We will define custom errors for these checks below the import statements:

```solidity
error DestinationZeroAddress();
error DestinationIdZero();
error AmountZero();
```

With the errors defined, we can now implement the `nestMint` function:

```solidity
    function nestMint(address to, uint256 destinationId, uint256 amount) public onlyOwner {
        if ( to == address(0) ) revert DestinationZeroAddress();
        if ( destinationId == 0 ) revert DestinationIdZero();
        if ( amount == 0 ) revert AmountZero();

        uint256 nextTokenId = totalSupply + 1;
        unchecked {
            totalSupply += amount;
        }
        uint256 totalSupplyOffset = totalSupply + 1;

        for (uint256 i = nextTokenId; i < totalSupplyOffset; ){
            _nestMint(to, i, destinationId, "");
            unchecked {
                i++;
            }
        }
    }
```

#### Add asset entry

Just like the [`addAssetEntry`](broken-reference) of the `Album.sol`, the `addAssetEntry` of the `Song.sol` will be used to add the asset to the Song NFTs. As they have the same functionality, we can just copy-paste it from there (we will also need to add the `numberOfAssets` public variable):

```solidity
    uint64 public numberOfAssets;

    ...

    function addAssetEntry(string memory metadataURI) public onlyOwner {
        unchecked {
            numberOfAssets++;
        }
        _addAssetEntry(numberOfAssets, metadataURI);
    }
```

#### Add asset to tokens

Much like adding assets to Album NFTs, we will add the assets to the Song NFTs in a similar manner. We could slightly modify the `addAssetToTokens` function of the `Album.sol` to be able to add multiple assets at the same time. To do this we will modify the `assetId` parameter to be an array of asset IDs.

The `addAssetToTokens` function will look like this:

```solidity
    function addAssetToTokens(uint256[] memory tokenIds, uint64[] memory assetIds) public onlyOwner {
        for (uint256 i = 0; i < tokenIds.length; ) {
            for(uint256 j = 0; j < assetIds.length; ) {
                _addAssetToToken(tokenIds[i], assetIds[j], 0);

                if ( ownerOf(tokenIds[i]) == msg.sender ) {
                    uint256 assetIndex = getPendingAssets(tokenIds[i]).length - 1;
                    acceptAsset(tokenIds[i], assetIndex, assetIds[j]);
                }
                
                unchecked {
                    j++;
                }
            }

            unchecked {
                i++;
            }
        }
    }
```

#### Restricting transfers

As the songs are a part of the album and they shouldn't be transferable separately, we will restrict the transfers of the Song NFTs. For this we will use one of the [ERC-6454](https://eips.ethereum.org/EIPS/eip-6454) implementations that we provide. You can find the list in the [`Soulbound`](https://github.com/rmrk-team/evm/tree/master/contracts/RMRK/extension/soulbound) directory of our smart contracts.

The Song NFTs will be minted directly to the albums, so we will use the simplest implementation of the ERC-6454, the [`RMRKSoulbound.sol`](https://github.com/rmrk-team/evm/blob/master/contracts/RMRK/extension/soulbound/RMRKSoulbound.sol). This implementation makes the token non-transferable as soon as it is minted. We will import it and set it to be inherited by our smart contract:

```solidity
import "@rmrk-team/evm-contracts/contracts/RMRK/extension/soulbound/RMRKSoulbound.sol";

...

contract Song is RMRKNestableMultiAsset, RMRKSoulbound, Ownable {

...

```

Unfortunately inheriting `RMRKSoulbound` will require the `_beforeTokenTransfer` hook and `supportsInterface` to be overriden. We will override them as follows:

```solidity
    function _beforeTokenTransfer(
        address from,
        address to,
        uint256 tokenId
    ) internal override(RMRKCore, RMRKSoulbound) {
        RMRKSoulbound._beforeTokenTransfer(from, to, tokenId);
    }

    function supportsInterface(bytes4 interfaceId)
        public
        view
        override(RMRKSoulbound, RMRKNestableMultiAsset)
        returns (bool)
    {
        return
            RMRKSoulbound.supportsInterface(interfaceId) ||
            super.supportsInterface(interfaceId);
    }
```

<details>

<summary>Click to see the full code of the Song smart contract</summary>

```solidity
    // SPDX-License-Identifier: Apache-2.0
    pragma solidity ^0.8.18;

    import "@rmrk-team/evm-contracts/contracts/RMRK/nestable/RMRKNestableMultiAsset.sol";
    import "@rmrk-team/evm-contracts/contracts/RMRK/extension/soulbound/RMRKSoulbound.sol";
    import "@openzeppelin/contracts/access/Ownable.sol";

    error DestinationZeroAddress();
    error DestinationIdZero();
    error AmountZero();

    contract Song is RMRKNestableMultiAsset, RMRKSoulbound, Ownable {
        uint256 public totalSupply;
        uint64 public numberOfAssets;

        constructor(
            string memory name_,
            string memory symbol_
        ) RMRKNestableMultiAsset(name_, symbol_) {}

        function nestMint(
            address to,
            uint256 destinationId,
            uint256 amount
        ) public onlyOwner {
            if (to == address(0)) revert DestinationZeroAddress();
            if (destinationId == 0) revert DestinationIdZero();
            if (amount == 0) revert AmountZero();

            uint256 nextTokenId = totalSupply + 1;
            unchecked {
                totalSupply += amount;
            }
            uint256 totalSupplyOffset = totalSupply + 1;

            for (uint256 i = nextTokenId; i < totalSupplyOffset; ) {
                _nestMint(to, i, destinationId, "");
                unchecked {
                    i++;
                }
            }
        }

        function addAssetEntry(string memory metadataURI) public onlyOwner {
            unchecked {
                numberOfAssets++;
            }
            _addAssetEntry(numberOfAssets, metadataURI);
        }

        function addAssetToTokens(
            uint256[] memory tokenIds,
            uint64[] memory assetIds
        ) public onlyOwner {
            for (uint256 i = 0; i < tokenIds.length; ) {
                for (uint256 j = 0; j < assetIds.length; ) {
                    _addAssetToToken(tokenIds[i], assetIds[j], 0);

                    if (ownerOf(tokenIds[i]) == msg.sender) {
                        uint256 assetIndex = getPendingAssets(tokenIds[i]).length -
                            1;
                        acceptAsset(tokenIds[i], assetIndex, assetIds[j]);
                    }
                    
                    unchecked {
                        j++;
                    }
                }

                unchecked {
                    i++;
                }
            }
        }

        function _beforeTokenTransfer(
            address from,
            address to,
            uint256 tokenId
        ) internal override(RMRKCore, RMRKSoulbound) {
            RMRKSoulbound._beforeTokenTransfer(from, to, tokenId);
        }

        function supportsInterface(
            bytes4 interfaceId
        )
            public
            view
            override(RMRKSoulbound, RMRKNestableMultiAsset)
            returns (bool)
        {
            return
                RMRKSoulbound.supportsInterface(interfaceId) ||
                super.supportsInterface(interfaceId);
        }
    }
```

</details>

This concludes the implementation of the Song NFT smart contract. We can now use the `prettier` and `typechain` sctipts to format the code and generate the typechain bindings. We will also need to compile the smart contracts, so we will run the following commands:

```bash
yarn prettier && yarn hardhat compile --network zkSyncTestnet && yarn typechain
```

## Deploying the smart contracts

As the smart contracts are ready, we can write the deployment script. We will create a new file in the `deploy` directory called `deploy.ts`.

We will import `delay` from `hardhat-etherscan`, `Deployer` from `hardhat-zksync-deploy`, `HardhatRuntimeEnvironment` from `hardhat/types`, `run` from `hardhat`, `Album` and `Song` from `typechain-types`, `Wallet` and `utils` from `zksync-web3` and `ethers` from `ethers`. Additionally we will add the skeleton of the deployment function:

```typescript
import { delay } from '@nomiclabs/hardhat-etherscan/dist/src/etherscan/EtherscanService';
import { Deployer } from '@matterlabs/hardhat-zksync-deploy';
import { HardhatRuntimeEnvironment } from 'hardhat/types';
import { run } from 'hardhat';
import { Album, Song } from '../typechain-types';
import { Wallet, utils } from 'zksync-web3';
import * as ethers from 'ethers';

export default async function (hre: HardhatRuntimeEnvironment) {
    
}
```

The deploy script will be comprised of three distinct sections:

1. Deploying the Album NFT smart contract
2. Deploying the Song NFT smart contract
3. Verifying the smart contracts in the chain explorer

### Deploying the Album NFT smart contract

We will start by deploying the Album NFT smart contract. In order to be able to track the progress of the deployment, we will add a `console.log` statement. The private key stored in the `PRIVATE_KEY` environment variable will be used to generate the `wallet`, which will in turn be used to generate the `deployer`.

```typescript
  console.log('Deploying Album smart contract');

  const wallet = new Wallet(process.env.PRIVATE_KEY || '');

  const deployer = new Deployer(hre, wallet);
```

In order to be able to deploy the smart contract, we will need to get the `Album` artifact and prepare the arguments to be passed to the constructor. The deployment arguments will be stored in a variable, so that we can reuse it when verifying the smart contract. Additionally, we will estimate the deployment fee. This will allow us to deposit the funds to L2 within the script:

```typescript
  const albumArtifact = await deployer.loadArtifact('Album');

  const albumArgs = ['Album', 'ALB', 10_000];

  const albumDeploymentFee = await deployer.estimateDeployFee(albumArtifact, albumArgs);
```

Now we can add the L2 deposit logic, which allows us to automatically deposit funds required for deployment from L1 to L2 during the execution of the script. Here we will use the `albumDeploymentFee` that we calculated in the previous step. It is worth noting, that the `wallet` needs to have sufficient balance to make a deposit. Once the deposit is made, we have to make sure that it has been recorded in the L2 chain, before continuing the deployment script:

```typescript
  const albumDepositHandle = await deployer.zkWallet.deposit({
    to: deployer.zkWallet.address,
    token: utils.ETH_ADDRESS,
    amount: albumDeploymentFee,
  });

  await albumDepositHandle.wait();
```

We can now log the album deployment fee to the console.;

```typescript
  const parsedAlbumFee = ethers.utils.formatEther(albumDeploymentFee.toString());
  console.log(`The deployment is estimated to cost ${parsedAlbumFee} ETH`);
```

Everything is now ready to deploy the Album NFT smart contract:

```typescript
 const album = <Album>await deployer.deploy(albumArtifact, albumArgs);

 await album.deployed();
 console.log(`Album smart contract deployed to ${album.address}.`);
```

### Deploying the Song NFT smart contract

With the Album NFT smart contract deployed, we can now deploy the Song NFT smart contract. As the process of deploying the Song NFT smart contract just slightly differs from the process of deploying the Album NFT smart contract, we can just reuse the code from the previous steps, modifying the deployment arguments to be in line with what Song NFT smart contract requires:

```typescript
 console.log('Deploying Song smart contract');

 const songArtifact = await deployer.loadArtifact('Song');

 const songArgs = ['Song', 'SNG'];

 const songDeploymentFee = await deployer.estimateDeployFee(songArtifact, songArgs);

 const songDepositHandle = await deployer.zkWallet.deposit({
   to: deployer.zkWallet.address,
   token: utils.ETH_ADDRESS,
   amount: albumDeploymentFee,
 });

 await songDepositHandle.wait();

 const parsedSongFee = ethers.utils.formatEther(songDeploymentFee.toString());
 console.log(`The deployment is estimated to cost ${parsedSongFee} ETH`);

 const song = <Song>await deployer.deploy(songArtifact, songArgs);

 await song.deployed();
 console.log(`Song smart contract deployed to ${song.address}.`); 
```

### Verifying the smart contracts in the chain explorer

All that remains after the smart contracts have been deployed is to verify them in the chain explorer. Before initiating the verification, we will add a delay of 20 seconds, to make sure the chain explorer is ready for the verification. We will use the `verify` task from `hardhat-etherscan` to do so. We will pass the address, constructor argument and smart contract for each of the smart contracts to the task:

```typescript
  await delay(20000);
  console.log('Verifying smart contracts');

  await run(`verify:verify`, {
    address: album.address,
    constructorArguments: albumArgs,
    contract: 'contracts/Album.sol:Album',
  });

  await run(`verify:verify`, {
    address: song.address,
    constructorArguments: songArgs,
    contract: 'contracts/Song.sol:Song',
  });
```

{% hint style="info" %}
**NOTE: If you encounter an error reporting no network found when running the deployment script, add and set the `GOERLI_URL` environment variable.**
{% endhint %}

<details>

<summary>Expand this section for the full deployment script</summary>

```typescript
    import { delay } from '@nomiclabs/hardhat-etherscan/dist/src/etherscan/EtherscanService';
    import { Deployer } from '@matterlabs/hardhat-zksync-deploy';
    import { HardhatRuntimeEnvironment } from 'hardhat/types';
    import { run } from 'hardhat';
    import { Album, Song } from '../typechain-types';
    import { Wallet, utils } from 'zksync-web3';
    import * as ethers from 'ethers';

    export default async function (hre: HardhatRuntimeEnvironment) {
        console.log('Deploying Album smart contract');

        const wallet = new Wallet(process.env.PRIVATE_KEY || '');

        // Create deployer object and load the artifact of the contract you want to deploy.
        const deployer = new Deployer(hre, wallet);
        const albumArtifact = await deployer.loadArtifact('Album');

        const albumArgs = ['Album', 'ALB', 10_000];

        // Estimate contract deployment fee
        const albumDeploymentFee = await deployer.estimateDeployFee(albumArtifact, albumArgs);

        // OPTIONAL: Deposit funds to L2
        // Comment this block if you already have funds on zkSync.
        const albumDepositHandle = await deployer.zkWallet.deposit({
            to: deployer.zkWallet.address,
            token: utils.ETH_ADDRESS,
            amount: albumDeploymentFee,
        });
        // Wait until the deposit is processed on zkSync
        await albumDepositHandle.wait();

        // Deploy this contract. The returned object will be of a `Contract` type, similarly to ones in `ethers`.
        const parsedAlbumFee = ethers.utils.formatEther(albumDeploymentFee.toString());
        console.log(`The deployment is estimated to cost ${parsedAlbumFee} ETH`);

        const album = <Album>await deployer.deploy(albumArtifact, albumArgs);

        await album.deployed();
        console.log(`Album smart contract deployed to ${album.address}.`);

        console.log('Deploying Song smart contract');

        const songArtifact = await deployer.loadArtifact('Song');

        const songArgs = ['Song', 'SNG'];

        const songDeploymentFee = await deployer.estimateDeployFee(songArtifact, songArgs);

        const songDepositHandle = await deployer.zkWallet.deposit({
            to: deployer.zkWallet.address,
            token: utils.ETH_ADDRESS,
            amount: albumDeploymentFee,
        });
        // Wait until the deposit is processed on zkSync
        await songDepositHandle.wait();

        const parsedSongFee = ethers.utils.formatEther(songDeploymentFee.toString());
        console.log(`The deployment is estimated to cost ${parsedSongFee} ETH`);

        const song = <Song>await deployer.deploy(songArtifact, songArgs);

        await song.deployed();
        console.log(`Song smart contract deployed to ${song.address}.`); 

        await delay(20000);
        console.log('Verifying smart contracts');

        await run(`verify:verify`, {
            address: album.address,
            constructorArguments: albumArgs,
            contract: 'contracts/Album.sol:Album',
        });

        await run(`verify:verify`, {
            address: song.address,
            constructorArguments: songArgs,
            contract: 'contracts/Song.sol:Song',
        });
    }
```

</details>

With the deploy script ready, we can now run it:

```bash
yarn hardhat deploy-zksync --network zkSyncTestnet
```

## User journey

In order to better observe the interaction and the operation of RMRK-powered smart contracts, we will create a simple user journey. The user journey will be comprised of the following steps:

1. Deploying the Album and Song NFT smart contracts
2. Minting Album NFTs
3. Adding asset entries for the Album NFTs
4. Adding assets to the Album NFTs
5. Minting Song NFTs into the Album NFTs
6. Adding asset entries for the Song NFTs
7. Adding assets to the Song NFTs

As running the script would be wasteful in a public network, the script will be designed to be run in the Hardhat's emulated network. The user journey script will reside in the `scripts` directory and will be named `user-journey.ts`.

The empty skeleton of the script will look as follows:

```typescript
async function main () {

}

main()
    .then(() => process.exit(0))
    .catch(error => {
        console.error(error);
        process.exit(1);
    });
```

### Deploying the Album and Song NFT smart contracts

We will start by deploying the Album and Song NFT smart contracts. In order to be able to track the progress of the deployment, we will add a `console.log` statement. Prior to deploying the smart contract, we will also generate the signers that will be used to deploy the smart contracts, and interact with them.

In order to be able to use `ethers`, we will need to import it:

```typescript
import { ethers } from 'ethers';
```

Getting the signers and deploying the smart contracts should look like this:

```typescript
    console.log('Getting signers');

    const [owner, user] = await ethers.getSigners();

    console.log(`Owner: ${owner.address}`);
    console.log(`User: ${user.address}`);

    console.log('Deploying the smart contracts')

    const Album = await ethers.getContractFactory('Album');
    const Song = await ethers.getContractFactory('Song');

    const album = await Album.deploy('Album', 'ALB', 10_000);
    await album.deployed();
    
    const song = await Song.deploy('Song', 'SNG');
    await song.deployed();

    console.log(`Album smart contract deployed to ${album.address}.`);
    console.log(`Song smart contract deployed to ${song.address}.`);
```

### Minting Album NFTs

Album NFTs will be minted to both, the `owner` and the `user`. This will allow us to compare the behavior of the smart contracts when the `owner` and the `user` are interacting with them.

In order to mint the Album NFTs, we will use the `mint` function of the Album NFT smart contract. We will mint 2 Album NFTs to the `owner` and 1 Album NFT to the `user`. We will also add a `console.log` statement to track the progress of the minting.

```typescript
    console.log('Minting Album NFTs');

    await album.mint(owner.address, 2);
    await album.mint(user.address, 1);

    console.log(`Album balance of owner: ${await album.balanceOf(owner.address)}`);
    console.log(`Album balance of user: ${await album.balanceOf(user.address)}`);
```

### Adding asset entries for the Album NFTs

We will add asset entries for the Album NFTs. One entry will represent the album artwork and the other will contain the album metadata. We will use the `addAssetEntry` function of the Album NFT smart contract:

```typescript
    console.log('Adding asset entries to the Album smart contract');

    await album.addAssetEntry('ipfs://artwork');
    await album.addAssetEntry('ipfs://metadata');
```

### Adding assets to the Album NFTs

Once the asset entries are added, we can add assets to the Album NFTs. We will use the `addAssetToTokens` function of the Album NFT smart contract. We will add both assets to all of the albums:

```typescript
    console.log('Adding asset entries to the Album smart contract');

    await album.addAssetEntry('ipfs://artwork');
    await album.addAssetEntry('ipfs://metadata');

    console.log('Adding assets to the Album NFTs');

    await album.addAssetToTokens([1, 2, 3], 1);
    await album.addAssetToTokens([1, 2, 3], 2);

    console.log(`Active assets of Album NFT 1: ${(await album.getActiveAssets(1)).length}`);
    console.log(`Pending assets of Album NFT 1: ${(await album.getPendingAssets(1)).length}`);
    console.log(`Active assets of Album NFT 2: ${(await album.getActiveAssets(2)).length}`);
    console.log(`Pending assets of Album NFT 2: ${(await album.getPendingAssets(2)).length}`);
    console.log(`Active assets of Album NFT 3: ${(await album.getActiveAssets(3)).length}`);
    console.log(`Pending assets of Album NFT 3: ${(await album.getPendingAssets(3)).length}`);
```

You might have noticed, that the assets are added to the active assets of the tokens with IDs of `1` and `2`. This is because the token are owned by the caller. The token with ID `3` is owned by the `user` and the assets are added to the pending assets of the token. For the assets of the token with ID `3` to be added to the active assets, the `user` will need to call the `acceptAsset` function of the Album NFT smart contract.

{% hint style="info" %}
**NOTE: When an asset is accepted, the asset with the greatest index is moved to its slot. This means that if there are two assets in the pending array and the asset with index of `0` is accepted, the asset with the highest index (in our case the asset with the index of `1`) is moved into its place.**
{% endhint %}

Accepting the assets of the token with ID `3` should look like this:

```typescript
    console.log('Accepting assets for Album NFT 3');

    await album.connect(user).acceptAsset(3, 0, 1);
    await album.connect(user).acceptAsset(3, 0, 2);

    console.log(`Active assets of Album NFT 3: ${(await album.getActiveAssets(3)).length}`);
    console.log(`Pending assets of Album NFT 3: ${(await album.getPendingAssets(3)).length}`);
```

### Minting Song NFTs into the Album NFTs

Song NFTs will be minted directly into the Album NFTs. Each Album will contain 3 Song NFTs. We will use the `nestMint` function of the Song NFT smart contract. The destination of the nest minting should be parent token's smart contract address (in our case this is the Album smart contract). The destination ID will be the ID of each Album NFT that we will be minting the Song NFTs into:

```typescript
    console.log('Minting Song NFTs into Album NFTs');

    await song.nestMint(album.address, 1, 3);
    await song.nestMint(album.address, 2, 3);
    await song.nestMint(album.address, 3, 3);

    console.log(`Active child tokens of Album NFT 1: ${(await album.childrenOf(1)).length}`);
    console.log(`Pending child tokens of Album NFT 1: ${(await album.pendingChildrenOf(1)).length}`);
    console.log(`Active child tokens of Album NFT 2: ${(await album.childrenOf(2)).length}`);
    console.log(`Pending child tokens of Album NFT 2: ${(await album.pendingChildrenOf(2)).length}`);
    console.log(`Active child tokens of Album NFT 3: ${(await album.childrenOf(3)).length}`);
    console.log(`Pending child tokens of Album NFT 3: ${(await album.pendingChildrenOf(3)).length}`);
```

Since the parent token has to accept the child tokens, we have to use the `acceptChild` function that the Album smart contract inherits from the `RMRKNestable`. In addition to the token ID of the parent token accepting the child token and the index of the child token in the pending array, it also requires the address of the token smart contract and the ID of the child token. The latter two are required, so that the child that is accepted is the one we are expecing. This is done in case the parent token's pending child array is modified by another transaction:

```typescript
    console.log('Accepting child tokens for Album NFTs');

    await album.acceptChild(1, 0, song.address, 1);
    await album.acceptChild(1, 0, song.address, 3);
    await album.acceptChild(1, 0, song.address, 2);
    await album.acceptChild(2, 0, song.address, 4);
    await album.acceptChild(2, 0, song.address, 6);
    await album.acceptChild(2, 0, song.address, 5);
    await album.connect(user).acceptChild(3, 0, song.address, 7);
    await album.connect(user).acceptChild(3, 0, song.address, 9);
    await album.connect(user).acceptChild(3, 0, song.address, 8);

    console.log(`Active child tokens of Album NFT 1: ${(await album.childrenOf(1)).length}`);
    console.log(`Pending child tokens of Album NFT 1: ${(await album.pendingChildrenOf(1)).length}`);
    console.log(`Active child tokens of Album NFT 2: ${(await album.childrenOf(2)).length}`);
    console.log(`Pending child tokens of Album NFT 2: ${(await album.pendingChildrenOf(2)).length}`);
    console.log(`Active child tokens of Album NFT 3: ${(await album.childrenOf(3)).length}`);
    console.log(`Pending child tokens of Album NFT 3: ${(await album.pendingChildrenOf(3)).length}`);
```

### Adding asset entries for the Song NFTs

There will be 3 asset entries for each Song NFT. The first one will be the audio file, second one metadata, containing the title, artist, author, etc., and the last one will be the lyrics. Since we have 3 songs per album, this means that we will have to add a total of 9 asset entries:

```typescript
    console.log('Adding asset entries to the Song smart contract');

    await song.addAssetEntry('ipfs://audio1');
    await song.addAssetEntry('ipfs://metadata1');
    await song.addAssetEntry('ipfs://lyrics1');
    await song.addAssetEntry('ipfs://audio2');
    await song.addAssetEntry('ipfs://metadata2');
    await song.addAssetEntry('ipfs://lyrics2');
    await song.addAssetEntry('ipfs://audio3');
    await song.addAssetEntry('ipfs://metadata3');
    await song.addAssetEntry('ipfs://lyrics3');
```

### Adding assets to the Song NFTs

As previously mentioned, each Song NFT will have 3 assets. We will use a similar approach as we did with the Album NFTs; the assets will be added using the `addAssetToTokens`. The difference is that we will be adding the assets to the NFTs in batches (using the arrays for both the token to receive the assets as well as for the assets):

```typescript
    console.log('Adding assets to the Song NFTs');

    await song.addAssetToTokens([1, 4, 7], [1, 2, 3]);
    await song.addAssetToTokens([2, 5, 8], [4, 5, 6]);
    await song.addAssetToTokens([3, 6, 9], [7, 8, 9]);

    console.log(`Active assets of Song NFT 1: ${(await song.getActiveAssets(1)).length}`);
    console.log(`Pending assets of Song NFT 1: ${(await song.getPendingAssets(1)).length}`);
    console.log(`Active assets of Song NFT 4: ${(await song.getActiveAssets(4)).length}`);
    console.log(`Pending assets of Song NFT 4: ${(await song.getPendingAssets(4)).length}`);
    console.log(`Active assets of Song NFT 7: ${(await song.getActiveAssets(7)).length}`);
    console.log(`Pending assets of Song NFT 7: ${(await song.getPendingAssets(7)).length}`);
```

Similarly to the Album NFTs, we will have to accept the assets for the Song NFTs that belong to the Album NFT not owned by the `owner`. This is done using the `acceptAsset` function of the Song smart contract:

```typescript
     console.log('Accepting assets for the Song NFTs not belonging to the owner');

    await song.connect(user).acceptAsset(7, 0, 1);
    await song.connect(user).acceptAsset(7, 0, 3);
    await song.connect(user).acceptAsset(7, 0, 2);
    await song.connect(user).acceptAsset(8, 0, 4);
    await song.connect(user).acceptAsset(8, 0, 6);
    await song.connect(user).acceptAsset(8, 0, 5);
    await song.connect(user).acceptAsset(9, 0, 7);
    await song.connect(user).acceptAsset(9, 0, 9);
    await song.connect(user).acceptAsset(9, 0, 8);

    console.log(`Active assets of Song NFT 1: ${(await song.getActiveAssets(1)).length}`);
    console.log(`Pending assets of Song NFT 1: ${(await song.getPendingAssets(1)).length}`);
    console.log(`Active assets of Song NFT 4: ${(await song.getActiveAssets(4)).length}`);
    console.log(`Pending assets of Song NFT 4: ${(await song.getPendingAssets(4)).length}`);
    console.log(`Active assets of Song NFT 7: ${(await song.getActiveAssets(7)).length}`);
    console.log(`Pending assets of Song NFT 7: ${(await song.getPendingAssets(7)).length}`);
```

With this, the album by _**The RMRKables**_ is ready to be distributed.

### Observing the child-parent relationship

As the tokens are properly nested now with the assets accepted, we can observe the child-parent relationship between the Album NFTs and the Song NFTs. This can be done using the `childrenOf`, `directOwnerOf` and `ownerOf` functions of the Album smart contract:

```typescript
    console.log('Observing the child-parent relationship');

    console.log(`Children of Album NFT 1: ${await album.childrenOf(1)}`);
    console.log(`Children of Album NFT 2: ${await album.childrenOf(2)}`);
    console.log(`Children of Album NFT 3: ${await album.childrenOf(3)}`);
    console.log(`Parent of Album NFT 1: ${await album.directOwnerOf(1)}`);
    console.log(`Parent of Song NFT 1: ${await song.directOwnerOf(1)}`);
    console.log(`Parent of Song NFT 4: ${await song.directOwnerOf(4)}`);
    console.log(`Parent of Song NFT 7: ${await song.directOwnerOf(7)}`);
    console.log(`Owner of Song NFT 1: ${await song.ownerOf(1)}`);
    console.log(`Owner of Song NFT 4: ${await song.ownerOf(4)}`);
    console.log(`Owner of Song NFT 7: ${await song.ownerOf(7)}`);
```

The `childrenOf` function returns the array of active tokens that contains the token ID and the smart contract address for of the token.

The `directOwnerOf` function returns the token ID and the smart contract address of the direct owner of the parent token, as well as a boolean value indicating whether the direct owner of the token is an NFT or not. In case the direct owner is not an NFT, the token ID is `0`.

The `ownerOf` function returns the address of the root owner of the token. This means that it returns the address of the first non-token owner in the parent-token chain.

{% hint style="info" %}
**NOTE: It is worth noting that a child token can also be a parent token to another token.**
{% endhint %}

<details>

<summary>Expand this section for the full user journey script</summary>

```typescript
    import { ethers } from 'hardhat';
    
    async function main () {
        console.log('Getting signers');

        const [owner, user] = await ethers.getSigners();

        console.log(`Owner: ${owner.address}`);
        console.log(`User: ${user.address}`);

        console.log('Deploying the smart contracts')

        const Album = await ethers.getContractFactory('Album');
        const Song = await ethers.getContractFactory('Song');

        const album = await Album.deploy('Album', 'ALB', 10_000);
        await album.deployed();
        
        const song = await Song.deploy('Song', 'SNG');
        await song.deployed();

        console.log(`Album smart contract deployed to ${album.address}.`);
        console.log(`Song smart contract deployed to ${song.address}.`);

        console.log('Minting Album NFTs');

        await album.mint(owner.address, 2);
        await album.mint(user.address, 1);

        console.log(`Album balance of owner: ${await album.balanceOf(owner.address)}`);
        console.log(`Album balance of user: ${await album.balanceOf(user.address)}`);

        console.log('Adding asset entries to the Album smart contract');

        await album.addAssetEntry('ipfs://artwork');
        await album.addAssetEntry('ipfs://metadata');

        console.log('Adding assets to the Album NFTs');

        await album.addAssetToTokens([1, 2, 3], 1);
        await album.addAssetToTokens([1, 2, 3], 2);

        console.log(`Active assets of Album NFT 1: ${(await album.getActiveAssets(1)).length}`);
        console.log(`Pending assets of Album NFT 1: ${(await album.getPendingAssets(1)).length}`);
        console.log(`Active assets of Album NFT 2: ${(await album.getActiveAssets(2)).length}`);
        console.log(`Pending assets of Album NFT 2: ${(await album.getPendingAssets(2)).length}`);
        console.log(`Active assets of Album NFT 3: ${(await album.getActiveAssets(3)).length}`);
        console.log(`Pending assets of Album NFT 3: ${(await album.getPendingAssets(3)).length}`);

        console.log('Accepting assets for Album NFT 3');

        await album.connect(user).acceptAsset(3, 0, 1);
        await album.connect(user).acceptAsset(3, 0, 2);

        console.log(`Active assets of Album NFT 3: ${(await album.getActiveAssets(3)).length}`);
        console.log(`Pending assets of Album NFT 3: ${(await album.getPendingAssets(3)).length}`);

        console.log('Minting Song NFTs into Album NFTs');

        await song.nestMint(album.address, 1, 3);
        await song.nestMint(album.address, 2, 3);
        await song.nestMint(album.address, 3, 3);

        console.log(`Active child tokens of Album NFT 1: ${(await album.childrenOf(1)).length}`);
        console.log(`Pending child tokens of Album NFT 1: ${(await album.pendingChildrenOf(1)).length}`);
        console.log(`Active child tokens of Album NFT 2: ${(await album.childrenOf(2)).length}`);
        console.log(`Pending child tokens of Album NFT 2: ${(await album.pendingChildrenOf(2)).length}`);
        console.log(`Active child tokens of Album NFT 3: ${(await album.childrenOf(3)).length}`);
        console.log(`Pending child tokens of Album NFT 3: ${(await album.pendingChildrenOf(3)).length}`);

        console.log('Accepting child tokens for Album NFTs');

        await album.acceptChild(1, 0, song.address, 1); // (tokenId, index, childContract, childTokenId)
        await album.acceptChild(1, 0, song.address, 3);
        await album.acceptChild(1, 0, song.address, 2);
        await album.acceptChild(2, 0, song.address, 4);
        await album.acceptChild(2, 0, song.address, 6);
        await album.acceptChild(2, 0, song.address, 5);
        await album.connect(user).acceptChild(3, 0, song.address, 7);
        await album.connect(user).acceptChild(3, 0, song.address, 9);
        await album.connect(user).acceptChild(3, 0, song.address, 8);

        console.log(`Active child tokens of Album NFT 1: ${(await album.childrenOf(1)).length}`);
        console.log(`Pending child tokens of Album NFT 1: ${(await album.pendingChildrenOf(1)).length}`);
        console.log(`Active child tokens of Album NFT 2: ${(await album.childrenOf(2)).length}`);
        console.log(`Pending child tokens of Album NFT 2: ${(await album.pendingChildrenOf(2)).length}`);
        console.log(`Active child tokens of Album NFT 3: ${(await album.childrenOf(3)).length}`);
        console.log(`Pending child tokens of Album NFT 3: ${(await album.pendingChildrenOf(3)).length}`);

        console.log('Adding asset entries to the Song smart contract');

        await song.addAssetEntry('ipfs://audio1');
        await song.addAssetEntry('ipfs://metadata1');
        await song.addAssetEntry('ipfs://lyrics1');
        await song.addAssetEntry('ipfs://audio2');
        await song.addAssetEntry('ipfs://metadata2');
        await song.addAssetEntry('ipfs://lyrics2');
        await song.addAssetEntry('ipfs://audio3');
        await song.addAssetEntry('ipfs://metadata3');
        await song.addAssetEntry('ipfs://lyrics3');

        console.log('Adding assets to the Song NFTs');

        await song.addAssetToTokens([1, 4, 7], [1, 2, 3]);
        await song.addAssetToTokens([2, 5, 8], [4, 5, 6]);
        await song.addAssetToTokens([3, 6, 9], [7, 8, 9]);

        console.log(`Active assets of Song NFT 1: ${(await song.getActiveAssets(1)).length}`);
        console.log(`Pending assets of Song NFT 1: ${(await song.getPendingAssets(1)).length}`);
        console.log(`Active assets of Song NFT 4: ${(await song.getActiveAssets(4)).length}`);
        console.log(`Pending assets of Song NFT 4: ${(await song.getPendingAssets(4)).length}`);
        console.log(`Active assets of Song NFT 7: ${(await song.getActiveAssets(7)).length}`);
        console.log(`Pending assets of Song NFT 7: ${(await song.getPendingAssets(7)).length}`);

        console.log('Accepting assets for the Song NFTs not belonging to the owner');

        await song.connect(user).acceptAsset(7, 0, 1);
        await song.connect(user).acceptAsset(7, 0, 3);
        await song.connect(user).acceptAsset(7, 0, 2);
        await song.connect(user).acceptAsset(8, 0, 4);
        await song.connect(user).acceptAsset(8, 0, 6);
        await song.connect(user).acceptAsset(8, 0, 5);
        await song.connect(user).acceptAsset(9, 0, 7);
        await song.connect(user).acceptAsset(9, 0, 9);
        await song.connect(user).acceptAsset(9, 0, 8);

        console.log(`Active assets of Song NFT 1: ${(await song.getActiveAssets(1)).length}`);
        console.log(`Pending assets of Song NFT 1: ${(await song.getPendingAssets(1)).length}`);
        console.log(`Active assets of Song NFT 4: ${(await song.getActiveAssets(4)).length}`);
        console.log(`Pending assets of Song NFT 4: ${(await song.getPendingAssets(4)).length}`);
        console.log(`Active assets of Song NFT 7: ${(await song.getActiveAssets(7)).length}`);
        console.log(`Pending assets of Song NFT 7: ${(await song.getPendingAssets(7)).length}`);

        console.log('Observing the child-parent relationship');

        console.log(`Children of Album NFT 1: ${await album.childrenOf(1)}`);
        console.log(`Children of Album NFT 2: ${await album.childrenOf(2)}`);
        console.log(`Children of Album NFT 3: ${await album.childrenOf(3)}`);
        console.log(`Parent of Album NFT 1: ${await album.directOwnerOf(1)}`);
        console.log(`Parent of Song NFT 1: ${await song.directOwnerOf(1)}`);
        console.log(`Parent of Song NFT 4: ${await song.directOwnerOf(4)}`);
        console.log(`Parent of Song NFT 7: ${await song.directOwnerOf(7)}`);
        console.log(`Owner of Song NFT 1: ${await song.ownerOf(1)}`);
        console.log(`Owner of Song NFT 4: ${await song.ownerOf(4)}`);
        console.log(`Owner of Song NFT 7: ${await song.ownerOf(7)}`);
    }

    main()
        .then(() => process.exit(0))
        .catch(error => {
            console.error(error);
            process.exit(1);
        });
```

</details>

### Running the user journey script

Having completed the user journey script, we can now run it and observe the results:

```bash
yarn hardhat run scripts/userJourney.ts
yarn run v1.22.19

Getting signers
Owner: 0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266
User: 0x70997970C51812dc3A010C7d01b50e0d17dc79C8
Deploying the smart contracts
Album smart contract deployed to 0x5FbDB2315678afecb367f032d93F642f64180aa3.
Song smart contract deployed to 0xe7f1725E7734CE288F8367e1Bb143E90bb3F0512.
Minting Album NFTs
Album balance of owner: 2
Album balance of user: 1
Adding asset entries to the Album smart contract
Adding assets to the Album NFTs
Active assets of Album NFT 1: 2
Pending assets of Album NFT 1: 0
Active assets of Album NFT 2: 2
Pending assets of Album NFT 2: 0
Active assets of Album NFT 3: 0
Pending assets of Album NFT 3: 2
Accepting assets for Album NFT 3
Active assets of Album NFT 3: 2
Pending assets of Album NFT 3: 0
Minting Song NFTs into Album NFTs
Active child tokens of Album NFT 1: 0
Pending child tokens of Album NFT 1: 3
Active child tokens of Album NFT 2: 0
Pending child tokens of Album NFT 2: 3
Active child tokens of Album NFT 3: 0
Pending child tokens of Album NFT 3: 3
Accepting child tokens for Album NFTs
Active child tokens of Album NFT 1: 3
Pending child tokens of Album NFT 1: 0
Active child tokens of Album NFT 2: 3
Pending child tokens of Album NFT 2: 0
Active child tokens of Album NFT 3: 3
Pending child tokens of Album NFT 3: 0
Adding asset entries to the Song smart contract
Adding assets to the Song NFTs
Active assets of Song NFT 1: 3
Pending assets of Song NFT 1: 0
Active assets of Song NFT 4: 3
Pending assets of Song NFT 4: 0
Active assets of Song NFT 7: 0
Pending assets of Song NFT 7: 3
Accepting assets for the Song NFTs not belonging to the owner
Active assets of Song NFT 1: 3
Pending assets of Song NFT 1: 0
Active assets of Song NFT 4: 3
Pending assets of Song NFT 4: 0
Active assets of Song NFT 7: 3
Pending assets of Song NFT 7: 0
Observing the child-parent relationship
Children of Album NFT 1: 1,0xe7f1725E7734CE288F8367e1Bb143E90bb3F0512,3,0xe7f1725E7734CE288F8367e1Bb143E90bb3F0512,2,0xe7f1725E7734CE288F8367e1Bb143E90bb3F0512
Children of Album NFT 2: 4,0xe7f1725E7734CE288F8367e1Bb143E90bb3F0512,6,0xe7f1725E7734CE288F8367e1Bb143E90bb3F0512,5,0xe7f1725E7734CE288F8367e1Bb143E90bb3F0512
Children of Album NFT 3: 7,0xe7f1725E7734CE288F8367e1Bb143E90bb3F0512,9,0xe7f1725E7734CE288F8367e1Bb143E90bb3F0512,8,0xe7f1725E7734CE288F8367e1Bb143E90bb3F0512
Parent of Album NFT 1: 0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266,0,false
Parent of Song NFT 1: 0x5FbDB2315678afecb367f032d93F642f64180aa3,1,true
Parent of Song NFT 4: 0x5FbDB2315678afecb367f032d93F642f64180aa3,2,true
Parent of Song NFT 7: 0x5FbDB2315678afecb367f032d93F642f64180aa3,3,true
Owner of Song NFT 1: 0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266
Owner of Song NFT 4: 0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266
Owner of Song NFT 7: 0x70997970C51812dc3A010C7d01b50e0d17dc79C8
✨  Done in 2.62s.
```

## Conclusion

We observed rudimentary operation of the next generation of NFT smart contracts provided by RMRK. You are invited to explore the RMRK ecosystem further and to build your own NFT smart contracts. The best place to start is the [RMRK documentation](https://docs.rmrk.app/).

We encourage you to explore our Equippable legos as well as our extensions as well.

Have a RMRKable day!

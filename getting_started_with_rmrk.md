# Getting Started with RMRK

RMRK (pronounced "remark") is a set of NFT standards that bring advanced functionality to NFTs, including equippable assets and nestable tokens. This guide will walk you through the basics of interacting with RMRK-based NFTs using the provided smart contracts.

## Table of Contents

1. [Understanding RMRK Contracts](#understanding-rmrk-contracts)
2. [Minting RMRK NFTs](#minting-rmrk-nfts)
3. [Nested Minting](#nested-minting)
4. [Equipping Assets](#equipping-assets)
5. [Working with Different Payment Options](#working-with-different-payment-options)

## Understanding RMRK Contracts

RMRK provides several implementation contracts for different use cases. The main contracts we'll focus on are:

- `RMRKEquippableLazyMintErc20`: Allows minting with ERC20 tokens
- `RMRKEquippableLazyMintNative`: Allows minting with native cryptocurrency
- `RMRKEquippablePreMint`: Allows pre-minting of tokens by the contract owner or contributors

These contracts all inherit from `RMRKAbstractEquippable`, which provides the core RMRK functionality.

## Minting RMRK NFTs

To mint RMRK NFTs, you'll need to interact with one of the implementation contracts. Here's an example of how to mint using the `RMRKEquippableLazyMintNative` contract:

```solidity
function mint(address to, uint256 numToMint) public payable virtual returns (uint256)
```

This function mints the specified number of tokens to the given address. Here's how you might use it:

```javascript
const contract = await ethers.getContractAt("RMRKEquippableLazyMintNative", contractAddress);
const price = await contract.pricePerMint();
const numToMint = 1;

const tx = await contract.mint(recipientAddress, numToMint, { value: price.mul(numToMint) });
await tx.wait();
```

## Nested Minting

One of RMRK's unique features is the ability to mint tokens directly into other tokens. This is done using the `nestMint` function:

```solidity
function nestMint(address to, uint256 numToMint, uint256 destinationId) public payable virtual returns (uint256)
```

Here's an example of how you might use it:

```javascript
const parentTokenId = 1; // The ID of the token you want to mint into
const numToMint = 1;

const tx = await contract.nestMint(contractAddress, numToMint, parentTokenId, { value: price.mul(numToMint) });
await tx.wait();
```

## Equipping Assets

RMRK NFTs can have equippable assets. While the equipping logic itself is not shown in the provided contract snippets, the contracts inherit from `RMRKAbstractEquippable`, which provides this functionality. You would typically interact with these functions to manage equippables:

- `equip(uint64 parentId, uint64 assetId, uint64 slotId, uint64 childId)`
- `unequip(uint64 parentId, uint64 assetId, uint64 slotId)`

## Working with Different Payment Options

RMRK supports different payment options for minting:

### ERC20 Payments

If you're using the `RMRKEquippableLazyMintErc20` contract, you'll need to approve the contract to spend your ERC20 tokens before minting:

```javascript
const erc20Contract = await ethers.getContractAt("IERC20", erc20TokenAddress);
await erc20Contract.approve(rmrkContractAddress, pricePerMint.mul(numToMint));

const rmrkContract = await ethers.getContractAt("RMRKEquippableLazyMintErc20", rmrkContractAddress);
await rmrkContract.mint(recipientAddress, numToMint);
```

### Native Currency Payments

For contracts like `RMRKEquippableLazyMintNative`, you'll send the native currency along with the transaction:

```javascript
const contract = await ethers.getContractAt("RMRKEquippableLazyMintNative", contractAddress);
const price = await contract.pricePerMint();
await contract.mint(recipientAddress, numToMint, { value: price.mul(numToMint) });
```

### Pre-minting

If you're the contract owner or a contributor, you can use the `RMRKEquippablePreMint` contract to pre-mint tokens:

```javascript
const contract = await ethers.getContractAt("RMRKEquippablePreMint", contractAddress);
await contract.mint(recipientAddress, numToMint, "ipfs://your-token-uri");
```

Remember to handle errors and transaction receipts in your actual implementation.

This guide covers the basics of interacting with RMRK-based NFTs. As you become more familiar with the system, you can explore more advanced features and customizations available in the RMRK ecosystem.
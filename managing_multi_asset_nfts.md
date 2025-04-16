# Managing Multi-Asset NFTs

Multi-asset NFTs are a powerful extension of the traditional NFT concept, allowing a single token to contain multiple assets. This guide will walk you through the process of managing multi-asset NFTs using the RMRK protocol, including adding, removing, and prioritizing assets. We'll also explore the benefits and use cases of multi-asset NFTs.

## Table of Contents

1. [Introduction to Multi-Asset NFTs](#introduction-to-multi-asset-nfts)
2. [Benefits of Multi-Asset NFTs](#benefits-of-multi-asset-nfts)
3. [Managing Assets](#managing-assets)
   - [Adding Assets](#adding-assets)
   - [Accepting Assets](#accepting-assets)
   - [Rejecting Assets](#rejecting-assets)
   - [Setting Asset Priorities](#setting-asset-priorities)
4. [Approvals for Asset Management](#approvals-for-asset-management)
5. [Use Cases](#use-cases)
6. [Best Practices](#best-practices)

## Introduction to Multi-Asset NFTs

Multi-asset NFTs are an innovative concept that allows a single NFT to contain multiple assets. This is implemented in the RMRK protocol through the `RMRKMultiAsset` contract, which extends the traditional ERC721 standard with additional functionality for managing multiple assets within a single token.

## Benefits of Multi-Asset NFTs

1. **Versatility**: A single NFT can represent multiple items or attributes, making it more flexible and feature-rich.
2. **Reduced Gas Costs**: Instead of minting multiple NFTs, you can add multiple assets to a single NFT, potentially saving on gas fees.
3. **Dynamic Content**: Assets can be added, removed, or prioritized over time, allowing for evolving NFTs.
4. **Enhanced User Experience**: Users can interact with multiple assets within a single NFT, providing a more engaging experience.

## Managing Assets

### Adding Assets

To add assets to an NFT, you'll need to implement the `addAssetToToken` function in your contract. This function is not directly provided in the `RMRKMultiAsset` contract, but you can implement it as follows:

```solidity
function addAssetToToken(uint256 tokenId, uint64 assetId, uint64 replacesAssetWithId) external {
    _addAssetToToken(tokenId, assetId, replacesAssetWithId);
}
```

### Accepting Assets

Assets added to a token may need to be accepted before they become active. Use the `acceptAsset` function:

```solidity
function acceptAsset(uint256 tokenId, uint256 index, uint64 assetId) public virtual onlyApprovedForAssetsOrOwner(tokenId) {
    _acceptAsset(tokenId, index, assetId);
}
```

This function can only be called by the token owner or an approved address.

### Rejecting Assets

To reject a specific asset:

```solidity
function rejectAsset(uint256 tokenId, uint256 index, uint64 assetId) public virtual onlyApprovedForAssetsOrOwner(tokenId) {
    _rejectAsset(tokenId, index, assetId);
}
```

To reject all pending assets:

```solidity
function rejectAllAssets(uint256 tokenId, uint256 maxRejections) public virtual onlyApprovedForAssetsOrOwner(tokenId) {
    _rejectAllAssets(tokenId, maxRejections);
}
```

### Setting Asset Priorities

You can set the priority order of assets using the `setPriority` function:

```solidity
function setPriority(uint256 tokenId, uint64[] calldata priorities) public virtual onlyApprovedForAssetsOrOwner(tokenId) {
    _setPriority(tokenId, priorities);
}
```

This allows you to determine the order in which assets are displayed or used.

## Approvals for Asset Management

The `RMRKMultiAsset` contract introduces additional approval mechanisms for managing assets:

1. **Approve for Assets**: Grant permission to an address to manage assets for a specific token.

```solidity
function approveForAssets(address to, uint256 tokenId) public virtual {
    // Implementation details
}
```

2. **Get Approved for Assets**: Check which address is approved to manage assets for a token.

```solidity
function getApprovedForAssets(uint256 tokenId) public view virtual returns (address) {
    _requireMinted(tokenId);
    return _tokenApprovalsForAssets[tokenId];
}
```

3. **Is Approved for Assets or Owner**: Check if an address is the owner or approved to manage assets for a token.

```solidity
function _isApprovedForAssetsOrOwner(address user, uint256 tokenId) internal view virtual returns (bool) {
    address owner = ownerOf(tokenId);
    return (user == owner || isApprovedForAllForAssets(owner, user) || getApprovedForAssets(tokenId) == user);
}
```

## Use Cases

1. **Gaming Items**: A single NFT can represent a character with multiple equipment pieces as separate assets.
2. **Digital Art**: Artists can create NFTs with multiple variations or layers as different assets.
3. **Event Tickets**: An NFT ticket could contain multiple assets for different aspects of an event (e.g., main event, VIP area, merchandise).
4. **Real Estate**: A property NFT could have multiple assets representing different documents (deed, inspection report, photos).

## Best Practices

1. **Asset Management**: Carefully consider which assets to add, accept, or reject to maintain the NFT's value and relevance.
2. **Prioritization**: Use asset priorities to create a meaningful order for displaying or using assets.
3. **Approval Delegation**: Use the approval mechanisms judiciously to allow trusted parties to manage assets without transferring ownership.
4. **Gas Optimization**: Batch operations when possible to reduce gas costs, especially when managing multiple assets.
5. **User Experience**: Design your application to clearly display and interact with multiple assets within a single NFT.

By leveraging the power of multi-asset NFTs, you can create more dynamic, versatile, and engaging token experiences for your users.
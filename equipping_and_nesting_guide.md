# Equipping and Nesting Guide

## Introduction

RMRK NFTs introduce advanced features like equipping and nesting, which allow for more complex and interactive NFT ecosystems. This guide will walk you through the concepts, benefits, and steps to implement these features in your RMRK NFT collections.

## Equipping

Equipping allows NFTs to be "worn" or utilized by other NFTs, creating a dynamic relationship between tokens.

### Key Concepts

- **Equippable NFTs**: NFTs that can be equipped into other NFTs.
- **Slot**: A designated space in an NFT where another NFT can be equipped.
- **Catalog**: Defines the valid equippable items for specific slots.

### Benefits

1. Enhanced interactivity between NFTs
2. Creation of composite NFTs with changeable parts
3. New gameplay mechanics for NFT-based games

### Implementation

To implement equipping functionality:

1. Deploy an `RMRKEquippable` contract for your collection.
2. Define slots and catalogs for your NFTs.
3. Mint equippable NFTs.
4. Use the `equip` function to attach an NFT to a slot in another NFT.

Example:

```solidity
function equip(IntakeEquip memory data) public virtual onlyApprovedOrOwner(data.tokenId) nonReentrant {
    _equip(data);
}
```

The `IntakeEquip` struct contains:
- `tokenId`: ID of the parent NFT
- `childIndex`: Index of the child NFT
- `assetId`: ID of the asset being equipped
- `slotPartId`: ID of the slot to equip into
- `childAssetId`: ID of the child asset being equipped

## Nesting

Nesting allows NFTs to own other NFTs, creating a hierarchical structure.

### Key Concepts

- **Parent NFT**: An NFT that can own other NFTs.
- **Child NFT**: An NFT owned by another NFT.
- **Pending Children**: Child NFTs waiting to be accepted by the parent.

### Benefits

1. Creation of complex, hierarchical NFT structures
2. Bundling of related NFTs
3. New ownership models for digital assets

### Implementation

To implement nesting functionality:

1. Deploy an `RMRKNestable` contract for your collection.
2. Use the `nestTransferFrom` function to transfer child NFTs to parent NFTs.
3. Manage pending and active children using the provided functions.

Example:

```solidity
function nestTransferFrom(
    address from,
    address to,
    uint256 tokenId,
    uint256 destinationId,
    bytes memory data
) public virtual onlyApprovedOrDirectOwner(tokenId) {
    _nestTransfer(from, to, tokenId, destinationId, data);
}
```

## Best Practices

1. **Careful Planning**: Design your NFT ecosystem with equipping and nesting in mind from the start.
2. **Gas Optimization**: Be mindful of the gas costs associated with complex nesting structures.
3. **User Experience**: Provide clear interfaces for users to interact with equipped and nested NFTs.
4. **Security**: Implement proper access controls and checks to prevent unauthorized equipping or nesting.

## Conclusion

Equipping and nesting are powerful features that can significantly enhance the functionality and value of your NFT collections. By understanding and implementing these concepts, you can create more engaging and versatile NFT experiences for your users.

For more detailed information on the specific functions and their implementations, refer to the `RMRKEquippable` and `RMRKNestable` contract documentation.
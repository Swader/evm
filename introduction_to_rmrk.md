# Introduction to RMRK

RMRK (pronounced "remark") is an advanced NFT standard that enhances the functionality and versatility of non-fungible tokens. It introduces a set of powerful features that go beyond traditional NFT implementations, allowing for more complex and interactive digital assets.

## Core Concepts

RMRK is built on several key concepts that expand the capabilities of NFTs:

1. **Equippable**: Allows NFTs to be equipped into other NFTs, creating composable and interactive digital assets.
2. **Nestable**: Enables NFTs to own other NFTs, creating hierarchical relationships between tokens.
3. **MultiAsset**: Permits a single NFT to have multiple visual representations or properties.

These concepts work together to create a flexible and extensible NFT ecosystem.

## Benefits of RMRK

- **Enhanced Interactivity**: NFTs can interact with each other, opening up new possibilities for gaming, digital art, and virtual worlds.
- **Increased Flexibility**: A single NFT can have multiple representations or properties, allowing for dynamic and evolving digital assets.
- **Hierarchical Ownership**: NFTs can own other NFTs, enabling complex ownership structures and nested collections.
- **Efficient Resource Management**: The ability to equip and nest NFTs reduces the need for creating new tokens for every variation or combination.

## Use Cases

1. **Gaming**: Create characters with equippable items, nested inventories, and multiple visual representations.
2. **Digital Art**: Develop evolving artworks with interchangeable elements or collaborative pieces owned by multiple artists.
3. **Virtual Real Estate**: Build complex property structures with nested ownership and customizable elements.
4. **Collectibles**: Design dynamic collections with interchangeable parts and hierarchical relationships.

## Main Modules

### Equippable (RMRKEquippable)

The Equippable module allows NFTs to be equipped into other NFTs. This is achieved through a system of catalogs, parts, and assets.

Key features:
- Define equippable groups and valid parent slots
- Equip and unequip child NFTs into parent NFTs
- Manage asset equipability and catalog associations

Example usage:
```solidity
function equip(IntakeEquip memory data) public virtual onlyApprovedOrOwner(data.tokenId) nonReentrant {
    _equip(data);
}
```

### Nestable (RMRKNestable)

The Nestable module enables NFTs to own other NFTs, creating parent-child relationships between tokens.

Key features:
- Add, accept, and reject child NFTs
- Transfer child NFTs between parent tokens
- Manage pending and active children

Example usage:
```solidity
function addChild(uint256 parentId, uint256 childId, bytes memory data) public virtual {
    _requireMinted(parentId);
    address childAddress = _msgSender();
    if (!childAddress.isContract()) revert RMRKIsNotContract();
    // ... (additional logic)
}
```

### MultiAsset (RMRKMultiAsset)

The MultiAsset module allows a single NFT to have multiple visual representations or properties.

Key features:
- Add and manage multiple assets for a single token
- Set priorities for assets
- Accept or reject pending assets

Example usage:
```solidity
function addAssetEntry(
    uint64 id,
    uint64 equippableGroupId,
    address catalogAddress,
    string memory metadataURI,
    uint64[] memory partIds
) internal virtual {
    _addAssetEntry(id, metadataURI);
    // ... (additional logic)
}
```

## Getting Started

To start using RMRK in your project, you'll need to import the relevant contracts and interfaces. Here's a basic example of how to create an RMRK-compatible token:

```solidity
pragma solidity ^0.8.21;

import "@rmrk-team/evm-contracts/contracts/RMRK/equippable/RMRKEquippable.sol";

contract MyRMRKToken is RMRKEquippable {
    constructor(string memory name, string memory symbol) RMRKEquippable(name, symbol) {
        // Initialize your token here
    }

    // Implement additional functionality as needed
}
```

This example creates a basic RMRK token with Equippable functionality. You can further customize it by adding MultiAsset and Nestable features as required for your specific use case.

## Conclusion

RMRK provides a powerful set of tools for creating advanced, interactive, and flexible NFTs. By leveraging the Equippable, Nestable, and MultiAsset modules, developers can create rich, dynamic digital assets that go beyond the limitations of traditional NFT standards. As you explore RMRK, you'll discover new ways to enhance your NFT projects and create unique user experiences.
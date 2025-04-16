---
title: RMRK Integration Guide
description: A comprehensive guide for developers and project owners on how to integrate RMRK-based NFTs into their existing projects or new applications.
---

# RMRK Integration Guide

## Introduction

This guide is designed to help developers and project owners integrate RMRK-based NFTs into their existing projects or new applications. RMRK is a set of NFT standards that bring advanced features to NFTs, such as multi-asset support, on-chain emotes, and equippable assets. By following this guide, you'll learn how to leverage these features in your projects.

## Table of Contents

1. [Understanding RMRK Contracts](#understanding-rmrk-contracts)
2. [Integration Approaches](#integration-approaches)
3. [Best Practices](#best-practices)
4. [Common Use Cases](#common-use-cases)
5. [Examples of Successful Integrations](#examples-of-successful-integrations)

## Understanding RMRK Contracts

Before integrating RMRK-based NFTs, it's essential to understand the core contracts and their functionalities. The RMRK implementation provides several abstract and concrete contracts that you can use or extend:

### RMRKAbstractEquippable

This is an abstract contract that implements the RMRK equippable module. It provides functions for adding assets to tokens, managing equippable assets, and setting valid parents for equippable groups.

Key functions:

- `addAssetToToken`: Add an asset to a token
- `addEquippableAssetEntry`: Add an equippable asset entry
- `setValidParentForEquippableGroup`: Declare assets as equippable into a specific slot of a parent collection

### RMRKEquippableLazyMintErc20

This contract implements RMRK equippable module with ERC20-powered lazy minting. It allows users to mint tokens by paying with ERC20 tokens.

Key functions:

- `mint`: Mint tokens to a specified address
- `nestMint`: Mint child tokens to a parent token
- `erc20TokenAddress`: Get the address of the ERC20 token used for payments
- `pricePerMint`: Get the price per mint in ERC20 tokens

### RMRKEquippableLazyMintNative

Similar to `RMRKEquippableLazyMintErc20`, but uses native currency (e.g., ETH) for payments instead of ERC20 tokens.

### RMRKEquippablePreMint

This contract implements the RMRK equippable module with pre-minting functionality. It's suitable for projects that want to mint all tokens upfront or in batches.

Key functions:

- `mint`: Mint tokens to a specified address with a given tokenURI
- `nestMint`: Mint child tokens to a parent token with a given tokenURI

## Integration Approaches

There are several ways to integrate RMRK-based NFTs into your project:

1. **Extend existing contracts**: If you're building a new NFT project, you can directly extend one of the RMRK implementation contracts (e.g., `RMRKEquippableLazyMintNative`) and customize it to your needs.

2. **Use RMRK as a dependency**: For existing projects, you can add RMRK as a dependency and use its interfaces and base contracts to add RMRK functionality to your NFTs.

3. **Interact with deployed RMRK contracts**: If you want to integrate with existing RMRK-based NFTs, you can interact with their deployed contracts using their public interfaces.

## Best Practices

When integrating RMRK-based NFTs, consider the following best practices:

1. **Use the appropriate minting strategy**: Choose between lazy minting (ERC20 or native currency) and pre-minting based on your project's requirements.

2. **Implement proper access control**: Use the `onlyOwnerOrContributor` modifier for sensitive functions to ensure only authorized users can perform certain actions.

3. **Handle asset management carefully**: When adding or replacing assets, make sure to validate input and handle edge cases.

4. **Optimize gas usage**: For bulk operations, consider using loops with unchecked increments to save gas.

5. **Implement event listeners**: Listen for important events emitted by RMRK contracts to keep your application in sync with on-chain state changes.

## Common Use Cases

Here are some common use cases for RMRK-based NFTs:

1. **Gaming assets**: Use equippable NFTs to represent in-game items that can be equipped by character NFTs.

2. **Digital art collections**: Leverage multi-asset support to create NFTs with multiple visual representations or layers.

3. **Virtual real estate**: Use nested NFTs to represent buildings or parcels within a larger virtual world.

4. **Membership tokens**: Create NFTs with upgradable assets to represent different membership tiers or levels.

5. **Customizable avatars**: Use equippable NFTs to create avatars with interchangeable parts.

## Examples of Successful Integrations

While we don't have specific examples of successful integrations in the provided context, you can showcase your integration by following these steps:

1. Implement one of the RMRK contracts (e.g., `RMRKEquippableLazyMintNative`) in your project.
2. Create a simple frontend that allows users to mint and manage their NFTs.
3. Demonstrate the equippable functionality by creating parent and child NFTs with equippable assets.
4. Show how to add and replace assets on existing NFTs.
5. Implement a basic marketplace or trading function to showcase the transferability of RMRK-based NFTs.

By following this guide and exploring the provided contract implementations, you'll be well-equipped to integrate RMRK-based NFTs into your projects and leverage their advanced features.
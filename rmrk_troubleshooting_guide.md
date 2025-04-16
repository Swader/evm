# RMRK Troubleshooting Guide

This guide is designed to help developers troubleshoot common issues when working with RMRK-based NFTs. It includes explanations of error messages, their possible causes, and solutions, as well as a FAQ section addressing frequent user questions.

## Common Error Messages and Solutions

### 1. ERC721AddressZeroIsNotaValidOwner

**Cause**: Attempting to grant token ownership to the zero address (0x0).

**Solution**: Ensure you're providing a valid, non-zero address when minting or transferring tokens.

### 2. ERC721ApprovalToCurrentOwner

**Cause**: Trying to grant approval to the current owner of the token.

**Solution**: Check if the address you're granting approval to is different from the current token owner.

### 3. RMRKChildAlreadyExists

**Cause**: Attempting to accept a child that has already been accepted.

**Solution**: Verify the child token's status before trying to accept it again.

### 4. RMRKChildIndexOutOfRange

**Cause**: Attempting to interact with a child using an index higher than the number of children.

**Solution**: Ensure you're using a valid child index within the range of existing children.

### 5. RMRKCollectionNotRegistered

**Cause**: Trying to manage or interact with a collection that is not registered.

**Solution**: Register the collection before performing any operations on it.

### 6. RMRKMintOverMax

**Cause**: Attempting to mint a number of tokens that would exceed the maximum supply.

**Solution**: Check the current supply and the maximum supply before minting. Adjust the number of tokens to mint accordingly.

### 7. RMRKNestableTooDeep

**Cause**: Attempting to nest a child over the nestable limit (current limit is 100 levels of nesting).

**Solution**: Ensure your nesting structure doesn't exceed the maximum allowed depth.

### 8. RMRKNotApprovedOrDirectOwner

**Cause**: Attempting to interact with a token without being its owner or having been granted permission.

**Solution**: Verify that the caller is either the token owner or has been approved to manage the token.

## FAQ

### Q1: What is the difference between `mint` and `nestMint`?

A1: `mint` is used to create new tokens and assign them to a specific address, while `nestMint` is used to create new tokens as children of existing tokens. Use `nestMint` when you want to create hierarchical relationships between NFTs.

### Q2: How do I set up royalties for my RMRK NFTs?

A2: Royalties are set during the contract initialization. Use the `royaltyRecipient` and `royaltyPercentageBps` parameters when deploying your contract to specify the royalty recipient and percentage (in basis points).

### Q3: Can I change the maximum supply after deploying the contract?

A3: No, the maximum supply is set during contract initialization and cannot be changed afterward. Make sure to carefully consider your desired maximum supply before deploying.

### Q4: How do I add assets to my RMRK NFTs?

A4: You can add assets using the `addAssetEntry` function in the RMRKEquippable contracts. This allows you to associate multiple assets with a single NFT.

### Q5: What is the purpose of the `erc20TokenAddress` in RMRKEquippableLazyMintErc20?

A5: The `erc20TokenAddress` specifies the ERC20 token that will be used for payments when minting NFTs in the RMRKEquippableLazyMintErc20 contract. Users will need to approve the contract to spend the specified ERC20 token before minting.

### Q6: How can I withdraw the funds raised from minting?

A6: For native currency payments, use the `withdrawRaised` function in RMRKEquippableLazyMintNative. For ERC20 payments, use the `withdrawRaisedERC20` function in RMRKEquippableLazyMintErc20. Both functions can only be called by the contract owner.

### Q7: What should I do if I encounter a "RMRKMintZero" error?

A7: This error occurs when attempting to mint zero tokens. Ensure that you're specifying a positive number of tokens to mint in your function call.

### Q8: How can I check if a token is soulbound (non-transferrable)?

A8: RMRK supports soulbound tokens, but the implementation may vary. Generally, you can check if a token is transferrable by attempting to transfer it or by looking for a specific flag in the token's metadata or contract state.

## Best Practices

1. Always check for error messages and handle them appropriately in your frontend applications.
2. Use the `onlyOwnerOrContributor` modifier when implementing functions that should be restricted to the contract owner or authorized contributors.
3. When working with nested NFTs, be mindful of the nesting depth limit to avoid the `RMRKNestableTooDeep` error.
4. Regularly check and update your token URIs to ensure they point to valid metadata.
5. When implementing custom logic, make sure to respect the RMRK standards and existing implementations to maintain compatibility.

By following this troubleshooting guide and adhering to best practices, you can create robust and error-resistant applications using RMRK-based NFTs. If you encounter issues not covered in this guide, please refer to the official RMRK documentation or reach out to the community for support.
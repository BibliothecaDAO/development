---
sidebar_position: 5
title: Tokens
---

# Overview

Tokens following OpenZeppelin standards where possible so they can easily interoperate with external services.


## ERC721 Contracts

### Realms

The Core Realms ERC721 contract. Contains the on-chain metadata for each Realm.

### S_Realms

Players receive an S_Realm when they have staked their Realm. This allows the player to interact with contracts.

---

## ERC20 Contracts

### $LORDS

LORDS is the native token of the Realmverse. It exists on both Ethereum mainnet and StarkNet.

---

## ERC1155 Contracts

### Resources

The Resources contract contains all 22 Realms resources and other fungible tokens of the Realmverse. New modules can propose to extend this contract. Since ERC1155 tokens are denoted by an ID, we can simply allowing minting of new IDS. The benefit of this is native interoperability with the rest of the game.
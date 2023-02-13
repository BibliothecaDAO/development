# Concepts

Terms to consider. We recommend reading the [Master Scroll](https://scroll.bibliothecadao.xyz) which outlines the theory behind the game. 

Eternum is in active development and is evolving every month. This information could be outdated.

#### Player Account
  - A player with a wallet
  
#### Governance Account
  - An admin who controls the Arbiter.
  - The admin may be an L2 DAO to administer governance decisions
    voted through on L2, where voting will be cheap.
  - Governance might enable a new module to have write-access to
    and important game variable. For example, to change the location
    that a player is currently in. All other modules that read and use location
    would be affected by this.

#### Arbiter
  - Contract that can update/add module mappings in ModuleController

#### Module Controller
  - The game 'swichboard' that connects all modules.
  - Is the reference point for all modules. Modules call this
    contract as the source of truth for the address of other modules.
  - The controller stores where modules can be found, and which modules
    have write access to other modules.

#### Modules (open ended set)
  - Game mechanics (where a player would interact to play).
  - Storage modules (game variables).
  - L1 connectors (for integrating L1 state/ownership to L2)
  - Other arbitrary contracts

---

## How does the game work?

From a technical POV the game has two central contracts. The `ModuleController.cairo` and `Arbiter.cairo`. All the games logic is split into Modules whose addresses are stored within the `ModuleController.cairo`.

### Module Controller

The `ModuleController.cairo` acts like a "switchboard" for the game. All modules route via it as it controls what modules can write. It is the long lived contract that should not have to be upgradable. 

It contains:

- Contract addresses
- Permissions of each contract

#### Arbiter

The Arbiter contract owns the `ModuleController.cairo` contract. Only the owner of the `Arbiter.cairo` can adjust the game state. In production the `Arbiter.cairo` will be owned by a Multisig, or itself might be a multisig.

---

## Design Patterns

The game revolves around a Module Controller, this acts like a switchboard for the modules to route through. It controls what modules can write to what other module.

### Proxy Pattern
You will notice all contracts follow the proxy pattern. We believe in immutability when you do not have ownership governance, however games require constant upgrades, hence why we use the proxy pattern. Currently the owner of the contracts is the deployer, however this will be change to the Arbiter once in production. For fast iteration we have purposely left it as is.

### Module structure (Core, Library, Interface, Constants)
All modules follow the same pattern. Once a module is complete it can be added to the `ModuleController.cairo` contract.

#### `Core.cairo`
This contains the actual deployable contract. This contract contains imports from the modules Library, Interface and Constants files. It is best practice to develop this part of the module last. All logic should be ommited from this contract where possible and be contained within the `library.cairo` file. Depoloying and testing contracts even in tests takes time, so by offloading all the logic into the libraries we can greatly accelerate development.

#### `library.cairo`
Libraries are composed of small composable stateless functions. They are the core of the module and contain all the logic necessary.

#### `interface.cairo`
Interface file contains the necessary public endpoints to allow the contract to be called by another contract.

#### `constants.cairo`
Any specific `consts` that belong to the module go in this file. Any generalised `structs` live in `contracts/settling_game/utils/game_structs.cairo` file.

---
Get started by copying the module template folder and renaming.

`contracts/settling_game/modules/example`

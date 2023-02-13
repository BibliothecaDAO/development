## Design Principles
1. Layered architecture with minimally biased primitives at the core.
2. Make all biases/stats at each layer of the stack easily modifiable.
3. Maintain integrity of OG Loot as described in https://docs.loot.foundation/

## Design Overview
Starknet Loot consists of four primitives:
1. Items
2. Bags
3. Adventurers
4. Physics/Statistics

### Items
Starknet Loot items will feature the same items that appear in the original Loot bags but with a few changes:
1. Items become a standalone primitive with a unique identifier enabling them to be traded separately from the bags and more explicitly referenced by on-chain stories.
2. For ease of use, the item contract will provide direct api access to all of the OG Loot item attributes such as: name prefix, suffix (Order), greatness, and rank
3. Starknet Loot items will feature two new attributes:
   1. State: {Equipped, Bagged, Loose}. When equipped, the item will store the adventurer wielding that item. When bagged, the item will store the loot bag the item is in. When loose, the item will provide x,y coordinate of it's location
   2. Material: {Steel, Gold, Hide, Cloth, etc}. The mapping of item->material will be provided via a separate contract which will provide ability for anyone to add their own mappings. More on this topic in the Physics/Statistics section.


### Bags
Starknet Loot bags will be a separate primitive which will serve to store and protect the Loot items. The bags will have an expandable carrying capacity and provide list of the items inside the bag.

### Physics and Statistics (Utility Contracts

The Physics and Statistics contracts will utilize a layered approach, seeking to keep the core as unbiased as possible, with each additional layer becoming increasingly more biased. For example:
- L0: Physics (i.e the density of steel is 7.85 g/cm3)
- L1: Loot Physics (i.e katanas are made of steel)
- L2: Loot Combat (i.e katana is the top ranked blade, blades are highly effective against cloth)
- L3: Damage System (i.e item rank has a multiplicative effective on damage, critical hit does 1.5x damage, defense)
- L4: Game Engine: (i.e adventurer1 using a katana to attack adventurer2 who is wearing a divine robe will deal 100HP of damage)

The higher layers of the stack will depend on constants defined in the lower layers which will be easily modifiable. For example, the amount of damage a Katana will deal to a Divine Robe will depend on:
1. Katana material (Steel), weapon type (Blade), and rank (1)
2. Divine Robe material (Cloth) and rank (1)
3. Damage multiplier for Blade vs Cloth
4. Damage and armor multiplier for item rank


The contract will come with a default set of configuration biases (configId 0) but users will be able to easily add their own. For example calling `getMaterial(katana, 0)` would return Steel but if someone preferred katanas to be made of titanium, they could add a new mapping via `addMaterialMapping(katana, titanium)` and then call `getMaterial(katana, 1)` which would return titanium. Mappings will be immutable once they are added to preserve the integrity of the games using those configurations.

By simply changing the material of a particular weapon (or another constant), one could significantly alter the damage that weapon deals without having to change any of the code in the damage system.

### Adventurers
Adventurers will be able to equip loot items, carry loot bags, and of course quest for loot. Adventurers will feature their own statistics will be factored into the damage system.
# Materials and Ores

QuantaVolt adds two ores, a handful of crafting materials and the nuclear and black-hole fuels. Crafting recipes are on
the [Recipes](Recipes) page; the machines that process the materials are on [Machines](Machines).

---

## Ores

| Ore | Height range | Veins per chunk | Vein size | Needs | Drops |
|---|---|---|---|---|---|
| Uranium Ore | Y −48 to 32, triangular distribution (most common around Y −8) | 4 | up to 6 blocks | iron pickaxe | 1 Raw Uranium |
| Lithium Ore | Y −16 to 80, triangular distribution (most common around Y 32) | 6 | up to 8 blocks | stone pickaxe | 1–2 Raw Lithium |
| Lead Ore | Y −40 to 64, triangular distribution (most common around Y 12) | 8 | up to 9 blocks | stone pickaxe | 1–2 Raw Lead |

* Each ore replaces stone-type blocks as the normal ore and deepslate-type blocks as **Deepslate Uranium Ore** /
  **Deepslate Lithium Ore** / **Deepslate Lead Ore**. Veins are not reduced when exposed to air.
* Fortune increases the drops; Silk Touch drops the ore block itself.
* **Biomes:** every biome the Overworld generator can produce, including biomes from world generation mods and data
  packs (Fabric: all Overworld biomes; NeoForge: a biome modifier that covers every biome of the Overworld generator).
  At server start QuantaVolt writes one log line saying how many Overworld biomes it found and in how many the ores
  are missing.
* The ore features are data (`quantavolt:uranium_ore`, `quantavolt:lithium_ore`, `quantavolt:lead_ore` under `worldgen/configured_feature`
  and `worldgen/placed_feature`), so a data pack can change or empty them.

---

## Items

| Item | Comes from | Used for |
|---|---|---|
| <img src="images/items/raw_uranium.png" width="32" alt=""> **Raw Uranium** | Uranium Ore | Crusher → 2 Uranium Dust |
| <img src="images/items/raw_lithium.png" width="32" alt=""> **Raw Lithium** | Lithium Ore | Crusher → 2 Lithium Dust |
| <img src="images/items/uranium_dust.png" width="32" alt=""> **Uranium Dust** | Crusher | Chemical Processor → Yellowcake |
| <img src="images/items/lithium_dust.png" width="32" alt=""> **Lithium Dust** | Crusher | Chemical Processor → Lithium Carbonate |
| <img src="images/items/yellowcake.png" width="32" alt=""> **Yellowcake** | Chemical Processor (+250 mB water) | Centrifuge Cascade, 4 per batch |
| <img src="images/items/enriched_uranium.png" width="32" alt=""> **Enriched Uranium** | Centrifuge Cascade (1 per batch) | Fuel Fabricator → 4 Uranium Fuel Pellets; Containment Rod recipe |
| <img src="images/items/depleted_uranium.png" width="32" alt=""> **Depleted Uranium** | Centrifuge Cascade (3 per batch) | Byproduct, no use in QuantaVolt |
| <img src="images/items/uranium_pellet.png" width="32" alt=""> **Uranium Fuel Pellet** | Fuel Fabricator | Fuel Fabricator: 4 pellets + Empty Fuel Rod |
| <img src="images/items/empty_fuel_rod.png" width="32" alt=""> **Empty Fuel Rod** | Crafting (steel and glass, 2 per craft) | Fuel Fabricator |
| <img src="images/items/uranium_fuel_rod.png" width="32" alt=""> **Uranium Fuel Rod** | Fuel Fabricator | Fission Reactor fuel, 10,000,000 HU per rod |
| <img src="images/items/depleted_fuel_rod.png" width="32" alt=""> **Depleted Fuel Rod** | Fission Reactor (a spent rod comes out of the item output) | Byproduct, no use in QuantaVolt |
| <img src="images/items/lithium_carbonate.png" width="32" alt=""> **Lithium Carbonate** | Chemical Processor (+250 mB water) | Battery Cell, Breeding Blanket and Stellar Containment Glass recipes; Tokamak tritium breeding (2,000 lithium units per item) |
| <img src="images/items/raw_lead.png" width="32" alt=""> **Raw Lead** | Lead Ore | Furnace (200 ticks) or Blast Furnace (100 ticks) → Lead Ingot |
| <img src="images/items/lead_ingot.png" width="32" alt=""> **Lead Ingot** | Raw Lead or Lead Ore smelted; 9 from a Block of Lead | Block of Lead, Lead Concrete, Lead Glass, radiation suit (see [Safety and Incidents](Safety-and-Incidents#radiation)) |
| <img src="images/items/steel_blend.png" width="32" alt=""> **Steel Blend** | Crafting: 1 iron ingot + 2 coal or charcoal | Blast Furnace → Steel Ingot |
| <img src="images/items/steel_ingot.png" width="32" alt=""> **Steel Ingot** | Blast Furnace (100 ticks) | Most plant parts |
| <img src="images/items/biomass.png" width="32" alt=""> **Biomass** | Crafting: 3 wheat, 4 leaves or 2 saplings | Gasifier (7,000 mB syngas); Industrial Boiler (400 burn ticks). Not a furnace fuel. |
| <img src="images/items/ash.png" width="32" alt=""> **Ash** | Gasifier (1 per 4 fuel items) | Byproduct, no use in QuantaVolt |
| <img src="images/items/compressed_matter.png" width="32" alt=""> **Compressed Matter** | Matter Compressor: 8 compressible blocks | Fuel of the Micro Black Hole Plant and Hawking Reactor; 1 item = 1 mass unit = 10,000,000 E (`energyPerMassUnit`) |
| <img src="images/items/singularity_capsule.png" width="32" alt=""> **Singularity Capsule** | Split off a running Micro Black Hole Plant (3 mass units each) | Starts a Hawking Reactor; Hawking Reactor Controller and Dimension Core recipes |

---

## Processing chains

### Uranium → fuel rods

| Step | Machine | In | Out |
|---|---|---|---|
| 1 | Crusher (100 t, 20 E/t) | 1 Raw Uranium (or 1 uranium ore block) | 2 Uranium Dust |
| 2 | Chemical Processor (160 t, 30 E/t) | 1 Uranium Dust + 250 mB water | 1 Yellowcake |
| 3 | Centrifuge Cascade (2,400 separative work; each Gas Centrifuge does 1 per tick for 40 E) | 4 Yellowcake | 1 Enriched Uranium + 3 Depleted Uranium |
| 4 | Fuel Fabricator (100 t, 40 E/t) | 1 Enriched Uranium | 4 Uranium Fuel Pellets |
| 5 | Fuel Fabricator (200 t, 40 E/t) | 4 Uranium Fuel Pellets + 1 Empty Fuel Rod | 1 Uranium Fuel Rod |

So two Raw Uranium give four Yellowcake, one Enriched Uranium and one Uranium Fuel Rod.

### Lithium → Lithium Carbonate

Crusher: 1 Raw Lithium → 2 Lithium Dust. Chemical Processor: 1 Lithium Dust + 250 mB water → 1 Lithium Carbonate.

### Gasifier fuels

Each batch takes 160 ticks per Reaction Chamber and 250 mB of steam.

| Fuel (item tag) | Syngas per item |
|---|---|
| Coal, Charcoal (`quantavolt:gasifier_fuel/coal`) | 34,000 mB |
| Coal Block (`quantavolt:gasifier_fuel/coal_block`) | 306,000 mB |
| Biomass (`quantavolt:gasifier_fuel/biomass`) | 7,000 mB |

### Compressible blocks

The Matter Compressor accepts 8 of any item in `quantavolt:compressible`: Cobblestone, Cobbled Deepslate, Stone,
Deepslate, Dirt, Gravel, Sand, Netherrack, Andesite, Diorite, Granite, Tuff, Blackstone, Basalt, End Stone.

---

## Tags shared with other mods

QuantaVolt puts its own items into the common `c:` tags, and most of its recipes and machines read tags, so equivalent
materials from other mods work where the tag says so.

**Tags QuantaVolt fills:**

| Tag | Contents |
|---|---|
| `c:ores`, `c:ores/uranium`, `c:ores/lithium`, `c:ores/lead` (block and item) | the six ore blocks |
| `c:ores_in_ground/stone`, `c:ores_in_ground/deepslate` (block and item) | the stone and deepslate variants |
| `c:raw_materials/uranium`, `c:raw_materials/lithium`, `c:raw_materials/lead` | Raw Uranium, Raw Lithium, Raw Lead |
| `c:ingots/lead`, `c:storage_blocks/lead` (block and item) | Lead Ingot, Block of Lead |
| `c:dusts/uranium`, `c:dusts/lithium` | Uranium Dust, Lithium Dust |
| `c:ingots/steel` | Steel Ingot |
| `c:steam` (fluid) | Steam |

**Tags QuantaVolt reads:**

| Tag | Used by | Default contents |
|---|---|---|
| `quantavolt:materials/uranium` | Crusher | Raw Uranium + `c:raw_materials/uranium` |
| `quantavolt:materials/lithium` | Crusher | Raw Lithium + `c:raw_materials/lithium` |
| `c:ores/uranium`, `c:ores/lithium` | Crusher | any mod's uranium / lithium ore |
| `c:dusts/uranium`, `c:dusts/lithium` | Chemical Processor | any mod's uranium / lithium dust |
| `quantavolt:materials/yellowcake` | Centrifuge Cascade | Yellowcake |
| `quantavolt:enriched_uranium`, `quantavolt:uranium_pellets`, `quantavolt:empty_fuel_rods` | Fuel Fabricator | the QuantaVolt items |
| `quantavolt:fission_fuel` | Fission Reactor | Uranium Fuel Rod |
| `quantavolt:breeding_lithium` | Tokamak | Lithium Carbonate |
| `quantavolt:materials/structural_steel` | recipes | `c:ingots/steel` (any mod's steel) |
| `quantavolt:materials/lead` | Furnace and Blast Furnace → Lead Ingot | Raw Lead + `c:raw_materials/lead` |
| `c:ores/lead` | Furnace → Lead Ingot | any mod's lead ore |
| `c:ingots/lead` | lead recipes (blocks, glass, concrete, suit) | any mod's lead ingot |
| `quantavolt:radiation_shielding` (block) | radiation | Block of Lead, Lead Concrete, Lead Glass + `c:storage_blocks/lead` |
| `quantavolt:blast_shielding` (block) | non-explosive incidents | Reinforced Concrete, Reinforced Glass |
| `quantavolt:gasifier_fuel/*` | Gasifier | see above |
| `quantavolt:compressible` | Matter Compressor | see above |
| `quantavolt:steam` (fluid) | all steam inputs | Steam + `c:steam` (other mods' steam) |
| `quantavolt:thermoelectric/hot`, `hot_strong`, `cold`, `cold_strong` (block) | Thermoelectric and Stirling Generator | see [Machines](Machines) |

Some `c:` tags inside QuantaVolt's tags are optional: if no other mod provides them, nothing breaks.

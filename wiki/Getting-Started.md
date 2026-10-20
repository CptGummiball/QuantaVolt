# Getting Started

QuantaVolt is an industrial power mod: you start with a single burning dynamo and work your way up through steam,
gas, renewables and storage to fission, fusion, an artificial star and black hole technology. Large plants are
multiblocks you build yourself, block by block.

**Required mod:** Pipster must be installed (it is not bundled). All QuantaVolt gases (hydrogen,
syngas, deuterium …) live only in Pipster's gas system and travel through Pipster's gas pipes.

Recipes for everything on this page are on the [Recipes](Recipes) page. Numbers below are the defaults of the
[server configuration](Configuration).

---

## 1. Ores

| Ore | Height | Vein size | Tool | Drops |
|---|---|---|---|---|
| Uranium Ore / Deepslate Uranium Ore | Y −48 to 32 (most common in the middle), 4 veins per chunk | up to 6 | iron pickaxe | 1 Raw Uranium (Fortune applies) |
| Lithium Ore / Deepslate Lithium Ore | Y −16 to 80 (most common in the middle), 6 veins per chunk | up to 8 | stone pickaxe | 1–2 Raw Lithium (Fortune applies) |
| Lead Ore / Deepslate Lead Ore | Y −40 to 64 (most common in the middle), 8 veins per chunk | up to 9 | stone pickaxe | 1–2 Raw Lead (Fortune applies) |

All three ores generate in every Overworld biome, including biomes added by world generation mods and data packs. Details:
[Materials and Ores](Materials-and-Ores).

Two other materials you will need early:

* **Steel Ingot** – craft a Steel Blend from 1 iron ingot and 2 coal or charcoal, then smelt it in a Blast Furnace.
* **Biomass** – crafted from wheat, leaves or saplings; a fuel for the Gasifier and the Industrial Boiler.

---

## 2. First machines

| Block | What it does |
|---|---|
| <img src="images/items/basic_dynamo.png" width="32" alt=""> **Basic Dynamo** | Burns any furnace fuel, 40 E/t while burning, pushes energy into every neighbor. Your first generator. |
| <img src="images/items/energy_cell.png" width="32" alt=""> **Energy Cell** | Stores 1,000,000 E, takes energy on every side except the front, gives it out of the front (2,000 E/t). |
| <img src="images/items/fluid_tank.png" width="32" alt=""> **Fluid Tank** / **Gas Tank** | 32,000 mB of one fluid (see-through, shows the fill level) / 64,000 mB of one gas. |
| <img src="images/items/pump.png" width="32" alt=""> **Pump** | Pumps 100 mB/t of water from an infinite water source directly below it, for 10 E/t. |
| <img src="images/items/crusher.png" width="32" alt=""> **Crusher**, **Chemical Processor**, **Fuel Fabricator** | Ore processing for the nuclear chain. |
| <img src="images/items/condenser.png" width="32" alt=""> **Condenser** | Turns turbine exhaust steam back into water. |
| <img src="images/items/electrolyzer.png" width="32" alt=""> **Electrolyzer** | Water + energy into hydrogen and oxygen (and back, in fuel cell mode). |

All single-block machines with their numbers: [Machines](Machines).

---

## 3. Moving energy, fluids and gases

QuantaVolt has no cables or pipes of its own. Its machines and plant ports use the standard interfaces of the loader,
so cables and pipes of other mods (for example Pipster) connect to them.

* **Energy** is measured in **E**. 1 E = 1 FE = 1 Team Reborn Energy unit. Generators push energy into neighbors.
* **Fluids** (water, steam, exhaust steam, hot coolant) are normal fluids in mB.
* **Gases** move only through Pipster's gas pipes (unit mB). They are not fluids.
* **Heat** (HU) moves only between QuantaVolt HEAT ports and heat machines that touch each other.

Details: [Energy, Fluids and Gases](Energy-Fluids-Gases).

---

## 4. How multiblocks work

Most plants are hollow boxes:

* **Frame** – every edge and corner must be the plant's frame block (usually its casing).
* **Walls** – casing, the matching sight glass, an **Inspection Hatch** and plant-specific wall parts.
* **Controller** – sits in a wall with its front facing out. You never set a size: the controller looks from the block
  behind it into the structure and finds the walls itself.
* **Ports** – Item, Fluid, Gas, Energy Input/Output Ports and the Heat Port go in the walls. Each plant allows only
  certain port types. A port connects only on its outer face and only while the plant is formed.
* **Interior** – the working parts (combustion chambers, rotor blades, fuel assemblies …), often with air allowed.

Right-click the controller to see the status. Once the plant is formed, its ports and any **Inspection Hatch** in the
wall open the same screen, so you can check a large plant from any side. The first line of the screen says
**Formed** or exactly what is wrong, for example *Wrong block at … (expected: …)*, *Missing parts: …*,
*Port not allowed here* or *Structure too large or not closed*. If part of a plant is in an unloaded chunk, it pauses
(*Paused (part of the structure is not loaded)*). The default size limit is 16 blocks per edge (fission reactor 15).

A few plants have other shapes: the Wind Turbine (nacelle, rotor and tower), the Gas Engine (a line of cylinders), and
the Solar Array, Solar Thermal field and Capacitor Bank (any shape of connected modules around the controller).

**Build Projector:** place the controller, then right-click it with a Build Projector. Choose the size, switch the
projection on, and the plan appears in the world: small floating blocks where parts are missing, red frames where
something is in the way, plus a list of the blocks you still need. See [Build Projector](Build-Projector).

---

## 5. Steam power

The classic power plant: **Industrial Boiler → Steam Turbine → Condenser**.

* **[Industrial Boiler](Build-Industrial-Boiler)** (from 3×4×3): Combustion Chambers on the lowest interior layer,
  Heat Exchanger Tubes above. Burns solid fuel (furnace fuel and Biomass), syngas, natural gas or heat from HEAT ports. Each chamber
  gives up to 100 HU/t; each tube boils up to 40 mB/t of steam; 1 mB water becomes 10 mB steam. Default setpoint
  250 °C (100–350 °C). Add **Safety Valves** to the walls (see [Safety and Incidents](Safety-and-Incidents)).
* **[Steam Turbine](Build-Steam-Turbine)** (from 5×5×5, odd cross-section): a Rotor Shaft through the middle, each
  slice holds either Rotor Blades (25 mB/t of steam each) or Generator Coils (up to 120 E/t each). The rotor reaches
  its best efficiency at 1,800 rpm. Too many coils for the steam slow the rotor down; the screen then says
  *Generator overloaded*.
* **Condenser** – closes the water loop (10 mB exhaust steam → 1 mB water).

Other steam sources: the **Geothermal Heat Exchanger** (lava and magma below) and the **Heat Exchanger** (hot coolant
from reactors and engines).

---

## 6. Gas power

| Plant / machine | Role |
|---|---|
| <img src="images/items/electrolyzer.png" width="32" alt=""> **Electrolyzer** | Water + energy → hydrogen + oxygen. |
| **[Gasifier](Build-Gasifier)** (from 3×4×3) | Coal, coal blocks or Biomass + steam → syngas and Ash. One batch per Reaction Chamber takes 160 ticks. |
| <img src="images/items/gas_compressor.png" width="32" alt=""> **Gas Compressor** | Turns hydrogen or syngas into its compressed form (+25 % heat in the Gas Turbine). |
| **[Gas Turbine](Build-Gas-Turbine)** (from 5×5×6) | Stages along the shaft in this order: Compressor Blades, Combustion Liners, Rotor Blades, Generator Coils. Burns hydrogen, syngas or natural gas. |
| **[Gas Engine](Build-Gas-Engine)** | 1–8 Engine Cylinders in a line, closed by an Engine Generator. 80 E/t per cylinder; runs at a setpoint or follows demand; cooling water keeps it from overheating. |
| <img src="images/items/gas_prospector.png" width="32" alt=""> **Gas Prospector**, **[Gas Derrick](Build-Gas-Derrick)** (3×3, 6–12 high) | Find a natural gas field and extract it: 60–300 mB/t depending on the height, 0.5 E per mB. Fields empty for good. See [Natural Gas](Natural-Gas). |
| <img src="images/items/gas_flare.png" width="32" alt=""> **Gas Flare** | Burns surplus fuel gas (up to 500 mB/t) without using it. |

**Combined cycle:** half of the Gas Turbine's fuel heat leaves as hot exhaust through its HEAT ports. Put a Heat Port
of the turbine directly against a Heat Port of an Industrial Boiler and the exhaust drives a steam cycle as well. The
Gas Engine's exhaust works the same way.

**Natural gas** carries twice the heat of syngas (8 HU/mB in the Gas Turbine and Gas Engine, 2 HU/mB in the Industrial
Boiler). **Oxyfuel:** with oxygen from the Electrolyzer (1 mB per 2 mB of fuel), the Gas Turbine, Gas Engine and
Industrial Boiler get 25 % more heat from their gas ([details](Energy-Fluids-Gases#oxyfuel)).

---

## 7. Renewables

| Plant | Notes |
|---|---|
| **[Solar Array](Build-Solar-Array)** | PV Modules connected to the controller, 6 E/t each in full sun, nothing at night. |
| **[Solar Thermal](Build-Solar-Thermal)** | Heliostats focus sunlight on a Solar Receiver: 8 HU/t each in full direct sun, delivered through HEAT ports. |
| **[Wind Turbine](Build-Wind-Turbine)** | 2–4 equal blade arms, 1–3 Wind Generators (200 E/t each), a tower of at least 4 segments. Higher hubs see more wind; storms stop it. |
| <img src="images/items/thermoelectric_generator.png" width="32" alt=""> **Thermoelectric Generator**, **Stirling Generator**, **Geothermal Heat Exchanger** | Single blocks that use hot and cold blocks around them; see [Machines](Machines). |

---

## 8. Storage

| Store | Character |
|---|---|
| <img src="images/items/energy_cell.png" width="32" alt=""> **Energy Cell** | Single block, 1,000,000 E, 2,000 E/t. |
| **[Capacitor Bank](Build-Capacitor-Bank)** | 25,000 E per Capacitor Module, the same amount per tick in and out; loses 0.2 % per second; redstone control. |
| **[Battery Hall](Build-Battery-Hall)** | 8,000,000 E per Battery Cell; rate set by the Inverters; gets warm under load. |
| **[Molten-Salt Store](Build-Molten-Salt-Store)** | Stores heat, not energy: Thermal Salt (liquid 290–565 °C) and/or Thermal Concrete, through HEAT ports. |
| **[Gravity Store](Build-Gravity-Store)** | Gravity Weights lifted by Gravity Winches in a shaft up to 64 blocks high; 90 % each way, no self-discharge. |
| **[SMES](Build-SMES)** | 50,000,000 E per Superconducting Coil and 250,000 E/t per Power Converter, once cooled below 9 K with helium and Cryocoolers. |
| **[Large Gas Tank](Build-Large-Gas-Tank)** | Gas, not energy: 64,000 mB per interior block of a box from 3x3x3 to 32x32x32. |

---

## 9. Fission

The nuclear fuel chain:

1. **Crusher:** Raw Uranium (or uranium ore) → 2 Uranium Dust.
2. **Chemical Processor:** Uranium Dust + 250 mB water → Yellowcake.
3. **[Centrifuge Cascade](Build-Centrifuge-Cascade)** (from 3×4×4, at least 2 Gas Centrifuges): 4 Yellowcake →
   1 Enriched Uranium + 3 Depleted Uranium. A batch needs 2,400 separative work; each Gas Centrifuge does 1 per tick
   for 40 E. More centrifuges are faster, never more product.
4. **Fuel Fabricator:** Enriched Uranium → 4 Uranium Fuel Pellets; 4 pellets + 1 Empty Fuel Rod → Uranium Fuel Rod.

The **[Fission Reactor](Build-Fission-Reactor)** (from 5×5×5, up to 15) holds Fuel Assemblies, Control Rods (in
columns up to the top interior layer, one per 4 assemblies), Graphite Moderators and Coolant Channels. Each fuel rod
holds 10,000,000 HU. Cooling water goes in, Hot Coolant comes out; a **Heat Exchanger** turns it into steam for a
Steam Turbine. Add Reactor Instrumentation for the automatic SCRAM.

**Radiation:** from here on, running plants radiate (fission, fusion, Little Star and the black hole plants). Wall
the plant in with lead blocks (Block of Lead, Lead Concrete, Lead Glass) and wear the radiation suit when you work
close to it. Reinforced Concrete and Reinforced Glass protect against incidents. Details:
[Safety and Incidents](Safety-and-Incidents#radiation).

---

## 10. Fusion

The **[Tokamak](Build-Tokamak)** (from 11×5×11, square footprint with odd edge) burns deuterium and tritium.
Deuterium comes from the **Isotope Separator** (hydrogen → deuterium); tritium is bred in Breeding Blankets from
Lithium Carbonate. Starting the plasma needs 800,000,000 E of startup energy. Heat leaves through HEAT ports and/or as
Hot Coolant.

---

## 11. Little Star

The **[Little Star](Build-Little-Star)** is an odd cube of edge 9 or more with six Containment Rods that hold a small
artificial star. It burns hydrogen into helium and delivers electricity directly: 1,000 E per mB of hydrogen. Igniting
it takes 2,000,000,000 E, and the rods keep drawing energy through the Energy Input Ports while it burns.

---

## 12. Black hole plants and the dimensional store

* **[Micro Black Hole Plant](Build-Singularity-Plant)** – odd cube of edge 9 or more. Fed with Compressed Matter
  (Matter Compressor: 8 blocks of stone, dirt, sand and similar → 1 Compressed Matter = 1 mass unit). Forming the
  singularity takes 10,000,000,000 E. It can split off **Singularity Capsules**.
* **[Hawking Reactor](Build-Hawking-Reactor)** – odd cube of edge 7 or more; starts from a Singularity Capsule (and
  100,000,000 E), is fed Compressed Matter and makes power from the evaporation of its tiny singularity.
* **[Dimensional Store](Build-Dimensional-Store)** – odd cube of edge 5 or more around a Dimension Core. Opening the
  pocket costs 50,000,000,000 E once; it holds 10^15 E.

Before you build anything that can fail, read [Safety and Incidents](Safety-and-Incidents). Computers can watch and
control most plants: [ComputerCraft](ComputerCraft).

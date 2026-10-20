# Natural Gas

Natural Gas (since 0.2.0) is a fuel gas you do not make but extract: from natural gas fields deep below the world,
with a **Gas Derrick**. You find the fields with the **Gas Prospector**. Natural gas carries twice the heat of syngas,
but every field runs dry for good.

Numbers are the defaults of the [server configuration](Configuration#natural-gas).

---

## Gas fields

The world is divided into **regions of 128 × 128 blocks** (8 × 8 chunks), counted from block 0: one region runs from
x 0 to 127, the next from 128 to 255, the one to the west from −128 to −1, and the same along z. A region holds at most
one field, over its full height.

| Field | Share of the regions | Content | Highest rate |
|---|---|---|---|
| none | about 60 % | – | – |
| **Small field** | 32 % (`naturalGasSmallFieldChance`) | 5 – 15 million mB | 120 mB/t |
| **Large field** | 8 % (`naturalGasLargeFieldChance`) | 50 – 150 million mB | 480 mB/t |

* **Nothing is generated in the world.** Whether a region has a field, which kind and how much it holds follows from
  the world seed, the dimension and the region's position alone. No blocks are placed and no chunks are searched, so
  the fields work with every world generation mod, and the same seed always gives the same fields.
* **Dimensions:** only the Overworld has natural gas (`naturalGasDimensions`). In every other dimension (the Nether,
  the End, dimensions of other mods) there is none unless the server adds it to that list.
* **Content and rate** can be scaled with `naturalGasFieldSizeMultiplier` and `naturalGasFieldRateMultiplier`.

### Pressure and depletion

A field gives the most at the start. Its rate falls in a straight line with what is left, down to a quarter of the
highest rate, and stays there until the field is empty:

rate = highest rate × (0.25 + 0.75 × share left)

| Share left | Small field | Large field |
|---|---|---|
| 100 % | 120 mB/t | 480 mB/t |
| 50 % | 75 mB/t | 300 mB/t |
| almost empty | 30 mB/t | 120 mB/t |
| empty | 0 | 0 |

* **Fields empty for good.** An empty field never refills. Breaking or rebuilding a derrick changes nothing: what was
  taken from each region is kept in the world's save data (per dimension), not in the derrick.
* **One field, one rate.** Every derrick in the same region takes from the same field rate. Two derricks on one field
  share it; they do not double it.
* If the server changes the natural gas options later, the fields change with them (they are calculated, not stored).
  What was already taken from a region stays taken.

---

## <img src="images/items/gas_prospector.png" width="32" alt=""> Gas Prospector

A hand tool (no energy, never used up). **Right-click any block** with it; it reports the field of the region that
block lies in, as chat messages:

| Line | Example meaning |
|---|---|
| *Small field here: 87.5 % left (…), … now* | Kind of the field, the share and amount left, and the field's rate right now (shared by all derricks of the region). |
| *No natural gas in this region* | This region has no field. |
| *Nearest other field: north-east* | The direction of the nearest field among the 8 neighbouring regions (a region straight north, south, east or west wins over a diagonal one). |
| *No field in the neighbouring regions either* | Neither this region nor its 8 neighbours has a field. |
| *Region from x, z to x, z* | The corners of the current region, so you know where its field ends. |
| *There is no natural gas in this dimension* | The dimension is not in `naturalGasDimensions`. |

The prospector only calculates; it reads nothing in the world and looks no further than the neighbouring regions.
Finding a field with it earns the advancement *Under Your Feet* (see [Advancements](Advancements)). Recipe: compass,
iron ingots and redstone ([Recipes](Recipes)).

---

## Gas Derrick

The Gas Derrick is a lattice tower that extracts natural gas from the field of its region (the region of its
controller). How to build it, layer by layer: **[Build the Gas Derrick](Build-Gas-Derrick)**.

* **Size:** 3 × 3 wide, **6 to 12 blocks high**. In the middle stands the mast: a Wellhead directly above the floor,
  Drill Pipe above it up to the roof. Derrick Frame everywhere else.
  While the derrick extracts, the drill string turns (20–60 rpm, faster at a higher rate; since 1.0.0).
* **Ports:** Gas Output Port (natural gas out, pulled by Pipster gas pipes) and Energy Input Port. An Inspection Hatch
  may go in a face as well.
* **Rate:** a derrick extracts at most its own capacity, which grows with its height, and never more than the field's
  current rate:

| Height | 6 | 7 | 8 | 9 | 10 | 11 | 12 |
|---|---|---|---|---|---|---|---|
| Derrick capacity (mB/t) | 60 | 100 | 140 | 180 | 220 | 260 | 300 |

* **Energy:** 0.5 E per mB (1 E for every 2 mB, rounded up each tick), so 150 E/t at 300 mB/t.
* **Buffers:** 32,000 mB of natural gas, 20,000 E (up to 2,000 E/t in).
* While it extracts, a small flame burns at the top of the tower (client option `flowEffects`). The derrick has no
  incidents.

The screen (controller, port or Inspection Hatch) shows the state, the field, *Field content* (what is left),
*Field pressure* (the share left), *Field rate* (shared by the region), *Derrick capacity*, *Extraction* (what it took
in the last tick) and the gas and energy buffers.

| State | Meaning |
|---|---|
| Extracting | Running. |
| No natural gas in this region | The controller's region has no field (or the dimension has none). Move the derrick; the prospector shows where. |
| Field depleted | The field is empty for good. |
| Output full | The gas buffer is full: pipe the gas away. |
| No energy | Feed energy into the Energy Input Port. |

Jade shows the screen values, and CC: Tweaked computers read them with `getInfo()` (see [ComputerCraft](ComputerCraft)).

---

## Where natural gas burns

| Machine | Heat of natural gas | With oxyfuel | For comparison |
|---|---|---|---|
| [Gas Turbine](Build-Gas-Turbine) | 8 HU/mB | 10 HU/mB | Hydrogen 6, Syngas 4 HU/mB |
| [Gas Engine](Build-Gas-Engine) | 8 HU/mB: 31.25 mB/t per cylinder at full load (80 E/t at 32 % efficiency) | 25 mB/t per cylinder | Syngas needs 62.5 mB/t per cylinder |
| [Industrial Boiler](Build-Industrial-Boiler) | 2 HU/mB | 2.5 HU/mB | Syngas 1 HU/mB |

* The Industrial Boiler takes natural gas through its Gas Input Port into the same tank as syngas (screen label
  *Fuel gas*, 16,000 mB), one gas at a time. Like syngas it only tops up: solid fuel in the fuel slots burns first.
* The Gas Engine does not knock on natural gas (only hydrogen does).
* The Gas Compressor compresses natural gas too (2 E per mB): compressed natural gas gives 10 HU/mB in the Gas Turbine.
* Oxyfuel (burning with oxygen for 25 % more heat) works with natural gas like with every fuel gas: see
  [Energy, Fluids and Gases](Energy-Fluids-Gases#oxyfuel).
* Surplus natural gas can be stored in a Gas Tank or [Large Gas Tank](Build-Large-Gas-Tank), burned without use in a
  [Gas Flare](Machines#gas-flare) or released with an Emergency Vent.

## Balance notes

* **Turbine blades:** a Rotor Blade of the Gas Turbine passes at most 450 E/t to the shaft. Natural gas brings twice
  the heat of syngas per mB, so a turbine built for syngas reaches this limit much sooner. Shaft power above the limit
  is lost (the exhaust heat stays half of the fuel heat). To use natural gas fully, build more Rotor Blades or turn the
  fuel setpoint down.
* **Extraction pays:** 0.5 E per mB against 8 HU of heat per mB.
* **One derrick or two:** a full-height derrick (300 mB/t) cannot take all of a fresh large field (480 mB/t); two
  derricks in the region can. For a small field (120 mB/t) a derrick of height 8 (140 mB/t) is enough.
* **Finite:** a small field holds 40 to 120 million HU of heat. One coal through the Gasifier gives 34,000 mB of
  syngas = 136,000 HU, so a small field is worth roughly 290 to 880 coal, a large field ten times as much.
* Natural gas gives no helium; helium still comes only from the Tokamak and the Little Star.

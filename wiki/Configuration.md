# Configuration

QuantaVolt uses two plain `.properties` files, the same format on Fabric and NeoForge and on every game version.

| File | Side | Read |
|---|---|---|
| `config/quantavolt-server.properties` | server (also the integrated server of a singleplayer world) | when the server starts, before the worlds load |
| `config/quantavolt-client.properties` | client | once when the game starts |

`config/` is the loader's config folder in the game or server directory (Fabric: the Fabric Loader config directory,
NeoForge: the FML config directory).

* A missing file means all defaults. After reading, QuantaVolt writes the file back with every key, a comment and the
  default and range of each entry.
* A value that is not a valid number or lies outside its range falls back to the default; the log says so.
* Whole numbers may contain underscores (`800_000_000`). Unknown keys are ignored.
* Changes take effect the next time the server (or, for the client file, the game) starts. There are no in-game
  commands for the configuration.
* All gameplay rules are decided by the server file. The client file changes only visuals.

---

## Server options

### Output and fuel

| Key | Default | Range | Meaning |
|---|---|---|---|
| `generatorOutputMultiplier` | 1.0 | 0.01 – 100.0 | Multiplier for the energy output of every generator and turbine |
| `fuelConsumptionMultiplier` | 1.0 | 0.01 – 100.0 | Multiplier for fuel consumption (higher = fuel lasts shorter) |
| `basicDynamoOutput` | 40 | 1 – 100,000 | Energy per tick of a burning Basic Dynamo (E/t) |
| `stirlingMaxOutput` | 100 | 1 – 100,000 | Largest electrical output of a Stirling Generator (E/t) |
| `solarModuleOutput` | 6 | 1 – 10,000 | Energy per tick of one PV Module in full sun (E/t) |
| `heliostatHeat` | 8 | 1 – 10,000 | Heat per tick of one Heliostat in full direct sun (HU/t) |
| `windPowerFactor` | 10.0 | 0.01 – 1,000.0 | K in the wind turbine power K × rotor area × wind³ × Cp (E/t) |

### Start and capacity energies

| Key | Default | Range | Meaning |
|---|---|---|---|
| `fusionStartupEnergy` | 800,000,000 | 1,000 – 100,000,000,000 | Energy a Tokamak needs to reach ignition (E) |
| `littleStarIgnitionEnergy` | 2,000,000,000 | 1,000 – 1,000,000,000,000 | Energy a Little Star needs to ignite (E) |
| `singularityIgnitionEnergy` | 10,000,000,000 | 1,000 – 10,000,000,000,000 | Energy a Micro Black Hole Plant needs to form its singularity (E) |
| `energyPerMassUnit` | 10,000,000 | 1,000 – 1,000,000,000,000 | Energy of one mass unit (one Compressed Matter) in the singularity technology (E) |
| `dimensionOpenEnergy` | 50,000,000,000 | 1,000 – 10,000,000,000,000 | Energy that opens the pocket of a Dimensional Store (E) |
| `dimensionCapacity` | 1,000,000,000,000,000 | 1,000,000 – 4,000,000,000,000,000,000 | Capacity of a Dimensional Store (E) |
| `batteryCellCapacity` | 8,000,000 | 1,000 – 1,000,000,000 | Energy one Battery Cell of a Battery Hall stores (E) |
| `gravityEnergyPerWeightBlock` | 20,000 | 100 – 10,000,000 | Energy a Gravity Store holds per weight and block of lift height (E) |
| `smesCoilCapacity` | 50,000,000 | 1,000 – 100,000,000,000 | Energy one Superconducting Coil of an SMES stores (E) |

### Structure limits

These limits bound how much work checking a structure can take.

| Key | Default | Range | Meaning |
|---|---|---|---|
| `maxStructureSize` | 16 | 5 – 32 | Largest edge length of any multiblock |
| `maxFissionReactorSize` | 15 | 5 – 32 | Largest edge length of a Fission Reactor |
| `maxSolarModules` | 256 | 1 – 4,096 | Most PV Modules one Solar Array Controller collects |
| `maxHeliostats` | 512 | 1 – 4,096 | Most Heliostats one Solar Receiver collects |
| `maxCapacitorModules` | 128 | 1 – 1,024 | Most Capacitor Modules one Capacitor Bank Controller collects |
| `maxWindBladeLength` | 8 | 2 – 16 | Longest wind turbine rotor arm (blocks) |
| `minWindTowerHeight` | 4 | 1 – 64 | Fewest tower segments (including ports) below a wind turbine nacelle |

Plants with a fixed minimum size are always allowed at that size, even if `maxStructureSize` is smaller (Little Star
and Micro Black Hole Plant 9, Hawking Reactor 7, Dimensional Store 5). The Gravity Store shaft may be up to 64 blocks
high regardless of `maxStructureSize`; its width and depth follow `maxStructureSize`. A Gas Engine has at most 8
cylinders.

### Natural gas

The [natural gas fields](Natural-Gas) are not stored in the world but calculated from the seed with these options, so
changing them changes the fields of the whole world, also where players have already found or tapped them. What was
already taken from a region stays taken.

| Key | Default | Range | Meaning |
|---|---|---|---|
| `naturalGasDimensions` | `minecraft:overworld` | list of dimension ids | Dimensions with natural gas fields (comma-separated ids; empty = none) |
| `naturalGasSmallFieldChance` | 0.32 | 0.0 – 1.0 | Share of 128x128 regions with a small natural gas field |
| `naturalGasLargeFieldChance` | 0.08 | 0.0 – 1.0 | Share of 128x128 regions with a large natural gas field (small + large at most 1) |
| `naturalGasFieldSizeMultiplier` | 1.0 | 0.01 – 100.0 | Multiplier for the content of natural gas fields (small 5–15 million mB, large 50–150 million mB) |
| `naturalGasFieldRateMultiplier` | 1.0 | 0.01 – 100.0 | Multiplier for the highest extraction rate of natural gas fields (small 120 mB/t, large 480 mB/t) |

If the two chances add up to more than 1, large fields are decided first and small fields get the rest. Contents are
rounded to whole 1,000 mB (at least 1,000 mB), rates to whole mB/t (at least 1 mB/t).

### Safety

| Key | Default | Meaning |
|---|---|---|
| `safeMode` | `false` | Only overheating and immediate shutdown: no explosions, no damage to entities or blocks. Also keeps the turbines' overspeed trip and the Battery Hall's thermal disconnect on. |
| `incidentTerrainDamage` | `false` | Whether severe incidents (bursts, meltdowns, breaches) destroy blocks (only without `safeMode`) |
| `radiation` | `true` | Running nuclear plants, meltdowns and radiation flashes irradiate living beings nearby (see [Radiation](Safety-and-Incidents#radiation)). Off in `safeMode`. |

Details on what each incident does: [Safety and Incidents](Safety-and-Incidents).

**Older keys:** files from earlier versions may still contain `explosionDamage` or `meltdownTerrainDamage`. If the new
key is missing, the old value is taken over (`explosionDamage=false` becomes `safeMode=true`, `explosionDamage=true`
becomes `safeMode=false`; `meltdownTerrainDamage` becomes `incidentTerrainDamage`) and the log notes it once.

---

## Client options

| Key | Default | Range | Meaning |
|---|---|---|---|
| `particleDensity` | 1.0 | 0.0 – 4.0 | Multiplier for particles of turbines, reactors and the Tokamak (0 = off) |
| `incidentEffects` | `true` | – | Show incident effects and warning signs (steam, sparks, smoke, frost) at plants |
| `interiorEffects` | `true` | – | Show life inside plants behind sight glass (embers, steam, glints, frost) |
| `flowEffects` | `true` | – | Show what leaves plants (exhaust plumes, flue smoke) |

The client options never change gameplay: incidents happen the same way with the effects switched off.

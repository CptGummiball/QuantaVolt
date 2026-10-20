# Energy, Fluids and Gases

QuantaVolt has no cables, pipes or transport network of its own. Its machines and plant ports offer the standard
interfaces of the mod loader, so cables, pipes and tanks of other mods can connect to them. The one exception is gas:
neither loader has a gas interface, so gases use the gas system of the required mod **Pipster**.

---

## Units

| Quantity | Unit | Notes |
|---|---|---|
| Energy | **E** | 1 E = 1 FE (NeoForge Forge Energy) = 1 Team Reborn Energy unit (Fabric). Rates in E/t (per tick, 20 ticks = 1 second). |
| Fluids | **mB** | 1,000 mB = 1 bucket. On Fabric only whole mB are moved (81 droplets each). |
| Gases | **mB** | Pipster's gas system (`pipster:gas`). |
| Heat | **HU** | QuantaVolt's own heat unit. 1 HU boils 1 mB of steam. Heat moves only between QuantaVolt blocks. |
| Temperature | °C | Plasma and star core temperatures in MK (million kelvin), SMES coils in K. |
| Mass | ME | Mass unit of the black hole plants; 1 Compressed Matter = 1 ME. |

---

## Energy

* Interfaces: Team Reborn Energy on Fabric (bundled with QuantaVolt), the energy capability (FE) on NeoForge.
* **Generators push.** These blocks send energy into their neighbors on their own: Basic Dynamo (all sides), Energy
  Cell (front), Energy Transformer (front), Thermoelectric and Stirling Generator (all sides), Electrolyzer in fuel
  cell mode (all sides), Solar Array Controller (all sides) and every **Energy Output Port** of a formed plant.
  Pipster cables accept this push when their port is set to *Extract* or *Both*.
* Machines that need energy accept it on their input sides (see [Machines](Machines)); plants take it through
  **Energy Input Ports**.
* Simulated transfers never change anything, and transfers never move more than requested.

---

## Ports

Plants connect to the outside only through their ports. A port works only on its **outer face** and only while the
plant is **formed**. Each plant accepts only certain port types; the screen tells you when a port is not allowed.

| Plant | Item | Fluid | Gas | Energy | Heat |
|---|---|---|---|---|---|
| Industrial Boiler | in: fuel | in: water · out: Steam | in: Syngas or Natural Gas, Oxygen | – | in |
| Steam Turbine | – | in: Steam · out: Exhaust Steam | – | out | – |
| Gasifier | in: fuel · out: Ash | in: Steam | out: Syngas | – | – |
| Gas Turbine | – | – | in: Hydrogen, Syngas or Natural Gas (all also compressed), Oxygen | out | out |
| Gas Engine | – | in: water · out: Hot Coolant | in: Hydrogen, Syngas or Natural Gas, Oxygen | out | out |
| Gas Derrick | – | – | out: Natural Gas | in | – |
| Centrifuge Cascade | in: Yellowcake · out: Enriched / Depleted Uranium | – | – | in | – |
| Fission Reactor | in: Uranium Fuel Rods · out: Depleted Fuel Rods | in: water · out: Hot Coolant | – | – | – |
| Tokamak | in: Lithium Carbonate | in: water · out: Hot Coolant | in: Deuterium, Tritium · out: Helium, Tritium | in | out |
| Little Star | – | in: water · out: Steam | in: Hydrogen · out: Helium | in and out | out |
| Battery Hall | – | in: water · out: Hot Coolant | – | in and out | – |
| Capacitor Bank, Gravity Store, Dimensional Store | – | – | – | in and out | – |
| Molten-Salt Store | – | – | – | – | in and out |
| SMES | – | – | in and out: Helium | in and out | out (dump heat) |
| Micro Black Hole Plant | in: Compressed Matter · out: Singularity Capsules | in: water · out: Hot Coolant | – | in and out | – |
| Hawking Reactor | in: Compressed Matter, Singularity Capsule | in: water · out: Hot Coolant | – | in and out | – |
| Wind Turbine | – | – | – | out (ports in the tower) | – |
| Solar Thermal (Solar Receiver) | – | – | – | – | out |
| Large Gas Tank | – | – | in and out: any one gas | – | – |

The Solar Array has no ports: its controller pushes energy into all neighbors.

---

## Fluids

| Fluid | Made by | Used by |
|---|---|---|
| Water (vanilla) | Pump, Condenser, Heat Exchanger (primary return), Electrolyzer in fuel cell mode | Boilers, coolant loops, Chemical Processor, Electrolyzer |
| **Steam** | Industrial Boiler, Heat Exchanger, Geothermal Heat Exchanger, Little Star (shell cooling) | Steam Turbine, Gasifier |
| **Exhaust Steam** | Steam Turbine (1 mB per mB of steam used) | Condenser (10 mB → 1 mB water), Emergency Vent |
| **Hot Coolant** | Fission Reactor, Tokamak, Gas Engine, Battery Hall, Micro Black Hole Plant, Hawking Reactor | Heat Exchanger (10 HU per mB) |

* Steam, Exhaust Steam and Hot Coolant are real registered fluids, so any fluid pipe or tank can carry them. They
  exist only in tanks and pipes: no bucket, no fluid block in the world.
* Steam is in the tag `c:steam`. Every QuantaVolt steam input accepts the tag `quantavolt:steam`, which also includes
  `c:steam`, so steam from other mods works too.
* 1 mB water becomes 10 mB steam (boilers, Heat Exchanger, Geothermal Heat Exchanger).
* **Closed water loop:** Boiler → Steam → Steam Turbine → Exhaust Steam → Condenser → water → Boiler.
* **Reactor loop:** Reactor → Hot Coolant → Heat Exchanger → water back to the reactor. The Heat Exchanger keeps this
  primary water separate from the feedwater it boils into steam.

---

## Gases

All gases live only in Pipster's gas system, in mB. They are not fluids and cannot go into fluid pipes or tanks; use
Pipster's gas pipes and the **Gas Tank**. Mekanism chemicals are not compatible.

| Gas | Made by | Used by |
|---|---|---|
| **Hydrogen** | Electrolyzer | Gas Turbine (6 HU/mB), Gas Engine, Isotope Separator, Little Star (1,000 E per mB), Electrolyzer in fuel cell mode |
| **Oxygen** | Electrolyzer | Electrolyzer in fuel cell mode; Gas Turbine, Gas Engine and Industrial Boiler for [oxyfuel](#oxyfuel) |
| **Syngas** | Gasifier | Gas Turbine (4 HU/mB), Gas Engine, Industrial Boiler (1 HU/mB) |
| **Natural Gas** | Gas Derrick, from natural gas fields ([Natural Gas](Natural-Gas)) | Gas Turbine (8 HU/mB), Gas Engine, Industrial Boiler (2 HU/mB) |
| **Deuterium** | Isotope Separator | Tokamak fuel |
| **Tritium** | Tokamak (bred from lithium in the Breeding Blankets) | Tokamak fuel; surplus leaves through the gas output |
| **Helium** | Tokamak (divertors), Little Star (the star's ash) | SMES (cooling charge) |

**Compressed gas:** the Gas Compressor turns Hydrogen, Syngas or Natural Gas into a compressed form of the same gas (2 E per mB).
Only the Gas Turbine benefits: hydrogen gives 7 instead of 6 HU/mB, syngas 5 instead of 4 HU/mB. The Gas Engine, the
Industrial Boiler and the Isotope Separator accept only uncompressed gas. Pipster stores both forms separately.

Gases a plant cannot get rid of can be dumped with an **Emergency Vent** (2,000 mB/t, any gas, released unburnt) or
burned with a **Gas Flare** (up to 500 mB/t, only gases that burn: Hydrogen, Syngas and Natural Gas, compressed
forms too; no energy gained). See [Machines](Machines#gas-flare).

### Oxyfuel

The Gas Turbine, the Gas Engine and the Industrial Boiler can burn their fuel gas with **Oxygen** instead of air. Each
has its own oxygen tank (16,000 mB), filled through the same Gas Input Ports as the fuel. The screen line
*Oxygen (oxyfuel +25 %)* shows it.

* **1 mB of oxygen per 2 mB of fuel gas** (rounded up) gives **25 % more heat** from the same gas.
* The oxygen for the fuel of a tick must be in the tank; if it is not, that tick burns with air as before (no bonus,
  no oxygen used).

| Machine | Effect | Heat per mB with oxyfuel |
|---|---|---|
| Gas Turbine | Same fuel flow, 25 % more heat: more shaft power (up to the blade limit) and more exhaust heat | Hydrogen 7.5, Syngas 5, Natural Gas 10 HU/mB; compressed Hydrogen 8.75, compressed Syngas 6.25, compressed Natural Gas 12.5 HU/mB |
| Gas Engine | Same power from 80 % of the fuel | Hydrogen 7.5, Syngas 5, Natural Gas 10 HU/mB |
| Industrial Boiler | The same heat from fewer mB of gas | Syngas 1.25, Natural Gas 2.5 HU/mB |

Oxygen comes from the Electrolyzer (5 mB with every 10 mB of hydrogen), so the oxygen left over from making hydrogen
for the Tokamak or the Little Star becomes useful. Oxyfuel is no energy loop: electrolysis costs 100 E for 10 mB of
hydrogen and 5 mB of oxygen, and burning that hydrogen with oxyfuel gives 75 HU.

---

## Heat (HU) and HEAT ports

Heat is QuantaVolt's own resource. It has no loader interface and does not travel through pipes: a heat source hands
it, once per tick, to the heat receiver **directly touching** its HEAT port (or the front of an Electric Heater). Put
the Heat Ports of two plants face to face, or a Stirling Generator against a Heat Port.

| Heat sources (give heat) | Heat receivers (take heat) |
|---|---|
| Gas Turbine – 50 % of the fuel heat as exhaust | Industrial Boiler – up to 40 HU/t per Heat Exchanger Tube |
| Gas Engine – 60 % of its waste heat as exhaust | Molten-Salt Store – up to 100 HU/t per Heat Exchanger Tube |
| Tokamak – blanket and divertor heat | Stirling Generator – up to 240 HU/t |
| Little Star – heat of its shell | |
| Molten-Salt Store – up to its output setpoint (100 HU/t per tube) | |
| SMES – dump heat of a controlled quench | |
| Solar Receiver – heat of the heliostats | |
| Electric Heater (front) – 0.9 HU per E, up to 400 HU/t | |

What happens to heat nobody takes:

* Gas Turbine and Gas Engine exhaust goes up the stack (you see the plume).
* The Solar Receiver has no buffer: its heat is lost.
* The Electric Heater keeps it as energy.
* The Tokamak collects heat in a buffer and can also hand it out as Hot Coolant.

### Combined cycle

1. A Gas Turbine burns hydrogen, syngas or natural gas. Up to 45 % of the fuel heat turns the rotor (less when the rotor is far from its rated
   3,600 rpm); 50 % always leaves as exhaust heat.
2. A Heat Port of the Gas Turbine touches a Heat Port of an Industrial Boiler. The exhaust heat boils water in the
   boiler (no fuel needed).
3. The boiler's steam drives a Steam Turbine.

The Gas Engine works the same way with its exhaust; the rest of its waste heat goes into its cooling water as Hot
Coolant, which a Heat Exchanger can turn into steam as well.

The boiler takes no more outside heat than its tubes can boil. If its steam cannot leave, the heat still builds up:
see *Overpressure* on [Safety and Incidents](Safety-and-Incidents).

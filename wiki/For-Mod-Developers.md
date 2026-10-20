# For Mod Developers

API version **1** · package `dev.cptgummiball.quantavolt.api` · mod id `quantavolt`

**Most mods need nothing from this page:** QuantaVolt's machines use the standard interfaces of the loader, so pipes,
cables and logistics mods work with them directly.

## Getting the API

`quantavolt-api-1.jar` and `quantavolt-api-1-javadoc.jar` are attached to the GitHub release of the API. Use them as a
**compile-only** dependency. Do not ship the API or any QuantaVolt files in your mod. If QuantaVolt is optional for your
mod, check that the mod `quantavolt` is loaded before touching its classes. Compiling against the API and publishing
mods that use it is allowed by the [license](License-and-Permissions).

## How QuantaVolt talks to other mods

QuantaVolt has **no own transport API**. Every machine exposes the standard interfaces of the
loader, so Pipster and every other logistics mod can work with it. Only gases use Pipster's gas
API, because neither loader has a gas interface.

## Interfaces per version family

| Resource | Fabric (1.21.1 – 26.3) | NeoForge 1.21.1 – 1.21.8 | NeoForge 1.21.9 – 26.3 |
|---|---|---|---|
| Items | `ItemStorage.SIDED` (vanilla `WorldlyContainer` through `InventoryStorage`) | `Capabilities.ItemHandler.BLOCK` (`SidedInvWrapper`) | `Capabilities.Item.BLOCK` (`ResourceHandler<ItemResource>`) |
| Fluids | `FluidStorage.SIDED`, droplets; only whole mB (81 droplets) are moved | `Capabilities.FluidHandler.BLOCK`, mB | `Capabilities.Fluid.BLOCK` (`ResourceHandler<FluidResource>`), mB |
| Energy | Team Reborn Energy `EnergyStorage.SIDED` (bundled as jar-in-jar) | `Capabilities.EnergyStorage.BLOCK` (FE) | `Capabilities.Energy.BLOCK` (`EnergyHandler`, FE) |
| Gas | Pipster `GasHandler` via `BlockApiLookup` id `pipster:gas_handler` | Pipster `GasHandler` via `BlockCapability` id `pipster:gas_handler` | as 1.21.1 – 1.21.8 |

All three families are covered by the automated game tests of every released file.

## Conventions

* **Units:** 1 E = 1 FE = 1 Team Reborn Energy unit. Fluids and gases in mB.
* **Energy push:** generators (Basic Dynamo, Energy Cell front, energy output ports) actively push
  into neighbours, as the Fabric energy convention and Pipster on Fabric expect. Pipster cables
  accept the push when their port is set to *Extract* or *Both*.
* **Directions:** machine inputs are insert-only, outputs extract-only. Multiblock ports expose their
  interface only on the side facing out of the structure, and only while the structure is formed.
* **Simulation:** simulations never change state; results never exceed the request; extraction
  removes only the exact resource (id + components).
* **Gases:** `quantavolt:hydrogen`, `oxygen`, `syngas`, `deuterium`, `tritium`, `helium` exist only
  in the `pipster:gas` domain (unit mB). They are not fluids and not in `#pipster:gaseous`.
* **Steam:** `quantavolt:steam` is a normal fluid (also in `#c:steam`). QuantaVolt machines accept
  every fluid of `#quantavolt:steam`, which includes `#c:steam` of other mods.
* **Mekanism chemicals** are not compatible (Pipster has no general adapter).

## Stability

`QuantaVoltApi.API_VERSION` changes with every incompatible change of
`dev.cptgummiball.quantavolt.api`. Everything else is internal.

## Computers

Machines are CC: Tweaked peripherals when CC: Tweaked is installed: see [ComputerCraft](ComputerCraft).

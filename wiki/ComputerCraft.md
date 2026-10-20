# ComputerCraft

When **CC: Tweaked** is installed, QuantaVolt machines and plant controllers become peripherals. Without CC: Tweaked
nothing of this is loaded.

* **Peripheral type:** `quantavolt` (find it with `peripheral.find("quantavolt")`).
* **Where:** place the computer or a wired modem directly against the machine, or against the **controller** of a
  plant (ports and other wall parts have no readings).
* Every method runs on the server thread.
* Write methods check the machine, the command and every argument on the server. If something does not fit, they
  raise a Lua error and change nothing; values are never silently clamped. Use `pcall` if you want to catch the error.

---

## Reading methods (every machine)

| Method | Returns |
|---|---|
| `getInfo()` | Table of every value of the machine's screen, keyed by the screen label, plus `type` (screen id) and, for plants, `formed` (boolean). Bars also give `<label>Max`. State lines are translation keys (e.g. `gui.quantavolt.turbine.running`). |
| `getReadings()` | Table of all the readings below that this machine has. |
| `getCommands()` | List of the write commands this machine accepts. |
| `temperature()`, `powerOutput()`, `energyStored()`, `fuelLevel()`, `turbineRpm()`, `reactorFlux()`, `controlRodPosition()`, `plasmaTemperature()`, `stability()`, `alarmState()`, `coolantTemperature()`, `steamFlow()`, `netPower()`, `fusionRate()`, `tritiumBreedingRate()`, `reactorState()`, `windSpeed()`, `heatStored()`, `coilTemperature()`, `singularityMass()` | One reading. A reading the machine does not have raises the error `this machine has no reading '…'`. |

### Readings per machine

| Machine | Readings |
|---|---|
| Basic Dynamo | `powerOutput` (E/t), `energyStored` (E), `fuelLevel` (burn ticks left) |
| Energy Cell | `energyStored` |
| Pump, Energy Transformer, Crusher, Chemical Processor, Fuel Fabricator, Matter Compressor, Centrifuge Cascade | `energyStored` |
| Electrolyzer | `powerOutput` (E/t in fuel cell mode), `energyStored` (input buffer; output buffer in fuel cell mode), `reactorState` (`electrolysis`, `fuel_cell`) |
| Thermoelectric Generator | `powerOutput`, `energyStored` |
| Stirling Generator | `temperature` (hot head, °C), `coolantTemperature` (cold side, °C), `powerOutput`, `energyStored` |
| Heat Exchanger, Geothermal Heat Exchanger | `steamFlow` (mB/t) |
| Industrial Boiler | `temperature` (°C), `steamFlow` (mB/t), `fuelLevel` (fuel heat, HU) |
| Steam Turbine | `turbineRpm`, `powerOutput`, `energyStored`, `steamFlow` |
| Gas Turbine | `turbineRpm`, `powerOutput`, `energyStored`, `fuelLevel` (mB) |
| Gas Engine | `powerOutput`, `energyStored`, `fuelLevel` (mB), `temperature` (engine block, °C), `reactorState` (`stopped`, `starting`, `running`, `no_fuel`, `overheated`) |
| Solar Array | `powerOutput`, `energyStored` |
| Solar Receiver | `powerOutput` (heat delivered, HU/t) |
| Wind Turbine | `windSpeed` (% of the rated wind at the hub), `turbineRpm`, `powerOutput`, `energyStored`, `reactorState` (`calm`, `running`, `storm`, `no_wind`) |
| Capacitor Bank | `energyStored`, `powerOutput`, `temperature` (°C) |
| Battery Hall | `energyStored`, `powerOutput`, `temperature` (°C), `reactorState` (`idle`, `charging`, `discharging`, `hot`, `shutdown`) |
| Molten-Salt Store | `temperature` (°C), `heatStored` (HU usable above the freezing point), `powerOutput` (HU/t) |
| Gravity Store | `energyStored`, `powerOutput` |
| SMES | `energyStored`, `powerOutput`, `coilTemperature` (K; superconducting below 9 K), `fuelLevel` (helium, mB), `reactorState` (`warm`, `cooling`, `ready`, `warning`, `quench`) |
| Fission Reactor | `temperature` (core, °C), `coolantTemperature` (outlet, °C), `reactorFlux` (0 to about 1), `controlRodPosition` (% inserted), `powerOutput` (HU/t), `fuelLevel` (% left), `alarmState` (`normal`, `warning`, `overheating`, `coolant_problem`, `fuel_damage`, `severe_failure`), `reactorState` (`not_formed`, `no_fuel`, `shutdown`, `running`, `scrammed`, `failed`) |
| Tokamak | `plasmaTemperature` (MK), `stability` (0–1), `energyStored`, `powerOutput` (fusion power, HU/t), `netPower` (heat out minus magnets and auxiliary heating), `fusionRate` (mB/t), `tritiumBreedingRate` (mB/t), `fuelLevel` (deuterium + tritium, mB), `coolantTemperature` (blanket, °C), `alarmState` (last event: `none`, `manual_stop`, `fuel_starvation`, `instability`, `magnet_power`, `startup_energy`, `blanket_overheat`, `structure`), `reactorState` (`off`, `vacuum`, `magnets`, `injection`, `ignition`, `heating`, `stable`, `collapse`, `shutdown`) |
| Little Star | `temperature` (core, MK), `stability`, `energyStored` (output buffer), `powerOutput` (E/t), `netPower` (minus the rods' upkeep), `fuelLevel` (hydrogen, mB), `controlRodPosition` (%), `coolantTemperature` (shell, °C), `steamFlow` (mB/t), `alarmState` (`none`, `manual_stop`, `auto_fade`, `fuel_starvation`, `containment_power`, `instability`, `shell_overheat`, `structure`), `reactorState` (`off`, `charging`, `compression`, `ignition`, `burning`, `fading`, `breach`, `failed`) |
| Micro Black Hole Plant | `singularityMass` (ME), `stability`, `powerOutput`, `netPower` (minus containment), `energyStored` (output buffer), `fuelLevel` (matter, ME), `reactorState` (`off`, `charging`, `forming`, `running`, `shutdown`, `failed`), `alarmState` (`none`, `manual_stop`, `evaporated`, `containment_lost`, `no_matter`, `structure`) |
| Hawking Reactor | `singularityMass`, `stability`, `powerOutput`, `energyStored`, `fuelLevel` (matter, ME), `reactorState` (`empty`, `starting`, `running`, `shutdown`, `failed`), `alarmState` (`none`, `manual_stop`, `evaporated`, `no_matter`, `structure`, `overheat`) |
| Dimensional Store | `energyStored`, `powerOutput`, `stability` (link), `reactorState` (`closed`, `opening`, `open`, `disconnected`) |

Readings are the same ones the **Sensor Module** turns into redstone (see [Machines](Machines)).

---

## Writing methods

Each write method exists only on the machine it belongs to.

| Machine | Method | Arguments and rules |
|---|---|---|
| Industrial Boiler | `setSetpoint(celsius)` | 100 – 350 |
| Steam Turbine | `setFlow(mbPerTick)` | 0 – maximum flow of the formed turbine |
| | `setGenerator(engaged)` | boolean |
| | `setOverspeedTrip(on)` | boolean; `false` risks a rotor burst; refused in safe mode |
| Gas Turbine | `setFuelFlow(mbPerTick)` | 0 – maximum fuel flow of the formed turbine |
| | `setGenerator(engaged)` | boolean |
| | `setOverspeedTrip(on)` | boolean; `false` risks a rotor burst; refused in safe mode |
| Fission Reactor | `setControlRodTarget(percent)` | 0 – 100 (% inserted); refused while scrammed or failed |
| | `scram()` | drives all rods in |
| | `reset()` | clears a SCRAM; after a failure only below 100 °C; refused while overheating or with fuel damage |
| | `setAutoScram(on)` | boolean (needs Reactor Instrumentation to act) |
| | `setAutoScramTemperature(celsius)` | 300 – 1,200 |
| Tokamak | `start()` | vacuum, magnets, injection, ignition; refused if not formed |
| | `shutdown()` | safe ramp-down |
| | `setInjectionTarget(mbPerTick)` | 0 – 2 per Plasma Injector |
| | `setAuxHeating(ePerTick)` | 0 – 5,000 per Plasma Injector |
| | `setAutoRestart(on)` | boolean: re-ignite after a collapse |
| Little Star | `start()` | charge, compress, ignite; refused when it cannot start (the error says why) |
| | `shutdown()` | the star fades out |
| | `reset()` | only after a failure and with the shell below 100 °C |
| | `setFeed(mbPerTick)` | 0 – 10 % of the star's capacity |
| | `setControlRodTarget(percent)` | 20 – 100 |
| | `setAuto(on)` | boolean; `true` needs Stellar Diagnostics |
| Gas Engine | `start()` | refused if not formed or still too hot after an overheat stop |
| | `shutdown()` | |
| | `setPowerSetpoint(ePerTick)` | 0 – 80 per cylinder |
| | `setFollowDemand(on)` | boolean: follow its own buffer instead of the setpoint |
| Capacitor Bank | `setRedstoneMode(mode)` | `"always"`, `"release_on_signal"` or `"block_on_signal"` |
| Molten-Salt Store | `setHeatOutput(huPerTick)` | 0 – 100 per Heat Exchanger Tube |
| Battery Hall | `setProtection(on)` | boolean: thermal disconnect at 80 °C; `false` risks a thermal runaway; refused in safe mode |
| SMES | `setCooling(on)` | boolean; switching the Cryocoolers off with energy stored leads to a quench |
| Electrolyzer | `setFuelCell(on)` | `true`: fuel cell mode, `false`: electrolysis |
| Micro Black Hole Plant | `start()` | charge and form the singularity |
| | `shutdown()` | let the singularity shrink and dissolve through the collectors |
| | `reset()` | only after a failure, once the collectors cooled down |
| | `setFeed(mePerTick)` | 0 – 0.05 per Matter Injector; only with automatic control off |
| | `setJet(share)` | 0 – 1, share of the accreted matter the jets blow off; only with automatic control off |
| | `setAuto(on)` | boolean; `true` needs Gravimetry |
| | `splitCapsule()` | splits off a Singularity Capsule; only while running in the lower part of the mass window, with enough energy in the input buffer, and while the capsule output has room |
| Hawking Reactor | `shutdown()` | |
| | `reset()` | only after a failure, once the collectors cooled down |
| | `setPowerSetpoint(ePerTick)` | 1 – 10^12 |

---

## Example

A computer touching a Fission Reactor Controller prints the core state and scrams the reactor when the core gets too
hot:

```lua
local reactor = peripheral.find("quantavolt")

while true do
  local r = reactor.getReadings()
  print(("%s  core %.0f C  rods %.0f %%  fuel %.1f %%"):format(
    r.reactorState, r.temperature, r.controlRodPosition, r.fuelLevel))
  if r.temperature > 800 and r.reactorState == "running" then
    reactor.scram()
    print("SCRAM!")
  end
  sleep(1)
end
```

Catching a refused command:

```lua
local ok, err = pcall(reactor.setControlRodTarget, 150)
if not ok then print(err) end  -- the error text says: control rod target must be a number from 0 to 100
```

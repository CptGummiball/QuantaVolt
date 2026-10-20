# Safety and Incidents

Several QuantaVolt plants can fail badly. Nothing is random: the same situation always leads to the same incident, and
every severe incident has warning signs and a protection you can build or switch on. Ignore the warning or switch the
protection off, and you live with the result.

---

## Server switches

| Option | Default | Effect |
|---|---|---|
| `safeMode` | `false` | `true`: incidents still end the plant's run (fuel, charge or mass is lost), but nothing happens in the world: no explosion, no damage to entities or blocks. The client shows a harmless emergency shutdown instead of the full effect. It also keeps the turbines' overspeed trip and the Battery Hall's thermal disconnect switched on, and an Industrial Boiler above 380 °C takes no more outside heat. |
| `incidentTerrainDamage` | `false` | `true`: explosive incidents break blocks (only without `safeMode`). |
| `radiation` | `true` | `false`: no radiation from plants and incidents. `safeMode` switches it off as well. |

With the defaults, incidents explode and hurt entities, but no blocks are destroyed. See [Configuration](Configuration).

How an incident hits the world (with `safeMode=false`):

* **Explosive incidents** (overpressure, rotor burst, meltdown, star breach, thermal runaway) cause an explosion at
  the plant's center. Its power grows with the plant (boiler size and stored steam, rotor size, number of fuel
  assemblies, star size, stored charge); it is capped at 12.
* **Non-explosive incidents** (disruption, quench burst, radiation flash, gravity shock, implosion) damage living
  entities within reach of the plant (half the plant's size plus twice the incident strength, in blocks). The damage
  falls off with distance and ignores armor. Some push or pull entities.
* **Radiation:** meltdowns and radiation flashes also leave radiation behind (see [Radiation](#radiation)).

Client options `incidentEffects` and `particleDensity` only change what you see, not what happens.

---

## Warning signs

Before an incident, the plant shows a sign at its controller front (if `incidentEffects` is on):

| Sign | Meaning | Plants |
|---|---|---|
| Steam blowing off | Safety valves open, or coolant boiling away | Industrial Boiler (with valves), Fission Reactor (coolant problem) |
| Hissing white jets | Pressure rising with nowhere to go | Industrial Boiler (no valves) |
| Sparks | Rotor above its warning speed | Steam Turbine, Gas Turbine |
| Smoke and small flames | Overheating | Fission Reactor, Battery Hall, Gas Engine, Hawking Reactor |
| Cold fog | Cryostat warming up | SMES |
| Violet sparkles | Field or link unstable | Micro Black Hole Plant, Hawking Reactor, Dimensional Store |

The controller screen and the [ComputerCraft](ComputerCraft) readings show the same states in words.

---

## Incidents

### Overpressure – Industrial Boiler

* **Cause:** the boiler's temperature reaches **450 °C**. Fuel only burns up to the setpoint (at most 350 °C), so this
  happens when heat keeps coming through HEAT ports while the steam cannot leave (steam tank full).
* **Warning:** from **380 °C** the screen shows *OVERPRESSURE: steam cannot leave, the shell will burst* and the
  controller hisses.
* **Protection:** **Safety Valves** in the boiler wall open above 380 °C and blow off up to 1,000 HU/t of steam each
  (screen: *Overpressure: safety valves blowing off*). Keep the steam output flowing (turbine, tank, Emergency Vent).
* **Consequence:** steam explosion; all steam and water in the boiler are lost. Strength grows with the boiler size and
  the stored steam.

### Rotor burst – Steam Turbine and Gas Turbine

* **Cause:** only possible with the **overspeed trip switched off** (button *S* in the screen or
  `setOverspeedTrip` on a computer; refused in `safeMode`). The trip is on by default and closes the steam or fuel
  valve above the trip speed until the rotor is back at rated speed.

  | Turbine | Rated | Warning | Trip |
  |---|---|---|---|
  | Steam Turbine | 1,800 rpm | 2,200 rpm | 2,600 rpm |
  | Gas Turbine | 3,600 rpm | 4,200 rpm | 4,800 rpm |

* **Without the trip:** above the trip speed the blades wear (a worn rotor turns less steam or fuel into work, down to
  half; forming the turbine again repairs it). Above 115 % of the trip speed, or with fully worn blades, the rotor
  bursts.
* **Warning:** sparks above the warning speed; screen *Overspeed: reduce steam or engage the generator*.
* **Consequence:** explosion; the rotor's energy is gone. Strength grows with the rotor's size.
* **Prevention:** keep the trip on, keep the generator engaged, admit less steam or fuel.

### Meltdown – Fission Reactor

* **Escalation by core temperature:**

  | Core | Alarm |
  |---|---|
  | 600 °C | *Warning: high temperature* |
  | 900 °C | *Overheating* |
  | coolant missing | *Coolant problem* |
  | above 1,200 °C | *Fuel damage!* – damage builds up |
  | damage 100 % or 1,800 °C | *Severe failure* |

* **Consequence:** meltdown explosion at the core. All fuel is destroyed and the reactor is locked (*Severe failure –
  let it cool, then reset*). A reset is only possible below 100 °C.
* **Protection:**
  * **SCRAM** drives all control rods in fast: button in the screen, `scram()` on a computer, or a redstone signal at
    an **Emergency Shutdown** wall part.
  * **Auto-SCRAM** needs **Reactor Instrumentation** in the wall. It is on by default and trips at 900 °C (adjustable
    300–1,200 °C), and also when the coolant is short above 600 °C.
  * Enough Coolant Channels with water, and enough Control Rods (one per four Fuel Assemblies, otherwise even full
    insertion cannot shut the reactor down).
* After a SCRAM the reactor needs a reset; it is refused while the alarm still says *Overheating* or *Fuel damage!*.

### Disruption – Tokamak

* **Cause:** the plasma collapses while it holds more than 2,000,000 HU of thermal energy. A collapse comes from
  instability (stability below 25 %), lost magnet power, fuel starvation, the startup energy running out or a broken
  structure. Stability falls with plasma density above the limit, an overloaded divertor, helium in the plasma and a
  hot blanket.
* **Consequence:** thunder and damage to living entities nearby. No explosion, no block damage, no lasting damage to
  the tokamak; the plasma is lost.
* **Not an incident:** a blanket above 900 °C (no heat sink) triggers a controlled shutdown before anything happens.
* **Prevention:** watch the stability on the screen, keep fuel and magnet power supplied, take the heat away, pump the
  helium out. *Automatic re-ignition* (off by default) restarts after a collapse and costs the startup energy again.

### Star breach – Little Star

* **Cause:** the stability reaches zero, or the shell reaches **1,400 °C**, or the structure breaks while the star is
  burning. Stability falls with a mismatch between the rods' field and the star's pressure, with helium in the core,
  with a shell above 800 °C and when the rods do not get their power. The rods draw 2,000 E/t each (times their
  insertion) only from energy that comes in through **Energy Input Ports**, never from the star's own output.
* **Helium flash:** when helium makes up more than half of the core, it ignites at once: the star gets hotter, loses
  stability and heats the shell.
* **Consequence:** explosion that never breaks blocks; with `incidentTerrainDamage` the Stellar Containment Glass
  shatters. The star is lost, the rods lose half their condition, and the plant is *Failed – let the shell cool, then
  reset* (shell below 100 °C).
* **Protection:** **Stellar Diagnostics** enable the automatic control: it fades the star out safely when the
  stability falls below 35 %, the shell gets hotter than 1,000 °C or helium exceeds 42 %. Keep the energy input
  supplied, cool the shell (water to steam, or HEAT ports) and pull the helium out.

### Thermal runaway – Battery Hall

* **Cause:** only possible with the **thermal disconnect switched off** (button *S* or `setProtection(false)`; refused
  in `safeMode`). With it on, the hall disconnects at 80 °C and reconnects below 50 °C.
* **Without it:** above 80 °C the cells heat themselves, faster the hotter they get; at **140 °C** they run away.
* **Warning:** smoke and flames above 60 °C; from 60 °C the rate drops (*Hot: rate reduced*). Efficiency is 97 % up to
  45 °C and falls to 85 % at 80 °C.
* **Consequence:** explosion; the whole charge is lost. With `incidentTerrainDamage` it also breaks blocks and starts
  fires.
* **Prevention:** keep the disconnect on; add Battery Coolers and give them cooling water (each carries up to
  10 mB/t of water away as Hot Coolant).

### Quench burst – SMES

* **Cause:** the coils warm above **9 K** while energy is stored: coolers switched off or unpowered, helium charge
  empty, or the structure broken. The coils lose superconductivity.
* **Warning:** cold fog from 7 K (*Warning: coils warming up*).
* **With Dump Resistors:** a controlled quench. The energy leaves as heat over a few seconds (HEAT ports can use it),
  half of the helium boils off. No incident.
* **Without Dump Resistors:** the energy turns into heat in the coils at once, the whole helium charge boils off and
  the coils get very warm. A helium burst damages entities nearby, pushes them away and freezes them.
* Either way the store has to be cooled down again before it carries current.

### Radiation flash – Micro Black Hole Plant, Hawking Reactor

* **Micro Black Hole Plant:** the singularity evaporates, i.e. its mass falls below the lower edge of its operating
  window (30 mass units), for example when the matter runs out.
* **Hawking Reactor:** the singularity evaporates completely (below 0.3 mass units), the matter runs out, or the
  structure breaks while it runs.
* **Consequence:** a flash that damages living entities nearby (strength grows with the mass). No explosion.
* **Not an incident:** a Hawking Reactor whose collectors get too hot shuts itself down safely.
* **Prevention:** keep Compressed Matter coming; use **Gravimetry** for the automatic control.

### Gravity shock – Micro Black Hole Plant

* **Cause:** containment is lost: the mass grows above the upper edge of the window (50 + 10 × (edge − 9) mass units,
  so 50 for an edge of 9, 70 for 11), the containment does not get its power (2,000 E/t per mass unit), or the structure breaks
  while the singularity exists.
* **Warning:** violet sparkles while the stability is below 50 %.
* **Consequence:** a gravity shock throws living entities away and damages them.

### Implosion – Dimensional Store

* **Cause:** the link stability falls below 5 %. Stability settles at 0.9 + 0.08 per stabiliser − 0.06 per transfer
  channel − 0.15 × load; if the upkeep (5,000 E/t per Transfer Channel, 20,000 E/t per Dimensional Stabiliser) is not
  paid, it heads for 0. The stability follows this target slowly.
* **Warning:** below 50 % some of every transfer is lost and violet sparkles appear; below 20 % the store disconnects
  (*Disconnected (stabilising)*) until it is back above 35 %.
* **Consequence:** an implosion pulls living entities in and damages them. While the stability stays that low, the
  pocket loses 1 % of its content every second.
* **Prevention:** pay the upkeep, add Dimensional Stabilisers, do not run more transfer channels than the link holds.

---

## Radiation

Only running nuclear plants and two incidents radiate; there are no radioactive items or ores. Once per second every
living being within reach takes radiation damage (it ignores ordinary armor) and gets the **Radiation** effect for a
moment. Players in Creative or Spectator mode are not affected.

| Source | Strength | When |
|---|---|---|
| Fission Reactor | up to 6 (4 × flux, flux capped at 1.5) | while the reactor runs |
| Tokamak | 3 | ignition, heating and stable burn |
| Little Star | 4 | ignition, burning and fading |
| Micro Black Hole Plant | 3 | forming and running |
| Hawking Reactor | 4 | starting and running |
| Meltdown (incident) | 8, fading out over 5 minutes | after a meltdown, at the core |
| Radiation flash (incident) | 12 at the moment of the flash, then 6 fading out over 30 seconds | after a flash |

* **Strength** is the damage per second at the centre of the plant (2 = one heart), at most 8 per second.
* **Reach:** 6 blocks + half the plant size + 2 × strength. The damage falls off evenly to 0 at the edge of the reach.
* **Blocks in between** (on the straight line to the eyes):
  * **Shielding blocks** (Block of Lead, Lead Concrete, Lead Glass, any mod's lead block; tag
    `quantavolt:radiation_shielding`) let only 5 % through, each.
  * Other solid blocks let 60 % through, each. Glass and air let everything through.
* **Radiation suit:** every worn piece (Radiation Hood, Jacket, Trousers, Boots) takes 25 % of what arrives; the full
  suit stops it completely. Ordinary armor does not help. The suit is repaired with lead ingots in an anvil (on
  Minecraft 1.21.2–1.21.4 with leather).
* Below 0.25 damage per second nothing happens.

**Example:** a player right beside a running 5x5x5 Fission Reactor takes roughly 1 to 4 damage per second, depending
on the flux and on how many solid plant blocks lie in between (a glass front lets more through). One layer of lead
blocks between them cuts that to 5 %, below the threshold.

Shielding blocks protect only against radiation, not against explosions or the other incidents.

### Reinforced blocks

**Reinforced Concrete** and **Reinforced Glass** (tag `quantavolt:blast_shielding`) protect against incidents:

* They withstand explosions (blast resistance 1,200, like obsidian), so explosive incidents with
  `incidentTerrainDamage=true` do not break them, and the explosion does not reach entities behind them.
* The damage of non-explosive incidents (disruption, quench burst, radiation flash, gravity shock, implosion) is cut to
  10 % by every reinforced block on the straight line between the plant and the entity.
* They do not stop radiation (Reinforced Glass counts as glass, Reinforced Concrete as an ordinary solid block). Build
  a lead layer and a reinforced layer for both.

---

## Failures that are not incidents

| Plant | What happens |
|---|---|
| Gas Engine | Without cooling it derates above 110 °C (down to 40 % load) and stops at 130 °C; it can be restarted below 70 °C. |
| Capacitor Bank | Heats with its throughput; from 70 °C the rate is throttled, down to 20 % at 100 °C. |
| Molten-Salt Store | Thermal Salt freezes below 290 °C and gives no heat until it is heated again. |
| Wind Turbine | Storm shutdown above 1.6 × rated wind, back on below 1.3. |
| Tokamak | Blanket overheat → controlled shutdown. |
| Hawking Reactor | Collector overheat → safe shutdown. |

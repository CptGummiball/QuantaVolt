# Build Projector

The Build Projector (since 0.2.0) shows a plant's building plan in the world, at full size, where the plant will
stand: small floating blocks where parts are still missing and red frames where something is in the way. You choose the
plant's size first, within the sizes the plant allows, and the projector tells you which blocks you still need.

Recipe: spyglass, iron ingots and redstone ([Recipes](Recipes)).

---

## Using it

1. **Place the controller** of the plant first. Its position and the direction it faces decide where the plan goes.
   For box-shaped plants the controller sits in the front wall on the **second layer**: the plan's floor is one block
   below the controller, so place the controller one block above the ground the plant will stand on (or dig the floor
   in).
2. **Right-click the controller with the Build Projector in your main hand.** The projector screen opens instead of
   the controller's own screen.
3. Choose the size, then switch the projection on with **I/O**.
4. Build. The projection updates once a second.
5. When the plant **forms**, the projection ends by itself.

**Sneak + right-click** the controller with the projector to end the projection at once ("Projection switched off").
Right-clicking anything other than a controller only shows a short hint.

---

## The screen

| Line | Controls | What it does |
|---|---|---|
| Plant | – | The plant of this controller. |
| One line per size value (*Width*, *Height*, *Depth*, *Size*, *Edge*, *Cylinders*, *Blade length*, *Rotor arms*, *Generators*, *Tower height*, *Rows*, *Columns*) | `-` / `+` | Changes the value by one step within its range (shown in brackets, e.g. *Width: 5 (3–16)*). Odd-only values move by two. Past the largest value it starts again at the smallest, and the other way round. |
| *Sight glass front* | `-` / `+` | *yes*: every block of the front wall (the wall with the controller) that is not on an edge is the plant's sight glass instead of casing; *no*: casing. Only plants that allow sight glass have this line. |
| *Shown* | `-` / `+` | *whole plant* or *layer n of m*. `+` goes from the whole plant to layer 1 (the lowest), up layer by layer and back to the whole plant; `-` goes the other way. |
| *Projection* | **I/O** | Switches the projection on or off. *on (visible to everyone)*, *off*, or *the plant has formed – projection ended*. If the chosen values break a server limit it says so instead (*too many modules for this plant (server limit)*, *tower lower than the server minimum*) and nothing is projected. |
| *Blocks in the plan*, *Missing*, *In the way* | – | Counts for the shown part of the plan: all its blocks, the blocks still missing and the blocks in the way. |
| Material list | – | Up to eight lines: each block the shown part of the plan still needs (missing or with something else in its place), how many, and how many of it you carry in your inventory (*carried: …*), most needed first. With more than eight kinds the last line says how many more kinds there are. *nothing missing* when the shown part is complete. |

The values are kept in the controller (also after saving and loading) and are the same for every player. The server
checks every button: the screen works only while you stay near the controller, and values outside the plant's ranges
are never accepted. The counts and the material list refresh once a second.

---

## The projection

* **Missing block:** a half-size floating copy of the block that belongs there (ports show as the right port type).
* **In the way:** a glowing red glass frame around the block. That is any block where the plan wants a different
  block, a different port type, or air. The most common case: **ground below the floor layer.** If the controller was
  placed directly on the ground, the plan's floor layer lies inside the ground, and every dirt or stone block there
  shows red. Dig it out or place the controller one block higher.
* Blocks that already match the plan are left alone.
* The projection follows **one** valid layout of the plant: one port of each kind at fixed places, casing in all other
  walls. A different valid choice (an Inspection Hatch, a Safety Valve or sight glass where the plan has casing, ports
  elsewhere in the wall) shows as *in the way*, but the plant still forms. Where the plan leaves the inside of a plant
  open (for example the empty inside of the Large Gas Tank) nothing is checked.
* **Layers:** in *layer n of m* mode only that layer is projected and counted. Use it for big plants.

### Limits

* At most **256** displays per projection; the rest appears as blocks get placed (or show one layer at a time). Every display is a vanilla entity the server has to tick: while a large projection shows, it costs server time (about 1.5 ms per tick for 400 displays in the benchmark), so switch it off when you do not need it, or show one layer.
* At most 96 new displays appear per second, so a large plan builds up over a few seconds.
* Only loaded chunks are projected and counted.

### Visible to everyone

The projection consists of vanilla **block display** entities, so every player sees it, on every game version, without
any client setting. It is not saved: after loading, the controller finds its displays again (by their tag) and brings
them up to date.

The projection ends when the plant forms, when you switch it off (I/O or sneak + right-click), when you change the
plan (the old displays are removed and the new plan appears), and when the controller is broken. Finishing a plant
while its projection shows earns *By the Book* for the players within 32 blocks (see [Advancements](Advancements)).

Should displays ever be left over, an operator removes all projection displays of the world with

```
/kill @e[type=block_display,tag=quantavolt_projection]
```

---

## Plants and sizes

Every one of the 22 plants has a plan. The ranges below are those of the default
[server configuration](Configuration#structure-limits); where a limit comes from the configuration, the key is named.
"odd" values move in steps of two.

| Plant | Values in the plan (default) | Sight glass front |
|---|---|---|
| [Industrial Boiler](Build-Industrial-Boiler) | Width 3–16 (5), Height 4–16 (5), Depth 3–16 (5) – `maxStructureSize` | yes |
| [Steam Turbine](Build-Steam-Turbine) | Width 5–15 odd (5), Height 5–15 odd (5), Depth 5–16 (5) | yes |
| [Gasifier](Build-Gasifier) | Width 3–16 (3), Height 4–16 (4), Depth 3–16 (3) | yes |
| [Gas Turbine](Build-Gas-Turbine) | Width 5–15 odd (5), Height 5–15 odd (5), Depth 6–16 (7) | yes |
| [Gas Engine](Build-Gas-Engine) | Cylinders 1–8 (4) | – |
| [Gas Derrick](Build-Gas-Derrick) | Height 6–12 (8) | – |
| [Centrifuge Cascade](Build-Centrifuge-Cascade) | Width 3–16 (5), Height 4–16 (4), Depth 4–16 (4) | yes |
| [Fission Reactor](Build-Fission-Reactor) | Width, Height, Depth 5–15 each (5) – `maxFissionReactorSize` | yes |
| [Tokamak](Build-Tokamak) | Size 11–15 odd (11, square footprint), Height 5–16 (5) | yes |
| [Little Star](Build-Little-Star) | Edge 9–15 odd (9) | – (the faces are always Stellar Glass) |
| [Micro Black Hole Plant](Build-Singularity-Plant) | Edge 9–15 odd (9) | yes |
| [Hawking Reactor](Build-Hawking-Reactor) | Edge 7–15 odd (7) | yes |
| [Dimensional Store](Build-Dimensional-Store) | Edge 5–15 odd (5) | yes |
| [Battery Hall](Build-Battery-Hall) | Width 4–16 (5), Height 3–16 (4), Depth 4–16 (4) | yes |
| [Molten-Salt Store](Build-Molten-Salt-Store) | Width **4**–16 (4), Height 3–16 (4), Depth 3–16 (4) | yes |
| [Gravity Store](Build-Gravity-Store) | Width 3–16 (3), Height 5–64 (7), Depth 3–16 (3) | yes |
| [SMES](Build-SMES) | Width 5–16 (7), Height 4–16 (5), Depth 5–16 (5) | yes |
| [Large Gas Tank](Build-Large-Gas-Tank) | Width, Height, Depth 3–32 each (5) | yes |
| [Wind Turbine](Build-Wind-Turbine) | Blade length 2–8 (4) – `maxWindBladeLength`; Rotor arms 2–4 (3); Generators 1–3 (2); Tower height 1–128 (8), at least `minWindTowerHeight` (4) | – |
| [Capacitor Bank](Build-Capacitor-Bank) | Width, Height, Depth 1–8 each (3, 2, 2); together at most `maxCapacitorModules` (128) modules | – |
| [Solar Array](Build-Solar-Array) | Rows 1–16 (4), Columns 1–16 (5); together at most `maxSolarModules` (256) modules | – |
| [Solar Thermal Field](Build-Solar-Thermal) | Rows 1–16 (4), Columns 1–16 (5); together at most `maxHeliostats` (512) heliostats | – |

* The **Molten-Salt Store** plan starts at width 4: the store needs at least two interior blocks (a Heat Exchanger
  Tube and Thermal Salt), and a 3×3×3 box has only one.
* The plans of the Gas Engine, Wind Turbine, Capacitor Bank, Solar Array and Solar Thermal Field are not boxes: the
  cylinders, modules or heliostats lie behind or beside the controller, the wind turbine's rotor in front of it and
  its tower below it.
* Every plan is checked in the mod's tests to form: at every allowed size where the ranges are small, at the limits
  and at sample sizes in between where they are large.

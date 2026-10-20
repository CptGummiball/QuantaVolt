# FAQ

### Is there a single jar for all versions?

No, on purpose. Each file is for one Minecraft version or a few neighbouring ones, and only where that very file was
tested on each of them. See [Supported Versions](Supported-Versions).

### What else do I need?

[Pipster](https://modrinth.com/mod/pipster) on every version (QuantaVolt's gases live in Pipster's gas system), and on
Fabric the Fabric API. Everything else is optional.

### Does it have to be installed on the server and on every client?

Yes. QuantaVolt adds blocks, items and screens, so server and clients need the same QuantaVolt file.

### My plant does not form. What now?

Open the controller (or an Inspection Hatch): the screen names the problem and the position, for example
"Wrong block at … (expected: …)". Every build page lists the usual messages and how to fix them, and shows a working
example layer by layer. Start with [Getting Started](Getting-Started).

### The projection shows red frames under my plant. Why?

Red frames mark blocks that are in the way of the plan. For box-shaped plants the controller sits on the second
layer, so the plan's floor is one block below the controller. If you placed the controller directly on the ground,
the floor layer lies in the ground and every dirt or stone block there is "in the way". Dig the floor layer out or
place the controller one block higher. A red frame on a block that is also allowed there (an Inspection Hatch, sight
glass, a port at a different place) only means the plan chose something else; the plant still forms. See
[Build Projector](Build-Projector).

### How do I get rid of projection blocks that stayed behind?

Normally they vanish when the plant forms, the projection is switched off or the controller is broken. If any are
ever left over, an operator removes all of them with `/kill @e[type=block_display,tag=quantavolt_projection]`.

### There is no natural gas in the Nether (or the End).

That is intended: natural gas fields exist only in the Overworld. The server option `naturalGasDimensions` can add
other dimensions ([Configuration](Configuration#natural-gas)). The Gas Prospector says "There is no natural gas in
this dimension" there.

### My Gas Derrick says "No natural gas in this region".

About 60 % of the regions (128 × 128 blocks each) have no field, and the derrick takes gas only from the region its
controller stands in. Use the Gas Prospector: it shows the region's borders and the direction of the nearest field
among the eight neighbouring regions. Then rebuild the derrick there. See [Natural Gas](Natural-Gas).

### My Gas Derrick says "Field depleted".

The field of that region is empty and never refills. Move to another field.

### Which cables and pipes work?

QuantaVolt has no cables or pipes of its own. Its machines and ports use the standard interfaces of the loader, so
energy cables and item or fluid pipes of other mods connect to them. Gases need Pipster's gas pipes. Details:
[Energy, Fluids and Gases](Energy-Fluids-Gases).

### Can a plant destroy my base?

Some incidents explode or damage blocks, but only if you ignore the warnings (or switch protections off). Terrain damage
is controlled by the server option `incidentTerrainDamage`, and `safeMode` turns all incidents into a plain shutdown.
See [Safety and Incidents](Safety-and-Incidents).

### Does it work with JEI, Jade or CC: Tweaked?

Yes, where those mods exist for your Minecraft version: JEI shows the machine recipes, Jade shows machine status, and
CC: Tweaked computers can read and control the plants ([ComputerCraft](ComputerCraft)). They are optional. The exact
tested versions are on [Supported Versions](Supported-Versions).

### Do the ores generate with world generation mods?

They are added to every Overworld biome of the world generator. This was checked with Terralith and Biomes O' Plenty on
Minecraft 1.21.1 and 26.3 on both loaders; other world generators were not tested.

### Can I use QuantaVolt in my modpack?

Yes, as long as the jar files stay exactly as published. See [License and Permissions](License-and-Permissions).

### Where do I download QuantaVolt?

Only on Modrinth and CurseForge. Files from other sources are not official.

### I found a bug. Where do I report it?

In the GitHub issue tracker. Please give the exact file name of the QuantaVolt jar, the loader and its version, and
attach `logs/latest.log` (and a crash report if there is one).

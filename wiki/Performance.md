# Performance

All numbers on this page were **measured on one computer with one test scene**. They are not a promise for every server,
modpack or world: other hardware, other mods and other builds will give other numbers.

## Test computer

| | |
|---|---|
| CPU | Intel Core i7-13700H (20 threads), laptop in performance mode |
| RAM | 32 GB (server heap max. 8 GB) |
| GPU | Intel Iris Xe (integrated) |
| System | Windows 11 |
| Java | 21 (Minecraft 1.21.1), 25 (Minecraft 26.3) |

## Server: a large build in operation

A dedicated server with **54 formed and running plants** next to each other: 8 steam turbines, 8 industrial boilers,
4 gas turbines, 4 gasifiers, 4 centrifuge cascades, 4 fission reactors, 2 tokamaks, 2 Little Stars, a solar array (240
modules), a solar thermal field (224 heliostats), 4 wind turbines, 2 gas engines, 2 capacitor banks, a battery hall, a
molten-salt store, a gravity store, an SMES, a micro black hole plant, a Hawking reactor and a dimensional store – plus
168 single machines (dynamos, electrolyzers, condensers, thermoelectric and Stirling generators, pumps). Everything is
supplied and working. Since 0.2.0 the scene also has two Gas Derricks pumping natural gas, two burning Gas Flares and a
Build Projector projection of a Little Star (9×9×9, 397 block displays when measured; now at most 256, see below):
56 formed plants and 170 single machines. 60 s warm-up, then 3 runs of 5 minutes each.

Time QuantaVolt needs per server tick (a tick has 50 ms), median of each run and the 99th percentile, QuantaVolt 0.2.0:

| Minecraft | Loader | Median (3 runs) | 99th percentile (3 runs) |
|---|---|---|---|
| 1.21.1 | Fabric | 0.78 / 0.72 / 0.67 ms | 1.86 / 1.60 / 1.62 ms |
| 1.21.1 | NeoForge | 0.52 / 0.67 / 0.63 ms | 1.67 / 1.51 / 1.59 ms |
| 26.3 | Fabric | 0.58 / 0.46 / 0.28 ms | 1.78 / 1.51 / 0.92 ms |
| 26.3 | NeoForge | 0.43 / 0.40 / 0.35 ms | 1.41 / 1.49 / 0.77 ms |

So this large build used under 2 % of the tick budget in the median and under 4 % in the 99th percentile on this
computer. Only these two Minecraft versions were measured. The numbers vary a lot between runs on this laptop (26.3
Fabric: 0.58 to 0.28 ms within one series), so small differences between versions or loaders mean little.

0.1.0 (same scene without the 0.2.0 cell), for comparison: median 0.39–0.65 ms (1.21.1 Fabric), 0.81–0.87 ms (1.21.1
NeoForge), 0.77–0.83 ms (26.3 Fabric), 1.35–1.41 ms (26.3 NeoForge).

**Build projections cost server time while they show.** Every displayed block is a vanilla entity the server ticks. In
the same scene on 1.21.1 Fabric without the projection and without that one unformed controller, QuantaVolt took 0.22–0.27
ms in the median and the whole server tick was about 1.5 ms shorter. That is why a projection shows at most 256 blocks at
a time (or one layer). It ends by itself when the plant forms; switch it off when you do not need it.

**Upgrade from 0.1.0:** a world with all 54 plants saved by 0.1.0 loaded in 0.2.0 with all 54 plants formed and no errors
(1.21.1 Fabric and 26.3 NeoForge).

**1.0.0:** the same scene, 2 shorter runs of 2.5 minutes: median 0.47 / 0.40 ms and 99th percentile 1.34 / 1.04 ms on 1.21.1
Fabric, median 0.74 / 0.67 ms and 99th percentile 2.21 / 1.73 ms on 26.3 NeoForge – within the spread of the 0.2.0 runs.
**Upgrade from 0.2.0:** a world with all 56 plants saved by 0.2.0 loaded in 1.0.0 with all of them formed and no errors
(1.21.1 Fabric and 26.3 NeoForge).

## How QuantaVolt keeps the cost down

* A plant is checked again only after a block of it changed (at most every 10 ticks); between checks it works from the
  cached result, and a small audit looks at 8 positions per tick for foreign blocks in its air spaces. The size of every
  plant is limited (configurable).
* No chunk loading: a plant that is partly in unloaded chunks pauses until it is loaded again.

## Client: drawing the plants

Moving parts (rotors, centrifuges, plasma, the star) are drawn by the mod. Measured with six running plants in view at
854×480 on the integrated Intel GPU:

| Minecraft | Cost of all QuantaVolt renderers per frame |
|---|---|
| 1.21.1 (with all interior effects) | 0.39 ms |
| 26.3 (with all interior effects, 1.0.0) | 2.68 ms |
| 26.3 with `interiorEffects=false` | 1.94 ms |

**Known limitation:** on 26.x the same plants cost several times more per frame than on 1.21.1. About 0.8 ms of it is the
life inside the plants behind their sight glass; `interiorEffects=false` in `config/quantavolt-client.properties` switches
it off. The rest is not explained yet; two attempts to lower it before 1.0.0 made no measurable difference and were not
shipped. The visual effects can be reduced in the client configuration (see [Configuration](Configuration)). Not
measured: dedicated graphics cards, other resolutions, shader mods, multiplayer load.

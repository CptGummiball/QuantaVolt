# Supported Versions

QuantaVolt 1.0.0 has one file per loader and Minecraft version; a few files cover two neighbouring versions. Such a
file is offered only because that very file (same checksum) was started and tested **unchanged on each version
it lists**. There is no file that claims an open range.

**Required on every version:** [Pipster](https://modrinth.com/mod/pipster) (pipes and the gas system QuantaVolt uses),
and on Fabric the Fabric API.

## Which file do I need?

| Minecraft | Fabric | NeoForge |
|---|---|---|
| 1.21.1 | `quantavolt-1.0.0+mc1.21.1-fabric.jar` | `quantavolt-1.0.0+mc1.21.1-neoforge.jar` |
| 1.21.2 | `quantavolt-1.0.0+mc1.21.2-1.21.3-fabric.jar` | `quantavolt-1.0.0+mc1.21.2-1.21.3-neoforge.jar` |
| 1.21.3 | `quantavolt-1.0.0+mc1.21.2-1.21.3-fabric.jar` | `quantavolt-1.0.0+mc1.21.2-1.21.3-neoforge.jar` |
| 1.21.4 | `quantavolt-1.0.0+mc1.21.4-fabric.jar` | `quantavolt-1.0.0+mc1.21.4-neoforge.jar` |
| 1.21.5 | `quantavolt-1.0.0+mc1.21.5-fabric.jar` | `quantavolt-1.0.0+mc1.21.5-neoforge.jar` |
| 1.21.6 | `quantavolt-1.0.0+mc1.21.6-fabric.jar` | `quantavolt-1.0.0+mc1.21.6-neoforge.jar` |
| 1.21.7 | `quantavolt-1.0.0+mc1.21.7-1.21.8-fabric.jar` | `quantavolt-1.0.0+mc1.21.7-1.21.8-neoforge.jar` |
| 1.21.8 | `quantavolt-1.0.0+mc1.21.7-1.21.8-fabric.jar` | `quantavolt-1.0.0+mc1.21.7-1.21.8-neoforge.jar` |
| 1.21.9 | `quantavolt-1.0.0+mc1.21.9-1.21.10-fabric.jar` | `quantavolt-1.0.0+mc1.21.9-neoforge.jar` |
| 1.21.10 | `quantavolt-1.0.0+mc1.21.9-1.21.10-fabric.jar` | `quantavolt-1.0.0+mc1.21.10-neoforge.jar` |
| 1.21.11 | `quantavolt-1.0.0+mc1.21.11-fabric.jar` | `quantavolt-1.0.0+mc1.21.11-neoforge.jar` |
| 26.1 | `quantavolt-1.0.0+mc26.1-26.1.1-fabric.jar` | `quantavolt-1.0.0+mc26.1-26.1.1-neoforge.jar` |
| 26.1.1 | `quantavolt-1.0.0+mc26.1-26.1.1-fabric.jar` | `quantavolt-1.0.0+mc26.1-26.1.1-neoforge.jar` |
| 26.1.2 | `quantavolt-1.0.0+mc26.1.2-fabric.jar` | `quantavolt-1.0.0+mc26.1.2-neoforge.jar` |
| 26.2 | `quantavolt-1.0.0+mc26.2-fabric.jar` | `quantavolt-1.0.0+mc26.2-neoforge.jar` |
| 26.3 | `quantavolt-1.0.0+mc26.3-fabric.jar` | `quantavolt-1.0.0+mc26.3-neoforge.jar` |

Checksums of all files: `SHA256SUMS` next to the files of each release.

## What "tested" means

For every version above, the exact file from the table

* started a dedicated server and a client (the client also entered a world),
* ran all automated game tests of the mod (structures, machines, energy, fluids, gases, saving and loading),
* ran again together with each supported mod listed below that exists for that version.

Manual play tests are listed separately in the release notes; not every combination was played by hand.

## Exact versions used in testing

| Minecraft | Fabric Loader | Fabric API | NeoForge | Pipster |
|---|---|---|---|---|
| 1.21.1 | 0.19.5 | 0.116.17+1.21.1 | 21.1.252 | 1.0.0 |
| 1.21.2 | 0.19.5 | 0.106.1+1.21.2 | 21.2.1-beta (NeoForge was only available as beta) | 1.0.0 |
| 1.21.3 | 0.19.5 | 0.114.1+1.21.3 | 21.3.97 | 1.0.0 |
| 1.21.4 | 0.19.5 | 0.119.4+1.21.4 | 21.4.158 | 1.0.0 |
| 1.21.5 | 0.19.5 | 0.128.2+1.21.5 | 21.5.98 | 1.0.0 |
| 1.21.6 | 0.19.5 | 0.128.2+1.21.6 | 21.6.20-beta (NeoForge was only available as beta) | 1.0.0 |
| 1.21.7 | 0.19.5 | 0.129.0+1.21.7 | 21.7.25-beta (NeoForge was only available as beta) | 1.0.0 |
| 1.21.8 | 0.19.5 | 0.136.1+1.21.8 | 21.8.54 | 1.0.0 |
| 1.21.9 | 0.19.5 | 0.134.1+1.21.9 | 21.9.16-beta (NeoForge was only available as beta) | 1.0.0 |
| 1.21.10 | 0.19.5 | 0.138.4+1.21.10 | 21.10.64 | 1.0.0 |
| 1.21.11 | 0.19.5 | 0.141.6+1.21.11 | 21.11.45 | 1.0.0 |
| 26.1 | 0.19.5 | 0.145.1+26.1 | 26.1.0.19-beta (NeoForge was only available as beta) | 1.0.0 |
| 26.1.1 | 0.19.5 | 0.145.4+26.1.1 | 26.1.1.15-beta (NeoForge was only available as beta) | 1.0.0 |
| 26.1.2 | 0.19.5 | 0.155.3+26.1.2 | 26.1.2.112 | 1.0.0 |
| 26.2 | 0.19.5 | 0.161.0+26.2 | 26.2.0.88 | 1.0.0 |
| 26.3 | 0.19.5 | 0.161.0+26.3 | 26.3.0.37-beta (NeoForge was only available as beta) | 1.0.0 |

## Integrations

All integrations are optional: QuantaVolt never requires these mods and only switches the integration on when the
mod is installed. ✓ = tested with the released file and the partner version shown (S = server, C = client with a
world, G = game tests); "blocked" = the partner mod itself fails on that version (reason in the notes); "–" = not
tested on that version (for Jade, CC: Tweaked and JEI: the partner mod has no release for it; material and ore
checks with other mods were run on the oldest and the newest version only).

### Fabric

| Minecraft | Jade | CC: Tweaked | JEI | Tech Reborn (materials) | Terralith (ores) | Biomes O' Plenty (ores) | Oritech (fluids in its tanks) |
|---|---|---|---|---|---|---|---|
| 1.21.1 | ✓ 15.10.6 (SCG) | ✓ 1.120.2 (SCG) | ✓ 19.57.0.450 (C) | ✓ (S) | ✓ (S) | ✓ (S) | ✓ (SCG) |
| 1.21.2 | ✓ 16.0.0 (C) ¹ | – | – | – | – | – | – |
| 1.21.3 | ✓ 16.0.4 (SCG) | – | – | – | – | – | – |
| 1.21.4 | ✓ 17.2.2 (SCG) | ✓ 1.115.1 (SCG) | – | – | – | – | – |
| 1.21.5 | ✓ 18.2.0 (SCG) | – | ✓ 21.4.0.27 (C) | – | – | – | – |
| 1.21.6 | ✓ 19.3.2 (SCG) | – | – | – | – | – | – |
| 1.21.7 | ✓ 19.3.2 (SCG) | ✓ 1.116.1 (SCG) | ✓ 23.1.0.8 (C) | – | – | – | – |
| 1.21.8 | ✓ 19.3.2 (SCG) | ✓ 1.116.1 (SCG) | ✓ 24.2.0.6 (C) | – | – | – | – |
| 1.21.9 | ✓ 20.0.5 (SCG) | – | ✓ 25.0.1.4 (C) | – | – | – | – |
| 1.21.10 | ✓ 20.0.5 (SCG) | – | ✓ 26.3.0.31 (C) | – | – | – | – |
| 1.21.11 | ✓ 21.1.6 (SCG) | ✓ 1.117.1 (SCG) | ✓ 27.44.0.104 (C) | – | – | – | – |
| 26.1 | ✓ 26.1.9 (SCG) | – | ✓ 29.2.0.21 (C) | – | – | – | – |
| 26.1.1 | ✓ 26.1.9 (SCG) | – | ✓ 29.4.0.23 (C) | – | – | – | – |
| 26.1.2 | ✓ 26.1.9 (SCG) | ✓ 1.120.0 (SCG) | ✓ 29.43.0.106 (C) | – | – | – | – |
| 26.2 | ✓ 26.2.11 (SCG) | ✓ 1.120.2 (SCG) | ✓ 30.39.0.232 (C) | – | – | – | – |
| 26.3 | ✓ 26.3.1 (SCG) | ✓ 1.120.3 (SCG) | ✓ 31.8.0.53 (C) | ✓ (S) | ✓ (S) | ✓ (S) | – |

### NeoForge

| Minecraft | Jade | CC: Tweaked | JEI | Mekanism (materials) | Terralith (ores) | Biomes O' Plenty (ores) | Oritech (fluids in its tanks) |
|---|---|---|---|---|---|---|---|
| 1.21.1 | ✓ 15.10.6 (SCG) | ✓ 1.120.2 (SCG) | ✓ 19.57.0.450 (C) | ✓ (S) | ✓ (S) | ✓ (S) | ✓ (SCG) |
| 1.21.2 | ✓ 16.0.1 (C) ¹ | – | – | – | – | – | – |
| 1.21.3 | ✓ 16.0.4 (SCG) | – | – | – | – | – | – |
| 1.21.4 | ✓ 17.3.0 (SCG) | ✓ 1.115.1 (SG) ¹ | ✓ 20.0.0.4 (C) | – | – | – | – |
| 1.21.5 | ✓ 18.2.0 (SCG) | – | ✓ 21.4.0.27 (C) | – | – | – | – |
| 1.21.6 | ✓ 19.1.1 (SCG) | – | – | – | – | – | – |
| 1.21.7 | ✓ 19.1.1 (SCG) | ✓ 1.116.1 (SCG) | ✓ 23.1.0.8 (C) | – | – | – | – |
| 1.21.8 | ✓ 19.1.1 (SCG) | ✓ 1.116.1 (SCG) | ✓ 24.2.0.6 (C) | – | – | – | – |
| 1.21.9 | ✓ 20.0.5 (SCG) | – | ✓ 25.0.1.4 (C) | – | – | – | – |
| 1.21.10 | ✓ 20.0.5 (SCG) | – | ✓ 26.3.0.31 (C) | – | – | – | – |
| 1.21.11 | ✓ 21.1.7 (SCG) | ✓ 1.117.1 (SCG) | ✓ 27.44.0.104 (C) | – | – | – | – |
| 26.1 | ✓ 26.1.10 (SCG) | – | ✓ 29.2.0.21 (C) | – | – | – | – |
| 26.1.1 | ✓ 26.1.10 (SCG) | – | ✓ 29.4.0.23 (C) | – | – | – | – |
| 26.1.2 | ✓ 26.1.10 (SCG) | ✓ 1.120.0 (SCG) | ✓ 29.43.0.106 (C) | – | – | – | – |
| 26.2 | ✓ 26.2.10 (SCG) | ✓ 1.120.2 (SCG) | ✓ 30.39.0.232 (C) | – | – | – | – |
| 26.3 | ✓ 26.3.1 (SCG) | blocked ¹ | ✓ 31.8.0.53 (C) | – | ✓ (S) | ✓ (S) | – |

¹ Notes:

* 1.21.2 Fabric, Jade (gametest, server not run): Jade 16.0.0/16.0.1 (the only Jade builds for 1.21.2) crash every dedicated server on their own: Jade.loadComplete calls WailaClientRegistration.getConfigKeys() unconditionally and loads client classes (seen in the Pipster project). Tested on the client only.
* 1.21.2 NeoForge, Jade (gametest, server not run): Jade 16.0.0/16.0.1 (the only Jade builds for 1.21.2) crash every dedicated server on their own: Jade.loadComplete calls WailaClientRegistration.getConfigKeys() unconditionally and loads client classes (seen in the Pipster project). Tested on the client only.
* 1.21.4 NeoForge, CC: Tweaked (client not run): Client blocked by the partner: CC: Tweaked 1.115.1 (latest for 1.21.4) crashes the NeoForge 21.4.158 client on its own while firing RegisterRenderStateModifiersEvent (IllegalArgumentException: ? extends ItemFrame does not match expected type parameter Entity in computercraft), before any QuantaVolt integration code runs (seen 2026-10-02). Server and GameTest runs work.
* 26.3 NeoForge, CC: Tweaked: Blocked: CC: Tweaked 1.120.3 (latest for 26.3, 2026-09-28) is built for an older NeoForge 26.3 beta and fails to load on the pinned NeoForge 26.3.0.37-beta while CC itself loads (NoSuchFieldError ModConfig$Type.SERVER in CC's mod constructor ComputerCraft.<init>), before any QuantaVolt integration code runs. Re-test when CC: Tweaked updates.

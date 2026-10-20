# Advancements

Since 0.2.0 QuantaVolt has its own advancement tab, **QuantaVolt**, with 29 advancements (the tab's root included)
along the way from the first dynamo to the Dimensional Store.

## How they are earned

* **By getting an item:** the root, *Blueprint*, *Yellow Cake* and *Safety First* are earned the moment the item is in
  your inventory (crafted, picked up or taken from a machine).
* **Awarded by the server:** all others are earned through an event in the world. The server gives them to **every
  player within 32 blocks** of the plant's controller at that moment, so everyone who builds together gets them:
  * *a plant forms* (each plant has its own advancement; Solar Array, Solar Thermal Field and Wind
    Turbine share *Free Energy*),
  * *It Flows* and *Pure Oxygen* while the machine runs (checked every 5 seconds),
  * *By the Book* when a plant forms while its [Build Projector](Build-Projector) projection is switched on,
  * *Close Call* when an incident happens.
* *Under Your Feet* goes only to the player who used the [Gas Prospector](Natural-Gas#gas-prospector) on a region with
  a field.

A data pack may remove advancements; QuantaVolt then simply awards nothing for them.

## The tree

Each advancement is shown under its parent. The type (task, goal, challenge) is the frame in the advancement screen.

| Advancement | Type | How to earn it |
|---|---|---|
| **QuantaVolt** (root) | task | Have a Basic Dynamo in your inventory. |
| ├ **Under Steam** | task | Build an Industrial Boiler. |
| │ ├ **Full Speed** | task | Build a Steam Turbine. |
| │ │ └ **Yellow Cake** | task | Have Yellowcake in your inventory. |
| │ │ &nbsp;&nbsp;└ **Spin It** | task | Build a Centrifuge Cascade. |
| │ │ &nbsp;&nbsp;&nbsp;&nbsp;└ **Chain Reaction** | goal | Build a Fission Reactor. |
| │ │ &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├ **Safety First** | task | Have all four parts of the radiation suit in your inventory (hood, jacket, trousers, boots). |
| │ │ &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└ **Star Fire** | goal | Build a Tokamak. |
| │ │ &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└ **A Sun of Your Own** | challenge | Build a Little Star. |
| │ │ &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└ **Event Horizon** | challenge | Build a Micro Black Hole Plant. |
| │ │ &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└ **Hawking Was Right** | goal | Build a Hawking Radiation Reactor. |
| │ │ &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└ **Pocket Universe** | challenge | Build a Dimensional Store. |
| │ └ **Coal Becomes Gas** | task | Build a Gasifier. |
| │ &nbsp;&nbsp;├ **Turbine Hall** | task | Build a Gas Turbine. |
| │ &nbsp;&nbsp;│ └ **Pure Oxygen** | goal | Run a Gas Turbine, Gas Engine or Industrial Boiler on oxygen ([oxyfuel](Energy-Fluids-Gases#oxyfuel)). |
| │ &nbsp;&nbsp;└ **Cylinder by Cylinder** | task | Build a Gas Engine. |
| ├ **Under Your Feet** | task | Find a natural gas field with the Gas Prospector. |
| │ └ **Drill, Baby** | task | Build a Gas Derrick. |
| │ &nbsp;&nbsp;├ **It Flows** | goal | Extract natural gas with a Gas Derrick. |
| │ &nbsp;&nbsp;└ **Gasometer** | task | Build a Large Gas Tank. |
| ├ **Free Energy** | task | Build a Solar Array, Solar Thermal Field or Wind Turbine. |
| ├ **Charged** | task | Build a Capacitor Bank. |
| │ ├ **Battery Park** | task | Build a Battery Hall. |
| │ │ └ **Superconducting** | goal | Build an SMES. |
| │ ├ **Keep It Warm** | task | Build a Molten-Salt Store. |
| │ └ **Heavy Lifting** | task | Build a Gravity Store. |
| ├ **Blueprint** | task | Have a Build Projector in your inventory. |
| │ └ **By the Book** | goal | Finish a plant while its projection shows. |
| └ ***(hidden)*** | challenge | See below. |

"Build" always means: the plant forms while you are within 32 blocks of its controller.

## The hidden advancement

One advancement is **hidden**: it does not appear in the tab until you earn it. It is a challenge, a child of the root,
and it is called **Close Call**: be within 32 blocks of a plant's controller when one of its incidents happens (see
[Safety and Incidents](Safety-and-Incidents)). With the server option `safeMode` incidents are only shutdowns, and
*Close Call* cannot be earned.

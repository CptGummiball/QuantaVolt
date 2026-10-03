# QuantaVolt API for mod developers

API version **1** · package `dev.cptgummiball.quantavolt.api` · mod id `quantavolt`

**Most mods need nothing from this page** if QuantaVolt uses the standard loader interfaces.

## Getting the API

`quantavolt-api-1.jar` and `quantavolt-api-1-javadoc.jar` from the [releases](../../../releases),
as a **compile-only** dependency. Do not ship the API or any QuantaVolt files in your mod. If
QuantaVolt is optional for your mod, check that the mod `quantavolt` is loaded before touching its
classes.

The license (section 5) allows compiling against the API and publishing mods that use it.

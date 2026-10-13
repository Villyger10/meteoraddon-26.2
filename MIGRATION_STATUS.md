# Minecraft 26.2 migration status

This is a source-level migration attempt based on the supplied `meteor-client-26.2-35.jar`. It is **not yet a verified successful build**.

## Confirmed from the supplied Meteor JAR
- Its `fabric.mod.json` identifies Meteor Client `26.2-35`, targeting Minecraft `~26.2`, Java `>=25`, and Fabric Loader `>=0.19.3`.
- Its manifest reports Minecraft `26.2`, Fabric Loader `0.19.3`, and official Minecraft mapping namespace.
- Meteor's compiled `Command` API expects `LiteralArgumentBuilder<ClientSuggestionProvider>`.
- Meteor's compiled 3D renderer exposes `box(AABB, Color, Color, ShapeMode, int)`.

## Changes made
- Uses the configured Loom version property.
- Removed the missing Yarn mappings artifact/property dependency for this official-mapping target.
- Targets Java 25 and requires Java 25 in mod metadata.
- Updates the command source generic to `ClientSuggestionProvider`.
- Replaces Yarn-named `Box`/`BlockPos` code with `net.minecraft.world.phys.AABB`.
- Adds the supplied Meteor Client JAR under `libs/` and pins the compile dependency to that exact file.
- Removes the example mixin, which only logged from an outdated Minecraft client constructor and was not needed by the example addon features.
- Removes the old Minecraft `1.21.9` metadata compatibility entry.

## Not yet verified
- A full Gradle build has not succeeded in this environment because the Gradle distribution and game dependencies require network downloads, and network/DNS access is unavailable here.
- The exact Minecraft 26.2 API signatures for all source usages have not been checked by a full compiler.
- The supplied Meteor JAR is included for compilation; the player still needs the matching Meteor Client installed in their Minecraft instance.
- Local JAR dependency wiring can vary with Loom's remapping behavior. If Gradle reports mapping or classpath issues, use the compiler output to refine the setup.

Treat this ZIP as a migration work-in-progress, not a guaranteed ready-to-run addon.

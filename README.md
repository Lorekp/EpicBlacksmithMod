# Epic Blacksmith

An early Minecraft Forge mod prototype that adds Sapphire and Raw Sapphire as custom items. It establishes item registration, creative inventory integration, and item resources for a possible blacksmithing mod.

## Implemented features

- `eblacksmith:sapphire` and `eblacksmith:sapphire_raw`, registered using Forge's deferred item registry.
- Both items appear in the Ingredients creative inventory tab.
- English display names, generated item models, and PNG textures.

The items currently use ordinary `Item` behavior. There are no crafting or smelting recipes, ore generation, custom tools, workstations, or blacksmithing progression. Survival acquisition is not implemented.

## Development setup

Use JDK 17 and the included Gradle wrapper. The build targets Minecraft **1.20.2** with Forge **48.0.30**; the wrapper downloads Gradle **8.1.1**. Initial setup requires internet access to download Gradle, Forge, Minecraft development dependencies, and mappings. Gradle is configured with a 3 GB maximum heap.

From a checkout, run in PowerShell:

```powershell
.\gradlew.bat build
.\gradlew.bat runClient
```

On macOS or Linux, use `bash ./gradlew build` and `bash ./gradlew runClient`.

The build produces the mod JAR under `build/libs/`. The development client uses `run/` as its working directory. In a creative world, look for Sapphire and Raw Sapphire in Ingredients. With commands enabled, the item IDs can also be used directly:

```text
/give @s eblacksmith:sapphire
/give @s eblacksmith:sapphire_raw
```

**Build caveat:** `gradle.properties` selects Parchment mappings `2023.06.26-1.20.1` while targeting Minecraft 1.20.2. Compatibility of that combination needs verification. ForgeGradle and the Parchment plugin also use version ranges, so dependency resolution is not fully pinned.

## Source layout

| Path | Purpose |
| --- | --- |
| `src/main/java/de/lorekp/blacksmithmod/BlacksmithMod.java` | Forge entry point, registry hookup, and creative tab population |
| `src/main/java/de/lorekp/blacksmithmod/item/ModItems.java` | Sapphire item registrations |
| `src/main/resources/assets/eblacksmith/` | Item names, models, and textures |
| `src/main/resources/META-INF/mods.toml` | Mod metadata and dependency declarations |
| `gradle.properties` | Mod identity and dependency versions |
| `build.gradle` | Java toolchain, Forge development runs, resource expansion, and JAR packaging |

## Checks and status

There are no project tests or CI workflows. The build includes the standard Forge GameTest server configuration, but no GameTests are registered; it is not a working test suite. A useful manual check is to launch the client, verify both creative tab entries, and confirm their names and textures render correctly.

## Credits and license

Mod metadata names **Lorekp** as author and declares **All Rights Reserved**. No standalone license file is included, and `attributions.txt` is empty. The build and lifecycle scaffolding follow the Forge development template; Minecraft, Forge, Parchment, and Gradle remain their respective projects. The repository does not document the provenance of the item textures.

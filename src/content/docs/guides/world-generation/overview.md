---
title: Overview world generation
description: Gives an overview about server configuration.
---

## world generation in SteelMC

to generate chunk it use the trait [`ChunkGenerator`](https://steel-foundation.github.io/SteelMC/steel_core/chunk/chunk_generator/trait.ChunkGenerator.html) with the vanilla equivalent being the abstract class [`ChunkGenerator`](https://mcsrc.dev/1/1.21.11_unobfuscated/net/minecraft/world/level/chunk/ChunkGenerator).
steel have a pretty much a 1:1 convertion between function name so:

- [`create_structures`](https://steel-foundation.github.io/SteelMC/steel_core/chunk/chunk_generator/trait.ChunkGenerator.html#tymethod.create_structures) are... don't know.
- [`create_biomes`](https://steel-foundation.github.io/SteelMC/steel_core/chunk/chunk_generator/trait.ChunkGenerator.html#tymethod.create_biomes) are [`createBiomes`](https://mcsrc.dev/1/1.21.11_unobfuscated/net/minecraft/world/level/chunk/ChunkGenerator#L120) so the [Biomes step](https://minecraft.wiki/w/World_generation#Biomes).
- [`fill_from_noise`](https://steel-foundation.github.io/SteelMC/steel_core/chunk/chunk_generator/trait.ChunkGenerator.html#tymethod.fill_from_noise) are [`fillFromNoise`](https://mcsrc.dev/1/1.21.11_unobfuscated/net/minecraft/world/level/chunk/ChunkGenerator#L636) so the [Terrain/Noise step](https://minecraft.wiki/w/World_generation#Terrain).
- [`build_surface`](https://steel-foundation.github.io/SteelMC/steel_core/chunk/chunk_generator/trait.ChunkGenerator.html#tymethod.build_surface) are [`buildSurface`](https://mcsrc.dev/1/1.21.11_unobfuscated/net/minecraft/world/level/chunk/ChunkGenerator#L429) so the [Surface step](https://minecraft.wiki/w/World_generation#Surface).
- [`apply_carvers`](https://steel-foundation.github.io/SteelMC/steel_core/chunk/chunk_generator/trait.ChunkGenerator.html#tymethod.apply_carvers) are [`applyCarvers`](https://mcsrc.dev/1/1.21.11_unobfuscated/net/minecraft/world/level/chunk/ChunkGenerator#L129) so the [Carvers step](https://minecraft.wiki/w/World_generation#Carvers).
- [`apply_biome_decorations`](https://steel-foundation.github.io/SteelMC/steel_core/chunk/chunk_generator/trait.ChunkGenerator.html#tymethod.apply_biome_decorations) are [`applyBiomeDecoration`](https://mcsrc.dev/1/1.21.11_unobfuscated/net/minecraft/world/level/chunk/ChunkGenerator#L319) so the [Feature step](https://minecraft.wiki/w/World_generation#Features).

But a difference to notice is we don't need to create a thread, the thread are already create before and are manage by steel (so don't need to account about `CompletableFuture.supplyAsync`).

"Vanilla" generation also use datapack include and use by default who are execute by [`NoiseBasedChunkGenerator`](https://mcsrc.dev/1/1.21.11_unobfuscated/net/minecraft/world/level/levelgen/NoiseBasedChunkGenerator) but in steel we hardcode it for performance so each world gen are a variant in [`ChunkGeneratorType`](https://steel-foundation.github.io/SteelMC/steel_core/chunk/world_gen_context/enum.ChunkGeneratorType.html).

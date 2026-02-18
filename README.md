# mupencheat

An updated `mupencheat.txt` for Mupen64Plus with GameShark cheats that are missing from the standard file.

## What's new

### GoldenEye 007 (U) - Universal codes via MIPS code injection

The original cheat file had basic per-level GameShark codes or a single universal infinite health hack. We reverse-engineered the player struct pointer (stored at `0x80089EE0`) and confirmed consistent field offsets across all levels:

| Field | Struct offset | Purpose |
|---|---|---|
| Y-velocity | `0x7C` | Moonjump |
| Health | `0xDC` | Infinite health |
| X collision | `0x48D` | No-clip |
| Z collision | `0x495` | No-clip |

Using that, we wrote MIPS assembly code caves that hook the game at `0x800C0F4` and work on every level without needing separate codes per stage. The result is 5 cheats under the **"All Levels P1 (enable only one)"** submenu:

- **Infinite Health** - you simply don't die
- **Moonjump (hold B)** - hold B to fly upward after stepping off an edge
- **No-clip (hold L)** - hold L to pass through walls, release to restore collision
- **Infinite Health + Moonjump (hold B)** - both
- **Infinite Health + Moonjump + No-clip (hold B + L)** - the kitchen sink

These all share one hook point, so only enable one at a time. The submenu naming makes this obvious.

## Why

The biggest gaps in the existing GoldenEye cheat database were moonjump and proper no-clip. Both existed as giant lists of per-level GameShark codes in old FAQs from the late 90s, but nobody had consolidated them into universal codes that just work regardless of what level you're playing. Now they do.

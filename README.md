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

The biggest gaps in the existing GoldenEye cheat database were moonjump and proper no-clip. Both existed as massive per-level GameShark code lists in late-90s FAQs, but nobody had consolidated them into universal codes that just work regardless of what level you're playing. Now they do.

## How to use this

1. Click the green **Code** button at the top of this page, then **Download ZIP**
2. Unzip it - you'll get a folder with `mupencheat.txt` inside
3. Find your emulator's existing `mupencheat.txt` and rename it to `mupencheat.txt.backup` (just in case)
4. Drop the new `mupencheat.txt` into that same folder

Where to find your existing file depends on your setup:

- **macOS / Linux**: `~/.local/share/mupen64plus/mupencheat.txt`
- **Windows**: Same folder as the Mupen64Plus `.exe`, or `%APPDATA%\Mupen64Plus\`
- **RetroArch (mupen64plus-next core)**: Inside RetroArch's `system` folder

If you can't find it, just search your computer for `mupencheat.txt` - there should already be one from your emulator install.

Once replaced, open your emulator, load GoldenEye 007 (U), and check the cheats menu. The new codes show up under **"All Levels P1 (enable only one)"**. Only turn on one from that group at a time - they all modify the same spot in memory, so enabling two will break both. Just pick the combo you want.

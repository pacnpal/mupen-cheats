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

Using that, we wrote MIPS assembly code caves that hook the game at `0x800C0F4` and work on every level without needing separate codes per stage. The result is 7 cheats under the **"All Levels P1 (enable only one)"** submenu - every possible combination of the three features:

- **Infinite Health** - you simply don't die
- **Moonjump (hold B)** - hold B to fly upward after stepping off an edge
- **No-clip (hold L)** - hold L to pass through walls, release to restore collision
- **Infinite Health + Moonjump (hold B)** - health + moonjump
- **Infinite Health + No-clip (hold L)** - health + no-clip
- **Moonjump + No-clip (hold B + L)** - moonjump + no-clip
- **Infinite Health + Moonjump + No-clip (hold B + L)** - the kitchen sink

These all share one hook point, so only enable one at a time. The submenu naming makes this obvious.

### Perfect Dark (U) v1.0 / v1.1 - Additional single-player cheats

The original cheat file already had the basics (All Weapons, Infinite Ammo, Infinite Health, Infinite Shield, Moon Jump). We added 6 new Hi-Res codes under the **"Miscellaneous (Hi-Res)"** submenu:

- **Walk Through Most Doors** - pass through most locked doors
- **Walk Through Some Other Doors** - pass through some other doors
- **Walk Through Other Doors** - pass through other doors
- **Almost No Collisions** - removes most prop and environment collisions
- **Infinite Ammo All Clips** - keeps all weapon magazines full (no reloading)
- **X-Ray Scope All Weapons** - press L/R to use X-Ray scope with any weapon

The door codes each affect different door types. Only enable one door code at a time. These are Hi-Res mode codes only. Both v1.0 and v1.1 ROM versions are covered with identical codes.

## Why

The standard `mupencheat.txt` that ships with Mupen64Plus has decent coverage but notable gaps - missing moonjump/no-clip for GoldenEye, and missing door bypass/collision removal for Perfect Dark. These codes existed in scattered late-90s GameShark FAQs but were never consolidated into the standard cheat file. Now they are.

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

Once replaced, open your emulator, load a supported game, and check the cheats menu. The new codes will appear in their respective submenus.

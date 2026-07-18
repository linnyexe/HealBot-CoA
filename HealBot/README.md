# HealBot CoA Patch

**HealBot 3.3.5.4 patched for [Conquest of Azeroth](https://ascension.gg) (WoW Ascension)**

Adds support for all 21 custom classes on the Conquest of Azeroth (CoA) server.

## What This Fixes

HealBot 3.3.5.4 crashes on load when running CoA because `HealBot_Update_Skins()` calls `pairs(HealBot_GlobalsDefaults.WatchHoT[class])` where `class="CULT"` (first 4 chars of CULTIST). The WatchHoT table only contains 10 standard WoW classes, so `pairs(nil)` crashes Lua and kills the entire addon init - no panel ever shows.

## Changes Made

### Core Fix (nil-guard + auto-create)
- **HealBot.lua** — Nil guard on `pairs()` call in `HealBot_Update_Skins()`, auto-create `WatchHoT[class]` if missing, nil guard in `HealBot_configClassHoT`

### 21 Custom Classes Added
| Class | Abbrev | Class ID |
|-------|--------|----------|
| Barbarian | BARB | 12 |
| Witch Doctor | WITC | 13 |
| Felsworn | FELS | 14 |
| Witch Hunter | WITC | 15 |
| Stormbringer | STOR | 16 |
| Knight of Xoroth | XORO | 17 |
| Guardian | GUAR | 18 |
| Templar | TEMP | 19 |
| Bloodmage | BLMG | 20 |
| Ranger | RANG | 21 |
| Chronomancer | CHRO | 22 |
| Necromancer | NECR | 23 |
| Pyromancer | PYRO | 24 |
| Cultist | CULT | 25 |
| Starcaller | STAR | 26 |
| Sun Cleric | SUNC | 27 |
| Tinker | TINK | 28 |
| Primalist | PRIM | 31 |
| Reaper | REAP | 30 |
| Venomancer | VENO | 29 |
| Runemaster | RUNE | 32 |

> Note: Witch Hunter and Witch Doctor share the `WITC` abbreviation (both purple in RAID_CLASS_COLORS).

### Per-File Details
- **HealBot_Data.lua** — 21 custom classes in `HealBot_Class_En`, empty `WatchHoT` tables, `HoTReserve`
- **HealBot_Panel.lua** — 21 custom classes in `HealBot_ClassIconCoord` (DEFAULT icon fallback)
- **HealBot_Options.lua** — Nil guard in `InitBuffClassList`, empty entries in `Buff_Spells_Total_List` and `Debuff_Spells`, nil-guarded `WatchHoT` access in `_Refresh` and `_OnSelect`
- **HealBot_Action.lua** — 21 class colors in `hbClassCols` (sourced from CoA client's `RAID_CLASS_COLORS`), gray fallback for unknown classes

### Extra Features
- **BG Flag Carrier Icon** — Standalone `UNIT_AURA` event frame (`HealBot_CoA_FlagFrame`) that displays a flag icon on HealBot bars when a player is carrying Horde/Alliance flag. Works by matching buff name ("Horde Flag" / "Alliance Flag") since CoA returns nil for spell ID in UnitAura's 10th parameter.
- **Universal Range Check** — Added catch-all in `HealBot_Action_SetrSpell()` that scans `HealBot_Globals.Spell` table for first known spell, with nil guard for early init when Globals.Spell doesn't exist yet. Prevents custom classes from falling back to Heavy Runecloth Bandage (~15yd range).

## Installation

1. Download or clone this repo
2. Copy the **HealBot** folder into your `Interface/AddOns/` directory
3. Delete any existing HealBot folder first if upgrading
4. Launch the game

## Known Limitations

- General tab in options still shows standard WoW classes (cosmetic only, too many XML refs to patch)
- HoT/shield buff icons don't display for custom class spells (needs spell IDs from CoA devs)
- Emergency filter checkboxes missing for custom classes
- Talent calculator data may be missing alternate choice nodes for some talents

## Credits

- **HealBot** by Strife (original 3.3.5.4)
- **CoA patch** by Linny / Sean
- **Class data** sourced from Conquest of Azeroth client's `RAID_CLASS_COLORS`

## License

HealBot is open source under its original license. This patch is provided as-is.

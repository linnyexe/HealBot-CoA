# HealBot CoA Patch

**HealBot 3.3.5.4 patched for [Conquest of Azeroth](https://ascension.gg)**

## Download
Click the green **Code** button → **Download ZIP**, extract, and copy the `HealBot` folder into your `Interface/AddOns/` directory.

## What This Fixes
HealBot 3.3.5.4 crashes on load in CoA because `pairs(nil)` is called on custom class WatchHoT entries that don't exist in the defaults. This patch adds all 21 custom classes, nil-guards the crash points, and includes extra features for BG flag carriers and universal range checking.

See `HealBot/README.md` for full documentation, changelog, and class list.

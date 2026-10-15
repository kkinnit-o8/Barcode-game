# STOCK DEFENSE

A Bloons-style tower defense where the barcode scanner is the only controller. The groceries have come alive and are riding the conveyor belt to the exit without paying. Build scanners along the belt and scan them all before they get out.

Play it at **https://kkinnit-o8.github.io/Barcode-game/stock-defense/**, or open the [Scanner Games](../README.md) home page and scan its card.

Like every game on the site, it is a single `index.html` with no libraries, fonts or network requests, built for the SuSoft POS terminal (Android 7.1.2, Chrome 119).

## How to play

1. Scan **EASY**, **NORMAL** or **HARD** on the title screen, then scan your name (or **NEW PLAYER** and spell it). Scan **ALL GAMES** or press Esc to go back to the arcade.
2. Every empty pad on the map has a barcode under it. Scan a pad, then scan the scanner you want to build there from the list on the right.
3. Scan **GO** to send the next round down the belt. During a round, scanning **GO** again switches between 1×, 2× and 3× speed.
4. Each scan peels one layer off an item: an energy drink becomes chips, chips become soda, and so on down to gum. Every layer is worth $1. Upgraded scanners that do more damage keep going: a 7-damage label that pops a twin pack also hits both energy drinks inside.
5. Anything that reaches the **EXIT** costs lives, one per layer it still has. The game ends when you run out of lives.
6. Scan a scanner you already built to upgrade it, change what it aims at (**TARGET**: first, last, strong or close), or **SELL** it for 70% of what you spent.
7. You get $100 + the round number after every round. Survive all the rounds to win, then keep going in **FREEPLAY**.

The panel on the right always shows what the next round brings, with a warning when it has items that need a special scanner.

Scan **PAUSE** (top right) to stop at any time. The pause menu also has **RESTART**, **QUIT** and **AUTO-START**, which starts each round by itself after a short break.

## The groceries

| Item | Speed | Inside | Notes |
|---|---|---|---|
| Gum | 1 | – | |
| Candy | 1.4 | Gum | |
| Soda | 1.8 | Candy | |
| Chips | 3.2 | Soda | Fast |
| Energy drink | 3.5 | Chips | Fastest |
| Twin pack | 1.8 | 2 energy drinks | |
| Frozen pizza | 2 | 2 energy drinks | Freezers can't freeze it |
| Smudged box | 1 | 2 twin packs | Only price guns, label bombs and scanners that read smudged barcodes can hurt it |
| Multipack | 1.8 | Twin pack + frozen pizza | |
| Gift box | 2.2 | 2 multipacks | |
| Crate | 2.5 | 2 gift boxes | Takes 10 hits, worth $10 |
| Pallet | 1 | 4 crates | Takes 200 hits, worth $80. Freezers can't freeze it |
| Cart King | 0.3 | 4 pallets | The boss: 700 hits, worth $300 |

Two extra tags can appear on any item:

- **Hidden** (see-through): only scanners near a Security Cam, or upgraded with Night Scope or 2D Imager, can see it.
- **Restock** (green +): grows a layer back every 2.5 seconds it isn't hit.

From round 51 on, crates, pallets and carts get tougher every round.

## The scanners

Each scanner has two upgrade paths, three tiers each. Take one path to tier 3 and the other no higher than tier 1, or take both paths to tier 2.

| Scanner | Cost | Does | Path 1 | Path 2 |
|---|---|---|---|---|
| Handheld | $200 | Fires laser bolts | Quick Trigger, Twin Beam, Laser Shotgun | Long Range, Sharp Laser, 2D Imager (sees hidden, reads smudged) |
| Flatbed | $300 | Shoots 8 beams at once | Fast Motor, More Lines, Scan Tunnel (burns everything in range) | Wide Glass, Hot Beams, Blue Lasers (reads smudged, 2× vs crates) |
| Price Gun | $350 | Hits anything anywhere on the map, reads smudged | Full Auto, Night Scope (sees hidden), Machine Labeler | Heavy Labels, Price Slash (2× vs crates), Clearance (stuns pallets) |
| Label Bomb | $520 | Exploding label rolls, reads smudged | Bigger Rolls, Heavy Print, Paper Storm | Fast Feed, Sticky Labels (slows), Pallet Buster (4× vs crates and pallets) |
| Freezer | $350 | Freezes everything close by | Deep Freeze, Frost Bite, Absolute Zero (slows pallets) | Wide Vents, Chill Zone (slows), Blizzard (freezes pizza) |
| Security Cam | $450 | Scanners near it see hidden items | Wide Angle, Motion Tracking (+20% fire rate), AI Analytics (+1 damage, reads smudged) | Alarm (slows items), Spotlight (+15% range), Lockdown (stuns everything in range) |
| Self-Checkout | $900 | Earns $80 every round | More Lanes, Express Lane, Superstore (+$500 a round) | Loyalty Cards (+5% cash per scan), Bulk Deals (×1.4 round income), Stock Market (8% interest) |

Upgrade prices and descriptions are shown in the game when you scan a scanner.

## Difficulty

| | Rounds | Lives | Prices | Items per round | Score |
|---|---|---|---|---|---|
| Easy | 30 | 200 | −15% | −30% | ×0.6 |
| Normal | 40 | 150 | normal | −15% | ×1 |
| Hard | 50 | 100 | +8% | full | ×1.5 |

Everyone starts with $650.

## Leaderboard

Players are shared with the other games on the site, so the name you picked in HELLSCAN is already there.

- Players are ranked by the most rounds cleared, then by score. Score is one point per layer scanned plus 50 per round cleared, times the difficulty multiplier.
- Scan **LEADERBOARD** on the title screen to see everyone's best game, and **THIS WEEK** for games since Monday.
- The top players also show on the game's card on the arcade home page.

## Scanner requirements

- Scanner in keyboard (HID / keyboard-wedge) mode, with **Code 128** enabled.
- An Enter or Tab suffix is optional. Prefix and suffix characters are ignored.
- On a touchscreen, tapping a barcode works too.
- The layout keeps every barcode readable down to 1024×768. On 4:3 screens the game gets black bars above and below.

## URL options

| Option | Default | Use it when |
|---|---|---|
| `?module=3` | `2` | Barcodes are hard to read. This is the narrowest bar width in CSS pixels; larger values give bigger barcodes. |
| `?digits=6` | `4` | The scanner rejects short Code 128 barcodes (minimum-length setting). Must be an even number from 4 to 12. |
| `?nofs` | off | You don't want fullscreen on start. |
| `?debug` | off | You want to see FPS, frame time and the digits under each barcode. |

With `?module` or `?digits` on a smaller screen, the pad barcodes get wider than the space between pads, so every other one moves down a little. They overlap slightly but each one stays readable.

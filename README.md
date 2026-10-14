# HELLSCAN

A Doom-style shooter where the barcode scanner is the only controller. Every demon carries a Code 128 barcode; scan it to shoot it.

Built for a SuSoft POS terminal (Android 7.1.2, Chrome 119, RK3399), so it is a single `index.html` with no libraries, fonts or network requests.

## How to play

1. Open the page and scan **EASY**, **NORMAL** or **HARD** on the title screen.
2. Scan your name on the **Who's playing?** screen. The first time, scan **NEW PLAYER** and spell your name by scanning letters, then **DONE**.
3. You walk through the store automatically. When you reach a room, demons teleport in.
4. Scan a demon's barcode to shoot it. Big demons take several hits, and their barcode changes after each one.
5. A tag flashing yellow or red means that demon (or fireball) is about to hurt you. Shoot it first. Hitting a demon interrupts its attack.
6. Scan a **medkit** (green tag) for +25 health, **armor** (blue) for +50 armor, and a **barrel** (orange) to blow up the demons near it.
7. Clear 6 rooms. The last one has a boss. Levels repeat with new themes and get harder each time.

Scan **PAUSE** in the status bar to stop at any time (for example, when a customer shows up). Esc also pauses.

## Leaderboard

Everyone who plays on the same machine competes on one leaderboard.

- Scan **LEADERBOARD** on the title screen to see each player's best game. Scan **THIS WEEK** to switch to scores since Monday.
- During a game, the top-right corner shows who you need to beat next (`NEXT: OLA 12345`) and announces it when you pass them.
- The game-over screen shows your personal best and your rank, and how far you are behind the player above you.
- Points are multiplied by difficulty (Easy ×0.6, Normal ×1, Hard ×1.5), so everyone can share one board.

Scores are stored in the browser on that machine. Clearing Chrome's site data for the game resets the board.

## Loot crates

Gold-tagged **supply crates** sometimes appear. Demons can drop them, a cleared room may leave one behind, and the boss always drops a **Warlord chest** with better odds. Scan a crate to pause the game and see three items. Scan the one you want.

| Rarity | Item | Type | Effect |
|---|---|---|---|
| Common | Medpack | Item | Heals 35 health when used |
| Common | Armor plate | Instant | +35 armor |
| Common | Coupon | Instant | +1500 points |
| Common | Energy drink | Item | Demons move and attack at half speed for 8 s |
| Uncommon | Frost grenade | Item | Freezes all demons and fireballs for 6 s |
| Uncommon | Regen patch | Perk | Heal 1 health every 3 s while fighting |
| Uncommon | Loyalty card | Perk | +25% points |
| Uncommon | Thick skin | Perk | Take 20% less damage |
| Rare | Force field | Item | Nothing can hurt you for 7 s |
| Rare | Pipe bomb | Item | 3 damage to every demon in the room |
| Rare | Vampire laser | Perk | +2 health per kill |
| Rare | Double tap | Perk | Every scan does +1 damage |
| Epic | Nuke | Item | Kills every demon in the room (bosses take 6) |
| Epic | Lucky charm | Perk | More crates and rarer loot |
| Epic | Mega kit | Instant | Full health and full armor |
| Legendary | Extra life | Perk | Come back once with full health |
| Legendary | Golden scanner | Perk | Triple damage and +50% points |

- **Items** go in your backpack, shown in the bottom corners of the screen (2 slots). Scan an item's barcode to use it. If both slots are full, a new item replaces the oldest one.
- **Perks** last for the rest of the game. Most stack 2–3 times (Golden scanner only once). Their icons are in the top-right corner.
- **Instant** items work as soon as you pick them.

## Play it

**https://kkinnit-o8.github.io/Barcode-game/**

<img src="qr-code.png" alt="QR code linking to https://kkinnit-o8.github.io/Barcode-game/" width="240">

`qr-code.svg` is the same QR code as a vector file, for printing at any size.

## Publishing with GitHub Pages

The repo is already set up for Pages: `index.html` is at the root, and `.nojekyll` tells GitHub to serve the files as-is. To switch it on once:

1. Open the repo on GitHub and click **Settings**.
2. In the left sidebar, click **Pages**.
3. Under **Build and deployment → Source**, choose **Deploy from a branch**.
4. Under **Branch**, choose **`main`** and **`/ (root)`**, then click **Save**.
5. Wait 1–2 minutes. The **Actions** tab shows a "pages build and deployment" run, and the Pages screen then says *"Your site is live at …"*.
6. Open the link (or scan the QR code above) in Chrome on the POS terminal.

Every later push to `main` republishes the site automatically.

## Scanner requirements

- Scanner in keyboard (HID / keyboard-wedge) mode, with **Code 128** enabled. The existing Barcode Arcade already works this way.
- An Enter or Tab suffix is optional. Prefix and suffix characters are ignored.
- Scanners that type through an Android input method also work, through a hidden input field that is kept focused without opening the on-screen keyboard.

## URL options

| Option | Default | Use it when |
|---|---|---|
| `?module=3` | `2` | Barcodes are hard to read. This is the narrowest bar width in CSS pixels; larger values give bigger barcodes. |
| `?digits=6` | `4` | The scanner rejects short Code 128 barcodes (minimum-length setting). Must be an even number from 4 to 12. |
| `?res=180` | `216` | You want a lower internal resolution, for speed or a chunkier look. |
| `?nofs` | off | You don't want fullscreen on start. |
| `?touch` | off | You want tapping a tag to shoot it, for testing without a scanner. |
| `?debug` | off | You want to see FPS, frame time and the digits under each tag. Typing the digits and pressing Enter also works. |

Options can be combined: `index.html?module=3&digits=6`.

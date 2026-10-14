# HELLSCAN

A Doom-style shooter where the barcode scanner is the only controller. Every demon carries a Code 128 barcode; scan it to shoot it.

Built for a SuSoft POS terminal (Android 7.1.2, Chrome 119, RK3399), so it is a single `index.html` with no libraries, fonts or network requests.

## How to play

1. Open the page and scan **EASY**, **NORMAL** or **HARD** on the title screen.
2. You walk through the store automatically. When you reach a room, demons teleport in.
3. Scan a demon's barcode to shoot it. Big demons take several hits, and their barcode changes after each one.
4. A tag flashing yellow or red means that demon (or fireball) is about to hurt you. Shoot it first. Hitting a demon interrupts its attack.
5. Scan a **medkit** (green tag) for +25 health, **armor** (blue) for +50 armor, and a **barrel** (orange) to blow up the demons near it.
6. Clear 6 rooms. The last one has a boss. Levels repeat with new themes and get harder each time.

Scan **PAUSE** in the status bar to stop at any time (for example, when a customer shows up). Esc also pauses. Scores are saved on the device (top 10).

## Putting it on the machine

The game is one file. Host `index.html` anywhere the POS browser can reach, for example GitHub Pages (Settings → Pages → deploy from this branch), then open that URL in Chrome on the terminal.

## Scanner requirements

- Scanner in keyboard (HID / keyboard-wedge) mode, with **Code 128** enabled. The existing Barcode Arcade already works this way.
- An Enter or Tab suffix is optional. Prefix and suffix characters are ignored.
- Scanners that type through an Android input method also work, through a hidden input field that is kept focused without opening the on-screen keyboard.

## URL options

| Option | Default | Use it when |
|---|---|---|
| `?module=3` | `2` | Barcodes are hard to read. This is the narrowest bar width in CSS pixels; larger values give bigger barcodes. |
| `?digits=6` | `4` | The scanner rejects short Code 128 barcodes (minimum-length setting). |
| `?res=180` | `216` | You want a lower internal resolution, for speed or a chunkier look. |
| `?nofs` | off | You don't want fullscreen on start. |
| `?touch` | off | You want tapping a tag to shoot it, for testing without a scanner. |
| `?debug` | off | You want to see FPS, frame time and the digits under each tag. Typing the digits and pressing Enter also works. |

Options can be combined: `index.html?module=3&digits=6`.

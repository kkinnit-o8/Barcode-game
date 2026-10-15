# Scanner Games

Arcade games you play with a barcode scanner. Point the scanner at a barcode on the screen, pull the trigger, and play.

Built for a SuSoft POS terminal (Android 7.1.2, Chrome 119), but it works with any barcode scanner in keyboard mode.

**https://kkinnit-o8.github.io/Barcode-game/**

<img src="qr-code.png" alt="QR code linking to https://kkinnit-o8.github.io/Barcode-game/" width="240">

`qr-code.svg` is the same QR code as a vector file, for printing at any size.

## Games

| Game | Folder | What it is |
|---|---|---|
| [HELLSCAN](hellscan/README.md) | `hellscan/` | Doom-style shooter. Every demon carries a barcode; scan it to shoot it. Loot crates, bosses and a shared leaderboard. |

On the home page, scan a game's **SCAN TO PLAY** barcode or tap its card to start it. Each game has a way back to the home page (in HELLSCAN: the **ALL GAMES** barcode on the title screen, or Esc).

## How the site is organised

```
index.html          the arcade home page (Scanner Games)
hellscan/           one folder per game, each a single self-contained index.html
  index.html
  preview.png       screenshot shown on the game's card
  README.md
qr-code.png / .svg  QR code for the home page
.nojekyll           tells GitHub Pages to serve the files as-is
```

## Adding a game

1. Create a folder with the game in `index.html`, for example `checkout-rush/index.html`. Keep it to one file with no external libraries or fonts, so it loads instantly on the POS browser.
2. Add a `preview.png` screenshot (about 768×368).
3. Add an entry to the `GAMES` list near the top of the script in the root `index.html`: name, folder, preview, description, and a 6-digit barcode number starting with `71` (`710002`, `710003`, …).
4. In the game, link back to the home page with `location.href = '../'` from a scannable "ALL GAMES" barcode.
5. If the game keeps scores, store them in `localStorage` under its own prefix (like `hellscan.`). To show them on the card, give its `GAMES` entry a `top` function.

Barcode rules all games follow: Code 128, digits only, a white quiet zone around every barcode, and bars at least 2 CSS pixels wide.

## Publishing

GitHub Pages serves the `main` branch (Settings → Pages → Deploy from a branch → `main`, `/ (root)`). Every push to `main` republishes the site within a couple of minutes. If the POS still shows an old version, reload the page.

## Scanner requirements

- Scanner in keyboard (HID / keyboard-wedge) mode, with **Code 128** enabled.
- An Enter or Tab suffix is optional. Prefix and suffix characters are ignored.
- Scanners that type through an Android input method also work, through a hidden input field that is kept focused without opening the on-screen keyboard.
- Scores are saved in the browser on the machine, and all games on this site share that storage.

# Phone Wheel

The steering wheel for Scanner Games that run on the POS screen and are steered with a phone. Right now that is [RUSH HOUR](../rush-hour/README.md).

Open it at **https://kkinnit-o8.github.io/Barcode-game/wheel/**, or tap **PHONE WHEEL** in the bottom corner of the [Scanner Games](../README.md) home page.

## Install it on the phone

It is a web app (PWA), so you can keep it on the home screen and open it like any other app, full screen.

- **Android (Chrome):** tap **INSTALL AS AN APP** on the wheel's first screen, or use the browser menu and pick **Add to Home screen** / **Install app**.
- **iPhone (Safari):** tap **Share**, then **Add to Home Screen**.

## Using it

1. Type your name (2 to 10 letters) and the 4-digit code shown on the POS screen. Scanning the QR code on the screen with the phone camera fills in the code for you.
2. When the screen answers, the wheel appears. Tilt the phone to steer: hold it upright like a steering wheel, tilted back or flat, in portrait or landscape.
3. Use the big button for **START**, **PAUSE**, **RESUME** and **RACE AGAIN**.

On an iPhone, tap **TAP TO TURN ON TILT STEERING** and allow motion access the first time. The wheel keeps the screen on while you play, and on Android the phone buzzes when you crash.

The wheel remembers your name and the last code. Next time it connects straight away, as long as the game is open on that screen.

## Settings

Tap the gear in the top right corner.

| Setting | What it does |
|---|---|
| Steering | **Tilt the phone**, or **touch left / right**: hold the left or right half of the screen. Touch is used automatically when the phone has no tilt sensor. |
| Sensitivity | How far you tilt for full lock: 45° (low), 30° (medium) or 20° (high). |
| Flip steering | Swap left and right, in case a phone reports its tilt the other way round. |
| Straight ahead | **How I hold it now** makes your current angle the straight-ahead position. **Level** goes back to level. |
| Disconnect | Leave the screen so someone else can connect, or change your name or code. |

The top line shows the link: a green dot and **DIRECT** when the phone talks straight to the screen, yellow and **VIA RELAY** when it goes through the internet relays, with the round trip time.

## For game makers

The game and the wheel share the link code between the `phone link` markers in `rush-hour/index.html` and `wheel/index.html`. Keep the two copies the same. Messages are small JSON objects on the MQTT topics `scannergames/wheel/v1/<code>/p` (phone to game) and `.../g` (game to phone):

| From | `t` | Fields | Meaning |
|---|---|---|---|
| phone | `hi` | `n` name | Join the screen. Sent every second until the game answers. |
| phone | `s` | `a` steering, -1 (left) to 1 (right) | Up to 25 times a second. |
| phone | `c` | `c`: `start`, `pause`, `resume` or `quit` | A button. |
| phone | `po` | `k` | Answer to a ping. |
| phone | `bye` | `away` | Left (`away`: the app was closed, so pause and wait). |
| game | `ok` / `busy` | `g` game name / `n` who has the screen | Answer to `hi`. |
| game | `st` | `m` mode, `sp` km/h, `d` metres, `l` lives, `lv` level, `res` result... | State, 5 times a second. The wheel's buttons follow `m`. |
| game | `ev` | `e`: `crash`, `level` or `over` | Something happened (the phone buzzes). |
| game | `pi` | `k` | Ping, once a second. |
| game | `bye` | `kick` | The screen closed (`kick`: it disconnected this phone). |
| both | `rtc` | `d`: an SDP description or ICE candidate | Sets up the direct WebRTC link. |

Every message carries `id` (the phone), `to` (game to phone), `gi` (the game page) and `q`, a sequence number that lets each side drop the copies arriving through the other relays.

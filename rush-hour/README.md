# RUSH HOUR

A racing game that runs on the POS screen and that you steer with your phone. Tilt the phone like a steering wheel, weave through the traffic, and hang on: the car speeds up every 20 seconds until you have crashed three times.

Play it at **https://kkinnit-o8.github.io/Barcode-game/rush-hour/**, or open the [Scanner Games](../README.md) home page and scan its card. The steering wheel is the [Phone Wheel](../wheel/README.md) app at **https://kkinnit-o8.github.io/Barcode-game/wheel/**.

Like the other games it is a single `index.html` with no libraries or fonts. Unlike them it needs the internet, because that is how the phone reaches the screen.

## How to play

1. Open RUSH HOUR on the POS screen. It shows **WAITING FOR A PHONE**, a 4-digit code and a QR code.
2. On your phone, open the Scanner Games site and tap **PHONE WHEEL** in the bottom corner, or scan the QR code with the phone camera.
3. Type your name and the code. The screen says hi when the phone is connected.
4. Hold the phone like a steering wheel and tilt it to steer. You can try the steering before the race starts.
5. Tap **START** on the phone. After 3, 2, 1 you're off.
6. Overtake the traffic and stay on the road. The grass slows you down, and lamp posts, trees, signs and billboards stop you dead.
7. A crash costs one of your 3 cars. After a crash you get a clear road and two seconds where nothing can hit you.
8. Your score is the distance you drive.

Every 20 seconds the speed goes up by 15 km/h (it starts at 110 km/h), more cars come by, and the time of day moves on from day to sunset, night and dawn.

Tap **PAUSE** on the phone, or scan **PAUSE** on the screen, to stop at any time. If the phone goes quiet (it locked, the app was closed, or the network dropped), the game pauses by itself. Open the wheel again and tap **RESUME**.

## On the screen

| Barcode | Where | What it does |
|---|---|---|
| ALL GAMES | top left of the start screens | Back to the arcade (Esc works too) |
| LEADERBOARD | bottom left of the start screens | Best distance per player, all time or this week |
| SOUND | bottom right of the start screens | Sound on or off |
| DISCONNECT PHONE | top right of the start screen, when a phone is connected | Lets someone else connect their phone |
| PAUSE | top left during a race | Pause |
| RESUME / QUIT | pause screen | Carry on, or end the race and save the distance |
| RACE AGAIN / MENU | after a race | Same as AGAIN on the phone, or back to the start screen |

Only one phone can steer at a time. Another phone that types the same code is told that the screen is busy. After a race, the game goes back to its start screen when nobody has done anything for 45 seconds.

The code belongs to the POS terminal: it stays the same until the browser's site data is cleared. The phone remembers the last code, so next time it connects as soon as you open the wheel.

## Leaderboard

Players are shared with the other games on the site. The name you type on the phone is the one that goes on the board.

- Players are ranked by their longest race. The board also shows each player's top speed and number of races.
- During a race, the top right shows who you need to beat next (`NEXT: OLA 4.21 KM`) and announces it when you pass them.
- Scores are stored in the browser on the POS terminal, under `rushhour.`. Clearing Chrome's site data resets the board and gives the screen a new code.

## How the phone talks to the screen

The site is static (GitHub Pages), so there is no server of our own. The phone and the screen meet on public MQTT brokers, on a topic named after the code (`scannergames/wheel/v1/<code>/`):

| Broker | Address |
|---|---|
| EMQX | `wss://broker.emqx.io:8084/mqtt` |
| HiveMQ | `wss://broker.hivemq.com:8884/mqtt` |
| Eclipse Mosquitto | `wss://test.mosquitto.org:8081/mqtt` |
| shiftr.io | `wss://public.cloud.shiftr.io` (port 443) |

- Both sides connect to all four and send through every one that is up, so it works as long as the POS and the phone can both reach one of them. The start screen shows how many it reached.
- Once connected, they try to set up a direct WebRTC link. That works when both are on a network that allows it, typically the same Wi-Fi, and cuts the lag to a few milliseconds. The status line shows **DIRECT** or **VIA RELAY** and the round trip time.
- These brokers are free public test services with no guarantee. Anyone who knows the code could listen in on the steering, which doesn't matter for a game. If the store network blocks them, run your own broker and pass it with `?relay=` (see below). The QR code on the screen hands the same setting to the phone.

## URL options

| Option | Default | Use it when |
|---|---|---|
| `?relay=wss://host:port/path` | the four brokers above | The public brokers are blocked, or you want your own. Comma-separate several; `wss://user:pass@host` passes a login. |
| `?nop2p` | off | You want to test the relay path without the direct link. |
| `?keys` | off | You want to drive with the arrow keys and Space, without a phone. |
| `?module=3` | `2` | Barcodes are hard to read. This is the narrowest bar width in CSS pixels. |
| `?digits=6` | `4` | The scanner rejects short Code 128 barcodes. Must be an even number from 4 to 12. |
| `?nofs` | off | You don't want fullscreen. |
| `?debug` | off | You want to see FPS and the digits under each barcode. Turns on `?keys` too. |

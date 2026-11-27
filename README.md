# 🔴 Game Buzzer

A simple multiplayer game-show buzzer that runs in any web browser. No accounts, no app installs and no server to run.

- **Players** open the link on their phones, enter their name, pick a buzzer sound and get one big buzzer.
- **The host** sees who buzzed in what order, with the time gap behind first place. They can reset, lock or unlock the buzzers and remove players.
- Each player picks their own sound (12 choices). It plays on their phone and on the host's screen, so everyone can hear who buzzed.

## How to use it

1. **Host:** open the site on a laptop or TV and click **Host a game**. You get a 4-letter room code, a join link and a QR code. Keep this tab open: it runs the game.
2. **Players:** scan the QR code, or go to the site and type the room code. Enter a name, choose a sound and tap **Let's play**.
3. Play! The host presses **Reset buzzers** (or the space bar) between questions. **L** locks or unlocks the buzzers.

If the host refreshes the page, the room keeps the same code and players reconnect on their own.

## Putting it online for free (GitHub Pages)

The whole app is one file, `index.html`, so any static host works. With GitHub Pages:

1. Merge this into your `main` branch.
2. On GitHub, go to **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**, then pick `main` and `/ (root)`, and click **Save**.
4. After a minute or so the site is live at `https://<your-username>.github.io/buzzer/`.

Netlify Drop (drag the folder onto app.netlify.com/drop) or Cloudflare Pages work too.

## How it works

- Everyone connects through free public message servers (MQTT over secure WebSockets: [EMQX](https://www.emqx.com/en/mqtt/public-mqtt5-broker) and [HiveMQ](https://www.hivemq.com/mqtt/public-mqtt-broker/)). This is the same kind of connection ordinary websites use, so it works on mobile data and most strict networks.
- The host listens on both servers. Each player uses the first one that works and switches to the backup if it can't connect.
- The host's browser keeps the game state. Buzz order is the order the host receives the buzzes.
- The room's latest state is saved on the servers. If the host's screen sleeps or the page reloads, the room keeps its code, players see "Host's screen is offline", and everything picks up again when it comes back.
- Host and player screens ask the phone to stay awake while the page is open.
- Sounds are generated in the browser with the Web Audio API. On iPhone they play as media, so the silent switch doesn't mute them. The media volume still needs to be up.

### Limitations

- The host's screen needs to stay on during a game. A laptop or tablet plugged in is ideal. If it sleeps, buzzes can't be counted until it wakes.
- The public servers are shared, best-effort services. Room messages (player names and buzzes) aren't private. Anyone who knew the room code could see them.

### Using your own message server (optional)

Add `?brokers=wss://your.server/mqtt` (comma-separate several) to the host URL. Join links and QR codes keep this setting.

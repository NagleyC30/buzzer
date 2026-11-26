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

- The host's browser is the game server. Players connect directly to it over WebRTC using [PeerJS](https://peerjs.com/).
- PeerJS's free public server is only used to introduce the devices to each other. Buzzes then travel straight from each phone to the host.
- Buzz order is whatever order the host's browser receives the buzzes in. Over normal Wi-Fi or 4G/5G, timing differences are a few tens of milliseconds.
- Sounds are generated in the browser with the Web Audio API, so there are no audio files.

### Limitations

- The host's tab must stay open. If it closes, the room closes.
- Some very strict networks (some corporate or school firewalls) block WebRTC. If one player can't connect, try switching them to mobile data.
- On iPhone, make sure the ring/silent switch isn't on silent if you want to hear the buzzer sound.

### Using your own PeerJS server (optional)

If the public PeerJS server is ever down, run your own (`npx peer --port 9000`) and add these to the URL:
`?peerhost=your.host&peerport=9000&peersecure=0`. Join links and QR codes keep these settings.

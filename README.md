# 🔴 Game Buzzer

A simple multiplayer game-show buzzer that runs in any web browser. No accounts, no app installs and no server to run.

- **Players** open the link on their phones, enter their name, pick a buzzer sound and get one big buzzer.
- **The host** sees who buzzed in what order, with the time gap behind first place. They can reset, lock or unlock the buzzers and remove players.
- Each player picks their own sound (12 choices). It plays on their phone and on the host's screen, so everyone can hear who buzzed.

## How to use it

1. **Host:** open the site on a laptop or TV and click **Host a game**. You get an 8-letter room code (shown as `ABCD-EFGH`), a join link and a QR code. Keep this tab open: it runs the game.
2. **Players:** scan the QR code, or go to the site and type the room code. Enter a name, choose a sound and tap **Let's play**.
3. Play, Jeopardy style:
   - **New question** (or **N**) clears the buzz order. The buzzers start **locked** while you read.
   - **Open buzzers** (or the **space bar**) unlocks them when you finish reading. Players' buzzers flash and vibrate. Pressing space again locks them.
   - **Buzz too early** and your buzzer locks for **¼ second**, like the real show. Each early press restarts the lockout. Players see a grey **WAIT** button while locked and **LOCKED** during the lockout.
   - Turn off **Jeopardy rules** on the host screen for a plain buzzer: new questions open straight away and there's no lockout.

### Final Jeopardy

1. On the host screen, click **🏆 Final Jeopardy** and type the category and clue. Do this before the TV is visible: the clue stays blurred while you type.
2. **Show category & take bets.** The TV shows only the category. Each player enters their current score and a bet from $0 up to that score. The TV shows who has locked in, not the amounts. Players can change their bet until the clue is revealed.
3. **Reveal clue & start 32 seconds.** The clue appears on the TV and phones with a countdown and thinking music (an original tune, played from the host screen). Players type their answers, which lock when time runs out.
4. **Reveal.** Players are listed lowest score first. For each one, click **Reveal answer**, then **✓ Right** or **✗ Wrong**. Their bet and final score appear on the TV and on their phone.
5. **Finish Final Jeopardy** returns everyone to the buzzer.

**Using your own music:** under the Final Jeopardy controls, click **Choose music file…** and pick an audio file on the host device (MP3, M4A, WAV and so on, up to 40 MB). It starts with the 32-second clock and fades out when time is up. **▶ Preview** lets you check it first. The file is saved in that browser for next time and is never uploaded anywhere. **Use built-in tune** switches back. The site doesn't include the TV show's theme because it's copyrighted; use a copy you own.

The clue isn't sent to phones until you reveal it. Bets and answers stay on the host screen, hidden, until you reveal them.

If the host refreshes the page, the room keeps the same code and players reconnect on their own.

## Writing question boards (`editor.html`)

Open **✏️ Write question boards** from the home page. A board has **Round 1** and **Round 2** (6 categories × 5 clues each) and a **Final** question. Each clue has a value, the clue (shown to everyone), the correct response (shown only to the host) and an optional **Daily Double**.

- **In the editor:** type category names at the top of each column and click a square to write its clue. In the response box, **Enter** jumps to the next clue. **Row values** sets a row's value across all categories. **Place Daily Doubles at random** puts 1 in Round 1 and 2 in Round 2, in the lower rows and never two in one category.
- **From a spreadsheet:** click **Download spreadsheet template** and open it in Google Sheets (*File → Import → Upload*) or Excel. Fill in one row per clue: `Round` (1, 2 or Final), `Category`, `Value`, `Clue`, `Response`, `Daily Double` (yes or blank). Blank Round or Category cells repeat the row above. Copy the rows, including the header, and use **Paste from spreadsheet…**. Problems are listed by row number. **Download as spreadsheet** turns any board back into a spreadsheet for editing.
- **Saving:** boards save in your browser as you type, and you can keep several. **Save board file** downloads a board to back it up or share it, and **Open board file…** loads one.

Boards aren't playable yet. That's the next step: a game-screen view for the TV and a host remote for the phone.

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
- The public servers are shared, best-effort services. They can be slow or down, which is why there's a backup.

### Privacy

- Every message (names, buzzes, game state) is encrypted in the browser with AES-GCM, using a key derived from the room code. It's never sent in readable form. The servers only see scrambled data on a channel whose name is also derived from the code.
- Outsiders can't read the game or send fake buzzes, because messages without the room's key are ignored.
- Room codes are 8 letters (about 78 billion possibilities), and the key is derived with 150,000 rounds of PBKDF2. Trying every code would take a powerful graphics card weeks.
- In join links and QR codes the room code sits after the `#` (`.../buzzer/#room=ABCDEFGH`). Browsers never send that part to the web server, so GitHub never sees it.
- It's still a family-game buzzer, not a secure messenger. Don't put anything sensitive in player names.

### Using your own message server (optional)

Add `?brokers=wss://your.server/mqtt` (comma-separate several) to the host URL. Join links and QR codes keep this setting.

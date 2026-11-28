# Buzzers

Game-show night in your living room. The board goes on the TV, the buzzers go on everyone's phones, and the host runs it all from their own phone. It runs in any web browser: no accounts, no app installs and no server to run.

- **Players** open the link on their phones, enter their name, pick a buzzer sound and get one big buzzer.
- **The host** sees who buzzed in what order, with the time gap behind first place. They can reset, lock or unlock the buzzers and remove players.
- Each player picks their own sound (12 choices). It plays on their phone and on the host's screen, so everyone can hear who buzzed.

## The game screen

The game screen is made for the TV:

- **Lobby:** a big **Join the game!** sign with the QR code, the room code and players appearing as they join, next to the buzz order.
- **During a board game:** only the board (or the current clue) and the scoreboard, with the join code tucked into the top bar for latecomers.
- **☰ Host menu:** everything for setting up slides in from the right. Connect the host remote, pick or open a board, start the Final Round, switch fair-start rules and sounds, or start a new room.

## How to use it

1. **Host:** open the site on a laptop or TV and click **Start a game screen**. You get an 8-letter room code (shown as `ABCD-EFGH`), a join link and a QR code. Keep this tab open: it runs the game.
2. **Players:** scan the QR code, or go to the site and type the room code. Enter a name, choose a sound and tap **Let's play**.
3. Play with **fair-start rules** (on by default):
   - **New question** (or **N**) clears the buzz order. The buzzers start **locked** while you read.
   - **Open buzzers** (or the **space bar**) unlocks them when you finish reading. Players' buzzers flash and vibrate. Pressing space again locks them.
   - **Buzz too early** and your buzzer locks for **¼ second**, like the real show. Each early press restarts the lockout. Players see a grey **WAIT** button while locked and **LOCKED** during the lockout.
   - Turn off **Fair-start rules** in the **☰ Host menu** for a plain buzzer: new questions open straight away and there's no lockout.

### Host remote (the host's phone)

The page you open with **Start a game screen** is the **game screen**: put it on the TV or laptop everyone can see, plugged in. The host runs the game from their phone:

1. On the game screen, open **☰ Host menu** → **📱 Connect host remote** and scan the code with **the host's phone**. Don't let players scan it. You can also copy the link and send it only to the host.
2. The remote controls everything the game screen can: open and lock the buzzers, new question, see the buzz order, remove players, the fair-start rules switch, and all of Final Round. Final Round is typed privately on the phone and includes a **correct response** that only the host sees. The host also sees players' answers before showing each one on the TV.
3. While a remote is connected, the game screen hides its controls. **Show controls on this screen** brings them back, and they return by themselves if the remote disconnects.

The remote link has its own secret key, separate from the room code, so players can't read the correct responses or send commands. If someone else might have scanned the remote code, click **New host key** in the same window. The old link stops working.

Browsers keep a page silent until it's been clicked once. If the game screen shows **🔇 Click or tap anywhere…**, click it once so buzzer sounds and music can play.

### Final Round

1. On the host remote, tap **🏆 Final Round** and type the category, clue and correct response privately on your phone. Without a remote, use **☰ Host menu** → **🏆 Final Round** on the game screen; type before the TV is visible, since the clue stays blurred while you type.
2. **Show category & take bets.** The TV shows only the category. Each player enters their current score and a bet from $0 up to that score. The TV shows who has locked in, not the amounts. Players can change their bet until the clue is revealed.
3. **Reveal clue & start 32 seconds.** The clue appears on the TV and phones with a countdown and thinking music (an original tune, played from the host screen). Players type their answers, which lock when time runs out.
4. **Reveal.** Players are listed lowest score first. For each one, click **Reveal answer**, then **✓ Right** or **✗ Wrong**. Their bet and final score appear on the TV and on their phone.
5. **Finish Final Round** returns everyone to the buzzer.

**Using your own music:** under the Final Round controls, click **Choose music file…** and pick an audio file on the host device (MP3, M4A, WAV and so on, up to 40 MB). It starts with the 32-second clock and fades out when time is up. **▶ Preview** lets you check it first. The file is saved in that browser for next time and is never uploaded anywhere. **Use built-in tune** switches back. The site doesn't include the TV show's theme because it's copyrighted; use a copy you own.

The clue isn't sent to phones until you reveal it. Bets and answers stay on the host screen, hidden, until you reveal them.

If the host refreshes the page, the room keeps the same code and players reconnect on their own.

## Writing question boards (`editor.html`)

Open **✏️ Open the board editor** from the home page. A board has **Round 1** and **Round 2** (6 categories × 5 clues each) and a **Final** question. Each clue has a value, the clue (shown to everyone), the correct response (shown only to the host) and an optional **Double Down**.

- **In the editor:** type category names at the top of each column and click a square to write its clue. In the response box, **Enter** jumps to the next clue. **Row values** sets a row's value across all categories. **Place Double Downs at random** puts 1 in Round 1 and 2 in Round 2, in the lower rows and never two in one category.
- **From a spreadsheet:** click **Download spreadsheet template** and open it in Google Sheets (*File → Import → Upload*) or Excel. Fill in one row per clue: `Round` (1, 2 or Final), `Category`, `Value`, `Clue`, `Response`, `Double Down` (yes or blank). Blank Round or Category cells repeat the row above. Copy the rows, including the header, and use **Paste from spreadsheet…**. Problems are listed by row number. **Download as spreadsheet** turns any board back into a spreadsheet for editing.
- **Sample board:** `samples/sample-board.csv` is a complete game (2 rounds, 60 clues, 3 Double Downs and a Final). Open it, copy everything, and use **Paste from spreadsheet…**, or open it in Google Sheets first to edit. The import window links to it as well. The same game is also a ready-made board file, `samples/sample-game-night.board.json`, for **Open board file…** in the editor or on the game screen.
- **Saving:** boards save in your browser as you type, and you can keep several. **Save board file** downloads a board to back it up or share it, and **Open board file…** loads one.

### Playing a board

1. Write a board in the editor on the device that runs the game screen, or move it there with a board file. **☰ Host menu** → **Open board file…** on the game screen also works.
2. Connect the host remote, let players join, then choose the board under **Play a board** on the remote and tap **▶ Play this board**. The TV shows the board and everyone's score.
3. The player in control calls out a category and value, and the host taps it on the remote's mini board. The clue fills the TV and appears on every phone. Buzzers stay locked while the host reads, with the ¼-second early-buzz rule.
4. Tap **Open buzzers**. The first player to buzz answers and everyone else is locked out. The remote shows the correct response:
   - **✓ Right:** the value is added, that player picks next, and the TV shows the correct response for a few seconds before returning to the board.
   - **✗ Wrong:** the value is subtracted, that player is out for this clue, and the buzzers reopen at once for everyone else.
   - **No one got it:** shows the response; control doesn't change.
   - **Put this clue back on the board:** if it was tapped by mistake.
5. **Undo last ruling** reverses mistakes. **Edit** changes any score, and **Picks** sets who chooses next. **Go to Round 2** switches rounds; the lowest score picks first. **🏆 Final Round** opens pre-filled with the board's final question.

Players never receive the board. Each phone gets only the clue being played, and the correct response only once that clue is over. Without a host remote, the game screen's own controls work too, but it can't show correct responses, because everyone can see that screen.

**Double Downs:** when the host taps one, the TV shows **DOUBLE DOWN!** with a fanfare, and the clue stays hidden from everyone. The player in control wagers on their phone: at least $5, up to their score or the round's top value, whichever is higher. The host can also type the wager on the remote, and choose who plays it if no one has control yet. Then **Reveal the clue**. Only that player answers (no buzzers), **✓ / ✗** adds or subtracts the wager, and they keep control either way.

**End of the game:** tap **🏁 Show the winner** on the remote. It's the big button at the top once Final Round is done. The TV shows the final standings with confetti, handling ties and "no one finished above $0". Each phone shows that player's place. From there: **← Back to the board**, **Play this board again** (scores reset to $0), or **End board game**.

**Sound:** the game screen plays original sound effects: a chime when a clue appears, a jingle for Round 2, right and wrong sounds, a Double Down fanfare and a winner fanfare. **Buzzer sounds and sound effects on the game screen** at the top of the remote turns them all on or off.

**Answer key:** in the board editor, **🖨 Print answer key** prints every clue and correct response by round and category, with Double Downs marked "DD". A full board fits on two pages. Handy if you host without the remote, or as a backup.

**Final Round in a board game:** players don't type their score; their phone shows it and caps the bet at that amount. Anyone at $0 or below sits it out. Who plays is fixed when Final Round starts. Each **✓ / ✗** in the reveal goes straight onto the scoreboard (and comes off again on **Undo**). **Finish Final Round** returns to the board with the final totals.

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
- It's still a family game, not a secure messenger. Don't put anything sensitive in player names.

### Using your own message server (optional)

Add `?brokers=wss://your.server/mqtt` (comma-separate several) to the host URL. Join links and QR codes keep this setting.

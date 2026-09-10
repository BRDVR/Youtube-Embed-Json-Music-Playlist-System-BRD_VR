# Playlist Player

A local webpage that plays a YouTube playlist from a JSON file. It uses YouTube’s embed player. It does not download videos as `.mp4` files, and it does not upload your playlist to some other app server.

The page talks to YouTube only to play embeds and load thumbnails. Your queue, volume, and saves stay in this browser.

---

## What you need

- Python 3
- A browser
- One project folder
- A YouTube playlist link you can open

Do not open the HTML file as `file://`. The embed and JSON loading need a local web server.

---

## Files in the project folder

Put only this project in the folder. The server shares **every file** in that directory.

Typical files:

- the player page (`index.html` or `playlist-player.html`)
- `README.md`
- your playlist `.json`
- optional `Icon.png` if you want a tab icon

Example folder:

```text
Desktop/YoutubeServer
```

If the player file is named `index.html`, this URL is enough:

```text
http://localhost:8080
```

If it is named something else, add the filename:

```text
http://localhost:8080/playlist-player.html
```

The player also looks for this default JSON next to the HTML and loads it automatically if nothing is saved yet:

```text
playlist_PLCkc8vHfqcGqDrApY5s2dahvJFr5NCdRH_data.json
```

---

## Start the server

1. Open Terminal.
2. Go into the project folder:

```bash
cd ~/Desktop/YoutubeServer
```

3. Start the server:

```bash
python3 -m http.server 8080
```

If that command is not found:

```bash
python -m http.server 8080
```

4. Open `http://localhost:8080` (or the filename URL above).

One-line version. Replace `USER` with your Mac username:

```bash
cd /Users/USER/Desktop/YoutubeServer && python3 -m http.server 8080
```

Leave Terminal open while you use the player. Stop the server with `Ctrl + C`.

### Server rules

- This shares the whole folder, not just the player.
- Other computers cannot open it unless you set up port forwarding. Do not do that for this project.
- Ports go from `1` to `65535`. If `8080` is taken, use another port, such as `8081`.
- Two servers cannot use the same port.
- `localhost:8080` and `localhost:8081` are treated as different sites. Saves, volume, and playlists do not carry over between ports.
- If the command fails, check Python, the folder path, and the firewall.

---

## Get a playlist as JSON

The player needs video IDs and titles. You get those from a normal YouTube playlist.

You can use a playlist you own, including an **unlisted** one. Unlisted playlists are not shown on public feeds, but anyone with the link can watch them until you change that.

Example test playlist (not owned by this project):

```text
https://www.youtube.com/watch?v=WzO2RUQoryI&list=PLuvRKGApO-zoF2WBPN2kW188YLke0Igv8
```

That is CaseOh’s “Laundry Simulator” list: five videos.

### Extractor site

This step uses a site this project does not own. It can change or go down:

```text
https://seotools.davidbreder.com/youtube-playlist
```

From the player, click **Copy & extract**. That copies your saved playlist link, then opens the extractor. If no link is saved yet, paste one first. The app cleans `music.youtube.com` and `youtu.be` when it can.

If you do it by hand:

1. Copy the playlist link.
2. Change it to a `www.youtube.com` link before pasting.

| Use this | Not this |
| --- | --- |
| `https://www.youtube.com/watch?v=...&list=...` | `https://music.youtube.com/...` |
| `https://www.youtube.com/playlist?list=...` | `https://youtu.be/...` |

3. Complete the CAPTCHA and click **Extract**.
4. Download as **JSON**.
5. Put that file in your project folder.

### What the JSON should contain

The player reads a list of videos. These keys work:

- `video_id`, `id`, or `videoId`
- `title`

A simple file looks like this:

```json
{
  "name": "Laundry Simulator",
  "url": "https://www.youtube.com/playlist?list=PLuvRKGApO-zoF2WBPN2kW188YLke0Igv8",
  "videos": [
    { "video_id": "WzO2RUQoryI", "title": "Example title" }
  ]
}
```

If the JSON includes `url` or `playlistUrl`, the player stores that for **Copy & extract**.

If YouTube adds or removes videos later, extract a new JSON and open it again. The player does not watch the live YouTube playlist for changes.

---

## Load it in the player

1. Keep the server running.
2. Refresh the player.
3. Click **Open JSON**, or drop the `.json` file onto the window.
4. You should see the queue. The embed starts the current video by itself.

**Save** stores that list in this browser so you do not have to pick the file every time. **Delete save** removes a named save. **Export** downloads the current list.

If the queue is empty, the file is not valid JSON, it has no video IDs, or extract failed.

---

## What the buttons do

- **Copy & extract** — copies the playlist link, then opens the extractor
- **Open JSON** — load a playlist file
- **Save / Delete save** — named playlists in this browser
- **Export** — download the current list
- **Hide gone** — hide videos YouTube will not play
- **Fullscreen** — video area only
- **YouTube** — open the current video on YouTube
- **Shuffle** — on = random queue, off = JSON order
- **Loop** — repeat the current video
- **Mute** and **Speed** — volume and playback rate
- Queue **×** — remove one row
- Drag a queue row to reorder it

### Keys

- `F7` previous
- `F8` or Space play/pause
- `F9` next
- `←` / `→` skip 10 seconds
- `↑` / `↓` volume
- `M` mute
- `L` loop
- `S` shuffle

On a Mac, `F7` / `F8` / `F9` can still work from other apps while this tab is the one playing, because the player keeps Media Session.

Refresh keeps the queue, time, volume, and current video, then starts the embed again.

---

## If something goes wrong

| Problem | What to try |
| --- | --- |
| Page will not load | Check the `cd` path, then open the correct localhost URL |
| Blank page at `/` | The HTML may not be named `index.html`. Add the filename to the URL |
| `Address already in use` | Use another port |
| Saves disappeared after changing port | That is a new site to the browser. Use the same port as before |
| Extract fails | Use a `www.youtube.com` playlist URL |
| Queue stays empty | Re-download JSON and use **Open JSON** again |
| Video will not play | It may be private, deleted, age-restricted, or blocked in your region. Turn off **Hide gone** |
| Embed does not start | Keep using `http://localhost:...`, not `file://` |
| Favicon missing | Serve `Icon.png` at the URL in the HTML, then hard-refresh |

---

## What this does not do

- It does not download videos.
- It does not keep your YouTube playlist in sync by itself.
- It cannot play videos YouTube will not embed.
- It does not send your JSON or settings off your computer, except YouTube playback/thumbnails and the extractor site you open yourself.

Saves live in this browser under `localhost` and the port you used. Clearing site data for that address wipes volume, queue, and named playlists.

---

## Privacy

- Keep only project files in the server folder.
- Do not expose the port to the public internet.
- Extraction happens on a third-party site you visit yourself.
- After that, the player stays local and uses YouTube embeds.
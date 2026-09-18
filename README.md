# YouTube Playlist Player

A small static YouTube playlist player. Videos stay on YouTube. This project only embeds them.

Two apps live in `Master/`:

- **Main (V5)** — import / export JSON, named saves, queue, shuffle, loop
- **Straight (V3)** — playlists baked into the page for VR browsers and machines with no file picker

Live site: [https://brdvr.github.io/Youtube-Embed-Json-Music-Playlist-System-BRD_VR/](https://brdvr.github.io/Youtube-Embed-Json-Music-Playlist-System-BRD_VR/)

Repo: [BRDVR/Youtube-Embed-Json-Music-Playlist-System-BRD_VR](https://github.com/BRDVR/Youtube-Embed-Json-Music-Playlist-System-BRD_VR)

## Quick start

1. Open the [project page](https://brdvr.github.io/Youtube-Embed-Json-Music-Playlist-System-BRD_VR/).
2. Pick **Maintained (V5)** or **Straight (V3)**.
3. Allow the YouTube embed if the browser asks.

No Python server. No Node. No install. GitHub Pages is enough.

## Straight — Playlist Loader V3

Built-in lists. No JSON upload. Made for Quest / managed Macs / anything that cannot pick a file.

Playlists are stored in `Straight.html` as one line per video:

```js
["title", "id", "author"],
```

The list that starts on load is set here:

```js
const FirstPlaylistToPlay = "Simple";
```

Change that string to `Tasklike`, `RealFr`, `Brain`, or `Stuffy`.

## Main — Playlist Player V5

Use this when you want your own lists.

- Import a single playlist or a full save
- Import is a preview until you hit **Save**
- Same name overwrites that list only; a new name is added
- Export writes the short-row format
- Queue, shuffle, loop, hide gone, themes
- Browser save key: `ytPlaylistPlayer.v5`  
  If that is empty, Main will read the old `v4` save once, then write v5

Example full save: [`Extras/V5-Save-E1.json`](Extras/V5-Save-E1.json)

### JSON format

Full save:

```json
{
  "_format": "playlist-player-v5",
  "settings": { "theme": "classic", "shuffle": true, "loopCurrent": false },
  "current": {
    "name": "Tasklike",
    "url": "https://www.youtube.com/watch?v=2juWhQh8Vuw&list=PLCkc8vHfqcGqDrApY5s2dahvJFr5NCdRH",
    "videos": [
      [ "Dine and Dash (Taskmaster OST)", "2juWhQh8Vuw", "vineytunes" ]
    ]
  },
  "saved": {}
}
```

A single playlist file can be just `videos` plus a name. Old `playlist-player-v4` files with `ids` / `titles` / `authors` still import.

Browser storage stays as `{ video_id, title, author }` objects so old sessions do not break. Only imported and exported files use the one-line rows.

## What this is not

- It does not download videos
- It does not host videos
- It does not replace YouTube
- Thumbnails and playback come from YouTube

You need a browser that can load `youtube.com` embeds.

## Layout

```
index.html                 Traveler dashboard
README.md
LICENSE                    Unlicense
Master/Main.html           Playlist Player V5
Master/Straight.html       Playlist Loader V3
Icons/GreenIcon.svg
Icons/BlueIcon.svg
Icons/RedIcon.svg
Extras/V5-Save-E1.json     example V5 save
```

## License

[Unlicense](LICENSE). Copy it, change it, republish it, no credit required.

The code is public domain. The songs are not. YouTube’s terms still apply to the videos you embed.

First uploaded to GitHub on September 10, 2026.

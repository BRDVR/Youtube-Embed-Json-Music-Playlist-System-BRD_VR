# BRD_VR YouTube Playlist Project

This project is a JSON-based playlist player that plays videos through YouTube's official embeds. The playlists included here are the playlists that I use through GitHub Pages daily. They are examples for this project, not a required set of videos.

## AI assistance

This project is created and edited with assistance from AI tools. The repository owner reviews and tests changes before publishing them.

## Customize your playlists

To use your own playlists, download or clone the entire repository so the player and its playlist files stay together. The included playlists are my personal selections; replace or edit them in `Playlists/` to use your own videos.

The player is `index.html`. It loads playlists listed in the `PLAYLIST_FILES` array in that file. To add a playlist, create a JSON file in `Playlists/` and add its display name and file path to `PLAYLIST_FILES`. Also add it to the `PLAYLISTS` array in `Check.html` if you want it included in ZIP exports. Linked YouTube playlists use `"custom": false` and a `url` containing the playlist ID. A manually maintained playlist uses `"custom": true`; its `url` is ignored, its `videos` rows are not changed by the checker, and it may start with an empty `videos` array. Add or edit its one-line song rows directly in the JSON file:

```json
{
  "name": "My Custom Playlist",
  "custom": true,
  "url": "",
  "videos": [
    ["Song title", "YouTubeVideoID", "Artist"]
  ]
}
```

Because the player loads JSON files, run the repository through a local web server instead of opening `index.html` directly from your file manager. For example, with Python installed, open a terminal in the repository folder and run:

```sh
python3 -m http.server 8081
```

Then open `http://localhost:8081/` in your browser. The playlist dropdown in the player lets you choose a list. Keep the server running while you use the player.

Use **Check Live Playlists** to open `Check.html` and compare each linked playlist JSON only with its own YouTube playlist; it does not merge playlists. The page previews live additions, saved entries absent from the live response, order differences, missing title/artist metadata, and clear same-song upload variants where the only artist difference is a trailing `- Topic`. Both ZIP exports remove duplicate video IDs and clear `- Topic` variants; exported artist values omit that suffix. When one version is in the live playlist and the other is only in the JSON, the replacement ZIP keeps the live version. Other saved entries absent from the live response are retained at the end for review. **Download Replacement ZIP** exports live entries in playlist order plus retained JSON-only entries. **Full Restore ZIP** exports only entries returned by the API, in API order, including unavailable entries; it reuses saved titles and artists for matching video IDs and fills blanks from API data where available. Rows in `"custom": true` files bypass the API and pass through both ZIP types without API-based edits. The checker displays when PlaylistDuration last fetched each linked playlist and whether its response is cached; its response may lag recent YouTube changes, so check the timestamp and review the ZIP before using it. ZIPs are browser downloads and do not overwrite project files. The live-list check uses [PlaylistDuration's API](https://playlistduration.com/developers).

## Ownership and use

The project's original code and files are released under the [Unlicense](LICENSE), so they may be copied, modified, and used freely.

BRD_VR does not own YouTube, its platform, or videos hosted there. Videos remain on YouTube and are subject to YouTube's terms and the rights of their respective owners.

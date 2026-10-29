# BRD_VR YouTube Playlist Project

This project is a JSON-based playlist player that plays videos through YouTube's official embeds. The playlists included here are the playlists that I use through GitHub Pages daily. They are examples for this project, not a required set of videos.

## Customize your playlists

To use your own playlists, download or clone the entire repository so the player and its playlist files stay together. The included playlists are my personal selections; replace or edit them in `Playlists/` to use your own videos.

The player is `index.html`. It loads playlists listed in the `PLAYLIST_FILES` array in that file. To add a playlist, create a JSON file in `Playlists/` and add its display name and file path to `PLAYLIST_FILES`. To remove one, remove its entry from that array; you can also delete its JSON file if you no longer need it.

Because the player loads JSON files, run the repository through a local web server instead of opening `index.html` directly from your file manager. For example, with Python installed, open a terminal in the repository folder and run:

```sh
python3 -m http.server 8081
```

Then open `http://localhost:8081/` in your browser. The playlist dropdown in the player lets you choose a list. Keep the server running while you use the player.

Use **Check Live Playlists** to open `Check.html` and compare each saved playlist JSON only with its own current YouTube playlist; it does not merge playlists. The page previews live additions, saved entries absent from the live playlist, order differences, and missing title/artist metadata. Once every playlist check succeeds, **Download Replacement ZIP** exports all five JSON files under a `Playlists/` folder, preserving saved entries absent from the live playlist at the end for review. **Full Restore ZIP** instead exports only entries returned by the API in API order, including unavailable entries; it reuses saved titles and artists for matching video IDs, using API metadata where saved values are unavailable. The checker displays when PlaylistDuration last fetched each playlist and whether its response is cached; its response may lag recent YouTube changes, so check the timestamp and review the ZIP before using it. Both ZIPs are downloaded by the browser and do not overwrite project files. Review the preview, then extract the ZIP into the project and replace files manually if desired. The live-list check uses [PlaylistDuration's API](https://playlistduration.com/developers).

## Ownership and use

The project's original code and files are released under the [Unlicense](LICENSE), so they may be copied, modified, and used freely.

BRD_VR does not own YouTube, its platform, or videos hosted there. Videos remain on YouTube and are subject to YouTube's terms and the rights of their respective owners.

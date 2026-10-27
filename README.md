# BRD_VR YouTube Playlist Project

This project is a JSON-based playlist player that plays videos through YouTube's official embeds. The playlists included here are the playlists that I use through GitHub Pages daily. They are examples for this project, not a required set of videos.

## Customize your playlists

To use your own playlists, download or clone the entire repository so you have the player, its JSON playlist files, and required icons together. Edit the JSON files in `Playlists/` to add or remove playlists and videos. The player reads the playlist files from that folder.

Because the player loads JSON files, serve the repository through a local web server rather than opening `index.html` or `Straight.html` directly from your file manager. For example, with Python installed, open a terminal in the repository folder and run:

```sh
python3 -m http.server 8081
```

Then open `http://localhost:8081/` in your browser and select Straight. Keep the server running while you use the player.

## Ownership and use

The project's original code and files are released under the [Unlicense](LICENSE), so they may be copied, modified, and used freely.

BRD_VR does not own YouTube, its platform, or videos hosted there. Videos remain on YouTube and are subject to YouTube's terms and the rights of their respective owners.

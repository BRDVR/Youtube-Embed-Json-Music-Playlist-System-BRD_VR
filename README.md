# BRD_VR YouTube Playlist Project

This project is a JSON-based playlist player that plays videos through YouTube's official embeds. The playlists included here are the playlists that I use through GitHub Pages daily. They are examples for this project, not a required set of videos. As well, this project and it's repository are assisted by Github Copilot and other AI tools.

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

Then open `http://localhost:8081/` in your browser. The playlist dropdown in the player lets you choose a list. The player accent colors adapt to the current video's YouTube thumbnail; if the thumbnail cannot be read, it falls back to the default blue palette. Search is above the queue. Keyboard shortcuts remain available without being listed beside the playback buttons. Keep the server running while you use the player.

## Player configuration

`config.json` controls advanced settings for `index.html`; it does not change `Check.html`. The player validates the file at startup. If it is missing or invalid, the player logs the error, shows a notice, and uses built-in safe defaults. Serve the project through a web server so the player can fetch the file.

- `responsive`: width/height breakpoints, queue widths, and minimum heights for stacked layouts. The player keeps its two-column layout at normal desktop sizes, compacts controls and the queue at narrower widths, and stacks the player above the queue on small screens.
- `layout.flipHorizontally`: reverse the horizontal arrangement, including the player/queue sides, queue columns, toolbar and playback-control order, and mirrored YouTube player.
- `appearance`: initial theme, artwork-adaptive accent colors, color transition duration in milliseconds, and the fallback palette used when adaptation is disabled or a thumbnail cannot be read. A previously saved theme choice takes precedence over `defaultTheme`.
- `controls`: enable or disable keyboard shortcuts, set arrow-key seek and volume steps, choose the first-run volume, and show or hide playback speed. A previously saved volume takes precedence over `initialVolumePercent`.
- `queue`: show or hide queue thumbnails, set a viewport width below which thumbnails are hidden (`0` disables this breakpoint), auto-scroll to each newly playing track, and confirm before removing queue items.

Keep the settings as valid JSON. Values are range-checked when the player starts; invalid values cause the full file to fall back to defaults. The volume slider's nonlinear scale is unchanged.

Use **Check Playlist Snapshots** to open `Check.html`. The page displays the full YouTube playlist URL for each linked playlist, with a copy button, plus a link to the JSON exporter. Copy each URL into the exporter and download a JSON snapshot containing playlist ID, video ID, title, and position. Add the files all at once or in multiple batches; the on-page checklist tracks which playlist snapshots have been added, and checking stays disabled until all linked playlists have one. The checker matches each imported file to its own playlist ID, processes the files locally, and does not use PlaylistDuration for playlist membership. Keep the page open while adding batches; imported files are not retained after leaving or reloading the page. These are independent exported snapshots, not a live or guaranteed-current check against YouTube; verify uncertain results on YouTube. Imports with missing IDs, duplicate or gapped positions, or incomplete data are rejected. Duplicate video IDs and possible same-song `- Topic` variants are reported but never automatically removed; they do not require a separate keep-confirmation because the checker keeps rows by default. The playlist name in your JSON is always preserved and never replaced with an exporter title. For matching video IDs, video-row titles use the imported snapshot title when available; new rows use snapshot titles. Rows saved in JSON but not represented by the imported snapshot are called out without claiming they were deleted. A single acknowledgment is required for each affected playlist before export: Replacement retains those rows at the end, while Full Restore omits them to match the imported snapshot. **Download Replacement ZIP** outputs snapshot entries in playlist order, then appends saved rows that could not be paired with a snapshot occurrence. **Full Restore ZIP** exports entries from the imported snapshot in order. Both ZIPs are read back and checked against the planned JSON before download. Rows in `"custom": true` files bypass snapshot imports, preserve their JSON values and row ordering, and are recursively validated both before export and from the finished ZIP. ZIPs are browser downloads and do not overwrite project files.

## Ownership and use

The project's original code and files are released under the [Unlicense](LICENSE), so they may be copied, modified, and used freely.

BRD_VR does not own YouTube, its platform, or videos hosted there. Videos remain on YouTube and are subject to YouTube's terms and the rights of their respective owners.

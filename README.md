# Context
The version text refers to the project, not it's file.

# BRD_VR YouTube Playlist Project

This project is a JSON-based playlist player that plays videos through YouTube's official embeds. The playlists included here are the playlists that I use through GitHub Pages daily. They are examples for this project, not a required set of videos. As well, this project and it's repository are assisted by Github Copilot and other AI tools.

## AI assistance

This project is created and edited with assistance from AI tools. The repository owner reviews and tests changes before publishing them.

## Customize your playlists

To use your own playlists, download or clone the entire repository so the player and its playlist files stay together. The included playlists are my personal selections; replace or edit them in `Playlists/` to use your own videos.

The player is `index.html`. Playlist names and file paths are listed once in the `playlists` array in `config.json`; both the player and `Check.html` read that registry. To add a playlist, create its JSON file in `Playlists/`, then add one `{ "name": "My Playlist", "file": "Playlists/MyPlaylist.json" }` entry to `config.json`. It will appear in the player and checker automatically. Linked YouTube playlists use `"custom": false`, a `url` containing the playlist ID, and `videos` rows shaped like `["Song title", "YouTubeVideoID", "Artist"]`. A manually maintained playlist uses `"custom": true`; its `url` is ignored, its `videos` rows are not changed by the checker, and it may start with an empty `videos` array. Add or edit its one-line song rows directly in the JSON file:

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

`config.json` contains the shared playlist registry used by `index.html` and `Check.html`, as well as advanced player settings. The player validates both at startup. Invalid player settings fall back to safe defaults; an invalid playlist registry prevents playlists from loading so the configuration error is not hidden. Serve the project through a web server so the pages can fetch the file.

- `responsive`: width/height breakpoints, queue widths, and minimum heights for stacked layouts. The player keeps its two-column layout at normal desktop sizes, compacts controls and the queue at narrower widths, and stacks the player above the queue on small screens.
- `layout.flipHorizontally`: reverse the horizontal arrangement, including the player/queue sides, queue columns, toolbar and playback-control order, and mirrored YouTube player.
- `layout.flipVertically`: vertically mirror the entire player area, including the video, now-playing panel, and playback controls. This can be combined with `flipHorizontally`; enabling both rotates the player area 180 degrees.
- `appearance`: initial theme, artwork-adaptive accent colors, color transition duration in milliseconds, and the fallback palette used when adaptation is disabled or a thumbnail cannot be read. A previously saved theme choice takes precedence over `defaultTheme`.
- `controls`: enable or disable keyboard shortcuts, choose whether the volume slider uses the custom stepped curve (`useVolumeCurve: true`) or a linear percentage scale (`false`), set arrow-key seek and volume steps, choose the first-run volume, and show or hide playback speed. A previously saved volume takes precedence over `initialVolumePercent`.
- `queue`: show or hide queue thumbnails, set a viewport width below which thumbnails are hidden (`0` disables this breakpoint), auto-scroll to each newly playing track, and confirm before removing queue items.

Keep the settings as valid JSON. Values are range-checked when the player starts; invalid values cause the full file to fall back to defaults. `controls.useVolumeCurve` defaults to `true` to preserve the custom curve; set it to `false` for a linear slider where 50% is at the midpoint.

Use **Check Playlist Snapshots** to open `Check.html`. The page displays the full YouTube playlist URL for each linked playlist, with a copy button, plus a link to the JSON exporter. Copy each URL into the exporter and download a JSON snapshot containing playlist ID, video ID, title, and position. Add the files all at once or in multiple batches; the on-page checklist tracks which playlist snapshots have been added. Checking is enabled once at least one linked playlist snapshot is uploaded, and checks only uploaded linked playlists (plus any custom playlists); add more files and check again whenever you are ready. Each checked report has individual **Download Replacement JSON** and **Download Full Restore JSON** buttons, so a single playlist JSON can be downloaded without waiting for all snapshots. Custom playlists have a single unchanged **Download JSON** button. Required saved-row reviews must be approved before downloading. Complete ZIP exports remain disabled until every linked playlist has a snapshot and all playlists have been checked successfully. The checker matches each imported file to its own playlist ID, processes the files locally, and does not use PlaylistDuration for playlist membership. Keep the page open while adding batches; imported files are not retained after leaving or reloading the page. These are independent exported snapshots, not a live or guaranteed-current check against YouTube; verify uncertain results on YouTube. Imports with missing IDs, duplicate or gapped positions, or incomplete data are rejected. Duplicate video IDs and possible same-song `- Topic` variants are reported but never automatically removed; they do not require a separate keep-confirmation because the checker keeps rows by default. The playlist name in your JSON is always preserved and never replaced with an exporter title. For matching video IDs, video-row titles use the imported snapshot title when available; new rows use snapshot titles. Rows saved in JSON but not represented by the imported snapshot are called out without claiming they were deleted. A single acknowledgment is required for each affected playlist before export: Replacement retains those rows at the end, while Full Restore omits them to match the imported snapshot. **Download Replacement ZIP** outputs snapshot entries in playlist order, then appends saved rows that could not be paired with a snapshot occurrence. **Full Restore ZIP** exports entries from the imported snapshot in order. Both ZIPs are read back and checked against the planned JSON before download. Rows in `"custom": true` files bypass snapshot imports, preserve their JSON values and row ordering, and are recursively validated both before export and from the finished ZIP. ZIPs are browser downloads and do not overwrite project files.

The checker also includes **Repair or identify a playlist JSON** for other JSON files. Either upload tool recognizes a configured playlist from the export's playlist ID. Uploading an exported snapshot through the repair tool also adds that valid snapshot to the regular checker. The repair tool can additionally match by playlist name or saved-video overlap, fill blank titles and artists from saved rows, and download the repaired upload or a version with missing saved rows restored. Unmatched JSON can still be downloaded in the project playlist format. This tool runs locally and never changes your original files.

## Ownership and use

The project's original code and files are released under the [Unlicense](LICENSE), so they may be copied, modified, and used freely.

BRD_VR does not own YouTube, its platform, or videos hosted there. Videos remain on YouTube and are subject to YouTube's terms and the rights of their respective owners.

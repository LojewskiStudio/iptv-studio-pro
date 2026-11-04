# IPTV Studio Pro

A single-file IPTV player for HLS streams and M3U/M3U8 playlists. It runs in a modern browser and can be hosted as a static site; it does not require an application server or backend.

## Features

- Load playlists from a URL or from a local M3U/M3U8 file.
- Configure country and category metadata separately for each playlist.
- Browse channels by country or category, search, and save favorites.
- Optionally merge entries that share a `tvg-id` so other streams can act as backups.
- Keep a bounded playback history with Back and Forward navigation.
- Show stream statistics and select available HLS quality, audio, and subtitle tracks.
- Save settings and playlist data in the browser.

## Start

Open `index.html` in your browser. No separate app server is needed. Hls.js loads from jsDelivr, so HLS playback needs an internet connection in browsers that rely on it.

Playlist URLs must allow browser access through CORS. If a playlist URL is blocked, download its M3U/M3U8 file and use **Load from file** in Settings. Individual streams may also be unavailable or restricted by their providers.

## Data and privacy

The player has no application backend or account system. Settings, favorites, and cached playlists are stored in the browser. When you load a playlist or play a stream, the browser connects directly to the relevant playlist, logo, and stream providers.

## Third-party services and content

Hls.js is loaded from jsDelivr and is licensed separately from this project. Playlist entries, logos, and streams are supplied by third parties and remain subject to their respective terms and rights.

## License

The IPTV Studio Pro code in this repository is licensed under the MIT License. See [LICENSE](LICENSE). This license does not grant rights to third-party playlists, logos, or streams.

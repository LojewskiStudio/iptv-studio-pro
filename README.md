# IPTV Studio Pro

A single-file IPTV player for HLS streams and M3U/M3U8 playlists. It runs in any modern browser, needs no application server or backend, and can be hosted as a static page.

**DEMO:** https://lojewskistudio.github.io/iptv-studio-pro/

<sub><i>(The online demo is provided for preview. For full functionality and the best experience, download and run the application locally)</i></sub>

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/5a99611d-42c8-4229-b8fd-624c8c5d2d3a" />



## Features

- **Playlists:** load M3U/M3U8 playlists from a URL or from a local file, enable or disable each one, and refresh them on demand. IPTV-Org and Free-TV are included by default.
- **Country and category metadata:** read automatically, and configurable per playlist (see [Metadata](#metadata-countries-and-categories)).
- **Browsing:** by country, by category, all channels, favorites, or recently played. Search matches name, country, category, and playlist.
- **Favorites and recent channels**, stored in the browser. Favorites can be exported as an M3U file.
- **Backup streams:** optionally merge entries that share the same `tvg-id`. If one stream fails, the next one is tried automatically.
- **Navigation:** zap to the next or previous channel in the list, and go Back/Forward through the channels that actually started playing.
- **Stream controls:** choose the HLS quality level, audio track, and subtitles when the stream offers them. A statistics panel shows resolution, bitrate, buffer, and dropped frames.
- **Clear status:** connection, buffering, unavailable, and possible geo-block messages appear below the player. Nothing is shown while the picture is playing normally.
- **Keyboard navigation:** arrow keys move a cursor through the list without starting playback; Enter plays.
- **Fast restarts:** playlists are cached in the browser for 12 hours.

## Getting started

### Online

Open the live page above.

### Locally

1. Download `index.html`.
2. Open it in your browser. No server is needed.

<sub><i>(Playback uses [hls.js](https://github.com/video-dev/hls.js), loaded from the jsDelivr CDN, so an internet connection is needed)</i></sub>


## Using playlists

Open **⚙ Settings** to manage playlists:

- **Add by URL.** The server must allow cross-origin requests (CORS). GitHub and GitHub Pages do.
- **Load from file.** If a URL is blocked by CORS, download the M3U/M3U8 file and load it here instead. The file is kept in the browser.
- **Enable or disable** each playlist with its checkbox. Use **Refresh all** to bypass the cache.

### Metadata: countries and categories

Playlists describe channels differently, so each playlist has a **Metadata** button:

| Setting | What it does |
| --- | --- |
| **Country from** | Auto-detect, the `tvg-country` attribute, `group-title`, the `tvg-id` suffix (for example `.us`), or any other attribute you name. |
| **Default country** | Used when no country is found, for example `Spain` for a national channel list. |
| **Category from** | Auto-detect, `group-title`, any other attribute, or none. |
| **Country / category index URL** | An optional companion playlist whose `group-title` holds the country or category. It is matched to channels by stream URL. IPTV-Org uses this. |

Below these settings, an inspector shows which attributes the playlist contains, how its `group-title` values were interpreted, and sample channels with the resulting country and category. Changes apply immediately, without downloading the playlist again.

### Duplicate channels

By default, entries with the same `tvg-id` are merged into one channel with several streams (shown as **×2**, **×3**, and so on). Channels are never merged by name. You can turn merging off in Settings, and pick a specific stream from the **Stream** menu.

## Keyboard shortcuts

| Key | Action |
| --- | --- |
| `↑` `↓` | Move the cursor in the list (does not play) |
| `→` `←` | Open or close the group under the cursor |
| `Enter` | Play the channel, or open or close the group |
| `Home` `End` | Jump to the first or last item |
| `N` `P` | Next or previous channel (zap) |
| `,` `.` | History back or forward |
| `S` | Favorite the channel under the cursor (or the playing one) |
| `M` | Mute |
| `I` | Stream statistics |
| `F` | Fullscreen |
| `/` | Search (`↓` jumps to the results, `Esc` clears) |

While the video itself has keyboard focus, the arrow keys keep their native seek and volume behavior.

### Fullscreen

By default, the browser's own fullscreen button is used. It can only show the video, so the status cannot appear over the picture. In **Settings → Fullscreen**, choose **App fullscreen** to show the channel name and status over the picture, and to zap with `↑`/`↓`. This mode hides the native fullscreen button and adds a ⛶ button below the player. It works in Chrome and Edge.

## Limitations

- **HLS only.** Streams such as RTMP, RTSP, UDP/multicast, or raw MPEG-TS cannot be played by a browser.
- **CORS.** Some playlist or stream servers do not allow browser access, so those lists or channels cannot load here.
- **Mixed content.** On an HTTPS page, including GitHub Pages, browsers block streams that use plain `http://`. Those channels appear as unavailable. Open the file locally to play them.
- **Geo-blocking and dead streams.** Many public streams are region-locked or offline. A 403 or 451 response is reported as "Possibly blocked in your region". Channels that fail to start are hidden for 7 days unless you change that in Settings.
- **Browser autoplay rules.** If the browser blocks autoplay with sound, playback starts muted.

## Data and privacy

The player has no application backend and no accounts. Settings, favorites, history of recent channels, and cached playlists are stored in your browser (`localStorage` and IndexedDB). To reset everything, clear this site's data in your browser.

When you load a playlist or play a stream, your browser connects directly to the playlist, logo, and stream providers, which can see your IP address. The hls.js library is requested from jsDelivr.

## Third-party services and content

This project does not host, provide, or endorse any streams or playlists. The default playlists ([IPTV-Org](https://github.com/iptv-org/iptv) and [Free-TV](https://github.com/Free-TV/IPTV)) are maintained by third parties. Playlist entries, logos, and streams remain subject to their owners' terms and rights, and you are responsible for making sure you may access the content you play. hls.js is licensed separately from this project.

## License

The IPTV Studio Pro code in this repository is licensed under the [MIT License](LICENSE). This license does not grant rights to third-party playlists, logos, or streams.

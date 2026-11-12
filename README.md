# IPTV Studio Pro

A single-file IPTV player for HLS streams and M3U/M3U8 playlists. It runs in a modern browser, needs no application server or backend, and can be hosted as a static page.



<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/815d7873-e578-4c3a-8bae-0b39d1026d1d" />







**Demo:** https://lojewskistudio.github.io/iptv-studio-pro/ 

<sub>The online demo is provided for preview. For the best experience, download and open the HTML file locally.</sub>


## Features

- **Playlists:** load multiple M3U/M3U8 playlists from URLs or local files, rename them, enable or disable them, and refresh them on demand. IPTV-Org and Free-TV are included by default.
- **Playlist metadata:** configure country and category extraction separately for each playlist (see [Metadata: countries and categories](#metadata-countries-and-categories)).
- **Channel browsing:** browse by country, category, all channels, favorites, or recently played. Search matches channel name, country, category, and playlist.
- **Favorites and history:** favorites and recently played channels are stored in the browser. Export favorites as an M3U file, and use Back/Forward to return to channels that started playing.
- **Backup streams:** optionally merge entries with the same `tvg-id`. If a stream fails, the player tries another stream for that channel.
- **Playback controls:** choose video quality, audio track, and subtitles when offered by the stream. Stream info includes resolution, bitrate, buffer, and dropped frames.
- **EPG:** optional Now/Next guide per playlist. Use an XMLTV URL or load an XML/XML.GZ file locally. EPG has both a global setting and a separate enable switch for each playlist.
- **DVR:** record the current playback with the REC button. Press it again to stop and download the recording. Browser and stream support varies; keep the app page open while recording.
- **Themes and channel logos:** choose from seven color themes. Logo backgrounds are detected automatically and can be changed by clicking a channel logo; the choice is remembered for the selected theme.
- **Playback status:** see connection, buffering, unavailable, and possible geo-block messages.
- **Keyboard navigation:** arrow keys move a cursor through the list without starting playback; Enter plays.
- **Fast restarts:** playlists are cached in the browser for 12 hours.

## Getting started

### Online

Open the [live demo](https://lojewskistudio.github.io/iptv-studio-pro/).

### Locally

1. Download the HTML file from the repository.
2. Open it in a modern browser. No server is needed.

## Using playlists

Open **Settings** to manage playlists:

- **Add by URL:** the playlist server must allow cross-origin requests (CORS). If it does not, download the playlist and load the file instead.
- **Load from file:** local M3U/M3U8 files are stored in the browser.
- **Rename:** give each playlist a recognizable name, even when several have the same filename.
- **Enable or disable:** use each playlist's checkbox. Use **Refresh all** to bypass the cache.

### Metadata: countries and categories

Each playlist has its own **Metadata** settings because playlists describe channels differently:

| Setting | What it does |
| --- | --- |
| **Country from** | Auto-detect, the `tvg-country` attribute, `group-title`, the `tvg-id` suffix (for example `.us`), or another attribute you specify. |
| **Default country** | Country to use when none is found, such as `Spain` for a national channel list. |
| **Category from** | Auto-detect, `group-title`, another attribute, or none. |
| **Country/category index URL** | Optional companion playlist whose `group-title` contains the country or category. Entries are matched by stream URL. IPTV-Org uses this format. |

The metadata inspector shows the playlist's attributes, how `group-title` values were interpreted, and sample channels with their resulting country and category. Changes apply immediately without downloading the playlist again.

### EPG setup

1. In **Settings**, enable **EPG in the app**.
2. Open the **EPG** settings for a playlist and enable EPG for that playlist.
3. Add an XMLTV guide URL or load a downloaded `.xml`, `.gz`, or `.xml.gz` guide file.

The channel needs a matching `tvg-id` in both the playlist and guide. Online guides must allow cross-origin requests (CORS). If an online source is blocked, download the guide and load it locally. The player displays the current and next programme when guide data is available.

### DVR recording

Enable **DVR recording** in Settings. Start playback, then press **REC** to begin recording; press it again to stop and download the file. Recording support varies by device, browser, and stream. Keep the app page open while recording. The browser chooses the supported recording format and download location.

### Duplicate channels

By default, entries with the same `tvg-id` are merged into one channel with several streams (shown as **×2**, **×3**, and so on). Channels are not merged by name. Turn merging off in Settings to keep entries separate, or choose a specific stream from the **Stream** menu.

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
| `I` | Show stream statistics |
| `F` | Toggle native video fullscreen |
| `/` | Search (`↓` jumps to the results, `Esc` clears) |

While the video has keyboard focus, the arrow keys keep their native seek and volume behavior.

### Fullscreen

Use the browser's native fullscreen button on the video, or press `F`. This displays the video only; the app controls and status information remain outside fullscreen.

## Limitations

- **HLS only:** browsers cannot play formats such as RTMP, RTSP, UDP/multicast, or raw MPEG-TS.
- **CORS:** some playlist, stream, or online EPG servers do not allow browser access. Download playlists or guides and load them locally when possible.
- **Mixed content:** on an HTTPS page, including GitHub Pages, browsers block streams using plain `http://`. Those channels may be unavailable.
- **Geo-blocking and offline streams:** public streams may be region-locked or offline. HTTP 403/451 responses are reported as possible regional blocks. Channels that fail to start are hidden for seven days by default; this can be changed in Settings.
- **Autoplay rules:** if the browser blocks autoplay with sound, playback starts muted.
- **DVR support:** browser recording APIs and stream capture are not supported everywhere. Recording stops if the page is closed, and the app cannot schedule background recordings.
- **Local-file access:** playlist and guide files are stored in the browser used to load them. Clearing the browser's site data removes them.

## Data and privacy

The player has no application backend and no accounts. Settings, playlists, guide files, favorites, playback history, and cached playlist data are stored in your browser using `localStorage` and IndexedDB. To reset everything, clear this site's data in your browser.

When you load a playlist or play a stream, your browser connects directly to the playlist, guide, logo, and stream providers, which can see your IP address. The hls.js library is loaded from jsDelivr.

## Third-party services and content

This project does not host, provide, or endorse streams or playlists. The default playlists ([IPTV-Org](https://github.com/iptv-org/iptv) and [Free-TV](https://github.com/Free-TV/IPTV)) are maintained by third parties. Playlist entries, logos, and streams remain subject to their owners' terms and rights; you are responsible for making sure you may access the content you play. hls.js is licensed separately from this project.

<sub>Playback uses [hls.js](https://github.com/video-dev/hls.js), loaded from the jsDelivr CDN.</sub>

## License

The IPTV Studio Pro code in this repository is licensed under the [MIT License](LICENSE). This license does not grant rights to third-party playlists, logos, or streams.

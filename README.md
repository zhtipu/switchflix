# SwitchFlix

<img width="2880" height="1440" alt="banner" src="https://github.com/user-attachments/assets/b5773753-b17f-49bb-bcc7-106356833cc3" />


Watch movies, series and music from your own media servers on your Nintendo Switch.
SwitchFlix is made for home and ISP media servers: Emby, folder-index file servers and Flix-style movie sites,
plus the storage on your Switch itself.
<br clear="left">

## Features

- **Home** with rows from all your servers, and **Continue Watching** that survives restarts
- **Emby**: home rows, libraries, genres, search, audio language choice, quality (resolution) choice
- **Flix-style movie sites**: posters, details, seasons and episodes, search, resolution choice
- **File servers** (h5ai, Apache, nginx, WebDAV, FTP): browse folders and play files
- **Local and USB storage**: browse, play, rename, copy, move and delete files
- **Music player** with cover art and background playback
- **Subtitles**: from files next to the video, or found online (SubDL, OpenSubtitles). Subtitles you download are kept and reused
- **Resume Watching** on every title, with progress shown on posters
- **Player**: volume on ZL / ZR, hold + to reset volume, stereo audio by default, 30 or 60 fps limit
- **Power saver**: the screen drops to a low frame rate when nothing moves, so the console stays cooler
- Updates itself from the About tab

## Install

1. Download `SwitchFlix.nro` from the [latest release](https://github.com/zhtipu/switchflix/releases/latest).
2. Copy it to `/switch/SwitchFlix/` on your SD card.
3. Install SwitchFlix.nsp via DBI or Awoo Installer
4. Open **SwitchFlix** from home screen.
   (Alternatively) Open it from the Homebrew Menu. Use **title takeover** (hold R when launching a game), not the album applet, so the app has enough memory.

## Add your servers

**Easy way: a server file.** Someone who runs or knows your servers can give you a small `.json` file
(the SwitchFlix Server Tool makes them). Put it here:

```
/switch/SwitchFlix/servers/
```

Start SwitchFlix. The servers appear in the sidebar. Each file is read once, then renamed to `.json.done`.

**By hand.** Go to **Settings**, then add a source:

| Type | Address | Notes |
|---|---|---|
| Emby | `emby://host:8096/` or `embys://host:443/` | user and password if the server needs them |
| File index | `http(s)://host/path/` | any folder listing |
| Flix site | `flix://host:80/` | movies and TV series |
| WebDAV / FTP / SFTP | `webdav(s)://`, `ftp://`, `sftp://` | |

## Controls

| Button | Does |
|---|---|
| A / B | select / back |
| X | **Filters** (libraries, genres, sorting) |
| Y | edit a source, or pause background music |
| + | search |
| ZL / ZR | volume down / up in the player |
| hold + | reset volume (in the player) |

## Subtitles

- **Automatic download** can be switched off in Settings. Your language is English by default.
- To use online services, save your key as a plain text file, the key and nothing else:
  - `/switch/SwitchFlix/api/subdl.txt`
  - OpenSubtitles needs its own files, see the examples in the release.
- Your own subtitle file can be picked from the player menu. Downloaded subtitles are cached in `/switch/SwitchFlix/subtitles` and can be cleared in Settings.

## Folders on the SD card

| Folder | What is in it |
|---|---|
| `/switch/SwitchFlix/servers/` | server files to import |
| `/switch/SwitchFlix/api/` | subtitle API keys (text files) |
| `/switch/SwitchFlix/subtitles/` | downloaded subtitles |
| `/switch/SwitchFlix/Music/` | default music folder |
| `/switch/SwitchFlix/switchflix.log` | log of the last run (the run before is `switchflix.prev.log`) |

## Problems?

- **The app closes by itself:** reopen it with title takeover. Send `switchflix.log` and `switchflix.prev.log` with your report. If the console shows a crash report, send the newest file from `/atmosphere/crash_reports/`.
- **A server stops working:** the site may have changed. Ask whoever gave you the server file for a new one.
- **No sound on a video:** open the player menu, pick the audio track, and keep the output on stereo.

Please open an [issue](https://github.com/zhtipu/switchflix/issues) with the logs.

## Credits and license

Based on [Switchfin](https://github.com/dragonflylee/switchfin) by dragonflylee. Licensed under Apache-2.0, see `LICENSE`.

SwitchFlix is a player for servers you have legal access to. It does not provide any content.

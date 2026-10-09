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

**Step A. Install the forwarder (once)**

1. Put the .nsp file on the SD card, or on a USB stick.
2. On the Switch, open your install tool (for example DBI or Tinfoil).
3. Choose the .nsp file and press Install.
4. When it finishes, a SwitchFlix icon appears on the Switch's home screen. You can delete the .nsp file now.

**Step B. Put the app file on the SD card**

1. Turn the Switch off and put the SD card in a computer.
2. Open the folder switch, then make a new folder inside it called SwitchFlix.
3. Put SwitchFlix.nro in that folder.
4. Put the SD card back in the Switch.

**Step C. Open it**
Tap the SwitchFlix icon on the home screen. The forwarder starts the app from the folder you made in step B.

## Add your servers

1. Download **SwitchFlix-Server-Tool.zip** from the GitHub release.
2. Right-click it and choose **Extract All**, and put the folder anywhere (for example, your Desktop).
3. Open the folder and double-click **SwitchFlix-Server-Tool.exe**.
4. If Windows warns about an unknown program, click **More info**, then **Run anyway**.

Keep the exe next to the `_internal` folder. It won't work without it.

## Add a server
1. Type the server address in the box on the left. Use the web address your provider gave you, for example `http://movies.example.com`.
2. Only if the server asks for a user name and password, type them in. Otherwise leave those boxes empty.
3. Press **Analyze** and wait a few seconds.
4. Read the result on the right:
   - **Ready for SwitchFlix** means a video really opened. You can go on.
   - **Not usable yet** means the tool could not reach a video. Go to "If it says not ready" below.
5. Type a name you like in **Server name in the app**.
6. Press **Save server file** and save `.json` file and Put it here:
```
/switch/SwitchFlix/servers/
```

**Alternatively,**
8. Put your Switch's SD card in the computer. Press **Write to SD card** and choose the SD card itself (the drive, not a folder).
9. Put the card back in the Switch and open SwitchFlix. The server appears on the left side.


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

## Server Compatibility:

- **Emby servers (emby://, embys://):** Home rows, libraries, genres, search, playback with a resolution choice, audio language pick. A passwordless account signs in by itself. Jellyfin looks the same but is untested, so it may only partly work.
- **Ovoo movie portals (flix://, for example PlayTimeBD):** lists, genre/country/language/rating filters, detail pages, seasons and episodes, search. Streams are HLS, with subtitles from the site when it lists any. The site must answer on plain http. You can edit the site's settings in a profile file on the SD card.
- **Movie hub portals (hub://, hubs://, for example flixhub):** lists, genre and sort, detail, series with episodes, search. Video is a plain file, over http or https. For https the app uses its local helper. Today the page markers for this kind are built into the app and fit flixhub. Making them profile-driven is the work in progress.
- **Directory indexes (http://, https://):** Apache, nginx, h5ai. You can browse folders and play files, and the app builds a search index of them.
- **WebDAV (webdav://, webdavs://).**
- **FTP and SFTP (ftp://, sftp://):** the app can open them, but the tool doesn't check them.
- **Local and USB storage,** including rename, copy, move and delete, and music folders.

## What the Server Tool recognises and tests

Emby API server, Ovoo movie portal, movie hub portal, WebDAV, directory index.
A server counts as ready only when a video opens.
Anything else goes to the problem report.

## What does not work

Sites that need a login, build their pages only with scripts, or hide the video: the tool and the app can't read them.
HLS streams over https: the player has no TLS support. Direct video files over https only work for hub sites, through the helper.
Plex, Xtream or IPTV portals, Kodi, Stremio: not supported.


## Problems?

- **The app closes by itself:** reopen it with title takeover. Send `switchflix.log` and `switchflix.prev.log` with your report. If the console shows a crash report, send the newest file from `/atmosphere/crash_reports/`.
- **A server stops working:** the site may have changed. Ask whoever gave you the server file for a new one.
- **No sound on a video:** open the player menu, pick the audio track, and keep the output on stereo.

Please open an [issue](https://github.com/zhtipu/switchflix/issues) with the logs.

## Credits and license

Based on [Switchfin](https://github.com/dragonflylee/switchfin) by dragonflylee. Licensed under Apache-2.0, see `LICENSE`.

SwitchFlix is a player for servers you have legal access to. It does not provide any content.

# MPEG-DL-TOOL Video Downloader

[日本語](README.md) | **English**

A Windows tool that finds the videos on a web page and downloads them.
Besides YouTube and other supported sites, it can also find players embedded from other pages (iframes) and videos that JavaScript loads later (HLS/DASH streams).

> [!IMPORTANT]
> **Please read before use**
> - Only download videos **that you own the rights to, that the rights holder has permitted, or that the site's terms of service allow you to download**.
> - Downloading a video while knowing it was uploaded illegally is prohibited by copyright law (this is the case in Japan, and similar laws exist in many other countries).
> - Many sites, including YouTube, prohibit or restrict downloading in their terms of service. Please check each site's terms.
> - Do not redistribute, upload, or sell downloaded videos without the rights holder's permission.
> - Videos with copy protection (DRM), such as those on Netflix, Amazon Prime Video, and Disney+, are not supported.
>
> The same notice is shown at first launch, and you can only use the tool after accepting it. You can read it again later with "ℹ Notice" at the top right of the window.

## Requirements

| Item | Details |
| --- | --- |
| OS | Windows 10 / 11 (64-bit) |
| Browser | Microsoft Edge (included with Windows). Google Chrome if Edge is not available |
| Internet | Required (about 120 MB of components are downloaded at first launch) |
| Languages | 日本語, English, 简体中文, 繁體中文, 한국어, Español, Français, Deutsch, Português (Brasil) |
| Free disk space | About 400 MB or more (for the components; downloaded videos need extra space) |

## Download

Download `MPEG-DL-TOOL-v(version).zip` from the [latest release page (GitHub Releases)](https://github.com/s-zak-software/MPEG-DL-TOOL/releases/latest) and extract it anywhere you like.

| Contents of the zip | Description |
| --- | --- |
| `MPEG-DL-TOOL.exe` | The application |
| `README_ja.txt` / `README_en.txt` | This guide (Japanese / English) |
| `TERMS_ja.txt` / `TERMS_en.txt` | Terms of use (Japanese / English) |
| `THIRD_PARTY_LICENSES.txt` | Licenses of the software included in the application |

No installation is needed. Put `MPEG-DL-TOOL.exe` anywhere you like and run it.

The release page lists the SHA-256 checksum of each file. If the value shown by running `Get-FileHash MPEG-DL-TOOL.exe` in PowerShell matches, you can be sure the file was not altered on the way.

## First launch

1. Double-click `MPEG-DL-TOOL.exe`.
2. If you see "Windows protected your PC", click "More info" → "Run anyway".
   - This warning appears for programs without a digital signature. Antivirus software may also show a false warning.
3. Choose the display language (English is preselected).
   - You can change it later with **"🌐 Language"** at the top right. The new language takes effect after a restart.
4. The terms of use are shown. Read them and click "Accept".
5. The components needed to process videos (yt-dlp, ffmpeg, etc.) are downloaded automatically. The main window opens when this finishes.

From the second launch on, the main window opens right away.

## How to use

1. Paste the URL of a page that contains a video (you can also use the "📋 Paste" button).
2. Click **"🔍 Find Videos"**. The videos found are shown in the list.
3. Check the videos you want (click a row to toggle it), then click **"⬇ Download Selected"**.
   - Click the "Save as (click to edit)" cell to rename the file (Enter to confirm, Esc to cancel; the extension is added automatically).
   - Progress is shown in the "Status" column, and finished rows turn green.
   - Double-click a finished row to show the saved file in its folder.
   - If a file with the same name already exists, it is not overwritten; a number is added instead, like "name (2)".
4. Open the destination folder with **"📂 Open Download Folder"** (the default is your "Downloads" folder).

For video pages on YouTube and other supported sites, you can also use "Download URL directly" (it is faster because it skips the search step).

### Add more while it is working

- You can enter new URLs and click "Find Videos" or "Download URL directly" even while analysis or downloads are running. The input box is cleared each time, so you can paste the next URL right away.
- Pages are analyzed one at a time, and the results are added to the bottom of the list.
- Downloads wait in a queue and run in parallel up to the "Simultaneous downloads" setting (1–5).
- When **"Automatically download found videos"** is checked (on by default), the most likely video (the one already checked in the list) is downloaded automatically when analysis finishes. Videos that are already downloaded or queued are skipped.
- Right-click a row to cancel, retry, rename, or remove just that row. "Cancel All" stops everything, including pages waiting to be analyzed.
- "Clear Finished" removes all finished rows from the list.

### Formats

| Format | Details |
| --- | --- |
| Best quality (MP4) | The highest resolution. At the same resolution, H.264 is preferred because it plays on most devices |
| Up to 1080p / Up to 720p (MP4) | Limits the resolution (when you want smaller files) |
| Audio only (MP3) | Saves only the audio as MP3 (192 kbps) |

### If no video is found: manual mode

Check "Show browser and play manually" and click "Find Videos" to open a browser window.
Log in, close ads, press the play button, and so on yourself, and click "Stop capture" once the video starts playing (closing the browser also ends the capture).
Login information is stored in a location used only by this tool, so it is also used by automatic analysis from then on.

## Updates

Click **"🔄 Update"** at the top right to check for component updates (yt-dlp, ffmpeg, deno, Playwright, etc.) and update them all at once.

- The tool also checks automatically a few seconds after starting. If updates are available, the button changes to "🔄 Updates (number)".
- Updates take effect after a restart. If something is still running, or if you choose "No", they are applied automatically the next time you start the tool.
- If a site changes and downloads stop working, try updating first.

The tool itself (the exe) does not update automatically and does not notify you of new versions (so that the tool never connects anywhere on its own for this). When a new version is released, replace the exe (your settings and components are kept).

- When "🔄 Update" shows "All components are up to date", choose "Yes" to open the distribution page in your browser, where you can check for and download the latest version.
- If you have a GitHub account, set "Watch" → "Custom" → "Releases" on the [distribution page](https://github.com/s-zak-software/MPEG-DL-TOOL) to get an email from GitHub when a new version is released.

## Troubleshooting

- **Downloads stopped working** … Update the components with "🔄 Update".
- **"Access denied (403)" is shown** … Play the video in manual mode, then try again.
- **No video is found** … Try manual mode. Videos protected by DRM cannot be found.
- **Something is not working right** … Delete the `%LOCALAPPDATA%\MPEG-DL-TOOL\lib` folder and start the tool again to reinstall the components.
- Unexpected errors are recorded in `%LOCALAPPDATA%\MPEG-DL-TOOL\error.log`. Attaching it to your inquiry makes it easier to find the cause (it may contain URLs of pages you visited).

## Network access and stored data

**Network access**
- The tool connects to PyPI (the official Python package repository, pypi.org) to download components and check for updates. Downloaded components are checked against the SHA-256 checksums published by PyPI to make sure they were not altered in transit.
- When finding or downloading videos, it connects to the page you entered and to the servers that deliver the video.
- The tool has no feature that sends usage information or similar data to the developer.

**Data stored on your computer** (all inside `%LOCALAPPDATA%\MPEG-DL-TOOL`)

| Location | Contents |
| --- | --- |
| `lib` | Components (yt-dlp, ffmpeg, etc.) |
| `browser-profile` | Data of the browser used for analysis (site login status, cookies, etc.) |
| `error.log` | Error log |
| `settings.json` | Settings (display language) |
| `notice_accepted` | Record that you accepted the terms of use |

You can open `%LOCALAPPDATA%` by typing it into the address bar of File Explorer.

## Uninstall

1. Delete `MPEG-DL-TOOL.exe`.
2. Delete the `%LOCALAPPDATA%\MPEG-DL-TOOL` folder (this removes the components, login status, and all other data).

If you used the tool under its former name (DL-Tool), also delete `%LOCALAPPDATA%\DL-Tool` if it still exists.

## Support development

Your support for MPEG-DL-TOOL's development is a great encouragement. The support window is shown once at first launch, and you can open it anytime afterward from **"☕ Support"** at the top right of the window.
All features are available whether or not you support it (supporting does not unlock features or come with rewards).

- From Japan: [OFUSE](https://ofuse.me/c3ac3f49)

## Terms of use and disclaimer

This tool is free to use. See the [Terms of Use](TERMS.en.md) for the conditions (redistribution, modification, and reverse engineering are prohibited).

This tool is provided without any warranty. The author is not responsible for any damage resulting from its use.
You are responsible for how you use this tool.

## Third-party software

This tool uses the following open-source software. All rights to each piece of software belong to its respective authors.

**Included in the exe**

| Software | License |
| --- | --- |
| Python | PSF License |
| packaging | Apache-2.0 or BSD-2-Clause |
| PyInstaller (the exe's startup code) | GPL-2.0-or-later (thanks to its exception clause, the GPL does not apply to the generated exe) |
| Tcl/Tk (user interface) | Tcl/Tk License (BSD-style) |
| Microsoft Distributable Code (included with Python) | Subject to Microsoft's conditions ([Terms of Use](TERMS.en.md), Article 5) |

The full text of these licenses is in `THIRD_PARTY_LICENSES.txt` included in the zip.

**Downloaded from PyPI at first launch and when updating** (not included in this tool; your computer downloads them directly from PyPI)

| Software | Purpose | License |
| --- | --- | --- |
| yt-dlp | Analyzing and downloading videos | Unlicense |
| yt-dlp-ejs | Helper for yt-dlp | Unlicense / MIT / ISC |
| FFmpeg (via imageio-ffmpeg) | Merging and converting video and audio | GPL (imageio-ffmpeg itself is BSD-2-Clause) |
| Playwright | Analysis in the browser | Apache-2.0 |
| Deno | Running JavaScript for yt-dlp | MIT |
| requests / urllib3 / idna / charset-normalizer | Networking | Apache-2.0 / MIT / BSD-3-Clause / MIT |
| certifi | Certificates for secure connections | MPL-2.0 |
| mutagen | Writing metadata to audio files | GPL-2.0-or-later |
| Brotli / websockets / greenlet / pycryptodomex | Helpers for yt-dlp and Playwright | MIT / BSD-3-Clause / MIT, PSF / BSD, Public Domain |

Component versions change with updates. The full text of each license is included in each component's folder (`*.dist-info`) inside `%LOCALAPPDATA%\MPEG-DL-TOOL\lib`.


## Author and contact

- Author: s.zak.software
- Distribution page: https://github.com/s-zak-software/MPEG-DL-TOOL
- Bug reports and questions: [GitHub Issues](https://github.com/s-zak-software/MPEG-DL-TOOL/issues) (a GitHub account is required)

© 2026 s.zak.software

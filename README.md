# Luna

A small browser for Windows with nothing in the way: tabs down the side or across the top, and the page.
Pages run on Chromium through **WebView2**, the engine already in Windows, so there is no second copy of Chromium
to download or keep in memory.

This repository holds **signed releases only**. The latest build is on the
[Releases page](https://github.com/lavi-design-studio/luna-releases/releases/latest).

## Install

1. Download **`LunaBrowser-win-Setup.exe`** from the latest release and run it. Luna installs for your user
   (no administrator rights) under `%LOCALAPPDATA%\LunaBrowser` and adds a Start menu entry.
2. Setup is built to install the .NET 9 Desktop Runtime and the WebView2 runtime if your PC does not have them.
   (Windows 11 already has WebView2. The runtime step has not been tried on a clean machine.)
3. Windows 10 or 11, 64-bit.

Prefer no installer? `Luna-win-x64.zip` is the app on its own (needs the .NET 9 Desktop Runtime and WebView2), and
`Luna-win-x64-standalone.zip` carries .NET with it (about 60 MB).

## Updates

An installed Luna asks this repository every few hours whether there is a newer build, downloads only what changed
(a delta of a few hundred KB, with [Velopack](https://velopack.io)), checks that it is signed with Luna's release key
(ECDSA P-256), and puts it in place when you press **Restart to update** or the next time Luna closes. If a new build
can't open a window, the one before it is put back. Settings turns it off. Every file in a release has a `.sig`.

## What it does

- **One field** (`Ctrl+L`): addresses from your history, tabs already open, search, sums, site shortcuts
  (`yt moon landing`, `w moon`) and every command by name after `>`. Nothing you type is sent before Return.
- **Tabs** down the side or across the top, **pins**, **spaces** (each stays signed in or starts afresh), **split view**,
  **private tabs**, tabs that cost nothing until you look at them, and a sidebar that slides in from the edge.
- **Reading mode**, **hide anything** on a site for good, **floating video**, ad and tracker blocking in the network layer.
- **Chrome extensions** straight from the Chrome Web Store.
- **Import** bookmarks and history from Chrome, Edge, Brave, Vivaldi and Firefox (Settings › This PC). Passwords,
  cookies and cards are never read.
- **A look of its own**: Luna (pearl by day, umbra by night) or Liquid Glass, with a light that follows the page
  behind the frame, and an optional *Luminous* plate (Settings › General) that pours colour from the edge and the foot
  of what is lit.

### For people who design

- **Grid** (`Ctrl+Shift+G`) draws the page's own CSS grid, **Design system** (`Ctrl+Shift+D`) lists its colours, type
  and layout, and **Inspect** (`Ctrl+Shift+E`) shows any element's properties on hover.
- **Design snapshot** (`Ctrl+Shift+F`) saves the page (boxes, text lines, fonts, colours, gradients, shadows, pictures,
  flex and grid layout) and puts it on the clipboard.
  - **Paste into Figma** (`Ctrl+V` on the canvas) gives named frames, auto layout where the page's layout is
    reproduced exactly, gradients, shadows and text that shows at once. Figma does not take pictures this way.
  - **Luna import**, a small Figma plugin that comes with Luna (Settings › General › *Show the plugin folder*, then
    Plugins › Development › Import plugin from manifest…): run it and press `Ctrl+V` in its window to bring the page
    in with its **pictures**, icons, SVG and CSS grids built as Figma grid layouts.
  - It is a snapshot of one page at one size: video comes as a frame, WebGL as an empty layer, and web fonts Figma does
    not have are replaced by the nearest it does.

## The numbers

Measured on one PC (Windows 11), release build:

| | |
|---|---|
| Installed | about **6 MB** (the engine is Windows' own) |
| To the first window | **~0.45 s** |
| Before the first page | **1 process, ~45 MB**; Chromium starts when a page is opened |
| At rest | **0% CPU** for the browser's own window |

## Credits

Luna follows the structure of [Search](https://officecommun.com/search) by Office Commun (MIT), whose pieces it borrows;
see [THIRD-PARTY-NOTICES.md](THIRD-PARTY-NOTICES.md). It learns from the principles of [Mercury OS](https://www.mercuryos.com/) without
copying its look. Pages run on the Microsoft Edge WebView2 runtime. Updates use Velopack.

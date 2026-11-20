Installation instructions:
I don't have an Apple developer account, so to get the app working, you will need to drag it into your Applications folder, then open the Terminal and type “xattr -cr /Applications/banana.app”

# Banana 🍌

Banana is a macOS menu-bar and desktop utility that brings a Windows-style taskbar, a Spotlight-like launcher, an interactive notch, a screenshot and screen-recording suite, USB RGB lighting control and a long list of small system tweaks to the Mac — all in one native app, written in Swift/AppKit with no third-party dependencies.

Almost every feature is optional and has its own switch (and, where it makes sense, several sliders and menus) in the built-in Settings window, which also has a search bar, a backup/restore function and a language selector (Italian, English, Spanish, German).

- **Requires:** macOS 14 or later (Apple Silicon or Intel).
- **Runs as:** a background agent (no Dock icon of its own), started at login through a LaunchAgent.
- **Permissions it may ask for** (only for the features that need them): Accessibility, Input Monitoring, Screen Recording, Microphone, Automation (Finder, to empty the Trash), and audio capture (per-app volume).

---

## Contents

1. [Taskbar (Dock replacement)](#1-taskbar-dock-replacement)
2. [Window management](#2-window-management)
3. [Launcher](#3-launcher)
4. [⌘Tab window switcher](#4-tab-window-switcher)
5. [Notch tools and interactive island](#5-notch-tools-and-interactive-island)
6. [Volume and brightness HUD](#6-volume-and-brightness-hud)
7. [Menu-bar items](#7-menu-bar-items)
8. [Quick panel](#8-quick-panel)
9. [Capture: screenshots, text, colors and screen recording](#9-capture-screenshots-text-colors-and-screen-recording)
10. [Clipboard history](#10-clipboard-history)
11. [USB RGB lighting](#11-usb-rgb-lighting)
12. [Keyboard and mouse](#12-keyboard-and-mouse)
13. [Audio](#13-audio)
14. [Power](#14-power)
15. [Displays](#15-displays)
16. [Tools](#16-tools)
17. [Customization and backup](#17-customization-and-backup)
18. [Building and installing](#18-building-and-installing)
19. [Project layout](#19-project-layout)
20. [Notes and limitations](#20-notes-and-limitations)

---

## 1. Taskbar (Dock replacement)

A Windows-style taskbar that replaces the macOS Dock (the system Dock is hidden while Banana runs and restored on exit; if the bar is turned off the Dock comes back).

- **Pinned and running apps** in one bar: drag files, apps and links onto it to pin them, drag icons to reorder, drag onto the Trash icon to delete.
- **Dock-style magnification** when the cursor passes over the icons (size, gap and magnification radius are adjustable).
- **Position:** bottom, left or right edge. On the vertical bars the icons are rotated/mirrored correctly.
- **Auto-hide:** the bar slides away and returns when the cursor touches the screen edge.
- **Sections:** optional gap and thin separator between pinned and running apps; optional bounce when an app launches.
- **Clock:** optional clock at the right of the bar, with seconds, date and 12-hour format options.
- **Show-desktop strip** in the corner: hides every window; a second click brings them back.
- **Window previews:** hovering an app icon shows its windows (thumbnails need Screen Recording; titles otherwise). Click to raise, with an optional close button, and an option to show previews only when the app has several windows.
- **Click an icon of the frontmost app to minimize it**, as on Windows.
- **Per-app context menu:** Open, Quit, "Don't close with ✕", "Quit with the last window", Change icon…, Show in Finder, Keep in bar / Remove from bar, Empty Trash, and bar appearance options (style, color, icon style).
- **Trash** in the bar, with full/empty icon and drag-to-trash.
- **Icon style:** normal or monochrome; solid color or translucent bar.
- **Custom icons for any app:** *Settings → Bar → Custom app icons* opens a panel listing every app in the bar. Drag an image (PNG, JPG, ICNS, PDF…) or another app onto its row and the icon is replaced everywhere (bar, switcher, previews). Images are automatically normalized to the macOS icon style: 80% body, continuous "squircle" corners, soft shadow; already-shaped images (transparent corners) keep their shape. A *Reset* button restores the original.
- **Optional "File Explorer" icon for Finder:** a hand-drawn yellow folder with a blue base (off by default; Finder keeps its original icon).
- **Multi-display:** the bar, launcher, clipboard and HUD can appear on every connected display.
- **Fullscreen aware:** the bar hides when an app (or a YouTube video) goes full screen, and the black band behind the notch is kept in sync when switching apps with ⌘Tab in full screen.

## 2. Window management

- **Windows above the bar:** windows that would sit under the bar are shortened.
- **Green traffic-light button:** fills the space between the menu bar and the taskbar (instead of macOS full screen); ⌥-click gives real full screen.
- **Red traffic-light button:** closes the app like ⌘Q when it is the last window; with several windows it closes only the clicked one. Apps built to live in the background (menu-bar apps) are never quit; you can add your own exceptions ("apps that stay open with the red dot").
- **Quit an app when its last window closes:** per-app list (minimized windows and windows on other Spaces count as open). Works for Finder too once its *Quit* menu item is enabled in macOS.
- **Window snapping:** keyboard shortcuts for left/right/top/bottom halves, thirds, two-thirds, corners, maximize, center, and "move to next display", with an optional slide animation.
- **New windows on the main display:** windows that appear on another display are moved to the main one.
- **Window placement for new windows** (centered / cascade / remembered, configurable).

## 3. Launcher

A Spotlight-style launcher (opened with a shortcut or by tapping ⌘ alone) with fuzzy matching, a usage-ranked history and a configurable position (center, top, or remember last position), screen and animation (fade, zoom, slide). It is movable by dragging, closes on an outside click, and can show frequent apps before you type.

Prefix modes:

| Prefix | What it does |
|---|---|
| *(none)* | Search apps (optionally system apps and special entries: Trash, Camera, Clean keyboard) |
| `.` | Search files with Spotlight (Enter opens, ⌘Enter reveals in Finder) |
| `,` | Calculator and converter: `12*7`, `5 km in miles`, `20 c in f`, `100 eur in usd`, dates (`in 30 days`), times (`14:30 + 2h`), colors |
| `?` | Web search (Google, DuckDuckGo, Bing, Brave or your own engines); typing a site (`youtube.com`, `localhost:3000`) offers **Open** first, search second |
| `-` | Search the clipboard history and paste |
| `timer 10 min` | Starts a timer |
| system commands | Lock, Sleep, Display sleep, Dark mode, Restart, Shut down, … by name |

Plus custom web-search keywords, multi-language keywords for special entries, hidden-apps list and an option to clear usage history at every start.

## 4. ⌘Tab window switcher

Optional replacement for the macOS app switcher: one card **per window** (not per app) with a live thumbnail, including minimized windows and apps without windows (both optional). Needs Accessibility.

## 5. Notch tools and interactive island

- **Notch cover:** a black band behind the menu bar so the notch blends in; menus stay on the same row. Conditions are configurable (maximized window, visible window, empty desktop) and it works on external displays when "everything on every display" is on.
- **Interactive notch (island):** hovering (or clicking) the notch opens a panel with the widgets you choose: now playing (Music/Spotify, with progress, artwork and controls, including the site name for media playing in Zen/browsers), weather (temperature, humidity/wind, next hours, colored icons), file shelf (drag files in and out, optionally remembered after restart), clock, battery, CPU/RAM, recent clipboard items and quick timers. Widgets can be dragged to reorder. Dragging a file near the notch opens the shelf.

## 6. Volume and brightness HUD

Replaces the macOS indicator with a notch-style pill below the notch (works on external screens too), with optional percentage and ⇧⌥ for small steps; shows the output device icon for Bluetooth/external audio. Brightness can be unified across all displays (hardware control where available, software dimming otherwise).

## 7. Menu-bar items

- **iPhone-style battery:** percentage inside the battery, green while charging, yellow in Low Power Mode, red below 20%; click for a Low Power Mode toggle; optional hide when full. The macOS battery item can be removed from the menu bar.
- **System monitor:** CPU, CPU temperature, GPU, RAM, network, free disk space and battery in one compact item.
- **Caffeine:** a cup icon while the Mac is being kept awake.
- **Banana logo menu** with quick access to settings, restart and quit.
- **Microphone mute notice** when you toggle the mic.

## 8. Quick panel

A control-center-style panel from the menu bar: volume, per-app volume mixer, microphone choice and mute, display brightness, Wi-Fi/Bluetooth/dark-mode/etc. toggles, screenshot and screen-recording buttons, and tool shortcuts (copy text, copy color, scratchpad, snippets, window switcher, quit apps).

## 9. Capture: screenshots, text, colors and screen recording

**Screenshots** — area, window or full screen, global shortcuts; press Space during selection to switch area ↔ window. After the capture a thumbnail appears bottom-left with a trash can and a check mark (auto-saves after a configurable delay, hover to pause the countdown). Options: destination (file / clipboard / both), format (PNG/JPG/HEIC) and quality, file-name template (`%Y %m %d %H %M %S %a %t`), folder per day or per type, delay (3/5/10 s), cursor, window shadow, shutter sound, notice, open in Preview.

**Copy text from the screen (OCR)** — drag an area; the recognized text (and QR-code contents) goes to the clipboard. Options: accurate/fast, join lines into a paragraph, notice.

**Copy color from the screen** — an eyedropper; the color code (HEX, RGB, HSL…) goes to the clipboard.

**Screen recorder** — a QuickTime-style floating panel (move it freely; it can open at the bottom, center, top or where you left it, on the cursor's or main screen):
- **What:** full screen, a single window (click to pick) or a selected area (drag).
- **Frame rate:** 24, 30, 60 or 120 fps.
- **Quality:** FHD, 2K or 4K (never above the real resolution of the display).
- **Audio:** microphone on/off and Mac system audio on/off (two audio tracks in the same file).
- **Recording indicator:** time (h:mm:ss), a pause button and a red stop square; place it top, bottom, top-right or top-left. Pausing leaves no gap in the video.
- Output is a `.mov` (H.264, or HEVC for 4K/120 fps) in the screenshots folder, followed by the same thumbnail preview (trash / reveal in Finder). Banana's own windows are never recorded.

## 10. Clipboard history

Text, images and files copied from Finder, kept in memory (optionally persistent, with an expiry), searchable, with a context menu to **Copy / Pin / Delete**, pinned items that survive, ignore-list for password managers, clear-on-quit option, and a global shortcut. Reachable from the launcher with `-`, the island widget and the quick panel.

## 11. USB RGB lighting

*Settings → USB RGB.* Per-device on/off (state remembered and re-applied when the device is plugged back in) and, where the protocol allows it, **fixed color presets**: White, Light blue, Blue, Fuchsia, Purple, Lime, Green, Yellow, Orange, Red; plus a **"Blue in colors"** slider to compensate for the strong blue LEDs. A "?" button at the bottom of the page lists the supported brands.

| Brand | Devices | Capabilities | Verified on hardware |
|---|---|---|---|
| Razer | mice (OpenRazer protocol) | on/off | ✅ DeathAdder Essential |
| Trust GXT | mice with Instant A704 chip | on/off | ✅ |
| EVision / SONiX | keyboards (iOPPLE, Redragon, Ajazz, Diereya…) — protocol V2 with legacy fallback | on/off, fixed colors, 16 effects (static, breathing, wave, rainbow, ripple, …) with speed and color | ✅ iOPPLE |
| Logitech G | HID++ 2.0 mice/keyboards (G203, G502 X, G915…) | on/off, fixed colors | ⚠️ not tested |
| Keychron / QMK / VIA | keyboards with VIA firmware (also Glorious GMMK) | on/off, fixed colors | ⚠️ not tested |
| Glorious | Model O / Model D (wired) | on/off, fixed colors | ⚠️ not tested |
| HyperX | Pulsefire Surge, Core, FPS Pro, Haste | on/off, fixed colors | ⚠️ not tested |
| SteelSeries | Rival 3 | on/off, fixed colors | ⚠️ not tested |
| Corsair | protocol V2 (K55/K60/K70, Harpoon…) | on/off | ⚠️ not tested |

The drivers are derived from the public [OpenRGB](https://openrgb.org) protocol documentation. Devices that don't answer show an inline error. Requires Input Monitoring.

## 12. Keyboard and mouse

- **Mouse side buttons (back/forward)** work in every app, including Finder (via a synthetic swipe gesture), with an option to leave Safari, Chrome, Brave, Edge and Arc alone and a choice of method/keys.
- **Key remapping:** per-key rules editor, plus an option to reset macOS modifier-key mappings.
- **F-keys like on a Mac** for external keyboards (brightness, Mission Control, launcher, media, mute/volume) and **Home/End** to line start/end like on Windows.
- **Custom global shortcuts:** open a link, run a terminal command, paste a text snippet, or open an app/file.
- **Snippets:** quick phrases opened with a shortcut and pasted into the front app.
- **Keyboard lock / clean mode** for wiping the keyboard.
- **Every action can have its own global shortcut** (snapping, screenshots, recorder, scratchpad, lock, sleep, dark mode, hidden files, desktop icons, switcher, settings, restart…).

## 13. Audio

- **Per-app volume mixer** (Core Audio taps).
- **Microphone input choice:** automatic (a wired external mic wins) or a specific device; microphone mute toggle with notice.
- **Output device icon** in the HUD for Bluetooth devices (generic Bluetooth symbol).
- **Audio settings page** with the above plus volume-step options.

## 14. Power

- **Keep awake (Caffeine):** timed or indefinite; options to let the display sleep, pause while the Mac is locked, start automatically, keep awake while chosen apps are open, run with the **lid closed** (one-time password to enable), notice at the end, battery cut-off.
- **Low Power Mode toggle** from the battery item.

## 15. Displays

- **Everything on every display** (bar, launcher, clipboard, HUD).
- **Main display choice** (automatic = external if connected).
- **Automatic HiDPI** for external monitors (proposes and picks the best mode).
- **Unified brightness** across built-in and external screens.
- **System animations** switch and speed control for Banana's own animations.

## 16. Tools

- **Scratchpad:** a quick note window.
- **Quit apps panel:** quit one or all apps (skipping Finder and a "never quit" list).
- **Cache cleaner** and **Uninstaller** (removes an app and its leftovers).
- **URL tracker cleaner:** when you copy a link, strips `utm_*`, `fbclid`, `gclid`, `si` and similar and keeps only the useful part (Amazon → `/dp/code`, YouTube → video and time, …).
- **Hide/show desktop icons and hidden files**, dark-mode toggle, lock, display sleep, sleep.
- **Camera preview** from the launcher.

## 17. Customization and backup

- A **settings search bar**, sidebar pages and "restore defaults".
- **Almost every feature is adjustable** through switches, sliders, pop-up menus, app lists, color pickers and text fields (the "5× more customizable" pass).
- **Preference backup / restore** to a file.
- **First-run feature picker** (choose what to enable) and permission setup guidance.
- **Languages:** Italian, English, Spanish, German (translation dictionary guarded by `checkdict.py`).

## 18. Building and installing

```bash
./build.sh                 # optimized build, installs to /Applications/Banana.app, signs and restarts the LaunchAgent
FAST=1 ./build.sh          # same, but unoptimized (-Onone): ~25 s instead of many minutes
FAST=1 ./package.sh ~/Desktop/Banana.dmg   # universal (arm64 + x86_64) DMG
```

- `build.sh` compiles `Sources/**/*.swift` with `swiftc`, writes the `Info.plist`, installs the app, signs it with a local identity (so Accessibility/Screen Recording grants survive rebuilds — create one with `setup-signing.sh`), and restarts it through `~/Library/LaunchAgents/local.fra.banana.plist`.
- `checkdict.py` runs first and fails the build if the translation dictionary has duplicate keys.
- Info.plist usage descriptions: Apple Events, audio capture, camera, microphone.

## 19. Project layout

```
Sources/
  App/        Controller (wiring, actions, settings hooks)
  Audio/      mixer, microphone choice
  Bar/        taskbar views, store, zones
  Branding/   Banana icon, File-Explorer-style icon, custom app icons
  Capture/    screenshots, OCR, color picker, screen recorder
  Clipboard/  clipboard history
  Core/       globals, preferences, translations, backup
  Display/    brightness, notch fit, display helpers
  Input/      shortcuts, key remaps, mouse side buttons, USB RGB drivers
  Island/     interactive notch and widgets
  Launcher/   launcher and its modes, camera preview
  Media/      media keys, notch HUD, now playing
  MenuBar/    battery, quick panel, logo menu
  Monitor/    system monitor
  Power/      keep awake
  Preview/    window previews
  Settings/   settings window and model
  Setup/      first-run picker and permissions
  Switcher/   ⌘Tab switcher
  System/     quick toggles, Dock handling, animations
  Tools/      scratchpad, quit apps, cache cleaner, snippets, trash, URL cleaner
  Uninstaller/
  Windows/    snapping, close/zoom handling, placement
```

## 20. Notes and limitations

- Banana is a personal project distributed locally; it is signed with a local certificate, not notarized.
- Some drivers (Logitech, Keychron/QMK, Glorious, HyperX, SteelSeries, Corsair) were written from OpenRGB's protocol documentation and **have not been tested on real hardware**.
- The Trust GXT 929 Helox (`145F:0326`) is not supported: its protocol is not publicly documented.
- The macOS ⌘Tab and Dock cannot be modified directly; Banana replaces them with its own switcher and bar.
- Quitting Finder with the ✕ requires the macOS Finder option `defaults write com.apple.finder QuitMenuItem -bool true`.
- Screen-recording resolution is capped at the display's real resolution, and 144 Hz external displays are limited to whatever refresh rates macOS exposes for the connection.

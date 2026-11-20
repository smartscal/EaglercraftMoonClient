# ☾ Moon Client

**A lightweight mod menu, HUD, and performance toolkit for EaglercraftX 1.20.6, built into a single HTML file that runs in your browser.**

Made by **SmartScal**.

> **Status:** early release (v1.6). Several features are marked *Experimental* because they depend on how the game handles simulated input and low-level rendering. They are off by default or clearly labeled, and the [Troubleshooting](#troubleshooting) section covers what to do if one misbehaves.

---

## Contents

- [What is Moon Client?](#what-is-moon-client)
- [Quick start](#quick-start)
- [Controls](#controls)
- [Features](#features)
- [Not included (and why)](#not-included-and-why)
- [Settings and saved data](#settings-and-saved-data)
- [Privacy and safety](#privacy-and-safety)
- [How it works](#how-it-works)
- [Building from source](#building-from-source)
- [Troubleshooting](#troubleshooting)
- [FAQ](#faq)
- [Known limitations](#known-limitations)
- [Changelog](#changelog)
- [Credits and legal](#credits-and-legal)

---

## What is Moon Client?

[Eaglercraft](https://eaglercraft.com) lets you play a Minecraft-compatible game in a web browser. **EaglercraftX 1.20.6** is a compiled WebAssembly (WASM-GC) build of that game, so its code can't simply be edited like a normal mod.

Moon Client works around that. It:

1. **Adds an overlay on top of the game page**: a mod menu, HUD widgets, a developer console, and more.
2. **Hooks into the browser** (rendering, timing, audio, networking) to add features such as Fullbright, Render Scale, and an FPS limiter without touching the game's compiled code.
3. **Patches the game's asset bundle** to give it a new look: a Moon Client logo, a custom splash text, and a moonlit-ocean title screen.

Everything ships as **one `.html` file**. Open it in your browser and play.

## Quick start

1. Go to the [**Releases**](../../releases) page and download `MoonClient-1_20_6.html`.
2. Open the file in a Chromium-based browser (Chrome, Edge, Brave). It was built with these browsers in mind; other browsers may behave differently.
3. Wait for the game to launch.
4. Press **Right Shift** to open the Moon Client menu.

You can also click the **☾ Mods** button in the top-right corner of the title screen and pause menu.

## Controls

| Action | Default key | Notes |
|---|---|---|
| Open / close the mod menu | **Right Shift** | Rebindable under *General*. Left Shift is the game's sneak key. |
| Developer console | **F9** | Works at any time, including during launch. Esc closes it. |
| Zoom | Hold **C** | Scroll while zooming to change the amount. Rebindable. |
| Toggle Sprint | **R** | Experimental. Rebindable. |
| Toggle Sneak | **V** | Experimental. Rebindable. |
| Peek at a hidden password | Hold **Ctrl+G** (**Cmd+G** on macOS) | Only while typing a `/login` or `/register` command. |
| Move HUD elements | Drag with the mouse | While the mod menu is open. |

## Features

### HUD

| Mod | What it does |
|---|---|
| FPS Counter | Shows the game's frame rate. |
| CPS Counter | Left and right clicks per second. |
| Keystrokes | On-screen WASD, Space, and mouse buttons. |
| Clock | Your real-world time (12 or 24-hour). |
| Session Timer | How long you've been playing. |
| Toggle Status | Shows when Toggle Sprint or Toggle Sneak is active. |

All HUD elements are draggable, and positions are remembered.

### Visual

| Mod | What it does |
|---|---|
| **Fullbright** | Makes caves, nights, and other dark areas fully lit by overriding the game's light texture. Falls back to a screen brightness boost if the light texture isn't found. Three modes: *True fullbright*, *Screen gamma boost*, *Screen brightness*. |
| Zoom | Hold-to-zoom with optional smooth zoom and scroll adjustment. Implemented as a screen zoom, so it does not change field of view or mouse sensitivity. |
| Color Grade | Adjust saturation and contrast of the whole screen. |
| Smooth Hotbar *(experimental)* | Animated glide for the hotbar selector. Needs the right GUI scale (see *General*). |
| Animated Menu Background *(experimental)* | Replaces the spinning title-screen panorama with a still moonlit ocean: a glowing, pulsing moon, drifting clouds, and animated waves. Adjustable glow, wave speed, clouds, and detail level. |
| Menu Particles | Glowing fireflies and sparkles drifting over the title screen. Adjustable style, color, amount, and speed. |

### Optimization

| Mod | What it does |
|---|---|
| Render Scale *(experimental)* | Renders at 40–125% resolution and stretches the result. Lower values give a large FPS boost on weak GPUs. |
| Dynamic Resolution *(experimental)* | Lowers resolution automatically when FPS drops below your target and raises it again when there's headroom. |
| FPS Limit | Caps the frame rate (30–240) to save power and heat. |
| Background FPS Limit | Drops the frame rate while the window isn't focused. |
| High-Performance GPU | Asks the browser to use your dedicated graphics card. *Applies next launch.* |
| Low Latency Rendering *(experimental)* | Lets the browser present frames sooner. *Applies next launch.* |
| Disable Antialiasing | Turns off edge smoothing for a small performance gain. *Applies next launch.* |

### Gameplay

| Mod | What it does |
|---|---|
| Toggle Sprint *(experimental)* | Press a key once to keep sprinting. Works by holding Ctrl for you with simulated key presses. |
| Toggle Sneak *(experimental)* | Same idea, holding Left Shift. |

### Chat

| Mod | What it does |
|---|---|
| **Hide Password** | Masks what you type after `/login`, `/l`, `/register`, and similar commands so nobody can read it over your shoulder. Hold **Ctrl+G** to peek. |
| **Auto Login** *(experimental)* | Types your login command for you when you join a saved server. Save a server address (or `*` for any server), username, password, and a command prefix such as `/login` or `/l`. Includes a **Run now** test button. Types with simulated key presses, and checks the chat actually opened before typing anything. |

### Cosmetics

| Mod | What it does |
|---|---|
| Custom Player Tag | Turns an uploaded image into a Minecraft-style pixel tag (8–32 px, with a Minecraft dye color palette or original colors). Shown on **your own** HUD and downloadable as a PNG. Other players cannot see it. |

### Misc

| Mod | What it does |
|---|---|
| Mute When Tabbed Out | Pauses game audio while the tab is in the background. |
| Close Protection | Asks for confirmation before the tab or window closes. |

### General

- Change the menu key.
- Set the GUI scale used by overlays that line up with the game interface.
- Choose how the game resumes when you close a Moon Client window (*Automatically*, *Only lock the mouse*, or *Do nothing*).
- Reset all settings.

### Developer console (F9)

A built-in console that records everything from the moment the page loads, including the game's launch process.

- Captures logs, info, warnings, errors, uncaught errors, failed resource loads, and promise rejections.
- Filter by level, search, clear, **Copy**, or **Save** the whole log to a `.txt` file.
- Run JavaScript in the page from the input box (Up/Down for history).
- Logs useful diagnostics: browser info, WebAssembly/WebGL2 support, pointer-lock changes, and Moon Client's own status messages.

When reporting a bug, press **F9**, click **Save**, and attach the file.

## Not included (and why)

Some popular client mods **cannot** be built as a browser overlay, because they need to read or draw inside the compiled game itself:

- **AppleSkin** (saturation and food preview)
- **Armor HUD**
- **Chat Heads**
- **LambDynamicLights**
- **Moon Voice Chat** (also needs a voice backend on the server)
- **Player tag in the world** (drawing it beside names and syncing it to other players needs game and server support)
- **Smarter chunk rendering**

They appear greyed out under **Unavailable** in the menu. Adding them would require the game's source code and a rebuild of the game. The [Optimization](#optimization) mods are the closest available alternatives for performance.

## Settings and saved data

Settings are stored in your browser's `localStorage` under the key `moonclient.v1`. That includes mod toggles, HUD positions, your pixel tag, and any saved Auto Login accounts.

- Settings stay on the device and browser profile where you saved them.
- Clearing site data for the page removes them.
- *General → Reset everything* restores the defaults.

## Privacy and safety

- **Moon Client's own code does not send any data anywhere.** It makes no network requests of its own. (The Eaglercraft page itself may load third-party scripts, such as an analytics beacon; that is part of the original page, not Moon Client.)
- **Auto Login stores passwords unencrypted** in your browser's storage. Anyone with access to your browser profile can read them. Only use it on a device you trust, and consider a password you don't reuse elsewhere.
- The Hide Password mask protects against people looking at your screen. It is not encryption.
- **Check server rules.** Some servers restrict visual or movement helpers such as Fullbright, Zoom, or Toggle Sprint. You are responsible for following the rules of the servers you play on.

## How it works

> This section is for the curious and for contributors.

The Eaglercraft HTML file embeds one large base64 data blob (an "EPW" bundle) containing the loader and the xz-compressed game files, including the game's resource archive (`assets.epk`).

**Build step** (done once per release):

1. Decode the bundle and decompress `assets.epk` (an `EAGPKG` v2.0 archive).
2. Replace ten files: the title logo (`minecraft.png`, `minceraft.png`), the edition line (`edition.png`), the splash text (`splashes.txt`), and the six title-screen panorama faces. Each file's CRC32 is recalculated.
3. Recompress with the same xz settings, update the bundle header (sizes and the CRC32 over the bundle), and write it back into the page.
4. Inject the Moon Client overlay script as the **first** script on the page, so its hooks are installed before the game starts.

**Runtime hooks** (installed by the overlay script before the game runs):

| Hook | Used for |
|---|---|
| `console.*`, `error`, `unhandledrejection` | The F9 developer console. |
| `WebSocket` | Detecting which server you joined (Auto Login). |
| `AudioContext` | Mute When Tabbed Out. |
| `requestAnimationFrame` | FPS Limit, Background FPS Limit, and counting the game's real frames. |
| `devicePixelRatio` | Render Scale and Dynamic Resolution. |
| `HTMLCanvasElement.getContext` | GPU preference and latency/antialiasing hints. |
| WebGL texture uploads | Fullbright (forces the 16×16 light texture to white) and spotting the six panorama textures. |
| WebGL draw calls | The Animated Menu Background (draws a custom shader scene in place of the panorama). |
| Keyboard / mouse / pointer lock | Hotkeys, Zoom, CPS, Keystrokes, Hide Password, closing menus. |

The overlay (menu, HUD, console, particles) is plain DOM and canvas drawn on top of the game's canvas. It stays hidden until the game's screen is detected.

## Building from source

**Requirements:** Python 3 with `Pillow` and `numpy`, and the original `eaglercraft-1_20_6.html` file.

Suggested layout:

```
moon-client/
├── README.md
├── src/
│   └── moon_client.js        # the overlay (menu, HUD, hooks, console)
├── build/
│   ├── build.py              # patches assets, rebuilds the bundle, injects the script
│   ├── epk.py                # EAGPKG v2.0 reader/writer
│   └── gen_panorama.py       # generates the six title-screen panorama faces
└── LICENSE
```

1. Generate the panorama faces: `python gen_panorama.py` (writes `panorama_0.png` … `panorama_5.png`).
2. Put the original Eaglercraft HTML where `build.py` expects it. File paths are set at the top of the scripts and may need adjusting for your machine.
3. Run `python build.py`. It writes `MoonClient-1_20_6.html`.

The finished HTML is about 61 MB. Distribute it through **GitHub Releases** instead of committing it to the repository.

## Troubleshooting

**The menu doesn't show up**
- Wait until the game has fully launched. Moon Client stays hidden until then.
- Press **Right Shift** (not Left Shift), or click **☾ Mods** in the top-right corner while the game isn't capturing your mouse.
- Press **F9**, type `MoonClient.open()` and press Enter. Check for red error lines and save the log.

**Fullbright does nothing**
- Open *Visual → Fullbright*. The card says whether the light texture was detected. It's only found once you're in a world.
- If it says *not detected*, try the *Screen gamma boost* mode.

**The title screen still spins or shows the old background**
- Open *Visual → Animated Menu Background*. The card says whether the title screen was detected, or shows an error if the shader failed. Check F9 for details.
- Resource packs that replace the panorama can override the baked-in one.

**Render Scale makes things look wrong or the mouse feels off**
- Turn off *Render Scale* and *Dynamic Resolution*. They rely on the game re-reading the resolution when the window resizes.

**Auto Login doesn't type anything**
- Use **Run now**, close the menu, click into the game, and watch the status next to the button and the F9 console.
- If the log says the chat didn't open, this build isn't accepting simulated key presses. Nothing was typed, and it's safe.

**After closing the menu, my mouse isn't locked**
- Click into the game. Or change *General → Closing menus* to *Only lock the mouse*.

**Overlay (Hide Password, Smooth Hotbar) is misaligned**
- Set *General → GUI scale* to match your video settings.

## FAQ

**Is this a hacked client?**
No. It does not interact with other players, read hidden information, or give combat advantages. Fullbright and Zoom are visual helpers, but see [Privacy and safety](#privacy-and-safety) about server rules.

**Does it work on other Eaglercraft versions?**
The menu, HUD mods, F9 console, Zoom, and most hooks should work on any Eaglercraft page. The title-screen patching and animated background are specific to the 1.20.6 WASM-GC build and would need redoing per build.

**Can other players see my pixel tag or Moon Client features?**
No. Everything is local to your browser.

**Why are some mods greyed out?**
See [Not included (and why)](#not-included-and-why).

**Can I add my own mods?**
Yes. The overlay is one readable JavaScript file with a simple mod registry (`MODS` array). Add an entry with a name, category, and settings, then wire up its behavior.

## Known limitations

- Zoom, Color Grade, and the screen-based Fullbright modes work on the rendered picture, not inside the game, so they can't change field of view or lighting itself.
- Smooth Hotbar and Hide Password align with the game's interface using your GUI scale. A wrong scale makes them misalign.
- Toggle Sprint, Toggle Sneak, and Auto Login work by sending simulated key presses, which not every build accepts.
- Hide Password tracks what you type; it can't see edits made with the cursor keys or from chat history.
- The animated title screen needs this build's title panorama to be recognizable. If it isn't, the normal panorama is shown instead.
- Close Protection and Mute When Tabbed Out depend on browser behavior and may differ between browsers.

## Changelog

**1.6**: Closing the mod menu or F9 console returns you to the game (mouse re-lock, configurable). Particles no longer appear in the game when the title screen can't be detected.

**1.5**: Animated Menu Background: still moonlit ocean with a pulsing moon, clouds, and animated waves.

**1.4**: Optimization tab (Render Scale, Dynamic Resolution, FPS Limit, Background FPS Limit, GPU hints). Menu Particles. New ocean-and-moon panorama. Fixed the overlay not detecting the game screen.

**1.3**: Fullbright rebuilt to override the game's light texture.

**1.2**: Auto Login.

**1.1**: F9 developer console. Overlay stays hidden until the game launches.

**1.0**: Mod menu, HUD mods, Zoom, Hide Password, Custom Player Tag, Moon Client logo and splash text.

## Credits and legal

- **Moon Client** is made by **SmartScal**.
- **Eaglercraft** and **EaglercraftX** are created by lax1dude and contributors. The **1.20.6** port was also done by **o_xer**. Moon Client is an independent add-on and is **not affiliated with or endorsed by** the Eaglercraft developers or porters.
- **Minecraft** is a trademark of Mojang Synergies AB / Microsoft. This project is **not affiliated with or endorsed by Mojang or Microsoft**.
- The released HTML file contains the Eaglercraft client and game assets that belong to their respective authors. Review their licenses and terms before redistributing.
- Moon Client's original code, the generated title-screen images, and the build scripts in this repository are released under **[choose a license, for example MIT, and add a `LICENSE` file]**.

---

*Found a bug or have an idea? Open an [issue](../../issues) and include your F9 log.*

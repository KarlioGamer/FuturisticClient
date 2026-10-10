# FuturisticClient 1.8.9

A Minecraft 1.8.9 client built from scratch on top of the **Minecraft Coder
Pack 919 (MCP 919)**, with **OptiFine 1.8.9 HD_U_M5** pre-merged for a
bigger FPS gain.

## Deliverables

| File | What it is |
|---|---|
| `FuturisticClient 1.8.9.jar` | Final client jar (vanilla + OptiFine + 103 mods + security) |
| `FuturisticClient 1.8.9.json` | Version JSON for your launcher |
| `MODS.md` | Full table of all 103 mods (number, name, category, description) |

After the build, both files are also auto-installed into
`%APPDATA%\.minecraft\versions\FuturisticClient 1.8.9\`.

## How to build

Prerequisites: JDK 8+ (`javac` / `java` on PATH), Python 3, and the full MCP 919
workspace (`mcp919/conf`, `mcp919/jars`, `mcp919/src`).

```
python build_client.py
```

Or just run `build.bat` on Windows.

Options:

- `python build_client.py --skip-compile` — reuse `build/out` and redo only
  reobfuscation → merge → json → installation.

Pipeline stages:

1. Compile 1650+ sources (MCP + client) → `build/out`
2. Generate MCP → notch mappings → `build/reobf.srg`
3. Reobfuscate with SpecialSource → `build/reobf.jar`
4. Merge: vanilla + OptiFine + modified classes + `fc/logo.png` +
   `fc/integrity.dat` (Anti-Tamper sealed) → `FuturisticClient 1.8.9.jar`
5. Write the version JSON and install it into `.minecraft/versions`

## How to play

1. Copy `FuturisticClient 1.8.9.jar` and `FuturisticClient 1.8.9.json` into
   `%APPDATA%\.minecraft\versions\FuturisticClient 1.8.9\`
2. In your launcher, create / select the **FuturisticClient 1.8.9** version
   and start it.

The JSON is deliberately minimal (`id` + `inheritsFrom: 1.8.9` + `mainClass`):
assets, logging, arguments and libs from vanilla are all inherited from 1.8.9,
and the OptiFine + launchwrapper-of are **pre-merged into the jar** — no extra
libraries need to be downloaded, so any launcher that runs the official 1.8.9
(SKLauncher, MultiMC, etc.) opens the client without fuss.

You can also launch directly, without a launcher:

```
java -cp "build/out;$(cat tools/cp.txt);mcp919/jars/versions/1.8.9/1.8.9.jar" net.minecraft.client.main.Main
```

## First-run setup

1. **Animated splash** — black background, logo with a 0.5 s fade-in, a hold of
   ~1 s, the logo rises smoothly and the text fades in; a 3 s animated loading
   bar **blocks the vanilla menu** while loading.
2. **First-user setup** — neon "setup is initializing" and "Loading" text with
   0.5 s fades, then a modern GUI for picking mods before setup finishes.
3. After that, the animated HD main menu (Vector Renderer) takes over.

## Main features

- **103 legitimate utility mods** — full list in `MODS.md` — including
  HitDelayFix, NoHitResetDelay, MouseDelayFix, SnapTap, ProjectL, FPS Boost,
  1.7 Animations, and more. No hacks.
- **30 client settings**, including *Fast World Load* and *NoWorldStartDelay*.
- **Animated HD main menu** with a Vector Renderer.
- **Modern ClickGUI** to toggle mods on/off and tune settings.
- **ALT Manager** offline / cracked (imports the launcher session).
- **Anti-Inject** — blocks internal and external hack injection.
- **Anti-Tamper** — 153 classes sealed with SHA-256 in `fc/integrity.dat`;
  any modification or reverse engineering is detected.
- **OptiFine HD_U_M5 pre-merged** — no runtime tweaker; the game starts with
  `net.minecraft.client.main.Main` directly and the launchwrapper-of
  (Reflector) ships inside the jar.
- **Full branding** — window title `FuturisticClient 1.8.9` and brand
  `futuristic` in F3 / MC|Brand.

## The 103 mods

### 🖥️ Client (6)

| # | Mod | Description |
|---|-----|-------------|
| 1 | UI Sounds | Click and hover sounds on client screens |
| 2 | Streamer Mode | Hides server IP and name from the HUD |
| 3 | Silent Mode | Disables all client notifications (toasts) |
| 4 | Panic Key | Turns every mod off at once (F7) |
| 5 | Reduced Motion | Removes animations from client screens (accessibility) |
| 6 | Open Folder | Opens the game folder with a key (F8) |

### ⚔️ Combat (14)

| # | Mod | Description |
|---|-----|-------------|
| 7 | HitDelayFix | Removes the hit delay |
| 8 | NoHitResetDelay | Removes the hit reset on every hit landed |
| 9 | MouseDelayFix | Removes the mouse movement delay |
| 10 | SnapTap | A/D toggle with no delay even when both keys are held |
| 11 | ProjectL | Fixes head position as in 1.7.10 |
| 12 | Combo Counter | Counts consecutive hits on the same target |
| 13 | CPS Counter | Shows clicks per second |
| 14 | Reach Display | Shows the distance of the last hit |
| 15 | Hit Flash | Highlights the aim on each hit |
| 16 | Hit Sound | Plays a custom sound on each hit |
| 17 | Arrow Counter | Shows how many arrows you have |
| 18 | Potion HUD | Lists active effects with their remaining time |
| 19 | Armor Status | Shows armor durability |
| 20 | Target Info | Shows the name and health of the targeted entity |

### 🏃 Movement (7)

| # | Mod | Description |
|---|-----|-------------|
| 50 | Auto Sprint | Keeps sprinting automatically when walking forward |
| 51 | Toggle Sprint | Keeps sprint active without holding a key |
| 52 | Toggle Sneak | Keeps crouching active without holding a key |
| 53 | Sprint Status | Indicates when sprint is active |
| 54 | Speedometer | Shows your speed in blocks per second |
| 55 | Velocity Display | Shows your movement vector |
| 56 | Jump Counter | Counts jumps in the session |

### 🎨 Render (13)

| # | Mod | Description |
|---|-----|-------------|
| 82 | Smooth Animations | Smooth item transitions in first person |
| 83 | Zoom | Hold C to zoom the camera |
| 84 | Hitmarker | Visual marker when hitting an entity |
| 85 | 1.7 Animations | First-person animations from 1.7 |
| 86 | Custom Crosshair | Custom crosshair with style, color and size |
| 87 | Hit Particles | Emits particles on each hit |
| 88 | Mining Sparks | Sparks while breaking blocks |
| 89 | Health Bar Style | Modern health bar above the hotbar |
| 90 | Hunger Bar Style | Modern hunger bar above the hotbar |
| 91 | XP Bar Style | Modern experience bar |
| 92 | Low Health Alert | Red warning when health is low |
| 93 | Jitter Stabilizer | Reduces camera shake on rapid clicking |
| 94 | Head Ping | Shows a player's ping above their head, next to the name |

### 🧑 Player (9)

| # | Mod | Description |
|---|-----|-------------|
| 70 | Auto Reconnect | Automatically reconnects when the server drops |
| 71 | Quick Disconnect | Key to leave the server instantly |
| 72 | Chat Helper | Sends a quick message with a key |
| 73 | Durability Alert | Warns when an item is breaking |
| 74 | Friend List | Marks your friends |
| 75 | Last Message Repeat | Repeats the last message sent |
| 76 | Death Coord Tracker | Stores your death coordinates |
| 77 | Ping Warning | Warns when your ping goes up |
| 78 | Tool Suggest | Suggests the ideal tool for a block |

### 🌍 World (8)

| # | Mod | Description |
|---|-----|-------------|
| 96 | Weather Info | Shows the weather forecast |
| 97 | Light Grid | Shows the light level around you |
| 98 | Day Counter | Counts world days |
| 99 | Spawn Distance | Distance to the spawn point |
| 100 | Sun Position | Shows the sun and moon progress |
| 101 | World Border | Distance to the world border |
| 102 | Load Times | Measures world load time |
| 103 | World Info | Basic world information |

### 📊 HUD (16)

| # | Mod | Description |
|---|-----|-------------|
| 21 | Watermark | FuturisticClient brand in the top-left corner |
| 22 | Server IP | Numeric IP of the current server |
| 23 | FPS Counter | Dedicated FPS counter on the HUD |
| 24 | Coordinates | Shows x / y / z coordinates |
| 25 | Clock | Local clock on the HUD |
| 26 | Ping Display | Server ping |
| 27 | Server Address | Current server address |
| 28 | Memory Usage | Game memory usage |
| 29 | Session Time | Play time since the session started |
| 30 | Entity Counter | Loaded entities count |
| 31 | Chunk Counter | Chunks in view |
| 32 | World Time | World time of day |
| 33 | Frame Time | Frame time in ms |
| 34 | TPS Estimate | Estimated ticks per second |
| 35 | Module Count | Active modules count |
| 36 | Debug Panel | Compact panel with all information |
| 37 | Advanced Position | Coordinates, region and chunk |
| 38 | Dimension Info | Current dimension |
| 39 | Block Target | Block you are looking at |
| 40 | Item Info | Information about the item in hand |
| 41 | Biome Display | Current biome |

### 💎 Performance (10)

| # | Mod | Description |
|---|-----|-------------|
| 61 | FPS Boost | Built-in FPS engine: fixes memory leaks and eases CPU usage without changing game settings |
| 62 | Memory Cleaner | Automatic garbage collection when memory is high |
| 63 | Adaptive Quality | Reduces client effects when FPS drops |
| 64 | Font Cache Manager | Limits memory used by client fonts |
| 65 | CPU Saver | Reduces client work when the window is in the background |
| 66 | Fast Startup | Preloads menu fonts and texts for a lag-free open |
| 67 | GC Monitor | Shows garbage collections and memory used |
| 68 | FPS Graph | Animated FPS graph of the last seconds |
| 69 | Random Lag | Runs GC only in idle moments, never mid chunk load |
| 79 | Coordinates Copy | Copies your coordinates with a key |

### 📦 Misc (11)

| # | Mod | Description |
|---|-----|-------------|
| 42 | Death Counter | Counts deaths in the current session |
| 43 | Achievement Toast | Unlocked achievement notification |
| 44 | Chat Logger | Saves chat to `futuristic-chat.log` |
| 45 | Quick Reload | Reloads textures and resources with a key (F9) |
| 46 | Moon Phase | Current moon phase |
| 47 | Auto Respawn | Respawns automatically after death |
| 48 | Packet Counter | Packets received and sent per second |
| 49 | InventoryClickDelayFix | Removes inventory click delay and picks up ground items instantly (client-side only, no extra packets) |
| 104 | NoTCPDelay | Reduces network lag (ping), optimizes data sending to the server and avoids drops on weak connections |

### 🎯 Render Extras

| # | Mod | Description |
|---|-----|-------------|
| 84 | Hitmarker | Visual marker when hitting an entity (repeat for visibility) |

### 🧩 Bonus modules (started ON for a fresh install)

| Mod | Description |
|-----|-------------|
| FPS Culling | Frustum culling for entities — fewer rendered entities, more FPS |
| Wave Cape | Animated cape with a wave motion |
| Item Physics | Items and experience orbs use real physics in the world |

> The bonus modules start enabled on a fresh install. `ConfigManager.load()`
> runs right after `build()` and overwrites them with the saved choice, so on
> later boots the user's own toggles are always the single source of truth.

## ClickGUI and hotkeys

Open the **ClickGUI** to toggle mods and adjust settings per module. Default
hotkeys:

| Key | Action |
|-----|--------|
| **F7** | Panic — disables all mods at once |
| **F8** | Open game folder |
| **F9** | Quick reload textures and resources |
| **C** (hold) | Zoom |

Hotkeys are configurable from the ClickGUI when a module exposes them.

## Browser

FuturisticClient ships with an in-game browser (CEF-based) reachable from the
main menu. It can open arbitrary URLs, renders web content as an overlay, and
feeds the current URL and page title back into the client for the Server IP /
server-address HUD entries. The browser module is the layer that keeps web
content visually aligned with the Minecraft HUD and keyboard focus.

## Launchwrapper and anti-cheat

- **Launchwrapper-of (Reflector)** is pre-merged into the jar. The client starts
  with `net.minecraft.client.main.Main` directly; no separate launchwrapper
  download is needed.
- **Anti-Inject** blocks internal and external hack injection.
- **Anti-Tamper** seals 153 classes with SHA-256 in `fc/integrity.dat`. Any
  modification or reverse-engineering attempt is detected. The integrity file is
  generated at build time and sealed into the final jar.

## Settings (30)

The client exposes 30 settings, including:

- **Fast World Load** — reduces startup and chunk-load friction
- **NoWorldStartDelay** — skips the vanilla world-start pause
- **Streamer Mode** — hides server IP and name from the HUD
- **FPS Culling** — entity frustum culling
- Plus the per-module settings exposed by individual mods in the ClickGUI.

The full setting list is owned by `ConfigManager` and the ClickGUI setting
panels.

## Code structure

```
mcp919/src/minecraft/net/futuristic/   # whole client (153 classes)
  api/       Mod, ModManager, categories
  config/    ConfigManager (30 settings)
  gui/       ClickGUI, ALT Manager, setup, components
  hud/       Watermark, mod list, counter, etc.
  render/    Elegant font, animations, vector renderer
  security/  Anti-Inject, Anti-Tamper
  mods/      the 103 mods (Combat/Movement/Render/Hud/World/Player/...)
  browser/   CEF-based in-game browser
mcp919/src/minecraft/net/minecraft/     # 9 patched vanilla classes
tools/cp.txt                            # vanilla lib classpath (31 jars)
tools/of_modified.txt                   # classes modified by OptiFine
build_client.py                         # full build pipeline
```

## Technical notes

- LWJGL 2.9.4-nightly-20150209; natives extracted into `build/natives`.
- Vanilla classes are selected **by notch name** and the full "nest" is embedded
  (avoids `VerifyError` on anonymous classes).
- Vanilla jar signatures are stripped and a new MANIFESTO is written (avoids
  `SecurityException: SHA-256 digest error`).
- `MouseDelayFix` hooks raw input on `MouseHelper.mouseXYChange()`.
- `Server IP` and `FPS Counter` live in `HudExtras` as real widgets:
  `Mod List` no longer exists, and the HUD must not reveal which modules are
  enabled. Slot 93 is now a real widget (current server IP) sized to hold a
  19-character hostname.
- The HUD layout was widened so the IP box (19-char hostname painted over the
  old title-only 74px box) no longer overran its container.

## Support and troubleshooting

- If the client fails to start, confirm JDK 8+ and that `mcp919/conf`,
  `mcp919/jars` and `mcp919/src` are all present.
- If F3 shows a different brand, check the build merged the branding resources.
- If FPS is low, enable **FPS Boost**, **Memory Cleaner**, **FPS Culling** and
  **Adaptive Quality** from the ClickGUI.
- If the browser overlay does not show, confirm CEF natives were extracted
  correctly in `build/natives`.

---

FuturisticClient 1.8.9 — legitimate utility, not hacks.

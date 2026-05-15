# OBS Telestrator

A live telestration (whiteboard drawing) script for OBS Studio on Windows. Draw annotations directly on top of your scene in real time using a projected window.

Each scene can have its own independent telestrator canvas. Pencil settings (color, size, eraser) are shared across all scenes.

> **Windows only** — requires LuaJIT FFI for Windows API input detection.

---

## Requirements

- OBS Studio 28 or later
- Windows 10/11
- The script must be loaded from a folder that also contains `winapi.lua`, `glue.lua`, and the `winapi/` subfolder

---

## Installation

1. Copy the entire `obs-telestrator-lua` folder to a location of your choice (e.g. `C:\obs-plugins\obs-telestrator-lua`).
2. In OBS, open **Tools → Scripts**.
3. Click the **+** button and browse to `Telestration_v1.lua`.
4. The script will load and register a new **Telestrator** source type.

---

## Setup

1. In the Sources panel, click **+** and add a **Telestrator** source.
2. Place it at the **top** of your scene stack so drawings appear above everything else.
3. If the source appears red in the list, that is a known OBS limitation — it functions correctly once the scene is active.
4. If the source does not respond after being added, **toggle its visibility off and on once** to activate it.

---

## Drawing

1. Right-click anywhere in the **OBS Preview** area.
2. Choose **Open Preview Projector**, then select a monitor from the submenu or choose **New window** to open it in a floating window.
3. Click and drag in the projector window to draw.
4. Drawing only works while the projector window is in the foreground.

---

## Hotkeys

Hotkeys are configured in **Settings → Hotkeys** (search for "Telestrat"):

| Action | Description |
|---|---|
| **Cycle Color** | Steps through Yellow → Red → Green → Blue → White → Custom |
| **Cycle Pencil Size** | Steps through even sizes: 2, 4, 6 … up to 12, then wraps |
| **Toggle Eraser** | Switches between drawing and erasing |
| **Clear Canvas** | Wipes the entire drawing canvas |

---

## Script Properties

Open **Tools → Scripts** and select the Telestrator entry to access these settings:

| Setting | Description |
|---|---|
| **Color** | Active drawing color (Yellow, Red, Green, Blue, White, Custom) |
| **Size** | Pencil radius in pixels (1–12) |
| **Custom Color** | Color used when "Custom" is selected |
| **Eraser** | Toggle eraser mode |
| **Preview** | Title fragment for the OBS Preview window |
| **Program** | Title fragment for the OBS Program window |
| **Projector** | Title fragment for the Projector window |
| **Clear Telestrator** | Button to wipe the canvas immediately |
| **Language Presets** | One-click buttons to set the Preview / Program / Projector fields for a supported locale (English, Spanish, French, German, Portuguese BR, Italian) |

---

## Non-English OBS Installations

The script identifies OBS windows by their title bar text. If OBS is set to a language other than English, the window names must be updated to match your locale.

### Quick presets (script properties)

In the script properties panel, scroll to **Language Presets** at the bottom and click the button for your language. The Preview, Program, and Projector fields update immediately and the change persists.

### Manual setup (other languages)

Open a projector and check its title bar — the format is:

```
<Projector fragment> - <Preview or Program fragment>
```

Type the two parts into the **Preview / Program** and **Projector** text fields in the script properties.

| Language | Projector | Preview | Program |
|---|---|---|---|
| English (default) | `Projector` | `Preview` | `Program` |
| Spanish | `Proyector` | `Vista Previa` | `Programa` |
| French | `Projecteur` | `Aperçu` | `Programme` |
| German | `Projektor` | `Vorschau` | `Programm` |
| Portuguese (BR) | `Projetor` | `Pré-Visualização` | `Programa` |
| Italian | `Proiettore` | `Anteprima` | `Programma` |

---

## Troubleshooting

**Source shows in red text in the Sources list**
This is an OBS limitation. Sources registered by scripts are checked at startup before scripts have activated them. The source works correctly at runtime.

**Drawing does not work after adding the source or reloading the script**
Toggle the source visibility off and on. Alternatively, switch to another scene and back, or restart OBS.

**Source appears minimized / tiny when first added**
Right-click the source in the preview and select **Transform → Fit to Screen**.

**Hotkey changes are not reflected in the script properties panel**
OBS does not refresh the script properties UI when hotkeys fire. The active state is correct internally — the panel is just not live-updating.

**Script fails to load (error about winapi or bit)**
Make sure `winapi.lua`, `glue.lua`, and the `winapi/` folder are in the **same directory** as `Telestration_v1.lua`. OBS sets the Lua path relative to the script file location.

---

## Credits

Original script by **mwelsh** ([GitHub](https://github.com/Herschel/obs-whiteboard) · [TILT Forums](http://tiltforums.com/u/mwelsh)) and **Tari**, with contributions by **Paladin**.

`winapi/` and `glue.lua` are by [Cosmin Apreutesei](https://github.com/capr/winapi) — Public Domain.

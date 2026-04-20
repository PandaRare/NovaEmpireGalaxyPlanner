# NOVA — Galaxy Navigation System
### User Guide — `galaxy_mapfinale.html`

---

## Overview

NOVA Galaxy Map is an interactive single-file tool for exploring star systems, managing alliance influence zones, visualizing territorial control, and calculating routes between systems. It runs entirely in the browser with no server required.

---

## Interface Layout

```
┌─────────────────────────────────────────────────────────────────┐
│  HEADER — View mode / Map selector / System counter             │
├──────────────────┬──────────────────────────────────────────────┤
│                  │                                              │
│   SIDEBAR        │            INTERACTIVE MAP                  │
│                  │                                              │
│  • Search        │   (zoomable / pannable canvas)              │
│  • System list   │                                              │
│  • System info   │        [Influence legend]  [Cluster badge]  │
│  • Influence     │                              [+ − ⌖]       │
│  • Pathfinder    │                                              │
└──────────────────┴──────────────────────────────────────────────┘
```

---

## 1. Map Navigation

| Action | Result |
|---|---|
| **Click on a node** | Select the system |
| **Left click + drag** | Pan the map |
| **Right click + drag** | Pan the map (while in placement mode) |
| **Scroll wheel** | Zoom centered on cursor |
| **`+` button** | Zoom in |
| **`−` button** | Zoom out |
| **`⌖` button** | Reset view |
| **Escape** | Deselect / exit placement mode |

System **name labels** appear automatically past a certain zoom level.

---

## 2. View Modes

Two modes are toggled via the **`⬡ Normal` / `⬢ Influence`** buttons in the header.

### Normal Mode
Standard star-map view. Shows star systems, hyperspace lanes, and radial influence circles around buildings. Select any system by clicking directly on it — details appear in the sidebar.

### Influence Mode
A **political territory map** rendered in real time. The entire visible space is rasterized pixel-by-pixel using a weighted Voronoi algorithm:

- Every pixel is assigned to the alliance whose building (within its range) has the strongest claim at that position.
- **Score formula:** `(rank × weight) / distance` — higher rank and closer distance both increase the claim.
- HQ buildings are weighted **×1.8** compared to Outposts.
- Pixels at the boundary between two competing alliances are drawn in **gold** — giving a sharp, continuous frontier line.
- Each building also has a guaranteed **core zone** (radius 4.4 world units) that cannot be overridden by a distant rival.
- Systems with no building within range stay **dark and neutral**.
- A system that physically hosts a building is **locked** to that alliance (shown in white with a thick colored ring) and cannot be claimed by a neighboring alliance's influence.
- **Contested systems** (where a rival's score exceeds 78% of the owner's) show a dashed warning ring.

---

## 3. Maps

Four maps are accessible via the tab buttons in the header:

| Button | Map |
|---|---|
| **Elite** | Elite Galaxy (main map) |
| **Standard A** | Standard Galaxy 135 |
| **Standard B** | Standard Galaxy 136 |
| **Standard C** | Standard Galaxy 137 |

Alliance data (buildings) is stored per-map and switches automatically when you change maps.

---

## 4. System Types

| Symbol | Type | Color | Buildings |
|---|---|---|---|
| ● | Normal system | Cyan blue | ✓ Allowed |
| ● | Black hole | Purple | ✗ Forbidden |
| ◆ | Neutron star | Cyan | ✗ Forbidden |

Black holes and neutron stars **cannot host any buildings** and receive no territorial color in Influence mode.

---

## 5. Influence Panel — Alliance Management

### 5.1 Creating an Alliance
1. Enter a name in the **"Alliance name..."** field (16 characters max)
2. Pick a color from the palette
3. Click **`+ Add`**

### 5.2 Selecting the Active Alliance
- Via the **"Alliance:"** dropdown
- Or by clicking directly on an alliance row in the list

### 5.3 Placing Buildings

Select a placement mode, then **click on a system** on the map:

| Button | Mode | Limit | Notes |
|---|---|---|---|
| **⬡ HQ** | Headquarters | 1 per alliance | Weighs ×1.8 in influence calculations |
| **◈ Outpost** | Outpost | 10 max per alliance | — |
| **✕ Remove** | Remove a building | — | Removes from active alliance only |

> Black holes and neutron stars **cannot host any buildings**.

> A system can only hold **one building** across all alliances.

> A system with a building is **unconditionally owned** by that alliance — no rival can claim it through influence.

### 5.4 Setting Building Rank

Before placing (or after selecting an existing building), adjust the sliders:

| Slider | Effect |
|---|---|
| **HQ Rank** (1–20) | Sets the HQ influence radius and score weight |
| **OP Rank** (1–20) | Sets the Outpost influence radius and score weight |

**Influence radius formula:** `r = 5.5 + (7.5 − 5.5) × (rank − 1) / 19`

This gives a range from **5.5 world units** at rank 1 to **7.5 world units** at rank 20. The displayed `r=` value shows the radius in world units.

**Influence score tables:**

| Rank | HQ base value | Outpost base value |
|---|---|---|
| 1 | 500 | 300 |
| 10 | 950 | 525 |
| 20 | 1500 | 800 |

### 5.5 Deleting an Alliance
Click the **✕** to the right of the alliance name in the list.

---

## 6. Pathfinder — Route Calculator

The Pathfinder computes the **shortest path** between two systems using BFS along existing hyperspace lanes.

### Setting Endpoints

| Action in the system list | Role |
|---|---|
| **Ctrl + click** (Cmd on Mac) | Sets the **FROM** point (green) |
| **Shift + click** | Sets the **TO** point (orange) |

Once both points are set, the route appears automatically as a **yellow dashed line** on the map.

### Reading the Result

- **FROM** — departure system (green circle)
- **TO** — destination system (orange circle)
- **PATH** — number of jumps displayed in the sidebar
- The ordered list of systems along the route is shown below the counters

Click **`Clear path`** to reset.

---

## 7. Export / Import

Alliance data (buildings, ranks, colors, map context) can be saved or shared as JSON.

| Button | Action |
|---|---|
| **↑ Export** | Generates a JSON string — copy it to save or share |
| **↓ Import** | Paste a JSON string to restore a configuration |

> Import replaces the current alliances after a confirmation prompt.

---

## 8. Mobile Version

On screens narrower than 700 px, the sidebar is replaced by a bottom navigation bar with three tabs:

| Tab | Content |
|---|---|
| **Map** | Full-screen map only |
| **Systems** | System list and search |
| **Influence** | Alliance management |

Panels slide up from the bottom as a drawer.

---

## 9. Keyboard Shortcuts

| Key | Action |
|---|---|
| **Escape** | Deselect system / exit placement mode |

---

## 10. Technical Notes

- **Single HTML file** — no server, no dependencies, runs offline.
- All map data (nodes + edges for all 4 galaxies) is embedded as a JSON constant.
- Influence rendering uses a pixel-level **weighted Voronoi rasterizer** on an offscreen canvas scaled by `VOI_RES = 2` (one sample per 2 screen pixels). Increase this value to improve performance on large canvases at the cost of border sharpness.
- Alliance data is **not persisted** between page reloads. Use Export/Import to save your configuration.

---

*NOVA Galaxy Navigation System — `galaxy_mapfinale.html`*

# NOVA — Galaxy Navigation System
### User Guide
 
---
 
## Overview
 
NOVA Galaxy Map is an interactive mapping tool for exploring star systems, managing alliance influence zones, and calculating routes between systems.
 
---
 
## Interface
 
```
┌─────────────────────────────────────────────────────────┐
│  HEADER — Map selection / system counter                │
├──────────────┬──────────────────────────────────────────┤
│              │                                          │
│   SIDEBAR    │           INTERACTIVE MAP               │
│              │                                          │
│  • Search    │   (zoomable / pannable canvas)          │
│  • List      │                                          │
│  • Info      │                  [Legend]  [Badge]      │
│  • Influence │                            [+ − ⌖]     │
│  • Pathfinder│                                          │
└──────────────┴──────────────────────────────────────────┘
```
 
---
 
## 1. Map Navigation
 
| Action | Result |
|---|---|
| **Left click + drag** | Pan the map |
| **Scroll wheel** | Zoom centered on cursor |
| **Right click + drag** | Pan the map (while in placement mode) |
| **`+` button** | Zoom in |
| **`−` button** | Zoom out |
| **`⌖` button** | Reset view |
| **Click on a node** | Select the system |
| **Escape** | Deselect / exit placement mode |
 
System **name labels** appear automatically past a certain zoom level.
 
---
 
## 2. Selecting a Map
 
The header provides 4 maps accessible via the tab buttons:
 
| Button | Map |
|---|---|
| **Elite** | Elite Galaxy (main map) |
| **Standard A** | Standard Galaxy 135 |
| **Standard B** | Standard Galaxy 136 |
| **Standard C** | Standard Galaxy 137 |
 
---
 
## 3. Searching for a System
 
The search field at the top of the sidebar filters the list in real time. Clicking a system in the list:
- **Centers the view** on that system
- Displays its **detailed info** in the bottom panel
---
 
## 4. System Types
 
| Symbol | Type | Color | Buildings |
|---|---|---|---|
| ● blue dot | Normal system | Cyan blue | ✓ Allowed |
| ● purple dot | Black hole | Purple | ✗ Forbidden |
| ◆ cyan diamond | Neutron star | Cyan | ✗ Forbidden |
 
---
 
## 5. Influence Panel — Alliance Management
 
### 5.1 Creating an Alliance
1. Enter a name in the **"Alliance name..."** field (16 characters max)
2. Pick a color from the palette
3. Click **`+ Add`**
### 5.2 Selecting the Active Alliance
- Via the **"Alliance:"** dropdown
- Or by clicking directly on an alliance in the list
### 5.3 Placing Buildings
 
Select a placement mode, then **click on a system** on the map:
 
| Button | Mode | Limit |
|---|---|---|
| **⬡ HQ** | Headquarters | 1 per alliance |
| **◈ Outpost** | Outpost | 10 max per alliance |
| **✕ Remove** | Remove a building | — |
 
> Black holes and neutron stars **cannot host any buildings**.
 
> A system can only hold **one building** across all alliances.
 
### 5.4 Setting Building Rank
 
Before placing a building, adjust the sliders:
- **HQ Rank** (1–20) — sets the HQ influence radius (`r=` shows the radius in world units)
- **OP Rank** (1–20) — sets the outpost influence radius
### 5.5 Deleting an Alliance
Click the **✕** to the right of the alliance name in the list.
 
---
 
## 6. Pathfinder — Calculating a Route
 
The Pathfinder computes the **shortest path** (BFS) between two systems by following existing lane connections.
 
### Setting the Endpoints
 
| Action in the list | Role |
|---|---|
| **Ctrl + click** (or Cmd on Mac) | Sets the **FROM** point (green) |
| **Shift + click** | Sets the **TO** point (orange) |
 
Once both points are set, the route is displayed automatically on the map as a **yellow dashed line**, along with the jump count.
 
### Reading the Result
 
- **FROM** — departure system (green circle)
- **TO** — destination system (orange circle)
- **PATH** — number of jumps (`X jump(s)`)
- The ordered list of systems along the route is shown below
Click **`Clear path`** to reset.
 
---
 
## 7. Export / Import
 
Alliance data (buildings, ranks, colors) can be exported for saving or sharing.
 
| Button | Action |
|---|---|
| **↑ Export** | Generates a JSON string to copy |
| **↓ Import** | Paste a JSON string to restore data |
 
> Import replaces the current alliances after a confirmation prompt.
 
---
 
## 8. Mobile Version
 
On narrow screens (< 700px), the sidebar is replaced by a bottom navigation bar:
 
| Tab | Content |
|---|---|
| **Map** | Map only (full screen) |
| **Systems** | System list and search |
| **Influence** | Alliance management |
 
Panels slide up from the bottom in a drawer.
 
---
 
## 9. Keyboard Shortcuts
 
| Key | Action |
|---|---|
| **Escape** | Deselect system / exit placement mode |
 
---
 

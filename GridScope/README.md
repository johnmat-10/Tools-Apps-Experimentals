# GridScope

**Zero-install, client-side molecular docking grid visualizer & cross-engine parameter translator** built with [3Dmol.js](https://3dmol.csb.pitt.edu/).

Live App: **https://johnmat-10.github.io/Tools-Apps-Experimentals/GridScope/**

---

## Why GridScope?

> *"AutoDockTools draws a cluttered red-green-blue cube on legacy graphics that journals reject, and switching between Vina, AutoDock 4, and Glide requires error-prone manual math. **GridScope** is a zero-install, privacy-first browser tool that lets you visually sanity-check docking boxes, translate parameters across 5 engines/scripts, and export 300/600 DPI colorblind-safe figures."*

---

## Version History

### v1.0 Beta (Initial Prototype)
- **3Dmol.js Grid Cage**: Replaced AutoDockTools' solid RGB cube with a translucent 3D box, 12 cylinder edges, 8 corner spheres, and toggleable RGB axis crosshairs.
- **Structure Loading**: Local `.pdb` / `.pdbqt` receptor upload via `FileReader`.
- **Docking Modes**:
  - **Blind Docking**: Auto-computes protein bounding box + padding.
  - **Site-Specific**: Centers grid on comma-separated residue IDs (`41:A, 145:A`).
  - **Manual**: Direct `Center (X, Y, Z)` and `Size (W, H, D)` inputs with `-`/`+` steppers.
- **Studio Controls**: Cartoon/Stick/Line representations, Spectrum/Chain/Hydrophobicity/Element coloring, Orthographic camera toggle, Solid Black vs. Laboratory White background, and draggable HUD overlay.
- **Exports & Persistence**: AutoDock Vina / GNINA (`.txt`), AutoDock 4 (`.gpf` with even `npts` at `0.375 Å` spacing), basic Glide template, screen-resolution PNG snapshot, and `localStorage` state persistence.

---

### v1.1 (Current Release)
#### Bug Fixes & Performance
- **Cached 3Dmol Models**: Eliminated full PDB re-parsing on slider/coordinate changes by caching `receptorModel` and `ligandModel` and updating only shapes/styles.
- **Valid Schrödinger Glide Export**: Updated `.in` output to standard `GRIDFILE`, `RECEP_FILE`, `GRID_CENTER`, `INNERBOX`, and `OUTERBOX` syntax.
- **Site-Specific Highlighting & Auto-Fit**: Selected residues are highlighted in `stick` style with optional 3D labels and auto-sized bounding box + padding.
- **Stability & Edge Cases**: Clamped HUD dragging inside the viewport, preserved tab inputs on mode switches, fixed `0`/empty-input fallbacks (`safeNum`), and revoked object URLs after downloads.

#### Publication-Grade Visual Fidelity
- **Toggleable Publication Mode**: One-click switch between Studio Mode and Publication Mode (Laboratory White background, Okabe-Ito colorblind-safe palette, Charcoal dashed cage, Orthographic camera, `10 Å` labeled scale bar, RGB crosshairs off).
- **AlphaFold pLDDT Coloring**: Color predicted structures by per-residue confidence (`>90`, `70–90`, `50–70`, `<50`).
- **Box Styles**: Added **Solid Cage**, **Wireframe Only**, **Dashed Edges**, **Dual Inner/Outer** (Glide-style), and **Spherical Pocket** (Discovery Studio-style).
- **High-DPI Snapshot Export**: Native offscreen WebGL resizing for **Single Column (90 mm)** and **Double Column (180 mm)** presets at **300 DPI** or **600 DPI**, with optional **Transparent Background**.
- **Light-Mode HUD**: Adapts `#hud-stats` and PNG composite rendering cleanly for white backgrounds.

#### Docking Workflow Bridges & UX
- **Apo Pocket Finder (`Pocket`)**: Client-side geometric cavity detector that locates and centers on buried binding pockets when no co-crystal ligand is present.
- **Mouse-Adjustable Grid Box + Per-Axis Resizing**: Hold `Shift + Drag` (or toggle **Mouse Box: ON**) to move the grid box in the camera plane; use `Shift + Wheel` or `Right-Drag` with `Resize: All / X / Y / Z` for uniform or single-axis scaling.
- **Docked-Pose Contact Inspector**: Automatically highlights receptor pocket residues within `4.0 Å` of a loaded ligand/pose and draws dashed polar/H-bond contacts (`2.2–3.5 Å`).
- **RCSB Fetch, Sample & Drag-and-Drop**: Fetch any 4-character PDB ID from RCSB, load the `1ATP` sample complex in one click, or drag-and-drop `.pdb`, `.pdbqt`, `.cif`/`.mmcif`, `.sdf`, or `.mol2` files.
- **Ligand Upload, Multi-Pose Viewer & Co-Crystal Auto-Fit**: Auto-detects non-water `HETATM` ligands (`Fit Ligand`), and supports stepping through multi-`MODEL` `.pdbqt`/`.sdf` docked poses with Vina affinity readouts (`kcal/mol`).
- **3D Pick & Molecular Surface**: Click residues directly in the 3D viewport to target them, and toggle a VDW molecular surface with adjustable opacity.
- **Hide Waters (`HOH`) & Ions**: One-click toggle to hide crystallographic waters and common buffer ions.
- **Config Import, Presets & Sanity Warnings**: Import/paste Vina, AD4, or Glide configs; save/switch named multi-box presets; get warnings for `> 30 Å` focused boxes or AD4 `npts > 126`.
- **PyMOL (`.pml`), ChimeraX (`.cxc`) & Methods Export**: Export ready-to-run figure scripts and copy-ready manuscript *Methods* text.
- **Shortcuts (`?`), Collapsible Sidebar (`☰`) & Shareable URLs**: `Ctrl+Z` / `Ctrl+Y` undo/redo, arrow-key box nudging, `?` cheat-sheet modal, and `Share Link` URL state encoding.
- **Design Overhaul**: Precision Cyan / Obsidian Slate palette, isometric cube + node SVG logo, and **Plus Jakarta Sans** + **IBM Plex Mono** typography.

---

## Live 3-Minute Demo Script (Course / Lab / Portfolio)

Open **https://johnmat-10.github.io/Tools-Apps-Experimentals/GridScope/**:
1. **1-Click Complex (`1ATP`)**: Click `1ATP` in **Structure Engine** → demonstrates instant RCSB fetch, `HETATM` ligand detection, pocket contacts, and an auto-fitted grid box.
2. **Interactive Control**: `Shift + Drag` the box in 3D, switch `Resize` to `X`/`Y`/`Z` with `Shift + Wheel`, or toggle **3D Pick** and click a residue to center/highlight it.
3. **Cross-Engine Translation**: Click **Export** and flip through **Vina**, **AD4** (even `npts` at `0.375 Å`), **Glide** (`INNERBOX`/`OUTERBOX`), **PyMOL (`.pml`)**, **ChimeraX (`.cxc`)**, and **Methods** (copy-ready manuscript text).
4. **Publication Payoff**: Click **Publication Mode** (white background, Okabe-Ito colorblind-safe palette, dashed charcoal cage, `10 Å` scale bar) → open **Export Snapshot (DPI)** to show `90 mm @ 300 DPI` transparent PNG export.

### Slide / Poster Tip
Use a **Before vs. After** comparison on your main slide:
- **Left**: Classic AutoDockTools RGB cube screenshot.
- **Right**: GridScope's **Publication Mode** render + a QR code linking to `https://johnmat-10.github.io/Tools-Apps-Experimentals/GridScope/`.

---

*Built with assistance from Gemini in Antigravity.*

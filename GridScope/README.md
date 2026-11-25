# GridScope

**Zero-install, client-side molecular docking grid visualizer & cross-engine parameter translator** built with [3Dmol.js](https://3dmol.csb.pitt.edu/).

Live App: **https://johnmat-10.github.io/Tools-Apps-Experimentals/GridScope/**

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
- **Box Styles**: Added **Solid Cage**, **Wireframe Only**, **Dashed Edges**, **Dual Inner/Outer** (Glide-style), and **Spherical Pocket** (Discovery Studio-style).
- **High-DPI Snapshot Export**: Native offscreen WebGL resizing for **Single Column (90 mm)** and **Double Column (180 mm)** presets at **300 DPI** or **600 DPI**, with optional **Transparent Background**.
- **Light-Mode HUD**: Adapts `#hud-stats` and PNG composite rendering cleanly for white backgrounds.

#### Docking Workflow Bridges & UX
- **Mouse-Adjustable Grid Box**: Hold `Shift + Drag` (or toggle **Mouse Box: ON**) to move the grid box in the camera plane; `Shift + Wheel` or `Right-Drag` (in Mouse Box mode) to resize.
- **RCSB Fetch, Sample & Drag-and-Drop**: Fetch any 4-character PDB ID from RCSB, load the `1ATP` sample complex in one click, or drag-and-drop `.pdb`, `.pdbqt`, `.cif`/`.mmcif`, `.sdf`, or `.mol2` files.
- **Ligand Upload, Multi-Pose Viewer & Co-Crystal Auto-Fit**: Auto-detects non-water `HETATM` ligands (`Fit Ligand`), and supports stepping through multi-`MODEL` `.pdbqt`/`.sdf` docked poses with Vina affinity readouts (`kcal/mol`).
- **3D Pick & Molecular Surface**: Click residues directly in the 3D viewport to target them, and toggle a VDW molecular surface with adjustable opacity.
- **Hide Waters (`HOH`) & Ions**: One-click toggle to hide crystallographic waters and common buffer ions.
- **Config Import, Presets & Sanity Warnings**: Import/paste Vina, AD4, or Glide configs; save/switch named multi-box presets; get warnings for `> 30 Å` focused boxes or AD4 `npts > 126`.
- **PyMOL (`.pml`), ChimeraX (`.cxc`) & Methods Export**: Export ready-to-run figure scripts and copy-ready manuscript *Methods* text.
- **Keyboard Shortcuts & Shareable URLs**: `Ctrl+Z` / `Ctrl+Y` undo/redo, arrow-key box nudging, and `Share Link` URL state encoding.
- **Design Overhaul**: Precision Cyan / Obsidian Slate palette, isometric cube + node SVG logo, and **Plus Jakarta Sans** + **IBM Plex Mono** typography.

# DKST XP Terrain Editor

**English** · [한국어](./README.ko.md) · [한국어 사용자 매뉴얼](./user-guide.ko.md)

DKST XP Terrain Editor is a desktop application for browsing X-Plane Ortho scenery and editing terrain elevations and mesh topology. You can save an edited tile as a full Ortho4XP `.mesh` or apply the edits to an existing scenery DSF. This documentation covers version 0.17.0.

Original `.mesh` and `.cfg` files are optional for an existing Ortho scenery tile: the app can prepare editable terrain from its DSF. Existing `terrain` and `textures` are reused; without CFG, geometry-derived normals use standard strength 1.

The application is now branded **DKST XP Terrain Editor**. Its existing application identifier, settings/cache locations and tile-local `dkst` project files remain compatible.

**[User guide](./user-guide.en.md)**

## Features

| Feature | What you can do |
| --- | --- |
| Scenery browser | Find Ortho tiles in the X-Plane library or open a work folder directly. Inspect the work area or the whole tile in 2D and 3D. |
| 3D viewport | Toggle mesh, imagery, wireframe, and water. Use top, orthographic, or perspective views and exaggerate the displayed elevation with Y-axis Scale. |
| Toolbar and input | Choose icon/text display modes from a toolbar context menu and read functional tooltips. Adjust numeric fields by horizontal dragging or scrolling; switch between Metric and US units. |
| Lighting and upper-scenery preview | Preview time-dependent sunlight, shadows, and supported building LM night textures. Display OBJ/FAC buildings as references with distance and LOD controls, without affecting terrain edits or output. |
| Vertex and face editing | Select vertices, edges, or faces with Brush, Rectangle, Polygon, or Click; switch modes with Z/X/C. Enter elevations, flatten a selection, or drag the Y-axis handle with Soft Selection. Store named selections in the project. |
| Mesh topology | Cut faces, subdivide selected faces, or merge faces into an N-gon. Selected-face subdivision improves coplanar triangulation by default. |
| Normal selection and Bevel | Select connected faces by geometric normal angle and round selected face outlines or individual edges, including concave wall-to-ground corners. Vertex Bevel also rounds pointed peaks and depressions. Supports 100% inward bevels and locally reduced contacts in narrow regions. |
| Selection-sized defaults | Suggest subdivision spacing and bevel width from one tenth of the shorter horizontal selection span. Manual values stay unchanged for the same selection, with Metric/US display. |
| Terrain brushes | Raise or lower terrain, smooth slopes, or paint a mask and apply elevation changes to it. |
| Runway Slope | Edit an actual terrain cross-section along a drawn direction in the selected m/ft units. Use reference images, a soft brush, point alignment, and a knife to refine the profile. |
| External editing | Export OBJ, MTL, and textures. Inspect the edited OBJ and merge it back into the tile, with a repair-copy workflow for supported defects. |
| DSF output and backups | Reuse existing scenery assets, validate the generated DSF, and back up the current file before replacement. |
| Tile projects | Keep edits, recovery data, exports, and build results inside the Ortho tile's `dkst` folder. Reopen the tile folder to resume work. |

## Workspaces

- **Explore** to inspect scenery and define a work area.
- **In-app editing** to edit terrain directly.
- **External editing** to round-trip a mesh through Blender or another 3D editor.

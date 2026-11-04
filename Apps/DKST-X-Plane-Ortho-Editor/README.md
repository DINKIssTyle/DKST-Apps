# DKST X-Plane Ortho Editor

**English** · [한국어](./README.ko.md) · [한국어 사용자 매뉴얼](./user-guide.ko.md)

DKST X-Plane Ortho Editor is a desktop application for browsing X-Plane Ortho scenery and editing terrain elevations and mesh topology. You can save an edited tile as a full Ortho4XP `.mesh` or apply the edits to an existing scenery DSF. This documentation covers version 0.14.0.

**[User guide](./user-guide.en.md)**

## Features

| Feature | What you can do |
| --- | --- |
| Scenery browser | Find Ortho tiles in the X-Plane library or open a work folder directly. Inspect the work area or the whole tile in 2D and 3D. |
| 3D viewport | Toggle mesh, imagery, wireframe, and water. Use top, orthographic, or perspective views and exaggerate the displayed elevation with Y-axis Scale. |
| Vertex and face editing | Select with Brush, Rectangle, Polygon, or Click. Enter elevations, flatten a selection, or drag the Y-axis handle with Soft Selection. Store named selections in the project. |
| Mesh topology | Cut faces, subdivide selected faces, or merge faces into an N-gon. Converting an N-gon to triangles can improve internal diagonals on coplanar terrain. |
| Terrain brushes | Raise or lower terrain, smooth slopes, or paint a mask and apply elevation changes to it. |
| Runway Slope | Edit an actual terrain cross-section along a drawn direction. Use reference images, a soft brush, point alignment, and a knife to refine the profile. |
| External editing | Export OBJ, MTL, and textures. Inspect the edited OBJ and merge it back into the tile, with a repair-copy workflow for supported defects. |
| DSF output and backups | Reuse existing scenery assets, validate the generated DSF, and back up the current file before replacement. |
| Tile projects | Keep edits, recovery data, exports, and build results inside the Ortho tile's `dkst` folder. Reopen the tile folder to resume work. |

## Workspaces

- **Explore** to inspect scenery and define a work area.
- **In-app editing** to edit terrain directly.
- **External editing** to round-trip a mesh through Blender or another 3D editor.


## Download
[https://github.com/DINKIssTyle/DKST-Apps/releases/tag/xporthoeditor](https://github.com/DINKIssTyle/DKST-Apps/releases/tag/xporthoeditor)
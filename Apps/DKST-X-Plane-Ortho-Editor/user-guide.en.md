# DKST X-Plane Ortho Editor User Guide

[Feature overview](./README.md) · [한국어 사용자 매뉴얼](./user-guide.ko.md) · Version 0.14.0

## 1. Start a project

1. To browse installed scenery in **Library**, set the X-Plane installation path in Settings. Add your Ortho4XP source folders if the original meshes live separately from the scenery.
2. To open a standalone tile, switch to **Work folder** and click **Open work folder**. Select the Ortho tile folder. Include its `dkst` directory when moving an existing project.
3. Select a tile in the left panel. Define an area on the map and use **Work area**, or switch to **Whole tile**.
4. Open **In-app editing** and select vertices or faces. Use **Save** to write the mesh and editing state. Use **Build DSF** when you want to apply the result to X-Plane scenery.

A folder containing an Ortho4XP `.mesh` supports terrain editing and mesh output. Imagery and DSF output require the corresponding existing scenery assets.

## 2. View and camera

| Control | Action |
| --- | --- |
| **TOP** | Look straight down to inspect terrain boundaries or runway alignment. |
| **Orthographic / Perspective** | Orthographic view keeps scale consistent with distance. Perspective shows depth through changes in apparent size. |
| **Y-axis Scale** | Exaggerate terrain height in the viewport. Labels, input values, and saved elevations stay in actual metres. Use the reset icon to return to 1×. |
| **Mesh / Texture / Wireframe / Water** | Toggle display layers. Turn off Texture to inspect shading or use Wireframe to see the face connections. |
| **Fit selection** | Frame the selected vertices or faces. Press `H` to use the shortcut. |

Right-drag to rotate the view. Hold `Space` and drag to pan. The mouse wheel zooms around the point under the cursor. Settings let you use the mesh point under the cursor as the rotation pivot or restrict that behavior to the current selection.

## 3. Select and edit elevations

1. Choose **Vertices** or **Faces**. Editing a face elevation moves its shared vertices, so adjoining faces that use those vertices also move.
2. Under **Selection**, choose **Brush**, **Rectangle**, **Polygon**, or **Click**. Use `Shift` to add and `Ctrl/Cmd` to subtract. Use `[` and `]` to change the selection brush size.
3. To finish a polygon, place at least three points and right-click or press `Enter`. You can also click near the starting point when the preview snaps to it.
4. Enter an elevation in the selection card or use **Flatten** to set the selected vertices to their median elevation. **Elevation labels** show elevations at the north, south, east, west, and center of the selection.
5. Enable the **Y-axis move handle** and drag the green arrow to adjust elevation. Hold `Ctrl` for 0.1 m increments or `Shift` for 1 m increments.
6. For a gradual transition, enable **Soft Selection** in the selection card and set its range in metres. The effect falls off with distance from the selection, and the viewport shows the affected area.

Click **Deselect** below the viewport summary to clear the current selection. To reuse a selection, give it a name in the right-hand **Selection Manager** and save it there. Each entry shows whether it contains vertices or faces. You can recall, rename, update, or delete it. Saving the tile includes these selections in the project.

## 4. Edit mesh topology

### Knife

1. Choose **Knife** and click to place cut points. The dashed line and intersection markers preview the next segment.
2. Right-click or press `Enter` to commit an open cut. To close a path, place at least three points and click the starting point when it snaps. Press `Esc` to cancel an unfinished path.
3. Enable **Snap to vertices** to use nearby mesh vertices. Snapping to the path's own starting point is always available.
4. If a segment turns red because it crosses or overlaps an earlier cut segment, move its endpoint. After the cut, vertex mode selects the cut boundary vertices. Face mode removes changed faces from the prior selection while keeping untouched faces selected.

### Subdivide area

1. Open **Subdivide area** and select the faces to refine. A brush, rectangle, or polygon can pick faces. Subdivision follows the existing face boundaries.
2. Set the target vertex spacing in metres and preview the result. Blue shows changed connections. Orange marks triangles with a minimum angle below 15°.
3. Enable **Improve triangulation on coplanar faces** to redistribute internal diagonals on the same plane. Subdivision interpolates elevations on the original surface. When it splits a shared edge, it uses the same new vertex in the adjoining face.
4. Check the expected counts and apply the preview. One Undo reverses the operation. Protected boundaries can limit how closely the result reaches the target spacing.

### N-gons and vertex removal

- Select connected faces and use **Merge selected faces / Create N-gon** to simplify the interior while retaining the outline. Removing interior vertices can change the terrain profile.
- Select individual N-gons or use **Select all N-gons**, then choose **Convert to triangles** when the selection contains only N-gons. Conversion uses existing vertices and can redistribute internal diagonals on coplanar terrain. Use **Subdivide area** afterward if you need a denser mesh.
- In vertex mode, **Delete selected vertices / Reconnect faces** removes selected interior vertices and reconnects the surrounding faces. Work boundaries, shoreline contacts, and other protected connections constrain the operation.

## 5. Terrain brushes

| Tool | Use |
| --- | --- |
| **Height** | Set diameter, hardness, and strength, then drag to adjust elevation. Use the options card to choose the elevation operation and rate. |
| **Smooth terrain** | Blend elevation differences across nearby terrain. Inspect wireframe and shading together when working on steep transitions. |
| **Paint** | Paint or erase a mask before applying an elevation operation. You can paint inside a large triangle even when there are no interior vertices. |

To limit a brush operation, select vertices or faces and enable the selection-only option in the brush panel. Automatic brush subdivision adds control points around a height brush stroke where needed. Press `Esc` during a stroke to cancel the pending change.

## 6. Runway Slope

1. Select the vertices or faces to edit and click **Runway Slope**.
2. Click the start and end on the terrain. Check the arrow, use **Reverse direction** if needed, and click **Open profile**.
3. Read the profile from start to end, left to right. The horizontal axis is distance and the vertical axis is elevation, both in metres.
4. Drag a point or edge vertically, or enter an elevation. Drag across empty space to select multiple points. Use `Shift` to add or `Ctrl/Cmd` to subtract. **Line up** aligns the intermediate selected points to the straight line between the two outermost selected points.
5. Use the **Soft brush** to move the profile vertically with a weighted falloff. Set its radius, hardness, and strength. Use the profile **Knife** to add a split at a chosen distance.
6. Load a **Reference image** and adjust its position, width, height, and opacity. Use two-point calibration to align two image points with known distances and elevations.
7. Review the modified terrain preview and apply the elevation changes. Cancelling before Apply discards the profile edits and cuts.

## 7. Save, package, and build a DSF

**Save** records the editing state and writes a full-tile mesh. **Save as** branches the project into a separate Ortho package. To archive or move the project, copy the entire tile folder with its scenery assets and `dkst` directory.

| Path | Contents |
| --- | --- |
| `dkst/project.json` | Ortho package metadata |
| `dkst/tiles/<coordinate>/source/` | Baseline mesh and baseline DSF when applicable |
| `dkst/tiles/<coordinate>/saved/` and `recovery/` | Saved editing state and automatic recovery data |
| `dkst/tiles/<coordinate>/exports/` and `builds/` | OBJ exports, build results, and reports |
| `dkst/tiles/<coordinate>/backups/dsf/` | Previous DSF versions |

### Apply edits to X-Plane

1. Click **Build DSF** in **In-app editing**. Verify the source Ortho scenery folder. For a mesh-only project, specify the folder containing the tile's existing DSF, `terrain`, `textures`, and Ortho4XP configuration.
2. Follow the progress and console output. The completion screen shows the actual DSF and backup paths. The new DSF uses the normal tile filename under the scenery's `Earth nav data` directory.
3. Reload the scenery in X-Plane and inspect the edited area. The editor's viewport Y-axis Scale has no effect on the DSF elevations.

This workflow updates an existing Ortho DSF. Initial DSF generation from a standalone mesh, imagery downloads, and new coastlines or bathymetry require a separate Ortho4XP workflow.

### Work from a backup

In **DSF backups**, choose the current DSF or a backup and click **Edit selected DSF**. The app uses that version's terrain as the editing baseline. Building from it backs up the current active DSF and writes the edited result to the normal tile filename.

## 8. Edit an OBJ in another application

1. In **External editing**, define the work area and export the OBJ. If you export several tiles, identify the OBJ for the tile you intend to edit.
2. Open the terrain OBJ in Blender or another 3D application. Coordinates are in local metres. X points east, Y points up, and Z points south. Keep the original scale and origin, and preserve the exported `project.json`, MTL, texture, and baseline file paths relative to the project.
3. Edit the terrain OBJ. Preserve the position and elevation of protected outer vertices, water boundaries, and shared edges.
4. Open **Merge Mesh** or **Merge and build DSF** in the editor. Select the exported project folder and the edited `*_terrain.obj`.
5. Use the OBJ inspection option to locate problem faces. For supported defects, create and use a repaired copy. Then run the merge or DSF build.
6. Check the completion status and output paths. If you deleted or moved an exported OBJ in the file manager, check the project file list and select the file you want to use again.

## 9. Keyboard shortcuts

| Key | Action |
| --- | --- |
| `W`·`A`·`S`·`D` or arrow keys | Move the 3D camera up, left, down, or right |
| `,` / `.` | Move backward / forward |
| `Q`·`E` / `R`·`F` | Rotate horizontally / vertically |
| `+` / `−` | Zoom in / out |
| `H` | Fit selection |
| `Ctrl/Cmd+A` | Select all in the current vertex or face mode |
| `Ctrl/Cmd+S` | Save |
| `Ctrl/Cmd+Shift+S` | Save as |
| `Ctrl/Cmd+Z` / `Ctrl/Cmd+Shift+Z` | Undo / Redo |
| `Enter` / `Esc` | Commit the drawn path / cancel the current operation |
| `Delete` | Delete selected vertices and reconnect faces in vertex mode |

## 10. Troubleshooting

| Symptom | What to check |
| --- | --- |
| **Terrain face has zero area** | The build detected a degenerate terrain face. Check the last stage and any coordinates in the console. Inspect that area in Wireframe and compare it before and after the last cut or subdivision. |
| **Preserve protected boundary vertex elevations and positions** | Compare the OBJ patch outline with the original. Use the inspection results to check whether the external editor changed the axes, units, or origin. |
| **New face crosses a source imagery or water boundary** | Inspect the logged coordinates and how the new faces meet the source material or water boundary. The build can split some material crossings and stops if validation fails. |
| **Gaps, overlaps, or T-junctions** | Check that both sides of each shared edge use matching vertices and that faces do not overlap. |
| **Progress stops with an error** | The operation failed. Read the final console error. A successful operation shows a completion status and the actual output path. |
| **X-Plane still shows the old terrain** | Confirm the output DSF path matches the active scenery pack. Check that the pack is enabled and that a higher-priority base mesh is not covering it. |

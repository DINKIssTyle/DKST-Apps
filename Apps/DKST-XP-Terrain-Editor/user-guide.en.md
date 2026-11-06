# DKST XP Terrain Editor User Guide

[Feature overview](./README.md) · [한국어 사용자 매뉴얼](./user-guide.ko.md) · Version 0.17.0

## 1. Start a project

1. To browse installed scenery in **Library**, set the X-Plane installation path in Settings. Add your Ortho4XP source folders if the original meshes live separately from the scenery.
2. To open a standalone tile, switch to **Work folder** and click **Open work folder**. Select the Ortho tile folder. Include its `dkst` directory when moving an existing project.

3. Select a tile in the left panel. Define an area on the map and use **Work area**, or switch to **Whole tile**.
4. Open **In-app editing** and select vertices or faces. Use **Save** to write the mesh and editing state. Use **Build DSF** when you want to apply the result to X-Plane scenery.

An Ortho tile containing an existing DSF, `terrain` and `textures` can be edited without an original `.mesh`. Click **Start in-app editing**, **In-app editing**, or **Edit in external tool**: on first edit, the app extracts the physical terrain from the current DSF and retains `source/base.dsf` and `source/source.mesh` under `dkst/tiles/<coordinate>`. Saved edits resume when the folder is reopened. Existing imagery, materials and water are retained. An Ortho4XP `.cfg` is optional: if present, its `normal_map_strength` is used; if absent, edited normals are calculated from terrain geometry at standard strength **1**. A mesh-only folder still supports terrain editing and mesh output; DSF output needs the existing scenery assets.

The **Work folder list** contains only editing projects with a `dkst` directory. It checks Custom Scenery, registered external scenery packs and grouping folders within the configured X-Plane installation. Listing projects does not read mesh contents or modify scenery files. Disabled scenery packs can still appear as editing projects.

- Sections appear as **Pinned → Recent (up to 5) → All projects**. Use the pin icon to pin/unpin a folder; the current folder has its own pin control at the top.
- The current folder appears at the top and is excluded from all three lists to avoid duplicates. Select its tiles in the top area.
- Search filters folder names, paths and tile coordinates across all three lists. Opening an entry loads that folder's saved work; unsaved edits trigger the existing save confirmation.
- Pins and recent history persist across app restarts. Pinned folders are excluded from Recent to avoid duplicates. **Clear recent** removes history only, leaving pins, folders and editing files intact.
- External work folders are also remembered. They remain in **All projects** after falling out of the last five recent entries or clearing recent history. **Remove from list** removes their pin, recent and external-list records without deleting the folder or editing files.
- A recorded folder or `dkst` location that cannot be found is shown struck through with **Location not found**. Click the row to select the moved work folder and reconnect its pin and history to the new path. Locations without `dkst` are rejected; no files are moved.
- Pin and remove buttons appear on row hover or keyboard focus. Refresh the list or return focus to the app to recheck paths. Standalone mode skips installation discovery while retaining recorded external projects.

## 2. View and camera

| Control | Action |
| --- | --- |
| **TOP** | Look straight down to inspect terrain boundaries or runway alignment. |
| **Orthographic / Perspective** | Orthographic view keeps scale consistent with distance. Perspective shows depth through changes in apparent size. |
| **Y-axis Scale** | Exaggerate terrain height in the viewport. This affects only the view, not actual elevations or saved values. Labels and inputs follow the **Units** setting. Use the reset icon to return to 1×. |
| **Mesh / Texture / Wireframe / Water** | Toggle display layers. Turn off Texture to inspect shading or use Wireframe to see the face connections. |
| **Fit selection** | Frame the selected vertices or faces. Press `H` to use the shortcut. |

Right-drag to rotate the view. Hold `Space` and drag to pan. The mouse wheel zooms around the point under the cursor. Settings let you use the mesh point under the cursor as the rotation pivot or restrict that behavior to the current selection.

### Toolbar appearance

Right-click a toolbar to choose its display mode.

| Menu | Display |
| --- | --- |
| **Icons** | Icons only. Hover a button to read its name and function. |
| **Icons with Text** | Icons and text side by side. This is the default. |
| **Text** | Text only. |
| **Text below Icons** | Smaller text below each icon. |

The setting applies to the scene and editing toolbars and is remembered between sessions. It does not change the top header containing **Explore / In-app editing / External editing**, **Save**, and **Save as**. **Y-axis move handle**, **Elevation labels**, and **Snap to vertices** use toggle buttons rather than checkboxes; a blue background indicates that an option is enabled.

### Button tooltips

Hover a button for about **0.7 seconds** to see its name on the first line and a description of its function below. Relevant keyboard shortcuts are included. After a tooltip appears, moving to another button shows its tooltip immediately. Leaving the buttons for **1 second** restores the initial 0.7-second delay. Keyboard focus shows the description immediately; press `Esc` to dismiss it.

### Units and numeric inputs

Use **Units → Metric / US**, to the right of **Scope**, or press `M` to switch. **Metric** displays and accepts distances and elevations in m and related rates in m/s; **US** uses ft and ft/s. The setting is remembered between sessions. This changes display and input units while terrain coordinates and saved data retain their metre-based values. Exported OBJ coordinates also remain in metres. The `M` shortcut is inactive while typing in an input field.

Numeric fields—including elevation, Soft Selection range, brush diameter, and Y-axis Scale—support typing and native stepper arrows as well as these gestures:

| Gesture | Action |
| --- | --- |
| Left-drag horizontally on a numeric field | Drag left to decrease or right to increase |
| Wheel up / down over a numeric field | Increase / decrease |
| Hold `Ctrl/Cmd` while dragging or scrolling | Adjust at 0.1× the field's increment |
| Hold `Shift` while dragging or scrolling | Adjust at 10× the field's increment |
| Press `Esc` during a numeric drag | Restore the value from before the drag |

Each field respects its minimum and maximum values. In US mode, gestures adjust the displayed feet value. These modifiers are separate from the fixed elevation increments used by the viewport's Y-axis move handle.

### Sun light and overlays

Enable **Display → Sun light** to show the time slider at the bottom centre of the viewport. Adjust the time to inspect sunlight and shadows on terrain and buildings. Supported building LM night textures also respond to the time. Shadow samples compare depth on the actual receiver plane to reduce self-shadow banding. Daytime sky fill and ground bounce improve visibility on shaded and steep terrain while retaining sun direction and shadow contrast. Lighting and time are preview settings and do not change terrain elevations or DSF edits.

Click **Display → Overlays**, immediately to the right of **Sun light**, to open the shared card on the left. Enable **Show upper scenery** to display higher-priority OBJ and FAC buildings as references. Toggle individual packs and adjust **Render distance** and **LOD quality**. Disabled scenery packs are excluded; library-pack assets are used to resolve placed buildings. Type 2 facades may use simplified geometry. The card reports unsupported placements and asset problems. Upper scenery is display-only and is excluded from terrain selection, editing, mesh output, and DSF generation.

Enable **Airport layout** in the Overlays card to read the active airport definitions from the configured X-Plane installation. Runways (including water runways and helipads) are shown in gold/blue, taxiway and apron pavement in cyan, and airport boundaries as dashed green outlines. **Color fill**, **Outlines** and **Opacity** control the display. Pavement curves and interior holes are preserved; names and source-file paths identify the displayed airports. Disabled packs are ignored, and higher-priority airport definitions replace lower-priority definitions as a whole.

Airport layouts are draped onto the current terrain and follow height edits. Airport elevation and flattening settings never modify the mesh. The initial implementation shows reference geometry rather than X-Plane pavement textures, markings, lights or buildings. It requires a configured X-Plane installation with standalone mode disabled. No matching layout or missing installation produces a message in the card. The overlay remains visible when the card is closed; this is a temporary viewport setting.

In the same card, enable **OSM map** to drape OpenStreetMap over the loaded terrain. Adjust **Opacity** to compare it with imagery. Internet access is needed for uncached tiles. Resolution adapts to the work area, with at most 16 requested tiles; selecting a smaller work area gives more detail. Attribution stays visible while the map is displayed, including when the card is closed.

Use **Open GeoTIFF** to load a local `.tif`/`.tiff` with EPSG:4326/WGS84 geographic coordinates and affine georeferencing. The image is positioned automatically on the terrain; north-up and rotated affine rasters, PixelIsArea/PixelIsPoint, RGB and single-band grayscale images are supported. A single band is stretched over its valid range; NoData pixels are transparent. Only the overlapping read window is decoded, using internal overviews when available. Other coordinate systems require reprojection before opening. Files without coordinates, without overlap, or with an oversized read window produce a message in the card. Show/hide, replace/remove the image and adjust opacity independently from OSM. The file is read locally and is not uploaded.

OSM and GeoTIFF are display-only reference layers. They follow terrain height edits but never enter terrain picking, saved mesh geometry, or DSF output. Closing the card leaves enabled layers visible. These raster selections are temporary viewport settings; reopening the app requires opening the GeoTIFF again.

## 3. Select and edit elevations

1. Choose **Vertices (Z)**, **Edges (X)**, or **Faces (C)**. Editing a face elevation moves its shared vertices, so adjoining faces that use those vertices also move.
2. Under **Selection**, choose **Brush**, **Rectangle**, **Polygon**, or **Click**. Use `Shift` to add and `Ctrl/Cmd` to subtract. Use `[` and `]` to change the selection brush size.
3. To finish a polygon, place at least three points and right-click or press `Enter`. You can also click near the starting point when the preview snaps to it.
4. Enter an elevation in the selection card or use **Flatten** to set the selected vertices to their median elevation. **Elevation labels** show elevations at the north, south, east, west, and center of the selection.
5. Enable the **Y-axis move handle** and drag the green arrow to adjust elevation. Hold `Ctrl` for 0.1 m increments or `Shift` for 1 m increments.
6. For a gradual transition, enable **Soft Selection** in the selection card and set its range in the displayed units. The effect falls off with distance from the selection, and the viewport shows the affected area.

The selection shape remembers its last-used value and defaults to **Brush** when no preference has been saved. Vertex, edge, and face selection always includes occluded components.

Click **Deselect** below the viewport summary to clear the current selection. To reuse a selection, give it a name in the right-hand **Selection Manager** and save it there. Each entry shows whether it contains vertices, edges, or faces. You can recall, rename, update, or delete it. Saving the tile includes these selections in the project.

### Edge and connected-chain selection

In **Edges (X)** mode, Click selects the edge closest to the cursor. Brush, Rectangle, and Polygon are also available; Shift adds and Ctrl/Cmd subtracts. Selected edges appear orange. Internal render-triangulation diagonals of N-gons are excluded.

Set **Connection angle** in the edge card and click **Select connected edges** to extend the selection along the closest continuation at each endpoint. Angles use actual 3D directions; lower thresholds follow straighter chains. The last connection angle is remembered. Edge selections can be stored, recalled, renamed, updated, and deleted in Selection Manager. Cuts and subdivisions can invalidate saved edges, which are then reported as missing.

Elevation editing, Flatten, and the Y-axis handle affect the shared endpoints of selected edges, moving adjoining faces too. Selection limits in Height, Smooth, and Paint use the selected edge vertices.

## 4. Edit mesh topology

Converting an N-gon to triangles optimizes internal diagonals in plan view while keeping all boundary/interior point coordinates and elevations. Varying vertex heights do not prevent conversion. Changed diagonals can change interpolated terrain heights and shading between vertices; Undo restores the previous connectivity.

Saved Mesh output automatically removes vertices that no face references. Editing keeps stable vertex IDs for undo and stored selections, while unreferenced vertices and vertices belonging only to faces that emitted no preview surface are excluded from selection handles. Points actually referenced by an N-gon's triangle cache are not unused vertices and are not deleted automatically.

### Knife

Cuts create **N-gons** by default, allowing faces to span existing internal triangle edges while retaining the drawn knife edges and material boundaries. Actual terrain heights and the triangle cache used for DSF output are preserved. Enable **Cut into triangles** next to **Snap to vertices** to keep the result as individual triangles. Both options remember their last state across application restarts.

1. Choose **Knife** and click to place cut points. The dashed line and intersection markers preview the next segment.
2. Right-click or press `Enter` to commit an open cut. To close a path, place at least three points and click the starting point when it snaps. Press `Esc` to cancel an unfinished path.
3. Enable **Snap to vertices** to use nearby mesh vertices. Snapping to the path's own starting point is always available.
4. If a segment turns red because it crosses or overlaps an earlier cut segment, move its endpoint. After the cut, vertex mode selects the cut boundary vertices. Face mode removes changed faces from the prior selection while keeping untouched faces selected.

### Subdivide area

1. Open **Subdivide area** and select the faces to refine. A brush, rectangle, or polygon can pick faces. Subdivision follows the existing face boundaries.
2. Set the target vertex spacing in the displayed units and preview the result. Blue shows changed connections. Orange marks triangles with a minimum angle below 15°.
3. **Improve triangulation on coplanar faces** is enabled by default, matching the connectivity optimization used by Bevel and automatic brush refinement. It redistributes internal diagonals on the same plane. Subdivision interpolates elevations on the original surface. When it splits a shared edge, it uses the same new vertex in the adjoining face.
4. Check the expected counts and apply the preview. After applying, the new faces covering the original selection remain selected. Neighbouring faces split only to maintain shared-edge connections are excluded. One Undo reverses the operation. Protected boundaries can limit how closely the result reaches the target spacing.

Bevel, automatic brush refinement, and selected-face subdivision share the same basic refinement process. Selected-face subdivision interpolates the original surface; Bevel subsequently changes elevations in the transition strip to form a curve. You can disable **Improve triangulation on coplanar faces** when needed.

Selected-face subdivision supports up to **65,536 new vertices** per operation. If the limit is exceeded, increase vertex spacing or split the face selection. Interactive brush refinement retains a separate limit of **8,192 new vertices** per stroke. A preview is invalidated when the selection, work area, spacing, or triangulation option changes; camera and display changes do not clear it.

### Defaults from selection size

Initial **subdivision vertex spacing** and **Bevel width** use **one tenth of the shorter horizontal span** of a new vertex/face selection. They use actual terrain dimensions; elevation differences, camera zoom, and Y-axis Scale do not affect the estimate.

| Selection dimensions | Subdivision spacing | Bevel width |
| --- | --- | --- |
| 10 × 20 m | 1 m | 1 m |
| 600 × 1,000 m | 60 m | 60 m |
| 30,000 × 50,000 m | 3,000 m | 1,000 m — bevel maximum |

- A **new selection** recalculates both defaults. Reopening a tool or card with the same selection retains manually entered values.
- Estimates round to 0.1 m in terrain units. **US** displays the equivalent feet value without changing the physical distance.
- Subdivision spacing is limited to 0.1–100,000 m. The automatic bevel width starts within 0.4–1,000 m and is raised, if needed, to at least the current segment count × 0.1 m.
- These are starting estimates. Adjust them for the required detail and inspect the preview's added vertex/triangle counts. Generation limits and protected-boundary checks still apply.

### Normal Break Selection

In **Faces → Selection**, choose **Normal Break Selection** immediately after **Click**. The **Normal Angle** slider replaces Brush size. Hover over a face to preview the connected region, then click to select it. Shift adds; Ctrl/Cmd subtracts.

Selection crosses a shared edge when the angle between the adjacent geometric face normals is within the threshold. Lower values stop at sharper edges; higher values expand the region. Changing the angle after clicking recalculates from the same seed face. N-gons remain atomic selection units. Calculations use actual terrain dimensions, independent of **Y-axis Scale** and shading normals. The last angle is remembered across restarts. Protected faces and faces outside the work area are excluded.

### Bevel

Select faces and open **Bevel** below **Flatten** in the selection card. This terrain operation rounds a finite transition strip around the selected outline. Vertex elevations inside that strip change; parts of the top and surrounding terrain outside the strip retain their elevations.

| Setting | Meaning |
| --- | --- |
| Bevel width | Nominal transition width, entered in the active m/ft units. |
| Inside | Percentage directed inside the selection. At 100%, a contact on the adjacent slope is still retained so the raised corner can be cut back. |
| Roundness | 0% connects endpoints linearly; 100% uses a sectional curve with the original corner as its control point. |
| Segments | Sets target vertex spacing by dividing the width. Higher values create a denser transition mesh. |

To round the top edge of raised terrain:

1. Select its top faces in **Faces** mode. **Normal Break Selection** can help separate them from the side slopes.
2. Open **Bevel** and review the width suggested from the selection size. Start with **Inside 100%** for an inward cutback.
3. Preview with **Roundness 100%** and the default **Segments 1**. Increase the segment count when you need a denser curved surface. Even at 100% inside, the calculation retains contact with the adjacent slope to round the top corner.
4. Contacts shrink locally in narrow or concave regions, so the actual transition width there can be smaller than the nominal input.

Choose **Preview bevel** to inspect blue faces/wireframe and the original orange outline. Review changed/added vertex counts, then choose **Apply bevel**. Changing the selection or settings requires a new preview. Apply stays unavailable when no slope change produces a modified vertex.

Results that affect water/material seams, open boundaries, protected vertices, or the work-area boundary are rejected. Contact widths are reduced locally where a narrow or concave region limits the available surface. Shared terrain vertices are retained; this is a terrain transition operation rather than a general solid-model bevel. Apply is one undo step. Topology changes reset the existing paint state. Saving and DSF output include the result.

### Edge Bevel — wall-to-ground corners

Use **Edges (X)** to round specific edges rather than the entire outline of selected faces.

1. Enable **Wireframe** and select the edges where a wall meets the ground. Extend a chain with **Select connected edges** if needed.
2. Open **Bevel** below **Flatten** in the selection card, review the suggested width, and choose **Preview bevel**.
3. In edge mode, **Flatter side (%)** allocates the width toward the less steep of the two adjoining faces. Start at 50% and adjust the balance. Face mode retains **Inside (%)**.
4. Adjust **Roundness** and **Segments** and inspect the blue transition strip and original orange edges. Convex corners are cut back; concave ground corners are filled between the adjoining surfaces.
5. Apply the preview. Subdivided edges along the original selected chains remain selected. One Undo reverses the operation.

The effect tapers at open chain ends to meet the surrounding terrain. Water/material seams, open mesh boundaries, protected vertices, and work-area boundaries remain protected. Mesh saves and DSF builds include the result.

### Vertex Bevel — rounded peaks and depressions

Use **Vertices (Z)** to round a pointed pyramid or a sharp depression.

1. Select the apex vertex, then open **Bevel** below **Flatten** in its selection card. Up to 64 vertices can be processed together.
2. Set **Bevel radius** in the active m/ft units, **Roundness**, and **Segments**. Vertex mode does not use the Inside/Flatter side setting.
3. Choose **Preview bevel**. The operation adds conforming geometry around the point and forms a curved cap: the center becomes flatter while the outside contact follows the original slope. The peak can become lower, and a depression can become shallower.
4. The radius can span multiple neighboring faces, independently of existing vertex spacing. Protected terrain/material boundaries, the work area, and other selected caps limit it. The cap uses the actual outside slope at its contact to avoid a new shoulder crease.
5. Apply the preview. The original vertices stay selected. One Undo reverses both refinement and elevation changes; saves and DSF builds include the result.

Turning junctions in face/edge Bevel blend the adjoining sections into a shared corner patch. Vertex caps also use a two-dimensional corner patch instead of retaining angular fan ridges. These are geometry changes and do not depend on UV preservation.

Existing vertex XY positions and elevations outside each cap stay unchanged. Adjacent selected caps are kept separate. Flat regions do not change. Open boundaries and water/material seams are protected. Refinement shares the existing Bevel/brush process; the segment count controls target spacing, with a 0.1 m minimum.

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
3. Read the profile from start to end, left to right. The horizontal axis is distance and the vertical axis is elevation, both shown in m or ft according to **Units**.
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

### Backup retention

Set **Preferences → Maximum backups** to a value from 1 to 1,000. The default is **5**. The limit applies separately to Mesh-save and DSF backups for each tile, retaining the newest versions. Changing the setting does not immediately delete files; older backups are removed after the next successful save or DSF build. Active working files, immutable source baselines, automatic recovery data, and separately named manual copies are excluded. If cleanup fails, the saved result is retained and the completion dialog shows a warning.

### Apply edits to X-Plane

1. Click **Build DSF** in **In-app editing**. Verify the source Ortho scenery folder. For a mesh-only project, specify the folder containing the tile's existing DSF, `terrain`, and `textures`.
2. Follow the status and progress. Expand **Build console** to view detailed logs; it opens automatically on an error. Completion shows a success status and the actual DSF and backup paths. Longer instructions are under **Build information**, and footer buttons remain visible while the body scrolls. The new DSF uses the normal tile filename under the scenery's `Earth nav data` directory.
3. Reload the scenery in X-Plane and inspect the edited area. The editor's viewport Y-axis Scale has no effect on the DSF elevations.

N-gon triangulation avoids thin ears formed from nearly collinear boundary points while retaining boundary vertices and elevations. If previously converted triangles collapse onto a line during transfer to DSF coordinates, the build can reconnect their internal diagonal with a neighboring face of the same material. No faces are discarded and final topology validation remains required.

During a DSF build, coordinate precision is increased automatically if quantization would invert or collapse a narrow face. Extremely narrow overlaps introduced by editing or coordinate transfer can be repaired by reconnecting an internal diagonal within the same material. Vertex positions, elevations, and outer boundaries are retained, and the console reports automatic precision and repair stages. Reconnection does not cross material or water boundaries. The final DSF must pass shared-edge, duplicate-face, and gap validation before it is saved.

This workflow updates an existing Ortho DSF. Initial DSF generation from a standalone mesh, imagery downloads, and new coastlines or bathymetry require a separate Ortho4XP workflow.

### Build error locations and reports

Knife, subdivision, Bevel, and other topology changes share a cumulative limit of 50 records. When the limit message appears, use **Build DSF** to apply the edits, then select the **Current** DSF under **DSF backups** on the right and click **Edit selected DSF** to continue from the new baseline. Saving or restarting alone does not reset the count. The previous workspace is retained in `dkst/archive`.

When a DSF build fails, **Go to problem** and **Generate report** appear below the error. Go to problem focuses the camera without shrinking the current work area. If needed, it expands the area to include the existing scope and a 250m margin around the problem, so neighboring faces remain editable. Whole-tile mode is retained. The location button is disabled for file or configuration errors without a reliable geometry location.

Reports are ZIP files in `dkst/tiles/<coordinate>/reports/` inside the current Ortho folder. They contain the error stage, coordinates, area and vertex details, build logs, edit metadata, and nearby original, edited and DSF compiler-input mesh excerpts (JSON and OBJ). Excerpts cover a 100m margin and at most 4,096 faces per snapshot; JSON marks truncated excerpts. Complete scenery and textures are excluded. Data is frozen at failure time, so later edits do not change the evidence. Send the ZIP to the developer yourself; it is not uploaded automatically. Logs and editing metadata may contain local paths.

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

Mode and camera shortcuts are inactive while typing in numeric/text fields or using a modal. Hold `1`, `2`, or `3` to temporarily navigate with the left mouse button without editing terrain. Releasing the key ends that camera gesture.

| Key | Action |
| --- | --- |
| `W`·`A`·`S`·`D` or arrow keys | Move the 3D camera up, left, down, or right |
| `,` / `.` | Move backward / forward |
| `Q`·`E` / `R`·`F` | Rotate horizontally / vertically |
| `+` / `−` | Zoom in / out |
| `H` | Fit selection |
| `Z` / `X` / `C` | Switch to Vertices / Edges / Faces mode |
| `F1` | Toggle Top view / previous camera position, orientation, projection and zoom |
| Hold `1` + left drag | Pan |
| Hold `2` + left drag | Zoom: right/up to zoom in, left/down to zoom out |
| Hold `3` + left drag | Rotate the view |
| `M` | Switch Metric / US units |
| `Ctrl/Cmd+A` | Select all in the current vertex, edge, or face mode |
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
| **Dense stripes appear when Sun light is enabled** | This can indicate self-shadow depth-comparison artifacts. Disable Texture and Wireframe and compare Sun light on/off. If the issue persists, include both views, the sun time, and Y-axis Scale in your report. |
| **Spacing or width changes after changing the selection** | A new selection recalculates defaults from its horizontal size. Manual input remains unchanged for the same selection. Check for unintentionally selected distant faces if a suggested value looks unexpected. |
| **Apply bevel is unavailable** | Preview the current selection/settings and check the changed vertex count. Terrain without a slope change may produce no changes. Changing the selection or settings requires another preview. |
| **Progress stops with an error** | The operation failed. Read the final console error. A successful operation shows a completion status and the actual output path. |
| **X-Plane still shows the old terrain** | Confirm the output DSF path matches the active scenery pack. Check that the pack is enabled and that a higher-priority base mesh is not covering it. |

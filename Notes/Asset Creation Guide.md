# ProtoKit — Per-Asset Checklist (Blender → Godot → Library)

## 1) Blender: Author the asset

- [ ]  **Units check**: 1 BU = 1 m (Scene → Units → Metric, Unit Scale 1.0).
- [ ]  **Model + scale** to real size (Item panel → Dimensions).    
- [ ]  **Apply transforms** (`Ctrl+A` → All Transforms). Target: Scale 1, Rot 0.    
- [ ]  **Set origin** (bottom/hinge/rotation center):    
    - [ ] Edit Mode → select reference face/vertex → `Shift+S` → Cursor to Selected → Object Mode → Object → Set Origin → Origin to 3D Cursor.        
- [ ]  **Name cleanly** (Collection, Object, Mesh): `prop_<category>_<size>[_variant]` (e.g., `prop_cube_1m_a`).    (Add "-col" if you want it to have the same collision)
- [ ]  **Shade**: Flat (for hard placeholders).    
- [ ]  **UV unwrap**:    
    - [ ] Simple boxes → **Cube Projection**.        
    - [ ] Other hard-surface → **Smart UV Project** (Island Margin ≈ 0.02).        
    - [ ] Keep **uniform texel density** (Kenney grid looks same size across assets).      
- [ ]  **(Optional)** temp material for preview (assign Kenney grid just to eyeball UVs).
    

## 2) Blender → Export (glTF **separate**)

- [ ]  File → Export → **glTF 2.0 (.gltf)**.    
- [ ]  **Include**: _Selected Objects_ only.    
- [ ]  **Do not** enable Draco/mesh compression in Blender.    
- [ ]  **Geometry**: Apply Modifiers ON, UVs ON, Normals ON, Tangents ON.    
- [ ]  **Materials/Textures**: Export Materials ON; **don’t embed** textures.    
- [ ]  **Axis**: default (glTF/Godot are Y-up; no axis hacks).    
- [ ]  **Path**: export into your project:    
    - [ ] `res://libraries/protokit/models/<category>/<asset_name>.gltf`        
    - [ ] Place Kenney PNG in `res://libraries/protokit/textures/placeholder_kenney.png`
        
## 3) Godot: Import settings (once per project; reimport if needed)
- [ ]  In **FileSystem**, select the new `.gltf` → **Import** dock:    
    - [ ]  **Meshes**: **Generate LODs = ON**, **Ensure Tangents = ON**.        
    - [ ]  Materials: leave default import, we’ll **override** with a shared one.        
- [ ]  **Reimport**.
    

## 4) Godot: Shared placeholder material (one-time, reused)
- [ ]  Create **StandardMaterial3D** at:    
    - [ ] `res://libraries/protokit/materials/placeholder_grid.tres`        
- [ ]  Set **Albedo Texture** = `res://libraries/protokit/textures/placeholder_kenney.png`.    
- [ ]  (Optional) Uncheck **Specular/Metallic** if you want a flat look while blocking out.    

## 5) Godot: Make a game-ready prefab (PackedScene)
- [ ]  New Scene → **Node3D** root named exactly like the asset (e.g., `prop_cube_1m`).    
- [ ]  **Instance** the imported model (`MeshInstance3D`) under the root.    
- [ ]  **Material override** on MeshInstance3D = `placeholder_grid.tres`.    
- [ ]  **Collision**:
    - [ ] Static architecture → **StaticBody3D** + **CollisionShape3D (Box/Convex)** _or_ Mesh → **Create Trimesh Static Body** (coarse).        
    - [ ] Dynamic/pushable props → **RigidBody3D** + **Convex** or simple primitive shapes.
- [ ]  **Snap test**: with grid snap ON, asset sits on Y=0 (origin correct).    
- [ ]  Save to:    
    - [ ] `res://libraries/protokit/scenes/<category>/<asset_name>.tscn`
        

## 6) (Optional) Add to MeshLibrary for GridMap painting
- [ ]  Create or open: `res://libraries/protokit/gridmap/protokit_meshlib.tres`.    
- [ ]  Add a new **item**; assign the imported **Mesh**.    
- [ ]  Assign **Shapes** (Convex/Box) for collision (keep it simple).    
- [ ]  (Optional) Add **Occluder**/**Navigation** shapes if you maintain tile-based nav/occlusion.    
- [ ]  Test: Add a **GridMap** node in a test scene, set MeshLibrary, paint the tile.    

## 7) Sanity checks (quick)
- [ ]  Drop the **.tscn** into a test level.    
- [ ]  Size matches a 1×1×1 BoxMesh reference.    
- [ ]  Grid-snap placement is clean; pivot behavior correct.    
- [ ]  Collision behaves (walk on it, bump into it, or push it if dynamic).    
- [ ]  Material shows the Kenney grid with the **same pad size** as your other assets.
    

## 8) Commit to ProtoKit
- [ ]  Add/commit files under `libraries/protokit/…`    
- [ ]  Update `libraries/protokit/README.md` if you added a new category or notes.    
- [ ]  (If reused cross-project) push to the ProtoKit repo/submodule.
    

---

## Minimal per-asset fast-path (muscle memory)
- [ ]  Blender: scale → `Ctrl+A` → origin → UV (Cube/Smart) → export glTF (separate).    
- [ ]  Godot: reimport with LODs+Tangents → prefab `.tscn` with material override + collision.    
- [ ]  (Optional) add to MeshLibrary → sanity test → commit.    

---

## Notes / comments

- **Why glTF (separate)**: one shared texture/material across the whole kit, tiny reimports, easy global swaps.    
- **Collision discipline**: primitives/convex for anything that moves, coarse trimesh only for big static shells.    
- **Keep scenes clean**: never edit imported meshes directly; always wrap in your own `.tscn` prefab.    
- **Consistent naming** keeps your GridMap and search sane: `prop_`, `arch_`, `kit_`, etc.  
- **Reusing ProtoKit in a new project**: copy or add as a git submodule under `res://libraries/protokit/`, set import flags once, and you’re ready to drag prefabs or paint GridMaps.



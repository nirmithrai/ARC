# 0. Notes
Doing it in [[Blockbench]] now. 
For BlockBench
- name your meshes
- get the pivot point right
- .gltf
- 

For godot
1. maintain a source glb folder
2. create New Inherited Scene from that glb
3. Now you can treat this as usual Godot scene. Add collisions, scripts, VFX, etc to it
4. Save that scene.
5. In projects, we will use this scene as asset. 
6. if there's an update to the glb, just overwrite in the source folder, it should update its inherited scenes as well. 

-col on model will add collision to it
-colonly for only collision without the mesh
# 📦 1. Environment Building Blocks
****

## Cubes / Boxes (base = 1×1×1 unit)
- [x] Box 1×1×1 (basic cube)
- [x] Box 2×1×1 (rectangular brick)
- [x] Box 2×2×1 (flat tile)
- [x] Box 4×4×1 (big platform tile)
- [x] Box 4×1×1 (wall segment)
- [x] Box 4×4×4 (big block)
- [x] Box 1x2x1 (column)
## Walls
- [x] Thin wall: 2x2x0.5
- [x] Thick wall: 2x2x1
- [x] Tall thin wall: 4x4x0.5
## Floors / Platforms
- [x] Flat tile: 1×0.25x1
- [x] Large flat: 4×0.25x4
- [x] Ramp: 4×2×0.25 angled at 30°
- [x] Stairs (blocky): 2×2×2 subdivided
## Doorways / Arches
- [x] Door frame: 2×0.25×3
- [x] Arch: 2×0.25×3 with curve cutout

# 🪑 2. Props
- [ ] Crate: 1×1×1
- [ ] Barrel: Cylinder Ø1 × 1.5
- [ ] Column: Cylinder Ø0.5 × 3
- [ ] Rock: 1×1×1 blobby mesh
- [ ] Table: 2×1×1 with 4 cylinder legs
- [ ] Chair: 1×1×1.5 (blocky L-shape)
- [ ] Collectible sphere: Ø0.5
- [ ] Collectible diamond: Cube 0.5×0.5×0.5 rotated 45°
- [ ] Health pack: Cube 0.5×0.5×0.5 with cross extrude
- [ ] Ammo box: 1×0.5×0.5
- [ ] Key: Flat cross shape 0.25×0.25×1

# 🧍 3. Characters / NPCs

- [ ] Player dummy: Capsule Ø0.5 × 2
- [ ] Enemy small: Sphere Ø1
- [ ] Enemy medium: Capsule Ø1 × 2
- [ ] Enemy large: Cube 2×2×2
(optional: rig a capsule with stick limbs for animation tests)

# ⚔️ 4. Items / Weapons
- [ ] Sword placeholder: Cube 0.1×0.1×1 + small cross-guard
- [ ] Gun placeholder: L-shape block 1×0.25×0.5
- [ ] shield 
- [ ] 

# Vehicles
- [ ] Car placeholder: Box 2×1×0.5 with 4 cylinders for wheels
- [ ] Plane placeholder: Box fuselage 2×0.5×0.5 with flat wing planes
- [ ] boat
- [ ] 

# 🚩 5. Markers / UI
- [ ] Arrow: Cone Ø0.5 × 1 + small cylinder base
- [ ] Cone marker: Ø1 × 2
- [ ] Checkpoint pillar: Cylinder Ø0.25 × 2
- [ ] Flag: Cylinder pole Ø0.1 × 3 with flat plane flag

# old
[[Asset Creation Guide]] 
get textures from https://www.kenney.nl/assets/prototype-textures
# 0. Notes
get textures from https://www.kenney.nl/assets/prototype-textures
[[Asset Creation Guide]]

# 📦 1. Environment Building Blocks

## Cubes / Boxes (base = 1×1×1 unit)
- [ ] Box 1×1×1 (basic cube)
- [ ] Box 2×1×1 (rectangular brick)
- [ ] Box 2×2×1 (flat tile)
- [ ] Box 4×4×1 (big platform tile)
- [ ] Box 4×1×1 (wall segment)
- [ ] Box 4×4×4 (big block)
## Walls
- [ ] Thin wall: 4×0.25×2
- [ ] Thick wall: 4×1×2
- [ ] Tall wall: 4×0.25×4
## Floors / Platforms
- [ ] Flat tile: 2×2×0.25
- [ ] Large flat: 4×4×0.25
- [ ] Ramp: 4×2×0.25 angled at 30°
- [ ] Stairs (blocky): 2×2×2 subdivided
## Doorways / Arches
- [ ] Door frame: 2×0.25×3
- [ ] Arch: 2×0.25×3 with curve cutout

# 🪑 2. Props
- [ ] Crate: 1×1×1
- [ ] Barrel: Cylinder Ø1 × 1.5
- [ ] Column: Cylinder Ø0.5 × 3
- [ ] Rock: 1×1×1 blobby mesh
- [ ] Table: 2×1×1 with 4 cylinder legs
- [ ] Chair: 1×1×1.5 (blocky L-shape)

# 🧍 3. Characters / NPCs

- [ ] Player dummy: Capsule Ø0.5 × 2
- [ ] Enemy small: Sphere Ø1
- [ ] Enemy medium: Capsule Ø1 × 2
- [ ] Enemy large: Cube 2×2×2
(optional: rig a capsule with stick limbs for animation tests)

# 🎮 4. Gameplay Objects
- [ ] Collectible sphere: Ø0.5
- [ ] Collectible diamond: Cube 0.5×0.5×0.5 rotated 45°
- [ ] Health pack: Cube 0.5×0.5×0.5 with cross extrude
- [ ] Ammo box: 1×0.5×0.5
- [ ] Key: Flat cross shape 0.25×0.25×1

# ⚔️ 5. Weapons / Vehicles
- [ ] Sword placeholder: Cube 0.1×0.1×1 + small cross-guard
- [ ] Gun placeholder: L-shape block 1×0.25×0.5
- [ ] Car placeholder: Box 2×1×0.5 with 4 cylinders for wheels
- [ ] Plane placeholder: Box fuselage 2×0.5×0.5 with flat wing planes

# 🚩 6. Markers / UI
- [ ] Arrow: Cone Ø0.5 × 1 + small cylinder base
- [ ] Cone marker: Ø1 × 2
- [ ] Checkpoint pillar: Cylinder Ø0.25 × 2
- [ ] Flag: Cylinder pole Ø0.1 × 3 with flat plane flag

# 🔧 7. Extra Utility
- [ ] Grid floor plane (10×10)
- [ ] Bounding box (wireframe cube, 5×5×5)
- [ ] Simple camera placeholder (pyramid frustum shape)
# 3D Assets — MEP Suits

Every 3D model in the 3D System Viewer is a real downloaded model with a verified open license.
No paid, restricted, or unclear-license model is used. All models below are CC0 (public domain),
which needs no attribution; the viewer still credits Poly Haven as a courtesy.

## What changed (2026-10-19 3D fix)

The previous GLBs were repacked **diffuse-only**: normal, metallic-roughness (ARM),
and occlusion maps were dropped and replaced with scalar
`metallicFactor 0.35 / roughnessFactor 0.6` fallbacks — that is why the models
looked like flat plastic. They have been replaced with **full-PBR GLBs** rebuilt
from the original Poly Haven 1k glTF downloads: every map the 1k glTF references
(base color + normal + ARM metallic-roughness) is embedded, plus the separate
1k AO map where Poly Haven publishes one (wired as `occlusionTexture`).
Geometry is unchanged. No texture is above 1k.

Download method: the 1k `.gltf` + `.bin` come from
`https://dl.polyhaven.org/file/ph-assets/Models/gltf/1k/<slug>/<slug>_1k.gltf`
(the `.gltf`'s own include map is authoritative). The textures do NOT live under
that path — each texture's exact URL, size, and md5 comes from the Poly Haven
API, `https://api.polyhaven.com/files/<slug>` → `gltf` → `1k` → `gltf` →
`include` (texture URLs live under `Models/jpg/1k/<slug>/…`), and AO maps from
the same API (`<key>_ao` → `1k` → `jpg`). Every file below was downloaded from
those API URLs and verified against the API's size + md5.

Renderer (in `index.html`, 3D viewer only): ACESFilmicToneMapping, exposure
1.05, sRGB output, PCFSoft shadows, physically-correct lights; hemisphere +
warm key directional (2048 shadow map, ±8 frustum) + warm fill + cool rim;
image-based lighting from an inline emissive-panel room scene baked through
PMREM (r128 ships no `RoomEnvironment.js` and no `Scene.environment`, so the
PMREM texture is applied per material). Ground is a large dark concrete-style
plane that receives shadows (no grid).

Composition: AC unit on the ground, left. ONE straight duct run above/behind
it (rectangular OR circular, never both — swapped by the Duct Sizer shape).
ONE straight pipe run on the right, near the ground. Ceiling fan hung above
the duct run. The duct/pipe sets are
modular kits; only their straight sections are shown, chained end-to-end on
one centreline (bends, corners, transitions, vents, braces removed — see
"Straight sections kept" per model). Final world bounds (verified by
recomputing the arranged + fitted boxes from the GLB geometry):
- AC unit: x −5.60…−3.00, y 0…1.34, z −1.17…−0.63
- Rectangular duct run: x −3.40…3.00, y 2.00…2.82, z −1.63…−0.57
- Circular duct run: x −3.40…3.00, y 2.00…2.55, z −1.37…−0.83
- Pipe run: x −1.90…4.30, y 0.55…1.01, z 1.37…1.83
- Ceiling fan: x −0.60…1.60, y 3.40…4.60, z −0.30…1.90 (hung above the
  duct run, clear of it — duct top is 2.82)

No two visible groups overlap. Camera: orbit + zoom only (X-ray, auto-rotate,
and view-preset controls removed).

## Used

### 1. Outdoor AC unit — "plant unit"
- **File:** `models/ac-unit.glb` (8,118,308 bytes)
- **What it is:** "Exterior Aircon Unit" — a real outdoor air-conditioning unit model.
  Used as the plant-room unit. It is labelled **"Outdoor AC unit"** — never labelled an AHU.
- **Source page:** https://polyhaven.com/a/exterior_aircon_unit
- **Download URLs (source files, 1k glTF):**
  - glTF: https://dl.polyhaven.org/file/ph-assets/Models/gltf/1k/exterior_aircon_unit/exterior_aircon_unit_1k.gltf
  - `.bin` + textures: exact URLs/sizes/md5s from https://api.polyhaven.com/files/exterior_aircon_unit → `gltf` → `1k` → `gltf` → `include`
  - AO: same API → `01_ao` / `rusted_01_ao` → `1k` → `jpg`
- **License:** CC0 1.0 — Poly Haven publishes all assets under CC0.
  (https://polyhaven.com/license — "All assets on Poly Haven are CC0.")
- **License link:** https://creativecommons.org/publicdomain/zero/1.0/
- **Author:** Poly Haven contributors (no individual author name shown on the asset page).
- **Maps kept (all 1k, all embedded in the GLB):**
  - `exterior_aircon_unit_01`: base color (`01_diff`, 506,664 B) + normal (`01_nor_gl`, 472,088 B) + ARM (`01_arm`, 651,293 B) + AO (`01_ao`, 453,572 B, as `occlusionTexture`)
  - `exterior_aircon_unit_02`: base color (`01_opacity`, 333,675 B — this is what the author's 1k glTF references for this material) + normal (`02_nor_gl`, 942,230 B) + ARM (`02_arm`, 484,026 B). No separate AO published for `02` → no `occlusionTexture`.
  - `exterior_aircon_unit_rusted_01`: base color (`rusted_01_diff`, 606,076 B) + normal (`rusted_01_nor_gl`, 583,620 B) + ARM (`rusted_01_arm`, 673,246 B) + AO (`rusted_01_ao` — byte-identical to `01_ao`, embedded once and shared)
  - `exterior_aircon_unit_rusted_02`: base color (`rusted_02_opacity`, 357,558 B — as authored in the 1k glTF) + normal (`rusted_02_nor_gl`, 947,477 B) + ARM (`rusted_02_arm`, 605,557 B). No separate AO published for `rusted_02` → no `occlusionTexture`.
  - Geometry: `exterior_aircon_unit.bin` (494,784 B). Total embedded images: 13.
- **Modifications by Darren Labs:** repacked from the original 1k glTF + `.bin` + textures into a single self-contained `.glb`, keeping ALL maps. Only change from the source glTF: `occlusionTexture` added where a separate AO map exists. Geometry unchanged. This is permitted under CC0.
- **Straight sections kept:** n/a — the AC unit is shown whole (both units).
- **Replaces:** the procedural AHU box (body + panels + stripe + fan disc + ring + plinth), and the earlier diffuse-only GLB.

### 2. Rectangular duct run
- **File:** `models/duct-rectangular.glb` (2,953,744 bytes)
- **What it is:** "Modular Airduct Rectangular 01" — a real set of rectangular metal
  duct pieces (author: James Ray Cock).
  Shown when the Duct Sizer shape is Rectangular. Labelled **"Rectangular duct run"**.
- **Source page:** https://polyhaven.com/a/modular_airduct_rectangular_01
- **Download URLs (source files, 1k glTF):**
  - glTF: https://dl.polyhaven.org/file/ph-assets/Models/gltf/1k/modular_airduct_rectangular_01/modular_airduct_rectangular_01_1k.gltf
  - `.bin` + textures: exact URLs/sizes/md5s from https://api.polyhaven.com/files/modular_airduct_rectangular_01 → `gltf` → `1k` → `gltf` → `include`
  - AO: same API → `parts01_ao` / `parts02_ao` → `1k` → `jpg`
- **License:** CC0 1.0 — confirmed on the asset page ("CC0 1.0 Universal — public domain
  dedication, no attribution required", creator James Ray Cock).
- **License link:** https://creativecommons.org/publicdomain/zero/1.0/
- **Author:** James Ray Cock
- **Maps kept (all 1k, all embedded in the GLB):**
  - `…_parts02`: base color (`parts02_diff`, 158,760 B) + normal (`parts02_nor_gl`, 88,121 B) + ARM (`parts02_arm`, 188,686 B) + AO (`parts02_ao`, 52,145 B, as `occlusionTexture`)
  - `…_parts01`: base color (`parts01_diff`, 187,245 B) + normal (`parts01_nor_gl`, 63,936 B) + ARM (`parts01_arm`, 247,732 B) + AO (`parts01_ao`, 149,601 B, as `occlusionTexture`)
  - Geometry: `modular_airduct_rectangular_01.bin` (1,795,116 B). Total embedded images: 8.
- **Modifications by Darren Labs:** repacked to `.glb` with ALL maps (see above) + `occlusionTexture` added. Geometry unchanged.
- **Straight sections kept (chained end-to-end, 4.00 local units, uniform 0.66 × 0.51 cross-section):** `single_01`, `double_01`, `tripple_01`, `half_01`. Removed from view: corners, bends, transitions, splitter, connector, vents, braces, fastener.
- **Replaces:** the procedural rectangular duct boxes, and the earlier diffuse-only GLB.

### 3. Circular duct run
- **File:** `models/duct-circular.glb` (1,981,040 bytes)
- **What it is:** "Modular Airduct Circular 01" — a real set of circular metal duct pieces.
  Shown when the Duct Sizer shape is Round. Labelled **"Circular duct run"**.
- **Source page:** https://polyhaven.com/a/modular_airduct_circular_01
- **Download URLs (source files, 1k glTF):**
  - glTF: https://dl.polyhaven.org/file/ph-assets/Models/gltf/1k/modular_airduct_circular_01/modular_airduct_circular_01_1k.gltf
  - `.bin` + textures: exact URLs/sizes/md5s from https://api.polyhaven.com/files/modular_airduct_circular_01 → `gltf` → `1k` → `gltf` → `include`
  - AO: Poly Haven publishes **no** separate AO map for this asset → no `occlusionTexture` (the AO channel inside the ARM texture is not wired, to avoid sampling the wrong channel).
- **License:** CC0 1.0 — Poly Haven publishes all assets under CC0.
- **License link:** https://creativecommons.org/publicdomain/zero/1.0/
- **Author:** Poly Haven contributors (no individual author name shown on the asset page).
- **Maps kept (all 1k, all embedded in the GLB):**
  - Both materials (`modular_airduct_circular_01`, two texture slots sharing one image set): base color (`…_diff`, 542,554 B) + normal (`…_nor_gl`, 317,118 B) + ARM (`…_arm`, 620,251 B). No AO (see above).
  - Geometry: `modular_airduct_circular_01.bin` (485,456 B). Total embedded images: 3.
- **Modifications by Darren Labs:** repacked to `.glb` with ALL maps. Geometry unchanged.
- **Straight sections kept (chained end-to-end, 4.35 local units, uniform Ø 0.37 cross-section):** `single`, `double`, `triple`, `smooth_single`, `smooth_double`, `smooth_triple`. Removed from view: vent fan, converter, bends, fan, braces.
- **Replaces:** the procedural round duct cylinders, and the earlier diffuse-only GLB.

### 4. Industrial pipe run
- **File:** `models/pipes-industrial.glb` (5,219,488 bytes)
- **What it is:** "Modular Industrial Pipes 01" — a real set of industrial pipes.
  Labelled **"Straight pipe run"**.
- **Source page:** https://polyhaven.com/a/modular_industrial_pipes_01
- **Download URLs (source files, 1k glTF):**
  - glTF: https://dl.polyhaven.org/file/ph-assets/Models/gltf/1k/modular_industrial_pipes_01/modular_industrial_pipes_01_1k.gltf
  - `.bin` + textures: exact URLs/sizes/md5s from https://api.polyhaven.com/files/modular_industrial_pipes_01 → `gltf` → `1k` → `gltf` → `include`
  - AO: same API → `group01_ao` / `group02_ao` → `1k` → `jpg`
- **License:** CC0 1.0 — Poly Haven publishes all assets under CC0.
- **License link:** https://creativecommons.org/publicdomain/zero/1.0/
- **Author:** Poly Haven contributors (no individual author name shown on the asset page).
- **Maps kept (all 1k, all embedded in the GLB):**
  - `…_group01`: base color (`group01_diff`, 553,576 B) + normal (`group01_nor_gl`, 674,568 B) + ARM (`group01_arm`, 860,825 B) + AO (`group01_ao`, 150,165 B, as `occlusionTexture`)
  - `…_group02`: base color (`group02_diff`, 580,676 B) + normal (`group02_nor_gl`, 725,187 B) + ARM (`group02_arm`, 898,932 B) + AO (`group02_ao`, 250,837 B, as `occlusionTexture`)
  - Geometry: `modular_industrial_pipes_01.bin` (515,160 B). Total embedded images: 8.
- **Modifications by Darren Labs:** repacked to `.glb` with ALL maps (see above) + `occlusionTexture` added. Geometry unchanged.
- **Straight sections kept (chained end-to-end, 2.81 local units, uniform Ø 0.21 cross-section):** `pipe02`, `pipe01` (the only two straight cylinders in the set; the other six pieces are elbow/drop assemblies). Removed from view: `pipe03`–`pipe08`.
- **Replaces:** the procedural pipe cylinders, and the earlier diffuse-only GLB.

### 5. Ceiling fan
- **File:** `models/ceiling-fan.glb` (1,870,740 bytes)
- **What it is:** "Ceiling Fan" — a real ceiling fan model (mount + blades).
  Hung above the duct run at (0.5, 3.4, 0.8), fitted to ≤2.2 m × ≤1.2 m ×
  ≤2.2 m. Labelled **"Ceiling fan"** — it is NOT labelled a centrifugal fan.
- **Source page:** https://polyhaven.com/a/ceiling_fan
- **Download URLs (source files, 1k glTF):**
  - glTF: https://dl.polyhaven.org/file/ph-assets/Models/gltf/1k/ceiling_fan/ceiling_fan_1k.gltf (4,777 bytes, md5 `c5ec36847eb915c1cc924a70edd88854`)
  - Geometry: `ceiling_fan.bin` (455,032 bytes, md5 `f073b4dd387c8a6f9374307fc4b6f1df`) — served from the 4k path per the API, same file
  - Base color: `ceiling_fan_diff_1k.jpg` (392,243 bytes, md5 `75f1c808dcd3ba2d7c22b00c724105b0`)
  - Normal (OpenGL): `ceiling_fan_nor_gl_1k.jpg` (390,818 bytes, md5 `c81e02695e4c8528b192b458f2db23c2`)
  - ARM: `ceiling_fan_arm_1k.jpg` (566,114 bytes, md5 `d1356bc14a05ecc25ae96d093e43c546`)
  - Emissive: `ceiling_fan_emissive_1k.jpg` (36,867 bytes, md5 `778d0adc5af793919e26c21da0d18032`)
  - Specular: `ceiling_fan_spec_1k.jpg` (26,647 bytes, md5 `7ba7036733c1e57ed3e9c3f01ac056ca`) — kept as `KHR_materials_specular` (r128 ignores it, as with the generator)
- **License:** CC0 1.0 — Poly Haven publishes all assets under CC0.
- **License link:** https://creativecommons.org/publicdomain/zero/1.0/
- **Author:** Poly Haven contributors (no individual author name shown on the asset page).
- **Maps kept (FULL PBR — nothing dropped):** base color + normal + ARM +
  emissive + specular. 2 meshes, 1 material, 5 textures. All MD5s verified
  against the Poly Haven API.
- **Modifications by Darren Labs:** repacked from the original 1k glTF + `.bin` +
  textures into a single self-contained `.glb`. Geometry unchanged. This is
  permitted under CC0.

## What was NOT found
- **No true CC0 AHU model exists** on Poly Haven (521 models — no AHU; closest plant
  equipment is the outdoor AC unit). The viewer therefore shows an outdoor AC unit and
  labels it exactly that — it is NOT labelled an AHU.
- **No true CC0 pump model exists** on Poly Haven (the only "pump" hit is a tire pump).
  The procedural pump was removed entirely rather than replaced with a wrong model.
- **No true CC0 VAV box / diffuser / fan-coil model exists** on Poly Haven. The
  procedural fan, VAV, and diffuser blocks were removed entirely.
- **No separate AO map** is published for the circular duct set, or for the AC
  unit's `02` / `rusted_02` materials. Those materials have no `occlusionTexture`;
  their ARM maps still carry the AO channel, but it is left unwired rather than
  sampled from the wrong channel.
- Kenney / Quaternius were not needed: Poly Haven supplied duct, pipes, and the AC unit.
- Kenney City Kit (Industrial) was downloaded and inspected this pass
  (CC0, `kenney_city-kit-industrial_2.0.zip`, License.txt verified): it
  contains only buildings, chimneys, tanks, containers, solar panels, a
  water tower, and windmills — no AHU, pump, VAV, diffuser, or fan. None
  was added (a stylised Kenney building would also clash with the photoreal
  PBR models).
- **AHU / pump / VAV / diffuser — NOT FOUND via anonymous download.**
  Sketchfab HAS CC-BY candidates, all verified via the Sketchfab API
  (license + downloadable: true):
  - AHU: "HAHU-B Mini Horizontal Air Handling Unit" by polar_air
    (https://sketchfab.com/3d-models/hahu-b-mini-horizontal-air-handling-unit-23b8c1949ddb4c8b9be2e30ff37358bb,
    CC Attribution) and "VAHU Mini Vertical Air Handling Unit" by polar_air
    (https://sketchfab.com/3d-models/vahu-mini-vertical-air-handling-unit-ed1376ac63434cbdab7dc55c19a09f98,
    CC Attribution)
  - Pump: "CENTRIFUGAL PUMP | BOMBA CENTRÍFUGA" by engipros
    (https://sketchfab.com/3d-models/centrifugal-pump-bomba-centrifuga-a49b7e1567714040826fc6a24c4e8a7d,
    CC Attribution)
  - Diffuser: "Rectangular Diffuser" by krio302
    (https://sketchfab.com/3d-models/rectangular-diffuser-3e0d1d2f3399421c8902646c54903250,
    CC Attribution) and "Circular General Diffuser" by krio302
    (https://sketchfab.com/3d-models/circular-general-diffuser-534338b5842149eea73d5ed5471d83b6,
    CC Attribution). The "Square Ceiling Air Diffuser" by MohammadRajabloo
    was SKIPPED — CC-BY-ND (NoDerivs, modification not allowed).
  - Fan (centrifugal): "Centrifugal fan" by zyzz.az.zyzz
    (https://sketchfab.com/3d-models/centrifugal-fan-c8078f48cf08484cac6dd3182fa7eeb6,
    CC Attribution) and "Radial Centrifugal Fan / Blower" by nasateja4
    (https://sketchfab.com/3d-models/radial-centrifugal-fan-blower-3d-cad-model-a51a965888164d48b3abd2a614bf69cb,
    CC Attribution). The Poly Haven ceiling fan added this pass is NOT a
    centrifugal fan and is labelled exactly as a ceiling fan.
  - VAV box: no Sketchfab CC-BY VAV box found (search returned 0
    downloadable results) — still genuinely missing.
  - BLOCKER for all of the above: Sketchfab's download API returns
    **401 Unauthorized** without an OAuth token — downloads require a
    signed-in Sketchfab account. This subagent cannot sign in (no
    live-browser / credential flow). **To get them: run a browser-task with
    Darren's Sketchfab sign-in, download the CC-BY GLBs, and add each with
    attribution.** Do NOT bypass the login, do NOT use NC/ND models.

## Loading + fallback + live link
- Models load via Three.js `GLTFLoader` (r128, jsdelivr → unpkg fallback), lazily:
  loading starts only when the 3D System Viewer tab is opened.
- CSP still allows the loader CDNs (`script-src` includes `https://cdn.jsdelivr.net`
  and `https://unpkg.com`); models are same-origin, allowed by `connect-src 'self'`.
- Live link to the calculators: the Duct Sizer shape (Round / Rectangular) swaps which
  real duct run is shown; the duct / pipe size labels (chips) update from the calculator
  inputs; particle speed follows the calculated air / water velocities. The models
  themselves are fixed real sets — inputs do NOT rebuild procedural geometry.
- If GLTFLoader or all GLBs fail to load, a clean message is shown in the viewer
  ("3D models could not load… Every calculator still works in 2D.") and NO
  placeholder blocks are rendered — the scene stays empty (floor + labels) and
  every calculator keeps working.
- Click a model for a one-line label. Drag to orbit, scroll to zoom.
- Reduced-motion: the scene is static (no auto-rotate, no particle motion).
- The Patterns-style abstract diagrams elsewhere on the site stay procedural — they are
  diagrams, not physical objects.

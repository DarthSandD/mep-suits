# MEP Suits viewer v3: parametric BIM system (2026-10-21)

Darren rejected the v2 direction at the model level: the three downloaded
GLB props were static and unusable. This build replaces them with a
parametric, procedurally generated plant room inside the same single-file
app (`index.html` + `vendor/three.min.js`, no new dependencies). The v2
furniture (purpose strip, Revit tags, duct dimension, compass, title block)
is unchanged and now anchors to the generated groups.

## What is generated

- **AHU-1 outdoor unit** (group `unit`): casing with panel seams and top
  rim, coil face with a fin bank (Fine detail), fan disc with grille rings
  and hub (spokes at Fine), access panel with handle, plinth feet.
  Casing 2.3 x 1.7 x 1.05 m.
- **Duct network** (group `duct`): main run in three flanged segments, a
  connector stub toward the unit, two branch take-offs (one with a
  segmented 90-degree elbow, vertical drop and end cap; one straight with
  end cap; collars at the roots), then a square-to-round transition
  (custom frustum geometry) into a circular spigot with end cap. In round
  mode the main is a cylinder with ring flanges and circular branches.
  Section size is live from the Duct Sizer (rect W x H or round diameter).
- **Pipe network** (group `pipes`): CHW supply and return pair with torus
  90-degree elbows, floor risers at the left, drops to the pump at the
  right, three gate valves (body, flange rings, bonnet, stem, handwheel;
  spokes at Fine) and one check valve. Bore is live from Pipe Hydraulics.
- **Pump set P-1** (group `pump`): plinth, volute with face ring, motor
  with terminal box and cooling fins (Fine).
- **Supports** (group `supports`): duct trapeze hangers (rods + bar,
  following the live section) and pipe posts with saddles.

## Option matrix (as built)

| Control | Options | Effect |
| --- | --- | --- |
| View | 3D / Plan / Section / Elevation | Camera preset with eased tween; Section adds one clipping plane (z = -1.05) through the duct run, applied to BIM materials only |
| Detail level | Coarse / Medium / Fine | Coarse hides flanges, collars, valve rings; Medium shows them; Fine adds coil fins, fan spokes, handwheel spokes, motor fins |
| Visual style | Shaded / Realistic / Hidden Line / Wireframe | Shaded flattens environment response; Realistic is the v2 lighting; Hidden Line swaps to a pale basic material with dark EdgesGeometry lines on a light background; Wireframe sets wireframe on all standard materials |
| Systems | Air / Water / Supports | Independent group visibility (unit + duct, pipes + pump, supports) |
| Insulation | Pipe / Duct | Pale cladding cylinders (r + 38 mm) on the pipe straights; foil-grey wrap boxes on the main duct segments |
| Flow particles | Air / Water (existing toggles) | Particle streams on the duct centreline and the supply pipe, speed from the live calculator velocities |

## Live wiring

- The existing 250 ms sync interval detects Duct Sizer / Pipe Hydraulics
  changes; a 240 ms debounced rebuild regenerates only the duct group
  (plus supports, which follow the section) or only the pipe group.
- Clicking a component raycasts to its group, draws an orange BoxHelper
  (Revit selection vernacular), and fills the Component properties box in
  the sidebar: name, type, live size, and values read straight from the
  calculator readouts on the page (duct velocity / airflow / friction
  rate, water velocity / flow, pump duty head / shaft power). Nothing is
  invented; uncomputed readouts show as they appear on the page.
- Dimension callout measures the first main-run segment (rect) or the
  main cylinder (round), so branches and hangers cannot corrupt it.

## GLB retirement

`modelDefs`, `arrangeRun`, `fitGroup`, `ensureLoader`, `loadModels_RETIRED`
and `pick_RETIRED` remain in the file under a RETIRED banner (Darren's
direction, 2026-10-21), never called. The model files stay in the repo
untouched. Delete the block in one pass once the parametric system soaks.

## Verification

Frames in `verification-v3/`, captured headless (Chromium + SwiftShader,
1280x900) from a local copy with boot scripts driving the page like a
user (nav click, shape click, input events, panel clicks):

- `01-3d-shaded-medium-rect-600x300.png`
- `02-plan-rect-600x300.png`
- `03-hidden-line-rect-600x300.png`
- `04-3d-realistic-round-630.png`

Inspection notes (every frame read at full size by the builder):

- 01: Panel controls render cleanly as a properties palette, no overlaps.
  Scene shows AHU-1 (casing seams, coil slats, fan grille rings), the
  flanged rectangular run, square-to-round transition and capped spigot,
  branches, hangers, the pipe pair with red handwheels, and the pump set.
  Tags all legible and separated (first capture had the AHU and DUCT tags
  touching; anchors were moved and the frame re-captured). Dimension tag
  reads 600 x 300 on the run's end section. Purpose strip and chips echo
  the page readouts (600 x 300 mm, 15.24 m/s, ID 105.3 mm, 0.92 m/s).
- 02: True plan (compass N up): duct band with flange lines, two branch
  tabs, taper and spigot at the right, unit rectangle at the left, pipe
  pair and pump below. First plan framing clipped the AHU tag at the left
  edge and crowded the chips; the plan preset was widened twice
  (r 13.8 to 19, recentred) and the final frame has every tag inside the
  frame and legible.
- 03: Hidden Line reads as a proper line drawing: pale fills, dark edges,
  all equipment and tags legible, no tag overlap.
- 04: Default state (Realistic, Medium): round main with ring flanges,
  circular branches with drops, end cap; dimension and tags read
  O 630 (DOM probe confirms the exact text). The viewer opens on the
  app's own default, which is the round duct.
- Selection was verified separately with scripted pointer clicks on a
  grid over the canvas in the same headless copy: AHU, duct, pipes, pump
  and supports all select and fill the properties box. That pass caught
  one real bug: the Airflow and Flow rows read two calculator INPUTS
  (dQ, wQ) as if they were text readouts and showed blank; they now read
  the input values with their page unit (2500 L/s verified in the panel).

Capture method note: frames were driven over the DevTools protocol in
real time. SwiftShader starves page timers, so captures waited 25-45 s
for staged actions (nav, shape click, input events, panel clicks) and
camera tweens to settle; a DOM state probe (tag texts, live class)
confirmed the settled state behind frames 02 and 04.

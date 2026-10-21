# Viewer V4 - coordinator craft pass (2026-10-22)

Built personally by the coordinator under Darren's Two-Rejection Rule
(v2 furniture + v3 parametric both rejected on quality). V3's wiring,
options and furniture are unchanged; V4 is model craft and framing:

- Galvanised steel is now a procedural spangle texture (canvas-generated),
  brushed steel likewise; edge lines on in Shaded and Realistic
  (Revit shaded-with-edges), not only Hidden Line.
- Ductwork: longitudinal seam, extra TDC joints/stiffeners on the long
  runs, shorter round spigot.
- AHU rebuilt as a machine: fan cowl plate with the grille and impeller
  blades behind it, louvre bank on the intake end, corner posts, base
  rails, door hinges, data plate.
- Room context: back wall + column for scale, soft AO pools grounding
  unit, duct, pipes and pump; floor and grid contrast raised.
- Cameras tightened (3D r 12.8 -> 10.4; Plan r 19 -> 16) and plan
  re-centred; tags and the dimension tag are now clamped inside the
  canvas in every view (the plan view previously clipped the AHU tag).

Verified by the coordinator on captured frames (verification-v4/):
rect 800x300 3D Realistic, rect Plan, round 3D Realistic - inspected
at full size against the v3 frames. Rect defaults on the page are
800x300; 600x300 is one input change away and rebuilds live.

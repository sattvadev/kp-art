# Trace Camera

A browser tool for tracing a picture onto paper. The phone's camera shows your paper live,
and your chosen photo floats see-through on top, so you can draw while watching your pencil on screen.

- Modes: the photo itself, **Outlines** (sketch strokes in the style of Coherent Line Drawing / flow-based DoG with
  XDoG-style soft thresholding: long, continuous lines that follow the form, heavier on strong edges, tapering at the ends),
  or **Values**: a breakdown strip of every value from lightest (1, paper) to darkest,
  shown as a breakdown: the whole picture in greys with the current step filled in a bright colour (coral, blue, green
  or yellow). Layered fills the area painted at that step (that value and darker), Stencil fills exactly that value, All shows the greys.
  Shapes have smooth, anti-aliased edges with a clean contour stroke. Numbered grey swatches pick the step, lightest (1) to darkest.
- Values are found with an edge-preserving filter (keeps edges crisp, no halo rings), grouped by the photo's own tones,
  then cleaned of slivers and specks so each value is a solid stencil. A second 'details' pass from a lightly smoothed
  photo keeps small features the broad shapes would flatten: eye openings, nostrils, ear holes, the lip line, catchlights.
  A Simplify slider trades detail for bolder shapes.
- Drag to move, pinch to resize and rotate, then Lock. Hold "peek" to check your lines.
- See-through slider, mirror, grid, line colour, torch (where the phone supports it), screen kept awake.

Photos are processed on the device and never uploaded. Everything is in `index.html`; no build step.
Needs https for camera access (GitHub Pages provides it).

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
- **AI sketch** (optional, in Outlines): the "OpenSketch" model from *Informative Drawings* by Caroline Chan, Frédo Durand
  and Phillip Isola (CVPR 2022, MIT License, https://github.com/carolineec/informative-drawings), run on the phone with
  onnxruntime-web: WebGPU where available, else WebAssembly. The 17 MB model downloads once and is kept on the device.
  See `models/README.md` and `models/LICENSE-informative-drawings`.
- Controls: a top bar (Back, undo, redo, Tools), a Tools sheet with tabs (Picture, Strobe, Grid, Camera, Flashlight),
  and a bottom bar choosing what your fingers move (Picture, Camera, Grid) plus Move, Hide and Opacity.
- With **Move** on, drag, pinch and twist the picture (or drag the grid). Turn Move off to lock it; then pinch to zoom
  the whole view (camera, picture and grid together, so the picture stays on the paper). Double-tap to zoom back out.
- Strobe blinks the picture to compare with your drawing; the grid covers the screen with adjustable colour, opacity and
  cell size; Camera can pause or switch cameras; Flashlight turns on the torch where the browser allows it.
- Opacity, mirror and line colour; the screen is kept awake.

Photos are processed on the device and never uploaded. Everything is in `index.html`; no build step.
Needs https for camera access (GitHub Pages provides it).

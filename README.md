# Trace Camera

A browser tool for tracing a picture onto paper. The phone's camera shows your paper live,
and your chosen photo floats see-through on top, so you can draw while watching your pencil on screen.

- Modes: the photo itself, **Outlines** (a line drawing of the photo's real edges: eyes, nose, lips, jaw, hair, clothing,
  jewellery, found in colour as well as brightness, with no lines across smooth gradients), or **Values**: a breakdown strip of every value from lightest (1, paper) to darkest,
  shown Layered (light to dark up to the chosen value, the new shape outlined in red), as a single Stencil, or All at once.
- Values are found with an edge-preserving filter (keeps edges crisp, no halo rings), grouped by the photo's own tones,
  then cleaned of slivers and specks so each value is a solid stencil. A Simplify slider trades detail for bolder shapes.
- Drag to move, pinch to resize and rotate, then Lock. Hold "peek" to check your lines.
- See-through slider, mirror, grid, line colour, torch (where the phone supports it), screen kept awake.

Photos are processed on the device and never uploaded. Everything is in `index.html`; no build step.
Needs https for camera access (GitHub Pages provides it).

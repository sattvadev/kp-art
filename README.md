# KP Art

KP Art is a camera tracing app for drawing and watercolour. Live at https://sattvadev.github.io/kp-art/

It is the art-only edition of NUMOTIFSTUDIO - Trace: the camera tracing and the draw-on-screen painting tools, without the
fashion features, kept separate from the fashion edition (sattvadev/trace-camera). Colours follow the KP Art logo (wine #6C0130) on the NU Motif design system
(warm paper, DM Sans). Icons and the white KP mark are in `assets/`.

A browser tool for tracing a picture onto paper. The phone's camera shows your paper live,
and your chosen photo floats see-through on top, so you can draw while watching your pencil on screen.

- Modes: the photo itself, **Outlines** (sketch strokes in the style of Coherent Line Drawing / flow-based DoG with
  XDoG-style soft thresholding: long, continuous lines that follow the form, heavier on strong edges, tapering at the ends),
  or **Values**: a breakdown strip of every value from lightest (1, paper) to darkest,
  shown as a breakdown: the whole picture in greys with the current step filled in a bright colour (coral, blue, green
  or yellow). By default a step fills only that one value, so you see exactly where that shade goes; with Show earlier steps on, it fills that value and every darker one (the area painted at that step). All shows the greys.
  Shapes have smooth, anti-aliased edges with a clean contour stroke. Numbered grey swatches pick the step, lightest (1) to darkest.
- Values are found with an edge-preserving filter (keeps edges crisp, no halo rings), grouped by the photo's own tones,
  then cleaned of slivers and specks so each value is a solid stencil. A second 'details' pass from a lightly smoothed
  photo keeps small features the broad shapes would flatten: eye openings, nostrils, ear holes, the lip line, catchlights.
  A Simplify slider trades detail for bolder shapes.
- **AI sketch** (optional, in Outlines): the "OpenSketch" model from *Informative Drawings* by Caroline Chan, Frédo Durand
  and Phillip Isola (CVPR 2022, MIT License, https://github.com/carolineec/informative-drawings), run on the phone with
  onnxruntime-web: WebGPU where available, else WebAssembly. The 17 MB model downloads once and is kept on the device.
  See `models/README.md` and `models/LICENSE-informative-drawings`.
- Drawing screen: a top bar (Home, undo, redo, Help, Tools) and, at the bottom, a **step strip** plus Move, Hide and Opacity.
  The step strip shows in Values and AI outlines: tap any number (1 lightest first) to jump straight to that step, or All.
  Picture / Grid choices appear only while Move is on and the grid is shown.
- **Tools** opens a short panel under the top bar (View, Grid, Strobe, Camera, Light) with the drawing still visible.
  The button turns into **Done**; tapping the picture or the phone's back gesture also closes it. Rarely used options
  (line style, show earlier steps, fit, mirror, new photo) sit under More options.
- **Home** asks before leaving the drawing. The browser back gesture closes Tools or Help first, and asks before leaving.
- With **Move** on, drag, pinch and twist the picture (or drag the grid). Magnifying only works with the picture locked:
  turn Move off, then pinch to zoom the camera view with the picture on it, so the picture stays on the paper.
  A Locked badge shows the zoom; tap it to unlock. Double-tap to zoom back out. The browser's own page zoom is blocked.
- AI sketch comes in three layers, traced in passes: 1 main lines, 2 secondary lines, 3 light lines and texture
  (strokes grouped by how firmly they are drawn). Show earlier steps (on by default) builds the steps up; off shows one step alone.
- **Grid on the photo** (default): square cells fixed to the picture, with its outline and optional diagonals. It moves,
  scales, turns and mirrors with the photo, so proportions and perspective stay lined up while you place it. Choose how many
  squares go across; Hide leaves the grid showing. A screen grid (fixed to the screen, draggable) is still available.
- Strobe blinks the picture to compare with your drawing; the grid has adjustable colour and opacity; Camera can pause or switch cameras; Flashlight turns on the torch where the browser allows it.
- Opacity, mirror and line colour; the screen is kept awake.

## Draw on screen (iPad + Apple Pencil, or a finger on a phone)

The same painting tools as NUMOTIFSTUDIO - Trace, without the fashion features (no prints, croquis, line-up or AI sketches
from photos).

- **The screen is the paper:** the start screen's second button skips the camera. The Pencil draws over the picture with
  pressure (wider line) and tilt (shading). Fingers never draw unless **Finger draws** is on (Tools → Draw), so a resting palm
  leaves no marks; a touch while the Pencil is down, or just after it lifts, is ignored. On a phone the finger draws by default;
  on iPad the first one-finger tap asks once whether to turn finger drawing on. Two fingers move and pinch-zoom the page (the
  drawing re-renders sharp at the new zoom); two- and three-finger taps undo and redo.
- **Rail on the left:** Brush, Eraser, Fill, Colour, Settings, Layers and Mirror. On short screens (a phone on its side) the
  rail starts under the top bar.
- **Brushes**, grouped in the picker: Sketch: pencil (paper grain, tilt to shade), charcoal (coarse, broken grain). Ink and
  lines: fineliner, technical pen (one even width), brush pen (tapered, pressure-swelling), dip pen (hairline to bold with
  pressure), calligraphy (a flat nib at a set angle, thick and thin from the stroke's direction). Paint and colour: marker
  (see-through, multiplies where it overlaps), watercolour, gouache, dry brush (bristles that streak and run dry, seeded per
  stroke so a saved drawing looks the same), pastel (waxy, paper showing through), airbrush. Shading: Shadow and Highlight
  (work anywhere by default; "Only on paint already there" limits them to paint on their layer). Hard or soft eraser on the
  chosen layer. Every line stroke is built from simple shapes (round dabs, a swept nib, or bristles) shared by the screen and
  the SVG export.
- **Brush settings panel:** a live preview stroke drawn by the real engine, then Size and Opacity and only the settings that
  apply to the brush: Hardness, Nib angle, Nib thickness and "Nib turns with Apple Pencil" (calligraphy), Size with pressure,
  Tilt to shade, Smoothing, Taper start and end, Size jitter, Paper grain, Only on paint already there. Each brush keeps its own
  settings; Reset this brush restores them. What a stroke needs is saved with the stroke, so changing settings later never
  changes earlier lines.
- **Size ring:** a circle at the brush's size under a hovering Apple Pencil (or mouse), under the eraser while erasing, and in
  the middle of the screen while dragging Size.
- **Colour:** recent colours, the value-step greys, neutrals, earth pigments (ochre, siennas, umbers, Payne's grey), a colour
  wheel of paint colours, the system colour picker, and Pick colour from photo (averages the reference photo's real pixels
  under the tap). **Recolour** swaps one colour for another across the whole drawing (undo puts it back).
- **Fill:** tap inside a closed outline (the shown Sketch and Lines layers) to fill it with the current colour on the Colour
  layer, under the lines. Close gaps bridges small breaks; an open shape is refused instead of flooding the page.
- **Layers** bottom to top: Colour, Sketch, Lines, each shown or hidden with its own opacity; brushes pick their layer (paint
  goes under the lines). Optional watercolour paper texture behind the page. Watercolour, airbrush, shading and soft edges are
  painted per stroke (blurred body and bleed, darker drying edge, pigment variation and paper granulation) and cached per zoom.
- **Mirror:** copies what you draw across the middle of the page (shown as a dashed line), for symmetrical subjects.
- **Save:** Tools → Draw saves a PNG of every shown layer (about 3000 px on the long side) or an SVG of the line brushes,
  grouped by layer, with erasers as masks (watercolour, airbrush, shading, soft edges and fills are pixels, so only in the PNG).
  Files go through the share sheet on iPhone and iPad.
- **Layers (rail: Layers):** every drawing starts with Colour, Sketch and Lines; + New layer adds one above the current
  layer (up to 12). Each row has a thumbnail, show/hide, lock and opacity; ⋯ has Blend (Normal, Multiply, Screen, Overlay,
  Soft light, Darken, Lighten, Colour), Rename (or double-tap the name), Move up/down, Duplicate, Merge down, Clear and
  Delete. Every change is one undo step and the layers are saved with the drawing. A locked layer cannot be drawn on,
  erased, filled or moved. Fills go on Colour (or on your own layer when you are on one). Merge down keeps plain strokes
  as strokes; a layer that erases, blends, is faded or shades only its paint merges as one picture so it looks the same.
- **Select (rail: Select):** draw a loop on the current layer. A loop round whole lines keeps them as lines; a loop that
  cuts through lines (or round lines an eraser touched) takes the pixels inside as one picture. Tap a line to pick it.
  Drag to move, corners to scale, edge squares to stretch, the round handle to turn; Flip ↔ ↕, Duplicate, Copy, Cut,
  Paste, Delete and Move to another layer. Two fingers still move and zoom.
- **Pick a colour:** touch and hold with the Pencil (or finger, with finger drawing on): a loupe shows the new colour over
  the current one; lift to keep it. A resting palm never picks. Option-click picks at once. Switch it off in Colour.
- **Pattern studio (rail: Pattern):** a kaleidoscope (every line turned round a centre, 2–32 segments, mirrored or not),
  a seamless repeat (Grid, Half-drop, Brick, Mirror, Hex; draw anywhere and it repeats live, across the tile edges) or
  one of the 17 wallpaper symmetries (picture tiles with friendly names). Tile size, movable centre, guides; fills
  follow the symmetry. Colourways: Shuffle colours or New palette (keeps light and dark). Save the tile (one exact
  repeat, 1024–4096 px with 150/300 DPI print sizes; upload as Basic), a 3×3 swatch PNG, or the swatch as SVG.
  Kaleidoscopes save from Tools → Draw with every segment. Saved with the drawing.
- **Keyboard:** Cmd/Ctrl+Z undo; Shift+Cmd/Ctrl+Z or Ctrl+Y redo (ignored while typing in a text field). With a selection:
  Cmd+C, Cmd+X, Cmd+V, Cmd+D, Delete, arrows nudge (Shift ×10), Escape lets go; Cmd+A selects the whole layer.
- **Speed and memory (for iPad):** watercolour, airbrush and shading pixels are painted in a pool of workers (identical
  pixels); after a zoom the paint shows at once and sharpens in the background; PNG export paints in the workers first.
  Soft paint is cached at lower resolution on screen only, within a memory budget (96 MB on iPad), and layer canvases
  exist only for layers with something on them.
- **Saving:** 0.9 s after the last change, at least every 5 s while drawing without a pause, and at once when the app goes
  to the background; a failed save (a full device) says so.
- **Device check (`?selftest`, or Help → Check this device):** tests every tool on the device with a simulated Pencil and
  reports times and results to copy or share. It uses its own storage ('-selftest'), cleared at the end.

## Saved on the device, a new canvas every start

- The photo, its placement and the drawing are saved in this browser (IndexedDB `kp-art`) as you work. Nothing is uploaded.
- **Home** saves the project and resets the start screen (no photo, drawing or undo history), so whatever starts next is
  blank. "Continue where you left off" reopens the last project; the first save of a new project keeps the one it replaces,
  shown as "or open the one before" (opening it swaps the two).
- The drawing stays with the centred picture when the iPad or phone rotates.

## Update banner

The page carries its build number (`<meta name="app-build">`) and `version.json` on the server holds the newest. The app
checks when it opens, when it comes back to the front and every 30 minutes; if the server is newer it offers "A new version
of KP Art is ready. Update". Update saves the open drawing, refreshes the browser's copy of the page (GitHub Pages lets
browsers keep it for 10 minutes; KP Art has no service worker) and reloads. `stamp-build.sh` sets a new build number (date
plus count) in both files; the git pre-commit hook runs it whenever `index.html` is committed. (The hook lives in
`.git/hooks/pre-commit`, so on a fresh clone run `./stamp-build.sh` before committing, or copy the hook back:

```sh
#!/bin/sh
if git diff --cached --name-only | grep -qx 'index.html'; then
  ./stamp-build.sh >/dev/null && git add index.html version.json
fi
```
)

Photos are processed on the device and never uploaded. Everything is in `index.html`; no build step.
Needs https for camera access (GitHub Pages provides it).

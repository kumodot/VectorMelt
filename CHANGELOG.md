# Changelog

## 0.6.2 (2026-11-09)
- **Line arrow**: *Arrow* is now a stroked arrow (shaft plus two head strokes, round caps) with *Length*, *Thickness*, *Head size* and *Head angle*. *Arrow style* switches to the filled *Block* arrow from 0.6.1; arrows in older project files stay *Block*.

## 0.6.1 (2026-11-09)
- **Multi selection**: *Shift* / *Ctrl* click on the canvas or in the layer list, box select by dragging on empty canvas (*Shift* adds), *Ctrl+A* selects all, *Esc* clears. Move, arrow nudge, scale and rotate act on the whole selection; the group gizmo scales and rotates around the group centre. *Ctrl+D* duplicates and *Delete* removes every selected layer. *Shift* while moving locks the axis.
- Pan: middle drag, right drag or *Space* + drag (left drag on empty canvas is now box select).
- **New shapes**: *Triangle*, *Cross* and *Arrow* (shaft width, head width, head length). Exact distance fields; *Corner radius* insets the shape and offsets it back, so only the convex corners round and the straight edges stay put.
- Shape buttons are icons now. *Box* starts square.

## 0.6.0 (2026-11-09)
- **Profile is now exact**: on a *Round* layer, *Profile* above 0 puts a true rolling ball fillet (radius 0.6 x *Blend*) at the junction between that layer and everything below it. Each layer's own field is rendered, the layers are combined on a grid, and the junction is closed (*Union*) or opened (*Subtract* / *Intersect*) with exact distances, only where the ball touches both edges. The letters' own corners stay as they are. The old per pixel arc, which made noise and spikes on text, is gone.
- **Fillet circles** (Preview): construction circles of the exact fillets, with the ball, its centre and the two tangent points.
- Tested on two overlapping copies of a text layer at *Profile* 0 / 0.5 / 1: no spikes; exported curves stay within 0.4 px of the shape; on straight edges the fillet radius measures 60.1 for a target of 60 at 0, 20, 40 and -30 degrees.

## 0.5.0 (2026-11-09)
- **SVG import**: drop an `.svg` on the canvas or use the new *SVG* button (*Image* accepts SVG too). The file stays a vector: it is rasterized at the layer *Resolution* (default 2048), sized from its `viewBox` (works without width / height), and saved inside `.vmelt` projects.
- **Exact fillets** panel: *Inner fillet* (rolling ball on every concave corner) and *Outer round* (every convex corner), computed on the final shape from exact distances. Clean circular arcs on text, images and SVG, where the per layer *Profile* can get noisy. Used by the preview, the vector overlay, SVG and PNG export.
- **Rings**: built from a re-distanced field, so offsets are clean inside and outside the shapes (they were noisy and deformed where layers overlap). New *Ring side*: *Outside*, *Inside* or *Both*. *Rings in SVG* toggle; the SVG gets `rings-outside` and `rings-inside` paths.
- **Blend fixes**: blend inputs are normalized by their gradient length (chained layers keep the right radius), and the *Profile* arc falls back to the soft blend near ridges (inside corners of letters, gaps between copies) instead of making spikes. Text, image and SVG layers start with *Profile* 0.
- **Legend** in the canvas corner. The SDF edge in *Outline* mode is now lavender, the exported vector stays cyan, rings orange.

## 0.4.0 (2026-11-09)
- **Text layers**: type text and melt it like any other layer. Fonts from Google Fonts or installed on your computer, with a filter (*All* / *Google* / *Installed*), search, *Other font name* (any Google family or local font by name) and *Find installed fonts* (Chrome / Edge list every installed font after asking permission). *Weight*, *Italic*, *Align*, *Letter spacing*, *Line height*, *Detail*.
- **About** dialog with shortcuts.
- Smoother image and text fields: Catmull-Rom sampling and sub-pixel edges from anti-aliasing, so Profile 1 fillets on images and text are cleaner.
- Arc fillet: gradient step tied to the fillet radius, fades to a plain union on nearly collinear edges.
- GitHub Pages layout: versioned `VectorMelt_vX.Y.Z.html`, `version.json`, `index.html` redirect.

## 0.3.1 (2026-11-09)
- Fix: tight fillets were mistaken for sharp corners, and the corner recovery pushed those nodes off the curve (spikes and loops in the vector). A corner is now kept only when its recovered point sits on the contour (within 1.5 grid px).
- Fix: the circular arc fillet could jump between nearly parallel or facing surfaces, creating seams and stray bridges. The angle is clamped so the field stays continuous. On a ring + circles test the max distance from the exported curves to the shape went from 247 px to 0.32 px.
- **Tolerance**, **Corner angle**, **Min area** and **Resolution** moved from Export to a new **Curves** panel, since they drive the live overlay as well as the export.
- Live vector overlay uses a higher resolution when idle (2.5 MP budget).

## 0.3.0 (2026-11-08)
- **Profile 1 is now a true circular arc** tangent to both edges at any corner angle, like a rolling ball / CAD fillet. The arc is solved in the oblique frame of the two field gradients, so it no longer stretches into an ellipse when edges meet at angles other than 90 degrees.
- Measured on straight edges with Blend 100 (radius 60): the fitted radius is 60.0 at 0, 20, 40 and -30 degrees, with a max deviation under 0.02 px. In v0.2.1 the same corners came out with radius 101 to 202 (stretched).

## 0.2.1 (2026-11-08)
- **Ref** button in the Add panel to load the background reference image (the Reference panel is at the bottom of the left column).

## 0.2.0 (2026-11-08)
- Per layer blend controls:
  - **Blend style**: Round or Chamfer (straight 45 degree bevel).
  - **Profile**: from the soft SDF blend (0, can bulge or flatten at shallow angles) to a true circular fillet with constant radius (1). New layers start at 0.6.
  - **Contact only**: gradient based. Reduces the blend where surfaces face each other, so shapes that only get close do not bridge or bulge; the blend grows only where they actually touch.
- **Show handles** in the vector overlay (Bezier control handles). Nodes are white when smooth and orange at corners.

## 0.1.2 (2026-11-08)
- Renamed to **VectorMelt** (formerly Vector SDF).
- New metaball chain logo, used as favicon and in the header.
- Projects are saved as `.vmelt`; old `.vsdf` files still open.
- App lives in `index.html` so the GitHub Pages link never changes. The version is shown in the header badge.

## 0.1.1 (2026-11-08)
- Default look is a light shape on a dark background (better over reference images).
- New **Export > SVG color** (default black), independent from the preview colors.

## 0.1.0 (2026-11-08)
- First version.
- Image layers: Otsu or manual threshold, auto invert, real signed distance (EDT) + smoothing, or Blur + Level mode.
- Shape layers: circle, ellipse, rounded box, capsule, star/polygon, ring.
- Per layer Union / Subtract / Intersect with its own blend radius, grow/shrink, move / scale / rotate gizmo.
- Reference image in the background with opacity, lock and transform.
- Preview modes Fill / Outline / Field and a live Bezier vector overlay with nodes.
- SVG export (marching squares, corner detection, Bezier fit, even-odd fill), offset rings, PNG export, project save/load, undo/redo.

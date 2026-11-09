<p align="center">
  <a href="https://github.com/kumodot/VectorMelt/releases/latest"><img alt="version" src="https://img.shields.io/github/v/tag/kumodot/VectorMelt?label=version&style=flat"></a>
  <img alt="license MIT" src="https://img.shields.io/badge/license-MIT-blue?style=flat">
  <img alt="platform browser" src="https://img.shields.io/badge/platform-browser-lightgrey?style=flat">
  <img alt="stack" src="https://img.shields.io/badge/stack-vanilla%20JS%20%2B%20WebGL2-orange?style=flat">
</p>
<p align="center">
  <a href="https://kumodot.github.io/VectorMelt/"><img alt="Run online" src="https://img.shields.io/badge/Run-online-4fb3ff?style=for-the-badge"></a>
  <a href="https://github.com/kumodot/VectorMelt/archive/refs/heads/main.zip"><img alt="Download" src="https://img.shields.io/badge/Download-zip-555?style=for-the-badge"></a>
  <a href="https://ko-fi.com/msouza3d"><img alt="Support" src="https://img.shields.io/badge/Support-Ko--fi-ff5e5b?style=for-the-badge"></a>
</p>

![VectorMelt](screenshots/vectormelt_banner.jpg)

VectorMelt melts black and white images, text and simple shapes together like metaballs, then gives you clean SVG. Every layer becomes a signed distance field (SDF), layers are combined with smooth booleans you tune per layer, and the result is traced into Bezier curves you can see live on top of the preview before you export.

## Screenshots

| | |
| --- | --- |
| ![Text and shapes melted together](screenshots/ui_text.png) | ![Field view with offset rings](screenshots/field_rings.png) |
| Text layer (Google or installed fonts) melted with circles, a star and a capsule. | *Field* preview with offset *Rings*, exported as extra stroked paths. |
| ![Live Bezier curves](screenshots/curves_nodes.png) | |
| Live vector overlay: the same curves the SVG export writes. | |

## Run it

- **Online**: https://kumodot.github.io/VectorMelt/
- **Local**: download the repo and double click `VectorMelt_v0.4.0.html` (or `index.html`). No install, no server. Chrome or Edge recommended (WebGL2). Google Fonts need an internet connection; everything else works offline.

## Workflow

**Layers** (left panel, applied bottom to top)
- *Image*: drop black and white images (logos, lettering, scans). Threshold (Otsu or manual), auto invert, *Smooth*, or the *Blur + Level* field.
- *Text*: type text, pick a font. Filter *All* / *Google* / *Installed*, search, *Other font name* for any Google family or local font, *Find installed fonts* (Chrome / Edge ask permission). *Weight*, *Italic*, *Align*, *Letter spacing*, *Line height*, *Detail*.
- Shapes: *Circle*, *Ellipse*, *Box*, *Capsule*, *Star* (also polygons), *Ring*.
- *Ref*: a reference image in the background with *Opacity*, never part of the shape.

**Blending** (per layer)
- *Operation*: *Union*, *Subtract* (cut holes, image into image works), *Intersect*.
- *Blend*: blend radius. *Blend style*: *Round* or *Chamfer*.
- *Profile*: 0 is the classic soft SDF blend, 1 is a true circular arc fillet tangent to both edges at any angle (like a rolling ball fillet).
- *Contact only*: shapes that are only close do not bridge or bulge, the blend grows where they actually touch.
- *Grow / shrink*, move, scale (corner handles) and rotate (top dot) on the canvas.

**Preview and curves**
- *Fill*, *Outline* and *Field* modes, *Vector overlay* with *Show nodes* (orange = corner) and *Show handles*.
- *Curves* panel: *Resolution*, *Tolerance* (how far the Bezier curves may drift from the shape), *Corner angle*, *Min area*.

**Export**
- *Export SVG*: one even-odd filled path, optional *Rings* (offset contours) as strokes, *SVG color*, optional background rect.
- *Export PNG* (transparent or with background).

### Shortcuts

| Key | Action |
| --- | --- |
| Wheel | Zoom at cursor |
| Middle drag / Space + drag / drag on empty area | Pan |
| F | Fit document |
| 1 / 2 / 3 | Fill / Outline / Field preview |
| V | Vector overlay |
| Arrows (Shift = 10 px) | Nudge layer |
| Ctrl+D / Delete | Duplicate / delete layer |
| Ctrl+Z / Ctrl+Shift+Z | Undo / redo |
| Ctrl+S | Save project |

## Projects and files

- `.vmelt` project: JSON with every layer and the images embedded. Old `.vsdf` files (Vector SDF) still open.
- Export: `.svg` and `.png`.

## Tech notes

- WebGL2 fragment shader generated from the layer stack; image and text layers are float textures sampled with Catmull-Rom.
- Image / text field: threshold, Felzenszwalb Euclidean distance transform, sub-pixel edges from anti-aliasing, Gaussian smoothing.
- Blends: polynomial smooth min (soft), an angle aware circular arc fillet solved from the two field gradients (Profile), gradient based contact falloff.
- Vector: the field is rendered on a grid on the GPU, traced with marching squares, sharp corners detected and recovered, then fitted with cubic Beziers (Schneider).

## Layout

```
index.html                 Pages entry: reads version.json, redirects to the versioned app
version.json               current version + entry file
VectorMelt_v0.4.0.html     the app (single file, no build step)
assets/logo.svg            logo / favicon
Samples/                   black and white test images
screenshots/               README images and banner
docs/                      release notes
README.md  CHANGELOG.md  LICENSE
```

## License

MIT. See [LICENSE](LICENSE).

Marcelo Souza / Kumodot.art - 2026 // @Msouza3d · [Support Marcelo Souza on Ko-fi](https://ko-fi.com/msouza3d)

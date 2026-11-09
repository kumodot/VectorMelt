## VectorMelt v0.5.0

- **SVG import**: drop an `.svg` or use the *SVG* button. It stays a vector, rasterized at the layer *Resolution*, sized from its `viewBox`, saved in `.vmelt` projects.
- **Exact fillets**: *Inner fillet* and *Outer round* on the final shape. True rolling ball arcs on text, images and SVG.
- **Rings**: clean offsets inside and outside (rebuilt from a true distance field). *Ring side* *Outside* / *Inside* / *Both*, *Rings in SVG* toggle, separate `rings-outside` / `rings-inside` paths.
- **Fix**: spikes and kinks where text layers overlap with *Profile* above 0 (inputs normalized, arc falls back to the soft blend near inside corners).
- **Legend** in the canvas: lavender = live SDF edge, cyan = exported vector, orange = rings.

Run: open `VectorMelt_v0.5.0.html`, or online at https://kumodot.github.io/VectorMelt/

## VectorMelt v0.4.0

First public release.

- **Image layers**: drop black and white images, each one becomes a real distance field (threshold + Euclidean distance transform) or a *Blur + Level* field.
- **Text layers**: Google Fonts or installed fonts, with *All* / *Google* / *Installed* filter, search and *Find installed fonts*.
- **Shapes**: circle, ellipse, rounded box, capsule, star / polygon, ring.
- **Smooth booleans per layer**: *Union*, *Subtract*, *Intersect*, each with its own *Blend*, *Blend style* (Round / Chamfer), *Profile* (soft SDF blend to a true circular arc fillet) and *Contact only*.
- **Reference image** in the background with opacity.
- **Live vector overlay** with nodes and handles, **SVG export** with offset rings, PNG export, `.vmelt` projects, undo / redo.

Run: open `VectorMelt_v0.4.0.html`, or online at https://kumodot.github.io/VectorMelt/

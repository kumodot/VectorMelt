## VectorMelt v0.6.6

- **Profile only touches the junction**: a layer's own notches (like the inner V of a line arrow) are no longer filled and bulged when they sit near the junction. A fillet is kept only where its rolling ball touches both the layer and what is below it.
- **Self affect** checkbox per layer (under *Profile*) brings the old behaviour back for that layer.
- **Faster edits with Profile**: the exact pipeline caches the result after each layer, so changing one layer only recomputes from that layer up.

Run: open `VectorMelt_v0.6.6.html`, or online at https://kumodot.github.io/VectorMelt/

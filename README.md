# OMSI Nightmap Tool

A single-file browser tool for generating **nightmap textures** for the OMSI bus simulator.
Load a daytime facade, draw rectangular "rooms," mask the window frames and mullions,
randomize illumination, and export the nightmap ready to drop into OMSI's `night/` folder
beside the original.

No build step, no server, no dependencies — open `omsi_nightmap_tool.html` in any
modern browser.

## What it does

Four-step pipeline, walked through in-app:

| Step | What you do | Output |
| ---- | ----------- | ------ |
| **0 — Draw Rooms** | Load a facade, drag room boxes | Locked room geometry |
| **1 — Window Masking** | Assist or hand-paint which frames/glass to ignore | Binary illumination mask |
| **2 — Randomized Illumination** | Tune lit-room ratio, brightness, glow | Previewable nightmap |
| **3 — Export** | One click to write `<name>.png` next to the source | Ready-to-drop-in OMSI files |

Extras shipped with the pipeline:

- **2D / 3D split preview** — orbit the facade and watch the lit rooms glow.
- **Editable `.nmt` sessions** — save the texture, every box, and every setting to a
  single file you can re-open later or hand to a collaborator. The file is plain text;
  the `profile_json` section is human-readable JSON, the `texture_data` section is the
  original image bytes (base64).
- **Binary mask export** — download the B/W mask separately if you want to bring it
  into another tool.

## Supported inputs

| Format | OMSI | Browser | Supported |
| ------ | :--: | :-----: | :-------: |
| PNG    |  yes |   yes   |   **yes** |
| JPG / JPEG | yes |   yes   |   **yes** |
| BMP    |  yes |   yes   |   **yes** |
| WebP   |  no  |   yes   |   **no**  |
| TGA / TIFF | yes |   no   |   **no**  |
| GIF / SVG / ICO | varies | varies | **no** |

The set is deliberately the intersection of what OMSI can load and what any modern
browser can decode. Files outside that list are rejected with a message in the command
log rather than producing a silent blank canvas.

## Running it

```
# Just open the file
omsi_nightmap_tool.html
```

That's it. Chrome / Edge / Firefox / Safari all work. Some browsers will refuse to
serve a file with `file://` against `Image()` operations for cross-origin textures;
if you ever need to bundle one as a real `.zip` with a sample, serving over `http`
avoids any quirk:

```
# Optional, if you want a tiny static server
python -m http.server 8000
# then open http://localhost:8000/omsi_nightmap_tool.html
```

## File layout

This repo intentionally ships one file. All state, all UI, all logic live in
`omsi_nightmap_tool.html`. Open it, use it, archive it.

## Credits

Released by HC2105 @ TJ x HC Studio, 2026.

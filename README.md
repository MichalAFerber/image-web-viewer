# Image Viewer

A **single-file image viewer for the whole gamut of formats** — from everyday
PNG/JPEG to the ones few web viewers handle, like **TIFF, TGA, QOI, PCX,
Netpbm (PPM/PGM/PBM), farbfeld and DDS**. Zoom, pan, inspect the metadata, and
export anything to PNG. It's a **viewer** — no accounts, no uploads. Everything
runs locally in your browser.

🔗 **Live:** <https://image-viewer.us/>

![Single file](https://img.shields.io/badge/build-single%20HTML%20file-success) ![No build step](https://img.shields.io/badge/build%20step-none-success) ![License](https://img.shields.io/badge/license-MIT-blue)

> Part of the **[File Viewer](https://file-viewer.us/) family** — HTML, Markdown,
> ePUB, PDF, Data, DOCX, Sheets, EML, PPTX, Log, Cert, PUB and Image each have
> their own dedicated viewer. Use the **☰ menu** in the header to jump between them.

## Supported formats

**Rendered by the browser** (fast, native): PNG, JPEG, GIF (animated), WebP,
AVIF, SVG, BMP, ICO. HEIC/HEIF display where the browser supports them (e.g.
Safari).

**Decoded in-page** (built-in, dependency-light decoders):

| Format | Notes |
| --- | --- |
| **TIFF / TIF** | Multi-page, uncompressed · LZW · PackBits · CCITT G3/G4 · JPEG |
| **TGA (Targa)** | Uncompressed & RLE, 8/16/24/32-bit, color-mapped |
| **QOI** | The "Quite OK Image" format |
| **PCX** | RLE, 1/4/8/24-bit, palette & true-color |
| **Netpbm** | PPM · PGM · PBM (ASCII & binary) |
| **farbfeld** | suckless 16-bit RGBA |
| **DDS** | Uncompressed + DXT1/DXT3/DXT5 (BC1/2/3) |

Formats that require a WebAssembly codec — **JPEG XL** and camera **RAW** — aren't
decoded here (the viewer keeps a strict, eval-free Content-Security-Policy); export
them to PNG/TIFF first.

## Features

- 🔍 **Zoom & pan** — wheel to zoom, drag to pan, pinch on touch, double-click to
  toggle fit ↔ 100%. Fit, actual-size and zoom controls in a floating toolbar.
- 🧊 **Transparency checkerboard** — see the alpha channel on any background.
- 🧾 **Metadata panel** — format, dimensions, bit depth, color type, transparency,
  compression, page count, and **EXIF** (camera, exposure, ISO, focal length,
  orientation) for JPEG/TIFF.
- 📄 **Multi-page** — step through TIFF pages.
- 💾 **Export to PNG** — turn any decoded format (TIFF, QOI, DDS…) into a PNG.
- 🪶 **One file, no build, no dependencies** — works offline, even from `file://`.
- ☰ **Family menu** · 🫥 **auto-hiding header** · 🎨 **pick any background color**.
- 🔒 **Local only** — your images never leave your device.
- 📊 **Privacy-friendly analytics** — self-hosted, cookieless [Plausible](https://plausible.io/).

## Quick start

**Just open it.** Download [`index.html`](index.html), double-click it — no
server, no build, no internet needed.

```sh
python3 -m http.server 8080   # then open http://localhost:8080
```

## Deploy to Cloudflare Pages

Connect the repo (**Workers & Pages → Create → Pages → Connect to Git**),
framework preset **None**, build command blank, output directory `/`. The
[`_headers`](_headers) file applies a strict CSP automatically. Add the custom
domain **image-viewer.us** under the project's Custom domains tab.

## How it works

Everything is in [`index.html`](index.html). Browser-native formats render
through an `<img>` element; everything else is decoded to pixels by small
in-page decoders and drawn to a `<canvas>`. TIFF decoding uses the bundled
[UTIF.js](https://github.com/photopea/UTIF.js) (MIT); the TGA, QOI, PCX, Netpbm,
farbfeld and DDS decoders are original to this project. The CSP stays strict
(`default-src 'none'`, no `eval`, no WASM); `img-src` allows `blob:` so native
images can be shown.

## Credits

Bundled: [UTIF.js](https://github.com/photopea/UTIF.js) (MIT) for TIFF. The other
decoders and the UI are original to this project. Icon by the author. Analytics
by [Plausible](https://plausible.io/). Headings use a subset of
[JetBrains Mono](https://github.com/JetBrains/JetBrainsMono) (SIL OFL-1.1).

## License

[MIT](LICENSE) © 2026 Michal Ferber, aka **TechGuyWithABeard**.

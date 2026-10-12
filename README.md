# qrpic

Client-side QR tools. Plain static files, no build step: serve the repo root (e.g. `python3 -m http.server`) and open `/`.

## Picture QR (`/picture-qr/`)

Embeds a picture inside a QR code that still scans. Everything runs in the browser: the image never leaves the page, and a Content-Security-Policy blocks all network requests.

- Each QR module is drawn as a 3×3 block of pixels. The centre pixel carries the real data bit; the other eight are free.
- Function patterns (finders, separators, timing, alignment, format/version info) are solid 3×3 blocks.
- Pass 1 fixes every data centre pixel and spreads its error evenly over its free neighbours. Pass 2 runs Floyd–Steinberg dithering over the remaining free pixels.
- 4-module quiet zone. Export as PNG (nearest-neighbour scaling) or SVG.
- Every render is decoded with jsQR, and a badge shows whether it scans. Always test with a phone before printing.

Until you choose a picture it renders a plain QR code.

Technique credit: [andrewt.net — dithered QR codes](https://www.andrewt.net/dithered-qr-codes/wtf/).

## Third-party code

Vendored under `vendor/` (see `vendor/README.md` for versions and checksums):

- [qrcode-generator](https://github.com/kazuhikoarase/qrcode-generator) 2.0.4, © Kazuhiko Arase, MIT — `vendor/qrcode-generator/LICENSE`
- [jsQR](https://github.com/cozmo/jsQR) 1.4.0, Apache-2.0 — `vendor/jsqr/LICENSE`

"QR Code" is a registered trademark of DENSO WAVE INCORPORATED.

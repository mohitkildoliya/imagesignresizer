# Photo & Sign Resizer Tool (v1.2)

![Version](https://img.shields.io/badge/version-v1.2-22c55e?style=flat-square)
![Privacy](https://img.shields.io/badge/network-zero%20CSP%20locked-ff9933?style=flat-square)
![Dependencies](https://img.shields.io/badge/dependencies-zero-ff9933?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-blue?style=flat-square)

A **100% offline, zero-network, single-file web utility** built with Vanilla JavaScript and the HTML5 Canvas API. Designed for strict online application portals, it resizes photos and signatures, locks output files to exact kilobyte (KB) ranges, injects custom DPI metadata headers, and whitens signature paper—**entirely inside local volatile RAM**.

🔗 **Live Tool:** [https://mohitkildoliya.github.io/photo-sign-resizer/](https://mohitkildoliya.github.io/photo-sign-resizer/)

---

## 🔒 Zero-Trust Privacy Architecture

Most "free online photo resizers" upload your passport photo, signature, full name, and camera metadata to third-party servers. This tool makes data exfiltration impossible by design:

* **Browser-Enforced Network Kill-Switch:** Hardcoded with a strict Content Security Policy (`default-src 'none'; connect-src 'none'; form-action 'none'`) that blocks all outbound `fetch`, `XMLHttpRequest`, WebSocket, and external asset requests at the browser engine level.
* **Automatic EXIF & GPS Stripping:** Re-encodes raw pixel data from an HTML5 Canvas, destroying embedded smartphone GPS coordinates, device serials, and timestamps before generating a clean file header.
* **Zero External Dependencies:** No CDNs, no external fonts, no analytics trackers, and no cookies or `localStorage` persistence. Works offline directly via `file://` or hosted statically.

---

## ⚡ Key Engineering Features

1. **Modular "Tick-What-You-Need" Workflow**
   * Enable only the operations you need: **Resize/Crop**, **Compress to Target KB**, **Change Format**, or **Signature & Photo Extras**.
2. **Exact-KB Compression Engine (Binary Search + Byte Padding)**
   * Runs an 11-step binary search across `canvas.toBlob()` quality levels (`0.02` to `0.98`) to maximize visual sharpness while staying strictly under your `Max KB` limit.
   * **Underflow Protection:** If a small image (like a `140×60 px` signature) is lighter than your `Min KB` even at 98% quality, the engine injects valid JFIF Comment (`0xFF 0xFE`) byte segments before the End-of-Image (`0xFF 0xD9`) marker to hit the exact target KB window without corrupting the file.
3. **Raw JFIF APP0 DPI Header Injection**
   * Converts physical units (`cm`, `mm`, `inch`) to exact pixel dimensions and overwrites the 16-bit big-endian X/Y density bytes (`offset 13–17`) in the JPEG header (`72` to `1200` DPI) so strict portal validators read the exact required DPI.
4. **Multi-Step Bicubic Downsampling Pyramid**
   * Prevents jagged aliasing when shrinking 12 MP–50 MP smartphone photos down to passport dimensions by stepping down resolution in iterative 50% passes.
5. **Smooth Anti-Aliased Signature Paper Whitener**
   * Uses a custom luminance transition ramp (`0.299R + 0.587G + 0.114B`) to turn shadowy, grey smartphone photos of paper signatures into crisp dark ink on a pure `#FFFFFF` background without jagged pixel edges.
6. **Auto-Fitting Name & Date Photo Banner**
   * Optionally draws a compliant 18%-height bottom white banner with bold centered text that dynamically scales down font size so long candidate names never clip off the edges.
7. **Monkeytype-Inspired Adaptive UI**
   * High-contrast saffron terminal aesthetic that automatically switches between Carbon Dark Mode and Warm Paper Light Mode based on the user's OS preference (`prefers-color-scheme`).

---

## 🚀 Usage (Online & Offline)

* **Use Online:** Open the [GitHub Pages live link](https://mohitkildoliya.github.io/photo-sign-resizer/). Once loaded, you can turn off Wi-Fi/mobile data and use it completely offline.
* **Use 100% Offline Locally:** Download `index.html` from this repository and open it in any mobile or desktop browser.
* **Embed on Any Website / Blog:**
  ```html
  <iframe src="[https://mohitkildoliya.github.io/photo-sign-resizer/](https://mohitkildoliya.github.io/photo-sign-resizer/)" width="100%" height="720px" style="border:none; border-radius:16px;"></iframe>
  

# 📄 PDF Builder

A single-page web app for turning images and PDFs into a polished PDF — combine, reorder, rotate, draw, sign and annotate.

**Everything runs in your browser.** No files are ever uploaded to a server, which makes it safe for private documents.

👉 **[Open the app](https://inclusive46192.github.io/ImageToPdf/)**

---

## Features

| | |
|---|---|
| 📥 **Add anything** | Drag & drop images (PNG/JPG/…) or existing PDFs. PDF pages are converted into editable pages automatically. |
| 🔀 **Reorder** | Drag page thumbnails to change their order. |
| ⟳ **Rotate** | Rotate any page in 90° steps — annotations rotate along with it. |
| ✏️ **Draw** | Freehand drawing with adjustable colour and pen width. Works with mouse, trackpad, touch and stylus. |
| ✍️ **Sign** | Draw a signature on a signature pad, or upload a photo/scan of one. Drag to position and resize proportionally. |
| 🅣 **Text** | Place text boxes anywhere, type into them, and set font size and colour. |
| ⚙️ **Quality control** | Choose JPEG (with a quality slider) or lossless PNG, cap the resolution, and see a live file-size estimate. |
| 💾 **Export** | Download everything as a single PDF. |

## Usage

1. Open the app and drop in some images or a PDF.
2. Drag the thumbnails to get the order you want.
3. Click **✎ Edit** on a page to draw, sign, or add text.
4. Adjust the **Output quality** settings to trade file size against sharpness.
5. Click **Export PDF**.

### Notes on the editor

- Switch between **🖱 Select** (move text and signatures) and **✏️ Draw** (draw on the page).
- The **Pen** field sets the drawing width; the **Font** field sets the font size of the currently selected text box. Click a text box to select it (it stays selected until you click another one), then adjust **Font** or **Color**.
- Hover a text box or signature to reveal its ✕ delete button; signatures also get a corner handle for resizing.
- Click **Save changes** to apply your edits to the page.

## Output quality

| Setting | Effect |
|---|---|
| **JPEG** | Much smaller files. The quality slider trades sharpness for size. Best for photos and scans. |
| **PNG** | Lossless and crisp, but produces considerably larger files. Best for screenshots, diagrams and text. |
| **Max resolution** | Caps each page's longest edge. *Medium (1754 px)* ≈ A4 at 150 DPI and suits most uses; *High (2480 px)* ≈ A4 at 300 DPI for printing. |

Pages are written at 150 DPI so they come out at sensible physical dimensions.

## Running it locally

No build step and nothing to install. `index.html` holds all of the app's own code; the two PDF libraries sit alongside it in `vendor/`, so keep the folder together. Either:

- Open `index.html` directly in your browser, or
- Serve the folder, e.g. `python -m http.server 8000`, then visit <http://localhost:8000>.

## Hosting your own copy

The app is fully static, so any static host works. To use GitHub Pages: go to **Settings → Pages**, set the source to the `main` branch and the `/ (root)` folder.

## How it works

- **[pdf-lib](https://pdf-lib.js.org/)** assembles and writes the final PDF.
- **[pdf.js](https://mozilla.github.io/pdf.js/)** renders pages of uploaded PDFs so they can be edited like images.

Each page is drawn to a `<canvas>` with its rotation, drawings, signatures and text baked in, then embedded into the PDF. Annotation coordinates are stored relative to the page (0–1) so they stay correctly positioned at any export resolution.

Both libraries are vendored in `vendor/`, so the app works fully offline — no CDN and no network requests at all once you have the folder.

## Limitations

- Pages are exported as images, so text in the finished PDF is **not selectable or searchable**.
- Text from an imported PDF is rasterised rather than preserved as text.
- Very large or numerous pages take longer to export and use more memory.

## Browser support

Works in current versions of Chrome, Edge, Firefox and Safari.

## License

[MIT](LICENSE)

# Luna import

A Figma development plugin that builds a page from a Luna **design snapshot**, with the page's real pictures.

Why a plugin: Figma refuses pictures on every clipboard route (an image fill needs a hash Figma already holds, SVG paste drops `<image>`, HTML to design is flat). The Plugin API can place them: `figma.createImage(bytes)`, then an image fill. So Luna writes the snapshot to a folder, and this plugin reads that folder.

## Install (once)

1. In Luna: Settings, General, **Show the plugin folder**. (Or take this folder from the Luna source: `tools/figma-plugin/luna-import`.)
2. In the **Figma desktop app**, open a Design file and choose **Plugins, Development, Import plugin from manifest...**
3. Pick `manifest.json` in that folder. "Luna import" now sits under Plugins, Development.

The plugin needs no network access (its manifest says so): it reads only the folder you choose.

## Use (copy and paste)

1. In Luna, open the page and press **Ctrl+Shift+F** (Save design snapshot). Luna also puts the page on the clipboard: layers for Figma's own paste, and, as plain text, the whole snapshot with its pictures.
2. In Figma: **Ctrl+Alt+P** (Mac: Cmd+Option+P), Figma's "Run last plugin" (third-party sources agree on this shortcut; the first time, use **Plugins, Development, Luna import**).
3. The window opens with a big box focused: press **Ctrl+V**. The page is imported at once (tick "Ask before importing what I paste" to look at the summary and the options first).

Notes:

* After step 1 the clipboard holds a **large piece of text** (a few MB; up to 64 MB for a very large page). Pasting it anywhere else, such as a text field, will be slow or messy; paste into the plugin window. Copy something else when you are done.
* Pasting into the Figma canvas itself still gives the layers without pictures (that is Luna's other clipboard format).
* If Figma lets the window read the clipboard, it imports as soon as it opens; if not, Ctrl+V does the same.
* Very large pictures are left out of the copy (the window says how many; "Choose the snapshot folder" brings everything). Pictures a page serves as WebP/AVIF are converted to PNG/JPEG; over 4096 px they are scaled down.
* Without the clipboard: **Choose the snapshot folder** (or drop it on the window) and pick `Documents\Luna\Snapshots\latest`, which Luna keeps current.

Options:

| option | what it does |
|---|---|
| Ask before importing what I paste | off: a paste imports at once |
| Page name | a new Figma page with this name; empty puts the frame on the current page |
| Use auto layout where the page proves it | a flex row or column becomes an auto layout frame **only** when auto layout would put every child within 1 px of where the page had it (spacing, padding and alignment are measured, not guessed); everything else stays at exact positions |
| Images | off: every picture is a grey box (a fast structure-only import) |
| Scale | scales the whole frame (1 = the page's own pixels) |

## What you get

* One top-level frame, the size of the page (at the scroll position of the snapshot), layers in paint order, named by meaning (`Header`, `Nav / Work`, `Hero`, `Button / Start a project`, `Image / alt text`, `Card`, `Text / first words`, `Video / title`), needless wrappers gone, runs of three or more equal siblings grouped (`Cards`).
* **Pictures as image fills**: `<img>`, CSS background images (several layers, in order, with gradients), canvas bitmaps, video frames or posters. `object-fit`/`background-size` become Fill (cover), Fit (contain) or Stretch; tiled backgrounds become a tiled fill; offsets (`object-position`, `background-position`) become a rectangle placed exactly, inside a clipping frame. Rounded corners are kept. A picture used twice is imported once.
* Text as text: one layer per run, a wrapped paragraph as one paragraph (with the browser's line breaks kept when the page's font is not in Figma), line height, letter spacing, alignment, underline, shadows, links.
* **CSS grids** become Figma grid frames (rows, columns, gaps, padding, track sizes, each child's cell, span and alignment) **only** when a simulation of Figma's grid puts every child within 1 px of where the page had it. Equal tracks that fill the box are `1fr` each, other tracks are fixed at the page's pixel size. Grids with subgrid, dense auto-flow, overlapping items, item margins, or `justify-content` that moves the tracks stay plain frames at exact positions (the window counts them). Layers that are not grid items (backgrounds, absolute boxes) stay beside an inner grid frame.
* Fills (solid, linear, radial and conic gradients), borders (per side), corner radii, shadows (inner and drop), blur, opacity, blend modes, clipping, rotation of simple boxes.
* Inline SVG and icons as real vectors.

## Icons, wrapped runs and checks

* **Icon fonts** (Font Awesome and the like): Figma has no such font, so the character the browser drew is kept by Luna as a picture and imported as a layer named `Icon / U+XXXX` (accordion chevrons, arrows). Needs a snapshot taken with this Luna; older snapshots import those characters as text in a missing font.
* **A run that wraps** (a bold phrase that starts at the end of a line): its lines begin in different places, so each line is its own text layer, placed where the browser drew it; it is no longer one paragraph drawn over the line before.
* **Text width**: a page font Figma lacks is drawn in another face; letter spacing is nudged (at most 6% of the size) until the line is as wide as the browser drew it.
* **Layout is checked**: when the last child of an auto layout or grid frame is in, the plugin reads back sizes and positions. If Figma laid it out differently from the plan (a collapsed picture, a moved cell), that frame goes back to plain frames at the page's positions and the summary says `grid-fallback` / `layout-fallback`.
* A grid cell the grid fills is set to FILL rather than aligned, and a frame the grid fills never hugs that axis (this keeps carousel pictures full height).

## Lazy pictures, scaled boxes, runs of one sentence

* **Lazy pictures**: a picture that has not loaded has no size (an img shows the height of its alt text), so cards showed 24 px strips. Luna now gives the page what a visitor gives it before it reads it: lazy pictures are made eager, the page is scrolled through once and put back, and the pictures are waited for (6 s at most). Snapshots from older Luna builds can still contain such strips: the import warns `picture-not-loaded` / `picture-missing`; take the snapshot again.
* **Scaled boxes**: a picture under a non-uniform scale (`scaleY(.3)` on a closed card) is drawn as the page shows it: cropped in the box it has without the scale, then scaled with it (whole picture squashed), not cropped to the scaled box. Text and boxes under such a scale stay upright at their scaled rectangles.
* **Runs of one sentence** (regular text, a bold phrase, regular text again in one paragraph): every line that shares its line with another run is its own layer at the browser's position, and a line followed by a run keeps the space as a trailing space, so the words cannot run into each other in a wider fallback font. Such paragraphs are no longer one editable text layer.

## Limits (what the import cannot do)

* Fonts are matched to what Figma has (Inter, Roboto, Roboto Mono, Playfair Display, Merriweather, Lora, Open Sans, DM Sans, Arial, Helvetica, Times New Roman, Courier New and every family in your file's font list); anything else falls back to Inter, Roboto Mono or Merriweather, and the window says which. Widths differ by a few percent.
* WebGL canvases and cross-origin video are blank in the snapshot; they become named empty layers.
* CSS masks, `clip-path`, `filter` other than blur, `background-blend-mode` and hover or animation states are not captured.
* Animated GIFs and WebP: the first frame, as the browser gave it.
* Rotated boxes that have children stay upright (their children's boxes are already the rotated bounding boxes).
* Sticky and fixed layers stay at their positions (fixed and sticky are pinned only for direct children of the page frame).
* Pictures over 400 MB in all (decoded) are left as grey boxes, and a page over 12,000 layers is cut at a height; the window says so.

Source: `tools/figma-plugin` in the Luna repository (`src/` builds `code.js`: `node bundle.js`).

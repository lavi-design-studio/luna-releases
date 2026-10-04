# Third-party notices

## Search, by Office Commun

Luna's structure (one field, tabs down the side or across the top, pins, the
metrics) and parts of its behaviour are adapted from
[Search](https://github.com/driceroland/Search). In particular:

- `src/Scripts/picker.js` — adapted from the element picker in `Curtain.swift`
- `src/Scripts/reader.js` — the article heuristic from `Reader.swift`
- `src/Core/Shield.cs` — the ad and tracker host list from `Shield.swift`
- `src/Core/Crx.cs` — the CRX3 verification approach from `Crx.swift`

"Search" and its icon are Office Commun's; Luna uses neither.

```
MIT License

Copyright (c) 2026 Office Commun

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

## Mercury OS, by Jason Yuan

Luna's design learns from the principles set out in the art direction of
[Mercury OS](https://www.mercuryos.com/) (2019) — selective contrast, things lit
from within at night, hierarchy by size, instant answers and motion that settles.
Its colours, layouts and visuals are Luna's own; no code, images, fonts or
colour values from Mercury are used.

## ABC Areal, by Dinamo

Luna asks Windows for [ABC Areal](https://abcdinamo.com/typefaces/areal) when it
is installed and falls back to Segoe UI Variable otherwise. The font files are not
part of Luna and must not be added to it: Dinamo's free fonts license does not
allow sharing them or putting them in public repositories.

## Microsoft Edge WebView2

`Microsoft.Web.WebView2` (the SDK) is distributed by Microsoft under the BSD-style
license in its NuGet package. The WebView2 runtime itself — the Chromium the pages
run on — ships with Windows 11 and is updated by Windows.

## liquidGL, by NaughtyDuk

The way Liquid Glass's panes bend what is under them (`src/UI/Optics.cs`,
`Optics.Glass` and `Optics.Lens`: the bevel's refraction along the rounded
rectangle's normal, the colour fringing and the two highlights) and the
panes' drop shadow (`src/UI/GlassEdge.cs`) are adapted from the fragment
shader and styles of [liquidGL](https://github.com/naughtyduk/liquidGL).

```
MIT License

Copyright (c) NaughtyDuk

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

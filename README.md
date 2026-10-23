# dream_propaganda

OPERATION: BUILD SOMETHING, DreamWeave's recruitment posters, drawn by
[Jess](https://github.com/DreamWeave-MP/jess). The package is `org.dreamweave.dream-propaganda`;
its command is `dream-propaganda`.

Ten posters from one file of copy, two logos, and installed fonts. Every shape is a primitive
(circles, polygons, strokes, rectangles), every letter is set from the font's own outlines, and
the logos are the supplied files, never redrawn: the founder's S3 logo on P01 alone, and
DreamWeave's as the signature of the rest. No image model and no image service: the pixels come
from [Magick](https://dreamweave-mp.github.io/magick/), Jess's raster toolkit based on ImageMagick,
and [truetype](https://dreamweave-mp.github.io/truetype/), both JSL running in Jess. The same inputs make the same bytes.

## What it needs

- Jess.
- Its two dependencies, `org.dreamweave.magick` 0.1.3 and `org.dreamweave.truetype` 0.1, which
  `jess.lock` pins from their sites and `jess workspace sync` fetches.
- The S3 logo and the DreamWeave logo, PNGs. Neither is in this repository; the build reads them
  from where you keep them.
- Noto Sans and Noto Sans Mono, installed: `NotoSans-CondensedBlack.ttf`, `NotoSans-Medium.ttf`
  and `NotoSansMono-Bold.ttf`, looked for in `/usr/share/fonts/google-noto` (Fedora's
  `google-noto-sans-fonts` and `google-noto-sans-mono-fonts`). They're read where they're
  installed and never copied here.
- Oxanium SemiBold, for the banner alone: `Oxanium-SemiBold.ttf` in `~/.local/share/fonts`, or
  named with `--font`.

## Building

From this folder:

```sh
jess workspace sync --locked
jess workspace run --trusted dream-propaganda -- \
  --logo path/to/s3logo.png --dreamweave-logo path/to/DWLogo.png
```

That builds all ten into `posters/`. The command takes:

| Option | What it does |
| --- | --- |
| `--poster ID` | Build this poster (repeatable); all of them without it |
| `--logo PATH` | The S3 logo; without it, `DREAM_PROPAGANDA_LOGO`, else `Pictures/s3logo.png` under `HOME` |
| `--dreamweave-logo PATH` | The DreamWeave logo; without it, `DREAM_PROPAGANDA_DREAMWEAVE_LOGO` |
| `--out-dir DIR` | Where the posters go (`posters`) |
| `--size WxH` | Another size of the same 2:3 shape, such as `600x900` |
| `--edition NAME` | An edition's copy, into `DIR/NAME` |
| `--debug-layout` | Also the layout views, into `DIR/debug` |
| `--no-preview` | Skip the 360 pixel previews in `DIR/preview` |
| `--manifest PATH` | Copy from another `posters.toml` |
| `--editions PATH` | Editions from another file |
| `--font-dir DIR` | Where the fonts are |

`dream-propaganda check` reads the copy and the editions and stops there, and `-- --help` lists
the options.

`--trusted` grants what the target declares, and that is all it declares: `filesystem.read` (the
copy, the logos, the fonts), `filesystem.write` (the posters), `process.environment` (finding
the logos without their flags), and `process.stdio`. It runs no other program and opens no connection.
`jess package inspect .` lists them.

The packed JPK, a release's archive, builds the same bytes:

```sh
jess package run --trusted --package-path .jess/packages dream_propaganda.jpk \
  --logo path/to/s3logo.png --dreamweave-logo path/to/DWLogo.png
```

## What a build writes

For each poster, `<id>-<slug>.png` and `<id>-<slug>.txt`, its alt text; for the build,
`manifest.json`: the campaign, the edition, the size, the palette, the renderer's version and
Jess's, and the SHA-256 of every input (the copy, the editions, each logo, each font, with the
fonts' names and versions) and every poster. It names the logos by their file names, never by
where they were. A build of some posters keeps what an earlier build from the same inputs recorded of the
others.

## The banner

`dream-propaganda banner` draws jess's social preview, the image GitHub shows for the repository:
GitHub's 1280 by 640, the word `jess` in Oxanium SemiBold in the site's purple (`#cf9bff`) on its
near-black (`#07060a`), and nothing else. The word is centered on the body of its letters, so the
j's dot and tail hang off the center, and kept inside the middle four fifths of the canvas, where
the sites that crop a preview squarer than GitHub does still show it.

```sh
jess workspace run --trusted dream-propaganda -- banner
```

That writes `banners/jess-github.png`, its alt text beside it, and `banners/manifest.json` with
the font's digest and the PNG's. It takes `--out PATH`, `--size WxH` (1280x640 scaled), and
`--font PATH`, the Oxanium SemiBold TTF, read from `~/.local/share/fonts` without it. The font is
the SIL Open Font License's, read where it's installed and never shipped; the suites set the
banner in Noto Sans instead, so a machine without Oxanium still tests it.

## The copy

`posters.toml` is the copy, word for word as approved. The build never rewrites it: copy that
doesn't fit its box at its smallest size stops the build with what it measured, and so does
anything that would land outside the 72 pixel safe area. Each voice has its template:
`founder-emblem` (the S3 logo as the hero, the headline over it and the mission under it), `collective-builders` (anonymous builders at shared
work, at most 25 primitives), and `doctrine-diagram` (type over a diagram). The copy is checked
before anything is drawn: ten posters, one founder, five collective, four doctrine, every field
there, every voice drawn by its own template, every destination a URL.

`editions.toml` holds editions, copy replaced field by field for other venues: `safe` swaps the
calls to action and the headline that swear for the alternates the campaign documents give, and
refuses to build while any field still holds a word it forbids; `newcomer` gives P03 its gentler
copy.

`docs/STYLE_GUIDE.md` is the campaign's visual contract.

## Testing

```sh
jess workspace test
jess package check --package-path .jess/packages .
```

The suites draw with stand-in logos of their own and set copy in the installed Noto Sans.

## License

MIT OR Apache-2.0. The fonts are the SIL Open Font License's and aren't part of this package; the
logos are their owners'.

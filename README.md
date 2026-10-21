# dream_propaganda

OPERATION: BUILD SOMETHING, DreamWeave's recruitment posters, drawn by
[Jess](https://github.com/DreamWeave-MP/jess). The package is `org.dreamweave.dream-propaganda`;
its command is `dream-propaganda`.

Ten posters from one file of copy, the founder's S3 logo, and installed fonts. Every shape is a
primitive (circles, polygons, strokes, rectangles), every letter is set from the font's own
outlines, and the logo is the supplied file, screened onto the poster, never redrawn. No image
model and no image service: the pixels come from [Magick](https://dreamweave-mp.github.io/magick/),
Jess's raster toolkit based on ImageMagick, and [truetype](https://dreamweave-mp.github.io/truetype/),
both JSL running in Jess. The same inputs make the same bytes.

## What it needs

- Jess.
- Its two dependencies, `org.dreamweave.magick` 0.1.3 and `org.dreamweave.truetype` 0.1. Until both
  are published, name their checkouts with `--package`, as below.
- The S3 logo, a PNG. It isn't in this repository; the build reads it from where you keep it.
- Noto Sans and Noto Sans Mono, installed: `NotoSans-CondensedBlack.ttf`, `NotoSans-Medium.ttf`
  and `NotoSansMono-Bold.ttf`, looked for in `/usr/share/fonts/google-noto` (Fedora's
  `google-noto-sans-fonts` and `google-noto-sans-mono-fonts`). They're read where they're
  installed and never copied here.

## Building

From this folder, with Magick and truetype checked out beside it:

```sh
jess package run --trusted --package ../magick --package ../truetype . --logo path/to/s3logo.png
```

That builds all ten into `posters/`. The command takes:

| Option | What it does |
| --- | --- |
| `--poster ID` | Build this poster (repeatable); all of them without it |
| `--logo PATH` | The logo; without it, `DREAM_PROPAGANDA_LOGO`, else `Pictures/s3logo.png` under `HOME` |
| `--out-dir DIR` | Where the posters go (`posters`) |
| `--size WxH` | Another size of the same 2:3 shape, such as `600x900` |
| `--edition NAME` | An edition's copy, into `DIR/NAME` |
| `--debug-layout` | Also the layout views, into `DIR/debug` |
| `--no-preview` | Skip the 360 pixel previews in `DIR/preview` |
| `--manifest PATH` | Copy from another `posters.toml` |
| `--editions PATH` | Editions from another file |
| `--font-dir DIR` | Where the fonts are |

`dream-propaganda check` reads the copy and the editions and stops there. `jess package run`
takes its own `--help`, so the command's is `-- --help`.

`--trusted` grants what the target declares, and that is all it declares: `filesystem.read` (the
copy, the logo, the fonts), `filesystem.write` (the posters), `process.environment` (finding the
logo without `--logo`), and `process.stdio`. It runs no other program and opens no connection.
`jess package inspect .` lists them.

The packed JPK builds the same bytes:

```sh
jess pack -o dream_propaganda.jpk .
jess package run --trusted --package magick.jpk --package truetype.jpk dream_propaganda.jpk --logo path/to/s3logo.png
```

## What a build writes

For each poster, `<id>-<slug>.png` and `<id>-<slug>.txt`, its alt text; for the build,
`manifest.json`: the campaign, the edition, the size, the palette, the renderer's version and
Jess's, and the SHA-256 of every input (the copy, the editions, the logo, each font, with the
fonts' names and versions) and every poster. It names the logo by its file name, never by where
it was. A build of some posters keeps what an earlier build from the same inputs recorded of the
others.

## The copy

`posters.toml` is the copy, word for word as approved. The build never rewrites it: copy that
doesn't fit its box at its smallest size stops the build with what it measured, and so does
anything that would land outside the 72 pixel safe area. Each voice has its template:
`founder-emblem` (the S3 logo as the hero), `collective-builders` (anonymous builders at shared
work, at most 25 primitives), and `doctrine-diagram` (type over a diagram). The copy is checked
before anything is drawn: ten posters, two founder, four collective, four doctrine, every field
there, every voice drawn by its own template, every destination a URL.

`editions.toml` holds editions, copy replaced field by field for other venues: `safe` swaps the
calls to action and the headline that swear for the alternates the campaign documents give, and
refuses to build while any field still holds a word it forbids; `newcomer` gives P03 its gentler
copy.

`docs/STYLE_GUIDE.md` is the campaign's visual contract.

## Testing

```sh
jess package test --package ../magick --package ../truetype .
jess package check --package ../magick --package ../truetype .
```

The suites draw with a stand-in logo of their own and set copy in the installed Noto Sans.

## License

MIT OR Apache-2.0. The fonts are the SIL Open Font License's and aren't part of this package; the
logo is its owner's.

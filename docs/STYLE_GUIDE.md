# DreamWeave Propaganda — Campaign Style Guide

**Draft:** 1.0  
**Campaign:** `OPERATION: BUILD SOMETHING`  
**Purpose:** Recruit independent developers, modders, toolmakers, educators, artists, and maintainers into a shared software-building ecosystem.  
**Medium:** Deterministically rendered posters, produced with **Jess** and its Magick package, a JSL raster toolkit based on ImageMagick. **No generated illustrations, image-model outputs, or image-model dependencies.**

## 1. The message

**Shared foundations. Independent creation.**

DreamWeave builds open infrastructure so people can inherit useful work instead of continually rebuilding it. Jess provides a runtime and development environment; AsHyAmS concerns publishing and distribution; StroggForge supplies shared build/release infrastructure. The posters should invite people to **create**, not merely applaud the founder.

Two statements anchor the campaign:

- **Dissent as Craft.** Build, measure, document, and ship a working alternative.
- **Civilization as Collaboration.** Leave the foundations stronger for whoever comes next.

Campaign CTA: **MAKE SOME FUCKING ART.** Use this where profanity suits the venue; have a publication-safe alternate **BUILD WHAT COMES NEXT.** The alternate is not a replacement for the brand voice, just a distribution option.

**Success test:** A newcomer should understand *who is being invited, what they're being invited to do, and where to start* within five seconds. Each piece should link to a real first action, not simply a brand homepage if a suitable quickstart/contribution route exists.

## 2. Speakers and subjects — the editorial rule

The words determine the imagery. Do not reverse this rule just because a striking character treatment is available.

| Speaker / words | Main visual | Message | Constraint |
|---|---|---|---|
| **Founder** — `I`, `my`, `I built`, `I want you` | The **actual S3 logo** as the dominant icon; optionally a *procedural, anonymous* suit/pointing-hand silhouette | A personal invitation from S3kshun8 | Exactly **one** founder-address poster in wave one, `I WANT YOU`: first-person copy stands only beside the founder's own mark. Do not invent a realistic likeness or a portrait. |
| **Collective** — `we`, `our`, `us`, `together` | Simple anonymous **builder silhouettes**, one to three people using primitive geometry | Shared work, mutual aid, durable institutions | Never substitute the founder portrait. Avoid portraying the collective as uniformed followers. |
| **Doctrine / capability** — imperative or neutral language | Typography, lines, modules, arrows, terminal cursors, scaffolds, simple circuitry | A principle or demonstrable utility | Prefer no human figures. A small DreamWeave mark may sign the piece, not dominate it. |

**`I WANT YOU` MUST center the supplied S3 emblem.** It is the founder's seal/signature, not a license to generate a face, and it appears on that poster alone. On collectivist and doctrine posters, the DreamWeave mark is a small signature, secondary to the builders or the diagram.

## 3. Visual ancestry, without imitation

The compositional references are the direct address of historic **Uncle Sam recruitment posters** and the bold, limited-palette, posterized economy associated with the **Obama “CHANGE” poster**. Borrow the **principles**, not the portraits, exact layouts, lettering, insignia, or political messaging.

The finished result must be an unmistakably original *DreamWeave software-development* campaign:

- One dominant graphic, not an illustrated scene.
- One large headline and one smaller command or explanatory line.
- Strong negative space and a tight palette.
- Sharp hierarchy visible as a phone thumbnail.
- Small, consistent provenance/footer markings.
- No flags, military uniforms, faux government seals, political-party marks, or implied real-government endorsement.

A campaign for one project may be one poster. It keeps every rule here but the first wave's
shape; its founder-address count is still at most one.

**Explicitly avoid** nebula skies, planets, enormous crowds, complex architecture, detailed facial art, photorealistic characters, cinematic effects, excessive distress/grain, and overly intricate typography. If Magick cannot create the object from clean shapes and the supplied logos, simplify it.

## 4. Color — the authoritative S3 palette

These are the campaign's palette values. Use them directly rather than inventing neighboring purple shades.

| Token | Hex | Use |
|---|---|---|
| `black` | `#070707` | Primary background |
| `shadow` | `#290430` | Backplate or deep purple section |
| `violet` | `#6B3F6F` | Structural lines, secondary panels |
| `orchid` | `#A269A7` | Supporting headline, motif |
| `lavender` | `#DA96E0` | Primary accent, CTA, key figure |
| `pinkwhite` | `#FFE6FF` | Headline and high-contrast text |
| `body` | `#F0F0F0` | Supporting copy |
| `amber` | `#FFB000` | Optional single-point signal accent, never mandatory |

Per poster: generally background + pinkwhite/body + **one** dominant purple + at most one accent. The logos have native internal color/glow; **don't recolor them wholesale** in version one.

Combinations to start with:

- Founder: black / pinkwhite / lavender; the large centered S3 logo.
- Collective: black / pinkwhite / violet or orchid; geometric silhouettes in lavender.
- Doctrine: black / pinkwhite / orchid; grid/rules/circuits in subdued violet.

Use solid fills or restrained two-stop gradients only. No gratuitous lens flares.

## 5. Image and asset rules

**The logos are supplied, never shipped.** Each is its owner's file and stays out of the repository and the package. The generator reads them from wherever its operator keeps them, the S3 logo named with `--logo PATH` and the DreamWeave logo with `--dreamweave-logo PATH`, and fails clearly when a file is missing or isn't a PNG. Do not silently replace either with generated or redrawn art.

The S3 logo is a **512 × 512 RGBA PNG with fully opaque alpha** and a nearly black background; do **not** treat it as a cutout with pre-existing transparency. Retain the original silhouette and hand-drawn edge. Prefer presenting it in a clean square black field so there is no unwanted rectangular seam. If a mask is required for an unusual background, derive a transparent asset **deterministically** from this source, inspect the edge/glow, and retain the unmodified source.

The DreamWeave logo is a **512 × 512 RGBA PNG cut out already**: a round emblem whose glow lives in its own alpha. Lay it over the poster as it is; only the faint glow that reaches the square's corners is masked away, so no square shows on black.

Allowed visual sources:

1. These two **actual logo files**.
2. Shapes, gradients, strokes, lines, simple typography, and deterministic patterns constructed by Jess and Magick, in JSL.
3. Additional human-drawn or photographed assets **only if explicitly added and licensed/approved later**, recorded by source and author.

Forbidden: any generative-image service, prompt-to-image feature, image-model output, downloaded “AI-style” stock art, or opaque image asset with undocumented provenance.

## 6. Templates and layout

**Canonical raster canvas:** `1200 × 1800` pixels (2:3). Render at this size first. Later derive social crops and print-sized editions by reflowing the layout, **not by simply trimming critical text**.

**Safe inset:** at least `72 px` from all outer edges.  
**Optical grid:** 12 columns, `24 px` gutters, strong vertical alignments.  
**Reading direction:** headline → symbol/figure → supporting message → CTA → destination.

### A. `founder-emblem` — direct-address recruitment

The recruitment formula's order: the hook at the top, the emblem in the center, the mission under it, and the call to action as the final strike.

- Headline alone: y≈110–330.
- The S3 logo centered, within y≈350–1110.
- Subheadline as the mission line, with any supporting invitation after it: y≈1150–1425. A founder poster may carry no supporting line at all; `I WANT YOU` doesn't.
- CTA panel y≈1465–1590.
- URL and provenance line y≈1622–1728.
- Optional simple pointer formed from vector strokes/polygons; not a detailed hand or face. **The S3 is the hero.**

### B. `collective-builders` — shared work

- Headline y≈130–415.
- Two or three **flat procedural silhouettes** y≈470–1160: heads as circles, torsos and arms as paths/polygons, work surfaces as rectangles. Differ through pose and tool, not stereotyping.
- A shared object to construct (a horizontal beam, three interlocking blocks, a simple terminal panel) makes their cooperation legible.
- Support and CTA y≈1200–1590; URL/footer beneath.
- Tiny DreamWeave signature only; no huge brand halo obscuring the workers.

### C. `doctrine-diagram` — principle or technical promise

- Large typography in upper half.
- A **reproducible diagram** in middle: blocks, dependency nodes, connected lanes, a simple stack of reusable modules, or lines of terminal output (all drawn by Magick).
- CTA and link in lower third.
- Avoid pictorial scenes entirely.

Layouts may be adjusted for text length, but the safe inset, clear hierarchy, and fixed footer rules are mandatory.

## 7. Typography

- **Primary:** bold, condensed sans serif for 1–2 short headline lines; all-caps permitted. Prefer a pinned installed family (e.g. an available Liberation Sans / DejaVu Sans variant) and verify actual metrics before layout.
- **Supporting:** readable sans serif in mixed case.
- **Metadata:** monospaced for identifiers/URLs and tiny doctrinal signatures; never use a 1980s “military” gimmick font merely for theme.
- **One display family + one supporting/mono family** maximum unless demonstrated necessary.
- **A themed campaign may bring its own display face**, declared in its campaign file (`display`)
  and used for every display role on its posters: headline, subheadline, call to action. The
  supporting and monospaced faces don't change, and nothing else about the layout does. The face
  must be free to use (the SIL Open Font License, say), read where it is installed and never
  shipped, and recorded in the build's manifest like any other font. The DreamWind announcement
  sets its type in Mystic Cards, the face OpenMW draws Morrowind's interface in: the theme is the
  typeface, not borrowed artwork.

Do not rasterize text as an uneditable fixed image upstream. Render source strings from the font's own outlines, read by truetype and filled by Magick. Define font size per text box and **fit from a bounded set of sizes**, failing if a string cannot fit at its minimum size. Avoid auto-shrinking until unreadable.

Suggested raster targets at 1200 × 1800: headline 110–180 px, subheadline 68–110 px, support 36–52 px, CTA 60–85 px, URL 24–32 px. These are starting points, not mandatory font metrics. Test on a downscaled 360 px-wide thumbnail; the headline and CTA must remain readable.

## 8. Text, attitude, and ethical limits

Keep language **short, defiant, funny, technically legible**. Three acceptable voices:

- **Invitation:** “I WANT YOU / TO BUILD WHAT COMES NEXT.”
- **Collective:** “WE NEED BUILDERS / NOT SPECTATORS.”
- **Doctrine:** “DISSENT AS CRAFT / BUILD THE BETTER ARGUMENT.”

Do not shame inexperienced developers, demand loyalty, promise guaranteed outcomes, invent performance numbers, or imply DreamWeave represents a government. A joke is welcome; an unsupported claim isn't. When presenting real technical comparisons, link to the methods, baselines, and results.

**The poster must carry a true exit ramp:** docs, first-script tutorial, getting-started task, or a clearly marked contribution guide. “Enlist” is optional aesthetic language, never an actual membership obligation. The campaign seeks independent builders, not obedience.

## 9. CTA and publishing

Default destination: `https://dreamweave-mp.github.io/jess/` until a verified and stable DreamWeave recruiting/quickstart page exists. Future variants may point to project-specific contribution pages; do not fabricate links.

Every released poster includes:

- Legible destination URL (and optional QR code generated from that same URL, not a replacement for readable text).
- Optional campaign mark: `DW-03 // CIVILIZATION AS COLLABORATION` on the relevant doctrine poster.
- Campaign credit: `DreamWeave` or `DreamWeave-MP`, unobtrusively.
- Image alt text supplied alongside the asset.
- Source manifest and reproducible render invocation in the repository.

Deliver both a profanity-forward edition where appropriate and an optional venue-safe CTA edition without changing the art.

## 10. Acceptance criteria

A poster is acceptable only if:

- [ ] It is built by Jess with the Magick package, entirely in JSL; **no image model has been used**.
- [ ] The original logos, read from the files supplied with `--logo` and `--dreamweave-logo`; never a substitute.
- [ ] The visual matches the grammatical speaker rule.
- [ ] All copy is faithful to the committed text manifest.
- [ ] Correct dimensions, margins, color tokens, safe areas, and legible typography.
- [ ] No broken words, clipping, unreadable CTA, or hidden link.
- [ ] Rerunning from the same inputs gives pixel-identical output (prefer byte-identical where practicable).
- [ ] Font, renderer and Jess versions and the logos' checksums are recorded with the build.
- [ ] Output includes accessible alt text, provenance, and a real destination.
- [ ] A human review approves the 360 px-wide preview **before** publication.

**Design principle:** If in doubt, **remove detail**. One icon, one statement, one invitation. The code is the proof; the poster is the doorway.

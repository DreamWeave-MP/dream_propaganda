+++
title = "dream_propaganda"
description = "OPERATION: BUILD SOMETHING, DreamWeave's recruitment posters, drawn by Jess in JSL from their copy, two logos and installed fonts."
date = 2026-10-21

[taxonomies]
tags = ["Jess", "Luau"]

[extra]
sections = ["overview", "releases", "credits"]
+++

OPERATION: BUILD SOMETHING, DreamWeave's recruitment posters, drawn by Jess in JSL from their copy, two logos and installed fonts.

<!-- more -->

A [Jess](https://github.com/DreamWeave-MP/jess) package, `org.dreamweave.dream-propaganda`, whose
command, `dream-propaganda`, draws the campaign's ten posters. Every shape is a primitive, every
letter is set from the font's own outlines by [truetype](https://dreamweave-mp.github.io/truetype/),
and the pixels are [Magick](https://dreamweave-mp.github.io/magick/)'s: no image model, no image
service. The same inputs make the same bytes.

The logos and the fonts aren't in the package: the build reads the S3 and DreamWeave logos from
where you keep them, and Noto Sans and Noto Sans Mono from where they're installed.

Every release below is the package's own archive, with its content digest beside the archive's
SHA-256; `jess.lock` pins the first and checks both.

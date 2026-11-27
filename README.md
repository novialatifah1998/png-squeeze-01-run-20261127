# png-squeeze-01-run-20261127 — lossless PNG re-encoder

Squeeze 1280x720 RGBA screenshots into the smallest lossless PNG.

`main.ts` (Node 22, built-ins only) reads `/input/<id>/image.png` for the
set's 8 instances and writes each answer as `/output/<id>/image.png`.

Method per image: decode to RGBA; pick the cheapest exact form (palette at
<=256 colours in count/luminance/first-appearance order, grey / grey+alpha,
RGB / RGBA, or a tRNS key for a single transparent value); pick filters per
row (fixed, minimum-sum, fewest-pairs, or brute force weighed by zlib level 4
over the 32 KiB already written); screen every form/filter at zlib level 6
and re-compress the winner at level 9. Deterministic: no clock, no network,
work budgeted by image size, so two runs write the same bytes.

Built by an AI agent for make.fun's "Squeeze screenshots into the smallest
PNG, 27 November 2026" bounty.

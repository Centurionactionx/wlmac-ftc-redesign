# WLMAC Robotics — sponsorship page redesign

A redesign of the WLMAC Robotics FTC sponsorship page, in the **data-texture**
style: instrument-panel telemetry on warm near-black, one amber accent, and the
two alliance colours used exactly once each on the team plates.

**Live:** https://centurionactionx.github.io/wlmac-ftc-redesign/

## What this is

The page came out of a ten-way design bake-off (five visual styles, each built
twice). This is a merge of the two data-texture builds, taking the hero,
photography and most plates from one and the plate stamps and budget
visualisation from the other.

Everything is in `index.html` — markup, design tokens, and the scripts that draw
the hero character field and run the season carousel. There is no build step and
no dependency beyond the two webfonts.

## Layout

| Path | |
| --- | --- |
| `index.html` | the whole page |
| `images/` | photography and logo |
| `.nojekyll` | serve files as-is, skip Jekyll |

## The plates

1. Hero — a robot drawn as a 104×60 character field, settling on load
2. The two teams — CyberLyons 27964, MechLyons 32514
3. Program figures
4. What a partner gets
5. Partner tiers
6. The $10,000 budget, line by line
7. Season photographs — a continuously drifting carousel
8. Contact

## Notes

- The hero field, the budget bars and the carousel each treat animation as an
  enhancement: a timer owns every end state, so the page still lands correctly
  where animation frames never arrive.
- `prefers-reduced-motion` stops the carousel drift and the settle animations.
- Photographs run in their own colour, framed by a hairline and nothing else.

The contact form hands off to the visitor's mail client via `mailto:`; there is
no backend.

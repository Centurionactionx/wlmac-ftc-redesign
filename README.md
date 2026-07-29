# WLMAC Robotics sponsorship page redesign

A redesign of the WLMAC Robotics FTC sponsorship page in the data-texture
style, which means instrument-panel telemetry drawn in the school's colours.

Live at https://centurionactionx.github.io/wlmac-ftc-redesign/

## Palette

Taken from the live site at https://www.wlmacrobotics.ca so that the two pages
read as one program.

| | |
| --- | --- |
| Surface | `#0D1B2A` navy, raised to `#12263A` and `#17324C` |
| Gold | `#F0B44C` for figures, money, and the primary action |
| Blue | `#6FA6E8` for labels, links, and structure |
| Alliance | `#1D5FC2` blue and `#CE3038` red, once each, on the team plates |

Gold and blue split the work between them instead of competing. Gold marks
value and anything you can act on. Blue marks what a thing is. Every text
pairing clears WCAG AA on the navy, and the budget bars clear 3:1 against
their own track.

## What this is

The page came out of a ten-way design bake-off, five visual styles each built
twice. This merges the two data-texture builds, taking the hero, the
photography and most plates from one, and the plate stamps and budget
visualisation from the other.

Everything lives in `index.html`: markup, design tokens, and the scripts that
run the season carousel and the enquiry form. There is no build step, and
nothing to install beyond the two webfonts the page pulls in.

## Layout

| Path | |
| --- | --- |
| `index.html` | the whole page |
| `images/` | photography and logo |
| `.nojekyll` | serve files as-is, skip Jekyll |

## The plates

1. Hero, carrying the season photograph framed as on the live site
2. The two teams, CyberLyons 27964 and MechLyons 32514
3. Season photographs, on a carousel that drifts continuously
4. Program figures
5. What a partner gets
6. Partner tiers
7. The $10,000 budget, split by where the money goes
8. Contact

The budget plate runs as two columns that carry meaning rather than just
splitting the list in half. Gold on the left is what goes into the machines,
$6,400 across four lines. Blue on the right is what it costs to run the
season, $3,600 across six. Bar widths stay comparable across both columns,
since every bar is measured against the largest single line.

Plate and figure numbers are positional. Move a plate and both sequences get
renumbered so they still read in document order.

## Verification

The enquiry form carries a reCAPTCHA v2 checkbox. `CAPTCHA_KEY` near the
bottom of `index.html` holds the site key, and blanking it removes the widget
entirely.

A key is bound to a domain list in the reCAPTCHA console, so whichever host
serves this page has to be named there. Two things follow. The field ships
hidden and is revealed only once the widget has really rendered, so a blocked
script leaves the form exactly as it was. And the check prompts once, then
stands aside: an unticked box and a box that cannot be ticked look identical
from the page's side, and a gate nobody can pass must never be able to swallow
an enquiry.

Because the form hands off to the visitor's mail client, no server of ours ever
sees the token, so the widget works as a deterrent rather than proof of a
human. Real verification needs a backend holding the secret. The main site gets
that by sending through EmailJS, which checks the token before it delivers.

## Notes

The budget bars and the carousel both treat animation as an enhancement. A
timer owns every end state, so the page still lands correctly in a renderer
that never serves an animation frame. Setting `prefers-reduced-motion` stops
the carousel drift and the bar fills.
Photographs run in their own colour, framed by a hairline and nothing else.

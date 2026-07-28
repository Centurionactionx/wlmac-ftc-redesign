# WLMAC Robotics — sponsorship page redesign

A redesign of the WLMAC Robotics FTC sponsorship page, in the **data-texture**
style: instrument-panel telemetry drawn in the school's colours.

## Palette

Taken from the live site at <https://www.wlmacrobotics.ca> so the two read as
one program:

| | |
| --- | --- |
| Surface | `#0D1B2A` navy, raised to `#12263A` / `#17324C` |
| Gold | `#F0B44C` — figures, money, the primary action |
| Blue | `#6FA6E8` — labels, links, structure |
| Alliance | `#1D5FC2` blue and `#CE3038` red, once each, on the team plates |

Gold and blue divide the work rather than competing: gold marks value and
anything you can act on, blue marks what a thing *is*. Every pairing clears
WCAG AA on the navy, and the budget bars clear 3:1 against their own track.

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

1. Hero — the season photograph, framed as on the live site
2. Build grid — a robot drawn as a 104×60 character field, settling on load
3. The two teams — CyberLyons 27964, MechLyons 32514
4. Season photographs — a continuously drifting carousel
5. Program figures
6. What a partner gets
7. Partner tiers
8. The $10,000 budget, line by line
9. Contact

Plate and figure numbers are positional: if a plate moves, both sequences
are renumbered so they still read in document order.

## Verification

The enquiry form carries a reCAPTCHA v2 checkbox. `CAPTCHA_KEY` near the
bottom of `index.html` holds the site key; blanking it removes the widget.

A key is bound to a domain list in the reCAPTCHA console, so whichever host
serves this page has to be named there. Two things follow from that:

- The field ships hidden and is revealed only once the widget has really
  rendered, so a blocked script leaves the form exactly as it was.
- The check prompts once and then stands aside. An unticked box and a box
  that *cannot* be ticked are indistinguishable from the page's side, and a
  gate nobody can pass must not be able to swallow an enquiry.

Because the form hands off to the visitor's mail client, no server of ours
sees the token, so the widget is a deterrent rather than proof of a human.
Verification would need a backend holding the secret — the main site gets
this by sending through EmailJS, which checks the token before delivering.

## Notes

- The hero field, the budget bars and the carousel each treat animation as an
  enhancement: a timer owns every end state, so the page still lands correctly
  where animation frames never arrive.
- `prefers-reduced-motion` stops the carousel drift and the settle animations.
- Photographs run in their own colour, framed by a hairline and nothing else.

The contact form hands off to the visitor's mail client via `mailto:`; there is
no backend.

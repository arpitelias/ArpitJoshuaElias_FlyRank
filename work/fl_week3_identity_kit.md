# Week 3: Identity Kit

**Arpit Joshua Elias** | General AI Fluency, Week 3

## Type

**Headings:** Source Serif 4 (Google Fonts)
**Body:** Inter (Google Fonts)

Two fonts, both free. I considered a single-font Inter setup, which is what most technical sites do, and rejected it as safe to the point of invisible. A serif heading over a plain body reads considered without being loud, which suits a claim about noticing what other people miss.

## Palette

| Role | Hex | Use |
|---|---|---|
| Text | `#1A1A1A` | Body copy, headings. Near-black, softer than pure black. |
| Background | `#FAFAF8` | Page background. Warm near-white. |
| Accent | `#2D5F5D` | Links, CTA button. Muted deep teal. |
| Muted | `#6B6B6B` | Captions, secondary text, metadata. |

The teal is deliberately desaturated. My work is notebook screenshots full of charts and coloured output, and those need to be the loudest thing on the page. A brighter accent would compete with them.

## Contrast check

| Pair | Ratio | WCAG |
|---|---|---|
| `#1A1A1A` on `#FAFAF8` | 16.65:1 | AA and AAA pass |
| `#2D5F5D` on `#FAFAF8` | 6.91:1 | AA pass, AAA fail |
| `#6B6B6B` on `#FAFAF8` | 5.10:1 | AA pass, AAA fail |
| White on `#2D5F5D` (button) | 7.23:1 | AA pass |

The accent missing AAA is acceptable because it carries links and buttons, not paragraphs. If I used it for body text I would darken it.

## Style note

Source Serif 4 for headings at two sizes only, Inter for everything else. Near-black `#1A1A1A` on warm white `#FAFAF8`, one muted teal `#2D5F5D` for links and the single call to action. Generous space around every block, and nothing decorative anywhere: the case studies and the screenshots are the only things on the page allowed to be interesting.

## Logo / favicon

A single lowercase `a` in Source Serif 4, white on `#2D5F5D`, square with slightly rounded corners. No wordmark. The site is four pages and my name is in the header, so a logo has nothing to add beyond marking the browser tab.

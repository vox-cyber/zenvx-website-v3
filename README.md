# ZenvX AI Studio — v3 website

A six-page corporate-portfolio style site for **ZenvX AI Studio** — the independent R&D
studio behind **Tosse OS** (voice + gesture desktop with Eva, the on-device assistant).
Big display headlines on warm paper, pastel coral accents, full-bleed treated photography,
a product tile grid, people section, stories reader, FAQ and a dark CTA — one portable file.

## Open it

- **The six HTML files at the root of this ZIP are fully portable** — fonts and images are
  embedded in each. Open `index.html` and navigate; everything works offline.
- **`source/`:** the editable project. Shared chrome (header, footer, reader dialog) lives in
  `gen_v3.py` — edit it and re-run to regenerate all six pages.
- **`build.py`:** rebuild the portable files after editing: `python3 build.py` → writes `dist/`;
  copy `dist/*` to the zip root to publish.

## Pages

| File | Page |
| --- | --- |
| `index.html` | Home — hero, intro, work tiles, roadmap feature, latest writing, CTA |
| `work.html` | Work — product spec sheets + the archived ZenvX OS halfway-project note |
| `people.html` | People — the showpiece: marquee, founder cards, cursor-follow roster, stats, principles |
| `stories.html` | Stories — three essays with a built-in reader |
| `faq.html` | FAQ — accordions |
| `contact.html` | Contact — giant studio inbox, pick-a-door mailto cards, direct lines to the five, elsewhere links |

## Sections

## Notes

- Brand accent: muted pastel coral `#F49097` on dark, deeper `#C2575F` on paper for contrast.
- Reveal animations arm only after the interaction layer initialises — content stays fully
  visible with JavaScript blocked or disabled, and under reduced-motion.
- Contact actions open the visitor's email app addressed to **sk@zenvx.in** — nothing sends automatically.

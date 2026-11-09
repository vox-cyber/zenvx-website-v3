# ZenvX — the multi-page, dual-mode AI studio website

A responsive studio website with twelve real HTML pages and two visitor-controlled experiences:

- **Minimal:** a polished ivory-and-ink identity, concise copy, real project previews,
  clear pricing, a studio-at-a-glance panel and prominent founder names.
- **Extravagance:** cinematic page transitions, oversized kinetic type, SVG stroke
  animation, layered floating artwork, 3D project scenes, magnetic links, contextual
  hover labels, scroll parallax and an animated printed-receipt treatment.

The visual references and art direction are documented in `DESIGN.md`.

The site presents ZenvX as a studio that turns client ideas into websites,
apps, tools and automations. Its **₹2,500 first-year website package** includes
website creation, domain, hosting and five custom-domain Zoho Mail email IDs.

## Pages

| URL | Content |
| --- | --- |
| `index.html` | Home, studio introduction, prominent team names and selected work |
| `work.html` | Portfolio and links to dedicated case studies |
| `studio.html` | The five-person team, capabilities and approach |
| `websites.html` | ₹2,500 offer, included services, delivery process and FAQ |
| `contact.html` | Direct team contacts and the project brief form |
| `os-preview.html` | Tosse OS case study and live preview link |
| `cusat-cat.html` | CUSAT CAT case study and live mock-test link |
| `vayoseva.html` | VayoSeva case study — voice-first civic services |
| `popchats.html` | PopChats case study — chat, match and call |
| `apps.html` | Live tools and previews directory |
| `about.html` | Studio and team overview |
| `research.html` | Build notes and design principles |

Each page has its own URL, content, title, description and canonical metadata.
The mode selection and motion setting persist while navigating between pages.
You can open a mode explicitly with `?mode=minimal` or `?mode=extravagance`.

## Build and preview

Python 3 is the only build dependency. Run from this directory:

```bash
python3 gen_v3.py
python3 build.py
python3 -m http.server 4173 --bind 127.0.0.1 --directory dist
```

Open **http://localhost:4173**. You can also open `dist/index.html` directly:
the HTML includes its styles, scripts and fonts, so it works offline.

## Editing

| File | Purpose |
| --- | --- |
| `source/studio-home.html.template` | Shared shell and reusable hero, project, service, pricing and contact sections |
| `site_pages.py` | Individual page composition, case studies and the central `TEAM` roster |
| `source/studio.css` | Homepage design, responsive layouts and mode-specific styles |
| `source/studio.js` | Mode persistence, page transitions, motion controls, 3D/parallax, mobile navigation and email brief |
| `source/assets/project-*.webp` | Screenshots of the live Tosse OS and CUSAT CAT projects |
| `source/font-licenses.txt` | License for the self-hosted Instrument Serif typeface |
| `gen_v3.py` | Shared project URLs and current multi-page generation entry point |
| `build.py` | Embeds assets into portable HTML and copies SEO files into `dist/` |
| `source/robots.txt`, `source/sitemap.xml` | Search-engine discovery |
| `tests/site-smoke.mjs` | Browser-level interaction and responsive checks |
| `dist/` | Generated, ready-to-publish site |

**Do not edit generated `source/*.html` or `dist/*.html` directly.** Edit the
homepage template or the generator, then run both build commands.

Project URLs in `gen_v3.py`:

- Tosse OS preview: **https://tosse.zenvx.in/**
- CUSAT CAT mock tests: **https://cusatpyq.zenvx.in/**

Historical retired pages use the `.deprecated` extension. The previous generator
is retained as `gen_v3_legacy.py`; run `gen_v3.py` for the current site.

## Contact behavior

The Contact page’s brief form validates the visitor’s input and opens an encoded
email draft to **abhi@zenvx.in**. It does **not** send mail automatically, use a
backend or store the brief in local storage. After preparing the draft, the
visitor can copy the brief if no email app is configured. Direct email links
are provided for the five people in `TEAM`. Srihari Kalesh and Abhinav T S also
appear in the homepage founder sign-off; all five names are prominently displayed
on Home, Studio and Contact.

Service and pricing links carry the selected project category into the Contact
form through a URL parameter. Visitor names, email addresses and idea text are
not carried in the URL or saved in local storage.

The experience preference is stored locally as `zenvx-mode`. Reduced-motion
visitors default to minimal mode; they can select the richer visual layout
without enabling animations. Extravagance also has a **Pause motion** control,
stored as `zenvx-motion` and available on every page.

Motion uses CSS and the native Web Animations API for the base system, plus a
thin GSAP layer (pinned 3.15.1, vendored and inlined — no network requests)
for scroll choreography in extravagance mode: scrubbed 3D poster and case-stage
tilt, hand-drawn scribble stroke draw-ons, scroll-velocity skew on the
typographic band and a staged hero entrance. The GSAP layer sits behind the
same `hasMotion()` gate as everything else — paused motion, reduced motion and
minimal mode revert every tween through `gsap.context()`, and nothing is
hidden without JavaScript. Local-page navigation has an exit/entry curtain.
Other treatments include type entry, a continuous typographic band, animated
SVG paths, floating collage pieces, bounded pointer parallax, magnetic links,
3D perspective image tilt, contextual project cursors, scroll-linked image
movement, reveal transitions, responsive hover rows and animated seals.
Scrolling remains native. No external fonts, analytics or CDN requests are
required by the site.

## Browser checks

The smoke suite requires Node.js and Playwright. One setup that keeps the
browser-check dependency outside the project is:

```bash
npm install --prefix /tmp/omnirush playwright
PLAYWRIGHT_MODULE=/tmp/omnirush/node_modules/playwright CHROME_PATH=/usr/bin/google-chrome node tests/site-smoke.mjs
```

If Playwright and its browser are installed normally, run
`node tests/site-smoke.mjs`. `CHROME_PATH` optionally selects an installed Chrome
or Chromium binary. `SCREENSHOT_DIR` optionally saves preview screenshots into
an existing directory.

For an optional automated WCAG A/AA audit in both modes, install
`@axe-core/playwright` and set `AXE_MODULE` to that package’s module path.

Checks cover all twelve pages in both modes at 320/390/768/1440px, real page navigation,
active navigation state, transition cleanup, keyboard-accessible switching,
persistence, animation pause, case-study/live-project links, project-category handoff,
email draft encoding, clipboard fallback, FAQ, mobile navigation, reduced motion,
no-JavaScript fallbacks, portable assets and JavaScript errors. The optional axe
audit covers all nine primary pages in both modes.

## Publish to zenvx.in

Upload the **contents of `dist/`** to the web root on your static host, or use
`dist` as the output directory for an automated deployment. The build command is:

```bash
python3 gen_v3.py && python3 build.py
```

For Cloudflare Pages, the build output directory is `dist` (relative to this
project’s root). A manual deployment can upload `dist/` directly. GitHub Pages,
Netlify and standard static hosting can also serve these files.

The intended canonical URL is **https://www.zenvx.in/**. Configure the host’s
custom domain and redirect the other domain variant to the canonical one.
Publish `robots.txt` and `sitemap.xml` alongside `index.html`.

If the first-year package price, renewal policy, domain eligibility or Zoho
setup changes, update the offer, FAQ, meta description and JSON-LD in the
homepage template together. Final scope and renewal costs are discussed with
the client before work begins.

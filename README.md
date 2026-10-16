# FrameOps™ — web tools for live production

**English** · [Español](README.es.md)

> Free browser-based tools that help live-event technicians prepare graphics, slides and cues for **ATEM, vMix, OBS and QLab** — no install, no account, no uploads.

**Live:** [runframeops.com](https://runframeops.com) · Designed, built and shipped solo by **Argos Anton** (audiovisual technician & developer, Barcelona).

![FrameOps homepage](assets/home.jpg)

> ℹ️ This repository is a **project showcase**. The source code is kept private; everything described here can be tried live at the links below.

---

## The problem

I work as an audiovisual technician on live shows and events. Before every show there's the same small, repetitive prep work: lower thirds for each speaker, the client's PDF turned into something the switcher can play, a countdown for the break, the logo bug in the right corner. The usual answer is Photoshop, After Effects or a paid plugin — slow, expensive, and often unavailable on the venue's laptop.

**FrameOps** turns each of those jobs into a single-purpose web page: open it, drop in your material, download a file that's ready for the switcher.

## The tools

| Tool | What it does | Output |
|---|---|---|
| [**Cairons**](https://cairons.runframeops.com) | Lower thirds (name + title) generated in bulk from a CSV or spreadsheet | One transparent PNG per person, or all of them in a ZIP |
| [**Slides**](https://slides.runframeops.com) | Converts PDFs and images into screen-ready slides in 16:9, 4:3, vertical or custom sizes | PNG sequence, auto-advancing looping PowerPoint, or H.264 MP4 |
| [**Countdown**](https://countdown.runframeops.com) | Countdowns for show starts and breaks, to a fixed time or by duration | Live URL for vMix/OBS browser sources, fullscreen output, or MP4 |
| [**Moscas**](https://moscas.runframeops.com) | Logo bugs and watermarks placed inside the title/action safe area | Full-frame transparent PNG, optional black & white key, 4 corners in a ZIP |

Each tool ships with a step-by-step **tutorial** in Spanish and English.

<table>
<tr>
<td width="50%"><img src="assets/cairons_panel.jpg" alt="Cairons: lower thirds from a CSV"><br><sub><b>Cairons</b> — CSV in, transparent lower thirds out</sub></td>
<td width="50%"><img src="assets/slides_cargado.jpg" alt="Slides: PDF to PNG, PPTX or MP4"><br><sub><b>Slides</b> — PDF to PNG, looping PPTX or MP4</sub></td>
</tr>
<tr>
<td width="50%"><img src="assets/countdown_panel.jpg" alt="Countdown control panel"><br><sub><b>Countdown</b> — control panel; settings travel in the URL</sub></td>
<td width="50%"><img src="assets/moscas_final.jpg" alt="Moscas: logo bug inside the safe area"><br><sub><b>Moscas</b> — logo bug inside the safe area</sub></td>
</tr>
</table>

## How it's built

**Everything runs client-side.** Files never leave the user's computer: no backend, no database, no uploads. That keeps hosting costs near zero, avoids handling client material (often confidential before an event) and makes the tools work on locked-down venue machines.

Some of the technical work behind it:

- **In-browser video encoding** — Slides and Countdown render frames to a canvas and encode **H.264 MP4** with the **WebCodecs API** (`VideoEncoder`) plus `mp4-muxer`, without ffmpeg or a server.
- **PDF rendering** with `pdf.js`, and **PowerPoint generation** with `PptxGenJS` (slides auto-advance and loop, ready for unattended screens).
- **Transparent PNG export** with alpha channel at broadcast resolutions (720p / 1080p / 4K), matched to what ATEM, vMix and OBS expect.
- **Hand-written ZIP packaging** (CRC-32 included) in Cairons to download a whole batch of graphics in one file without extra dependencies.
- **Stateless live output** — Countdown encodes its entire configuration in the URL (`?out=1&…`), so it can be dropped into a vMix/OBS browser source and synced to the computer clock with no server.
- **CSV parsing** tolerant of real-world exports (auto-detects `;`, `,` or tab; UTF-8 accents).
- **Lightweight i18n layer** (ES/EN) shared across all tools, with language detection, `?lang=` override and persistence.
- **Shared design system** — common header, colour tokens and self-hosted fonts (Archivo + JetBrains Mono) across five sites; no Google Fonts or third-party trackers.

**Stack:** HTML, CSS and vanilla JavaScript (no framework, no build step) · WebCodecs · Canvas · pdf.js · PptxGenJS · JSZip · mp4-muxer · Vercel (one project per tool, deploy on push to `main`) · custom domain and subdomains · Vercel Web Analytics (cookieless).

## Product, not just code

FrameOps is run as a small product, end to end:

- **Brand & identity** — name, logo, colour system and typography designed from scratch; trademark application filed with the Spanish Patent and Trademark Office (OEPM, classes 9 and 42).
- **Infrastructure** — 5 sites on a custom domain with subdomains per tool, DNS, branded email.
- **Legal & privacy** — legal notice, privacy and cookie policies in two languages; privacy-by-design (no cookies, no personal data collected).
- **Marketing** — Instagram launch with scheduled carousel, posts and reels. The promo images and videos are themselves **generated by code**: HTML templates → screenshots of the real tools via headless Chrome (DevTools Protocol) → Python + ffmpeg pipeline that assembles the reels.
- **Roadmap driven by users** — upcoming tools (*Polls*: audience voting via QR; *Cue Prep*: media prep for QLab) have a "Notify me" button so demand decides what gets built next.

## What it shows about how I work

- I build tools for problems I hit in my own job, and ship them quickly (first tool to five live sites in about a week).
- I lean on modern browser APIs to avoid servers when a server isn't needed.
- I care about the whole thing: UX for non-technical users under time pressure, documentation, bilingual content, legal, branding and launch.

---

**Contact:** [hello@runframeops.com](mailto:hello@runframeops.com) · [runframeops.com](https://runframeops.com) · Instagram [@runframeops](https://instagram.com/runframeops)

<sub>FrameOps™ is a trademark application of its owner. Screenshots © FrameOps. Source code not included.</sub>

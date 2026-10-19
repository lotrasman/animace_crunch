# Notes: "Motion Graphics with Claude Code" guide + Protein Crunch Mix brand

Source: `C:\Users\matej\Downloads\Motion-Graphics-with-Claude-Code.pdf` (Damiano Caudullo, @damianodesu, 20 pages, 14 tested prompts).
The PDF comes with a starter kit (`prompts.md`, `sfx/`, `fonts/`, `clip.mp4`) that is NOT in this folder yet.

## How HyperFrames works (guide's summary)
- The video is a web page: `index.html` (what is on screen) + a timeline (what moves, when) + a render step (Chrome screenshots every frame, FFmpeg glues them into MP4).
- You never drag keyframes. You tell Claude in plain words: "slower", "move it up", "make the number bigger". Claude edits the file and renders again.
- Workflow rule: get a base you like first, then change ONE spot at a time. End change requests with "Keep everything else the same and render again to renders/<file>.mp4".
- Describe moments in words ("when I say 40 a week"), not in seconds. Claude finds it in the audio.
- After installing skills: restart Claude Code, skills only load on a fresh start.

## The 10 named moves
Rise (fade in + move up) · Pop (scale up with overshoot) · Count-up (number rolls to value) · Checklist tick (lines get green ticks one by one) · Typewriter · Slide-in · Blur-in · Punch-in (whole frame zooms fast, for the key line) · Reframe (video shrinks into a card, something new appears) · Bar fill.
Ask for them by name.

## The 4 style blocks (paste under a base prompt as "STYLE: ...")
1. **Kinetic Type**: text is the whole video, Archivo Black all caps, black bg, white text, accent #c6ff3d, words slam in (power4.out, 0.25–0.4 s), cut on the rhythm of the words.
2. **Liquid Glass**: frosted white cards (80% opacity, 30px blur, 32px radius), soft gradient bg with drifting blobs (pale blue, lilac, peach), Inter font, text #1d1d1f, accent green #34c759, calm motion (power3.out 0.6 s, scale from 0.96, nothing bounces).
3. **Editorial Grain**: paper #efe8dc + animated SVG grain (~12%), Instrument Serif headlines (upright + italic), Inter small caps labels, ink #1a1a1a, red accent #c2412d, rotated paper cut-outs, unhurried uneven stagger. Grain makes big files: re-render with `--crf 23`.
4. **Pop Bold**: flat neon, Bricolage Grotesque 800, blocks of #c6ff3d / #8a3cff / #ff4fd8 / #111111, 4px black outlines, 8px hard shadows, stickers, back.out(2.5) bounces, squash and stretch.

## Prompt templates (numbers as in the PDF)
- 01 Setup (done on this machine, see below).
- 02 First render: 6 s, 1920x1080, 30 fps, frosted card, count-up 0→100, green pill at 4 s, Inter, `renders/first.mp4`.
- 03 Demo of all 10 moves (14 s).
- 04–07 Style blocks (above).
- 08 Text-only video: 15 s vertical 1080x1920, one sentence per screen, keep text in the middle 80% of width, `renders/text.mp4`.
- 09 Product launch video: 12 s 1920x1080. Structure: 0–2 s logo reveal / 2–9 s three feature moments shown, not told / 9–12 s end card + CTA. Uses `product.png` as hero if present. `renders/product.mp4`. **Most relevant for the Protein Crunch Mix job.**
- 10 SaaS promo: 1 min, built around a `screenshots/` folder, zoom into what matters, kinetic cuts, `renders/promo.mp4`.
- 11 Graphics on own video: transcribe with `npx hyperframes transcribe`, keep footage untouched, one style, nothing in first 3 s, nothing on face / bottom third / outer 10%. `renders/with-cards.mp4`.
- 12 Fix one spot: name the moment in words, keep everything else the same.
- 13 Sound effects from `sfx/` (pop, tick, counter, chime, snap, star, switch, fill, success). Rule: tick on list items, counter while numbers roll, chime on last card, no sound on slide in/out, no whooshes, ~20 dB under voice.
- 14 Transparent export: ProRes 4444 `.mov` with alpha + PNG sequence. Frosted cards lose their blur with nothing behind, so use solid cards for overlays.

## Export commands (run in project folder)
```
npx hyperframes render . --fps 60
npx hyperframes render . --resolution 4k
npx hyperframes render . --resolution 4k --fps 120
npx hyperframes render . --fps 24
npx hyperframes render . --format mov
npx hyperframes render . --format png-sequence
```
Add `-o <file>` for the output name. Big file: `--crf 23`.

## Fix-it phrases
Wrong font → "use the font file in fonts". Text cut on phones → "keep all text inside the middle 80% of the width". Card over captions → "move every card above the caption area". Card early/late → "make the card appear when I say X". Huge file → "render again with --crf 23".

---

## Product: Protein Crunch Mix (from the two reference images)
Czech snack brand. Tagline on pack: **"Křupavá směs oříšků a semínek v lahodném těstíčku pro každý den."**
Ad headline: **"Energie do každého pohybu"**, subline "Křupavá směs oříšků a semínek v těstíčku pro aktivní den.", CTA button **"Měj energii vždy po ruce ›"**.

### Visual identity
- Pack: deep royal blue stand-up pouch (approx. #1f2d8f / #22318f) covered in thin gold line-art illustrations of nuts and seeds (peanut, almond, pumpkin seed outlines).
- Logo lockup: "Protein" white, "CRUNCH" yellow→orange gradient (approx. #ffc93c → #f5a623), "MIX" white. Bold rounded sans (Nunito-like).
- Yellow brush-stroke badge with blue text: "Křupavé oříšky a semínka v těstíčku."
- Ad artwork: warm orange/gold burst background, coated nuts and pumpkin seeds exploding outward, pack in the centre with a star-shaped window showing the product, small 40 g pack beside it.
- Palette: royal blue, warm yellow/gold, orange, white. Icons in yellow circles with blue glyphs.

### Three benefit claims (icons: dumbbell / flexed arm, wheat / leaf, no-flask / plant)
1. Vysoký obsah bílkovin
2. Zdroj vlákniny
3. Bez umělých barviv a konzervantů

### Nutrition per 100 g (from the pack)
| | |
|---|---|
| Energie | 2090 kJ / 500 kcal |
| Tuky | 28 g (nasycené 4,1 g) |
| Sacharidy | 38 g (cukry 12 g) |
| Vláknina | 8,5 g |
| Bílkoviny | 22 g |
| Sůl | 0,4 g |

### Other facts
- Složení: arašídy, dýňová semínka, obal z vaječného bílku a hrachového prášku, slunečnicový olej, rýžová mouka, mořská sůl. Může obsahovat stopy jiných skořápkových plodů, sóji a sezamu.
- Sizes: 150 g and 40 g.
- QR code on back: "Hlasuj o další příchuti!" (vote on the next flavour).
- Barcode on pack: 8595123456789 (looks like a placeholder).

---

## Machine setup status (2026-10-18)
- Node.js v24.13.0, npm 11.6.2 (already present).
- FFmpeg 9.0.2 installed via winget (Gyan.FFmpeg).
- whisper.cpp 1.9.5 (build b5454) in `C:\Users\matej\whisper-cpp\Release`, added to user PATH.
- HyperFrames skills installed to `~\.claude\skills` (motion-graphics, product-launch-video, general-video, slideshow, talking-head-recut, music-to-video, pr-to-video, faceless-explainer, figma, remotion-to-hyperframes).
- HyperFrames 0.8.171. Installed Chrome hangs on `--version`, so HyperFrames uses its own Chrome Headless Shell 152 in `C:\Users\matej\.cache\hyperframes\chrome`. Doctor passes everything except optional Docker / Kokoro / MusicGen.
- Watch RAM: only ~1.5–3 GB of 13.8 GB was free during setup; doctor warns renders may fail under 2 GB. Close heavy apps before rendering.

---

## Intro video build (2026-10-18)
- Composition: `index.html` (standalone, 1920x1080, 20 s, `data-fps="60"`), GSAP in `vendor/gsap.min.js`, motion blur component in `vendor/motion-blur.js` (from `npx hyperframes add motion-blur`).
- Fonts: `fonts/Nunito-Variable.ttf` (Google Fonts variable file, weights 200–1000, Czech glyphs verified).
- Reference images in `reference/ad.jpeg` and `reference/back.jpeg`. No `pouch.png` existed and no clean cut-out was possible, so the pouch is rebuilt in SVG (`pouchSVG()` in index.html): blue body, gold nut pattern, skewed wordmark, star window with coated pieces, weight label.
- Scenes: hook 0–3 (flying pieces + slam), reveal 3–7 (pouch rise, crumb burst, gold sweep, 40 g pack), facts 7–14 (count-ups that shrink into a checklist), slogan 14–17 (punch-in), end card 17–20 (still from 18.5 s).
- No sfx folder was present, so the render is silent.
- Render: `npx hyperframes render --fps 60 --quality delivery --output renders/intro.mp4`. Stills: `npx hyperframes snapshot --at 2,5,10,16,19 --no-end --output renders/stills`.
- Legibility: WCAG audit forced navy-on-gold pills for "na 100 g" and navy for "150 g · 40 g"; dark halos sit behind every text block.

## Analysis doc (added 2026-10-19)
Full text in `docs/analysis.md` (from the team Google Doc). Key rules for the video: message order crunch → protein/satiety → short ingredients; honest numbers, funny, not fitness-bro; transparency story ("snack, který nemá co skrývat"); personas Adam (gym), Bára (office), Sam (gaming/parties). Never "vysoký obsah bílkovin", never "těstíčko". Feedback on v1: SVG pouch and drawn pieces looked fake, slogan too athlete-only, motion blur left ghost text. v2 needs real pouch cut-outs, real piece cut-outs, the logo file, and a persona-wide slogan.

## v2 / v3 (2026-10-19)
- Pouches: real cut-outs in `assets/pouch-150.png` and `assets/pouch-40.png`, cut from the Gemini renders by flood-filling the fake checkerboard (script logic: neutral grey + flood fill from the border, 2 px erode). Gold sweep is a masked gradient bar over the image.
- Background: gold line-art stars, peanuts, pumpkin seeds and nuts (SVG symbols `la-*`), far layer blurred, near layer at the edges. Hook flies filled gold stars and line-art pieces.
- Slogan: "Křupe. / Zasytí. / Nic neskrývá." (three beats, third in gold). Motion blur removed everywhere.
- Sound: synthesised in `assets/sfx/` (pop, tick, counter, thud, hit, crunch, sweep) via the scratch script make_sfx.py, plus the HyperFrames bundled chime. `<audio data-start data-volume>` cues sit at the bottom of `#root`. Openverse results in `.media` are unused (one near-silent, one a whoosh).
- Renders: `renders/intro-v2.mp4` (silent), `renders/intro-v3.mp4` (with audio). Stills in `renders/stills-v2`, `renders/stills-v3`.
- CTA decided 2026-10-19: keep "Měj energii vždy po ruce".
- Still open: real piece images for the hook, hook line wording, handoff route (GitHub vs zip).

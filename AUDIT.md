# ELEV8MI v34 verification

Checked on the box with headless Chromium (Playwright), 2026-10-03.
Viewports: 1280x800 (desktop) and 390x844 (phone), plus 667x375 for the
404 sweep. Each run covered the standalone site and the same files served
under a /repo/ subpath, as GitHub Pages does.

| Check | Result |
|---|---|
| Missing files (404s) on page load, standalone and /repo/ | 0 at 1280x800, 390x844 and 667x375 |
| Console errors | 0 |
| Hero glow at night (WebGL scene on) | Unchanged loader-style purple glow and dark ring |
| Hero glow mid-transition (daylight about 0.5) | Dark ring and white-violet halo each about half strength |
| Hero glow in daytime | Dark ring gone, white-violet halo full, purple glow at 45%; logo and wordmark crisp on the blue sky, no dark smudge |
| No-WebGL fallback at daytime clock (WebGL disabled) | 2D scene runs (9 bodies), sky stays night, glow unchanged (dark ring on, no halo) |
| Glow and sky in sync | Both are driven by the same --daylight value |

## E8-13 v34: animations, constellation cards, Moon fixes, efficiency (cache tag ?v=36)

| Check | Result |
|---|---|
| 404s and console/page errors, standalone and /repo/ | 0 at 1280x800, 390x844 and 667x375 (88 responses each) |
| Background scenes | Forest and cave plates drift, sweep and show motes in WebGL (frames 6 s apart differ); CSS drift and sweep without WebGL, only while the plate is on screen; still under reduced motion |
| Constellation glow | One constellation at a time lights up at night (desktop and phone) |
| Cards | Mouse click on Polaris opens its card in view; tap at 390x844 opens Polaris and Canis Minor (nearest target wins); outside click/tap and × close; Tab reaches the sky group, arrows move, Enter/Space open, Esc closes and returns focus; no focus ring on the × after a mouse open, gold ring for keyboard |
| Never blocks the UI | No sky target sits above content; header stays on top; no full-screen layer |
| Card text | 16 constellations and 21 stars checked against the star data (names, HIP numbers, magnitudes); facts spot-checked |
| Orbit Moon | Lit phase only (Last quarter today) in WebGL and in the 2D fallback; no dark disc; forced crescent and gibbous correct |
| Moon nearest | 90 s time scan (one Moon orbit, five Earth years) at 1280x800, 390x844 and 667x375: every planet overlap had the Moon on top (z 1000 against at most 900) |
| Spin | Planets and Moon keep turning (spin code unchanged since v33; Mars frames 15 s apart differ) |
| Reduced motion | Motion paused, static 2D sky, constellations off, plates still, no errors |
| No-WebGL fallback | 2D scene, plate drift on, constellations off (no real stars drawn), no errors |
| Rough frame time (software WebGL, busy box, comparison only) | 1280x800: 413 ms v33, 427 ms v34. 390x844: 216 ms v33, 242 ms v34 |

## E8-12 sky, planets, Moon and controls (cache tag ?v=35)

| Check | Result |
|---|---|
| 404s and console/page errors, standalone and /repo/ | 0 at 1280x800, 390x844 and 667x375 (86 responses each) |
| Console errors with WebGL, desktop (1440x900) and phone (390x844) tiers | 0 |
| Night sky | Real stars (mag 5 desktop, 4 phone) and constellation lines in place; Polaris, Orion (Betelgeuse, Rigel) and the Big Dipper (Dubhe, Alkaid) land on their computed positions; Milky Way band between Orion and Gemini |
| Day sky | Procedural clouds drift (frames 4 s apart differ), thin around the logo, none over Earth; stars, lines and band hidden |
| Planets by day | Opacity 1 at night, 0.69 mid, 0.38 full day (WebGL); Earth, Sun, Moon unchanged |
| Moon | Today's phase (Last quarter, 49%) matches the pill; unlit side transparent (faint earthshine at night only); forced crescent, half and gibbous render correctly |
| Spin | Every planet and the Moon turn (40-120 s per turn from spin-config.js; Venus, Uranus backwards) |
| Pause motion button | Removed (no element, no listeners); Moon pill in its place: 22 px from the right and 18 px from the bottom on desktop, 14 px and 12 px on phones (or the safe-area inset if larger) |
| Reduced motion | Motion paused automatically; static 2D sky with stars and Milky Way (fallback-sky.css), no errors |
| No-WebGL fallback | Runs with fallback-sky.css, 0 errors |
| Rough frame time (software WebGL, comparison only) | 1280x800: 245 ms before, 288 ms after. 390x844: 151 ms before, 176 ms after |


Earlier checks that still hold (v32): planets pass behind Earth with no
avoidance, the 528 Hz sound menu plays instruments on file:// as well as
over http, the day sky fades with the scene's Sun, the Moon turns on its
axis, the Moon-phase pill sits bottom right, and the hero card fits in the
first screen at 1440x900, 1280x800 and 390x844.

Limits: device performance sets the real frame rate. Reduced motion and
file:// use the still/2D scene. Celestial speeds, sizes, camera framing and
light levels are artistic, not to scale.

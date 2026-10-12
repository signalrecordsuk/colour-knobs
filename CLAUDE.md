# Colour Knobs

A toy for a 3-year-old: three animal knobs (red, green, blue) that mix the background colour.

## Where it lives

- **Live:** https://signalrecordsuk.github.io/colour-knobs/ (GitHub Pages, branch `main`, path `/`).
- **Repo:** `signalrecordsuk/colour-knobs`. Pushing to `main` redeploys in about a minute.
- **The GitHub page is the only target.** There is no claude.ai artifact to keep in sync.
- **Played mainly in Safari on an iPhone.** Test changes with touch input in mind.

## Code

- **Single file:** everything is in `index.html` (HTML, CSS and JS). There are no libraries and no build step.
- **Knobs:**
  - Each value runs 0–255 and maps to -135°..+135°, set through the CSS var `--a` on `.dial`.
  - A tap steps the value by 51 and wraps back to 0.
  - A vertical drag over 2.25× the knob height covers the full range.
  - A wheel or two-finger swipe turns the nearest knob.
- **Animals:**
  - Each animal is inline SVG in the `ANIMALS` map, drawn in the viewBox `-60 -60 120 120`.
  - The shared helpers are `eye`, `eyes`, `cheeks`, `smile` and `mirror`.
  - The `POINTER` is added to every animal automatically.
- **Adding an animal:** put it in both `ANIMALS` and `ORDER`. The paw button moves on one place in `ORDER` and shows three animals at a time. Update the animal count in `README.md` too.
- **Layout:** sized by `--k` (knob size) on `.tri`, which is derived from the viewport.
- **Sound:**
  - Uses WebAudio.
  - On iPhone it is unlocked by the first touch, which plays a silent buffer and sets `navigator.audioSession.type = 'playback'`.
  - Don't remove the touchend unlock, or iPhone sound breaks.
  - The sound on/off setting is saved in localStorage under `colourKnobsSound`.

## Git

- Commit with the GitHub no-reply email that is already set in the local git config. Pushes with a personal email are rejected by GitHub's email privacy setting.
- The local branch `main-old` is an old history with the personal email. Never push it.

## Testing

- Headless Chrome screenshots below ~500px wide look clipped. That is a Chrome limit, not a page bug.

# Colour Knobs

A toy for a 3-year-old: three animal knobs (red, green, blue) that mix the background colour.

## Where it lives

- **Live:** https://signalrecordsuk.github.io/colour-knobs/ (GitHub Pages, branch `main`, path `/`).
- **Repo:** `signalrecordsuk/colour-knobs`. Pushing to `main` redeploys in about a minute.
- **The GitHub page is the only target.** The old claude.ai artifact has been deleted; don't make a new one.
- **Played mainly in Safari on an iPhone.** Test changes with touch input in mind.

## Code

- **Single file:** everything is in `index.html` (HTML, CSS and JS). There are no libraries and no build step.
- **Knobs:**
  - Each value runs 0–255 and maps to -135°..+135°, set through the CSS var `--a` on `.dial`.
  - A tap steps to the next stop for the difficulty level and wraps back to 0 (hard taps through the medium stops).
  - Dragging turns the knob round like a real knob: the animal follows the finger's angle around the centre, clockwise to brighten. Movement within 0.12× the knob size of the centre is ignored.
  - While turning, `body.turning` turns off the colour transitions so the background and lights follow live.
  - A wheel or two-finger swipe turns the nearest knob.
- **Animals:**
  - Each animal is inline SVG in the `ANIMALS` map, drawn in the viewBox `-60 -60 120 120`.
  - The shared helpers are `eye`, `eyes`, `cheeks`, `smile` and `mirror`.
  - The `POINTER` is added to every animal automatically.
- **Groups:** `GROUPS` holds themed groups of three (red, green, blue knob in that order). The paw button moves to the next group. A new animal goes in `ANIMALS` and in a group of three; list any new group in `README.md`.
- **Layout:** the knobs zigzag down the screen: red top-left, green middle-right, blue bottom-left, each with its lamp on its inner side. `.tri` is a fixed-shape box (2.5k × 3.38k, where `--k` is the knob size) scaled to fit the screen, so nothing moves when the phone rotates; in landscape it's just smaller. Keep it orientation-independent.
- **Difficulty:** `LEVELS` holds easy (6 stops), medium (11 stops) and hard (no stops, match within 2). On easy and medium, a drag or swipe snaps to the nearest stop when let go (`settle`), and the match check waits until then. The ticks round each knob show the stops; hard shows only the two ends. Change level by shift-clicking the paw, or by holding the paw and pressing a knob (red easy, green medium, blue hard); the paw's click is skipped after a hold. The level is saved in localStorage under `colourKnobsLevel`, default easy.
- **Colour to match:** the paw button's background and the knob bases behind the animals are a random target colour: on a stop for easy and medium, any colour on hard. Both are flat (no border, gradient or shadow) so they disappear into the page on a perfect match; the paw icon is black or white depending on how light the target is. A new one is picked at load, on each paw press and on a level change. A match, once per target, wiggles the button, pops the knobs, plays a bugle fanfare (`fanfare`) and drops confetti on the `#confetti` canvas (skipped with reduced motion).
- **Buttons:** the paw button is top-right and the sound button bottom-right, because the left corners are taken by knobs.
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

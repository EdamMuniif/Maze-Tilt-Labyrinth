# ORBRINTH Level 10 — Triple Orb Extreme

**Release status (2026-11-01):** `level10.html` is now committed as a standalone Extreme test page on the main branch. It has NOT replaced the original integrated Classic Level 10. GitHub Pages deployment and real-phone completion remain unverified. The installation steps below document the original test package.

This package contains a standalone test version of a harder circular maze, **not** a replacement for the existing ORBRINTH `index.html`.

## Features

- 14 concentric rings, 40 angular sectors = 560 connected maze cells
- Three simultaneous balls starting on different outer-ring sectors
- One color-matched key per ball, placed on a verified route toward the goal
- One narrow, physically passable central entrance
- All three keys and all three balls required to finish
- No drag or keyboard movement: mobile browser orientation/gravity sensing controls the orbs
- Follow selected orb / full-maze view, pause, restart, CAL, Home

## Safe test deployment on GitHub Pages

1. In `EdamMuniif/Maze-Tilt-Labyrinth`, choose **Add file → Upload files**.
2. Upload `level10.html` from this ZIP **alongside** your existing `index.html`. **Do not overwrite `index.html`**.
3. Commit the new file to the repository.
4. Open `https://edammuniif.github.io/Maze-Tilt-Labyrinth/level10.html` in Chrome/Safari on your phone over HTTPS. Tap Enable tilt & start; press CAL in your natural landscape grip.
5. Test all three ball routes, all three colored keys, neutral calibration, and center completion.

This step adds a test page only. It does not yet replace Classic Level 10 in ORBRINTH, and does not affect existing player records.

## Adding the harder maze to the actual game

The **current main game's `index.html` already implements a three-ball circular Classic Level 10** using `multiActive()`, `buildOrbMaze()`, `updateOrbs()`, and `initOrbs()`.

Do not replace `index.html` with this standalone file: that would remove the original 15 other mazes, player profiles, themes, score logic, and other modules.

A low-risk first update to make the *existing* Level 10 harder is to adjust its maze configuration and canvas dimensions:

```js
// Main game: replace the existing ORB_* constants near buildOrbMaze().
const ORB_RINGS=14, ORB_SECTORS=40, ORB_INNER=190,
      ORB_RING_W=37, ORB_START_SECTORS=[3,16,29], ORB_GLIDE=520;

// Inside loadLevel(), for the orbLevel case, replace the square-grid sizing:
// old: if(orbLevel){C=R=26}
// new: if(orbLevel){C=R=42}
```

**Performance:** The current main game performs 300 candidate maze trials. With 560 maze cells, start with 64–80 trials and verify layout generation times on lower-end phones, rather than blindly keeping the old trial count.

**Adding the three key objectives:** Port the color-key placement logic from `mazeTry()` in `level10.html` into the existing `buildOrbMaze()`, add `key:false` to each state in `initOrbs()`, handle collection in `updateOrbs()`, and draw the keys in the main game's circular renderer. This part must be tested inside the main engine before publishing.

**Records:** Older Classic Level 10 completions may exist in `classic:9` and `classicBest['9']`. The harder challenge has different scoring conditions; keep those records unchanged and introduce a new *versioned* best-time/score record, or define a deliberate migration. The prototype writes only `orbrinth-triple-orb-extreme-v1` for its test time and does not update main profiles.

## Verification status

- JavaScript parse: passed.
- Browser simulation at 915×412, 390×844, and 320×700: passed without script exceptions or horizontal page overflow.
- Generated 560/560 connected maze cells; three solvable routes and placed color keys: passed.
- Simulated device tilt produced motion in all three balls: passed.
- Full end-to-end course completion on a physical phone: **not yet verified**.

## Production release recommendation

Publish this as `level10.html` only for private phone testing first. After controls and geometry are verified, integrate within the main code and explicitly confirm score versioning before replacing the existing Classic Level 10. Do not clear browser site data; it contains locally saved player progress.

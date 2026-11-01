# ORBRINTH — The Unknown Chapters (Levels 11–25)

## What is included
- `levels11_25.html`: self-contained, gyro-only chapter with 15 fixed-seed labyrinths.
- `level25_brief_landscape.png`, `level25_play_landscape.png`, `level25_brief_portrait.png`, `home_portrait.png`: actual Chromium screenshots.
- `patch_home_link.py`: safely generates a new `index.html` candidate containing a home-only expansion launcher, without editing the original file or its JavaScript.
- Every level explains its objective and unique hazards before players start.
- Three-dimensional phone tilt is **not** needed: the game uses the browser's device orientation or gravity-derived fallback, calibrates to a neutral position, and maps to a 2D board.
- No joystick, drag, swipe, or keyboard ball movement.
- Levels progressively introduce paired wormholes, corridor-connected fog, optional-path falling tiles, marked open boundary edges, original roaming Maw hunters, wall-impact health damage and supported phone vibration.

## Important: this is a modular expansion, not yet merged into index.html
The current ORBRINTH `index.html` contains Levels 1–10 and the existing six Special Mazes. For safety, the expansion is a separate HTML page with a ready-to-run integration patch. It reads the current V6 active nickname if it exists, but **does not write or migrate** existing `tilt-labyrinth-v6-profiles` or other main-game records.
Expansion scores use a new per-nickname key `orbrinth-chapter2-v2` and remain local to the same browser. A global Firestore leaderboard is **not** configured.

## Safest installation into GitHub Pages
1. Test the file separately over HTTPS, for example in a temporary GitHub Pages testing repository/branch deploy.
2. Upload `levels11_25.html` to the root of `EdamMuniif/Maze-Tilt-Labyrinth` **without replacing `index.html`**.
3. Once GitHub Pages builds, open `https://edammuniif.github.io/Maze-Tilt-Labyrinth/levels11_25.html` on Android Chrome or iPhone Safari.
4. Run `python patch_home_link.py index.html` against a fresh copy of your current game file. It creates `index_with_chapter2.html`, leaving the original untouched. Rename this generated file to `index.html` only after verifying the diff, then upload it alongside `levels11_25.html`. Alternatively, add the Home-menu link manually using:

   ```html
   <a class="cta secondary" href="./levels11_25.html">Levels 11–25 · The Unknown Chapters</a>
   ```
   
   Adapt the class to existing site styles. Do not overwrite the existing Home action handlers or progress keys.
5. Eventually merge the gameplay engine and progression using a controlled release once tested. This initial package provides 15 independently playable levels, **not** automatic unlocking from main game's Level 10.

## Fairness and score compatibility
- All players on this build use the same fixed seed per level; random maze changes are not used after start.
- Hole tiles do not occupy the verified solution route; generated mazes are fully connected.
- Wormholes are optional paths with safe paired destinations and a cooldown.
- Existing Level 1–10 achievements, scores, active player data, and legacy record keys are untouched.
- Any future online ranking should use server-side verification. Local JavaScript scores can be edited by players and are not authoritative.

## Physical phone test checklist
1. Open the HTTPS page in Chrome/Safari; choose a level and tap Enable tilt & play to authorize sensors.
2. Hold your phone neutrally and press `CAL`; tilt up/down/left/right, including in landscape orientation.
3. Confirm Level 12 wormholes teleport to their paired colors without looping.
4. Confirm Level 13 fog reveals connected corridors as the ball moves.
5. On Level 14, entering a dark pit **or rolling through a marked outer-wall gap** triggers one respawn and briefly requires neutral positioning.
6. On Level 16, the original Maw hunter follows corridors, can damage health, and can be avoided.
7. On Level 17, wall collisions reduce health but have an immunity cooldown; vibration works only where supported (`navigator.vibrate`). Vibration support varies between browsers and devices; absence of vibration does not affect gameplay.
8. Complete a level: score saves to the player name on that browser. Switch profiles and confirm records remain separate.
9. Leave the app in the background: the game should pause.

## Automated verification performed
- JavaScript syntax: passed.
- Generated Levels 11–25: each has a connected maze, reachable finish, and a nonempty path.
- Level 25: 33×33 cells, 533-cell guaranteed solution path (532 transitions), 4 wormhole pairs, 20 fall tiles, 3 hunters, fog, and wall damage.
- Pits and open boundary gaps excluded from solution paths; wormhole endpoints excluded from pits.
- Portal jump, pit and outer-edge respawn, fatal damage reset, wall damage cooldown, hunter contact, corridor fog visibility, and local score completion tested in Chromium with simulated events.
- Layouts at 320×700, 390×844, 915×412 tested without horizontal overflow or uncaught JavaScript errors.
- Actual Android and iPhone motion-sensor accuracy, vibration, and completion of every level are **not** physically verified.

## Security / limitations
- No network requests or third-party scripts; runs as a single HTML file.
- No personal accounts, passwords or server database are required. Player names should be nicknames only.
- Touch is limited to menu controls; it does not move the ball.
- The Maw creature is an original arcade chaser, not copied branded Pac-Man art.

## Additional edge-fall safeguards
- Edge-fall openings appear in Levels 14, 18 and 20–25 where outer branches permit them. They are explicitly marked with dashed pink rim indicators.
- Open boundary cells are never on the guaranteed solution route, on a pit, a portal, or an enemy spawn.
- A detected fall returns the marble to the start, applies a brief invulnerability period, and waits for neutral phone tilt before movement resumes.
- Wall damage that depletes health uses the same safe recovery rather than retaining the prior collision coordinate.

## Release boundary
This is a tested standalone Chapter II preview with a safe home-menu integration script. It is not yet a fully merged 25-level single-file build. Original scores, achievements and settings are not overwritten, and deployment of `index.html` or the chapter must be separately authorized.

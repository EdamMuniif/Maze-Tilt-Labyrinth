# ORBRINTH — Tilt Into the Unknown

A gyroscope-controlled HTML5 maze game hosted on GitHub Pages.

**Play:** https://edammuniif.github.io/Maze-Tilt-Labyrinth/

## Game pages

| File | Current status | What it contains |
| --- | --- | --- |
| `index.html` | Main game | Classic Levels 1–10 (including the three-ball circular Level 10), six Special Mazes, player customization, and a **Levels 11–25** selector/launcher |
| `levels11_25.html` | Published standalone Chapter II | Fifteen playable gyro-controlled challenges with pre-level briefing, fog, wormholes, falls, hunters, wall damage and optional phone vibration |
| `level10.html` | **Optional test build** | Triple Orb Extreme: harder 14-ring/40-sector circular level; **not** a replacement for main Classic Level 10 |
| `CHAPTER_II_SETUP.md` | Documentation | Chapter II architecture, testing and data limitations |
| `LEVEL10_EXTREME_SETUP.md` | Documentation | Extreme prototype and integration precautions |
| `LEADERBOARD_SETUP.md` | Optional setup guide | Firestore configuration steps; not proof that a server-backed leaderboard is currently enabled |

## How to play the new levels

1. Open the main game and enter or continue an existing player.
2. Select **LVL → LEVELS · 25**.
3. Select a level numbered **11–25**. The browser opens that chapter's briefing.
4. Read the rules, grant phone motion permission if requested, then tilt to move.

Chapter II can also be opened directly:
https://edammuniif.github.io/Maze-Tilt-Labyrinth/levels11_25.html

Level-specific deep link example:
https://edammuniif.github.io/Maze-Tilt-Labyrinth/levels11_25.html?level=11

## Save data and release limitations

- **Original Classic and Special progress remains browser-local.** Do not clear browser site data if you want to keep local records.
- Chapter II uses a **separate browser-local score and completion store** (`orbrinth-chapter2-v2`); its points do not yet combine automatically with the main game's score.
- The Chapters 11–25 page is a separately implemented game linked from the main level picker, not a single merged 25-level engine.
- The standalone `level10.html` does not override earlier Level 10 achievements.
- Phone sensor and vibration behavior must be verified on real devices. Uploading a file to GitHub is not proof that GitHub Pages finished deployment.
- The GitHub Pages URL stays the same. Query parameters such as `?v=25` may help request fresh HTML after an update; they do not reset saved data.

## Next release goals

Integrate the Chapter II progression and scoring into the main player model **with a tested migration**, preserve all existing achievements, and independently test Android/iPhone tilt and Chapter II hazard behavior before treating the 25-level release as fully unified.

TILT LABYRINTH — GYRO FIX V2
============================

IMPORTANT — HOW TO ENABLE PHONE TILT
1. Upload index.html from this folder to an HTTPS static website.
   Examples: GitHub Pages, Netlify Drop or your own HTTPS hosting.
2. On the phone, OPEN THE PUBLISHED HTTPS URL directly in Safari or Chrome.
   Avoid HTML file preview, file:// links, in-app browsers, or embedded previews.
3. Hold the phone in the position you want as neutral.
4. Tap "Enable tilt & play" and allow Motion & Orientation permission.
5. The status bar will say "WAITING FOR PHONE TILT DATA" and then
   "TILT LIVE (orientation)" or "TILT LIVE (gravity)" as data arrives.
6. Tilt the phone slowly. "X" and "Y" in the status should change.
7. Tap CAL to reset the neutral angle at any time.

IF IT STILL DOES NOT MOVE
- If you see "Tilt blocked": the website is not in a secure context.
- If permission is denied: allow motion/orientation access in browser
  site settings and try again.
- If you see "NO SENSOR DATA": your browser, device or page host is not
  providing sensor events. Try the phone's normal Safari/Chrome browser,
  an HTTPS link, and make sure motion sensors are allowed.
- If you see "TILT LIVE" but values stay zero, tilt the device more or CAL.
- Use TOUCH to continue playing with the joystick without losing progress.
- Hosting over HTTPS is essential for consistent sensor access; saving
  the HTML and opening it directly on your phone may not enable sensors.

CONTROLS
- Phone motion: DeviceOrientationEvent, backed up by DeviceMotionEvent
  accelerometer/gravity when orientation events are unavailable.
- Joystick: use the virtual on-screen touch circle.
- Keyboard: arrow keys or WASD.
- CAL: set neutral tilt position. TOUCH / TILT: switch control modes.

GAME
- 45 x 27 grid, randomized deeply branching but fully solvable maze.
- Top-down camera, wall collisions, momentum, timer, restart and pause.
- No external libraries, images or assets are required at runtime.

TEST STATUS
- Desktop Chromium automated browser tests passed with synthetic
  orientation and gravity values, permission denial, missing sensor
  message, and ball physics response.
- PHYSICAL gyro behaviour on a real user's Android/iPhone has not been
  tested here; actual support depends on device/browser/security policy.

V12 look (local, not pushed)
- New default look: one 48 px HUD row (level, time, pause, menu), a single menu for Home / Mazes / Style / Recalibrate / Restart, a one-screen home page, and a quiet tint outside the shaped mazes so the silhouette reads at play zoom.
- "Use the classic look" on the home screen switches back to the V11.4 layout (stored in localStorage key orbrinth-look-v12).
- Maze generation, collision, physics, tilt handling, scoring and profiles are untouched. Verified: all 15 mazes solvable, identical wall data, identical tilt replay in both looks.
- Not tested on a real phone yet.

Portrait update (local, not pushed)
- Classic mazes are now tall (columns x rows from 19x33 up to 37x65). The ball starts bottom-left and the finish is a random cell on the top edge.
- The finish column is drawn from the level seed, so it differs per level but is the same for every player (fair leaderboard).
- Shaped mazes also start bottom-left and finish near the top. Circle (centre goal) and the 3D level are kept as they were.
- The exit is an unmarked opening in the top wall (or silhouette edge for shapes): no marker, no arrow, you find the gap by playing. Set SHOW_FINISH=true in drawGoal to draw it again.
- Rotate-to-portrait logic removed. Maze version bump resets old wide-maze times; leaderboard season is players_s2.
- Verified in desktop Chromium only: solvability, goal on top row, deterministic tilt replay. Not tested on a real phone.

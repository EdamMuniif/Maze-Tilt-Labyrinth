# Leaderboard setup (about 5 minutes, free)

1. Go to https://console.firebase.google.com and tap **Add project**. Name it `orbrinth`. Turn Google Analytics off.
2. Left menu: **Build → Firestore Database → Create database**. Pick a location near you, choose **Production mode**.
3. Open the **Rules** tab, delete what is there, paste the full contents of `firestore.rules` from this repo, tap **Publish**.
4. Left menu: **Project settings (gear) → General → Your apps → Web (</>)**. Register an app called `orbrinth`. Copy two values from the config it shows: `projectId` and `apiKey`.
5. In `index.html`, find `const BOARD={projectId:'',apiKey:'',collection:'players_s2'};` and put the two values between the quotes.
6. Publish `index.html` to GitHub Pages. A **Leaderboard** button now appears on the home screen.

Notes
- The apiKey is meant to be public in web apps. The rules above are what protect the data: they cap name length and total, stop totals from going down, and block deletes.
- Anyone who knows how can still send a fake score. For a friends game that is usually fine. A real fix needs a server that replays the game.
- To reset the board for a new season: change `players_s2` to `players_s2` in both `index.html` and `firestore.rules`, and change `SHARED_SEED` if you also want new mazes.

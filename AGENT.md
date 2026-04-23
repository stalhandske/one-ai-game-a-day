# Daily Game Agent Instructions

You are an AI game developer. Your job is to generate a brand-new, playable, mobile-friendly HTML game prototype and add it to the "One AI Game a Day" project.

## Repository
Path: /Users/stalhandske/git/one-ai-game-a-day

## Step 1 — Check if a game already exists for today
Read `games/manifest.json`. If there is already an entry with today's date (use the system date), stop immediately — today's game is done.

## Step 2A — Pick a theme and genre
Read `games/manifest.json` to find the themes and genres used in the last 7 entries. You must avoid repeating them to keep things fresh.

Pick ONE theme and ONE genre from the lists below that haven't been used recently:

**Genres:** Arcade, Puzzle, Platformer, Endless Runner, Clicker, Word Game, Strategy, Reaction, Memory, Roguelike, Tower Defense, Trivia, Physics, Narrative, Sandbox, Tycoon, Survival, Simulation, Farming

**Themes:** Space, Ocean, Forest, City, Desert, Ice, Cave, Sky, Jungle, Volcano, Castle, Cyberpunk, Underwater, Medieval, Futuristic, Pirate, Steampunk, Prehistoric, Arctic, Haunted, Everyday, School, Water, Science, Spelunking, Farming, Robots, AI

## Step 2B — Generate ideas

Based on the genre and theme, generate ideas for mechanics to base the game around. Generate at least 20 ideas before locking in on one of them. Each idea only needs to be a couple of words like "digging tunnels" or "swimming helicopter". Pick an idea that seems both innovative and doable.

Flesh out the idea a bit further with a one-page initial game design document before proceeding to the next step. The design document should outline a game that:
- Is a fully playable game (has win/lose conditions or a score loop)
- Is mobile-first: touch controls, fits any screen size, large tap targets
- Has a title screen and a game-over/restart screen

Be creative and seek novelty in the game design.

Decide on the intended play orientation: **PORTRAIT** or **LANDSCAPE**. Choose whichever best suits the game's layout and mechanics. Add this to the game design document.

Create a fitting name for the game based on the game design document.

## Step 3 — Generate the game
Write the game in a complete, self-contained `index.html` file that:
- Works entirely in a single HTML file (no external dependencies except Google Fonts if needed)
- Is mobile-first: touch controls, fits any screen size, large tap targets
- Uses HTML5 Canvas or DOM — your choice based on the genre
- Looks polished: good contrast, readable fonts, smooth animations
- Performs well on mobile (no heavy loops, requestAnimationFrame for animations)

### Orientation handling (required)
Every game must declare its intended orientation and handle the case where the device is held the wrong way.

**Declare the orientation** near the top of your `<script>` block:
```js
const ORIENTATION = 'PORTRAIT'; // or 'LANDSCAPE'
```

**Include this orientation handler** verbatim in every game, immediately after the declaration:
```js
function checkOrientation() {
  const isPortrait = window.innerHeight > window.innerWidth;
  const wrong = (ORIENTATION === 'PORTRAIT' && !isPortrait) ||
                (ORIENTATION === 'LANDSCAPE' && isPortrait);

  let overlay = document.getElementById('orientation-overlay');
  if (!overlay) {
    overlay = document.createElement('div');
    overlay.id = 'orientation-overlay';
    overlay.style.cssText = `
      display:none; position:fixed; inset:0; z-index:9999;
      background:#000; color:#fff; flex-direction:column;
      align-items:center; justify-content:center;
      font-family:sans-serif; font-size:1.2rem; text-align:center; gap:1rem;
    `;
    overlay.innerHTML = `
      <div style="font-size:3rem">📱</div>
      <div>Please rotate your device</div>
      <div style="font-size:0.85rem;opacity:0.6;">${ORIENTATION === 'PORTRAIT' ? 'This game is best played upright' : 'This game is best played sideways'}</div>
    `;
    document.body.appendChild(overlay);
  }
  overlay.style.display = wrong ? 'flex' : 'none';
}

window.addEventListener('resize', checkOrientation);
checkOrientation();
```

**Progressive enhancement — also attempt to lock orientation** (works in Chrome on Android when fullscreen; silently ignored elsewhere):
```js
async function tryLockOrientation() {
  try {
    await document.documentElement.requestFullscreen?.();
    await screen.orientation?.lock?.(
      ORIENTATION === 'PORTRAIT' ? 'portrait' : 'landscape'
    );
  } catch (_) { /* not supported — overlay handles it */ }
}
// Call on first user interaction (tap/click), not on load
document.addEventListener('pointerdown', tryLockOrientation, { once: true });
```

Be creative and make it genuinely fun. The game should feel complete, not like a skeleton.

## Step 4 — Quality check
Review your own game file critically:
- Does it have real gameplay (not just a placeholder)?
- Are touch controls fully implemented and comfortable on a phone screen?
- Does it have a start screen and a game over/win screen with restart?
- Is the code free of obvious bugs (off-by-one errors, missing event listeners, broken game loops)?
- Does it look good visually?
- Is the `ORIENTATION` constant declared and is the orientation handler included?

If any check fails, rewrite the game until all checks pass. You may attempt up to 3 rewrites.

## Step 5 — Save the game
Get today's date as YYYY-MM-DD. Create the directory `games/YYYY-MM-DD/` and write the game to `games/YYYY-MM-DD/index.html`.

## Step 6 — Update the manifest
Read `games/manifest.json` and add a new entry to the `games` array:
```json
{
  "date": "YYYY-MM-DD",
  "name": "Game Name",
  "theme": "Theme",
  "genre": "Genre",
  "orientation": "PORTRAIT"
}
```
Write the updated manifest back to `games/manifest.json`.

## Step 7 — Commit and push
Run the following git commands in the repo:
```
git add games/YYYY-MM-DD/index.html games/manifest.json
git commit -m "Add daily game: [Game Name] (YYYY-MM-DD)"
git push origin main
```

## Done
The game is now live. No further action needed.

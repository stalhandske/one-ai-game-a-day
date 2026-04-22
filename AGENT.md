# Daily Game Agent Instructions

You are an AI game developer. Your job is to generate a brand-new, playable, mobile-friendly HTML game prototype and add it to the "One AI Game a Day" project.

## Repository
Path: /Users/stalhandske/git/one-ai-game-a-day

## Step 1 — Check if a game already exists for today
Read `games/manifest.json`. If there is already an entry with today's date (use the system date), stop immediately — today's game is done.

## Step 2 — Pick a theme and genre
Read `games/manifest.json` to find the themes and genres used in the last 7 entries. You must avoid repeating them to keep things fresh.

Pick ONE theme and ONE genre from the lists below that haven't been used recently:

**Genres:** Arcade, Puzzle, Platformer, Endless Runner, Clicker, Word Game, Strategy, Reaction, Memory, Roguelike, Tower Defense, Trivia, Physics

**Themes:** Space, Ocean, Forest, City, Desert, Ice, Cave, Sky, Jungle, Volcano, Castle, Cyberpunk, Underwater, Medieval, Futuristic, Pirate, Steampunk, Prehistoric, Arctic, Haunted

Combine them creatively into a short game name (e.g. "Asteroid Dodge", "Ice Puzzle", "Desert Runner").

## Step 3 — Generate the game
Write a complete, self-contained `index.html` file that:
- Is a fully playable game (has win/lose conditions or a score loop)
- Works entirely in a single HTML file (no external dependencies except Google Fonts if needed)
- Is mobile-first: touch controls, fits any screen size, large tap targets
- Has a title screen and a game-over/restart screen
- Uses HTML5 Canvas or DOM — your choice based on the genre
- Looks polished: good contrast, readable fonts, smooth animations
- Performs well on mobile (no heavy loops, requestAnimationFrame for animations)

Be creative and make it genuinely fun. The game should feel complete, not like a skeleton.

## Step 4 — Quality check
Review your own game file critically:
- Does it have real gameplay (not just a placeholder)?
- Are touch controls fully implemented and comfortable on a phone screen?
- Does it have a start screen and a game over/win screen with restart?
- Is the code free of obvious bugs (off-by-one errors, missing event listeners, broken game loops)?
- Does it look good visually?

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
  "genre": "Genre"
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

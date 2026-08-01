# 2048
Browser 2048 with keyboard and swipe controls
# 2048

A single-file browser implementation of 2048, with the classic tile-merge palette, keyboard and swipe controls, and a "keep going" option after reaching the 2048 tile.

## How to Play
- Arrow keys, or swipe on touch devices.
- Tiles slide and merge with equal neighbors in the direction you choose; a new tile (90% a 2, 10% a 4) spawns after every move that changes the board.
- Reach 2048 to win — you can keep playing past it. Game ends when no move in any direction is possible.

## Tech
- Single `.html` file — vanilla JS, no external dependencies beyond a Google Fonts CDN link.

## Testing
Verified with a Node + jsdom harness exercising the real merge/move functions directly, including the case that trips up most naive 2048 implementations: a tile merging twice in one move. Confirmed `[2,2,2,2]` correctly resolves to `[4,4,0,0]`, not `[8,0,0,0]`, and that `[4,4,4,0]` resolves to `[8,4,0,0]` (leftmost pair merges, the remaining tile doesn't chain into the new one). Also covered:
- All four directional moves (left/right/up/down) against a known board, checked against hand-computed expected results.
- One test initially failed here — but the mistake was in my own hand-computed expected value for the "move up" case, not the game's transpose/merge logic, which was correct on the first run. Corrected and re-verified.
- Tile spawn placement (never on an occupied cell, always value 2 or 4).
- Win detection at the 2048 tile, and game-over detection distinguishing a full board with no legal move from a full board where a merge is still possible.
- A no-op move (nothing to slide or merge) correctly does not spawn a new tile.

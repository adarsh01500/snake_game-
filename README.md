# Retro Snake Game (playsnake.org Recreation)

A faithful reverse-engineered recreation of the retro Snake game found on [playsnake.org](https://playsnake.org/).

Built with the assistance of **REA (Reverse Engineer Anything)** to inspect, decompile, and extract the original game architecture, mechanics, timing, and aesthetics.

---

## 🔍 Reverse-Engineering Findings (from playsnake.org)

1. **Board & Grid Specs**:
   - **Resolution**: 21 columns by 15 rows (315 cells total).
   - **Cell Dimensions**: 28px × 28px square cells (`float: left` / CSS grid).
   - **Board Dimensions**: 588px width × 420px height with 2px padding.
   - **Aesthetic**: Classic Nokia 3310 olive-green LCD screen (`#9bba5a` background, `#ac6` board background, `inset 0 0 60px rgba(48, 80, 0, 0.3)` inner shadow, and 4px solid outline).

2. **Game Logic & Mechanics**:
   - **Initial State**: Snake starts with 3 segments at `(10, 2)`, `(10, 1)`, `(10, 0)` moving `DOWN`.
   - **Speed Levels**:
     - **Slug**: 150 ms per tick
     - **Worm**: 100 ms per tick
     - **Python**: 50 ms per tick
   - **Countdown**: 3 → 2 → 1 → GO! (500ms intervals with audio pitch beeps).
   - **Bonus Food Decay**: Food starts worth 100 points. Every tick the food is not eaten, its value decreases by 5 points down to a minimum of 5 points.
   - **Collision Detection**:
     - Bounds checking: `x < 0 || x >= 21 || y < 0 || y >= 15`
     - Self-collision: `head.x === segment.x && head.y === segment.y`
   - **High Score Persistence**: Saved per difficulty level in `localStorage`.

3. **Audio**:
   - Recreated using procedural **Web Audio API** synthesizers (square and sawtooth oscillators) for zero latency and offline support:
     - `low`: 240Hz square wave (countdown beeps)
     - `high`: 520Hz square wave (GO! signal and food pickup)
     - `die`: 320Hz descending sawtooth buzz (game over)

4. **Added Enhancements**:
   - Multiple retro color themes (Classic Nokia Olive Green, Cyberpunk Dark, GameBoy DMG-01, Cyber Blue) toggleable via **T** or header button.
   - On-screen touch D-pad for mobile and touchscreens.
   - Touch swipe detection with 360-degree angle calculation.
   - Pause/Resume via **Space / P** or clicking the board.
   - Audio mute toggle via **M** or header button.
   - Share score feature.

---

## 🎮 How to Play

### Controls:
- **Move**: Arrow Keys or `W`, `A`, `S`, `D` (or touch swipe / on-screen D-Pad)
- **Pause / Resume**: `Space` or `P` (or click on the board)
- **Mute / Unmute**: `M` (or click mute icon)
- **Switch Theme**: `T` (or click theme icon)
- **Restart**: Click on the board when the game is over

### Launching the Game:
Simply open `index.html` in any modern web browser:
```bash
# Double-click index.html or open with your default browser:
start index.html
```
Or serve locally with any static HTTP server:
```bash
npx serve .
# or
python -m http.server 8080
```


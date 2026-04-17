# 👻 P.I.C. MAN — Reverse Pac-Man!

*You thought you were the hunter. But what if the prey bites back?*

Welcome to **Pic-Man** (which stands for **P**inky, **I**nky, and **C**lyde **Man**!), a twisted, wacky, parallel universe of the 90's arcade classic where the tables have turned. You are no longer the little yellow dot-munching circle. Instead, you are the ghosts! Your mission? Catch that ravenous, pixel-gobbling AI monstrosity before he eats you out of house and home!

Built upon a classic implementation, this has been transformed into a reverse-role thrill ride where the AI is smart, the ghosts are your responsibility, and power pellets will make you scream!

---

## 🎮 How to Play

It's time to put on your spectral matching outfits and hunt down the yellow menace:

- **Arrow Keys / WASD** — Move your currently active ghost.
- **Shift** — Cycle between ghosts! Take control of Pinky, Inky, or Clyde on the fly. The active ghost gets a shiny white aura!
- **P** — Pause / Unpause the game (for when your hands get sweaty).
- **M** — Mute / Unmute the retro sound effects.
- **R** — Restart (because you *will* lose).

### 🏆 Win / Lose Conditions

- **You WIN!** — Simply touch Pac-Man while he isn't glowing with cosmic energy.
- **You LOSE.** — Pac-Man clears the board of all dots.
- **Survival Horror Mode** — When Pac-Man eats a **power pellet**, he goes into overdrive. You are now the prey. Run. If he eats you, you respawn when the power wears off, but the humiliation lasts forever. Also, your ghost slows down to 75% speed while frightened!

---

## 🧠 What Algorithms Did I Use?

It's not just random wanderings! Pac-Man has an actual brain in this version:

- **Breadth-First Search (BFS) for Dot Seeking:** Pac-Man continuously calculates the shortest unobstructed path to the nearest dot using a BFS queue. He doesn't just bump into walls; he aggressively hunts his food.
- **Danger Mapping (Evasion AI):** When a ghost (you!) gets within 5 tiles, Pac-Man switches from "hungry" to "terrified." The game generates a "Danger Map" around the ghosts using BFS, and Pac-Man evaluates his nearby tiles, choosing the precise move that maximizes his distance from all ghosts and avoids dead ends (up to an 8-tile lookahead depth).
- **Hunting Mode Pathfinding:** If Pac-Man grabs a power pellet, the algorithm flips! He immediately locates the nearest frightened ghost via a Torus distance calculation (to account for the map's wrap-around portals) and executes a direct BFS attack path toward you.
- **Torus Mathematics for Portals:** The distance formulas account for map wrapping, so Pac-Man knows that sometimes the fastest way to escape you is to jump left through the magic wall and pop out on the right!

---

## 🧗 Problems I Faced During Development

Making an AI feel "smart but fair" was honestly a massive challenge. Here are some of the hurdles I tripped over:

1. **The Infamous Portal Glitch:** 
   Pac-Man used to literally jump out of bounds and skip a block when teleporting from the left portal to the right portal. The mathematical calculations for right-to-left worked flawlessly, but right-to-left caused him to desync from the tile grid. Fixing coordinate math and alignment constraints was a major headache!
2. **Ghost Switching Logic:**
   Implementing a system where you can seamlessly jump between 3 ghosts using the `Shift` key was tricky. They had to retain their state, pause their AI, hand control over to the player, and then resume their AI when you switched away—all while adding a glowing white halo to clearly show which one you are piloting.
3. **The "Checkmate" Corners:**
   Initially, the evasion AI was *too* scared. Pac-Man would run into corners just because the first tile felt safer, only to get trapped immediately. Implementing "lookahead depth" (evaluating tiles further down the path rather than just the immediate neighbors) solved this, making him actually capable of juking ghosts!
4. **Balancing Constraints:**
   When Pac-Man ate a power pellet, he became a bit *too* lethal. Giving the player-controlled ghosts infinite lives, combined with a 75% speed penalty when frightened and 3 total lives for Pac-Man, eventually brought the balance to a fun, heart-pounding level rather than an unwinnable mess.

---

## 🚀 How to Run Locally

Because this game uses modern ES modules (which means we break the game into nice, neat, separate files instead of one giant ball of spaghetti code), you can't just double-click the `index.html` file. Browsers block local file cross-loading for security reasons (CORS policy).

Don't worry, running it is easy! Pick your poison below:

### Option 1 — Node.js / npx (Highly Recommended!)
*(This automatically refreshes the page when you edit the code!)*
```bash
cd docs
npx live-server
```

### Option 2 — The Python Way
If you have Python installed, you already have a server!
```bash
cd docs
python -m http.server 8080
```
Then just pop open your web browser and navigate to: `http://localhost:8080`

---

*Now get out there and teach that yellow circle a lesson!*

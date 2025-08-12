# 🎯 MataTudo — AI-Assisted Browser Game

**MataTudo** is a fast-paced, infinite-level browser game built in just **3 days** using **ChatGPT as a coding partner**.  
It’s a fully playable HTML5 game with procedurally generated maps, enemy AI, boss battles, and dynamic biomes — all developed in a rapid prototype cycle.

---

## 🚀 Live Demo
[▶ Play MataTudo on GitHub Pages](https://esteves7771.github.io/MataTudo/)  

*(Runs directly in the browser — no installation required)*

---

## 🛠 Technologies
- **HTML5**, **JavaScript**, **CSS**
- AI-assisted coding with **ChatGPT**
- Procedural generation techniques
- Simple game physics and collision handling

---

## 🎮 Features
- **Infinite Levels** – Procedurally generated maps keep the gameplay fresh.
- **Enemy AI** – Ranged and melee enemies with varied spawn logic.
- **Boss Fights** – Every few levels, a stronger enemy appears with unique attack patterns.
- **Biomes** – Visual themes (Factory, Jungle, Neon City) with instant transitions after boss kills.
- **Combo System** – Bullet trails and score multipliers for skilled play.
- **UI/UX** – Health bar, score counter, and restart/start buttons for smooth game flow.

---

## ⏱ Development Speed
This game was **conceptualized, coded, tested, and fully deployed in 2–3 days** using ChatGPT for:
- Code generation and bug fixing
- Rapid iteration of gameplay mechanics
- Asset and UI styling suggestions
- Optimization and performance tweaks

---

## 🧠 Challenges & Solutions
- **Problem:** Enemies sometimes spawned too close to the player.  
  **Solution:** Added safe-zone logic to enemy spawn points.
- **Problem:** Restart flow felt too abrupt after player death.  
  **Solution:** Added a 3-second delay before restart option appears.
- **Problem:** Too many bullets and effects causing clutter.  
  **Solution:** Implemented conditional bullet trails and reduced enemy spawn rate for smoother play.

  Here’s a copy-paste-ready README block:

## Skills Used

* **Game architecture & state machine** (intro → menu → countdown → playing → gameover)
* **Canvas 2D rendering** (draw order, procedural sprites, particles, muzzle flash, screen shake)
* **Math & collisions** (vector math, circle–rect, AABB, bullet stepping, clamping)
* **AI & behaviors** (boss phases: aim/burst/spiral, enrages/dashes, mini-boss split, telegraphs)
* **Procedural generation** (obstacle layouts with BFS reachability, biomes, set-piece placement)
* **Balancing & pacing** (spawn caps/timers, elite/crimson gating, boss lulls, power-up cadence)
* **Audio integration** (HTMLAudio + light Web Audio SFX, mute/volume, music per phase)
* **UI/UX & CSS** (HUD panels, responsive poster-fit scaling, safe-area insets, micro-feedback banners)
* **Persistence** (localStorage leaderboards, daily goals, name sanitization & migration)
* **Debugging & iteration** (black-screen fixes, minimal diffs, rapid test cycles)
* **AI-assisted development** (spec-driven prompts, pair programming, change verification)


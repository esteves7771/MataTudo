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

🌐 Global Leaderboard (Firebase)
This build adds a cloud leaderboard using Firebase (Web v10 via CDN), Anonymous Auth, and Firestore.

What it does
Signs players in anonymously on load.

Saves a score document: { uid, name, score, level, accuracy, ts }.

Reads and renders Top-10 in the right panel.

Keeps the original localStorage boards as an offline fallback.

Setup (one-time)
Firebase Console → create project → Add app → Web.

Enable Authentication → Anonymous.

Enable Firestore (production or test).

In index.html, set your config inside the <script type="module"> Firebase block:

js
Copy
Edit
const firebaseConfig = {
  apiKey: "…",
  authDomain: "your-project-id.firebaseapp.com",
  projectId: "your-project-id",
  storageBucket: "your-project-id.appspot.com",
  messagingSenderId: "…",
  appId: "…"
};
(API key here is not a secret; Firebase security relies on Firestore Rules.)

Firestore structure
scores/{autoId}
uid:string, name:string(<=10), score:int, level:int, accuracy:int(0–100), ts:timestamp

users/{uid}
lastSubmit: timestamp (optional “last activity” write)

Minimal security rules (paste in Firestore Rules)
pgsql
Copy
Edit
// Firestore rules
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {

    match /scores/{id} {
      allow read: if true;
      allow create: if request.auth != null
        && request.resource.data.uid == request.auth.uid
        && request.resource.data.keys().hasOnly(['uid','name','score','level','accuracy','ts'])
        && request.resource.data.name is string
        && request.resource.data.name.size() > 0 && request.resource.data.name.size() <= 10
        && request.resource.data.score is int && request.resource.data.score >= 0 && request.resource.data.score <= 10000000
        && request.resource.data.level is int && request.resource.data.level >= 1 && request.resource.data.level <= 999
        && request.resource.data.accuracy is int && request.resource.data.accuracy >= 0 && request.resource.data.accuracy <= 100;
      allow update, delete: if false;
    }

    match /users/{uid} {
      allow read: if false;
      allow create, update: if request.auth != null && request.auth.uid == uid
        && request.resource.data.diff(resource.data).changedKeys().hasOnly(['lastSubmit']);
      allow delete: if false;
    }
  }
}
Query used for Top-10
js
Copy
Edit
const qy = query(collection(db, "scores"), orderBy("score", "desc"), limit(10));
Optional: add orderBy("ts","asc") as a tie-breaker (Firestore may prompt to create an index).

How to verify quickly
Open the browser DevTools Console while the game is running:

js
Copy
Edit
window.mtSubmitScore({ score: 999999, level: 1, accuracy: 100, name: "TestBot" })
  .then(() => console.log("Write OK"))
  .then(() => window.mtLoadGlobalTop());
You should see [Firebase] init …, [Firebase] signed in (anon) uid: …, and the right-panel Top-10 update.

Fallback & privacy
If Firebase is unreachable, the game still works with local leaderboards.

Player names are sanitized and truncated to 10 chars before writing.

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
  
---

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


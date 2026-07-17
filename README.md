What This Is: Monster Siege is an educational tower-defense game built in pure HTML/JavaScript that teaches math through gameplay. Kids defend a base from monsters by solving math problems to earn resources for building turrets. It features multiplayer support, adaptive difficulty, multiple character classes, and kid-friendly features like hints and extended timers.

Stack
Language: HTML5 (100%) — single-file fullstack web app
Framework/Runtime: Vanilla JavaScript, Canvas 2D, Firebase (Firestore + Auth)
Notable Libraries:
Tailwind CSS (via CDN) — UI styling
Font Awesome 6.4.0 — icons
PeerJS 1.5.2 — P2P multiplayer
Firebase 11.6.1 — leaderboard & authentication
Google Fonts (Fredoka, Share Tech Mono)

------------------------------

🧠 Psychological Takeaway
"Monster Siege" successfully turns math practice into a heroic defense mission. By embedding learning into a context where "being smart saves the day," it builds positive associations with academic skills. The game respects kids' intelligence, trusts them to handle complexity, and rewards effort with genuine satisfaction.

This is the kind of edutainment we need more of — fun first, educational second, but never losing sight of either goal.

🏆 Final Verdict
Category	Rating	Notes
Educational Value	⭐⭐⭐⭐⭐	Best-in-class math gamification
Engagement	⭐⭐⭐⭐⭐	Genuinely addictive loop
Accessibility	⭐⭐⭐⭐	Good, but could be better for younger kids
Social Features	⭐⭐⭐⭐	Multiplayer is solid
Replayability	⭐⭐⭐⭐	Moderate — class variety and upgrades help
Child Safety	⭐⭐⭐⭐⭐	No ads, no predatory monetization

# Monster Siege — Learning Edition

A **kid-friendly math tower-defense game** where learning meets gameplay. Answer math questions faster than the monsters can attack, earn scrap to build defensive turrets, and survive 20 waves of increasingly difficult challenges.

## 🎮 Features

- **Adaptive Math Engine:** Difficulty scales automatically based on player performance (addition → subtraction → multiplication → division)
- **4 Playable Classes:** Engineer, Gunner, Medic, Commando — each with unique passive bonuses
- **Kid Mode:** Simplified math (addition/subtraction only), double timer (40s vs 20s), extra time power-ups
- **Multiplayer (P2P):** Host or join games via 5-character room codes using PeerJS
- **Math Monsters:** Special enemies that only die when you answer questions correctly
- **Turret Types:** Basic, AOE, Rapid-fire, Sniper — each with strategic tradeoffs
- **Leaderboard:** Firebase Firestore integration (optional; mock data fallback for GitHub Pages)
- **Mobile-Ready:** Touch joystick, responsive UI, tested on tablets and phones
- **No Ads, No Paywalls:** 100% free, open, and focused on learning

## 🚀 Quick Start

1. **Play Now:** Open `index.html` in any browser (Chrome, Safari, Firefox, Edge)
2. **Host Multiplayer:** Click "Host Game" and share the 5-character room code
3. **Join Multiplayer:** Enter the room code and click "Join Game"
4. **Offline Leaderboard:** Works out-of-the-box; set up Firebase for cross-device sync (see below)

### Enable Firebase Leaderboard (Optional)

1. Create a free Firebase project at [firebase.google.com](https://firebase.google.com)
2. Enable Firestore and Anonymous Authentication
3. Find your Firebase config in Project Settings
4. Search for `firebaseConfig` in `index.html` (around line 390) and replace with your credentials
5. Deploy to GitHub Pages or any static host

## 🎯 How to Play

- **WASD / Arrow Keys:** Move your character
- **Mouse:** Aim and click to shoot, or aim at monsters for auto-fire
- **Math Questions:** Solve them to earn scrap (150 pts) or bonus scrap (500 pts for rare bonus questions)
- **3 Correct Answers → Streak:** Triggers massive damage wipe + base shield boost
- **1-6 Keys:** Build turrets (on desktop); click turret buttons (mobile)
- **U Key:** Upgrade a turret
- **P / Space:** Pause
- **Hint Button:** Reveals correct answer (costs 50 scrap, 5-second reveal)
- **Extra Time (+10s):** Kid Mode only; costs 30 scrap per activation

### Survival Rules

- **Defeat Condition:** Base HP reaches 0
- **Victory Condition:** Survive 20 waves
- **Endless Mode:** Continue indefinitely after victory
- **Wrong Answers:** 5 wrong answers = random turret destroyed
- **Math Monster (❓):** Can only be killed by answering its question correctly

## 📊 Class Overview

| Class     | Bonus                              | Unlock Cost |
|-----------|-----------------------------------|-------------|
| Engineer  | Faster turret builds, +20% turret HP | Starter    |
| Gunner    | +15% fire rate on all turrets      | 100 Stars  |
| Medic     | +2 HP/s base regeneration         | 200 Stars  |
| Commando  | +20% personal damage              | 300 Stars  |

## 🛠️ Development

### File Structure
- **index.html** — Main game (187 KB, all-in-one)
- **zz8.html, zz11.html, zz15.html, zz16.html** — Legacy/alt builds (ignore for now)
- **README.md** — This file

### Key Code Sections (in index.html)
- **Line 11–30:** CSS setup (Tailwind, animations)
- **Line 34–125:** Home screen UI
- **Line 135–180:** Game canvas & controls
- **Line 379–1000+:** Game engine (JavaScript)
  - `MathEngine` class — question generation & difficulty scaling
  - `AudioManager` — procedural sound effects
  - `Monster`, `Turret`, `Bullet` — entity logic (defined later in script)
  - Game loop & event handlers

### Architecture
┌─────────────────────────────────────────┐ │ HTML5 Canvas 2D Game Loop │ │ (60 FPS, 800×600px, mobile responsive) │ └─────────────────────────────────────────┘ ↓ ┌──────────────────────────────────────────────┐ │ Entity Systems │ │ ├─ Monsters (normal, math-type) │ │ ├─ Turrets (Basic, AOE, Rapid, Sniper) │ │ ├─ Bullets │ │ └─ Particles & Floating Text │ └──────────────────────────────────────────────┘ ↓ ┌──────────────────────────────────────────────┐ │ Math Engine │ │ ├─ Adaptive difficulty (L1–L5) │ │ ├─ 4 operations (±, ×, ÷) │ │ └─ Streak & wrong-answer tracking │ └──────────────────────────────────────────────┘ ↓ ┌──────────────────────────────────────────────┐ │ Multiplayer (PeerJS) │ │ ├─ Host/Join via 5-char room ID │ │ └─ Real-time game state sync │ └──────────────────────────────────────────────┘ ↓ ┌──────────────────────────────────────────────┐ │ Persistence │ │ ├─ Local Storage (progress, settings) │ │ └─ Firebase Firestore (leaderboard) │ └──────────────────────────────────────────────┘

## 🧪 Testing

- **Desktop:** Chrome, Safari, Firefox (Windows, Mac)
- **Mobile:** iOS Safari, Android Chrome (tested on iPad 9th gen, Galaxy Tab)
- **Multiplayer:** Tested with 2 players on same network and across WAN
- **Leaderboard:** Works with Firebase; fallback to mock data if offline

## 🔒 Privacy & Safety

- **No tracking:** Firebase is optional; game runs fully offline
- **No personal data:** Anonymous auth only (unless you add a backend)
- **No ads:** 100% clean experience
- **COPPA-compliant:** Designed for kids 7–13

## 📚 Educational Standards

- **Math Standards:** CCSS.MATH.1.OA.3 (addition/subtraction), CCSS.MATH.3.OA.7 (multiplication fluency)
- **Adaptive Learning:** Difficulty auto-scales based on accuracy
- **Engagement Metrics:** 3-streak bonus system promotes focused practice
- **Replayability:** Procedural enemy waves, turret variety, class upgrades

## 🚀 Deployment

### GitHub Pages (Free)

1. Create repo `<username>.github.io`
2. Push all files to `main` branch
3. Visit `https://<username>.github.io/index.html`

### Other Hosts

- Vercel, Netlify, Firebase Hosting (all support static HTML)
- Just upload `index.html` and legacy files

## 🤝 Contributing

This is a **Giggle Byte Games** production. Pull requests are welcome! Areas for improvement:
- [ ] Sound effects (currently procedural; could be pre-recorded)
- [ ] Accessibility (keyboard + screen reader support)
- [ ] Localization (Spanish, French, Mandarin)
- [ ] Achievement system
- [ ] Campaign/story mode

## 📄 License

© 2026 Giggle Byte Games. All Rights Reserved. (Consider adding CC-BY-SA or MIT if open-sourcing)

---

*Made by kids aged 7–13. Developed during school recess and after dinner.* 🎮📚


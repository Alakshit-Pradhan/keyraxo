# KEYRAXO TYPING — Project Context

> This file is the **source of truth** for the project. When starting a new Claude chat to add features or fix bugs, paste this file at the top of the conversation so the assistant immediately understands the project.

---

## 👤 Developer

- **Name:** Alakshit Pradhan
- **Age:** 18, independent developer from India
- **Credit line (appears in-game):** `MADE BY ALAKSHIT PRADHAN`

---

## 🔗 Project Links

- **Live game:** https://alakshit-pradhan.github.io/keyraxo/
- **GitHub repo:** https://github.com/Alakshit-Pradhan/keyraxo
- **Main file:** `index.html` (single-file, self-contained)
- **Images folder:** `images/` (12 JPG character portraits)

---

## 🎮 Game Overview

**KEYRAXO TYPING** is an anime-themed, ZType-style typing game inspired by shonen battle anime (Bleach, Naruto, Dragon Ball, One Piece).

**Core gameplay:**
- Words (enemy techniques) descend from the top of the screen
- Player types them to "counter-attack" and destroy them
- First keystroke locks onto a word — finish it to unleash a jutsu
- Combo/chain multiplier up to ×5 for speed & accuracy
- Powerup orbs (pink, from bonus words) stored in inventory, triggered with keys 1–4
- Boss wave every 5th stage (Stage 5, 10, 15...) with a single boss enemy that completes the wave when defeated
- Game over when stamina reaches 0

---

## 🗂 Tech Stack

- **Single-file HTML** — all HTML, CSS, and JS in one `index.html`
- **Vanilla JavaScript** — no frameworks (no React, Vue, etc.)
- **Canvas API** for sakura petals and visual FX layers
- **SVG** for character portraits (fallback when JPGs absent)
- **Web Audio API** for synthesized sound effects (no audio files)
- **localStorage** for per-difficulty high scores
- **Google Fonts:** Bungee, Bungee Shade, Russo One, Rubik, Share Tech Mono, Noto Sans JP

**Deployment:** GitHub Pages, free hosting, auto-deploys on commit to `main` branch.

---

## 👥 12 Fighters (character roster)

| ID | Full Name | Anime | Kanji | Signature |
|---|---|---|---|---|
| `ichigo` | Ichigo Kurosaki | Bleach | 護 | Getsuga Tensho, Bankai Tensa Zangetsu, Mugetsu, Final Getsuga |
| `goku` | Son Goku | Dragon Ball | 悟 | Kamehameha, Spirit Bomb, Ultra Instinct |
| `vegeta` | Prince Vegeta | Dragon Ball | 戦 | Galick Gun, Final Flash, Big Bang, Final Explosion |
| `gohan` | Son Gohan | Dragon Ball | 学 | Masenko, Father-Son Kamehameha, Beast Mode |
| `naruto` | Naruto Uzumaki | Naruto | 忍 | Rasengan, Shadow Clone, Sage Mode, Baryon Mode |
| `gin` | Gin Ichimaru | Bleach | 狐 | Shinso, Bankai Kamishini no Yari, Buto Renjin |
| `luffy` | Monkey D. Luffy | One Piece | 王 | Gum Gum Pistol, Gear 4 Boundman, Gear 5 Nika, Red Hawk |
| `sasuke` | Sasuke Uchiha | Naruto | 雷 | Chidori, Amaterasu, Susanoo, Kirin |
| `urahara` | Kisuke Urahara | Bleach | 店 | Nake Benihime, Bankai Kannonbiraki Benihime |
| `zoro` | Roronoa Zoro | One Piece | 剣 | Santoryu Onigiri, Shishi Sonson, Asura, King of Hell |
| `itachi` | Itachi Uchiha | Naruto | 月 | Amaterasu, Tsukuyomi, Susanoo, Izanami |
| `sanji` | Vinsmoke Sanji | One Piece | 脚 | Diable Jambe, Ifrit Jambe, Collier Shoot, Ogre Burn |

Each fighter has:
- Unique kanji emblem shown in center-bottom aura
- 3 themed colors (primary/secondary/accent) that tint the UI when selected
- 3–4 signature attack flashes shown during gameplay
- A detailed SVG fallback portrait drawn in code
- A JPG image at `images/{id}.jpg` (user-provided — may be absent)

---

## 🖼 Image System

- Character cards and info panels attempt to load `images/{characterId}.jpg`
- If the file is missing or fails to load, an inline SVG portrait renders as fallback via `onerror` handler
- Image filenames are case-sensitive lowercase, matching exactly: `ichigo.jpg`, `goku.jpg`, `vegeta.jpg`, `gohan.jpg`, `naruto.jpg`, `gin.jpg`, `luffy.jpg`, `sasuke.jpg`, `urahara.jpg`, `zoro.jpg`, `itachi.jpg`, `sanji.jpg`
- Images use `object-fit: cover; object-position: center 15%` so faces/heads aren't cropped

---

## 🎚 Difficulty Levels

| Level | Base Speed | Speed/Wave | Base Spawn | Hard Word % | Medium Word % |
|---|---|---|---|---|---|
| BEGINNER | 24 | +3.0 | 2.6s | 3% | 22% |
| INTERMEDIATE | 36 | +5.0 | 2.0s | 14% | 46% |
| ADVANCED | 50 | +7.5 | 1.4s | 26% | 52% |

- Separate localStorage high score for each difficulty
- 12 words per wave before advancement (except boss waves)

---

## ⚡ Powerups (inventory system)

| Slot | Name | Effect | Duration |
|---|---|---|---|
| 1 | JIKAN | Slows all falling words to 35% speed | 6s |
| 2 | FINAL | Destroys all on-screen words, massive combo | instant |
| 3 | GUARD | Shield aura blocks word hits | 10s |
| 4 | LIMIT | Double points scored | 10s |

Pink bonus words occasionally drop powerup orbs when destroyed.

---

## 🎨 Visual Identity

- **Background:** Dark purple/crimson radial gradients with breathing aura
- **Particles:** Sakura petals (30–50) drifting with swaying motion
- **Effects:** Speed lines on combo increase, shockwaves on explosions, camera shake on boss hits, impact frame flashes
- **Typography:**
  - `Bungee Shade` — KEYRAXO brand headline
  - `Bungee` — attack flashes, buttons
  - `Russo One` — HUD, stats, labels
  - `Share Tech Mono` — body text, instructions
  - `Noto Sans JP` — kanji decorations
- **Color scheme (CSS variables):**
  - `--c1, --c2, --c3` — dynamic, changes based on selected character
  - `--sakura` (#ffb3d1), `--blood` (#e02040), `--gold` (#ffd84d), `--cream` (#ffebd4)
- **Manga halftone dots** overlay (toggleable)

---

## 🧭 Navigation Flow

```
Home (PLAY)
    ↓
Character Select (12 cards + info panel + difficulty + FIGHT!)
    ↓   (BACK ← goes to Home)
Gameplay
    ├─ ESC or ← EXIT button → Pause
    │       ├─ CONTINUE → resume
    │       └─ CHANGE FIGHTER → Character Select
    └─ HP = 0 → Game Over (K.O.)
            ├─ REMATCH → restart same settings
            └─ CHANGE FIGHTER → Character Select
```

---

## 🔧 Key Design Decisions & Bug Fixes History

1. **Word visibility fix** — words use solid dark background + thick black text outline + white border so they never blend with the sakura background, even on complex scenes.
2. **Boss wave stuck bug fix** — originally required 12 kills to advance, but boss waves only spawn 1 boss. Fixed: on boss wave, killing the boss completes the wave immediately.
3. **In-game EXIT button** — taps trigger pause first (safer UX) so accidental clicks don't lose progress. Hidden automatically by overlay z-index when pause/menu visible.
4. **Character colors dynamic** — CSS variables swap on fighter select so the whole UI (HUD glow, emblem aura, attack flash, particle colors) reflects the chosen character's theme.
5. **SVG fallback portraits** — the game works 100% without any images uploaded. User can add JPGs at their own discretion.

---

## 💬 Communication Preferences (for future AI assistants)

- Reply in **English + Hindi mix** (Hinglish) — casual, direct, beginner-friendly tone
- Deliver **complete paste-ready files** — no truncation, no "rest of the code here" placeholders
- Prefer **targeted edits** when modifying existing code — preserve all working features, visual identity, and character designs exactly
- Use **analogies and step-by-step explanations** for technical concepts — the developer is learning
- **Production-quality code** even when teaching — don't write bad code for simplicity's sake
- When deploying changes: instructions should cover GitHub web UI (edit via pencil icon) since no local Git setup is assumed
- **Never silently remove or change** existing features when adding new ones — confirm if uncertain

---

## 📋 Deployment Workflow (no local setup)

1. Open `github.com/Alakshit-Pradhan/keyraxo` in browser
2. Click `index.html` → ✏️ pencil (edit)
3. `Ctrl+A` → delete → paste new full file
4. Scroll down → **Commit changes**
5. Wait 1–2 minutes for GitHub Pages to redeploy
6. Hard refresh live site (`Ctrl+Shift+R`) to bypass browser cache

---

## 🚀 Future Feature Ideas (roadmap — not yet built)

- [ ] Daily challenge mode (fixed seed, shareable scores)
- [ ] Global leaderboard (would require backend — Firebase / Supabase)
- [ ] More fighters (Madara, Kaguya, Yhwach, Blackbeard, etc.)
- [ ] Character unlock progression (play X stages to unlock Y fighter)
- [ ] Achievements / badges system
- [ ] Training mode (practice specific word lists)
- [ ] Sound volume slider (beyond current SFX on/off toggle)
- [ ] Background music option (royalty-free tracks)
- [ ] Keybind customization for powerup slots
- [ ] Custom character support (user uploads image + chooses color/kanji)

When adding any of these, **read the existing code carefully first** and preserve the established visual identity and gameplay feel.

---

## 🙏 Credits

- **Code, design, direction:** Alakshit Pradhan
- **Assistance:** Iterative collaboration with Claude (Anthropic)
- **Fonts:** Google Fonts (Bungee family, Russo One, Rubik, Share Tech Mono, Noto Sans JP)
- **Inspiration:** ZType (zty.pe) for the typing-shooter mechanic; Bleach, Naruto, Dragon Ball, One Piece for the fighter roster

---

*Last updated: when you change the project, update this file too.*

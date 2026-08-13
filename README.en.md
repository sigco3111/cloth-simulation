# 🧵 cloth-simulation

> Verlet Integration-based tearing red-velvet cloth simulation — grab, drag, ripple, and tear it with your mouse

A physical cloth simulation rendered with HTML5 Canvas + Verlet Integration. A 32×42 grid (1,344 points) woven with structural + shear constraints responds to mouse drag, wind, and gravity; pull hard enough that a constraint's distance exceeds the tear threshold and the cloth rips apart. A 5-pass rendering pipeline implementing anisotropic BRDF velvet shading produces realistic tone, sheen, and rim light.

[🇰🇷 한국어 (기본)](./README.md) · [🇺🇸 English](#)

---

## 🎬 Live Demo

> **👉 [https://sigco3111.github.io/cloth-simulation/](https://sigco3111.github.io/cloth-simulation/)** — open in any modern browser (60fps, desktop recommended)

| | |
|---|---|
| ![Status](https://img.shields.io/badge/Status-Live-22C55E?style=flat-square) | ![Stack](https://img.shields.io/badge/Stack-Canvas_+_Verlet-FF6B6B?style=flat-square) |
| ![Live](https://img.shields.io/badge/Live-Demo-222222?style=for-the-badge&logo=githubpages&logoColor=white) | [![Repo](https://img.shields.io/badge/GitHub-sigco3111%2Fcloth--simulation-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/sigco3111/cloth-simulation) |
| ![License](https://img.shields.io/badge/License-MIT-F1C40F?style=flat-square) | ![Deps](https://img.shields.io/badge/Dependencies-0-9CA3AF?style=flat-square) |

### 🎮 Quick controls
1. Click the link above → page opens in your browser
2. **Mouse drag** — grab any point on the cloth and pull it
3. **Pull hard** — when strain exceeds the tear threshold, constraints break and the cloth rips
4. Watch the torn piece flutter naturally under wind + gravity

---

## 🤖 Attribution

This project's code is **auto-generated** using the following model and prompt.

| Field | Value |
|---|---|
| **Model** | MiniMax-M3 |
| **Environment** | OpenCode CLI |
| **Repository** | [`sigco3111/cloth-simulation`](https://github.com/sigco3111/cloth-simulation) |
| **License** | MIT |
| **Dependencies** | None (Vanilla JS + Canvas 2D, single HTML) |

### 📝 Prompt Used (verbatim from source)

```
HTML5 Canvas와 Verlet Integration 알고리즘을 사용하여 마우스로 잡아서 당기면 물리적으로 늘어나고 세게 당기면 찢어지는
붉은색 벨벳 질감의 천(Cloth) 시뮬레이션을 구현하되, 바람의 영향으로 천이 자연스럽게 펄럭이는 효과와 중력 모델을 정교하게 적용해줘.
Implementation Advice: Use HTML5 Canvas. Implement Verlet Integration for the physics (points and constraints).
To "tear" the cloth, check if the distance between two points in a constraint exceeds a threshold, then remove that constraint.
모든 의존관계의 코드를 하나의 HTML에 담는 형태로 코드 작성.
```

---

## ✨ Features

- 🧶 **32×42 grid (1,344 points)** — structural + shear constraint topology
- 🖱️ **Mouse drag** — nearest-point pick + position snap + soft spring
- 💥 **Tearing** — constraint distance check removes the failed constraint; both halves continue freely
- 🎨 **5-pass velvet shading** — per-quad anisotropic BRDF (ambient + diffuse + sheen + backlit + rim) + ImageData noise nap overlay
- 💨 **Wind** — dual spatio-temporal sin pattern + direction reversal + position-based gusts
- ⚡ **60fps** — `requestAnimationFrame` + fixed dt substep, 4×0.75 constraint relaxation (~98% enforced)
- 📦 **Single HTML** — zero external dependencies; double-click to run
- 🎛️ **Live UI** — Wind / Gravity / Tear sliders, Drop / Re-Pin / Reset buttons

---

## 🚀 Quick Start

### Method 1: Live demo (GitHub Pages) — easiest
Click the Live Demo link above → runs without any install or clone.

### Method 2: Open in browser directly
```bash
git clone https://github.com/sigco3111/cloth-simulation.git
cd cloth-simulation
open index.html        # macOS
xdg-open index.html    # Linux
start index.html       # Windows
```

### Method 3: Local server (recommended; better mobile compatibility)
```bash
python3 -m http.server 8000
# → http://localhost:8000
```

**No internet required** — all assets (fonts, noise pattern, UI) are embedded in the single HTML.

---

## 🎮 Controls

| Input | Effect |
|---|---|
| **Mouse move** | Cursor halo over the cloth (radius indicator) |
| **Mouse drag (mousedown + move)** | Grab the nearest point and pull it (soft spring) |
| **Pull hard** | When strain exceeds threshold, constraints break and the cloth tears (free fall starts) |
| **Mouse up** | Held point returns to free simulation |

### UI controls

| Control | Range | Default | Effect |
|---|---|---|---|
| **Wind** slider | 0 – 100% | ~50% | Wind force amplitude (added per frame) |
| **Gravity** slider | 0.0g – 2.0g | 1.0g | Gravity multiplier (base 900 px/s² × multiplier) |
| **Tear** slider | 100 – 400% of rest length | ~180% | Tearing threshold (lower = easier to tear) |
| **Drop** button | — | — | Release every pin; cloth falls freely |
| **Re-Pin** button | — | — | Re-anchor the top row |
| **Reset** button | — | — | Recreate the cloth in initial state |

---

## 🛠️ Tech Stack

| Layer | Tech |
|---|---|
| **Rendering** | HTML5 Canvas 2D Context, 5-pass draw pipeline (BRDF + velvet nap overlay) |
| **Physics** | Verlet Integration (Jakobsen-style constraint relaxation) |
| **Data structures** | `Point` (x, y, px, py, ax, ay, pinned) + `Constraint` (a, b, restLength, torn) objects |
| **Mouse input** | Pointer events + nearest-point pick + soft-spring snap |
| **Velvet shading** | ambient + diffuse + sheen + backlit + rim (5 BRDF components) + procedural noise nap |
| **Wind model** | dual sin(time, space) + position-based gust + direction reversal |
| **Loop** | `requestAnimationFrame` + fixed-dt substep, accumulator pattern |
| **Deps** | None (Vanilla JS) |

---

## 📂 Project Structure

```
cloth-simulation/
├── index.html          # Single HTML (Canvas + Verlet + 5-pass shader + UI)
├── README.md           # Korean (default)
├── README.en.md        # English (this file)
├── LICENSE             # MIT License
└── .gitignore          # Node/IDE temp + .vercel/ exclusions
```

---

## 🎨 Design Choices

Four key decisions made during brainstorming:

| Decision | Choice | Rationale |
|---|---|---|
| **Render passes** | 5 passes (solid → highlight → pin → grabbed → cursor halo) | A single `fillStyle` call can't naturally compose pearl sheen, shadow, and pin markers; splitting into layers lets each pass contribute a single lighting cue |
| **Velvet tone** | anisotropic BRDF (5 components) + procedural nap overlay | Lambert alone can't express view-dependent velvet sheen/rim; ImageData noise adds the micro-glints that make velvet read as velvet |
| **Stability** | fixed-dt substep + 4×0.75 stiffness + 3-pass damping | Large frame deltas make constraint relaxation diverge → "exploding cloth" artifacts; shrinking dt and raising iteration count keeps stiffness tight without explosive energy |
| **Wind pattern** | dual sin(t) × sin(space) + gust + periodic direction reversal | A single sin produces a uniform one-way sway that reads as balloon, not cloth; layering temporal + spatial sin plus position-based gust and ±half-period direction flips yields organic flutter |

### Customizing further

Tweak the `CONFIG` block at the top of `index.html` to dial the feel:

```js
const CONFIG = {
  GRID_W: 32,           // columns
  GRID_H: 42,           // rows
  SPACING: 12,          // point spacing (px)
  TEAR_THRESHOLD: 1.8,  // multiplier of rest length before constraint breaks
  WIND_BASE: 0.5,       // baseline wind force
  GRAVITY: 900,         // px/s²
  CONSTRAINT_ITERS: 4,  // constraint relaxation passes (stability vs cost)
  DAMPING: 0.5,         // 0-1; closer to 1 = cloth oscillates forever
  // …more options in the source comments
};
```

For advanced users: swap the `step()` method inside `class Cloth` to try semi-implicit Euler or Position Based Dynamics (PBD). Modify the tearing logic in the `Constraint` array to evolve from "one-shot rip" to "gradual unravel" of the cloth.

---

## 📜 License

MIT © 2026 sigco3111

---

## 🙏 Acknowledgments

This project was generated by [MiniMax-M3](https://example.com) model in the OpenCode CLI environment. Prompt engineering and design decisions were made by the repository owner.

- **Coding mission reference**: [cokac.com — 코드깎는노인](https://cokac.com/list/announcement/24)
- **Previous-mission README template**: [sigco3111/neon-fluid](https://github.com/sigco3111/neon-fluid)

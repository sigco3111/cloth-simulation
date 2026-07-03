# 🧵 cloth-simulation

> Verlet Integration-based tearing 3D cloth simulation — red velvet cloth you can grab, drag, ripple, and tear

A physical cloth simulation rendered with HTML5 Canvas + Verlet Integration. Grab any point with your mouse to stretch the cloth; apply enough force that a constraint's distance exceeds the tear threshold and the cloth rips apart. Wind + gravity are integrated into the physics model for natural flutter and drape.

[🇰🇷 한국어 (기본)](./README.md) · [🇺🇸 English](#)

---

## 🎬 Live Demo

> **👉 Coming soon (Work in progress)** — `MiniMax-M3` is working on it via OpenCode

| | |
|---|---|
| ![Status](https://img.shields.io/badge/Status-In_Development-F59E0B?style=flat-square) | ![Stack](https://img.shields.io/badge/Stack-Canvas_+_Verlet-FF6B6B?style=flat-square) |
| ![License](https://img.shields.io/badge/License-MIT-F1C40F?style=flat-square) | ![Deps](https://img.shields.io/badge/Dependencies-0-9CA3AF?style=flat-square) |

---

## 🎮 Quick Controls (planned)
1. Open the page — red velvet cloth displayed, naturally fluttering
2. **Mouse drag** — grab any point on the cloth, stretch it
3. **Pull hard** — past the constraint tear threshold, cloth rips
4. Watch gravity + wind flutter the remaining cloth naturally

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

### 📝 Prompt Used

```
HTML5 Canvas와 Verlet Integration 알고리즘을 사용하여 마우스로 잡아서 당기면 물리적으로 늘어나고 세게 당기면 찢어지는 붉은색 벨벳 질감의 천(Cloth) 시뮬레이션을 구현하되, 바람의 영향으로 천이 자연스럽게 펄럭이는 효과와 중력 모델을 정교하게 적용해줘.
Implementation Advice: Use HTML5 Canvas. Implement Verlet Integration for the physics (points and constraints). To "tear" the cloth, check if the distance between two points in a constraint exceeds a threshold, then remove that constraint. 모든 의존관계의 코드를 하나의 HTML에 담는 형태로 코드 작성.
```

---

## 🛠️ Tech Stack (planned)

- **Rendering** — HTML5 Canvas 2D Context (`fillRect` + imageData pixel shading)
- **Physics engine** — Verlet Integration
  - **Points** — grid positions, previous positions, accumulated force
  - **Constraints** — distance constraints between adjacent points (stretch/tear)
  - **Integration** — position = 2×current - previous + acceleration (velocity-implicit)
- **Mouse interaction** — `mousedown`/`mousemove`/`mouseup` + ray pick
- **Velvet shading** — gradient + subtle noise per pixel for fabric depth
- **Bundle** — all dependencies embedded in single `index.html`

---

## 📂 Project Structure

```
cloth-simulation/
├── index.html          # Single HTML (Canvas + Verlet + minimal JS)
├── README.md           # Korean (default)
├── README.en.md        # English version
├── LICENSE             # MIT License
└── .gitignore          # Node/IDE temp files exclusion
```

---

## 🚀 Run Locally

```bash
git clone https://github.com/sigco3111/cloth-simulation.git
cd cloth-simulation
open index.html        # macOS
# or open index.html in any browser directly
```

**No internet required** — all assets embedded.

---

## 📜 License

MIT License — use, modify, and distribute freely.

---

> 🤖 *This README structure is adapted from the verified [neon-fluid](https://github.com/sigco3111/neon-fluid), [gravity-typography](https://github.com/sigco3111/gravity-typography), and [sci-fi-hud](https://github.com/sigco3111/sci-fi-hud) mission templates.*

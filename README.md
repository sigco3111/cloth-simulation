# 🧵 cloth-simulation

> Verlet Integration 기반 찢어지는 3D 천 시뮬레이션 — 마우스로 잡아당기고, 펄럭이고, 떨어뜨릴 수 있는 붉은 벨벳 천

HTML5 Canvas + Verlet Integration 알고리즘으로 구현된 물리적 천 시뮬레이션입니다. 마우스로 천을 잡아당기면 자연스럽게 늘어나고, 일정 임계값을 넘어 세게 당기면 천이 찢어집니다. 바람 효과와 중력이 물리 모델에 통합되어 자연스러운 펄럭임과 늘어짐을 표현합니다.

[🇰🇷 한국어 (기본)](#) · [🇺🇸 English](./README.en.md)

---

## 🎬 라이브 데모 (Live Demo)

> **✅ 완료 (Ready)** — `index.html`을 브라우저에서 열면 바로 실행됩니다

| | |
|---|---|
| ![Status](https://img.shields.io/badge/Status-Ready-10B981?style=flat-square) | ![Stack](https://img.shields.io/badge/Stack-Canvas_+_Verlet-FF6B6B?style=flat-square) |
| ![License](https://img.shields.io/badge/License-MIT-F1C40F?style=flat-square) | ![Deps](https://img.shields.io/badge/Dependencies-0-9CA3AF?style=flat-square) |

---

## 🎮 빠른 사용법
1. 페이지 열기 — 붉은 벨벳 천이 펄럭이며 표시됨
2. **마우스 드래그** — 천의 임의 지점 잡아당기기
3. **세게 당기기** — constraint 임계값 초과 시 천이 찢어짐
4. 천이 자유낙하 + 바람 영향으로 자연스럽게 펄럭이는 모습 감상

### UI 컨트롤
- **Wind** 슬라이더 — 바람 세기 (0–100%)
- **Gravity** 슬라이더 — 중력 강도 (0.0g–2.0g)
- **Tear** 슬라이더 — 찢어지는 임계값 (% of rest length)
- **Drop** — 모든 pin 해제, 천을 자유낙하
- **Re-Pin** — 상단을 다시 고정
- **Reset** — 천 재생성

---

## 🤖 생성 정보 (Attribution)

이 프로젝트의 코드는 아래 모델과 프롬프트를 이용해 **자동으로 생성**됩니다.

| 항목 | 값 |
|---|---|
| **모델** | MiniMax-M3 |
| **실행 환경** | OpenCode CLI |
| **저장소** | [`sigco3111/cloth-simulation`](https://github.com/sigco3111/cloth-simulation) |
| **라이선스** | MIT |
| **의존성** | 없음 (Vanilla JS + Canvas 2D, 단일 HTML) |

### 📝 사용된 프롬프트 (원문)

```
HTML5 Canvas와 Verlet Integration 알고리즘을 사용하여 마우스로 잡아서 당기면 물리적으로 늘어나고 세게 당기면 찢어지는 붉은색 벨벳 질감의 천(Cloth) 시뮬레이션을 구현하되, 바람의 영향으로 천이 자연스럽게 펄럭이는 효과와 중력 모델을 정교하게 적용해줘.
Implementation Advice: Use HTML5 Canvas. Implement Verlet Integration for the physics (points and constraints). To "tear" the cloth, check if the distance between two points in a constraint exceeds a threshold, then remove that constraint. 모든 의존관계의 코드를 하나의 HTML에 담는 형태로 코드 작성.
```

---

## 🛠️ 기술 스택

- **렌더링** — HTML5 Canvas 2D Context (per-quad anisotropic BRDF + ImageData-based velvet nap overlay)
- **물리 엔진** — Verlet Integration (Jakobsen-style constraint relaxation)
  - **Points** — 32×42 격자점, 각 (x, y, px, py, ax, ay, pinned, mass)
  - **Structural Constraints** — 수평/수직 인접점 (rest length = spacing)
  - **Shear Constraints** — 대각선 인접점 (rest length = spacing × √2)
  - **Integration** — `new = pos + (pos − prev) × damping + accel × dt²`
  - **Stiffness** — 4 iterations × 0.75 per iteration (~98% enforced)
- **마우스 인터랙션** — `mousedown`/`mousemove`/`mouseup` + nearest-point pick + positional snap
- **벨벳 질감** — anisotropic BRDF (ambient + diffuse + sheen + backlit + rim) + procedural noise overlay
- **바람** — 시간/공간 이중 sin 패턴 + 방향 반전 + 위치 기반 gust
- **중력** — 900 px/s² (조정 가능)
- **번들** — 모든 의존성을 단일 `index.html`에 임베드 (0 deps)

---

## 📂 프로젝트 구조

```
cloth-simulation/
├── index.html          # 단일 HTML 파일 (Canvas + Verlet + 최소 JS)
├── README.md           # 본 문서 (한국어)
├── README.en.md        # English version
├── LICENSE             # MIT License
└── .gitignore          # Node/IDE 임시 파일 제외
```

---

## 🚀 로컬 실행

```bash
git clone https://github.com/sigco3111/cloth-simulation.git
cd cloth-simulation
open index.html   # macOS
# 또는 브라우저에서 index.html 직접 열기
```

**인터넷 연결 불필요** — 모든 자원이 단일 HTML에 내장되어 있습니다.

---

## 📜 라이선스

MIT License — 자유롭게 사용, 수정, 배포하세요.

---

> 🤖 *이 리드미의 README 구조는 검증된 [neon-fluid](https://github.com/sigco3111/neon-fluid), [gravity-typography](https://github.com/sigco3111/gravity-typography), [sci-fi-hud](https://github.com/sigco3111/sci-fi-hud) 미션 형식을 차용했습니다.*

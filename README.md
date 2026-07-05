# 🧵 cloth-simulation

> HTML5 Canvas + Verlet Integration 기반 찢어지는 붉은 벨벳 천 시뮬레이션 — 마우스로 잡아당기고, 펄럭이고, 떨어뜨릴 수 있는 물리 기반 직물

HTML5 Canvas + Verlet Integration 알고리즘으로 구현된 물리적 천 시뮬레이션입니다. 32×42 격자점(총 1,344개)으로 직조된 붉은 벨벳 천이 마우스 드래그, 바람, 중력에 따라 자연스럽게 펄럭이며, 일정 임계값을 넘어 세게 당기면 천이 찢어집니다. 5-pass 렌더링으로 구현된 anisotropic BRDF 벨벳 셰이딩이 사실적인 톤과 광택을 만들어냅니다.

[🇰🇷 한국어 (기본)](#) · [🇺🇸 English](./README.en.md)

---

## 🎬 라이브 데모 (Live Demo)

> **👉 [https://cloth-simulation-delta.vercel.app/](https://cloth-simulation-delta.vercel.app/)** — 브라우저에서 바로 실행 (60fps, 데스크톱 권장)

| | |
|---|---|
| ![Status](https://img.shields.io/badge/Status-Live-22C55E?style=flat-square) | ![Stack](https://img.shields.io/badge/Stack-Canvas_+_Verlet-FF6B6B?style=flat-square) |
| ![Live](https://img.shields.io/badge/Live-Demo-7C3AED?style=for-the-badge&logo=vercel&logoColor=white) | [![Repo](https://img.shields.io/badge/GitHub-sigco3111%2Fcloth--simulation-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/sigco3111/cloth-simulation) |
| ![License](https://img.shields.io/badge/License-MIT-F1C40F?style=flat-square) | ![Deps](https://img.shields.io/badge/Dependencies-0-9CA3AF?style=flat-square) |

### 🎮 빠른 사용법
1. 위 데모 링크 클릭 → 브라우저에서 페이지 열기
2. **마우스 드래그** — 천의 임의 지점 잡아당기기
3. **세게 당기기** — constraint 임계값 초과 시 천이 찢어짐
4. 천이 자유낙하 + 바람 영향으로 자연스럽게 펄럭이는 모습 감상

---

## 🤖 생성 정보 (Attribution)

이 프로젝트의 코드는 아래 모델과 프롬프트를 이용해 **자동으로 생성**되었습니다.

| 항목 | 값 |
|---|---|
| **모델** | MiniMax-M3 |
| **실행 환경** | OpenCode CLI |
| **저장소** | [`sigco3111/cloth-simulation`](https://github.com/sigco3111/cloth-simulation) |
| **라이선스** | MIT |
| **의존성** | 없음 (Vanilla JS + Canvas 2D, 단일 HTML) |

### 📝 사용된 프롬프트 (원문)

```
HTML5 Canvas와 Verlet Integration 알고리즘을 사용하여 마우스로 잡아서 당기면 물리적으로 늘어나고 세게 당기면 찢어지는
붉은색 벨벳 질감의 천(Cloth) 시뮬레이션을 구현하되, 바람의 영향으로 천이 자연스럽게 펄럭이는 효과와 중력 모델을 정교하게 적용해줘.
Implementation Advice: Use HTML5 Canvas. Implement Verlet Integration for the physics (points and constraints).
To "tear" the cloth, check if the distance between two points in a constraint exceeds a threshold, then remove that constraint.
모든 의존관계의 코드를 하나의 HTML에 담는 형태로 코드 작성.
```

---

## ✨ 주요 특징 (Features)

- 🧶 **32×42 격자 (1,344점)** — 구조·전단 이중 constraint로 천 직조
- 🖱️ **마우스 드래그** — nearest-point pick + 위치 스냅 + soft spring
- 💥 **찢어짐 (Tearing)** — constraint 거리 임계값 초과 시 자동 분리, 양쪽 자유 시뮬레이션
- 🎨 **5-pass Velvet 셰이딩** — per-quad anisotropic BRDF (ambient + diffuse + sheen + backlit + rim) + ImageData 노이즈 오버레이
- 💨 **바람** — 시간/공간 이중 sin 패턴 + 방향 반전 + gust
- ⚡ **60fps** — `requestAnimationFrame` + fixed dt substep, 4×0.75 constraint relaxation (~98%)
- 📦 **단일 HTML** — 외부 의존성 0개, 파일 하나만 열면 실행
- 🎛️ **실시간 UI** — Wind / Gravity / Tear 슬라이더, Drop / Re-Pin / Reset 버튼

---

## 🚀 실행 방법 (Quick Start)

### 방법 1: 라이브 데모 (Vercel) — 가장 간단
위 Live Demo 링크 클릭 → 별도 설치 없이 바로 확인 가능합니다.

### 방법 2: 그냥 브라우저로 열기
```bash
git clone https://github.com/sigco3111/cloth-simulation.git
cd cloth-simulation
open index.html        # macOS
xdg-open index.html    # Linux
start index.html       # Windows
```

### 방법 3: 로컬 서버 (권장, 모바일 호환)
```bash
python3 -m http.server 8000
# → http://localhost:8000
```

**인터넷 연결 불필요** — 모든 자원(폰트·노이즈 패턴·컨트롤)이 단일 HTML에 내장되어 있습니다.

---

## 🎮 조작법 (Controls)

| 입력 | 효과 |
|---|---|
| **마우스 이동** | 천 위에서 cursor halo (반경 표시) |
| **마우스 드래그 (mousedown + move)** | 천의 가장 가까운 점을 잡고 끌기 (soft spring) |
| **세게 당기기** | constraint 임계값 초과 시 천이 찢어짐 (자유 낙하 시작) |
| **마우스 떼기** | 잡은 점이 자유 시뮬레이션으로 복귀 |

### UI 컨트롤

| 컨트롤 | 범위 | 기본값 | 효과 |
|---|---|---|---|
| **Wind** 슬라이더 | 0 – 100% | ~50% | 바람 세기 (per-frame 가속도 진폭) |
| **Gravity** 슬라이더 | 0.0g – 2.0g | 1.0g | 중력 배율 (기본 900 px/s² × multiplier) |
| **Tear** 슬라이더 | 100 – 400% (rest length 대비) | ~180% | 찢어지는 임계값 (낮을수록 쉽게 찢김) |
| **Drop** 버튼 | — | — | 모든 핀을 해제하고 천을 자유낙하 |
| **Re-Pin** 버튼 | — | — | 상단 행을 다시 고정 |
| **Reset** 버튼 | — | — | 천을 초기 상태로 재생성 |

---

## 🛠️ 기술 스택 (Tech Stack)

| 영역 | 사용 기술 |
|---|---|
| **렌더링** | HTML5 Canvas 2D Context, 5-pass draw pipeline (BRDF + velvet nap overlay) |
| **물리** | Verlet Integration (Jakobsen-style constraint relaxation) |
| **데이터 구조** | `Point`(x, y, px, py, ax, ay, pinned) + `Constraint`(a, b, restLength, torn) 객체 |
| **마우스 입력** | pointer events + nearest-point pick + soft spring snap |
| **벨벳 셰이딩** | ambient + diffuse + sheen + backlit + rim (5 BRDF 컴포넌트) + procedural noise nap |
| **바람 모델** | dual sin(시간, 공간) + 위치 기반 gust + 방향 반전 |
| **루프** | `requestAnimationFrame` + fixed dt substep, accumulator 패턴 |
| **의존성** | 없음 (Vanilla JS) |

---

## 📂 프로젝트 구조

```
cloth-simulation/
├── index.html          # 단일 HTML (Canvas + Verlet + 셰이더 5-pass + UI)
├── README.md           # 본 문서 (한국어)
├── README.en.md        # English version
├── LICENSE             # MIT License
└── .gitignore          # Node/IDE 임시 파일 + .vercel/ 제외
```

---

## 🎨 디자인 결정 (Design Choices)

브레인스토밍 단계에서 내린 결정 4가지:

| 결정 포인트 | 선택 | 이유 |
|---|---|---|
| **렌더링 패스 수** | 5-pass (solid → highlight → pin → grabbed → cursor halo) | 한 번의 fillStyle 호출로 끝내지 않고 단계별로 분리해 진주 광택·섀도·집게 표시를 자연스럽게 합성 |
| **벨벳 톤 표현** | anisotropic BRDF 5성분 + procedural nap overlay | 단순 Lambert만으로는 벨벳 특유의 시야각 의존 광택(sheen, rim)을 못 만들어 ImageData 노이즈로 미세 광택을 보강 |
| **물리 안정성** | fixed dt substep + 4×0.75 stiffness + 3-pass damping | 한 프레임에서 큰 변위가 생길 때 Constraint relaxation이 수렴하지 못해 폭주하는 문제를 dt를 잘게 쪼개고 반복 횟수를 늘려 해결 |
| **바람 패턴** | dual sin(t) × sin(space) + gust + 방향 반전 | 단일 sin만으로는 "한쪽 방향으로 흔들리는 천"처럼 균일해 풍선 같은 효과를 못 만듦. 시·공간 이중 sin에 위치별 gust와 ±주기로 방향 반전을 더해 자연스러운 펄럭임 구현 |

### 직접 커스터마이즈하고 싶다면

`index.html` 상단 `CONFIG` 영역에서 다음 상수를 조정하면 분위기를 바꿀 수 있어요:

```js
const CONFIG = {
  GRID_W: 32,           // 가로 점 수
  GRID_H: 42,           // 세로 점 수
  SPACING: 12,          // 점 사이 거리 (px)
  TEAR_THRESHOLD: 1.8,  // rest length 대비 찢어지는 비율 (낮을수록 쉽게 찢김)
  WIND_BASE: 0.5,       // 바람 기본 세기
  GRAVITY: 900,         // 중력 (px/s²)
  CONSTRAINT_ITERS: 4,  // constraint relaxation 반복 (안정성 vs 비용)
  DAMPING: 0.5,         // 0~1, 1에 가까울수록 무한히 천이 흔들림
  // ... 더 많은 옵션은 코드 내 주석 참조
};
```

고급 사용자용: `class Cloth` 안의 `step()` 메서드를 교체해 semi-implicit Euler나 Position Based Dynamics (PBD)로 바꿔볼 수도 있어요. `Constraint` 배열의 tearing 로직을 수정해 "천이 한 번 찢기면 끝"이 아니라 "천이 천천히 무너지다" 식으로 바꿔볼 수도 있습니다.

---

## 📜 License

MIT © 2026 sigco3111

---

## 🙏 Acknowledgments

이 프로젝트는 [MiniMax-M3](https://example.com) 모델과 OpenCode CLI 환경에서 생성되었습니다. 프롬프트 엔지니어링과 디자인 결정은 저장소 소유자가 직접 수행했습니다.

- **코딩미션 참조 페이지**: [cokac.com — 코드깎는노인](https://cokac.com/list/announcement/24)
- **이전 미션 README 템플릿**: [sigco3111/neon-fluid](https://github.com/sigco3111/neon-fluid)

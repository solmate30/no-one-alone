# CLAUDE.md
> Created: 2026-05-08 17:45
> Last Updated: 2026-05-13 12:30

> **Current phase: Proposal (2026-05-31 deadline). No application code exists.**
> Coding conventions, security rules, and performance targets in this file are for reference only — they activate at finals entry (2026-07-01).

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

---

## Project Overview

**Solmate** (repo: `no-one-alone`) is a welfare crisis detection platform for the 2026 Blockchain & AI Hackathon (Track 2). The tagline: "국가가 못 찾는 사람을, AI가 찾고, 복지가 닿고, 블록체인이 증명한다."

Core pipeline: **OmniOne CX 가입·로그인 본인확인 → Soli AI 정기 안부 감지 → Soli 복지 매칭 → 담당자 대시보드 승인 → 집행 직전 본인 재확인 → Open DID VC/VP + OmniOne Chain txId 기록**

**Current state**: Proposal/documentation phase only. No application code exists. Proposal submission deadline: **2026-05-31**. Finals MVP development runs 2026-07-01 ~ 2026-09-21 if the team advances.

---

## Docs-First Principle

**Documentation must be complete before any implementation begins.** This is not optional — it is the primary workflow rule for this project. Future Claude instances working on this repo must follow this sequence:

1. Read the relevant layer docs before writing any code or creating any document.
2. If a required document does not exist, create it first (using the rules below).
3. If a document needs updating, update it before modifying the code it describes.
4. Do not write code for a feature unless the corresponding Screen Flow, API Spec, and DB Schema documents are complete.

The reason: the proposal phase and the finals implementation phase are linked. Every implementation decision must trace back to a documented design. Undocumented code choices cannot be verified against the proposal scoring criteria (Creativity 35 / Feasibility 35 / Business 30).

---

## Repository Structure

```
/
├── docs/                         — 5-layer documentation (primary workspace)
│   ├── 01_Concept_Design/        — Vision, Lean Canvas, Product Specs, Pitch Deck
│   ├── 02_UI_Screens/            — Screen flows, UI design system
│   ├── 03_Technical_Specs/       — DB schema, API specs, dev principles
│   ├── 04_Logic_Progress/        — Roadmap, backlog, execution plans
│   └── 05_QA_Validation/         — Test scenarios, QA checklists
├── refs/                         — Hackathon guidebook + PPTX template (read-only reference)
└── .agent/skills/                — AI agent skill definitions (local only, not committed)
```

---

## 5-Layer Documentation System

### Layer responsibilities

| # | Path | Owned documents | Purpose |
|:--|:---|:---|:---|
| 1 | `docs/01_Concept_Design/` | `01_VISION_CORE.md`, `02_LEAN_CANVAS.md`, `03_PRODUCT_SPECS.md`, `04_PITCH_DECK.md` | What we build and why — vision, business model, MVP scope |
| 2 | `docs/02_UI_Screens/` | `00_SCREEN_FLOW.md`, `01_UI_DESIGN.md` | How users experience it — screen flows, component list, UX rules |
| 3 | `docs/03_Technical_Specs/` | `00_DEVELOPMENT_PRINCIPLES.md`, `01_DB_SCHEMA.md`, `02_API_SPECS.md` | How it is built — DB tables, API contracts, coding rules |
| 4 | `docs/04_Logic_Progress/` | `00_BACKLOG.md`, `00_ROADMAP.md` | When and what — milestones, task tracking |
| 5 | `docs/05_QA_Validation/` | `01_TEST_SCENARIOS.md`, `02_QA_CHECKLIST.md` | Whether it works — test criteria, submission checklist |

### Information flow (top-down)

```
01_Concept_Design  →  02_UI_Screens  →  03_Technical_Specs  →  04_Logic_Progress  →  05_QA_Validation
```

A change in a higher layer propagates down. If `03_PRODUCT_SPECS.md` changes the MVP scope, `00_SCREEN_FLOW.md`, `02_API_SPECS.md`, and `00_BACKLOG.md` must be updated to reflect it. Never let layers fall out of sync.

### Standard file names for Layer 4

| File | Purpose |
|:---|:---|
| `00_BACKLOG.md` | Task tracking — ToDo / In Progress / Done with checkboxes |
| `00_ROADMAP.md` | Milestones and phase-level schedule |
| `01_EXECUTION_PLAN.md` | Concrete implementation steps with checkboxes (created at finals entry) |

---

## Documentation Quality Framework (365 Principle)

All documents must be designed and verified against this framework:

**3 Investor Lenses** (used in `04_PITCH_DECK.md` internal check):
- **Leverage**: Does the system create network effects or data moats?
- **Realistic Money Flow**: Is the revenue path credible and sequenced correctly?
- **Defensibility**: What makes the data or position hard to replicate?

**6 Global Rubric** (all docs must address the relevant criteria):
1. Functionality — does it actually work? is the code clean?
2. Potential Impact — is the TAM large? does it contribute to an ecosystem?
3. Novelty — is the combination genuinely new?
4. UX — does the design reflect the performance requirement (e.g., 400ms responsiveness)?
5. Open-source — can other builders reuse components?
6. Business Plan — is the revenue model sustainable?

`05_QA_Validation` layer documents must include all 6 rubric criteria explicitly.

---

## Document Writing Rules

### Metadata (required on every document)

```markdown
# [Document Title]
> Created: YYYY-MM-DD HH:mm
> Last Updated: YYYY-MM-DD HH:mm
```

If a document has associated backlog items, add them on the next line:
```markdown
> Backlog: P-01, T-03, M-02
```

Update `Last Updated` when making a substantial content change. Tiny typo, spacing, or formatting-only edits may keep the existing timestamp.

### Related Documents section (required at end of every document)

```markdown
## Related Documents
- **Layer_Name**: [Title](./relative/path.md) — relationship description
```

Use relative paths. Same layer: `./02_LEAN_CANVAS.md`. Different layer: `../01_Concept_Design/03_PRODUCT_SPECS.md`. Include a one-line description of the relationship.

### Writing discipline

- **Ask before Write**: Before drafting a new document or section, identify and state the key design decisions that need to be made. Do not write a full draft before the scope is clear.
- **No overwrite**: Always read an existing document fully before editing. Update and extend; do not replace.
- **No emoji** anywhere in documentation.
- Place new planning/schedule documents in `04_Logic_Progress/`, not anywhere else.
- All checklist items in `04_Logic_Progress/` must use `[ ]` checkboxes and be atomic (one action per item).

### Backlog ID system

Documents reference backlog tasks by ID. The ID format encodes the category:

| Prefix | Category |
|:---|:---|
| `P-xx` | Proposal writing tasks |
| `T-xx` | Technical spec tasks |
| `M-xx` | MVP implementation tasks |
| `D-xx` | Document/design tasks |
| `Q-xx` | QA and validation tasks |

When creating or referencing a task, use the ID consistently across docs. The authoritative list lives in `docs/04_Logic_Progress/00_BACKLOG.md`.

---

## Implementation Gate (Before Writing Any Code)

Before starting any feature implementation, confirm:

- [ ] `01_Concept_Design/03_PRODUCT_SPECS.md` includes this feature in the finals MVP scope
- [ ] `02_UI_Screens/00_SCREEN_FLOW.md` defines all screens for this feature
- [ ] `02_UI_Screens/01_UI_DESIGN.md` defines the components involved
- [ ] `03_Technical_Specs/01_DB_SCHEMA.md` defines the tables this feature reads/writes
- [ ] `03_Technical_Specs/02_API_SPECS.md` defines the API endpoints this feature calls
- [ ] `04_Logic_Progress/00_BACKLOG.md` has a task item for this feature with an ID

If any of these is missing, complete the document first.

---

## Planned Tech Stack (Finals MVP)

| Layer | Technology |
|:---|:---|
| Frontend | Next.js 14+ App Router + TypeScript — in `/web` |
| Backend | NestJS + PostgreSQL 16+ — in `/server` |
| ORM | Drizzle ORM (`server/drizzle/schema.ts`) |
| AI | Claude API — latest Sonnet model (confirm at finals entry) |
| Auth | OmniOne CX (mobile ID / DID), Open DID |
| Blockchain | OmniOne Chain |
| Infra | Vercel (frontend) + AWS (backend) |

### Frontend directory structure (planned)

```
web/
├── app/
│   ├── (user)/             — 대상자 웹 화면 라우트 (Soli 정기 안부, Soli 복지 매칭)
│   ├── (dashboard)/        — 담당자 대시보드 (우선순위 리스트, 케이스 상세, 집행)
│   └── api/                — Next.js BFF API Routes
├── components/
│   ├── soli/               — Soli 챗봇 컴포넌트
│   ├── auth/               — OmniOne CX 인증 컴포넌트
│   └── chain/              — 온체인 기록 표시 컴포넌트
└── lib/
    ├── api.ts              — API 클라이언트
    └── omni-cx.ts          — OmniOne CX SDK 래퍼
```

### Backend directory structure (planned)

```
server/src/
├── auth/       — OmniOne CX DID 인증, JWT 발급
├── crisis/     — 위기도 스코어링
├── soli/       — Claude API 챗봇
├── targets/    — 정기 안부 대상자 등록
├── welfare/    — Soli 복지 매칭
├── dashboard/  — 담당자 대시보드
├── chain/      — OmniOne Chain 연동
└── csr/        — 파일럿 이후 CSR 기부·ESG 리포트 후보 모듈
```

Coding conventions, security rules, and performance targets: see [`docs/03_Technical_Specs/00_DEVELOPMENT_PRINCIPLES.md`](./docs/03_Technical_Specs/00_DEVELOPMENT_PRINCIPLES.md).

---

## UI Design System (from `docs/02_UI_Screens/`)

### Breakpoints

- **Citizen app**: mobile-first, base 375px
- **Officer dashboard**: desktop-first, base 1280px

### Accessibility

- Font: 16px minimum body, 20px+ headings (citizen app)
- Touch targets: 44×44px minimum
- Color contrast: WCAG AA (4.5:1 minimum)
- Keyboard: full keyboard navigation required on dashboard

### Soli crisis score thresholds

| Score | Level | Soli behavior | UI change |
|:---|:---|:---|:---|
| 0–3 | 정상 | 일반 대화 유지 | 없음 |
| 4–6 | 주의 | 복지 도움 제안 | 복지 제안 카드 표시 |
| 7–8 | 경고 | 전문가 연결 제안 | 상담 연결 버튼 강조 |
| 9–10 | 위급 | 즉시 담당자 알림 발송 | 긴급 알림 UI |

---

## Git Conventions

**Branch strategy**: `main` (deploy) → `develop` (integration) → `feat/[설명]` / `fix/[설명]` / `docs/[설명]`

**Commit format** — Conventional Commits, Korean subject, minimum 3 detail lines:
```
feat(auth): OmniOne CX 본인 확인 연동

- POST /auth/omni-cx/verify 엔드포인트에 검증 결과 처리 추가
- OmniOne CX SDK 콜백 처리 후 DID 해시 저장
- 인증 실패 시 403 에러 반환 처리
```

Types: `feat` / `fix` / `chore` / `docs` / `refactor` / `test`

---

## Hackathon Scoring Context

The proposal is scored: **Creativity 35 / Feasibility 35 / Business 30**. Every document and every implementation decision should strengthen one of these three axes. When in doubt about what to build or document next, ask which axis it serves most.

Key differentiators to preserve across all docs and code:
- OmniOne CX mobile ID used at 2 trust points: sign-up/login, execution recipient
- Open DID for beneficiary VC issuance and VP verification (+5% bonus)
- OmniOne Chain for VC metadata and execution proof txId (+5% bonus)
- Soli AI as proactive first contact — not a reactive chatbot
- Social isolation data moat (crisis scores, response gaps, officer feedback) — defensibility argument

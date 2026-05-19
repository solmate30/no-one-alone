# Document Index — no-one-alone
> Created: 2026-05-08 17:35
> Last Updated: 2026-05-20 13:00
> Backlog: D-01

## 1. 목적

이 문서는 no-one-alone의 공유 문서가 어떤 백로그 작업과 연결되는지 추적하는 문서 지도다. 앞으로 새 문서를 만들거나 기존 문서를 수정할 때는 [Backlog](./04_Logic_Progress/00_BACKLOG.md)의 관련 ID와 이 인덱스를 함께 갱신한다.

모든 AI 에이전트는 루트 [AGENTS.md](../AGENTS.md)를 먼저 읽고, 도구별 세부 지침이 있으면 해당 파일을 보조로 참조한다.

## 2. 문서 연결 규칙

문서 업데이트는 아래 조건을 만족해야 완료로 본다.

1. 문서 본문 작성 또는 수정
2. 문서 하단 `Related Documents` 갱신
3. [Backlog](./04_Logic_Progress/00_BACKLOG.md)의 관련 작업 카드에 참조 문서 또는 생성/업데이트 문서로 연결
4. 이 인덱스의 `관련 백로그` 칸에 해당 작업 ID 반영

새 문서가 아직 어느 작업에 속하는지 불명확하면 문서를 작성하기 전에 다음을 먼저 결정한다.

- 기존 백로그 ID에 붙일 것인가
- 새 백로그 ID를 만들 것인가
- 구현 전 필수 참조 문서인가, 구현 결과 기록 문서인가

## 3. 백로그 ID 요약

| Prefix | 의미 |
|:---|:---|
| `P-*` | 2026년 5월 공모 제안서 제출 작업 |
| `D-*` | 개념, 전략, 문서 구조 정리 작업 |
| `T-*` | 기술 조사 및 기술 명세 작업 |
| `M-*` | MVP 구현 작업 |
| `Q-*` | QA, 검증, 발표 준비 작업 |

## 4. 문서 지도

| 문서 | 레이어 | 관련 백로그 | 용도 |
|:---|:---|:---|:---|
| [AGENTS.md](../AGENTS.md) | Root | `D-01` | 모든 AI 에이전트가 따라야 하는 공통 repo-level 작업 규칙. |
| [Backlog](./04_Logic_Progress/00_BACKLOG.md) | Logic_Progress | 전체 | 작업 허브. 모든 문서와 구현 작업은 여기의 ID를 기준으로 추적한다. |
| [Roadmap](./04_Logic_Progress/00_ROADMAP.md) | Logic_Progress | `P-06`, `Q-04` | 해커톤 일정, 장기 성장 단계, 수익 목표 기준. |
| [Vision & Core Values](./01_Concept_Design/01_VISION_CORE.md) | Concept_Design | `P-02`, `P-03`, `D-02` | 핵심 비전, 미션, 타겟 오디언스, 장기 방향성. |
| [Lean Canvas](./01_Concept_Design/02_LEAN_CANVAS.md) | Concept_Design | `P-02`, `P-03`, `P-06`, `D-02` | 문제, 고객 세그먼트, UVP, 수익 구조, 핵심 지표. |
| [Product Specs](./01_Concept_Design/03_PRODUCT_SPECS.md) | Concept_Design | `P-01`, `P-02`, `P-04`, `P-05`, `T-01`, `T-02`, `T-03`, `T-04`, `M-01`, `M-02`, `M-03`, `M-04`, `M-05`, `M-06` | MVP 범위, 핵심 기능, Track 2 필수·선택 조건. |
| [Proposal Deck](./01_Concept_Design/04_PITCH_DECK.md) | Concept_Design | `P-01`, `P-02`, `P-03`, `P-04`, `P-05`, `P-06`, `P-07`, `D-02`, `D-03`, `T-04`, `M-06`, `Q-02`, `Q-03` | 공모 제안서 본문, 요약서, 발표 흐름의 기준 문서. |
| [Field Outreach Strategy](./01_Concept_Design/05_FIELD_OUTREACH_STRATEGY.md) | Concept_Design | `P-03`, `P-04`, `P-06`, `P-07`, `D-05`, `M-01`, `M-02`, `M-04`, `M-06` | 55세 이상 시니어 현장 접점, 동의 기반 안부 연결, 마케팅·도입 시나리오, 구현 설계 입력. |
| [Pitch Deck HTML Preview](./01_Concept_Design/04_PITCH_DECK.html) | Concept_Design | `P-07`, `Q-02` | 공모 제안서 내용을 시각적으로 확인하기 위한 HTML 미리보기 산출물. |
| [Screen Flow](./02_UI_Screens/00_SCREEN_FLOW.md) | UI_Screens | `P-04`, `T-03`, `M-01`, `M-02`, `M-03`, `M-04` | 사용자별 화면 흐름과 핵심 플로우. |
| [UI Design](./02_UI_Screens/01_UI_DESIGN.md) | UI_Screens | `P-04`, `T-01`, `T-03`, `M-01`, `M-02`, `M-03`, `M-04` | 대상자 웹 화면, 담당자 대시보드, 솔이, 인증 UX 기준. |
| [Development Principles](./03_Technical_Specs/00_DEVELOPMENT_PRINCIPLES.md) | Technical_Specs | `D-01`, `P-05`, `T-01`, `T-02`, `M-01`, `M-05` | 기술 스택, 프로젝트 구조, 코딩 컨벤션, 보안 원칙. |
| [DB Schema](./03_Technical_Specs/01_DB_SCHEMA.md) | Technical_Specs | `T-01`, `T-02`, `T-03`, `M-02`, `M-03`, `M-04`, `M-05` | 데이터 모델, 인덱스, 온체인 기록 대상. |
| [API Specs](./03_Technical_Specs/02_API_SPECS.md) | Technical_Specs | `T-01`, `T-02`, `T-03`, `M-02`, `M-03`, `M-04`, `M-05` | 인증, 솔이, 위기도, 복지 매칭, 대시보드, 체인 API 계약. |
| [Blockchain DID Architecture](./03_Technical_Specs/04_BLOCKCHAIN_DID_ARCH.md) | Technical_Specs | `T-10` | OmniOne CX 연동 2개 신뢰 포인트, Open DID 컴포넌트 구성, VC/VP 라이프사이클, OmniOne Chain 온체인 기록 구조. |
| [Proposal Validation Scenarios](./05_QA_Validation/01_TEST_SCENARIOS.md) | QA_Validation | `P-05`, `T-03`, `M-02`, `M-04`, `Q-01`, `Q-03` | 창의성, 실현 가능성, 사업성, 발표 검증 시나리오. |
| [QA Checklist](./05_QA_Validation/02_QA_CHECKLIST.md) | QA_Validation | `P-07`, `D-03`, `T-04`, `M-01`, `M-02`, `M-03`, `M-05`, `M-06`, `Q-01`, `Q-02`, `Q-04` | 제출 전 점검, 내용 정합성, MVP 개발 단계 계획 검증. |
| [CLAUDE.md](../CLAUDE.md) | Root | `D-01` | Claude Code가 이 repo에서 작업할 때 참조하는 도구별 지침. |

## 5. 신규 문서 후보

아래 문서는 아직 없지만, 향후 토론 또는 구현 과정에서 필요해질 가능성이 높다. 생성 시 반드시 관련 백로그 ID를 확정한다.

| 후보 문서 | 권장 위치 | 관련 백로그 | 생성 조건 |
|:---|:---|:---|:---|
| `03_OMNIONE_CX_INTEGRATION.md` | `docs/03_Technical_Specs/` | `T-01`, `M-03`, `M-05` | OmniOne CX SDK 연동 방식이 구체화될 때 |
| `04_OPEN_DID_CHAIN_INTEGRATION.md` | `docs/03_Technical_Specs/` | `T-02`, `M-05` | Open DID, OmniOne Chain 기록 구조가 구체화될 때 |
| `01_SOLI_SCORING_LOGIC.md` | `docs/04_Logic_Progress/` | `T-03`, `M-02` | 위기 키워드와 스코어링 규칙을 구현 전 확정할 때 |
| `02_IMPLEMENTATION_DECISIONS.md` | `docs/04_Logic_Progress/` | `M-01` | MVP 개발 단계 진입 후 실제 코드 구조와 패턴을 확정할 때 |
| `03_DEMO_SCRIPT.md` | `docs/05_QA_Validation/` | `Q-03`, `Q-04` | 8분 발표와 최종 데모 흐름을 확정할 때 |

## Related Documents

- **Root**: [AGENTS.md](../AGENTS.md) — 모든 AI 에이전트의 공통 작업 규칙
- **Logic_Progress**: [Backlog](./04_Logic_Progress/00_BACKLOG.md) — 모든 작업 ID와 문서 연결의 기준
- **Logic_Progress**: [Roadmap](./04_Logic_Progress/00_ROADMAP.md) — 일정과 단계별 목표
- **Technical_Specs**: [Development Principles](./03_Technical_Specs/00_DEVELOPMENT_PRINCIPLES.md) — 문서와 구현이 따라야 할 개발 원칙
- **QA_Validation**: [QA Checklist](./05_QA_Validation/02_QA_CHECKLIST.md) — 제출 전 점검 기준

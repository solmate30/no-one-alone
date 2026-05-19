# Backlog — no-one-alone
> Created: 2026-05-08 01:39
> Last Updated: 2026-05-20 13:00
> Backlog: 전체

## 0. Backlog 운영 원칙

이 문서는 no-one-alone의 모든 제안서 작성, 문서 정리, MVP 구현 작업이 출발하는 작업 허브다. 앞으로 새 문서를 만들거나 기존 문서를 수정할 때는 반드시 관련 백로그 ID를 연결한다.

### 0-1. 문서 업데이트 완료 기준

문서 업데이트는 아래 3개가 끝나야 완료로 본다.

1. 문서 본문 작성 또는 수정
2. 문서 하단 `Related Documents` 갱신
3. 이 백로그의 관련 작업 카드에 참조 문서 또는 생성/업데이트 문서로 연결

### 0-2. 작업 카드 필드

각 작업은 가능한 한 아래 필드를 유지한다.

- 우선순위: High / Medium / Low
- 목표: 작업의 목적
- 작업 유형: Proposal / Documentation / Research / MVP Implementation / QA
- 필수 참조: 작업 전에 반드시 읽을 문서
- 생성/업데이트 문서: 이 작업으로 만들거나 수정할 문서
- 산출물: 실제 제출물, 문서, 코드, 화면, 검증 결과
- 완료 기준: [X]로 바꿀 수 있는 조건
- 구현 전 확인 질문: 코드 또는 세부 문서 작성 전에 사용자와 확인할 사항

### 0-3. 백로그 ID 체계

| Prefix | 의미 |
|:---|:---|
| `P-*` | 2026년 5월 공모 제안서 제출 작업 |
| `D-*` | 개념, 전략, 문서 구조 정리 작업 |
| `T-*` | 기술 조사 및 기술 명세 작업 |
| `M-*` | MVP 구현 작업 |
| `Q-*` | QA, 검증, 발표 준비 작업 |

---

## 1. 현재 상태

현재 no-one-alone은 **구현 전 설계 단계**다. 2026년 5월의 목표는 동작하는 MVP가 아니라, `refs/TrackNo_팀명_프로젝트명_yymmdd.pptx` 양식에 맞춘 공모 제안서 제출이다.

다만 Track 2는 MVP 모델 개발·시연을 요구하므로, 제안서에는 **5월 제출 계획**과 **MVP 개발 단계 2026-07-01 ~ 2026-09-21 구현 계획**을 함께 담는다.

---

## 2. 제안서 제출 마감 기준

| 단계 | 마감 | 산출물 | 관련 백로그 |
|:---|:---|:---|:---|
| Phase 1 제안서 골격 확정 | 2026-05-12 | 목차, 핵심 메시지, Track 2 선택 사유 | `P-01`, `P-02` |
| Phase 2 본문 작성 | 2026-05-18 | 목적·필요성, 상세 설명, 차별성, 기대효과 | `P-03`, `P-04`, `P-05`, `P-06` |
| Phase 3 수치·근거 검증 | 2026-05-22 | 통계 출처, 시장 근거, 개인정보/온체인 설명 | `D-03`, `T-01`, `T-02`, `Q-01` |
| Phase 4 PPTX 양식 반영 | 2026-05-26 | 제안 요약서, 10p 이내 본문, 관련 자료 | `P-07` |
| Phase 5 제출 전 점검 | 2026-05-30 | 오탈자, 분량, 8분 발표 가능성, 파일명 | `Q-02`, `Q-03` |
| 제출 | 2026-05-31 | 온라인 모집 마감 전 최종 제출 | `Q-04` |

---

## 3. 2026년 5월 제안서 제출 백로그

### [ ] P-01. 표지 및 제출 기본 정보 확정

- 우선순위: High
- 작업 유형: Proposal
- 목표: 공모 양식의 표지, Track, 참가 유형, 팀 정보를 확정한다.
- 필수 참조:
  - [Proposal Deck](../01_Concept_Design/04_PITCH_DECK.md) — 0. 작성 기준
  - [Product Specs](../01_Concept_Design/03_PRODUCT_SPECS.md) — 5-1. 5월 제안서 제출물
- 생성/업데이트 문서:
  - [Proposal Deck](../01_Concept_Design/04_PITCH_DECK.md)
- 산출물:
  - 팀명, 프로젝트명, 제출일, Track 2 표기, 참가 유형, 신청자·구성원 정보
- 완료 기준:
  - 표지 입력 정보가 공모 양식에 맞게 확정됨
  - 개인정보 입력 필요 항목과 공개 문서에 남길 항목이 분리됨

### [ ] P-02. 제안 요약서 2p 이내 작성

- 우선순위: High
- 작업 유형: Proposal
- 목표: 심사자가 2분 안에 문제, 해법, 기술 필연성, 사업성을 이해할 수 있는 요약서를 작성한다.
- 필수 참조:
  - [Proposal Deck](../01_Concept_Design/04_PITCH_DECK.md) — 2. 제안 요약서
  - [Vision & Core Values](../01_Concept_Design/01_VISION_CORE.md) — 1. 핵심 비전, 2. 미션
  - [Lean Canvas](../01_Concept_Design/02_LEAN_CANVAS.md) — 1. Problem, 3. Unique Value Proposition, 6. Revenue Streams
  - [Product Specs](../01_Concept_Design/03_PRODUCT_SPECS.md) — 3. 핵심 기능 명세
- 생성/업데이트 문서:
  - [Proposal Deck](../01_Concept_Design/04_PITCH_DECK.md)
- 산출물:
  - 제안 요약서 2p 이내 문안
- 완료 기준:
  - Track 2 선택 이유가 명시됨
  - 창의성, 실현 가능성, 사업성 메시지가 모두 포함됨
  - "AI가 찾고, 복지가 닿고, 블록체인이 증명한다" 태그라인이 일관되게 반영됨

### [ ] P-03. 목적 및 필요성 작성

- 우선순위: High
- 작업 유형: Proposal
- 목표: 고독사·복지 사각지대 문제와 기존 대응 방식의 한계를 설득력 있게 정리한다.
- 필수 참조:
  - [Proposal Deck](../01_Concept_Design/04_PITCH_DECK.md) — 3. 제안내용의 목적 및 필요성
  - [Vision & Core Values](../01_Concept_Design/01_VISION_CORE.md) — 3. 타겟 오디언스, 4. 핵심 가치
  - [Lean Canvas](../01_Concept_Design/02_LEAN_CANVAS.md) — 1. Problem, 2. Customer Segments
  - [Field Outreach Strategy](../01_Concept_Design/05_FIELD_OUTREACH_STRATEGY.md) — 55세 이상 현장 접점과 낙인 완화 프레이밍
- 생성/업데이트 문서:
  - [Proposal Deck](../01_Concept_Design/04_PITCH_DECK.md)
  - [Lean Canvas](../01_Concept_Design/02_LEAN_CANVAS.md)
  - [Field Outreach Strategy](../01_Concept_Design/05_FIELD_OUTREACH_STRATEGY.md)
- 산출물:
  - 목적 및 필요성 본문 문안
  - 문제 근거와 출처 목록
- 완료 기준:
  - 대상 사용자와 사각지대 발생 원인이 분리되어 설명됨
  - 통계 또는 공신력 있는 근거가 필요한 문장에 표시가 남아 있음

### [ ] P-04. 제안내용 상세 설명 작성

- 우선순위: High
- 작업 유형: Proposal
- 목표: 대상자 웹 화면, 솔이 전화·SMS·웹 채팅 선택 채널, 담당자 대시보드, OmniOne Chain 기록을 하나의 실행 파이프라인으로 설명한다.
- 필수 참조:
  - [Proposal Deck](../01_Concept_Design/04_PITCH_DECK.md) — 4. 제안내용의 상세 설명
  - [Product Specs](../01_Concept_Design/03_PRODUCT_SPECS.md) — 3. 핵심 기능 명세
  - [Field Outreach Strategy](../01_Concept_Design/05_FIELD_OUTREACH_STRATEGY.md) — 주민센터부터 솔이 정기 전화, 담당자 확인까지의 현장 흐름
  - [Screen Flow](../02_UI_Screens/00_SCREEN_FLOW.md) — 1. 전체 화면 구조
  - [UI Design](../02_UI_Screens/01_UI_DESIGN.md) — 2. 사용자 유형별 UI 원칙, 3. 솔이 전화 및 SMS·웹 채팅 UX 설계
- 생성/업데이트 문서:
  - [Proposal Deck](../01_Concept_Design/04_PITCH_DECK.md)
  - [Field Outreach Strategy](../01_Concept_Design/05_FIELD_OUTREACH_STRATEGY.md)
  - [Screen Flow](../02_UI_Screens/00_SCREEN_FLOW.md)
- 산출물:
  - 전체 파이프라인 설명
  - 핵심 기능 요약표
- 완료 기준:
  - 솔이 감지에서 담당자 승인, 온체인 기록까지의 흐름이 끊기지 않음
  - MVP 범위와 장기 비전이 혼동되지 않음

### [ ] P-05. 차별성 및 심사 기준 대응 정리

- 우선순위: High
- 작업 유형: Proposal
- 목표: 창의성 35점, 실현 가능성 35점, 사업성 30점에 직접 대응하는 메시지를 만든다.
- 필수 참조:
  - [Proposal Deck](../01_Concept_Design/04_PITCH_DECK.md) — 5. 제안내용의 차별성
  - [Proposal Validation Scenarios](../05_QA_Validation/01_TEST_SCENARIOS.md) — 2. 창의성 검증, 3. 실현 가능성 검증, 4. 사업성 검증
  - [Product Specs](../01_Concept_Design/03_PRODUCT_SPECS.md) — 4. 필수조건 충족, 5. MVP 범위
  - [Development Principles](../03_Technical_Specs/00_DEVELOPMENT_PRINCIPLES.md) — 1. 기술 스택, 5. 보안 원칙
- 생성/업데이트 문서:
  - [Proposal Deck](../01_Concept_Design/04_PITCH_DECK.md)
  - [Proposal Validation Scenarios](../05_QA_Validation/01_TEST_SCENARIOS.md)
- 산출물:
  - 심사 기준별 대응 문장
  - 기존 시스템 대비 차별성 표
- 완료 기준:
  - 모바일 신분증 필수조건과 Open DID/OmniOne Chain 선택조건이 명확히 드러남
  - MVP 개발 단계 기간 내 구현 가능한 범위와 제외 범위가 분리됨

### [ ] P-06. 기대효과 및 사업화 계획 정리

- 우선순위: Medium
- 작업 유형: Proposal
- 목표: 사회적 효과와 지속 가능한 수익 구조를 함께 설명한다.
- 필수 참조:
  - [Proposal Deck](../01_Concept_Design/04_PITCH_DECK.md) — 6. 기대효과와 사업화
  - [Lean Canvas](../01_Concept_Design/02_LEAN_CANVAS.md) — 6. Revenue Streams, 8. Key Metrics, 9. Unfair Advantage
  - [Field Outreach Strategy](../01_Concept_Design/05_FIELD_OUTREACH_STRATEGY.md) — B2G 현장 도입 채널과 운영 패키지
  - [Roadmap](./00_ROADMAP.md) — 2. 생존 단계, 3. 검증 단계, 7. 수익 목표 요약
- 생성/업데이트 문서:
  - [Proposal Deck](../01_Concept_Design/04_PITCH_DECK.md)
  - [Field Outreach Strategy](../01_Concept_Design/05_FIELD_OUTREACH_STRATEGY.md)
  - [Roadmap](./00_ROADMAP.md)
- 산출물:
  - 정량 목표
  - B2G SaaS, 보험사 공동 실증, 비식별 데이터 상품 수익 구조 요약
- 완료 기준:
  - 수익 모델이 제안서 분량 안에서 현실적으로 축약됨
  - 3년 파일럿 기준 KPI가 제시됨

### [ ] P-07. PPTX 양식 이식

- 우선순위: High
- 작업 유형: Proposal
- 목표: 확정된 문구를 `refs/TrackNo_팀명_프로젝트명_yymmdd.pptx` 양식에 맞춰 반영한다.
- 필수 참조:
  - [Proposal Deck](../01_Concept_Design/04_PITCH_DECK.md) — 전체
  - [Field Outreach Strategy](../01_Concept_Design/05_FIELD_OUTREACH_STRATEGY.md) — 55세 이상 현장 접점, 극적 시나리오, 발표용 문장
  - [QA Checklist](../05_QA_Validation/02_QA_CHECKLIST.md) — 1. 양식 준수, 7. 제출 전 최종 확인
- 생성/업데이트 문서:
  - [Proposal Deck](../01_Concept_Design/04_PITCH_DECK.md)
  - [Field Outreach Strategy](../01_Concept_Design/05_FIELD_OUTREACH_STRATEGY.md)
  - [QA Checklist](../05_QA_Validation/02_QA_CHECKLIST.md)
- 산출물:
  - 제출용 PPTX
  - PPTX에 들어간 최종 문구와 원문 문서 간 대응표
- 완료 기준:
  - 제안 요약서 2p 이내
  - 본문 10p 이내
  - 55세 이상 현장 접점과 동의 기반 안전망 메시지가 PPTX 본문 또는 발표 흐름에 반영됨
  - 파일명 규칙 충족
  - 8분 발표 흐름과 맞음

---

## 4. 문서 체계 및 지식 정리 백로그

### [ ] D-01. 문서 인덱스와 백로그 연결 체계 유지

- 우선순위: High
- 작업 유형: Documentation
- 목표: 새 문서가 생길 때마다 백로그와 누락 없이 연결되는 구조를 유지한다.
- 필수 참조:
  - [Document Index](../00_DOCUMENT_INDEX.md)
  - [Development Principles](../03_Technical_Specs/00_DEVELOPMENT_PRINCIPLES.md) — 4-4. 브랜치 전략
- 생성/업데이트 문서:
  - [AGENTS.md](../../AGENTS.md)
  - [CLAUDE.md](../../CLAUDE.md)
  - [Document Index](../00_DOCUMENT_INDEX.md)
  - [Backlog](./00_BACKLOG.md)
- 산출물:
  - 문서별 관련 백로그 ID 표
  - 문서 업데이트 완료 기준
- 완료 기준:
  - 모든 공유 문서가 최소 1개 이상의 백로그 ID에 연결됨
  - 새 문서 작성 시 백로그 연결 규칙이 명시됨

### [X] D-02. 제안서 원문과 5-Layer 문서 동기화

- 우선순위: High
- 작업 유형: Documentation
- 목표: 제안서 원문의 핵심 내용을 5-Layer 문서 구조와 정합성 있게 맞춘다. (solmate_hackathon_proposal.md는 삭제됨. 내용이 04_PITCH_DECK.md로 이식 완료)
- 필수 참조:
  - [Vision & Core Values](../01_Concept_Design/01_VISION_CORE.md)
  - [Lean Canvas](../01_Concept_Design/02_LEAN_CANVAS.md)
  - [Product Specs](../01_Concept_Design/03_PRODUCT_SPECS.md)
  - [Proposal Deck](../01_Concept_Design/04_PITCH_DECK.md)
- 생성/업데이트 문서:
  - [Document Index](../00_DOCUMENT_INDEX.md)
  - [Proposal Deck](../01_Concept_Design/04_PITCH_DECK.md)
- 산출물:
  - 제안서 원문과 5-Layer 문서 간 대응 관계
- 완료 기준:
  - 원문에만 있고 docs에 없는 핵심 주장이 식별됨
  - docs에 반영된 항목과 미반영 항목이 구분됨

### [X] D-04. 솔이 1차 감지 전환 — 파이프라인 구조 변경

- 우선순위: High
- 작업 유형: Documentation
- 목표: 핵심 파이프라인을 "이웃 제보 1차 감지"에서 "솔이 AI 전화 + SMS·웹 채팅 선택 채널 1차 감지"로 전환하고 6개 문서에 반영한다.
- 변경 근거: 이웃 신고는 한국 문화에서 거부감이 높고 자발적 제보 동기가 약함. 솔이가 먼저 거는 전화와 SMS·웹 채팅 선택 채널이 위기를 감지하는 구조가 실현 가능성과 창의성 모두를 강화함. 이웃 제보 기능은 완전 제거 (Phase 2 커뮤니티 케어 채널로 재검토 가능).
- 새 태그라인: "사회복지사의 눈이 닿지 않는 곳을, AI가 찾고, 복지가 닿고, 블록체인이 증명한다"
- 생성/업데이트 문서:
  - [Vision & Core Values](../01_Concept_Design/01_VISION_CORE.md) — 태그라인, 파이프라인
  - [Product Specs](../01_Concept_Design/03_PRODUCT_SPECS.md) — 기능 순서, 스코어 가중치
  - [Screen Flow](../02_UI_Screens/00_SCREEN_FLOW.md) — 홈 구조, 이웃 제보 제거
  - [API Specs](../03_Technical_Specs/02_API_SPECS.md) — 솔이 Critical Path, 보조 채널 명시
  - [DB Schema](../03_Technical_Specs/01_DB_SCHEMA.md) — 스코어 가중치 주석
  - [Backlog](./00_BACKLOG.md) — 태스크 반영

### [ ] D-05. 55세 이상 시니어 현장 도입·마케팅 전략 정리

- 우선순위: High
- 작업 유형: Documentation
- 목표: 55세 이상 시니어가 실제 현장에서 NOA를 어떻게 알게 되고, 어떤 동의 과정을 거쳐 담당 공무원의 직접 지원으로 연결되는지 정리한다.
- 필수 참조:
  - [Vision & Core Values](../01_Concept_Design/01_VISION_CORE.md) — 핵심 비전과 타겟 오디언스
  - [Lean Canvas](../01_Concept_Design/02_LEAN_CANVAS.md) — 고객 세그먼트와 채널
  - [Product Specs](../01_Concept_Design/03_PRODUCT_SPECS.md) — 모바일 신분증, 솔이, 데이터 경계
  - [Proposal Deck](../01_Concept_Design/04_PITCH_DECK.md) — 제안서 본문과 발표 흐름
- 생성/업데이트 문서:
  - [Field Outreach Strategy](../01_Concept_Design/05_FIELD_OUTREACH_STRATEGY.md)
  - [Document Index](../00_DOCUMENT_INDEX.md)
  - [Backlog](./00_BACKLOG.md)
- 산출물:
  - 55세 이상 대상 범위와 낙인 완화 프레이밍
  - 주민센터·복지관·경로당·보건소·관리사무소·생활지원사 등 현장 접점
  - 발표용 극적 시나리오와 마케팅 문구
  - 제안서 반영 포인트
- 완료 기준:
  - 55세 이상 누구나 시작 가능한 안부 연결 구조가 명시됨
  - 모바일 신분증 본인확인과 동의 기반 정보 공유의 경계가 명확함
  - 주민센터부터 솔이 정기 전화·SMS·웹 채팅, 담당자 대시보드, 지원 연결까지의 현장 흐름이 설명됨
  - P-07 PPTX 이식과 M-01/M-02/M-04/M-06 구현 설계 참조로 연결됨
  - 현장 인터뷰로 검증해야 할 질문이 정리됨

### [ ] D-03. 근거 자료 및 출처 정리

- 우선순위: High
- 작업 유형: Research
- 목표: 문제 정의, 시장성, 정책 적합성, 개인정보·블록체인 설명에 필요한 근거 자료를 모은다.
- 필수 참조:
  - [Proposal Deck](../01_Concept_Design/04_PITCH_DECK.md) — 7. 제안내용 관련 자료
  - [Proposal Validation Scenarios](../05_QA_Validation/01_TEST_SCENARIOS.md) — 1. 검증 기준
  - [QA Checklist](../05_QA_Validation/02_QA_CHECKLIST.md) — 5. 내용 정합성
- 생성/업데이트 문서:
  - [Proposal Deck](../01_Concept_Design/04_PITCH_DECK.md)
  - [QA Checklist](../05_QA_Validation/02_QA_CHECKLIST.md)
- 산출물:
  - 통계 출처 목록
  - 제안서에 넣을 근거 문장
- 완료 기준:
  - 통계, 정책, 기술 근거가 출처와 함께 정리됨
  - 출처가 필요한 문장과 출처가 이미 확보된 문장이 구분됨

---

## 5. 기술 조사 및 기술 명세 백로그

### [ ] T-01. OmniOne CX 모바일 신분증 인증 구조 정리

- 우선순위: High
- 작업 유형: Research
- 목표: 모바일 신분증 인증을 제안서와 MVP에 어떻게 넣을지 정리한다.
- 기술 레퍼런스:
  - 제공: RaonSecure, 해커톤 SDK 직접 제공 (별도 오픈소스 없음)
  - 연동: 표준 인증창 호출 → 콜백으로 `{ did_hash, verified_at, id_type, result_code }` 수신
  - 사용 지점 2곳: 가입·로그인 / 집행 직전
  - 상세: [Development Principles](../03_Technical_Specs/00_DEVELOPMENT_PRINCIPLES.md) — 7-1. OmniOne CX
- 필수 참조:
  - [Product Specs](../01_Concept_Design/03_PRODUCT_SPECS.md) — 4. 필수조건 충족
  - [UI Design](../02_UI_Screens/01_UI_DESIGN.md) — 4. OmniOne CX 인증 UX 가이드라인
  - [API Specs](../03_Technical_Specs/02_API_SPECS.md) — 2. `/auth`
  - [DB Schema](../03_Technical_Specs/01_DB_SCHEMA.md) — 2-1. `users`
- 생성/업데이트 문서:
  - [Development Principles](../03_Technical_Specs/00_DEVELOPMENT_PRINCIPLES.md)
  - [API Specs](../03_Technical_Specs/02_API_SPECS.md)
- 산출물:
  - 인증 시작, 검증, 실패, 만료 흐름 정리
  - 제안서용 기술 설명 문장
- 완료 기준:
  - 필수조건 충족 지점이 명확함
  - 데모 모드와 실제 SDK 연동 모드가 구분됨

### [X] T-10. 블록체인·DID 아키텍처 상세 문서 작성

- 우선순위: High
- 작업 유형: Documentation
- 목표: Open DID 오픈소스(GitHub)의 실제 API를 검증한 뒤, OmniOne Chain·OmniOne CX·Open DID 컴포넌트 간 연동 아키텍처를 InsureConnect 수준으로 구체적으로 기술한다.
- 조사 범위:
  - Ledger Service API 실제 경로 확인 (`/api/v1/diddoc/register`, `/api/v1/vcmeta/register` 등)
  - Issuer Server P210 5단계 프로토콜, Verifier Server P310 4단계 프로토콜
  - TAS(Trust Anchor Server) 역할 및 P132 사용자 등록 흐름
  - Blockchain SDK 메서드명 (`registDidDoc`, `registVcMetadata` 등)
  - RBAC 지원 범위 (SDK 미지원, 애플리케이션 레벨 구현 필요)
- 생성/업데이트 문서:
  - [Blockchain DID Architecture](../03_Technical_Specs/04_BLOCKCHAIN_DID_ARCH.md) — 신규 생성
  - [Development Principles](../03_Technical_Specs/00_DEVELOPMENT_PRINCIPLES.md) — Ledger API 실제 경로 수정, Related Documents 추가
- 완료 기준:
  - [X] `04_BLOCKCHAIN_DID_ARCH.md` 작성 완료 (실제 API 기반)
  - [X] `00_DEVELOPMENT_PRINCIPLES.md` Ledger API 경로 수정 완료
  - [X] 백로그에 T-10 등록

### [ ] T-05. 공공마이데이터 위기 신호 보조 데이터 설계

- 우선순위: Medium
- 작업 유형: Research / Documentation
- 목표: 공공마이데이터를 위기 신호 보조 입력으로 활용하는 구조를 정의하고, MVP Mock 시연 방법과 파일럿 실연동 경로를 명확히 분리한다.
- 배경:
  - 건보료 체납, 국민연금 납부 중단, 수급 이탈 등의 위기 신호 데이터는 행복e음에 이미 존재
  - 공공마이데이터 이용기관 심사(행안부 승인, 법인 요건) 통과 전에는 실연동 불가
  - MVP 대안: 담당자가 케이스 등록 시 위기 신호 체크리스트 직접 입력 → 스코어 반영
  - Mock 모드: 사전 입력된 Mock 공공마이데이터 데이터로 자동 반영 흐름 시연
- 실제 공공마이데이터 항목 (gov.kr/portal/mydata, 묶음정보 서비스 지속 확대 중 — MVP에서 항목 수 고정 주장 금지):
  - 고용보험피보험자격이력내역서 (근로복지공단) — 실직 시점 직접 확인, 활용도 높음
  - 일반건강검진정보 (국민건강보험공단) — 장기 미수검 감지, 활용도 높음
  - 국민기초생활대상자증명서 (보건복지부) — 수급 이탈 감지, 활용도 높음
  - 4대사회보험료완납증명서 (국민건강보험공단) — 발급 불가 = 건보료 체납 간접 확인
  - 국민연금가입자가입증명 (국민연금공단) — 납부 중단 기간 확인
  - 소득금액증명 (국세청) — 소득 급감 또는 0 확인
  - 보험급여지급확인원 (근로복지공단) — 실업급여 수급 = 실직 후 생계 불안
  - 차상위계층확인서, 장애인증명서 (보건복지부)
  - 수도·전기·가스·통신비 체납은 공공마이데이터 범위 밖 (지자체·KEPCO 별도 계약) — 사용자 제출 증빙 또는 기관 제휴 이후 확장 범위로 분리
- 필수 참조:
  - [Product Specs](../01_Concept_Design/03_PRODUCT_SPECS.md) — 3-2. 위기도 스코어링, 3-6. 공공마이데이터 위기 신호
  - [DB Schema](../03_Technical_Specs/01_DB_SCHEMA.md) — `crisis_scores`, `targets`
  - [API Specs](../03_Technical_Specs/02_API_SPECS.md) — `/crisis/score`, `/dashboard`
- 생성/업데이트 문서:
  - [Product Specs](../01_Concept_Design/03_PRODUCT_SPECS.md)
  - [DB Schema](../03_Technical_Specs/01_DB_SCHEMA.md) — targets 테이블에 위기 신호 체크리스트 컬럼 추가
  - [API Specs](../03_Technical_Specs/02_API_SPECS.md) — 담당자 케이스 등록 시 위기 신호 입력 엔드포인트
- 산출물:
  - 위기 신호 체크리스트 항목 목록
  - Mock 데이터 구조 정의
  - 스코어 반영 방식 (사회적 고립도 지표 가중치 내 반영)
- 완료 기준:
  - 담당자 체크리스트 입력 방식이 DB 컬럼과 API에 반영됨
  - Mock 공공마이데이터 데이터 구조가 정의되어 실연동과 구별됨
  - 파일럿 실연동 경로(이용기관 심사 → 건보료 체납·수급이탈 자동 감지)가 문서에 명시됨

### [ ] T-06. 솔이 AI 전화 통화 기술 스택 구조 정리

- 우선순위: High
- 작업 유형: Research / Documentation
- 목표: 솔이 아웃바운드 전화 통화의 전체 기술 파이프라인을 MVP 수준으로 정의한다. 발신 → STT → 대화 → TTS → 통화 후 분석까지 각 컴포넌트의 역할과 연결 방식을 확정한다.
- 기술 스택:
  - 발신 전화: 알리고 또는 NHN Cloud 아웃바운드 통화 API
  - STT: CLOVA Speech (한국어 통화 음성 → 텍스트)
  - 대화 흐름: GPT-4o mini (실시간 대화 생성)
  - TTS: CLOVA Voice (솔이 목소리 — 한국어 여성 음성)
  - 스케줄링: Vercel Cron Jobs (지정 시각 자동 발신 트리거)
  - 통화 후 분석: Claude API (STT 텍스트 위기 분석 + 담당자 요약)
- 확인 필요 사항:
  - 알리고 vs NHN Cloud 아웃바운드 통화 API 비교 (한국어 통화 품질, webhook 지원 여부)
  - CLOVA Speech 실시간 스트리밍 STT 지원 여부 (vs 통화 종료 후 일괄 처리)
  - CLOVA Voice 목소리 종류 및 솔이 페르소나에 맞는 음성 선택
  - Vercel 함수 실행 시간 제한 내 처리 가능 여부 (5분 통화 기준)
- 필수 참조:
  - [Product Specs](../01_Concept_Design/03_PRODUCT_SPECS.md) — 2. 기술 스택, 3-2. 솔이 AI 전화 통화
  - [Screen Flow](../02_UI_Screens/00_SCREEN_FLOW.md) — 6. 솔이 전화 통화 메인 플로우
- 생성/업데이트 문서:
  - [API Specs](../03_Technical_Specs/02_API_SPECS.md) — 솔이 전화 통화 관련 엔드포인트
  - [DB Schema](../03_Technical_Specs/01_DB_SCHEMA.md) — 통화 이력 테이블
- 산출물:
  - 발신 API 선택 및 webhook 연동 방식
  - STT/TTS 처리 시점 결정 (실시간 vs 통화 후)
  - 통화 1건당 예상 비용 계산
  - Vercel Cron 스케줄링 설계
- 완료 기준:
  - 전화 발신 → STT → GPT-4o mini → TTS → Claude 분석 전체 파이프라인이 정의됨
  - 부재 처리 (재시도 2시간 후, 2회 연속 담당자 알림) 구현 방식이 정의됨
  - 통화 원문 STT 암호화 저장 방식이 결정됨

### [ ] T-02. Open DID 및 OmniOne Chain 기록 구조 정리

- 우선순위: High
- 작업 유형: Research
- 목표: 가점 +10% 확보를 위해 Open DID와 OmniOne Chain 기록을 MVP 필수 성공 기준으로 정의한다.
- 기술 레퍼런스:
  - GitHub 조직: https://github.com/OmniOneID (Apache-2.0, 36개 저장소)
  - 핵심 저장소: `did-issuer-server`, `did-verifier-server`, `did-blockchain-sdk-server`, `did-ledger-service-server`, `did-besu-contract`, `did-demo-server`
  - Ledger API: `POST /register-diddoc`, `POST /register-vcmeta`, `GET /get-vcmeta`
  - 임의 이벤트 로그 미지원 → 지원 완료 증명을 VC 구조로 설계하여 `register-vcmeta`에 기록
  - MVP 최소 범위: `did-demo-server` 참조하여 VC 1개 발급 + VP 1회 검증 + txId 1개 화면 표시
  - 상세: [Development Principles](../03_Technical_Specs/00_DEVELOPMENT_PRINCIPLES.md) — 7-2. Open DID, 7-3. OmniOne Chain
- 필수 참조:
  - [Product Specs](../01_Concept_Design/03_PRODUCT_SPECS.md) — 3-4. OmniOne Chain 기록, 4. 필수조건 충족
  - [DB Schema](../03_Technical_Specs/01_DB_SCHEMA.md) — 4. 온체인 기록 대상 정리
  - [API Specs](../03_Technical_Specs/02_API_SPECS.md) — 8. `/chain`
  - [Development Principles](../03_Technical_Specs/00_DEVELOPMENT_PRINCIPLES.md) — 5. 보안 원칙
- 생성/업데이트 문서:
  - [DB Schema](../03_Technical_Specs/01_DB_SCHEMA.md)
  - [API Specs](../03_Technical_Specs/02_API_SPECS.md)
  - [Proposal Deck](../01_Concept_Design/04_PITCH_DECK.md)
- 산출물:
  - 온체인 기록 대상 목록
  - 개인정보 비저장·해시 기록 원칙
  - 제안서용 가점 확보 전략 설명
- 완료 기준:
  - 온체인에 올릴 데이터와 올리지 않을 데이터가 구분됨
  - 최소 1개 VC 발급, VP 검증, txId 기록 데모 범위가 정의됨

### [ ] T-03. 솔이 AI 위기 감지 및 스코어링 구조 정리

- 우선순위: Medium
- 작업 유형: Research
- 목표: 솔이 전화 통화 기반 위기 키워드 감지, 위기도 스코어 산출 방식을 MVP 수준으로 정의한다. (T-06과 연계 — 음성 처리 파이프라인은 T-06, 감지·스코어링 로직은 이 태스크)
- 기술 레퍼런스:
  - Claude API: `@anthropic-ai/sdk` (npm) — 통화 종료 후 STT 텍스트 분석 및 담당자 요약 생성
  - 스코어 가중치: voice_signal(40%) + absence_pattern(35%) + isolation(25%)
  - AI 실패 시 룰 기반 fallback 필수 (위기 키워드 사전 + 부재 임계값)
- 필수 참조:
  - [Product Specs](../01_Concept_Design/03_PRODUCT_SPECS.md) — 3-2. 솔이 AI 전화 통화
  - [Screen Flow](../02_UI_Screens/00_SCREEN_FLOW.md) — 6. 솔이 전화 통화 메인 플로우
  - [API Specs](../03_Technical_Specs/02_API_SPECS.md) — 4. `/crisis`, 5. `/soli`
  - [DB Schema](../03_Technical_Specs/01_DB_SCHEMA.md) — 2-3. `crisis_scores`, 2-6. `soli_conversations`
- 생성/업데이트 문서:
  - [Product Specs](../01_Concept_Design/03_PRODUCT_SPECS.md)
  - [API Specs](../03_Technical_Specs/02_API_SPECS.md)
  - [Proposal Validation Scenarios](../05_QA_Validation/01_TEST_SCENARIOS.md)
- 산출물:
  - 위기 키워드 fallback 기준 (통화 음성 기반)
  - 부재 패턴 스코어 반영 방식
  - 담당자 AI 요약 제공 범위
- 완료 기준:
  - 통화 STT 텍스트 기반 위기 감지 로직이 정의됨
  - 부재 연속 횟수별 알림 분기가 정의됨
  - 대화 원문 접근 제한 원칙이 반영됨

### [ ] T-04. 솔이 복지 매칭 데이터 연동 구조 정리

- 우선순위: High
- 작업 유형: Research
- 목표: 복지서비스 목록 실연동(한국사회보장정보원 API)과 개인 자격 확인의 파일럿 이후 범위를 구분하여 MVP 범위 안에서 정의한다.
- 기술 레퍼런스:
  - 중앙부처복지서비스 API: https://www.data.go.kr/data/15090532/openapi.do (자동 승인, 무료)
  - 지자체복지서비스 API: https://www.data.go.kr/data/15108347/openapi.do (자동 승인, 무료)
  - 사회서비스 제공기관 API: https://www.data.go.kr/data/15057683/openapi.do (자동 승인, 무료)
  - 복지로: https://www.bokjiro.go.kr (신청 외부 링크 대상)
  - 공공 마이데이터(개인 자격 확인): 이용기관 심사 필요, MVP 제외, 파일럿 이후 추진
  - 상세: [Development Principles](../03_Technical_Specs/00_DEVELOPMENT_PRINCIPLES.md) — 7-4. 복지 공공데이터 API
- 필수 참조:
  - [Product Specs](../01_Concept_Design/03_PRODUCT_SPECS.md) — 3-6. 복지 데이터 연동 구조, 4. 필수조건 충족
  - [Proposal Deck](../01_Concept_Design/04_PITCH_DECK.md) — 4. 제안내용의 상세 설명, 5. 제안내용의 차별성
  - [QA Checklist](../05_QA_Validation/02_QA_CHECKLIST.md) — 4. Track 2 및 가점 조건, 6. MVP 개발 단계 계획 점검
- 생성/업데이트 문서:
  - [Product Specs](../01_Concept_Design/03_PRODUCT_SPECS.md)
  - [Proposal Deck](../01_Concept_Design/04_PITCH_DECK.md)
  - [QA Checklist](../05_QA_Validation/02_QA_CHECKLIST.md)
- 산출물:
  - 복지서비스 API 실연동 방식
  - 기본 조건·상황 체크리스트·대화 맥락 매칭 기준
  - 개인 자격 확인은 파일럿 단계로 분리한다는 설명
- 완료 기준:
  - MVP는 개인 자격 확정이 아니라 복지 후보 매칭으로 정의됨
  - MVP 시연 범위와 실제 운영 연동 범위가 구분됨

---

## 6. MVP 구현 백로그

아래 항목은 5월에 구현하지 않는다. 대신 제안서에서 "MVP 개발 단계에서 실제로 만들 MVP 범위"로 제시하고, MVP 개발 단계 진입 전에 다시 기술 결정을 확정한다.

MVP 구현 일정은 예선 통과 후 별도 `01_EXECUTION_PLAN.md`로 수립한다 (2026-07-01 이후).

### MVP 구현 페이즈 일정 (결선 12주, 2026-07-01 ~ 09-21)

| 페이즈 | 기간 | 주요 작업 | 구현 가능성 |
|:---|:---|:---|:---|
| **P0. 프로젝트 셋업** | 07-01 ~ 07-14 (2주) | M-01 Next.js+NestJS 골격, DB, CI | 높음 |
| **P1. SDK 환경** | 07-01 ~ 07-14 (2주, P0 병행) | M-05-P1 did-demo-server 실행, CX Mock | 보통 (서버 셋업 복잡) |
| **P2. 핵심 기능** | 07-15 ~ 08-04 (3주) | M-02 솔이+스코어링, M-05-P2 CX 실연동+DID 등록 | 높음 |
| **P3. 대시보드+VC** | 08-05 ~ 08-25 (3주) | M-04 담당자 대시보드, M-05-P3 VC 발급+txId | 보통 (P210 프로토콜 복잡) |
| **P4. 집행 완성** | 08-26 ~ 09-07 (2주) | M-05-P4 VP 검증+2차 CX+집행, M-06 복지 매칭 | 보통 (QR VP 흐름 단순화 필요) |
| **P5. 데모·마무리** | 09-08 ~ 09-21 (2주) | 전체 시나리오 시연, fallback 준비, 문서 제출 | 높음 |

**구현 가능성 종합 판단**: 12주는 타이트하지만 `did-demo-server` 활용 전략을 쓰면 가능하다. P3(VC 발급)까지 완료하면 가점 +10% 최소 조건(OmniOne CX + VC + txId)을 충족한다. P4(VP 검증)는 시연 완성도 향상이 목적으로, 지연 시 P5에서 데모 시나리오로 흡수한다.

**핵심 리스크**: TAS P132·Issuer P210 프로토콜 구현 난이도. `did-demo-server` 소스 코드를 레퍼런스로 삼아 흐름을 복제하는 것이 처음부터 짜는 것보다 3~4일 단축 가능.

### [ ] M-01. 프로젝트 셋업 및 UI 골격

- 우선순위: High
- 작업 유형: MVP Implementation
- 목표: Next.js 앱, 기본 라우팅, 화면 목업을 구성한다.
- 필수 참조:
  - [Development Principles](../03_Technical_Specs/00_DEVELOPMENT_PRINCIPLES.md) — 1. 기술 스택, 3. 프로젝트 구조, 4. 코딩 컨벤션
  - [Product Specs](../01_Concept_Design/03_PRODUCT_SPECS.md) — 5-3. MVP 구현 범위
  - [Field Outreach Strategy](../01_Concept_Design/05_FIELD_OUTREACH_STRATEGY.md) — 55세 이상 현장 진입 채널과 안부 연결 신청 흐름
  - [Screen Flow](../02_UI_Screens/00_SCREEN_FLOW.md) — 1. 전체 화면 구조
  - [UI Design](../02_UI_Screens/01_UI_DESIGN.md) — 1. 설계 원칙
- 생성/업데이트 문서:
  - [Development Principles](../03_Technical_Specs/00_DEVELOPMENT_PRINCIPLES.md)
  - [QA Checklist](../05_QA_Validation/02_QA_CHECKLIST.md)
- 산출물:
  - `/web` 앱 구조
  - 기본 라우팅
  - 대상자 웹 화면/담당자 대시보드 화면 골격
  - 주민센터·복지관·경로당 QR 진입을 고려한 55세 이상 안부 연결 진입 화면
- 완료 기준:
  - 로컬 실행 가능
  - 핵심 화면 라우트가 존재함
  - 구현 전 폴더 구조와 패턴이 사용자 승인됨

### [ ] M-02. 솔이 전화·SMS·웹 채팅 및 위기 스코어링 구현

- 우선순위: High
- 작업 유형: MVP Implementation
- 목표: 아웃바운드 전화 흐름, SMS·웹 채팅 선택 채널, 위기 키워드 감지, 위기도 스코어 출력을 구현한다.
- 필수 참조:
  - [Product Specs](../01_Concept_Design/03_PRODUCT_SPECS.md) — 3-2. 솔이 AI 전화 통화
  - [Field Outreach Strategy](../01_Concept_Design/05_FIELD_OUTREACH_STRATEGY.md) — 솔이 정기 전화 문구, SMS·웹 채팅 선택 채널, 생활위기 신호, 부재 시나리오
  - [Screen Flow](../02_UI_Screens/00_SCREEN_FLOW.md) — 6. 솔이 전화 통화 메인 플로우, 7. 웹 채팅 보조 채널
  - [UI Design](../02_UI_Screens/01_UI_DESIGN.md) — 3. 솔이 전화 및 SMS·웹 채팅 UX 설계
  - [API Specs](../03_Technical_Specs/02_API_SPECS.md) — 4. `/crisis`, 5. `/soli`
  - [DB Schema](../03_Technical_Specs/01_DB_SCHEMA.md) — 2-3. `crisis_scores`, 2-7. `soli_call_sessions`, 2-8. `soli_conversations`
- 생성/업데이트 문서:
  - [Proposal Validation Scenarios](../05_QA_Validation/01_TEST_SCENARIOS.md)
  - [QA Checklist](../05_QA_Validation/02_QA_CHECKLIST.md)
- 산출물:
  - 전화·SMS·웹 채팅 UI
  - 키워드 감지
  - 스코어 산출
  - 정기 전화, SMS·웹 채팅 선택 채널, 생활요금 어려움, 부재 패턴을 포함한 현장 시나리오형 테스트
- 완료 기준:
  - 정상 통화·SMS·웹 채팅와 위기 감지 분기가 모두 시연됨
  - AI 응답 실패 시 fallback이 작동함
  - 담당자에게 보여줄 요약 범위가 제한됨

### [-] M-03. 커뮤니티 케어 채널 (Phase 2 검토)

- 우선순위: Low
- 메모: 이웃·관리인이 "이 분이 걱정돼요" 수준으로 안부를 공유하는 채널. 한국 문화에서 "신고" 거부감 문제로 MVP에서 제외. 파일럿 이후 커뮤니티 케어 채널로 재검토 가능.

### [ ] M-04. 담당자 대시보드 구현

- 우선순위: High
- 작업 유형: MVP Implementation
- 목표: 위기 우선순위 리스트, 대상자 상세, 솔이 요약, 지원 승인 버튼을 구현한다.
- 필수 참조:
  - [Product Specs](../01_Concept_Design/03_PRODUCT_SPECS.md) — 3-3. 담당자 대시보드
  - [Field Outreach Strategy](../01_Concept_Design/05_FIELD_OUTREACH_STRATEGY.md) — "오늘 먼저 확인할 5명"과 담당자 직접 지원 시나리오
  - [Screen Flow](../02_UI_Screens/00_SCREEN_FLOW.md) — 5. 담당자 대시보드 플로우
  - [UI Design](../02_UI_Screens/01_UI_DESIGN.md) — 2-2. 담당자 대시보드
  - [API Specs](../03_Technical_Specs/02_API_SPECS.md) — 7. `/dashboard`
  - [DB Schema](../03_Technical_Specs/01_DB_SCHEMA.md) — 2-5. `support_executions`
- 생성/업데이트 문서:
  - [Screen Flow](../02_UI_Screens/00_SCREEN_FLOW.md)
  - [Proposal Validation Scenarios](../05_QA_Validation/01_TEST_SCENARIOS.md)
- 산출물:
  - 우선순위 리스트
  - 대상자 상세 화면
  - 지원 승인 플로우
  - 응답 공백, 생활비 어려움, 최근 조치 이력을 요약하는 담당자 확인 카드
- 완료 기준:
  - 위기 스코어 기반 우선순위 정렬이 작동함
  - 승인 액션이 기록됨
  - 개인정보 마스킹 원칙이 적용됨

### [ ] M-05. OmniOne CX + Open DID + OmniOne Chain 연동 (4페이즈)

- 우선순위: High
- 작업 유형: MVP Implementation
- 필수 참조:
  - [Blockchain DID Architecture](../03_Technical_Specs/04_BLOCKCHAIN_DID_ARCH.md) — 전체 아키텍처 기준 문서
  - [Development Principles](../03_Technical_Specs/00_DEVELOPMENT_PRINCIPLES.md) — 7-1. OmniOne CX, 7-2. Open DID, 7-3. OmniOne Chain
  - [API Specs](../03_Technical_Specs/02_API_SPECS.md) — 2. `/auth`, 8. `/chain`
  - [DB Schema](../03_Technical_Specs/01_DB_SCHEMA.md) — `chain_tx_id`, `target_did_hash`

#### MVP 최소 성공 기준 (가점 +10% 충족 조건)

아래 3가지가 데모에서 동작하면 가점 조건을 충족한다:
- [ ] OmniOne CX 인증 1회 (가입 또는 로그인 중 1 지점)
- [ ] Open DID VC 발급 1회 + OmniOne Chain txId 1개 표시
- [ ] VP 검증 1회

M-05-P1~P3 완료 시 위 3가지를 충족한다. P4는 완성도와 시연 임팩트 향상이 목적이다.

#### 구현 전략

각 Open DID 서버(TAS, Issuer, Verifier, Ledger Service)를 처음부터 짜지 않는다.  
`did-demo-server`(OmniOneID GitHub, Apache-2.0)를 Docker로 로컬 실행 → 전체 흐름 파악 → NOA 백엔드에서 각 서버 API를 호출하는 방식으로 연동한다.  
OmniOne CX SDK는 해커톤 오리엔테이션(2026-07-01) 이후 RaonSecure가 직접 제공한다.

#### Fallback 전략

외부 SDK·서버 장애에 대비해 각 페이즈에 Mock 모드를 병행 유지한다.  
데모 당일 실연동이 안 될 경우: Mock 데이터로 동일 UI 흐름을 시연하고 화면 녹화로 보완한다.

---

### [ ] M-05-P1. SDK·서버 환경 셋업 (2026-07-01 ~ 07-14, 2주)

- 우선순위: High
- 작업 유형: MVP Implementation
- 목표: OmniOne CX SDK와 Open DID 서버군을 로컬에서 실행하고 기본 연결을 확인한다.
- 구현 방법:
  - [ ] `did-demo-server` Docker Compose로 로컬 실행 (TAS·CA·Issuer·Verifier·Ledger Service 포함)
  - [ ] 데모 서버 실행 확인 후 전체 흐름(DID 등록 → VC 발급 → VP 검증 → txId) 로컬 시연
  - [ ] OmniOne CX SDK 수령 및 연동 가이드 검토
  - [ ] OmniOne CX Mock 인증 모드 구현 (실 SDK 연동 전 UI 흐름 선행 개발)
  - [ ] NestJS 백엔드에서 Ledger Service `POST /api/v1/diddoc/register` 호출 테스트
- 리스크:
  - did-demo-server Java 21 + Gradle 환경 셋업에 1~2일 소요 예상
  - OmniOne CX SDK 수령이 오리엔테이션 이후 지연될 경우 Mock 모드로 P2 선행 진행
- 완료 기준:
  - [ ] did-demo-server 로컬에서 전체 흐름 1회 실행 성공
  - [ ] Ledger Service API 호출 시 txId 반환 확인
  - [ ] OmniOne CX Mock 인증 → JWT 발급 흐름 동작

### [ ] M-05-P2. OmniOne CX 1차 연동 + 사용자 DID 등록 (2026-07-15 ~ 08-04, 3주)

- 우선순위: High
- 작업 유형: MVP Implementation
- 목표: 서비스 가입·로그인 시 OmniOne CX 실인증을 연동하고, TAS P132를 통해 사용자 DID를 OmniOne Chain에 등록한다.
- 구현 방법:
  - [ ] OmniOne CX SDK 실인증 연동 (표준 인증창 호출 → 콜백 처리 → did_hash 추출)
  - [ ] TAS P132 6단계 구현: `propose-register-user` → `request-ecdh` → `request-create-token` → `retrieve-kyc` → `request-register-user` → `confirm-register-user`
  - [ ] Ledger Service `POST /api/v1/diddoc/register` → txId-1 수신 및 DB 저장 (`users.chain_tx_id`)
  - [ ] JWT 발급 연계 (OmniOne CX 콜백 검증 후 서버 JWT 발급)
  - [ ] P132 단계별 실패 처리 (재시도 3회, 가입 미완료 상태 유지)
- 리스크:
  - TAS P132 ECDH 세션키 교환 구현이 복잡. did-demo-server 소스 코드 참조 필수
  - OmniOne CX 콜백 파라미터가 제공 가이드와 다를 경우 적응 필요
- 완료 기준:
  - [ ] OmniOne CX 실인증 후 did_hash 추출 성공
  - [ ] DID Document OmniOne Chain 등록 txId 반환 확인
  - [ ] 사용자 가입 플로우 전체 동작

### [ ] M-05-P3. VC 발급 + OmniOne Chain 기록 (2026-08-05 ~ 08-25, 3주)

- 우선순위: High
- 작업 유형: MVP Implementation
- 목표: 담당자 승인 완료 후 수급 자격 VC를 발급하고 메타데이터를 OmniOne Chain에 기록하여 txId를 대상자에게 표시한다.
- 구현 방법:
  - [ ] Issuer Server P210 5단계 구현: `request-offer` → `inspect-propose-issue` → `generate-issue-profile` → `issue-vc` → `complete-vc`
  - [ ] VC 스키마 정의: `GET /api/v1/vc/vcschema`로 기존 스키마 확인 → 복지 수급 자격 VC 커스텀 스키마 등록
  - [ ] Ledger Service `POST /api/v1/vcmeta/register` → txId-2 수신 및 DB 저장 (`support_executions.chain_tx_id`)
  - [ ] 대상자 대시보드에 txId 표시 UI (OmniOne Chain 조회 링크 포함)
  - [ ] 담당자 승인 API(`POST /dashboard/execute`)와 VC 발급 흐름 연결
- 리스크:
  - P210 E2E 암호화 구현이 가장 복잡한 부분. did-demo-server의 issuer 모듈 코드를 그대로 활용
  - VC 커스텀 스키마 등록이 막힐 경우 기본 스키마로 대체
- 완료 기준:
  - [ ] 담당자 승인 → VC 발급 → txId 생성 → 대상자 화면 표시 전체 흐름 동작
  - [ ] 개인정보 원문이 온체인에 기록되지 않음 (메타데이터 해시만)
  - [ ] **이 시점에 가점 +10% 최소 조건 충족** (OmniOne CX + VC 발급 + txId)

### [ ] M-05-P4. VP 검증 + OmniOne CX 2차 확인 + 집행 완성 (2026-08-26 ~ 09-07, 2주)

- 우선순위: Medium
- 작업 유형: MVP Implementation
- 목표: 집행 직전 대상자 VP 제출과 OmniOne CX 재확인을 결합해 이중 신원 검증 후 집행하고 txId를 기록한다.
- 구현 방법:
  - [ ] Verifier Server P310 4단계 구현: `request-offer-qr` → `request-profile` → `request-verify` → `confirm-verify`
  - [ ] QR 기반 VP 제출 흐름: 담당자 화면에서 QR 생성 → 대상자 앱에서 스캔 → VP 제출
  - [ ] OmniOne CX 2차 재확인 (집행 직전 신뢰 포인트 2)
  - [ ] VP 검증 완료 후 VC 즉시 폐기: `updateVcStatus(vcId, REVOKED)` + Ledger Service 상태 변경
  - [ ] 집행 이벤트 해시 온체인 기록: SHA-256(did_hash + support_type + amount + timestamp) → txId-3
- 리스크:
  - QR 기반 VP 제출은 모바일 앱과 웹 동시 동작 필요. 데모용으로 같은 기기 QR 스캔 시나리오로 단순화 가능
  - OmniOne CX 2차 확인이 1차와 동일 SDK 경로면 재사용 가능, 다르면 추가 구현 필요
- 완료 기준:
  - [ ] 집행 직전 VP 검증 → 집행 → txId-3 기록 흐름 동작
  - [ ] VC 폐기 후 DB 원문 삭제 확인
  - [ ] 전체 신뢰 체인 (txId-1 DID 등록 → txId-2 VC 메타 → txId-3 집행) 시연 가능

### [ ] M-06. 솔이 복지 매칭 데모 구현

- 우선순위: Medium
- 작업 유형: MVP Implementation
- 목표: 한국사회보장정보원 복지서비스 API 연동, 기본 조건·상황 체크리스트 입력, 복지 매칭 카드 표시 흐름을 구현한다.
- 필수 참조:
  - [Product Specs](../01_Concept_Design/03_PRODUCT_SPECS.md) — 3-6. 복지 데이터 연동 구조
  - [Field Outreach Strategy](../01_Concept_Design/05_FIELD_OUTREACH_STRATEGY.md) — 공과금 체납 상담, 사용자 제출 증빙, 동의 기반 생활위기 체크
  - [Proposal Deck](../01_Concept_Design/04_PITCH_DECK.md) — 4. 제안내용의 상세 설명
  - [QA Checklist](../05_QA_Validation/02_QA_CHECKLIST.md) — 6. MVP 개발 단계 계획 점검
- 생성/업데이트 문서:
  - [Product Specs](../01_Concept_Design/03_PRODUCT_SPECS.md)
  - [QA Checklist](../05_QA_Validation/02_QA_CHECKLIST.md)
- 산출물:
  - 기본 조건 입력 UI
  - 상황 체크리스트
  - 복지 매칭 결과 카드
  - 복지로/정부24 외부 신청 링크
- 완료 기준:
  - 인증된 사용자 세션에서 매칭 결과가 생성됨
  - 개인 행정정보 조회가 진행되지 않음
  - 실제 공공 마이데이터 운영 API 계약·심사 완료가 MVP 필수 조건으로 오해되지 않음

---

## 7. QA 및 발표 준비 백로그

### [ ] Q-01. 내용 정합성 및 근거 검증

- 우선순위: High
- 작업 유형: QA
- 목표: 제안서의 문제, 기술, 사업성 문장이 기존 문서와 서로 충돌하지 않는지 확인한다.
- 필수 참조:
  - [Proposal Validation Scenarios](../05_QA_Validation/01_TEST_SCENARIOS.md)
  - [QA Checklist](../05_QA_Validation/02_QA_CHECKLIST.md) — 5. 내용 정합성
  - [Document Index](../00_DOCUMENT_INDEX.md)
- 생성/업데이트 문서:
  - [QA Checklist](../05_QA_Validation/02_QA_CHECKLIST.md)
- 산출물:
  - 불일치 목록
  - 수정 완료 목록
- 완료 기준:
  - MVP 범위, 기술 스택, 수익 모델, 개인정보 원칙이 문서 간 일치함

### [ ] Q-02. 제출 전 QA 체크리스트 완료

- 우선순위: High
- 작업 유형: QA
- 목표: 양식, 목차, 심사 기준, Track 2 조건, 제출 파일명을 최종 점검한다.
- 필수 참조:
  - [QA Checklist](../05_QA_Validation/02_QA_CHECKLIST.md)
  - [Proposal Deck](../01_Concept_Design/04_PITCH_DECK.md)
- 생성/업데이트 문서:
  - [QA Checklist](../05_QA_Validation/02_QA_CHECKLIST.md)
- 산출물:
  - 제출 전 체크 결과
- 완료 기준:
  - 모든 필수 항목이 체크됨
  - 미확정 항목이 별도 표시됨

### [ ] Q-03. 8분 발표 및 5분 Q&A 흐름 점검

- 우선순위: Medium
- 작업 유형: QA
- 목표: 제안서가 발표 시간 안에 설명 가능한 흐름인지 검증한다.
- 필수 참조:
  - [Proposal Deck](../01_Concept_Design/04_PITCH_DECK.md) — 10. 기타, 8분 발표 흐름
  - [Proposal Validation Scenarios](../05_QA_Validation/01_TEST_SCENARIOS.md) — 5. 8분 발표 검증
- 생성/업데이트 문서:
  - [Proposal Deck](../01_Concept_Design/04_PITCH_DECK.md)
  - [Proposal Validation Scenarios](../05_QA_Validation/01_TEST_SCENARIOS.md)
- 산출물:
  - 8분 발표 스크립트 초안
  - 예상 Q&A 목록
- 완료 기준:
  - 8분 내 설명 가능
  - 기술 필수조건, 사업성, 실현 가능성 질문에 답변 가능

### [ ] Q-04. 제출 패키지 최종화

- 우선순위: High
- 작업 유형: QA
- 목표: 온라인 모집 마감 전 제출 파일을 최종 확정한다.
- 필수 참조:
  - [QA Checklist](../05_QA_Validation/02_QA_CHECKLIST.md) — 7. 제출 전 최종 확인
  - [Roadmap](./00_ROADMAP.md) — 0. 해커톤 공식 일정
- 생성/업데이트 문서:
  - [QA Checklist](../05_QA_Validation/02_QA_CHECKLIST.md)
- 산출물:
  - 최종 제출용 PPTX
  - 최종 점검 기록
- 완료 기준:
  - 파일명 규칙 충족
  - 마감 전 제출 가능 상태
  - 백업본이 준비됨

---

## 8. MVP 개발 단계 리스크와 대응

| 리스크 | 대응 | 관련 백로그 |
|:---|:---|:---|
| OmniOne CX/Chain SDK 연동 지연 | 데모 모드와 실제 연동 모드를 분리하되, 가점 확보를 위해 최소 1개 인증·VC 발급·VP 검증·txId 성공을 목표로 축소 | `T-01`, `T-02`, `M-05` |
| 공공마이데이터 실연동 지연 (이용기관 심사 미통과) | 담당자 위기 신호 체크리스트 직접 입력 방식으로 대체. Mock 공공마이데이터 데이터로 자동 반영 흐름 시연. 개인 자격 확인은 복지서비스 API 실연동 기반 매칭으로 범위 축소 | `T-04`, `T-05`, `M-06` |
| AI 응답 품질 불안정 | 위기 키워드 룰 기반 스코어링을 fallback으로 구현 | `T-03`, `M-02` |
| 개인정보 이슈 | 실사용자 데이터 없이 데모 데이터와 DID 해시만 사용. 개인 행정정보 원문은 조회·저장하지 않음 | `T-01`, `T-02`, `T-04`, `M-05`, `M-06` |
| 범위 과대 | Phase 2 가족 안부 케어는 제외하고, 핵심 시연은 솔이 감지→담당자 승인→온체인 기록에 집중 | `P-05`, `M-02`, `M-04`, `M-05`, `M-06` |
| 발표 당일 네트워크 장애 | 로컬 데모 데이터와 녹화 영상을 백업으로 준비 | `Q-03`, `Q-04` |

---

## Related Documents

- **Documentation**: [Document Index](../00_DOCUMENT_INDEX.md) — 전체 문서와 백로그 ID 연결 지도
- **Logic_Progress**: [Roadmap](./00_ROADMAP.md) — 해커톤 일정 및 단계별 계획
- **Concept_Design**: [Product Specs](../01_Concept_Design/03_PRODUCT_SPECS.md) — 제안서 기준 MVP 범위
- **Concept_Design**: [Proposal Deck](../01_Concept_Design/04_PITCH_DECK.md) — 공모 제안서 본문 작성 기준
- **QA_Validation**: [QA Checklist](../05_QA_Validation/02_QA_CHECKLIST.md) — 제안서 및 MVP 계획 점검 항목

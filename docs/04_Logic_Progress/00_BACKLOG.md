# Backlog — no-one-alone
> Created: 2026-05-08 01:39
> Last Updated: 2026-05-13 02:00
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
- 생성/업데이트 문서:
  - [Proposal Deck](../01_Concept_Design/04_PITCH_DECK.md)
  - [Lean Canvas](../01_Concept_Design/02_LEAN_CANVAS.md)
- 산출물:
  - 목적 및 필요성 본문 문안
  - 문제 근거와 출처 목록
- 완료 기준:
  - 대상 사용자와 사각지대 발생 원인이 분리되어 설명됨
  - 통계 또는 공신력 있는 근거가 필요한 문장에 표시가 남아 있음

### [ ] P-04. 제안내용 상세 설명 작성

- 우선순위: High
- 작업 유형: Proposal
- 목표: 대상자 웹 화면, Soli 챗봇, 담당자 대시보드, OmniOne Chain 기록을 하나의 실행 파이프라인으로 설명한다.
- 필수 참조:
  - [Proposal Deck](../01_Concept_Design/04_PITCH_DECK.md) — 4. 제안내용의 상세 설명
  - [Product Specs](../01_Concept_Design/03_PRODUCT_SPECS.md) — 3. 핵심 기능 명세
  - [Screen Flow](../02_UI_Screens/00_SCREEN_FLOW.md) — 1. 전체 화면 구조
  - [UI Design](../02_UI_Screens/01_UI_DESIGN.md) — 2. 사용자 유형별 UI 원칙, 3. Soli 챗봇 UI 설계
- 생성/업데이트 문서:
  - [Proposal Deck](../01_Concept_Design/04_PITCH_DECK.md)
  - [Screen Flow](../02_UI_Screens/00_SCREEN_FLOW.md)
- 산출물:
  - 전체 파이프라인 설명
  - 핵심 기능 요약표
- 완료 기준:
  - Soli 감지에서 담당자 승인, 온체인 기록까지의 흐름이 끊기지 않음
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
  - [Roadmap](./00_ROADMAP.md) — 2. 생존 단계, 3. 검증 단계, 7. 수익 목표 요약
- 생성/업데이트 문서:
  - [Proposal Deck](../01_Concept_Design/04_PITCH_DECK.md)
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
  - [QA Checklist](../05_QA_Validation/02_QA_CHECKLIST.md) — 1. 양식 준수, 7. 제출 전 최종 확인
- 생성/업데이트 문서:
  - [Proposal Deck](../01_Concept_Design/04_PITCH_DECK.md)
  - [QA Checklist](../05_QA_Validation/02_QA_CHECKLIST.md)
- 산출물:
  - 제출용 PPTX
  - PPTX에 들어간 최종 문구와 원문 문서 간 대응표
- 완료 기준:
  - 제안 요약서 2p 이내
  - 본문 10p 이내
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

### [X] D-04. Soli 1차 감지 전환 — 파이프라인 구조 변경

- 우선순위: High
- 작업 유형: Documentation
- 목표: 핵심 파이프라인을 "이웃 제보 1차 감지"에서 "Soli AI 대화 1차 감지"로 전환하고 6개 문서에 반영한다.
- 변경 근거: 이웃 신고는 한국 문화에서 거부감이 높고 자발적 제보 동기가 약함. Soli 대화 자체가 위기를 감지하는 구조가 실현 가능성과 창의성 모두를 강화함. 이웃 제보 기능은 완전 제거 (Phase 2 커뮤니티 케어 채널로 재검토 가능).
- 새 태그라인: "국가가 못 찾는 사람을, AI가 찾고, 복지가 닿고, 블록체인이 증명한다"
- 생성/업데이트 문서:
  - [Vision & Core Values](../01_Concept_Design/01_VISION_CORE.md) — 태그라인, 파이프라인
  - [Product Specs](../01_Concept_Design/03_PRODUCT_SPECS.md) — 기능 순서, 스코어 가중치
  - [Screen Flow](../02_UI_Screens/00_SCREEN_FLOW.md) — 홈 구조, 이웃 제보 제거
  - [API Specs](../03_Technical_Specs/02_API_SPECS.md) — Soli Critical Path, 보조 채널 명시
  - [DB Schema](../03_Technical_Specs/01_DB_SCHEMA.md) — 스코어 가중치 주석
  - [Backlog](./00_BACKLOG.md) — 태스크 반영

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

### [ ] T-03. AI Soli 위기 감지 및 스코어링 구조 정리

- 우선순위: Medium
- 작업 유형: Research
- 목표: Soli 챗봇의 대화, 위기 키워드 감지, 위기도 스코어 산출 방식을 MVP 수준으로 정의한다.
- 기술 레퍼런스:
  - SDK: `@anthropic-ai/sdk` (npm), SSE 스트리밍 지원
  - 스코어 가중치: keywords(40%) + response_gap(35%) + isolation(25%)
  - AI 실패 시 룰 기반 fallback 필수 (위기 키워드 사전 + 응답 공백 임계값)
  - 상세: [Development Principles](../03_Technical_Specs/00_DEVELOPMENT_PRINCIPLES.md) — 7-4. Claude API
- 필수 참조:
  - [Product Specs](../01_Concept_Design/03_PRODUCT_SPECS.md) — 3-2. AI 챗봇 Soli
  - [Screen Flow](../02_UI_Screens/00_SCREEN_FLOW.md) — 6. Soli 챗봇 공통 화면
  - [UI Design](../02_UI_Screens/01_UI_DESIGN.md) — 3. Soli 챗봇 UI 설계
  - [API Specs](../03_Technical_Specs/02_API_SPECS.md) — 4. `/crisis`, 5. `/soli`
  - [DB Schema](../03_Technical_Specs/01_DB_SCHEMA.md) — 2-3. `crisis_scores`, 2-6. `soli_conversations`
- 생성/업데이트 문서:
  - [Product Specs](../01_Concept_Design/03_PRODUCT_SPECS.md)
  - [API Specs](../03_Technical_Specs/02_API_SPECS.md)
  - [Proposal Validation Scenarios](../05_QA_Validation/01_TEST_SCENARIOS.md)
- 산출물:
  - 위기 키워드 fallback 기준
  - 스코어 산출 기준
  - 담당자 요약 제공 범위
- 완료 기준:
  - AI 실패 시 룰 기반 fallback이 정의됨
  - 대화 원문 접근 제한 원칙이 반영됨

### [ ] T-04. Soli 복지 매칭 데이터 연동 구조 정리

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

### [ ] M-01. 프로젝트 셋업 및 UI 골격

- 우선순위: High
- 작업 유형: MVP Implementation
- 목표: Next.js 앱, 기본 라우팅, 화면 목업을 구성한다.
- 필수 참조:
  - [Development Principles](../03_Technical_Specs/00_DEVELOPMENT_PRINCIPLES.md) — 1. 기술 스택, 3. 프로젝트 구조, 4. 코딩 컨벤션
  - [Product Specs](../01_Concept_Design/03_PRODUCT_SPECS.md) — 5-3. MVP 구현 범위
  - [Screen Flow](../02_UI_Screens/00_SCREEN_FLOW.md) — 1. 전체 화면 구조
  - [UI Design](../02_UI_Screens/01_UI_DESIGN.md) — 1. 설계 원칙
- 생성/업데이트 문서:
  - [Development Principles](../03_Technical_Specs/00_DEVELOPMENT_PRINCIPLES.md)
  - [QA Checklist](../05_QA_Validation/02_QA_CHECKLIST.md)
- 산출물:
  - `/web` 앱 구조
  - 기본 라우팅
  - 대상자 웹 화면/담당자 대시보드 화면 골격
- 완료 기준:
  - 로컬 실행 가능
  - 핵심 화면 라우트가 존재함
  - 구현 전 폴더 구조와 패턴이 사용자 승인됨

### [ ] M-02. Soli 챗봇 및 위기 스코어링 구현

- 우선순위: High
- 작업 유형: MVP Implementation
- 목표: 기본 대화, 위기 키워드 감지, 위기도 스코어 출력을 구현한다.
- 필수 참조:
  - [Product Specs](../01_Concept_Design/03_PRODUCT_SPECS.md) — 3-2. AI 챗봇 Soli
  - [Screen Flow](../02_UI_Screens/00_SCREEN_FLOW.md) — 6. Soli 챗봇 공통 화면
  - [UI Design](../02_UI_Screens/01_UI_DESIGN.md) — 3. Soli 챗봇 UI 설계
  - [API Specs](../03_Technical_Specs/02_API_SPECS.md) — 4. `/crisis`, 5. `/soli`
  - [DB Schema](../03_Technical_Specs/01_DB_SCHEMA.md) — 2-3. `crisis_scores`, 2-6. `soli_conversations`
- 생성/업데이트 문서:
  - [Proposal Validation Scenarios](../05_QA_Validation/01_TEST_SCENARIOS.md)
  - [QA Checklist](../05_QA_Validation/02_QA_CHECKLIST.md)
- 산출물:
  - 대화 UI
  - 키워드 감지
  - 스코어 산출
- 완료 기준:
  - 정상 대화와 위기 감지 분기가 모두 시연됨
  - AI 응답 실패 시 fallback이 작동함
  - 담당자에게 보여줄 요약 범위가 제한됨

### [-] M-03. 커뮤니티 케어 채널 (Phase 2 검토)

- 우선순위: Low
- 메모: 이웃·관리인이 "이 분이 걱정돼요" 수준으로 안부를 공유하는 채널. 한국 문화에서 "신고" 거부감 문제로 MVP에서 제외. 파일럿 이후 커뮤니티 케어 채널로 재검토 가능.

### [ ] M-04. 담당자 대시보드 구현

- 우선순위: High
- 작업 유형: MVP Implementation
- 목표: 위기 우선순위 리스트, 대상자 상세, Soli 요약, 지원 승인 버튼을 구현한다.
- 필수 참조:
  - [Product Specs](../01_Concept_Design/03_PRODUCT_SPECS.md) — 3-3. 담당자 대시보드
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
- 완료 기준:
  - 위기 스코어 기반 우선순위 정렬이 작동함
  - 승인 액션이 기록됨
  - 개인정보 마스킹 원칙이 적용됨

### [ ] M-05. OmniOne CX, Open DID, Chain 연동 데모 구현

- 우선순위: High
- 작업 유형: MVP Implementation
- 목표: 가점 +10% 확보를 위해 인증 결과 저장, 지원 확인 VC 발급, VP 검증, 최소 1개 온체인 txId 표시를 구현한다.
- 필수 참조:
  - [Product Specs](../01_Concept_Design/03_PRODUCT_SPECS.md) — 3-4. OmniOne Chain 기록, 4. 필수조건 충족
  - [API Specs](../03_Technical_Specs/02_API_SPECS.md) — 2. `/auth`, 8. `/chain`
  - [DB Schema](../03_Technical_Specs/01_DB_SCHEMA.md) — 4. 온체인 기록 대상 정리
  - [Development Principles](../03_Technical_Specs/00_DEVELOPMENT_PRINCIPLES.md) — 5. 보안 원칙, 7-2. Open DID, 7-3. OmniOne Chain
- 생성/업데이트 문서:
  - [API Specs](../03_Technical_Specs/02_API_SPECS.md)
  - [DB Schema](../03_Technical_Specs/01_DB_SCHEMA.md)
  - [QA Checklist](../05_QA_Validation/02_QA_CHECKLIST.md)
- 산출물:
  - OmniOne CX 인증 결과 처리
  - Open DID VC 발급·VP 검증
  - txId 기록 및 조회
  - 해시 표시 UI
- 완료 기준:
  - 최소 1개 OmniOne CX 인증, Open DID VC 발급, VP 검증, OmniOne Chain txId 표시가 모두 성공함
  - 개인정보 원문이 온체인에 기록되지 않음
  - 실패 시 데모 모드 fallback이 준비됨

### [ ] M-06. Soli 복지 매칭 데모 구현

- 우선순위: Medium
- 작업 유형: MVP Implementation
- 목표: 한국사회보장정보원 복지서비스 API 연동, 기본 조건·상황 체크리스트 입력, 복지 매칭 카드 표시 흐름을 구현한다.
- 필수 참조:
  - [Product Specs](../01_Concept_Design/03_PRODUCT_SPECS.md) — 3-6. 복지 데이터 연동 구조
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
| 공공 마이데이터 운영 API 연동 지연 | MVP 범위에서 개인 자격 확인을 제외하고, 복지서비스 API 실연동 기반 Soli 복지 매칭으로 범위를 축소 | `T-04`, `M-06` |
| AI 응답 품질 불안정 | 위기 키워드 룰 기반 스코어링을 fallback으로 구현 | `T-03`, `M-02` |
| 개인정보 이슈 | 실사용자 데이터 없이 데모 데이터와 DID 해시만 사용. 개인 행정정보 원문은 조회·저장하지 않음 | `T-01`, `T-02`, `T-04`, `M-05`, `M-06` |
| 범위 과대 | Phase 2 가족 안부 케어는 제외하고, 핵심 시연은 Soli 감지→담당자 승인→온체인 기록에 집중 | `P-05`, `M-02`, `M-04`, `M-05`, `M-06` |
| 발표 당일 네트워크 장애 | 로컬 데모 데이터와 녹화 영상을 백업으로 준비 | `Q-03`, `Q-04` |

---

## Related Documents

- **Documentation**: [Document Index](../00_DOCUMENT_INDEX.md) — 전체 문서와 백로그 ID 연결 지도
- **Logic_Progress**: [Roadmap](./00_ROADMAP.md) — 해커톤 일정 및 단계별 계획
- **Concept_Design**: [Product Specs](../01_Concept_Design/03_PRODUCT_SPECS.md) — 제안서 기준 MVP 범위
- **Concept_Design**: [Proposal Deck](../01_Concept_Design/04_PITCH_DECK.md) — 공모 제안서 본문 작성 기준
- **QA_Validation**: [QA Checklist](../05_QA_Validation/02_QA_CHECKLIST.md) — 제안서 및 MVP 계획 점검 항목

# Development Principles — no-one-alone
> Created: 2026-05-08 01:39
> Last Updated: 2026-05-13 12:30
> Backlog: D-01, P-05, T-01, T-02, M-01, M-05

> 현재 구현된 코드는 없다. 이 문서는 5월 제안서에서 실현 가능성을 설명하고, MVP 개발 단계에서 적용할 후보 개발 원칙이다.

## 1. 기술 스택

| 레이어 | 기술 | 버전 기준 |
|:---|:---|:---|
| Frontend | Next.js + TypeScript | Next.js 14+ (App Router) |
| Backend | NestJS + PostgreSQL | NestJS 10+, PostgreSQL 16+ |
| ORM | Drizzle ORM | 최신 stable |
| AI | Claude API (Anthropic) | MVP 개발 단계 진입 시 공식 최신 Sonnet 계열 모델 확인 후 확정 |
| Auth | OmniOne CX (모바일 신분증), Open DID | OmniOne CX SDK |
| Blockchain | OmniOne Chain | 공식 SDK |
| Infra | Vercel (Frontend) + AWS (Backend) | - |
| CI/CD | GitHub Actions | - |

---

## 2. 환경변수

### Frontend (`.env.local`)

```
NEXT_PUBLIC_API_URL=https://api.example.no-one-alone.kr
NEXT_PUBLIC_OMNI_CX_CLIENT_ID=
NEXT_PUBLIC_CHAIN_EXPLORER_URL=
```

### Backend (`.env`)

```
# Database
DATABASE_URL=postgresql://user:pass@host:5432/no_one_alone

# Anthropic
ANTHROPIC_API_KEY=

# OmniOne CX (모바일 신분증)
OMNI_CX_CLIENT_ID=
OMNI_CX_CLIENT_SECRET=
OMNI_CX_REDIRECT_URI=

# Open DID
OPEN_DID_ENDPOINT=
OPEN_DID_ISSUER_DID=

# OmniOne Chain
OMNI_CHAIN_RPC_URL=
OMNI_CHAIN_CONTRACT_ADDRESS=
OMNI_CHAIN_PRIVATE_KEY=

# JWT
JWT_SECRET=
JWT_EXPIRES_IN=7d

# App
NODE_ENV=development
PORT=3001
```

---

## 3. 프로젝트 구조

### Frontend (`/web`)

단일 반응형 웹 MVP. 별도 모바일 앱 없이 경로와 권한으로 화면 분리.

```
web/
├── app/
│   ├── page.tsx                — / 서비스 소개·진입
│   ├── checkin/                — /checkin Soli 정기 안부 (대상자)
│   ├── welfare/                — /welfare Soli 복지 매칭 (대상자)
│   ├── verify/                 — /verify OmniOne CX 본인 확인
│   ├── officer/                — /officer 담당자 대시보드
│   │   ├── page.tsx            — 위기 우선순위 리스트
│   │   ├── targets/            — 정기 안부 대상자 등록·관리
│   │   └── cases/[id]/         — 위기 케이스 상세 + 집행 승인
│   ├── proof/[txId]/           — /proof/:txId 온체인 기록 확인
│   └── api/                    — Next.js API Routes (BFF)
├── components/
│   ├── soli/               — Soli 챗봇 컴포넌트
│   ├── auth/               — OmniOne CX 인증 컴포넌트
│   └── chain/              — 온체인 기록 표시 컴포넌트
└── lib/
    ├── api.ts              — API 클라이언트
    └── omni-cx.ts          — OmniOne CX SDK 래퍼
```

### Backend (`/server`)

```
server/
├── src/
│   ├── auth/               — OmniOne CX DID 인증 모듈
│   ├── crisis/             — 위기도 스코어링 모듈
│   ├── soli/               — Claude API 챗봇 모듈
│   ├── targets/            — 정기 안부 대상자 등록 모듈
│   ├── welfare/            — Soli 복지 매칭 모듈
│   ├── dashboard/          — 담당자 대시보드 모듈
│   ├── chain/              — OmniOne Chain 연동 모듈
│   └── csr/                — 파일럿 이후 CSR 기부·ESG 리포트 후보 모듈
└── drizzle/
    └── schema.ts           — DB 스키마 (Drizzle)
```

---

## 4. 코딩 컨벤션

### 4-1. TypeScript

- `strict: true` 필수
- `any` 타입 사용 금지 — `unknown` 후 타입 가드 사용
- API 응답은 Zod 스키마로 런타임 검증
- 환경변수는 `env.ts`에서 중앙 검증 후 사용

### 4-2. 네이밍

| 대상 | 규칙 | 예시 |
|:---|:---|:---|
| 컴포넌트 | PascalCase | `CrisisScoreCard` |
| 함수·변수 | camelCase | `getCrisisScore` |
| 상수 | UPPER_SNAKE_CASE | `MAX_CRISIS_SCORE` |
| DB 컬럼 | snake_case | `crisis_score` |
| API 경로 | kebab-case | `/crisis-scores` |

### 4-3. Git 커밋 (Conventional Commits — 한국어)

```
feat(auth): OmniOne CX 본인 확인 연동
fix(soli): 위기 키워드 감지 누락 수정
chore(infra): Vercel 환경변수 설정 추가
docs(api): 집행 승인 엔드포인트 명세 추가
```

**타입 목록**: `feat` / `fix` / `chore` / `docs` / `refactor` / `test`

### 4-4. 브랜치 전략

```
main          — 배포 브랜치
develop       — 통합 브랜치
feat/[설명]   — 기능 개발
fix/[설명]    — 버그 수정
```

---

## 5. 보안 원칙

| 항목 | 원칙 |
|:---|:---|
| Soli 대화 데이터 | AES-256 암호화 저장, 담당자만 요약 접근 (원문 불가) |
| 온체인 데이터 | 집계·익명화 처리 후 기록 — 개인 특정 불가 |
| DID·VC | VC 원문 서버 저장 금지 — 검증 후 즉시 폐기, DID는 해시·가명 ID만 DB 저장 |
| API 인증 | JWT Bearer Token, 담당자·시민 역할 분리 (RBAC) |
| 개인정보 마스킹 | MVP 데모에서는 실제 주소 원문을 저장하지 않음. 파일럿 이후 실제 주소가 필요할 경우 목록에서는 마스킹하고 상세 진입 시만 복호화 |
| 환경변수 | `.env` Git 커밋 금지, AWS Secrets Manager 사용 |
| SQL 인젝션 | Drizzle ORM 파라미터 바인딩만 사용, raw query 금지 |

---

## 6. 성능 기준

| 항목 | 목표 |
|:---|:---|
| Soli 응답 지연 | MVP 3초 이내 목표 (Claude API 스트리밍 활용) |
| 대시보드 초기 로드 | LCP 2.5초 이하 |
| 위기 알림 | 스코어 갱신 후 5초 이내 담당자 웹소켓 전달 |
| 온체인 기록 | 집행 완료 후 비동기 처리 (사용자 대기 없음) |

---

## 7. 외부 SDK 및 연동 기술 레퍼런스

### 7-1. OmniOne CX (모바일 신분증)

- 제공: RaonSecure (라온시큐어), 해커톤 SDK 직접 제공
- GitHub: 별도 오픈소스 없음 — 해커톤 참가팀에게 SDK 및 연동 가이드 제공
- 연동 방식: 해커톤 제공 SDK·가이드 기준 표준 인증창 호출 → 콜백으로 검증 결과 수신. 연동 지연 시 Mock 인증 모드와 실제 SDK 연동 모드를 분리
- 콜백 응답 구조 (예시): `{ did_hash, verified_at, id_type, result_code }`
- MVP 구현 가능 기능:
  - 서비스 가입·로그인 시 신원 확인
  - 서비스 최초 가입·로그인 본인 인증
  - 지원 집행 직전 수급자 확인

### 7-2. Open DID

- 제공: 한국정보화진흥원 (행안부 주관), Apache-2.0 오픈소스
- GitHub 조직: https://github.com/OmniOneID (36개 저장소)
- 핵심 저장소:

| 저장소 | 역할 |
|:---|:---|
| `did-core-sdk-server` | DID Document 생성·관리 핵심 SDK |
| `did-issuer-server` | VC (Verifiable Credential) 발급 서버 |
| `did-verifier-server` | VP (Verifiable Presentation) 검증 서버 |
| `did-blockchain-sdk-server` | OmniOne Chain 연동 SDK |
| `did-ledger-service-server` | 체인 원장 조회·기록 API 서버 |
| `did-besu-contract` | Hyperledger Besu 스마트 컨트랙트 (DID·VC 메타데이터) |
| `did-client-sdk-ios` | iOS 클라이언트 SDK |
| `did-ca-aos` | Android CA 앱 SDK |
| `did-demo-server` | 전체 플로우 데모 서버 (MVP 참조 기준) |

- MVP 구현 가능 기능:
  - DID Document 생성 및 OmniOne Chain 등록 (`register-diddoc`)
  - VC 발급: 지원 연결 사실을 확인하는 지원 확인 VC 발급 (`did-issuer-server`)
  - VP 검증: 발급된 VC 기반 신원 증명 (`did-verifier-server`)
  - txId 조회 및 화면 표시
- MVP 최소 범위: `did-demo-server` 참조하여 VC 1개 발급 + txId 화면 표시

### 7-3. OmniOne Chain

- 기반: Hyperledger Besu (PoA + aBFT), 퍼미션드 체인
- GitHub: `OmniOneID/did-besu-contract`, `OmniOneID/did-ledger-service-server`
- Ledger API (`did-ledger-service-server` 제공):

| 엔드포인트 | 역할 |
|:---|:---|
| `POST /api/v1/diddoc/register` | DID Document 체인 등록 (txId 반환) |
| `GET /api/v1/diddoc?did={did}` | DID Document 조회 |
| `PUT /api/v1/diddoc/update` | DID Document 수정 |
| `POST /api/v1/vcmeta/register` | VC 메타데이터 등록 (txId 반환) |
| `GET /api/v1/vcmeta?vcId={vcId}` | VC 메타데이터 조회 |

- 온체인 기록 원칙: 개인정보 원문이 아닌 해시값만 기록 (임의 이벤트 로그 미지원)
- MVP에서 기록할 데이터:
  - 지원 확인 VC 메타데이터 해시 (`register-vcmeta`) — 지원 완료 증명
  - 지원 완료 증명 해시 → `support_executions.chain_tx_id`에 저장
  - 지원 완료 증명은 VC 구조로 설계하여 `register-vcmeta`에 맞춤

### 7-4. 복지 공공데이터 API

모두 공공데이터포털(data.go.kr) 발급, 개발·운영 자동 승인, 무료, REST/XML.

| API | URL | 용도 |
|:---|:---|:---|
| 중앙부처복지서비스 | data.go.kr/data/15090532 | Soli 복지 매칭 핵심 — 서비스명·지원대상·신청방법 |
| 지자체복지서비스 | data.go.kr/data/15108347 | 지역별 복지 서비스 추가 매칭 |
| 사회서비스 제공기관 | data.go.kr/data/15057683 | 담당자 대시보드 — 지역 기관 연결 |

- 공통 파라미터: `serviceKey`(발급 키), `pageNo`, `numOfRows`, `sido`/`signgu`(지역 코드)
- Soli 활용 흐름: 대화 맥락 + 기본 조건(연령대·지역·가구 형태) + 선택형 상황 체크리스트를 정규화 → 조건 필터링 → 복지서비스 목록 반환 → 추천 카드 표시 → 서비스URL로 복지로/정부24 외부 신청 링크
- 개인 자격 확인(건강보험 자격득실 등): 공공 마이데이터 이용기관 심사 필요 → MVP 범위 제외, 파일럿 이후 정식 연계

### 7-5. Claude API (Soli AI)

- 제공: Anthropic
- SDK: `@anthropic-ai/sdk` (npm)
- 문서: https://docs.anthropic.com
- MVP 구현 가능 기능:
  - SSE 스트리밍 응답 (Soli 응답 지연 3초 이내 목표)
  - 시스템 프롬프트 기반 위기 키워드 감지 및 스코어 산출
  - 한국어 복지 상담 최적화 시스템 프롬프트
- 권장 모델: MVP 개발 단계 진입 시 최신 Sonnet 계열 확인
- 주의: API 키는 서버 사이드에서만 사용, 프론트엔드 노출 금지

---

## Related Documents

- **UI_Screens**: [UI Design](../02_UI_Screens/01_UI_DESIGN.md) — 컴포넌트 설계
- **Technical_Specs**: [DB Schema](./01_DB_SCHEMA.md) — 데이터베이스 스키마
- **Technical_Specs**: [API Specs](./02_API_SPECS.md) — API 엔드포인트 명세
- **Technical_Specs**: [Blockchain DID Architecture](./04_BLOCKCHAIN_DID_ARCH.md) — Open DID·OmniOne Chain 실제 API 기반 상세 아키텍처

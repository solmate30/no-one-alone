# Development Principles — no-one-alone
> Created: 2026-05-08 01:39
> Last Updated: 2026-05-08 17:35
> Backlog: D-01, P-05, T-01, T-02, M-01, M-05

> 현재 구현된 코드는 없다. 이 문서는 5월 제안서에서 실현 가능성을 설명하고, 예선 통과 후 결선 MVP를 구현할 때 적용할 후보 개발 원칙이다.

## 1. 기술 스택

| 레이어 | 기술 | 버전 기준 |
|:---|:---|:---|
| Frontend | Next.js + TypeScript | Next.js 14+ (App Router) |
| Backend | NestJS + PostgreSQL | NestJS 10+, PostgreSQL 16+ |
| ORM | Drizzle ORM | 최신 stable |
| AI | Claude API (Anthropic) | 결선 시점 공식 최신 Sonnet 계열 모델 확인 후 확정 |
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

```
web/
├── app/
│   ├── (citizen)/          — 시민 앱 라우트
│   │   ├── report/         — 이웃 제보
│   │   ├── care/           — 가족 케어 등록
│   │   └── welfare/        — 자가 복지 신청
│   ├── (dashboard)/        — 담당자 대시보드
│   │   ├── priority/       — 위기 우선순위 리스트
│   │   └── case/[id]/      — 대상자 상세 + 집행
│   └── api/                — Next.js API Routes (BFF)
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
│   ├── reports/            — 이웃 제보 모듈
│   ├── crisis/             — 위기도 스코어링 모듈
│   ├── soli/               — Claude API 챗봇 모듈
│   ├── welfare/            — 복지 매칭·신청 모듈
│   ├── dashboard/          — 담당자 대시보드 모듈
│   ├── chain/              — OmniOne Chain 연동 모듈
│   └── csr/                — CSR 기부·ESG 리포트 모듈
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
feat(reports): 이웃 제보 OmniOne CX 인증 연동
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
| 개인정보 마스킹 | 대시보드 목록에서 이름·주소 마스킹, 상세 진입 시만 복호화 |
| 환경변수 | `.env` Git 커밋 금지, AWS Secrets Manager 사용 |
| SQL 인젝션 | Drizzle ORM 파라미터 바인딩만 사용, raw query 금지 |

---

## 6. 성능 기준

| 항목 | 목표 |
|:---|:---|
| Soli 응답 지연 | 결선 MVP 3초 이내 목표 (Claude API 스트리밍 활용) |
| 대시보드 초기 로드 | LCP 2.5초 이하 |
| 위기 알림 | 스코어 갱신 후 5초 이내 담당자 웹소켓 전달 |
| 온체인 기록 | 집행 완료 후 비동기 처리 (사용자 대기 없음) |

---

## Related Documents

- **UI_Screens**: [UI Design](../02_UI_Screens/01_UI_DESIGN.md) — 컴포넌트 설계
- **Technical_Specs**: [DB Schema](./01_DB_SCHEMA.md) — 데이터베이스 스키마
- **Technical_Specs**: [API Specs](./02_API_SPECS.md) — API 엔드포인트 명세

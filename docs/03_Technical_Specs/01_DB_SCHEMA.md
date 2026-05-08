# DB Schema — no-one-alone
> Created: 2026-05-08 01:39
> Last Updated: 2026-05-08 17:35
> Backlog: T-01, T-02, T-03, M-02, M-03, M-04, M-05

## 1. 설계 원칙

- **개인정보 최소화**: 온체인 기록에는 DID 해시만 저장, 실명·주소는 DB에서 암호화
- **역할 분리**: 시민(user) / 담당자(officer) / 기업(company) 테이블 분리
- **감사 추적**: 모든 집행·승인 행위에 `created_at`, `updated_at`, 담당자 ID 기록
- **Drizzle ORM**: 모든 스키마는 `drizzle/schema.ts`에서 관리

---

## 2. 테이블 명세

### 2-1. `users` — 시민 앱 사용자

```sql
users
├── id              UUID PRIMARY KEY DEFAULT gen_random_uuid()
├── did_hash        TEXT UNIQUE              -- OmniOne CX DID 해시
├── phone_hash      TEXT                     -- 연락처 해시 (원문 저장 금지)
├── role            TEXT NOT NULL            -- 'citizen' | 'officer' | 'admin'
├── is_verified     BOOLEAN DEFAULT false    -- OmniOne CX 인증 완료 여부
├── created_at      TIMESTAMPTZ DEFAULT now()
└── updated_at      TIMESTAMPTZ DEFAULT now()
```

### 2-2. `officers` — 복지 담당자

```sql
officers
├── id              UUID PRIMARY KEY DEFAULT gen_random_uuid()
├── user_id         UUID REFERENCES users(id)
├── district_code   TEXT NOT NULL            -- 읍면동 코드
├── district_name   TEXT NOT NULL            -- "강남구 삼성동 행정복지센터"
├── created_at      TIMESTAMPTZ DEFAULT now()
└── updated_at      TIMESTAMPTZ DEFAULT now()
```

### 2-3. `reports` — 이웃 제보

```sql
reports
├── id              UUID PRIMARY KEY DEFAULT gen_random_uuid()
├── reporter_did_hash TEXT NOT NULL          -- 제보자 DID 해시 (원문 저장 금지)
├── address         TEXT NOT NULL            -- 암호화된 주소
├── address_code    TEXT                     -- 법정동 코드 (매칭용)
├── description     TEXT NOT NULL            -- 상황 설명 (암호화)
├── status          TEXT DEFAULT 'pending'   -- 'pending' | 'reviewed' | 'resolved'
├── chain_tx_hash   TEXT                     -- 온체인 기록 TX 해시
├── officer_id      UUID REFERENCES officers(id)  -- 배정 담당자
├── created_at      TIMESTAMPTZ DEFAULT now()
└── updated_at      TIMESTAMPTZ DEFAULT now()
```

### 2-4. `crisis_scores` — 위기도 스코어

```sql
crisis_scores
├── id              UUID PRIMARY KEY DEFAULT gen_random_uuid()
├── target_did_hash TEXT NOT NULL            -- 대상자 DID 해시
├── score           NUMERIC(4,1) NOT NULL    -- 0.0 ~ 10.0
├── score_basis     JSONB                    -- 근거: {keywords, response_gap, reports, isolation}
├── source          TEXT NOT NULL            -- 'soli' | 'report' | 'manual'
├── officer_id      UUID REFERENCES officers(id)
├── created_at      TIMESTAMPTZ DEFAULT now()
└── updated_at      TIMESTAMPTZ DEFAULT now()
```

### 2-5. `care_registrations` — 가족 케어 등록

```sql
care_registrations
├── id              UUID PRIMARY KEY DEFAULT gen_random_uuid()
├── child_did_hash  TEXT NOT NULL            -- 자녀 DID 해시
├── parent_did_hash TEXT NOT NULL            -- 부모 DID 해시
├── parent_phone    TEXT                     -- 암호화된 부모 연락처
├── frequency       TEXT DEFAULT 'daily'     -- 'daily' | 'every_other_day'
├── alert_threshold NUMERIC(4,1) DEFAULT 6.0 -- 알림 발송 위기도 기준
├── is_active       BOOLEAN DEFAULT true
├── chain_tx_hash   TEXT                     -- 관계 인증 온체인 기록
├── created_at      TIMESTAMPTZ DEFAULT now()
└── updated_at      TIMESTAMPTZ DEFAULT now()
```

### 2-6. `welfare_applications` — 자가 복지 신청

```sql
welfare_applications
├── id              UUID PRIMARY KEY DEFAULT gen_random_uuid()
├── applicant_did_hash TEXT NOT NULL         -- 신청자 DID 해시
├── welfare_type    TEXT NOT NULL            -- 복지 종류 코드
├── welfare_name    TEXT NOT NULL            -- "긴급복지지원" 등
├── status          TEXT DEFAULT 'pending'   -- 'pending' | 'approved' | 'rejected'
├── verified_at     TIMESTAMPTZ              -- OmniOne CX 자격 확인 시각
├── officer_id      UUID REFERENCES officers(id)
├── created_at      TIMESTAMPTZ DEFAULT now()
└── updated_at      TIMESTAMPTZ DEFAULT now()
```

### 2-7. `support_executions` — 지원 집행

```sql
support_executions
├── id              UUID PRIMARY KEY DEFAULT gen_random_uuid()
├── recipient_did_hash TEXT NOT NULL         -- 수급자 DID 해시 (원문 저장 금지)
├── support_type    TEXT NOT NULL            -- '긴급생활비' | '식료품' | '의료비' 등
├── amount          NUMERIC(12,0)            -- 집행 금액 (원)
├── officer_id      UUID NOT NULL REFERENCES officers(id)
├── approved_at     TIMESTAMPTZ NOT NULL
├── chain_tx_hash   TEXT NOT NULL            -- OmniOne Chain TX 해시 (필수)
├── csr_donation_id UUID REFERENCES csr_donations(id)  -- CSR 연계 시
├── created_at      TIMESTAMPTZ DEFAULT now()
└── updated_at      TIMESTAMPTZ DEFAULT now()
```

### 2-8. `soli_conversations` — Soli 대화 로그

```sql
soli_conversations
├── id              UUID PRIMARY KEY DEFAULT gen_random_uuid()
├── user_did_hash   TEXT NOT NULL            -- 대화 사용자 DID 해시
├── messages        BYTEA NOT NULL           -- AES-256 암호화된 대화 전문
├── summary         TEXT                     -- AI 요약 (담당자 제공용)
├── emotion_tags    TEXT[]                   -- ['불안', '고립', '무기력'] 등
├── crisis_score    NUMERIC(4,1)             -- 이 대화에서 산출된 위기도
├── created_at      TIMESTAMPTZ DEFAULT now()
└── updated_at      TIMESTAMPTZ DEFAULT now()
```

### 2-9. `csr_donations` — 기업 CSR 기부

```sql
csr_donations
├── id              UUID PRIMARY KEY DEFAULT gen_random_uuid()
├── company_name    TEXT NOT NULL
├── total_amount    NUMERIC(14,0) NOT NULL   -- 총 기부 금액
├── executed_amount NUMERIC(14,0) DEFAULT 0  -- 집행된 금액
├── start_date      DATE NOT NULL
├── end_date        DATE
├── platform_fee    NUMERIC(5,2)             -- 수수료율 (%) 3~5
├── esg_report_url  TEXT                     -- 자동 생성된 ESG 리포트 URL
├── chain_tx_hash   TEXT                     -- 기부 등록 온체인 기록
├── created_at      TIMESTAMPTZ DEFAULT now()
└── updated_at      TIMESTAMPTZ DEFAULT now()
```

### 2-10. `insurance_data_exports` — 보험사 데이터 API 제공 이력

```sql
insurance_data_exports
├── id              UUID PRIMARY KEY DEFAULT gen_random_uuid()
├── company_name    TEXT NOT NULL            -- 계약 보험사명
├── export_type     TEXT NOT NULL            -- 'underwriting_aggregate' 등
├── period_start    DATE NOT NULL
├── period_end      DATE NOT NULL
├── query_scope     JSONB                    -- 지역·연령대 등 집계 조건
├── record_count    INTEGER NOT NULL         -- 집계 대상 건수
├── data_hash       TEXT NOT NULL            -- 제공 데이터셋 해시
├── consent_basis   TEXT NOT NULL            -- 동의/익명화 근거 문서 ID
├── created_at      TIMESTAMPTZ DEFAULT now()
└── updated_at      TIMESTAMPTZ DEFAULT now()
```

---

## 3. 인덱스

```sql
-- 위기도 스코어 최신 조회 (대시보드 우선순위)
CREATE INDEX idx_crisis_scores_target_created ON crisis_scores(target_did_hash, created_at DESC);

-- 제보 상태별 담당자 조회
CREATE INDEX idx_reports_officer_status ON reports(officer_id, status);

-- 케어 등록 부모 DID 조회
CREATE INDEX idx_care_parent ON care_registrations(parent_did_hash, is_active);

-- 대화 로그 사용자별 최신
CREATE INDEX idx_soli_user_created ON soli_conversations(user_did_hash, created_at DESC);
```

---

## 4. 온체인 기록 대상 정리

| 테이블 | 온체인 기록 시점 | 기록 내용 |
|:---|:---|:---|
| `reports` | 제보 접수 완료 | 제보자 DID 해시 + 타임스탬프 + 상황 해시 |
| `care_registrations` | 관계 인증 완료 | 자녀·부모 DID 해시 + 등록 타임스탬프 |
| `support_executions` | 집행 승인 완료 | 수급자 DID 해시 + 지원 종류·금액 해시 + 담당자 DID 해시 |
| `csr_donations` | 기부 등록 + 집행 | 기업명 해시 + 금액 집계 + 수혜자 수 |
| `insurance_data_exports` | 데이터셋 제공 승인 | 보험사명 해시 + 집계 범위 해시 + 제공 데이터셋 해시 |

---

## Related Documents

- **Technical_Specs**: [Development Principles](./00_DEVELOPMENT_PRINCIPLES.md) — ORM 및 보안 원칙
- **Technical_Specs**: [API Specs](./02_API_SPECS.md) — 각 테이블을 사용하는 API
- **Logic_Progress**: [Backlog](../04_Logic_Progress/00_BACKLOG.md) — 스키마 구현 태스크

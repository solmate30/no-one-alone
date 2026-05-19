# DB Schema — no-one-alone
> Created: 2026-05-08 01:39
> Last Updated: 2026-05-20 13:00
> Backlog: T-01, T-02, T-03, M-02, M-03, M-04, M-05

## 1. 설계 원칙

- **개인정보 최소화**: 온체인 기록에는 DID 해시만 저장, MVP 데모에서는 실제 실명·주소 원문을 저장하지 않음
- **MVP 데모 데이터 제한**: 실제 주소·상세 상황 설명은 저장하지 않고, 지역 코드·해시·데모 데이터 중심으로 시연
- **역할 분리**: 시민(user) / 담당자(officer) / 기업(company) 테이블 분리
- **감사 추적**: 모든 집행·승인 행위에 `created_at`, `updated_at`, 담당자 ID 기록
- **Drizzle ORM**: 모든 스키마는 `drizzle/schema.ts`에서 관리

---

## 2. 테이블 명세

### 2-1. `users` — 대상자 웹 사용자

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

### 2-3. `crisis_scores` — 위기도 스코어

```sql
crisis_scores
├── id              UUID PRIMARY KEY DEFAULT gen_random_uuid()
├── target_did_hash TEXT NOT NULL            -- 대상자 DID 해시
├── score           NUMERIC(4,1) NOT NULL    -- 0.0 ~ 10.0
├── score_basis     JSONB                    -- 근거: {keywords(40%), response_gap(35%), isolation(25%)}
├── source          TEXT NOT NULL            -- 'soli' | 'manual'
├── officer_id      UUID REFERENCES officers(id)
├── created_at      TIMESTAMPTZ DEFAULT now()
└── updated_at      TIMESTAMPTZ DEFAULT now()
```

### 2-4. `monitoring_targets` — 정기 전화 대상자 등록

> **MVP 범위**: 현장 QR 자가 가입 또는 담당자 등록 후, 대상자 본인 동의 기반으로 솔이 정기 전화를 시작한다. 자가 가입은 수급 자격을 확정하는 복지 신청이 아니라, 솔이가 먼저 전화할 수 있도록 수신 동의를 확보하고 필요 시 복지 연결로 이어지는 안부 연결 신청이다. 전화 이후 2단계에서 SMS 또는 웹 채팅 중 사용자가 선택한 채널로 대화를 이어간다.

```sql
monitoring_targets
├── id              UUID PRIMARY KEY DEFAULT gen_random_uuid()
├── target_did_hash TEXT NOT NULL            -- 대상자 DID 해시
├── target_phone_hash       TEXT NOT NULL    -- 전화번호 해시 (검색·중복 방지용, 발신 불가)
├── target_phone_ciphertext TEXT NOT NULL    -- 암호화된 전화번호 원문 (AES-256-GCM, 발신·SMS 전송에만 사용)
├── district_code   TEXT NOT NULL            -- 담당 관할 코드
├── consented_at    TIMESTAMPTZ              -- 정기 전화 수신 동의 완료 시각
├── frequency       TEXT DEFAULT 'weekly'    -- 'weekly' | 'twice_weekly' | 'three_four_weekly'
├── preferred_time  TEXT                     -- 대상자가 선호하는 통화 시간대
├── alert_threshold NUMERIC(4,1) DEFAULT 7.0 -- 담당자 알림 발송 위기도 기준
├── is_active       BOOLEAN DEFAULT true
├── created_at      TIMESTAMPTZ DEFAULT now()
└── updated_at      TIMESTAMPTZ DEFAULT now()
```

### 2-5. `welfare_matches` — 솔이 복지 매칭 결과

```sql
welfare_matches
├── id              UUID PRIMARY KEY DEFAULT gen_random_uuid()
├── user_did_hash   TEXT NOT NULL            -- 대상자 DID 해시
├── signal_id       UUID                     -- 솔이 통화·SMS·웹 채팅 신호 ID
├── profile         JSONB                    -- 연령대·지역·가구 형태 등 직접 입력 조건
├── situation_tags  TEXT[]                   -- 실직·질병·주거 불안·돌봄 공백 등 체크리스트
├── welfare_code    TEXT NOT NULL            -- 복지서비스 코드
├── welfare_name    TEXT NOT NULL            -- "긴급복지지원" 등
├── match_score     NUMERIC(4,2)             -- 0.00 ~ 1.00
├── match_basis     JSONB                    -- 매칭 근거: 키워드·조건·체크리스트
├── apply_url       TEXT                     -- 복지로/정부24 외부 신청 링크
├── created_at      TIMESTAMPTZ DEFAULT now()
└── updated_at      TIMESTAMPTZ DEFAULT now()
```

### 2-6. `support_executions` — 지원 집행

```sql
support_executions
├── id              UUID PRIMARY KEY DEFAULT gen_random_uuid()
├── recipient_did_hash TEXT NOT NULL         -- 대상자 DID 해시 (원문 저장 금지)
├── support_type    TEXT NOT NULL            -- '긴급생활비' | '식료품' | '의료비' 등
├── amount          NUMERIC(12,0)            -- 집행 금액 (원)
├── officer_id      UUID NOT NULL REFERENCES officers(id)
├── approved_at     TIMESTAMPTZ NOT NULL
├── chain_tx_id     TEXT NOT NULL            -- OmniOne Chain txId (필수)
├── csr_donation_id UUID REFERENCES csr_donations(id)  -- CSR 연계 시
├── created_at      TIMESTAMPTZ DEFAULT now()
└── updated_at      TIMESTAMPTZ DEFAULT now()
```

### 2-7. `soli_call_sessions` — 솔이 전화 통화 로그 (위기 감지 1차 소스)

```sql
soli_call_sessions
├── id              UUID PRIMARY KEY DEFAULT gen_random_uuid()
├── target_did_hash TEXT NOT NULL            -- 통화 대상자 DID 해시
├── call_status     TEXT NOT NULL            -- 'scheduled' | 'completed' | 'missed' | 'failed'
├── scheduled_at    TIMESTAMPTZ
├── started_at      TIMESTAMPTZ
├── ended_at        TIMESTAMPTZ
├── absence_count   INTEGER DEFAULT 0
├── stt_ciphertext  BYTEA                    -- AES-256 암호화된 STT 전문
├── summary         TEXT                     -- AI 요약 (담당자 제공용)
├── emotion_tags    TEXT[]                   -- ['불안', '고립', '무기력'] 등
├── crisis_score    NUMERIC(4,1)             -- 이 대화에서 산출된 위기도
├── created_at      TIMESTAMPTZ DEFAULT now()
└── updated_at      TIMESTAMPTZ DEFAULT now()
```

### 2-8. `soli_conversations` — 솔이 SMS·웹 채팅 로그

```sql
soli_conversations
├── id                   UUID PRIMARY KEY DEFAULT gen_random_uuid()
├── user_did_hash        TEXT NOT NULL            -- 대상자 DID 해시
├── channel              TEXT NOT NULL            -- 'sms' | 'web'
├── provider_message_id  TEXT                     -- SMS Provider 메시지 ID (channel='sms'일 때)
├── from_phone_hash      TEXT                     -- 발신 전화번호 해시 (channel='sms'일 때)
├── messages             BYTEA NOT NULL           -- AES-256 암호화된 대화 전문
├── summary              TEXT                     -- AI 요약 (담당자 제공용)
├── emotion_tags         TEXT[]                   -- ['불안', '고립', '무기력'] 등
├── crisis_score         NUMERIC(4,1)             -- 이 대화에서 산출된 위기도
├── created_at           TIMESTAMPTZ DEFAULT now()
└── updated_at           TIMESTAMPTZ DEFAULT now()
```

### 2-9. `csr_donations` — 기업 CSR 기부

> **Future scope**: MVP 구현 대상이 아니다. 집행 증명 구조가 CSR 증빙으로 확장될 수 있음을 설명하기 위한 파일럿 이후 후보 테이블이다.

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
├── chain_tx_id     TEXT                     -- 기부 등록 온체인 기록
├── created_at      TIMESTAMPTZ DEFAULT now()
└── updated_at      TIMESTAMPTZ DEFAULT now()
```

### 2-10. `insurance_data_exports` — 보험사 데이터 API 제공 이력

> **Future scope**: MVP 구현 대상이 아니다. 보험사에는 개인 단위 데이터가 아니라 집계·비식별 통계만 제공한다는 장기 사업 경계를 설명하기 위한 후보 테이블이다.

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

-- 정기 전화 대상자 조회
CREATE INDEX idx_monitoring_targets ON monitoring_targets(district_code, is_active);

-- 통화 로그 사용자별 최신
CREATE INDEX idx_soli_call_target_created ON soli_call_sessions(target_did_hash, created_at DESC);

-- SMS·웹 채팅 로그 사용자별 최신
CREATE INDEX idx_soli_user_created ON soli_conversations(user_did_hash, created_at DESC);
```

---

## 4. 온체인 기록 대상 정리

| 테이블 | 온체인 기록 시점 | 기록 내용 |
|:---|:---|:---|
| `welfare_matches` | 복지 매칭 결과 참조 | 매칭 결과 해시 + 생성 타임스탬프 |
| `support_executions` | 집행 승인 완료 | 대상자 DID 해시 + 지원 종류·금액 해시 + 담당자 DID 해시 |
| `csr_donations` | 파일럿 이후 | 기업명 해시 + 금액 집계 + 수혜자 수 |
| `insurance_data_exports` | 파일럿 이후 | 보험사명 해시 + 집계 범위 해시 + 제공 데이터셋 해시 |

---

## Related Documents

- **Technical_Specs**: [Development Principles](./00_DEVELOPMENT_PRINCIPLES.md) — ORM 및 보안 원칙
- **Technical_Specs**: [API Specs](./02_API_SPECS.md) — 각 테이블을 사용하는 API
- **Logic_Progress**: [Backlog](../04_Logic_Progress/00_BACKLOG.md) — 스키마 구현 태스크

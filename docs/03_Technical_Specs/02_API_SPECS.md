# API Specs — no-one-alone
> Created: 2026-05-08 01:39
> Last Updated: 2026-05-20 13:00
> Backlog: T-01, T-02, T-03, M-02, M-03, M-04, M-05

## 1. 공통 규칙

- **Base URL**: `https://api.example.no-one-alone.kr/v1` (예시)
- **인증**: `Authorization: Bearer <JWT>` (모든 보호된 엔드포인트)
- **Content-Type**: `application/json`
- **응답 형식**:

```json
{
  "success": true,
  "data": { ... },
  "error": null
}
```

- **에러 형식**:

```json
{
  "success": false,
  "data": null,
  "error": { "code": "UNAUTHORIZED", "message": "인증이 필요합니다." }
}
```

---

## 2. `/auth` — OmniOne CX DID 인증

### `POST /auth/omni-cx/start`
OmniOne CX 인증 세션 시작

**Request**
```json
{ "redirect_uri": "https://no-one-alone.kr/auth/callback" }
```

**Response**
```json
{
  "session_id": "sess_abc123",
  "auth_url": "https://omni-cx.example/auth?session=sess_abc123"
}
```

---

### `POST /auth/omni-cx/verify`
OmniOne CX 인증 콜백 처리 → JWT 발급

**Request**
```json
{
  "session_id": "sess_abc123",
  "vc_token": "vc_eyJ..."
}
```

**Response**
```json
{
  "access_token": "eyJ...",
  "user": {
    "did_hash": "sha256:abc123...",
    "role": "citizen",
    "is_verified": true
  }
}
```

---

### `POST /auth/did/issue-beneficiary-vc`
Open DID — 지원 확인 VC 발급

**Request** (인증 필요)
```json
{
  "purpose": "support_confirmation",
  "application_id": "app_xyz"
}
```

**Response**
```json
{
  "beneficiary_did": "did:open:xyz789",
  "vc_id": "vc_123",
  "vc_metadata_hash": "sha256:vcmeta..."
}
```

---

### `POST /auth/did/verify-vp`
Open DID — 제출된 VP 검증

**Request** (인증 필요)
```json
{
  "vp_token": "vp_eyJ...",
  "required_claim": "support_confirmation"
}
```

**Response**
```json
{
  "verified": true,
  "subject_did_hash": "sha256:abc123...",
  "verified_at": "2026-05-08T11:10:00Z"
}
```

---

## 3. `/crisis` — 위기도 스코어

### `POST /crisis/score`
위기도 스코어 산출 (내부 서비스 전용)

**Request**
```json
{
  "target_did_hash": "sha256:target123...",
  "source": "soli_call",
  "soli_signal_id": "call_abc"
}
```

**Response**
```json
{
  "score": 7.4,
  "score_basis": {
    "keywords": 3.2,
    "response_gap": 2.6,
    "isolation": 1.6
  },
  "source_weights": {
    "keywords": 0.4,
    "response_gap": 0.35,
    "isolation": 0.25
  }
}
```

---

### `GET /crisis/scores` (담당자 전용)
관할 지역 위기 우선순위 리스트

**Query**: `?district_code=1168011000&limit=20`

**Response**
```json
{
  "items": [
    {
      "target_did_masked": "sha256:***456",
      "latest_score": 8.2,
      "trend": "rising",
      "eligibility_status": "verified",
      "last_soli_response_gap_hours": 48
    }
  ]
}
```

---

## 4. `/soli` — 솔이 전화 및 SMS·웹 채팅

솔이의 1단계는 아웃바운드 전화다. 2단계에서 대상자는 SMS 또는 웹 채팅(/checkin) 중 편한 채널을 선택한다. 두 채널은 병렬 운영되며, 모든 신호는 동일하게 NOA 서버가 수신·처리해 담당자 대시보드에 반영한다.

### `POST /soli/calls/schedule`
솔이 정기 전화 예약 (담당자 전용)

**Request**
```json
{
  "target_did_hash": "sha256:target123...",
  "frequency": "weekly",
  "preferred_time": "09:00"
}
```

> `target_did_hash`로 DB의 `monitoring_targets.target_phone_ciphertext`를 조회해 복호화한 뒤 Provider에 전달한다. 전화번호 원문은 API 요청에 포함하지 않는다.

**Response**
```json
{
  "call_schedule_id": "sched_abc",
  "next_call_at": "2026-07-22T00:00:00Z"
}
```

---

### `POST /soli/calls/webhook`
아웃바운드 통화 결과 수신 (전화 API webhook)

**Request**
```json
{
  "call_id": "call_abc",
  "target_did_hash": "sha256:target123...",
  "status": "completed",
  "duration_seconds": 312,
  "stt_ciphertext_ref": "s3://encrypted/call_abc",
  "absence_count": 0
}
```

**Response**
```json
{
  "accepted": true,
  "analysis_job_id": "job_abc"
}
```

---

### `POST /soli/chat`
솔이 웹 채팅 채널 (인증 필요 — 시민, JWT/DID 기반)

**Request**
```json
{
  "conversation_id": "conv_abc",
  "channel": "web",
  "message": "요즘 너무 힘들어요."
}
```

**Response** (스트리밍 SSE)
```
data: {"delta": "많이 힘드시겠어요. "}
data: {"delta": "어떤 부분이 가장 힘드세요?"}
data: {"done": true, "crisis_score": 5.2}
```

---

### `POST /soli/webhook/sms`
솔이 SMS 채널 수신 웹훅 (인증 불필요 — 통신사 Provider 발신)

MVP에서는 Twilio / 알리고 / NCP 중 1개 실연동 또는 mock으로 대체한다.

**Request** (Provider webhook payload)
```json
{
  "provider":          "twilio",
  "provider_message_id": "SM_abc123",
  "from_phone_hash":   "sha256:...",
  "body":              "요즘 많이 힘드네요",
  "received_at":       "2026-08-01T09:00:00Z"
}
```

**Response**
```json
{ "queued": true, "signal_id": "sig_xyz" }
```

---

### `GET /soli/summary/:signal_id` (담당자 전용)
솔이 통화·SMS·웹 채팅 요약 조회 (원문 아님)

**Response**
```json
{
  "source": "call",
  "summary": "최근 통화에서 경제적 어려움과 사회적 고립감 표현. 목소리 에너지 저하와 외출 빈도 감소 언급.",
  "emotion_tags": ["불안", "고립"],
  "crisis_score": 6.8
}
```

---

## 5. `/welfare` — 솔이 복지 매칭

### `POST /welfare/match`
복지 자동 매칭 (가입·로그인 인증 세션 필요)

**Request**
```json
{
  "conversation_id": "conv_abc",
  "profile": {
    "age_group": "65+",
    "region_code": "11680",
    "household_type": "single"
  },
  "situation_tags": ["질병", "주거 불안", "긴급 생계"]
}
```

**Response**
```json
{
  "matched": [
    {
      "code": "W001",
      "name": "긴급복지지원",
      "description": "생계·의료·주거 위기 시 즉시 지원",
      "match_score": 0.86,
      "match_basis": ["긴급 생계", "1인 가구", "주거 불안"],
      "apply_url": "https://www.bokjiro.go.kr"
    }
  ]
}
```

---

## 6. `/dashboard` — 담당자 도구

### `GET /dashboard/priority` (담당자 전용)
오늘의 케어 우선순위 리스트

**Response**
```json
{
  "total_pending": 12,
  "items": [
    {
      "id": "case_abc",
      "score": 8.2,
      "soli_gap_hours": 48,
      "eligibility_status": "verified",
      "care_type": ["솔이 감지", "솔이 복지 매칭", "담당자 등록"]
    }
  ]
}
```

---

### `POST /dashboard/execute` (담당자 전용)
지원 집행 승인

**Request**
```json
{
  "target_did_hash": "sha256:target123...",
  "support_type": "긴급생활비",
  "amount": 500000,
  "recipient_vc": "vc_eyJ..."
}
```

**Response**
```json
{
  "execution_id": "exec_abc",
  "chain_tx_id": "0xabc123...",
  "approved_at": "2026-05-08T12:00:00Z"
}
```

---

## 7. `/chain` — OmniOne Chain 기록 조회

### `GET /chain/record/:tx_id`
특정 txId 상세 조회

**Response**
```json
{
  "tx_id": "0xabc123",
  "type": "support_execution",
  "timestamp": "2026-05-08T12:00:00Z",
  "data_hash": "sha256:xyz...",
  "block_number": 1234567
}
```

---

### `GET /chain/history/:target_did_hash` (담당자 전용)
대상자 온체인 이력

---

## 8. Future APIs — MVP 이후 확장 후보

아래 API는 2026-07-01 ~ 2026-09-21 MVP 구현 범위가 아니다. 제안서에서는 사업 확장 가능성을 설명하기 위한 후보 계약으로만 다루며, 결선 MVP에서는 솔이 감지, 담당자 승인, 본인 확인, VC/txId 표시 흐름을 우선 구현한다.

### 8-1. `/csr` — CSR 기부·ESG 리포트

#### `POST /csr/donations` (기업 관리자)
CSR 기부 등록

**Request**
```json
{
  "company_name": "(주)no-one-alone 파트너스",
  "total_amount": 100000000,
  "start_date": "2026-06-01",
  "end_date": "2026-12-31"
}
```

---

#### `GET /csr/donations/:id/report` (기업 관리자)
ESG 리포트 자동 생성

**Response**
```json
{
  "total_executed": 87000000,
  "recipient_count": 127,
  "breakdown": {
    "food": 43,
    "medical": 31,
    "living": 26
  },
  "avg_score_before": 7.2,
  "avg_score_after": 4.1,
  "report_url": "https://no-one-alone.kr/reports/csr_xyz.pdf"
}
```

---

### 8-2. `/data-products` — 보험사 대상 익명 집계 데이터 상품 후보

#### `POST /data-products/insurance/exports` (관리자 전용)
보험사 대상 비식별·집계 데이터 상품 생성 요청

**Request**
```json
{
  "company_name": "sample-insurance",
  "export_type": "underwriting_aggregate",
  "period_start": "2026-01-01",
  "period_end": "2026-06-30",
  "query_scope": {
    "region_level": "district",
    "age_band": "70+"
  },
  "consent_basis": "privacy-policy-v1"
}
```

**Response**
```json
{
  "export_id": "exp_abc",
  "record_count": 1200,
  "data_hash": "sha256:abc...",
  "download_url": "https://api.example.no-one-alone.kr/v1/data-products/insurance/exports/exp_abc/download"
}
```

#### `GET /data-products/insurance/exports/:id` (계약 보험사 전용)
생성된 비식별·집계 데이터 상품 메타데이터 조회

**Response**
```json
{
  "export_id": "exp_abc",
  "export_type": "underwriting_aggregate",
  "period": {
    "start": "2026-01-01",
    "end": "2026-06-30"
  },
  "record_count": 1200,
  "data_hash": "sha256:abc...",
  "privacy_level": "aggregated_anonymized"
}
```

---

## Related Documents

- **Technical_Specs**: [DB Schema](./01_DB_SCHEMA.md) — 각 API가 사용하는 테이블
- **Technical_Specs**: [Blockchain DID Architecture](./04_BLOCKCHAIN_DID_ARCH.md) — `/auth/omni-cx/verify`, `/chain/record/:tx_id` 등 온체인 연동 API의 아키텍처 상세
- **UI_Screens**: [Screen Flow](../02_UI_Screens/00_SCREEN_FLOW.md) — API가 호출되는 화면
- **QA_Validation**: [Test Scenarios](../05_QA_Validation/01_TEST_SCENARIOS.md) — API 테스트 시나리오

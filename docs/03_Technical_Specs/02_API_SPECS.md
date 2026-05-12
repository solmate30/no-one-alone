# API Specs — no-one-alone
> Created: 2026-05-08 01:39
> Last Updated: 2026-05-08 17:35
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

### `POST /auth/did/issue`
Open DID — 시민 제보자 DID 발급

**Request** (인증 필요)
```json
{ "purpose": "reporter" }
```

**Response**
```json
{
  "did": "did:open:xyz789",
  "vc": "vc_eyJ..."
}
```

---

## 3. `/reports` — 이웃 제보

### `POST /reports`
제보 접수 (인증 필요 — 시민)

**Request**
```json
{
  "address": "서울시 강남구 삼성동 123",
  "description": "2주째 우편물이 쌓여 있고 소리가 없습니다.",
  "reporter_vc": "vc_eyJ..."
}
```

**Response**
```json
{
  "report_id": "rpt_abc",
  "status": "pending",
  "chain_tx_hash": "0xabc...",
  "estimated_review_hours": 24
}
```

---

### `GET /reports/:id`
제보 상세 조회 (인증 필요 — 담당자 or 제보자 본인)

**Response**
```json
{
  "id": "rpt_abc",
  "status": "reviewed",
  "created_at": "2026-05-08T10:00:00Z",
  "chain_tx_hash": "0xabc...",
  "officer": { "district_name": "강남구 삼성동 행정복지센터" }
}
```

---

### `GET /reports` (담당자 전용)
담당자 관할 제보 목록

**Query**: `?status=pending&page=1&limit=20`

---

### `PATCH /reports/:id/status` (담당자 전용)
제보 상태 업데이트

**Request**
```json
{ "status": "resolved", "note": "현장 방문 완료" }
```

---

## 4. `/crisis` — 위기도 스코어

### `POST /crisis/score`
위기도 스코어 산출 (내부 서비스 전용)

**Request**
```json
{
  "target_did_hash": "sha256:target123...",
  "source": "soli",
  "soli_conversation_id": "conv_abc"
}
```

**Response**
```json
{
  "score": 7.4,
  "score_basis": {
    "keywords": 3.2,
    "response_gap": 2.1,
    "reports": 1.5,
    "isolation": 0.6
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
      "report_count": 2,
      "last_soli_response_gap_hours": 48
    }
  ]
}
```

---

## 5. `/soli` — Soli 챗봇

### `POST /soli/chat`
Soli 대화 (인증 필요 — 시민)

**Request**
```json
{
  "conversation_id": "conv_abc",
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

### `GET /soli/summary/:conversation_id` (담당자 전용)
Soli 대화 요약 조회 (원문 아님)

**Response**
```json
{
  "summary": "최근 2주간 경제적 어려움과 사회적 고립감 표현. 외출 빈도 감소.",
  "emotion_tags": ["불안", "고립"],
  "crisis_score": 6.8
}
```

---

## 6. `/welfare` — 복지 매칭·신청

### `POST /welfare/match`
복지 자동 매칭 (인증 필요 — 시민)

**Request**
```json
{ "conversation_id": "conv_abc" }
```

**Response**
```json
{
  "matched": [
    {
      "code": "W001",
      "name": "긴급복지지원",
      "description": "생계·의료·주거 위기 시 즉시 지원",
      "eligible": true
    }
  ]
}
```

---

### `POST /welfare/apply`
복지 신청 (인증 필요 — OmniOne CX 자격 검증 포함)

**Request**
```json
{
  "welfare_code": "W001",
  "applicant_vc": "vc_eyJ..."
}
```

**Response**
```json
{
  "application_id": "app_xyz",
  "status": "pending",
  "verified_at": "2026-05-08T11:00:00Z"
}
```

---

## 7. `/dashboard` — 담당자 도구

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
      "report_count": 2,
      "soli_gap_hours": 48,
      "care_type": ["이웃 제보", "가족 케어"]
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
  "chain_tx_hash": "0xabc123...",
  "approved_at": "2026-05-08T12:00:00Z"
}
```

---

## 8. `/chain` — OmniOne Chain 기록 조회

### `GET /chain/record/:tx_hash`
특정 TX 상세 조회

**Response**
```json
{
  "tx_hash": "0xabc123",
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

## 9. `/csr` — CSR 기부·ESG 리포트

### `POST /csr/donations` (기업 관리자)
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

### `GET /csr/donations/:id/report` (기업 관리자)
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

## 10. `/data-api` — 보험사 익명 집계 데이터 API

### `POST /data-api/insurance/exports` (관리자 전용)
보험사 제공용 익명·집계 데이터셋 생성 요청

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
  "download_url": "https://api.example.no-one-alone.kr/v1/data-api/insurance/exports/exp_abc/download"
}
```

### `GET /data-api/insurance/exports/:id` (계약 보험사 전용)
생성된 익명 집계 데이터셋 메타데이터 조회

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
- **UI_Screens**: [Screen Flow](../02_UI_Screens/00_SCREEN_FLOW.md) — API가 호출되는 화면
- **QA_Validation**: [Test Scenarios](../05_QA_Validation/01_TEST_SCENARIOS.md) — API 테스트 시나리오

# 블록체인·DID 아키텍처
> Created: 2026-05-18 00:00
> Last Updated: 2026-05-20 13:00
> Backlog: T-10

---

## 1. 아키텍처 개요

NOA는 복지 집행의 투명성과 대상자 신원 보호를 동시에 달성하기 위해 Open DID 오픈소스 생태계와 OmniOne Chain을 결합한다. 블록체인·DID 기술은 두 신뢰 포인트에서 개입한다: ① 가입·로그인 본인확인, ② 집행 직전 지원 승인 사실·신원 이중 확인.

### 시스템 역할 구성도

```
대상자 ──────────────────────────────── NOA 플랫폼 (솔이 AI + 대시보드)
  │  OmniOne CX 인증 (신뢰 포인트 1·2)       │
  │                                        │
  │                              Open DID 서버군
  │                          (TAS · Issuer · Verifier)
  │                                        │ DID 등록 · VC 메타 기록
  │                                        ▼
담당자 ──── 케이스 승인 ──────────── OmniOne Chain (Hyperledger Besu)
                                          │ txId
                                          ▼
                                       대상자에게 txId 공개
```

### 핵심 신뢰 체인 흐름

```
[가입] OmniOne CX 본인확인
  → TAS: DID Document 생성 + OmniOne Chain 등록 (txId-1)
  → 솔이 정기 전화·SMS·웹 채팅 감지 → 위기도 스코어링
  → 담당자 대시보드: 케이스 검토·승인
  → Issuer Server: 지원 확인 VC 발급 + OmniOne Chain vcmeta 등록 (txId-2)
[집행 직전] OmniOne CX 재확인 + Verifier Server: VP 검증
  → 복지 집행 + 집행 이벤트 해시 OmniOne Chain 기록 (txId-3)
  → 대상자에게 txId-3 공개
```

---

## 2. OmniOne CX 연동 — 2개 신뢰 포인트

OmniOne CX는 RaonSecure의 모바일 신분증 서비스다. NOA는 가입·집행의 두 시점에서 OmniOne CX를 신원 확인 트리거로 사용하며, 두 경우 모두 NOA 백엔드가 인증 창 요청을 중개하고 결과를 JWT 또는 VP 흐름에 연계한다.

### 신뢰 포인트 1 — 가입·로그인 본인확인

```
대상자 앱          NOA 백엔드           OmniOne CX
    │                  │                    │
    │── POST /auth/omni-cx/start ──────▶│   │
    │◀── { session_id, auth_url } ──────│   │
    │── [CX 인증 창 열기] ───────────────────▶│
    │◀─────────────── [인증 완료 콜백] ────────│
    │── POST /auth/omni-cx/verify ──────▶│   │
    │◀── { access_token, did_hash, is_verified } ──│
    │                  │                    │
    │        (is_verified = true 이면 TAS P132 DID 등록 흐름 연계)
```

콜백 수신 후 NOA 백엔드는 `did_hash`를 `users.did_hash`에 저장하고 JWT를 발급한다. 실제 SDK 콜백 파라미터명은 해커톤 제공 OmniOne CX SDK 연동 가이드를 기준으로 구현하며, `did_hash`·`is_verified`는 NOA 내부 필드명이다.

### 신뢰 포인트 2 — 집행 직전 대상자 재확인

담당자가 집행 승인을 클릭하면 대상자 앱에 OmniOne CX 재확인을 요청한다. 재확인이 완료된 후에만 Verifier Server의 VP 검증(P310)이 시작되며, 두 확인이 결합되어 "담당자가 승인한 지원 대상이고 본인도 맞다"를 한 번에 증명한다.

```
담당자 대시보드   NOA 백엔드        대상자 앱         OmniOne CX
    │                │                  │                 │
    │── 집행 승인 ──▶│                  │                 │
    │               │── 재확인 요청 ───▶│                 │
    │               │                  │── [CX 재확인] ──▶│
    │               │                  │◀── 확인 완료 ────│
    │               │◀── is_verified ───│                 │
    │               │── Verifier Server P310: VP 검증 시작
    │               │── 집행 이벤트 해시 → OmniOne Chain (txId-3)
    │               │── txId-3 공개 ───▶│
```

---

## 3. Open DID 컴포넌트 구성

Open DID는 RaonSecure가 Apache 2.0 라이선스로 공개한 서버 컴포넌트 집합이다 ([OmniOneID GitHub](https://github.com/OmniOneID)). NOA에서 사용하는 컴포넌트는 다음과 같다.

| 컴포넌트 | 레포지토리 | NOA에서의 역할 |
|:---|:---|:---|
| Trust Anchor Server (TAS) | `did-ta-server` | 신뢰 루트. 사용자 DID 등록·KYC 조율, VC 발급 흐름 중개 |
| Issuer Server | `did-issuer-server` | 지원 확인 VC 발급 (담당 복지 기관 = Issuer) |
| Verifier Server | `did-verifier-server` | 집행 직전 VP 검증 |
| Ledger Service Server | `did-ledger-service-server` | OmniOne Chain 온체인 기록 인터페이스 |
| Blockchain SDK | `did-blockchain-sdk-server` | 체인 스마트컨트랙트 직접 호출 레이어 |
| Core SDK | `did-core-sdk-server` | DID Document·VC·VP 데이터 모델 생성·검증 |
| CA Server | `did-ca-server` | 기관 인증서 (Certificate VC) 관리 |

---

## 4. OmniOne Chain 네트워크

OmniOne Chain은 Hyperledger Besu 기반의 허가형(permissioned) 블록체인이다. Blockchain SDK(`did-blockchain-sdk-server`)는 Hyperledger Fabric 게이트웨이와 web3j(Ethereum 호환) 양쪽을 지원하며, OmniOne Chain은 Besu(web3j 경로)로 연결된다.

### 온체인 기록 원칙

| 기록 가능 | 기록 불가 |
|:---|:---|
| DID Document (인코딩된 문서 전체) | 대상자 성명·주소·연락처 등 PII 원문 |
| VC 메타데이터 (ID·상태·발급자·스키마 참조) | 솔이 통화·SMS·웹 채팅 원문 |
| 집행 이벤트 해시 (did_hash + 복지유형 + 금액 + 타임스탬프) | 위기도 점수 원문 |

### Ledger Service API (실제 엔드포인트)

쓰기 연산은 Bearer 토큰 인증 필요. 모든 쓰기 연산은 `txId`를 반환한다.

| 연산 | 메서드 | 경로 | 주요 파라미터 |
|:---|:---|:---|:---|
| DID Document 등록 | POST | `/api/v1/diddoc/register` | 멀티베이스 인코딩된 DID Document |
| DID Document 조회 | GET | `/api/v1/diddoc` | `?did={did_identifier}` |
| DID Document 수정 | PUT | `/api/v1/diddoc/update` | 수정된 DID Document |
| VC 메타데이터 등록 | POST | `/api/v1/vcmeta/register` | VC ID·상태·발급자·스키마 참조 |
| VC 메타데이터 조회 | GET | `/api/v1/vcmeta` | `?vcId={vc_identifier}` |

### Blockchain SDK 메서드

```
registDidDoc(InvokedDocument invokedDocument, RoleType roleType)
getDidDoc(String didUrl)
updateDidDocStatus(String didUrl, DidDocStatus status)
registVcMetadata(VcMeta vcMeta)
getVcMetadata(String vcId)
updateVcStatus(String vcId, VcStatus status)   // ACTIVE | INACTIVE | REVOKED
```

---

## 5. 사전 조건: NOA 백엔드 Issuer 엔티티 등록 (TAS P120)

VC를 발급하려면 NOA 백엔드(복지 기관)가 TAS에 **Issuer 엔티티**로 먼저 등록되어야 한다. 이 작업은 서비스 최초 배포 시 1회 수행하며 이후 반복하지 않는다.

```
NOA 백엔드(Issuer)           TAS                    CA Server
    │                          │                         │
    │── propose-enroll-entity ─▶│                         │
    │── request-ecdh ──────────▶│  (ECDH 세션키 교환)     │
    │── request-enroll-entity ─▶│                         │
    │                          │── Certificate VC 발급 ──▶│
    │                          │◀── Certificate VC ───────│
    │── confirm-enroll-entity ─▶│                         │
    │◀── 등록 완료 ─────────────│                         │
```

등록 완료 후 NOA 백엔드는 `RoleType.Issuer`로 TAS에 인식되며, 이후 P210 VC 발급 요청이 허용된다.

---

## 6. 사용자 등록 및 DID 발급 흐름 (TAS P132)

대상자가 처음 가입할 때 DID가 생성되고 OmniOne Chain에 등록된다. OmniOne CX 신뢰 포인트 1 완료 직후 이 흐름이 이어진다.

```
대상자 앱          OmniOne CX        TAS                Ledger Service
    │                  │               │                      │
    │── CX 본인확인 요청 ──▶│               │                      │
    │◀── 인증 결과 ─────────│               │                      │
    │                              │               │
    │── propose-register-user ────▶│               │
    │── request-ecdh ─────────────▶│ (세션키 교환)  │
    │── request-create-token ──────▶│               │
    │── retrieve-kyc ─────────────▶│ (KYC 결과 조회)│
    │── request-register-user ────▶│               │
    │                              │── POST /api/v1/diddoc/register ──▶│
    │                              │◀── txId-1 ────────────────────────│
    │── confirm-register-user ────▶│               │
    │◀── DID Document + txId-1 ────│               │
```

OmniOne CX 본인확인 결과는 NOA 백엔드가 콜백으로 수신한 뒤 TAS에 전달한다. TAS P132의 `retrieve-kyc` 단계는 실제 CX SDK 콜백 파라미터가 해커톤 제공 SDK에 따라 달라지므로, 어댑터 레이어를 두고 SDK 연동 가이드 수령 전까지 Mock으로 대체한다. CX SDK 미수령 시 전체 가입 흐름은 Mock 인증 모드로 fallback한다.

---

## 7. VC/VP 라이프사이클

### VC 발급 조건 및 주체

- **발급 시점**: 담당자 승인 완료 후 (위기감지 시점이 아님)
- **발급 주체**: 담당 복지 기관 (NOA 백엔드가 Issuer Server 호출)
- **발급 VC 종류**: 복지 지원 확인 VC (MVP 1종)
- **VC 스키마**: `GET /api/v1/vc/vcschema` 로 조회, 커스텀 스키마 정의 가능

### VC 내용 구조 (MVP 기준)

| 필드 | 내용 |
|:---|:---|
| `id` | VC 고유 식별자 |
| `issuer` | 집행 기관 DID (NOA 백엔드 Issuer DID) |
| `subject` | 대상자 `did_hash` |
| `support_type` | 복지 지원 유형 (예: `FOOD`, `MEDICAL`) |
| `valid_until` | VC 유효기간 (담당자 승인일 + 30일) |

PII 원문(성명·주소)은 VC에 포함하지 않는다.

### VC 발급 흐름 (Issuer Server P210 프로토콜, 5단계)

```
NOA 백엔드(담당자 승인 후)    Issuer Server         Ledger Service
    │                            │                       │
    │── POST /api/v1/request-offer ──▶│  (발급 세션 시작)  │
    │── POST /api/v1/inspect-propose-issue ──▶│           │
    │── POST /api/v1/generate-issue-profile ──▶│          │
    │── POST /api/v1/issue-vc ──────────▶│  (VC 발급)     │
    │── POST /api/v1/complete-vc ────────▶│               │
    │                            │── POST /api/v1/vcmeta/register ──▶│
    │                            │◀── txId-2 ────────────────────────│
    │◀── txId-2 ─────────────────│                       │
```

### VP 검증 흐름 (Verifier Server P310 프로토콜, 4단계)

집행 직전 대상자가 VP를 제출해 "승인된 사람이고 본인도 맞다"를 한 번에 증명한다. OmniOne CX 신뢰 포인트 2 완료 직후 이 흐름이 이어진다.

```
대상자 앱                   Verifier Server      NOA 백엔드
    │                            │                   │
    │── POST /api/v1/request-offer-qr ──▶│  (QR 세션 오퍼)
    │── POST /api/v1/request-profile ────▶│  (검증 요건 조회)
    │── POST /api/v1/request-verify ─────▶│  (VP 암호화 제출)
    │── POST /api/v1/confirm-verify ──────▶│  (검증 완료)
    │                            │── 검증 완료 통보 ──▶│
    │                                               │── 복지 집행
    │                                               │── 집행 이벤트 해시 → OmniOne Chain (txId-3)
    │◀── txId-3 공개 ────────────────────────────────│
```

### VC 상태 변경 및 보존 정책 (P220 프로토콜)

집행 완료 후 두 가지 동작이 분리된다.

| 대상 | 처리 | 의미 |
|:---|:---|:---|
| VC 원문 (NOA 서버) | 삭제 | 민감 정보 최소 보유 원칙 |
| 온체인 VC 메타데이터 상태 | `REVOKED` 변경 | 해당 VC가 재사용 불가임을 표시 — 집행 사실 자체를 무효화하는 것이 아님 |
| txId-3 (집행 이벤트 해시) | 온체인 영구 보존 | 집행 증명 근거 — 삭제·변경 불가 |

`REVOKED`는 "이 VC로 다시 권한을 행사할 수 없다"는 의미이며, txId-3로 기록된 집행 사실은 별도로 영구 보존된다. 다기관 사후 검증은 txId-3를 기준으로 수행한다.

---

## 8. 온체인·오프체인 하이브리드 데이터 주권 모델

블록체인에는 개인정보 원문을 기록하지 않는다. 대용량·개인정보 데이터는 오프체인에 보관하고 해시 또는 메타데이터만 온체인에 올린다.

| 데이터 | 저장 위치 | 암호화 | 비고 |
|:---|:---|:---|:---|
| 솔이 통화·SMS·웹 채팅 원문 | PostgreSQL (오프체인) | AES-256 | 담당자는 요약본만 조회 |
| 대상자 개인정보 | PostgreSQL (오프체인) | AES-256 | 해시(did_hash)만 온체인 참조 |
| DID Document | OmniOne Chain (온체인) | 멀티베이스 인코딩 | Ledger Service 경유 |
| VC 메타데이터 | OmniOne Chain (온체인) | — | VC 원문 아님, 메타만 |
| 집행 이벤트 해시 | OmniOne Chain (온체인) | SHA-256 | 아래 해시 구조 참조 |

### 집행 이벤트 해시 구조

```
SHA-256(did_hash || support_type || amount || approved_at_timestamp)
```

이 해시값과 담당자 DID, 집행 기관 ID를 함께 온체인에 기록한다. 대상자는 `txId`로 자신의 집행 기록을 투명하게 조회할 수 있다.

### NOA MVP 3개 온체인 기록 이벤트

| 시점 | 기록 내용 | txId | Ledger API |
|:---|:---|:---|:---|
| 사용자 DID 등록 완료 시 | DID Document (멀티베이스 인코딩) | txId-1 | `POST /api/v1/diddoc/register` |
| 담당자 승인 후 VC 발급 시 | VC 메타데이터 (ID·상태·발급자·스키마) | txId-2 | `POST /api/v1/vcmeta/register` |
| 복지 집행 완료 시 | 집행 이벤트 해시 (did_hash + 복지유형 + 금액) | txId-3 | `POST /api/v1/vcmeta/register` (집행 VC 메타로 감싸 기록) |

---

## 9. 역할별 접근 권한 (RBAC)

Open DID SDK는 블록체인 레벨의 RBAC를 내장하지 않는다. Ledger Service는 쓰기 연산에 Bearer 토큰 인증만 요구하며, 역할 분리는 NOA 백엔드(NestJS) 애플리케이션 레벨에서 JWT + Guard로 구현한다.

| 역할 | 주요 권한 | 온체인 쓰기 |
|:---|:---|:---|
| citizen (대상자) | 자신의 솔이 통화·SMS·웹 채팅 요약, 복지 매칭, 집행 txId 조회, VP 제출 | 없음 (앱 통해 간접 제출) |
| officer (담당자) | 위기 점수 목록·케이스 요약 조회, 집행 승인 | 백엔드 경유 집행 이벤트 기록 |
| admin | 집계 통계 조회 (PII 직접 접근 불가) | DID 상태 변경 (deactivate/revoke) |

TAS는 `RoleType` 파라미터로 참여 엔티티의 역할(Issuer, Verifier, Wallet Provider 등)을 구분하며, 이 역할은 TAS P120 엔티티 등록 단계에서 확정된다.

---

## 10. 신뢰 체인 (End-to-End)

```
[1] OmniOne CX 본인확인 (가입) — 신뢰 포인트 1
      ↓
[2] TAS P132: DID Document 생성 + OmniOne Chain 등록 (txId-1)
      ↓
[3] 솔이 AI 정기 전화·SMS·웹 채팅 감지 → 위기도 스코어링
      ↓
[4] 담당자 대시보드: 위기 케이스 검토·승인
      ↓
[5] Issuer Server P210: 지원 확인 VC 발급 (5단계)
    + Ledger Service: VC 메타데이터 온체인 등록 (txId-2)
      ↓
[6] 집행 직전: OmniOne CX 재확인 — 신뢰 포인트 2
      ↓
[7] Verifier Server P310: VP 검증 (4단계)
      ↓
[8] 복지 집행 → 집행 이벤트 해시 온체인 기록 (txId-3)
      ↓
[9] 대상자에게 txId-3 공개 → 언제든 온체인 조회 가능
```

### 단계별 실패 처리

| 단계 | 실패 시 처리 |
|:---|:---|
| [2] DID 등록 실패 | 재시도 3회 후 수동 처리, 가입 미완료 상태 유지 |
| [5] VC 발급 실패 | 담당자에게 오류 알림, 승인 상태 롤백 |
| [7] VP 검증 실패 | 집행 차단, 담당자·대상자 양쪽에 재시도 안내 |
| [8] 온체인 기록 실패 | 집행은 완료, DB에 pending 상태 기록 후 비동기 재시도 |

---

## 11. 보안 원칙 요약

| 항목 | 원칙 |
|:---|:---|
| PII 보호 | 온체인에 원문 기록 절대 불가. did_hash + 해시값만 기록 |
| VC 보존 | VC 원문은 VP 검증 완료 후 서버에서 삭제하고, 온체인 VC 메타데이터는 `REVOKED`로 변경해 재사용을 차단한다. 집행 증명은 txId-3 기준으로 보존한다. |
| 대화 원문 | AES-256 암호화 저장, 담당자는 솔이 요약본만 접근 |
| 쓰기 인가 | Ledger Service 쓰기 연산 전체 Bearer 토큰 필수 |
| 부인 방지 | 모든 VC·VP 연산에 ECDH 세션키 + 전자서명 포함 |

---

## Related Documents

- **Layer 3**: [00_DEVELOPMENT_PRINCIPLES.md](./00_DEVELOPMENT_PRINCIPLES.md) — 코딩 컨벤션·성능 목표·보안 원칙
- **Layer 3**: [01_DB_SCHEMA.md](./01_DB_SCHEMA.md) — `chain_tx_id`, `target_did_hash` 등 온체인 참조 컬럼
- **Layer 3**: [02_API_SPECS.md](./02_API_SPECS.md) — `/auth/omni-cx/verify`, `/chain/record/:tx_id` NOA 백엔드 API
- **Layer 1**: [03_PRODUCT_SPECS.md](../01_Concept_Design/03_PRODUCT_SPECS.md) — MVP 범위 (VC 1회 발급·VP 1회 검증·txId 표시)

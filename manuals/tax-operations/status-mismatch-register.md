# [발행 장애·상태불일치·운영 일정] 상태불일치 처리 등록 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

상태불일치 처리 대상을 조회하고 선택 건에 대해 기존 처리 시스템으로 전송을 요청한다. 이후 문서 상태를 다시 대조한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 발행 장애·상태불일치·운영 일정 |
| 언제 사용하는가 | 상태불일치 처리 등록 대상 조회, 상태불일치 선택 건 전송 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 상태불일치 대상과 선택 건 |
| 업무 흐름 | 상태불일치 처리 등록 대상 조회, 상태불일치 선택 건 전송 |
| 이 페이지의 역할 | 조회 · 상태불일치 처리 등록 대상 조회 |
| 판단 결과·다음 업무 | 현재 화면에서 결과를 확인한다. |
| 다른 화면과의 구분 | 같은 경로에서 열리는 조회·팝업은 이 문서에서 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 확인 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxoperations/StatusMismatchRegisterPage.tsx#L348) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 상태불일치 처리 대상을 조회하고 선택 건에 대해 기존 처리 시스템으로 전송을 요청한다. 이후 문서 상태를 다시 대조한다. |
| 메뉴·화면 경로 | SB 서비스관리 > 세금계산서 운영/관리 > 상태불일치 처리 등록 · `/tax-operations/status-mismatch-register` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | 현재 화면에서 결과를 확인한다. |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/tax-operations/status-mismatch-register` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 상태불일치 처리 등록 대상 조회 | `/tax-operations/status-mismatch-register` `VIEW` | `StatusMismatchRegisterSearchRequest` `fromDate`, `toDate`, `mismatchType`, `salesOrPurchaseType` |
| 상태불일치 선택 건 전송 | `/tax-operations/status-mismatch-register` `PROCESS` | `StatusMismatchProcessRequest` `fromDate`, `toDate`, `mismatchType`, `salesOrPurchaseType`, `items` |

코드에서 확인한 버튼·작업명은 **검색**, **전송**, **확인**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **SB 서비스관리 > 세금계산서 운영/관리 > 상태불일치 처리 등록**를 연다. `/tax-operations/status-mismatch-register`를 연다.
2. **처리일자**, **상태 선택**, **스마트빌 저장(S) 연동업체 미승인(I)**, **스마트빌 승인(C) 연동업체 미승인(I)**, **스마트빌 미승인(I) 연동업체 승인(C)**, **특정건 매입취소(시험중)**, **매출/매입** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색**, **전송**, **확인** 중 해당 버튼을 선택한다.
3. **상태불일치 처리 등록 대상 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 처리일자 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxoperations/StatusMismatchRegisterPage.tsx#L57) |
| 상태 선택 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxoperations/StatusMismatchRegisterPage.tsx#L63) |
| 스마트빌 저장(S) 연동업체 미승인(I) | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `SB_SAVED_ERP_UNAPPROVED` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxoperations/StatusMismatchRegisterPage.tsx#L69) |
| 스마트빌 승인(C) 연동업체 미승인(I) | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `SB_APPROVED_ERP_UNAPPROVED` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxoperations/StatusMismatchRegisterPage.tsx#L70) |
| 스마트빌 미승인(I) 연동업체 승인(C) | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `SB_UNAPPROVED_ERP_APPROVED` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxoperations/StatusMismatchRegisterPage.tsx#L71) |
| 특정건 매입취소(시험중) | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `PURCHASE_CANCEL_TEST` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxoperations/StatusMismatchRegisterPage.tsx#L72) |
| 매출/매입 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxoperations/StatusMismatchRegisterPage.tsx#L78) |
| 연동매출(AR) | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `AR` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxoperations/StatusMismatchRegisterPage.tsx#L84) |
| 연동매입(AP) | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `AP` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxoperations/StatusMismatchRegisterPage.tsx#L85) |
| 공급자 | 출력 | 조회 응답 기준 | 화면 필드 `supplierBusinessNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxoperations/StatusMismatchRegisterPage.tsx#L242) |
| 공급받는자 | 출력 | 조회 응답 기준 | 화면 필드 `recipientBusinessNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxoperations/StatusMismatchRegisterPage.tsx#L253) |
| 참조번호 | 출력 | 조회 응답 기준 | 화면 필드 `referenceNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxoperations/StatusMismatchRegisterPage.tsx#L262) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 상태불일치 처리 등록 대상 조회 | `GET /api/v1/tax-operations/status-mismatch-register/records` · `/tax-operations/status-mismatch-register` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/taxoperations/statusmismatchregister/StatusMismatchRegisterController.kt#L49) | `StatusMismatchRegisterSearchRequest` `fromDate`, `toDate`, `mismatchType`, `salesOrPurchaseType` → `success`, `data`, `error`, `content`, `totalElements` | `office.dbo.SCH_SEMIAUTO_MISMATCH` · 코드 연계 트랜잭션 |
| 상태불일치 선택 건 전송 | `POST /api/v1/tax-operations/status-mismatch-register/process` · `/tax-operations/status-mismatch-register` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/taxoperations/statusmismatchregister/StatusMismatchRegisterController.kt#L65) | `StatusMismatchProcessRequest` `fromDate`, `toDate`, `mismatchType`, `salesOrPurchaseType`, `items` → `success`, `data`, `error`, `isAllSuccess`, `successCount`, `failCount`, `failedReferences`, `failedItems` | 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `office.dbo.SCH_SEMIAUTO_MISMATCH` | @FROM_YYMM varchar(10), @TO_YYMM varchar(10), @STATUS_FLAG varchar(2), @DIRECT_FLAG varchar(2) | 정의 참조 `SmartBill3.dbo.COMPANY`, `SB_DTI.dbo.COMPANY_LINK_OUT`, `SB_DTI.dbo.DTI_HEADER_CUB`, `SB_DTI_LOG.dbo.ERP_STATUS_DATA` · 쓰기 구문 존재 · 대상 별칭 또는 하위 정의 확인 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxoperations/statusmismatchregister/repository/StatusMismatchRegisterMapper.kt#L31) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-ea860fc141487aa3) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 상태불일치 대상과 선택 건 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 서비스관리 > 세금계산서 운영/관리 > 상태불일치 처리 등록의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 전송할 항목을 선택해주세요. | 상태불일치 대상과 선택 건 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 검색 결과가 없습니다. | 상태불일치 대상과 선택 건 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/TaxOperationsRoutes.tsx#L23) · [StatusMismatchRegisterPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxoperations/StatusMismatchRegisterPage.tsx#L40) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxoperations/api/opsStatusMismatchApi.ts#L114) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxoperations/api/opsStatusMismatchApi.ts#L144) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 1개 중 개발 메타데이터 확인 1개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-0b368ee4969c58cc) | Demo 메타데이터 1/1개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

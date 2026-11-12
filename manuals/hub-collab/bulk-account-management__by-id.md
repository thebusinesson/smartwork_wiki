# [시스템 키·벌크계좌·업체 연결 설정] 벌크계좌 관리 상세 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

단건. 존재하지 않으면 data=null.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 시스템 키·벌크계좌·업체 연결 설정 |
| 언제 사용하는가 | 벌크계좌 상세 조회, 벌크계좌 발급 취소 (다건) 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 계좌생성일, 계좌발급일, 발급업체, 사업자번호, 은행, 계좌번호 |
| 업무 흐름 | 벌크계좌 상세 조회, 벌크계좌 발급 취소 (다건) |
| 이 페이지의 역할 | 상세 · 벌크계좌 상세 조회 |
| 판단 결과·다음 업무 | [벌크계좌 관리](bulk-account-management.md) |
| 다른 화면과의 구분 | 연동 협업 관리 > 연동 협업 관리 > 벌크계좌 관리에서 사용하는 상세 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 발급 취소 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/bulkAccount/components/BulkAccountCancellationDialog.tsx#L51) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 단건. 존재하지 않으면 data=null. |
| 메뉴·화면 경로 | 연동 협업 관리 > 연동 협업 관리 > 벌크계좌 관리 · `/hub-collab/bulk-account-management/:id` · 경로 변수 `id` |
| 화면 유형·담당 | 상세 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [벌크계좌 관리](bulk-account-management.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/hub-collab/bulk-account-management` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `id` |
| 벌크계좌 상세 조회 | `/hub-collab/bulk-account-management` `VIEW` | `id: Int` |
| 벌크계좌 발급 취소 (다건) | `/hub-collab/bulk-account-management` `PROCESS` | `CancelBulkAccountsRequest` `accountIds`, `cancelReason` · 서버 필수 `accountIds`, `cancelReason` |

코드에서 확인한 버튼·작업명은 **목록**, **계좌 발급 취소**, **발급 취소**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [벌크계좌 관리](bulk-account-management.md)에서 대상 또는 작업을 선택한다. `/hub-collab/bulk-account-management/:id`에서 이전 화면이 전달한 `id`와 현재 대상을 확인한다.
2. **계좌생성일**, **계좌발급일**, **발급업체**, **사업자번호**, **은행**, **계좌번호**, **상태**에서 현재 대상과 입력 또는 표시 내용을 확인한다.
3. **벌크계좌 상세 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [벌크계좌 관리](bulk-account-management.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `id` |
| 계좌생성일 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/bulkAccount/pages/BulkAccountDetailPage.tsx#L113) |
| 계좌발급일 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/bulkAccount/pages/BulkAccountDetailPage.tsx#L114) |
| 발급업체 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/bulkAccount/pages/BulkAccountDetailPage.tsx#L115) |
| 사업자번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `-` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/bulkAccount/pages/BulkAccountDetailPage.tsx#L117) |
| 은행 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/bulkAccount/pages/BulkAccountDetailPage.tsx#L120) |
| 계좌번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/bulkAccount/pages/BulkAccountDetailPage.tsx#L121) |
| 상태 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/bulkAccount/pages/BulkAccountDetailPage.tsx#L123) |
| 담당자 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/bulkAccount/pages/BulkAccountDetailPage.tsx#L130) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 벌크계좌 상세 조회 | `GET /api/v1/hub-collab/bulk-accounts/{id}` · `/hub-collab/bulk-account-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/bulkaccount/BulkAccountController.kt#L95) | `id: Int` → `success`, `data`, `error`, `id`, `createDate`, `issueDate`, `companyId`, `companyName`, `businessNumber`, `bankCode`, `bankName`, `accountNumber` | `SmartBill3.dbo.ACCOUNT_BULK`, `SmartBill3.dbo.COMMON_CODE`, `SmartBill3.dbo.COMPANY`, `office.dbo.SAWON` |
| 벌크계좌 발급 취소 (다건) | `POST /api/v1/hub-collab/bulk-accounts/cancel` · `/hub-collab/bulk-account-management` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/bulkaccount/BulkAccountController.kt#L160) | `CancelBulkAccountsRequest` `accountIds`, `cancelReason` · 서버 필수 `accountIds`, `cancelReason` → `success`, `data`, `error`, `message`, `id` | `SmartBill3.dbo.ACCOUNT_BULK`, `SmartBill3.dbo.ACCOUNT_BULK_HIS`, `smartwork.dbo.action_reason` · 정의에서 확인한 쓰기 `SmartBill3.dbo.ACCOUNT_BULK`, `SmartBill3.dbo.ACCOUNT_BULK_HIS`, `smartwork.dbo.action_reason` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `SmartBill3.dbo.ACCOUNT_BULK` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/bulkaccount/repository/BulkAccountMapper.kt#L86) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-a7ab9e70671b748f) |
| `SmartBill3.dbo.COMMON_CODE` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/bulkaccount/repository/BulkAccountMapper.kt#L86) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-49b15682b4d4770c) |
| `SmartBill3.dbo.COMPANY` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/bulkaccount/repository/BulkAccountMapper.kt#L86) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-0e6fcaa6b5086c07) |
| `office.dbo.SAWON` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/bulkaccount/repository/BulkAccountMapper.kt#L86) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3a9ea6e368df5cb3) |
| `SmartBill3.dbo.ACCOUNT_BULK_HIS` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL INSERT INTO | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/bulkaccount/repository/BulkAccountMapper.kt#L261) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-8486d37c36a1466d) |
| `smartwork.dbo.action_reason` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL INSERT INTO | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/shared/actionreason/repository/ActionReasonMapper.kt#L16) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b0430106ffe0743f) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 계좌생성일, 계좌발급일, 발급업체, 사업자번호, 은행, 계좌번호 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 연동 협업 관리 > 연동 협업 관리 > 벌크계좌 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/IntegrationRoutes.tsx#L93) · [BulkAccountDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/bulkAccount/pages/BulkAccountDetailPage.tsx#L28) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/bulkAccountManagementApi.ts#L59) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/bulkAccountManagementApi.ts#L69) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 6개 중 개발 메타데이터 확인 6개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-7e804669b24b339c) | Demo 메타데이터 6/6개 확인 · Dev와 계약 차이 1개 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

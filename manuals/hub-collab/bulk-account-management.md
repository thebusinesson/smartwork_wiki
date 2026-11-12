# [시스템 키·벌크계좌·업체 연결 설정] 벌크계좌 관리 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

발급일·업체조건·은행·계좌번호 검색 + 페이징. STATUS='B' 발급 상태만 반환.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 시스템 키·벌크계좌·업체 연결 설정 |
| 언제 사용하는가 | 은행 드롭다운 옵션, 벌크계좌 목록 조회, 은행별 계좌 발급 현황, 벌크계좌 목록 다운로드, 벌크계좌 발급 취소 (다건) 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 발급일, 업체 조건, 전체, 사업자번호, 회사명, 발급은행 |
| 업무 흐름 | 은행 드롭다운 옵션, 벌크계좌 목록 조회, 은행별 계좌 발급 현황, 벌크계좌 목록 다운로드, 벌크계좌 발급 취소 (다건) |
| 이 페이지의 역할 | 조회 · 벌크계좌 목록 조회 |
| 판단 결과·다음 업무 | [벌크계좌 관리 등록](bulk-account-management__new.md) · [벌크계좌 관리 상세](bulk-account-management__by-id.md) |
| 다른 화면과의 구분 | 이 경로에서 볼 수 있는 조건·결과를 기준으로 사용한다. 독립 경로의 상세·등록은 관련 화면에 연결한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 발급 취소 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/bulkAccount/components/BulkAccountCancellationDialog.tsx#L51) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 발급일·업체조건·은행·계좌번호 검색 + 페이징. STATUS='B' 발급 상태만 반환. |
| 메뉴·화면 경로 | 연동 협업 관리 > 연동 협업 관리 > 벌크계좌 관리 · `/hub-collab/bulk-account-management` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [벌크계좌 관리 등록](bulk-account-management__new.md) · [벌크계좌 관리 상세](bulk-account-management__by-id.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/hub-collab/bulk-account-management` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 은행 드롭다운 옵션 | `/hub-collab/bulk-account-management` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 벌크계좌 목록 조회 | `/hub-collab/bulk-account-management` `VIEW` | `BulkAccountSearchRequest` `page`, `size`, `issueDateFrom`, `issueDateTo`, `vendorFilterType`, `vendorFilterValue`, `bankCode`, `accountNumber` |
| 은행별 계좌 발급 현황 | `/hub-collab/bulk-account-management` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 벌크계좌 목록 다운로드 | `/hub-collab/bulk-account-management` `EXCEL_DOWNLOAD` | `BulkAccountSearchRequest` `page`, `size`, `issueDateFrom`, `issueDateTo`, `vendorFilterType`, `vendorFilterValue`, `bankCode`, `accountNumber` · `format: DownloadFormat` |
| 벌크계좌 발급 취소 (다건) | `/hub-collab/bulk-account-management` `PROCESS` | `CancelBulkAccountsRequest` `accountIds`, `cancelReason` · 서버 필수 `accountIds`, `cancelReason` |
| 벌크계좌 목록 원문 조회 | `/hub-collab/bulk-account-management` / `UNMASK` | `id`, `field` |

코드에서 확인한 버튼·작업명은 **검색**, **벌크계좌 발급**, **계좌발급 현황**, **다운로드**, **벌크계좌 다운로드**, **계좌 발급 취소**, **발급 취소**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **연동 협업 관리 > 연동 협업 관리 > 벌크계좌 관리**를 연다. `/hub-collab/bulk-account-management`를 연다.
2. **발급일**, **업체 조건**, **전체**, **사업자번호**, **회사명**, **발급은행**, **계좌번호** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색**, **다운로드**, **벌크계좌 다운로드** 중 해당 버튼을 선택한다.
3. **벌크계좌 목록 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [벌크계좌 관리 등록](bulk-account-management__new.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 발급일 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/bulkAccount/pages/BulkAccountManagementPage.tsx#L77) |
| 업체 조건 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/bulkAccount/pages/BulkAccountManagementPage.tsx#L87) |
| 전체 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/constants/bulkAccountManagement.ts#L18) |
| 사업자번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `BUSINESS_NUMBER` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/constants/bulkAccountManagement.ts#L19) |
| 회사명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `COMPANY_NAME` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/constants/bulkAccountManagement.ts#L20) |
| 발급은행 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/bulkAccount/pages/BulkAccountManagementPage.tsx#L104) |
| 계좌번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/bulkAccount/pages/BulkAccountManagementPage.tsx#L117) |
| 발급업체 | 출력 | 조회 응답 기준 | 화면 필드 `companyName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/bulkAccount/components/BulkAccountTable.tsx#L73) |
| 은행 | 출력 | 조회 응답 기준 | API 응답 `bankName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/bulkAccount/components/BulkAccountTable.tsx#L85) |
| 담당자 | 출력 | 조회 응답 기준 | 화면 필드 `managerName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/bulkAccount/components/BulkAccountTable.tsx#L104) |
| 은행명 | 출력 | 조회 응답 기준 | API 응답 `bankName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/bulkAccount/components/BulkAccountStatusDialog.tsx#L24) |
| 총발급계좌 | 출력 | 조회 응답 기준 | API 응답 `total` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/bulkAccount/components/BulkAccountStatusDialog.tsx#L25) |
| 사용가능계좌 | 출력 | 조회 응답 기준 | API 응답 `available` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/bulkAccount/components/BulkAccountStatusDialog.tsx#L26) |
| 사용중계좌 | 출력 | 조회 응답 기준 | API 응답 `inUse` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/bulkAccount/components/BulkAccountStatusDialog.tsx#L27) |
| 사용불가계좌 | 출력 | 조회 응답 기준 | API 응답 `cancelled` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/bulkAccount/components/BulkAccountStatusDialog.tsx#L28) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 은행 드롭다운 옵션 | `GET /api/v1/hub-collab/bulk-accounts/banks` · `/hub-collab/bulk-account-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/bulkaccount/BulkAccountController.kt#L190) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `code`, `name` | `SmartBill3.dbo.COMMON_CODE` |
| 벌크계좌 목록 조회 | `GET /api/v1/hub-collab/bulk-accounts` · `/hub-collab/bulk-account-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/bulkaccount/BulkAccountController.kt#L82) | `BulkAccountSearchRequest` `page`, `size`, `issueDateFrom`, `issueDateTo`, `vendorFilterType`, `vendorFilterValue`, `bankCode`, `accountNumber` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `currentPage`, `size` | `smartwork.dbo.usp_bulk_account_list_select` · 코드 연계 트랜잭션 |
| 은행별 계좌 발급 현황 | `GET /api/v1/hub-collab/bulk-accounts/status` · `/hub-collab/bulk-account-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/bulkaccount/BulkAccountController.kt#L201) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `bankCode`, `bankName`, `total`, `available`, `inUse`, `cancelled` | `SmartBill3.dbo.ACCOUNT_BULK`, `SmartBill3.dbo.COMMON_CODE` |
| 벌크계좌 목록 다운로드 | `GET /api/v1/hub-collab/bulk-accounts/download` · `/hub-collab/bulk-account-management` `EXCEL_DOWNLOAD` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/bulkaccount/BulkAccountController.kt#L226) | `BulkAccountSearchRequest` `page`, `size`, `issueDateFrom`, `issueDateTo`, `vendorFilterType`, `vendorFilterValue`, `bankCode`, `accountNumber` · `format: DownloadFormat` → 파일 또는 오류 응답 | `SmartBill3.dbo.ACCOUNT_BULK`, `office.dbo.SAWON`, `SmartBill3.dbo.COMPANY`, `SmartBill3.dbo.COMMON_CODE` |
| 벌크계좌 발급 취소 (다건) | `POST /api/v1/hub-collab/bulk-accounts/cancel` · `/hub-collab/bulk-account-management` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/bulkaccount/BulkAccountController.kt#L160) | `CancelBulkAccountsRequest` `accountIds`, `cancelReason` · 서버 필수 `accountIds`, `cancelReason` → `success`, `data`, `error`, `message`, `id` | `SmartBill3.dbo.ACCOUNT_BULK`, `SmartBill3.dbo.ACCOUNT_BULK_HIS`, `smartwork.dbo.action_reason` · 정의에서 확인한 쓰기 `SmartBill3.dbo.ACCOUNT_BULK`, `SmartBill3.dbo.ACCOUNT_BULK_HIS`, `smartwork.dbo.action_reason` · 코드 연계 트랜잭션 |
| 벌크계좌 목록 원문 조회 | `POST /api/v1/hub-collab/bulk-accounts/{id}/sensitive-values/reveal` · `/hub-collab/bulk-account-management` / `UNMASK` · [화면 컴포넌트](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/bulkAccount/components/BulkAccountTable.tsx#L108) · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/bulkaccount/BulkAccountController.kt#L105) | `id`, `field` → 요청한 항목의 원문 응답 | 권한 검사 후 대상 값을 조회하고 감사 기록을 남긴다. |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `SmartBill3.dbo.COMMON_CODE` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/bulkaccount/repository/BulkAccountMapper.kt#L98) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-49b15682b4d4770c) |
| `smartwork.dbo.usp_bulk_account_list_select` | @PAGE int, @PAGE_SIZE int, @ISSUE_DATE_FROM varchar(10) = NULL, @ISSUE_DATE_TO varchar(10) = NULL, @VENDOR_FILTER_TYPE char(1), @VENDOR_FILTER_VALUE varchar(60) = NULL, @BANK_CODE char(2) = NULL, @ACCOUNT_NUMBER varchar(30) = NULL | 정의 참조 `SmartBill3.dbo.ACCOUNT_BULK`, `SmartBill3.dbo.COMMON_CODE`, `SmartBill3.dbo.COMPANY`, `office.dbo.SAWON` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/bulkaccount/repository/BulkAccountMapper.kt#L58) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-70ffe7c54454f699) |
| `SmartBill3.dbo.ACCOUNT_BULK` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/bulkaccount/repository/BulkAccountMapper.kt#L213) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-a7ab9e70671b748f) |
| `office.dbo.SAWON` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/bulkaccount/repository/BulkAccountMapper.kt#L324) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3a9ea6e368df5cb3) |
| `SmartBill3.dbo.COMPANY` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/bulkaccount/repository/BulkAccountMapper.kt#L324) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-0e6fcaa6b5086c07) |
| `SmartBill3.dbo.ACCOUNT_BULK_HIS` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL INSERT INTO | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/bulkaccount/repository/BulkAccountMapper.kt#L261) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-8486d37c36a1466d) |
| `smartwork.dbo.action_reason` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL INSERT INTO | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/shared/actionreason/repository/ActionReasonMapper.kt#L16) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b0430106ffe0743f) |
| `smartwork.dbo.usp_sw_log_access_event_insert` | @EVENT_TYPE varchar(30) IN, @STATUS varchar(20) IN, @USER_ID bigint IN, @MEMBER_ID nvarchar(50) IN, @USER_NAME nvarchar(100) IN, @DEPARTMENT_NAME nvarchar(100) IN, @PAGE_TITLE nvarchar(200) IN, @PATH nvarchar(500) IN, @MENU_PATH nvarchar(500) IN, @MENU_LABEL nvarchar(200) IN, @CATEGORY_NAME nvarchar(200) IN, @SUB_CATEGORY_NAME nvarchar(200) IN, @MENU_ORDER int IN, @IP_ADDRESS varchar(45) IN, @USER_AGENT nvarchar(1000) IN, @BROWSER varchar(100) IN, @OS varchar(100) IN, @REFERRER nvarchar(500) IN, @DETAIL nvarchar(1000) IN, @RESULT int OUT, @COUNTS_AS_VISIT bit IN | 원문 조회 또는 감사 흐름에서 호출 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/logmanagement/repository/LogManagementMapper.kt#L92) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 발급일, 업체 조건, 전체, 사업자번호, 회사명, 발급은행 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 연동 협업 관리 > 연동 협업 관리 > 벌크계좌 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 전체 선택에 실패했습니다. | 발급일, 업체 조건, 전체, 사업자번호, 회사명, 발급은행 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 데이터가 없습니다. | 발급일, 업체 조건, 전체, 사업자번호, 회사명, 발급은행 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/IntegrationRoutes.tsx#L91) · [BulkAccountManagementPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/bulkAccount/pages/BulkAccountManagementPage.tsx#L63) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/bulkAccountManagementApi.ts#L79) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/bulkAccountManagementApi.ts#L41) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/bulkAccountManagementApi.ts#L84) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/bulkAccountManagementApi.ts#L109) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/bulkAccountManagementApi.ts#L69) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 7개 중 개발 메타데이터 확인 7개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-d9e5dee5c0691ff2) | Demo 메타데이터 8/8개 확인 · Dev와 계약 차이 1개 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

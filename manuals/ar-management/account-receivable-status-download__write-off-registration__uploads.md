# [매출채권과 회수·대손 기록] 매출 채권 현황 다운로드 업로드 이력 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

제각내역 엑셀을 업로드하고 staging 테이블에 적재한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 매출채권과 회수·대손 기록 |
| 언제 사용하는가 | 업로드 목록 조회, 샘플 엑셀 다운로드, 엑셀 업로드, 업로드 삭제 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 업로드 일자, 파일명, 총 제각 건수, 업로드 상태 |
| 업무 흐름 | 업로드 목록 조회, 샘플 엑셀 다운로드, 엑셀 업로드, 업로드 삭제 |
| 이 페이지의 역할 | 업로드 이력 · 엑셀 업로드 |
| 판단 결과·다음 업무 | [매출 채권 현황 다운로드](account-receivable-status-download.md) |
| 다른 화면과의 구분 | 서비스 현황 > 채권 관리 > 매출 채권 현황 다운로드에서 사용하는 업로드 이력 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 제각내역 개별등록 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/arManagement/components/WriteOffRegistrationTabs.tsx#L42) |
| 제각내역 파일 업로드 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/arManagement/components/WriteOffRegistrationTabs.tsx#L48) |
| 삭제 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/arManagement/AccountReceivableWriteOffRegistrationUploadsPage.tsx#L360) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 제각내역 엑셀을 업로드하고 staging 테이블에 적재한다. |
| 메뉴·화면 경로 | 서비스 현황 > 채권 관리 > 매출 채권 현황 다운로드 · `/ar-management/account-receivable-status-download/write-off-registration/uploads` |
| 화면 유형·담당 | 업로드 이력 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [매출 채권 현황 다운로드](account-receivable-status-download.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/ar-management/account-receivable-status-download` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 업로드 목록 조회 | `/ar-management/account-receivable-status-download` `VIEW` | `WriteOffUploadListRequest` `billingStartMonth`, `billingEndMonth`, `depositPeriodType`, `depositStart`, `depositEnd`, `includeTarget`, `includeNonTarget`, `page`, `size` |
| 샘플 엑셀 다운로드 | `/ar-management/account-receivable-status-download` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 엑셀 업로드 | `/ar-management/account-receivable-status-download` `EXCEL_UPLOAD` | `WriteOffUploadRequest` `billingStartMonth`, `billingEndMonth`, `depositPeriodType`, `depositStart`, `depositEnd`, `includeTarget`, `includeNonTarget` · `file: MultipartFile` |
| 업로드 삭제 | `/ar-management/account-receivable-status-download` `DELETE` | `WriteOffUploadDeleteRequest` `uploadIds` |

코드에서 확인한 버튼·작업명은 **파일 선택**, **샘플 다운로드**, **업로드**, **삭제**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [매출 채권 현황 다운로드](account-receivable-status-download.md)에서 대상 또는 작업을 선택한다. `/ar-management/account-receivable-status-download/write-off-registration/uploads`를 연다.
2. **파일명** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **샘플 다운로드** 중 해당 버튼을 선택한다.
3. **엑셀 업로드**을 실행하기 전에 변경 대상과 입력값을 확인한다. 처리 응답을 확인하고 관련 조회에서 대상의 상태를 확인한다.
4. 후속 조회나 목록 복귀가 필요하면 [매출 채권 현황 다운로드](account-receivable-status-download.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 업로드 일자 | 출력 | 조회 응답 기준 | 화면 필드 `uploadedAt` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/arManagement/AccountReceivableWriteOffRegistrationUploadsPage.tsx#L33) |
| 파일명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `fileName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/arManagement/AccountReceivableWriteOffRegistrationUploadsPage.tsx#L39) |
| 총 제각 건수 | 출력 | 조회 응답 기준 | API 응답 `totalCount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/arManagement/AccountReceivableWriteOffRegistrationUploadsPage.tsx#L48) |
| 업로드 상태 | 출력 | 조회 응답 기준 | API 응답 `uploadStatus` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/arManagement/AccountReceivableWriteOffRegistrationUploadsPage.tsx#L55) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 업로드 목록 조회 | `GET /api/v1/ar-management/account-receivable-status/write-off-registrations/uploads` · `/ar-management/account-receivable-status-download` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/armanagement/writeoffregistration/AccountReceivableWriteOffRegistrationController.kt#L90) | `WriteOffUploadListRequest` `billingStartMonth`, `billingEndMonth`, `depositPeriodType`, `depositStart`, `depositEnd`, `includeTarget`, `includeNonTarget`, `page`, `size` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `currentPage`, `pageSize` | `smartwork.dbo.usp_account_receivable_write_off_upload_list_select` |
| 샘플 엑셀 다운로드 | `GET /api/v1/ar-management/account-receivable-status/write-off-registrations/sample` · `/ar-management/account-receivable-status-download` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/armanagement/writeoffregistration/AccountReceivableWriteOffRegistrationController.kt#L103) | 추가 입력은 Controller 서명 참조 → 파일 또는 오류 응답 | 직접 DB 호출이 연결된 경로는 현재 소스에서 미확인. 세부 저장소는 Controller와 Service 참조. |
| 엑셀 업로드 | `POST /api/v1/ar-management/account-receivable-status/write-off-registrations/uploads` · `/ar-management/account-receivable-status-download` `EXCEL_UPLOAD` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/armanagement/writeoffregistration/AccountReceivableWriteOffRegistrationController.kt#L113) | `WriteOffUploadRequest` `billingStartMonth`, `billingEndMonth`, `depositPeriodType`, `depositStart`, `depositEnd`, `includeTarget`, `includeNonTarget` · `file: MultipartFile` → `success`, `data`, `error`, `uploadId`, `totalCount`, `validCount`, `invalidCount`, `savedCount`, `reflectFailedCount`, `uploadStatus`, `message` | `smartwork.dbo.account_receivable_write_off_upload_item`, `smartwork.dbo.account_receivable_write_off_upload`, `smartwork.dbo.usp_account_receivable_write_off_lookup_select`, `smartwork.dbo.usp_account_receivable_write_off_invoice_insert` · 정의에서 확인한 쓰기 `smartwork.dbo.account_receivable_write_off_upload_item`, `smartwork.dbo.account_receivable_write_off_upload`, `SB_BILL.dbo.INVOICE` · 코드 연계 트랜잭션 |
| 업로드 삭제 | `DELETE /api/v1/ar-management/account-receivable-status/write-off-registrations/uploads` · `/ar-management/account-receivable-status-download` `DELETE` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/armanagement/writeoffregistration/AccountReceivableWriteOffRegistrationController.kt#L132) | `WriteOffUploadDeleteRequest` `uploadIds` → `success`, `data`, `error` | `smartwork.dbo.account_receivable_write_off_upload_item`, `smartwork.dbo.account_receivable_write_off_upload` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.usp_account_receivable_write_off_upload_list_select` | @BILLING_START_MONTH char(7), @BILLING_END_MONTH char(7), @DEPOSIT_PERIOD_TYPE varchar(5), @DEPOSIT_START varchar(10), @DEPOSIT_END varchar(10), @INCLUDE_TARGET bit, @INCLUDE_NON_TARGET bit, @PAGE int, @PAGE_SIZE int | 정의 참조 `smartwork.dbo.account_receivable_write_off_upload`, `smartwork.dbo.account_receivable_write_off_upload_item` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/armanagement/writeoffregistration/repository/AccountReceivableWriteOffRegistrationMapper.kt#L71) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-82822004db297b50) |
| `smartwork.dbo.account_receivable_write_off_upload_item` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL UPDATE | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/armanagement/writeoffregistration/repository/AccountReceivableWriteOffRegistrationMapper.kt#L410) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-25f1d259fd76460a) |
| `smartwork.dbo.account_receivable_write_off_upload` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL INSERT INTO | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/armanagement/writeoffregistration/repository/AccountReceivableWriteOffRegistrationMapper.kt#L173) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-17788e2f7de63afb) |
| `smartwork.dbo.usp_account_receivable_write_off_lookup_select` | @BILLING_START_MONTH varchar(6), @BILLING_END_MONTH varchar(6), @DEPOSIT_PERIOD_TYPE varchar(5), @DEPOSIT_START varchar(10), @DEPOSIT_END varchar(10), @INCLUDE_TARGET bit, @INCLUDE_NON_TARGET bit, @BUSINESS_NUMBER varchar(10) | 정의 참조 `SmartBill3.dbo.COMPANY`, `SB_BILL.dbo.INVOICE`, `SB_BILL.dbo.PAYMENT` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/armanagement/writeoffregistration/repository/AccountReceivableWriteOffRegistrationMapper.kt#L44) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3a626dfb45302c84) |
| `smartwork.dbo.usp_account_receivable_write_off_invoice_insert` | @BUSINESS_CODE bigint, @BUSINESS_NUMBER varchar(10), @COMPANY_NAME nvarchar(200), @CHARGE_MONTH varchar(6), @WRITE_OFF_DATE varchar(10), @AMOUNT bigint, @DIVISION varchar(20), @SW_NO bigint, @MEMO nvarchar(100), @RESULT int OUT | 정의 참조 `SB_BILL.dbo.INVOICE` · 정적 쓰기 `SB_BILL.dbo.INVOICE` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/armanagement/writeoffregistration/repository/AccountReceivableWriteOffRegistrationMapper.kt#L430) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-92227dfcc2ffe12e) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 업로드 일자, 파일명, 총 제각 건수, 업로드 상태 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 서비스 현황 > 채권 관리 > 매출 채권 현황 다운로드의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 조회 조건이 없어 다운로드 화면으로 이동합니다. | 업로드 일자, 파일명, 총 제각 건수, 업로드 상태 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 전체 선택에 실패했습니다. | 업로드 일자, 파일명, 총 제각 건수, 업로드 상태 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 파일 업로드는 완료되었으나 INVOICE 반영에 실패했습니다. 상세에서 확인 후 삭제할 수 있습니다. | 업로드 일자, 파일명, 총 제각 건수, 업로드 상태 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 파일 업로드 중 오류가 발생했습니다. | 업로드 일자, 파일명, 총 제각 건수, 업로드 상태 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/ArManagementRoutes.tsx#L13) · [AccountReceivableWriteOffRegistrationUploadsPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/arManagement/AccountReceivableWriteOffRegistrationUploadsPage.tsx#L68) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/arManagement/api/accountReceivableWriteOffRegistrationApi.ts#L49) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/arManagement/api/accountReceivableWriteOffRegistrationApi.ts#L70) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/arManagement/api/accountReceivableWriteOffRegistrationApi.ts#L66) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/arManagement/api/accountReceivableWriteOffRegistrationApi.ts#L74) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 5개 중 개발 메타데이터 확인 5개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-2cbdb41343d29276) | Demo 메타데이터 5/5개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

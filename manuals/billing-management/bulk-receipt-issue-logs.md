# [이용료 청구·일일 정산·영수 발행] 영수 대량 발행 오류 로그 조회 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

오류 발생일자 기준 이력과 문서별 최근 처리 결과를 함께 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 이용료 청구·일일 정산·영수 발행 |
| 언제 사용하는가 | 영수 대량 발행 오류 로그 목록 조회 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 오류 발생일자, 업체 조건, 사업자번호, 회사명, 참조번호, 당시 오류 |
| 업무 흐름 | 영수 대량 발행 오류 로그 목록 조회 |
| 이 페이지의 역할 | 이력 조회 · 영수 대량 발행 오류 로그 목록 조회 |
| 판단 결과·다음 업무 | 현재 화면에서 결과를 확인한다. |
| 다른 화면과의 구분 | 같은 경로에서 열리는 조회·팝업은 이 문서에서 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 오류 발생일자 기준 이력과 문서별 최근 처리 결과를 함께 조회한다. |
| 메뉴·화면 경로 | 서비스 현황 > 요금관리 > 영수 대량 발행 오류 로그 조회 · `/billing-management/bulk-receipt-issue-logs` |
| 화면 유형·담당 | 이력 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | 현재 화면에서 결과를 확인한다. |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/billing-management/bulk-receipt-issue-logs` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 영수 대량 발행 오류 로그 목록 조회 | `/billing-management/bulk-receipt-issue-logs` `VIEW` | `BulkReceiptIssueLogsSearchRequest` `startDate`, `endDate`, `searchType`, `searchValue`, `page`, `size` |

코드에서 확인한 버튼·작업명은 **검색**, **다시 시도**, **새로고침**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **서비스 현황 > 요금관리 > 영수 대량 발행 오류 로그 조회**를 연다. `/billing-management/bulk-receipt-issue-logs`를 연다.
2. **오류 발생일자**, **업체 조건**, **오류 발생일시**, **최근 처리일시** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색** 중 해당 버튼을 선택한다.
3. **영수 대량 발행 오류 로그 목록 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 오류 발생일자 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/BulkReceiptIssueLogsPage.tsx#L25) |
| 업체 조건 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/BulkReceiptIssueLogsPage.tsx#L34) |
| 사업자번호 | 출력 | 조회 응답 기준 | 화면 필드 `businessNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/components/BulkReceiptIssueLogsTable.tsx#L61) |
| 회사명 | 출력 | 조회 응답 기준 | 화면 필드 `companyName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/components/BulkReceiptIssueLogsTable.tsx#L62) |
| 참조번호 | 출력 | 조회 응답 기준 | 화면 필드 `conversationId` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/components/BulkReceiptIssueLogsTable.tsx#L63) |
| 당시 오류 | 출력 | 조회 응답 기준 | 화면 필드 `description` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/components/BulkReceiptIssueLogsTable.tsx#L72) |
| 오류 발생일시 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `writeDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/components/BulkReceiptIssueLogsTable.tsx#L81) |
| 현재 처리 결과 | 출력 | 조회 응답 기준 | 화면 필드 `currentResult` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/components/BulkReceiptIssueLogsTable.tsx#L82) |
| 최근 처리일시 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `currentResult.updatedAt` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/components/BulkReceiptIssueLogsTable.tsx#L83) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 영수 대량 발행 오류 로그 목록 조회 | `GET /api/v1/service-status/billing/bulk-receipt-issue-logs` · `/billing-management/bulk-receipt-issue-logs` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/billing/bulkreceiptissuelogs/BulkReceiptIssueLogsController.kt#L46) | `BulkReceiptIssueLogsSearchRequest` `startDate`, `endDate`, `searchType`, `searchValue`, `page`, `size` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `currentPage`, `size` | `smartwork.dbo.upSBAdm_UseBillList_Bulk_error`, `smartwork.dbo.BULK_RECEIPT_ISSUE_JOB`, `smartwork.dbo.BULK_RECEIPT_ISSUE_JOB_RESULT`, `smartwork.dbo.sw_log_system_event`, `SB_DTI.dbo.DTI_HEADER_CUB` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.upSBAdm_UseBillList_Bulk_error` | @StartDate varchar(10), @EndDate varchar(10), @SearchType varchar(20), @SearchValue varchar(40), @Page int = 1, @PageSize int = 10 | 정의 참조 `master.dbo.dec_char_sel_tc`, `SB_DTI.dbo.DTI_HEADER_CUB`, `SmartBill3.dbo.MSG_N_ERROR_CODE`, `SB_COMMON.dbo.SB_USEBILL_BATCH_LOG` · 하위 호출 `master.dbo.dec_char_sel_tc` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/billing/bulkreceiptissuelogs/repository/BulkReceiptIssueLogsMapper.kt#L41) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-12840a5d9cbb2b74) |
| `smartwork.dbo.BULK_RECEIPT_ISSUE_JOB` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/billing/bulkreceiptissuelogs/repository/BulkReceiptIssueLogsMapper.kt#L87) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-59fa08958b4abc13) |
| `smartwork.dbo.BULK_RECEIPT_ISSUE_JOB_RESULT` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/billing/bulkreceiptissuelogs/repository/BulkReceiptIssueLogsMapper.kt#L87) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-abb63c3075531376) |
| `smartwork.dbo.sw_log_system_event` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/billing/bulkreceiptissuelogs/repository/BulkReceiptIssueLogsMapper.kt#L87) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-8196d04946c1429b) |
| `SB_DTI.dbo.DTI_HEADER_CUB` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM · 정의 참조 `sb_dti.dbo.dti_header_cub_2023_07`, `sb_dti.dbo.dti_header_cub_part`, `sb_dti.dbo.dti_header_cub_prev_buffer` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/billing/bulkreceiptissuelogs/repository/BulkReceiptIssueLogsMapper.kt#L100) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-9b704ca2245fb3f1) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 오류 발생일자, 업체 조건, 사업자번호, 회사명, 참조번호, 당시 오류 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 서비스 현황 > 요금관리 > 영수 대량 발행 오류 로그 조회의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 참조번호를 선택하여 직접 복사해 주세요. | 오류 발생일자, 업체 조건, 사업자번호, 회사명, 참조번호, 당시 오류 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/BillingManagementRoutes.tsx#L17) · [BulkReceiptIssueLogsPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/BulkReceiptIssueLogsPage.tsx#L64) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/api/bulkReceiptIssueLogsApi.ts#L21) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 5개 중 개발 메타데이터 확인 5개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-b5abf987bd4c5ab3) | Demo 메타데이터 5/5개 확인 · Dev와 계약 차이 2개 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

# [이용료 청구·일일 정산·영수 발행] 영수 대량 발행 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

조건에 맞는 영수 세금계산서 대상을 확인하고 여러 건을 한 작업으로 발행한다. 결과 미확인 건은 같은 문서의 외부 발행 상태를 조회해 중복 발행을 피한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 이용료 청구·일일 정산·영수 발행 |
| 언제 사용하는가 | 진행 중인 영수 대량 발행 Job 조회, 영수 대량 발행 Job 상태 조회, 영수 대량 발행 대상 미리보기, 영수 대량 발행 재처리 대상 조회, 진행 중인 상태 확인 조회 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 발행 대상·배치 진행·건별 결과 |
| 업무 흐름 | 진행 중인 영수 대량 발행 Job 조회, 영수 대량 발행 Job 상태 조회, 영수 대량 발행 대상 미리보기, 영수 대량 발행 재처리 대상 조회, 진행 중인 상태 확인 조회 |
| 이 페이지의 역할 | 조회 · 영수 대량 발행 Job 상태 조회 |
| 판단 결과·다음 업무 | [로그 관리](../settings/log-management.md) |
| 다른 화면과의 구분 | 이 경로에서 볼 수 있는 조건·결과를 기준으로 사용한다. 독립 경로의 상세·등록은 관련 화면에 연결한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 일반 발행 | 미발행 저장 문서를 처음 발행할 때 | 발행 대상과 작업 진행·결과 | 건수를 확인하고 발행한다. |
| 실패 재처리 | 실패 또는 결과 미확인 작업을 조사할 때 | 작업 이력, 오류 건, 외부 상태 확인 결과 | 발행 여부와 재처리 가능 상태를 대조한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 조건에 맞는 영수 세금계산서 대상을 확인하고 여러 건을 한 작업으로 발행한다. 결과 미확인 건은 같은 문서의 외부 발행 상태를 조회해 중복 발행을 피한다. |
| 메뉴·화면 경로 | 서비스 현황 > 요금관리 > 영수 대량 발행 · `/billing-management/bulk-receipt-issue` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [로그 관리](../settings/log-management.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/billing-management/bulk-receipt-issue` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 진행 중인 영수 대량 발행 Job 조회 | `/billing-management/bulk-receipt-issue` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 영수 대량 발행 Job 상태 조회 | `/billing-management/bulk-receipt-issue` `VIEW` | `jobId: String` |
| 영수 대량 발행 대상 미리보기 | `/billing-management/bulk-receipt-issue` `VIEW` | `BulkReceiptIssuePreviewRequest` `startDate`, `endDate`, `searchType`, `searchValue` · 서버 필수 `startDate`, `endDate` |
| 영수 대량 발행 재처리 대상 조회 | `/billing-management/bulk-receipt-issue` `VIEW` | `jobId: String` · `BulkReceiptIssueRetryTargetsRequest` `searchType`, `searchValue`, `page`, `size`, `retryableOnly` |
| 진행 중인 상태 확인 조회 | `/billing-management/bulk-receipt-issue` `VIEW` | `jobId: String` |
| 상태 확인 진행률 조회 | `/billing-management/bulk-receipt-issue` `VIEW` | `checkId: String` |
| 영수 대량 발행 Job 이력 | `/billing-management/bulk-receipt-issue` `VIEW` | `BulkReceiptIssueRetrySearchRequest` `startDate`, `endDate`, `searchType`, `searchValue`, `page`, `size`, `retryableOnly` · 서버 필수 `startDate`, `endDate` |
| 영수 대량 발행 Job 결과 조회 | `/billing-management/bulk-receipt-issue` `VIEW` | `jobId: String` · `BulkReceiptIssueJobResultsRequest` `page`, `size` |
| 영수 대량 발행 Job 시작 | `/billing-management/bulk-receipt-issue` `PROCESS` | `BulkReceiptIssueJobStartRequest` `startDate`, `endDate`, `searchType`, `searchValue`, `expectedCount` · 서버 필수 `startDate`, `endDate` |
| 확인 필요 건 전체 상태 확인 | `/billing-management/bulk-receipt-issue` `PROCESS` | `jobId: String` |
| 영수 대량 발행 선택 건 재처리 | `/billing-management/bulk-receipt-issue` `PROCESS` | `jobId: String` · `BulkReceiptIssueRetryStartRequest` `targets`, `unknownRetryConfirmed` |

코드에서 확인한 버튼·작업명은 **검색**, **발행**, **오류 이력 보기**, **오류 ID 복사**, **새로고침**, **다시 시도**, **선택 작업 오류 목록**, **확인 필요 건 전체 상태 확인**, **확인 작업 다시 조회**, **선택 건 재처리**, **취소**, **재처리 실행**, **확인**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **일반 발행** 탭에서 업체 조건 등 조회 조건을 정하고 **검색**을 누른다. 화면에서 **발행 대상** 건수를 확인한다.
2. 발행 권한이 있고 대상이 있으면 **발행**을 선택한다. 확인창의 대상 건수를 보고 다시 **발행**을 누른 뒤 진행과 완료 결과를 확인한다.
3. **실패 재처리** 탭에서 실행일자·업체 조건으로 작업 이력을 찾고 오류 건을 확인한다. 발행 여부가 불확실한 건은 **확인 필요 건 전체 상태 확인**으로 외부 상태를 확인한다.
4. 외부 확인에서 이미 발행된 건은 다시 발행하지 않는다. 미발행 저장으로 확인되고 다른 제외 조건이 없는 건은 **선택 건 재처리**로 요청한다. 재처리 직전에 시스템이 현재 상태를 다시 대조한다.

**발행**을 확인하면 확인창은 진행 창으로 바뀐다. 작업은 대상 건을 순차 발행한다. 진행 창에서 전체·처리 건수와 성공·실패·확인 필요·제외를 구분해 읽는다. 진행 조회에 실패해도 마지막 확인 건수를 표시하며, 작업이 진행 중이면 중복 발행 버튼을 누를 수 없다. [진행 창](https://github.com/thebusinesson/smartwork/blob/b923849c5d878772e0de2b67becff0ae511f03b3/frontend/src/feature/status/billing/components/BulkReceiptIssueProgressDialog.tsx) · [순차 발행](https://github.com/thebusinesson/smartwork/blob/b923849c5d878772e0de2b67becff0ae511f03b3/backend/src/main/kotlin/com/bizon/smartwork/core/status/billing/bulkreceiptissue/service/BulkReceiptIssueProcessor.kt)

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 작성일자 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/BulkReceiptIssuePage.tsx#L67) |
| 업체 조건 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/BulkReceiptIssuePage.tsx#L71) |
| 실행일시 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `job.createdAt` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/components/BulkReceiptIssueRetryPanel.tsx#L208) |
| 배치 ID | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `job.batchId` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/components/BulkReceiptIssueRetryPanel.tsx#L209) |
| 전체 | 출력 | 조회 응답 기준 | 화면 필드 `currentSummary.totalCount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/components/BulkReceiptIssueRetryPanel.tsx#L210) |
| 성공 | 출력 | 조회 응답 기준 | 화면 필드 `currentSummary.successCount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/components/BulkReceiptIssueRetryPanel.tsx#L219) |
| 실패 | 출력 | 조회 응답 기준 | 화면 필드 `currentSummary.failureCount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/components/BulkReceiptIssueRetryPanel.tsx#L220) |
| 확인 필요 | 출력 | 조회 응답 기준 | 화면 필드 `currentSummary.unknownCount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/components/BulkReceiptIssueRetryPanel.tsx#L221) |
| 재처리 가능 | 출력 | 조회 응답 기준 | API 응답 `retryableCount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/components/BulkReceiptIssueRetryPanel.tsx#L222) |
| 유형 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `sourceJobId` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/components/BulkReceiptIssueRetryPanel.tsx#L223) |
| 오류 목록 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `action` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/components/BulkReceiptIssueRetryPanel.tsx#L224) |
| 거래처명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `companyName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/components/BulkReceiptIssueRetryPanel.tsx#L230) |
| 사업자번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `businessNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/components/BulkReceiptIssueRetryPanel.tsx#L231) |
| 참조번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `conversationId` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/components/BulkReceiptIssueRetryPanel.tsx#L232) |
| 실행 당시 결과 | 출력 | 조회 응답 기준 | API 응답 `status` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/components/BulkReceiptIssueRetryPanel.tsx#L233) |
| 코드 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `resultCode` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/components/BulkReceiptIssueRetryPanel.tsx#L234) |
| 오류 내용 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `reason` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/components/BulkReceiptIssueRetryPanel.tsx#L235) |
| 현재 결과 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `latestStatus` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/components/BulkReceiptIssueRetryPanel.tsx#L236) |
| 재처리 여부 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `ineligibleReason` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/components/BulkReceiptIssueRetryPanel.tsx#L238) |
| 오류 증적 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `errorEventId` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/components/BulkReceiptIssueRetryPanel.tsx#L239) |
| 전송상태 | 출력 | 조회 응답 기준 | API 응답 `status` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/components/BulkReceiptIssueResultDialog.tsx#L75) |
| 상태코드 | 출력 | 조회 응답 기준 | 화면 필드 `resultCode` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/components/BulkReceiptIssueResultDialog.tsx#L90) |
| 리턴값 | 출력 | 조회 응답 기준 | 화면 필드 `resultMessage` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/components/BulkReceiptIssueResultDialog.tsx#L93) |
| 영수 발행 처리 진행률 | 출력 | 진행 상태는 약 2초마다 갱신 | processedCount / totalCount와 건별 처리 결과 집계 |
| 성공·실패·확인 필요·제외 | 출력 | 진행 창과 완료 결과에 사용 | successCount, failureCount, unknownCount, skippedCount |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 진행 중인 영수 대량 발행 Job 조회 | `GET /api/v1/service-status/billing/bulk-receipt-issues/jobs/active` · `/billing-management/bulk-receipt-issue` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/billing/bulkreceiptissue/BulkReceiptIssueController.kt#L63) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `jobId`, `batchId`, `status`, `totalCount`, `processedCount`, `successCount`, `failureCount`, `skippedCount`, `unknownCount` | 직접 DB 호출이 연결된 경로는 현재 소스에서 미확인. 세부 저장소는 Controller와 Service 참조. |
| 영수 대량 발행 Job 상태 조회 | `GET /api/v1/service-status/billing/bulk-receipt-issues/jobs/{jobId}` · `/billing-management/bulk-receipt-issue` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/billing/bulkreceiptissue/BulkReceiptIssueController.kt#L69) | `jobId: String` → `success`, `data`, `error`, `jobId`, `batchId`, `status`, `totalCount`, `processedCount`, `successCount`, `failureCount`, `skippedCount`, `unknownCount` | `smartwork.dbo.usp_bulk_receipt_issue_job_detail_select` |
| 영수 대량 발행 대상 미리보기 | `GET /api/v1/service-status/billing/bulk-receipt-issues/preview` · `/billing-management/bulk-receipt-issue` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/billing/bulkreceiptissue/BulkReceiptIssueController.kt#L45) | `BulkReceiptIssuePreviewRequest` `startDate`, `endDate`, `searchType`, `searchValue` · 서버 필수 `startDate`, `endDate` → `success`, `data`, `error`, `targetCount` | `smartwork.dbo.usp_bulk_receipt_issue_preview_select` · 코드 연계 트랜잭션 |
| 영수 대량 발행 재처리 대상 조회 | `GET /api/v1/service-status/billing/bulk-receipt-issues/jobs/{jobId}/retry-targets` · `/billing-management/bulk-receipt-issue` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/billing/bulkreceiptissue/BulkReceiptIssueController.kt#L92) | `jobId: String` · `BulkReceiptIssueRetryTargetsRequest` `searchType`, `searchValue`, `page`, `size`, `retryableOnly` → `success`, `data`, `error`, `content`, `retryableCount`, `totalElements`, `totalPages`, `currentPage`, `size` | `smartwork.dbo.usp_bulk_receipt_issue_job_detail_select` |
| 진행 중인 상태 확인 조회 | `GET /api/v1/service-status/billing/bulk-receipt-issues/jobs/{jobId}/status-checks/active` · `/billing-management/bulk-receipt-issue` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/billing/bulkreceiptissue/BulkReceiptIssueController.kt#L110) | `jobId: String` → `success`, `data`, `error`, `checkId`, `jobId`, `status`, `totalCount`, `processedCount`, `issuedCount`, `savedCount`, `blockedCount`, `failedCount` | `smartwork.dbo.usp_bulk_receipt_issue_job_detail_select`, `smartwork.dbo.sw_log_system_event` |
| 상태 확인 진행률 조회 | `GET /api/v1/service-status/billing/bulk-receipt-issues/status-checks/{checkId}` · `/billing-management/bulk-receipt-issue` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/billing/bulkreceiptissue/BulkReceiptIssueController.kt#L118) | `checkId: String` → `success`, `data`, `error`, `checkId`, `jobId`, `status`, `totalCount`, `processedCount`, `issuedCount`, `savedCount`, `blockedCount`, `failedCount` | `smartwork.dbo.sw_log_system_event` |
| 영수 대량 발행 Job 이력 | `GET /api/v1/service-status/billing/bulk-receipt-issues/jobs` · `/billing-management/bulk-receipt-issue` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/billing/bulkreceiptissue/BulkReceiptIssueController.kt#L86) | `BulkReceiptIssueRetrySearchRequest` `startDate`, `endDate`, `searchType`, `searchValue`, `page`, `size`, `retryableOnly` · 서버 필수 `startDate`, `endDate` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `currentPage`, `size` | 코드 연계 트랜잭션 |
| 영수 대량 발행 Job 결과 조회 | `GET /api/v1/service-status/billing/bulk-receipt-issues/jobs/{jobId}/results` · `/billing-management/bulk-receipt-issue` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/billing/bulkreceiptissue/BulkReceiptIssueController.kt#L77) | `jobId: String` · `BulkReceiptIssueJobResultsRequest` `page`, `size` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `currentPage`, `size` | `smartwork.dbo.usp_bulk_receipt_issue_job_detail_select` |
| 영수 대량 발행 Job 시작 | `POST /api/v1/service-status/billing/bulk-receipt-issues/jobs` · `/billing-management/bulk-receipt-issue` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/billing/bulkreceiptissue/BulkReceiptIssueController.kt#L53) | `BulkReceiptIssueJobStartRequest` `startDate`, `endDate`, `searchType`, `searchValue`, `expectedCount` · 서버 필수 `startDate`, `endDate` → `success`, `data`, `error`, `jobId`, `batchId`, `status`, `totalCount`, `processedCount`, `successCount`, `failureCount`, `skippedCount`, `unknownCount` | `smartwork.dbo.usp_bulk_receipt_issue_job_start`, `smartwork.dbo.usp_bulk_receipt_issue_job_claim`, `smartwork.dbo.BULK_RECEIPT_ISSUE_JOB`, `smartwork.dbo.BULK_RECEIPT_ISSUE_JOB_RESULT`, `smartwork.dbo.sw_log_system_event` 외 3개 · 정의에서 확인한 쓰기 `SB_COMMON.dbo.SB_USEBILL_BATCH`, `smartwork.dbo.BULK_RECEIPT_ISSUE_JOB`, `smartwork.dbo.BULK_RECEIPT_ISSUE_JOB_RESULT`, `smartwork.dbo.sw_log_system_event` 외 1개 · 코드 연계 트랜잭션 |
| 확인 필요 건 전체 상태 확인 | `POST /api/v1/service-status/billing/bulk-receipt-issues/jobs/{jobId}/status-checks` · `/billing-management/bulk-receipt-issue` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/billing/bulkreceiptissue/BulkReceiptIssueController.kt#L101) | `jobId: String` → `success`, `data`, `error`, `checkId`, `jobId`, `status`, `totalCount`, `processedCount`, `issuedCount`, `savedCount`, `blockedCount`, `failedCount` | `smartwork.dbo.usp_bulk_receipt_issue_job_detail_select`, `smartwork.dbo.sw_log_system_event`, `smartwork.dbo.BULK_RECEIPT_ISSUE_JOB_RESULT`, `smartwork.dbo.BULK_RECEIPT_ISSUE_JOB`, `SB_DTI.dbo.DTI_HEADER_CUB` |
| 영수 대량 발행 선택 건 재처리 | `POST /api/v1/service-status/billing/bulk-receipt-issues/jobs/{jobId}/retries` · `/billing-management/bulk-receipt-issue` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/billing/bulkreceiptissue/BulkReceiptIssueController.kt#L126) | `jobId: String` · `BulkReceiptIssueRetryStartRequest` `targets`, `unknownRetryConfirmed` → `success`, `data`, `error`, `jobId`, `batchId`, `status`, `totalCount`, `processedCount`, `successCount`, `failureCount`, `skippedCount`, `unknownCount` | `smartwork.dbo.usp_bulk_receipt_issue_job_detail_select` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.usp_bulk_receipt_issue_job_detail_select` | @JobId varchar(36) | 정의 참조 `smartwork.dbo.BULK_RECEIPT_ISSUE_JOB` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/billing/bulkreceiptissue/repository/BulkReceiptIssueMapper.kt#L74) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b7472e46028b7f27) |
| `smartwork.dbo.usp_bulk_receipt_issue_preview_select` | @StartDate varchar(10), @EndDate varchar(10), @SearchType varchar(20), @SearchValue varchar(20) | 정의 참조 `smartwork.dbo.BULK_RECEIPT_ISSUE_JOB_RESULT`, `SB_DTI.dbo.DTI_HEADER_CUB`, `master.dbo.enc_index_char_sel_tc`, `SmartBill3.dbo.MEMBER`, `SB_BILL.dbo.TAXINVOICE_CONTROL` · 하위 호출 `master.dbo.enc_index_char_sel_tc` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/billing/bulkreceiptissue/repository/BulkReceiptIssueMapper.kt#L36) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b3dd6a0dcae33e63) |
| `smartwork.dbo.sw_log_system_event` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/billing/bulkreceiptissue/repository/BulkReceiptIssueStatusCheckMapper.kt#L42) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-8196d04946c1429b) |
| `smartwork.dbo.usp_bulk_receipt_issue_job_start` | @AdminNo bigint, @StartDate varchar(10), @EndDate varchar(10), @SearchType varchar(20), @SearchValue varchar(20), @ExpectedCount int | 정의 참조 `smartwork.dbo.BULK_RECEIPT_ISSUE_JOB`, `smartwork.dbo.BULK_RECEIPT_ISSUE_JOB_RESULT`, `SB_DTI.dbo.DTI_HEADER_CUB`, `master.dbo.enc_index_char_sel_tc`, `SmartBill3.dbo.MEMBER` 외 2개 · 정적 쓰기 `SB_COMMON.dbo.SB_USEBILL_BATCH`, `smartwork.dbo.BULK_RECEIPT_ISSUE_JOB`, `smartwork.dbo.BULK_RECEIPT_ISSUE_JOB_RESULT` · 하위 호출 `master.dbo.enc_index_char_sel_tc` · 동적 SQL 포함 · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/billing/bulkreceiptissue/repository/BulkReceiptIssueMapper.kt#L46) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-713997c71a3b7420) |
| `smartwork.dbo.usp_bulk_receipt_issue_job_claim` | @LeaseOwner varchar(100), @LeaseSeconds int, @JobId varchar(36) = NULL | 정의 참조 `smartwork.dbo.BULK_RECEIPT_ISSUE_JOB` · 정적 쓰기 `smartwork.dbo.BULK_RECEIPT_ISSUE_JOB` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/billing/bulkreceiptissue/repository/BulkReceiptIssueMapper.kt#L79) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-c17c4a49772ff0cd) |
| `smartwork.dbo.BULK_RECEIPT_ISSUE_JOB` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/billing/bulkreceiptissue/repository/BulkReceiptIssueAuditMapper.kt#L15) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-59fa08958b4abc13) |
| `smartwork.dbo.BULK_RECEIPT_ISSUE_JOB_RESULT` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/billing/bulkreceiptissue/repository/BulkReceiptIssueAuditMapper.kt#L24) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-abb63c3075531376) |
| `SB_COMMON.dbo.SB_USEBILL_BATCH_LOG` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL INSERT INTO | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/billing/bulkreceiptissue/repository/BulkReceiptIssueAuditMapper.kt#L41) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-989a543bc1cb7b7b) |
| `smartwork.dbo.usp_bulk_receipt_issue_target_page_select` | @JobId varchar(36), @AfterDtiWday varchar(10) = NULL, @AfterDtiIdx bigint = NULL, @PageSize int = 300 | 정의 참조 `smartwork.dbo.BULK_RECEIPT_ISSUE_JOB_RESULT`, `SB_DTI.dbo.DTI_HEADER_CUB` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/billing/bulkreceiptissue/repository/BulkReceiptIssueMapper.kt#L89) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-99f403bd77ba0b68) |
| `smartwork.dbo.usp_bulk_receipt_issue_target_processing` | @JobId varchar(36), @LeaseOwner varchar(100), @DtiWday varchar(10), @DtiIdx bigint | 정의 참조 `smartwork.dbo.BULK_RECEIPT_ISSUE_JOB`, `smartwork.dbo.BULK_RECEIPT_ISSUE_JOB_RESULT`, `SB_DTI.dbo.DTI_HEADER_CUB` · 쓰기 구문 존재 · 대상 별칭 또는 하위 정의 확인 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/billing/bulkreceiptissue/repository/BulkReceiptIssueMapper.kt#L94) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-67fa37edd9502cc9) |
| `SB_DTI.dbo.DTI_HEADER_CUB` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN · 정의 참조 `sb_dti.dbo.dti_header_cub_2023_07`, `sb_dti.dbo.dti_header_cub_part`, `sb_dti.dbo.dti_header_cub_prev_buffer` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/billing/bulkreceiptissue/repository/BulkReceiptIssueStatusCheckMapper.kt#L95) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-9b704ca2245fb3f1) |

### 매퍼 호출 추가 확인

| DB 객체 | 호출 근거 | 개발 DB 확인 범위 |
| --- | --- | --- |
| [smartwork.dbo.usp_bulk_receipt_issue_job_active_select](../../references/all-pages-demo.md#object-52881e24b2da4862) | [findActiveJob](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/billing/bulkreceiptissue/repository/BulkReceiptIssueMapper.kt#L69) | 개발 카탈로그 확인 |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 발행 대상·배치 진행·건별 결과 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 서비스 현황 > 요금관리 > 영수 대량 발행의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 검색 조건에 해당하는 발행 대상이 없습니다. | 발행 대상·배치 진행·건별 결과 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 이미 진행 중인 영수 대량 발행 작업에 연결합니다. | 발행 대상·배치 진행·건별 결과 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 발행 대상이 변경되어 다시 조회했습니다. | 발행 대상·배치 진행·건별 결과 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 전체 선택 목록을 불러오지 못했습니다. 다시 시도해 주세요. | 발행 대상·배치 진행·건별 결과 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/BillingManagementRoutes.tsx#L16) · [BulkReceiptIssuePage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/BulkReceiptIssuePage.tsx#L43) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/api/bulkReceiptIssueApi.ts#L36) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/api/bulkReceiptIssueApi.ts#L40) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/api/bulkReceiptIssueApi.ts#L26) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/api/bulkReceiptIssueApi.ts#L65) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/api/bulkReceiptIssueApi.ts#L85) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/api/bulkReceiptIssueApi.ts#L81) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/api/bulkReceiptIssueApi.ts#L54) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/api/bulkReceiptIssueApi.ts#L48) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 11개 중 개발 메타데이터 확인 11개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-38405578bc770ebc) | 2026-11-11 기준으로 Demo 메타데이터 12/12개 확인 · Dev와 계약 차이 2개 · 2026-11-11 |
| 화면 재현 | [로컬 Playwright 표본](../../evidence/browser/all-pages-sample-2026-11-11.json) | 진입 및 표시 확인 · 표시 일반 발행, 실패 재처리 · 2026-11-11 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |
| 최신 변경 대조 | [11월 12일 전수 대조](../../references/all-pages-audit-2026-11-12.md) | 현재 코드 b923849c5 · 2026-11-12 |

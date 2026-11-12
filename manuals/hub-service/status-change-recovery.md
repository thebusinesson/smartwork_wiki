# [연동 문의·점검·라우팅·복구] [구연동] 복구솔루션 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

참조번호 또는 승인번호로 세금계산서 발행 정보를 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 연동 문의·점검·라우팅·복구 |
| 언제 사용하는가 | [구연동] 복구솔루션 단건 조회, [구연동] 복구솔루션 일괄 조회 샘플 다운로드, [구연동] 복구솔루션 일괄 조회, [구연동] 복구솔루션 상태비교, [구연동] 복구솔루션 상태변경 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 공급자, 공급받는자, 프로세스, 사업자번호, 회사명, 연동여부 |
| 업무 흐름 | [구연동] 복구솔루션 단건 조회, [구연동] 복구솔루션 일괄 조회 샘플 다운로드, [구연동] 복구솔루션 일괄 조회, [구연동] 복구솔루션 상태비교, [구연동] 복구솔루션 상태변경 |
| 이 페이지의 역할 | 조회 · [구연동] 복구솔루션 단건 조회 |
| 판단 결과·다음 업무 | 현재 화면에서 결과를 확인한다. |
| 다른 화면과의 구분 | 같은 경로에서 열리는 조회·팝업은 이 문서에서 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 확인 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/statusChangeRecovery/components/bulk/BatchLookupDialog.tsx#L257) |
| 시스템 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/statusChangeRecovery/components/comparison/StatusChangeRecoveryComparisonSection.tsx#L307) |
| 현재 상태 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/statusChangeRecovery/components/comparison/StatusChangeRecoveryComparisonSection.tsx#L308) |
| 상태변경 대상 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/statusChangeRecovery/components/comparison/StatusChangeRecoveryComparisonSection.tsx#L309) |
| 처리 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/statusChangeRecovery/components/comparison/StatusChangeRecoveryComparisonSection.tsx#L310) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 참조번호 또는 승인번호로 세금계산서 발행 정보를 조회한다. |
| 메뉴·화면 경로 | 연동 서비스 관리 > 연동 서비스 관리 > [구연동] 복구솔루션 · `/hub-service/status-change-recovery` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | 현재 화면에서 결과를 확인한다. |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/hub-service/status-change-recovery` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| [구연동] 복구솔루션 단건 조회 | `/hub-service/status-change-recovery` `VIEW` | `StatusChangeRecoverySearchRequest` `searchType`, `searchValue` · 서버 필수 `searchValue` |
| [구연동] 복구솔루션 일괄 조회 샘플 다운로드 | `/hub-service/status-change-recovery` `VIEW` | `searchType: String` |
| [구연동] 복구솔루션 일괄 조회 | `/hub-service/status-change-recovery` `VIEW` | `file: MultipartFile` · `searchType: String` |
| [구연동] 복구솔루션 상태비교 | `/hub-service/status-change-recovery` `VIEW` | `StatusChangeRecoveryComparisonRequest` `referenceNumber`, `selectedTargetKeys` · 서버 필수 `referenceNumber` |
| [구연동] 복구솔루션 상태변경 | `/hub-service/status-change-recovery` `PROCESS` | `StatusChangeRecoveryStatusChangeRequest` `referenceNumber`, `targetSystem`, `targetKey`, `statusChangeCode`, `oldStatus`, `checkNtsTransmission`, `checkReceiptApproval`, `selectedTargetKeys` · 서버 필수 `referenceNumber`, `targetSystem`, `statusChangeCode` |
| [구연동] 복구솔루션 등록번호 원문 조회 | `/hub-service/status-change-recovery` / `UNMASK` | `referenceNumber`, `field` |

코드에서 확인한 버튼·작업명은 **접속**, **일괄조회**, **검색**, **샘플 다운로드**, **취소**, **일괄 조회**, **첨부파일**, **확인**, **상태비교**, **상태변경**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **연동 서비스 관리 > 연동 서비스 관리 > [구연동] 복구솔루션**를 연다. `/hub-service/status-change-recovery`를 연다.
2. **공급받는자 사업자번호**, **참조번호**, **승인번호**, **첨부파일**, **국세청 전송**, **수신승인, 미승인 체크** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **일괄조회**, **검색**, **샘플 다운로드**, **일괄 조회**, **확인** 중 해당 버튼을 선택한다.
3. **[구연동] 복구솔루션 단건 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 공급자 | 출력 | 조회 응답 기준 | 화면 필드 `supplier-group` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/statusChangeRecovery/components/StatusChangeRecoverySearchSection.tsx#L313) |
| 공급받는자 | 출력 | 조회 응답 기준 | 화면 필드 `recipient-group` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/statusChangeRecovery/components/StatusChangeRecoverySearchSection.tsx#L314) |
| 프로세스 | 출력 | 조회 응답 기준 | 화면 필드 `supplier.process` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/statusChangeRecovery/components/StatusChangeRecoverySearchSection.tsx#L319) |
| 사업자번호 | 출력 | 조회 응답 기준 | 화면 필드 `supplier.businessNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/statusChangeRecovery/components/StatusChangeRecoverySearchSection.tsx#L325) |
| 회사명 | 출력 | 조회 응답 기준 | 화면 필드 `supplier.companyName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/statusChangeRecovery/components/StatusChangeRecoverySearchSection.tsx#L331) |
| 연동여부 | 출력 | 조회 응답 기준 | 화면 필드 `supplier.integrationStatus` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/statusChangeRecovery/components/StatusChangeRecoverySearchSection.tsx#L337) |
| 공급받는자 사업자번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `BUYER_BUSINESS_NUMBER` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/statusChangeRecovery/components/StatusChangeRecoverySearchSection.tsx#L355) |
| 참조번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `reference` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/statusChangeRecovery/components/StatusChangeRecoverySearchSection.tsx#L62) |
| 승인번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `approval` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/statusChangeRecovery/components/StatusChangeRecoverySearchSection.tsx#L63) |
| 첨부파일 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/statusChangeRecovery/components/bulk/BatchLookupDialog.tsx#L186) |
| 금액 입력 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/statusChangeRecovery/components/detail/StatusChangeRecoveryDetailSection.tsx#L168) |
| 날짜 선택 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/statusChangeRecovery/components/detail/StatusChangeRecoveryDetailSection.tsx#L186) |
| DTI_IDX 입력 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/statusChangeRecovery/components/detail/StatusChangeRecoveryDetailSection.tsx#L208) |
| 비고 입력 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/statusChangeRecovery/components/detail/StatusChangeRecoveryDetailSection.tsx#L246) |
| 유사건 정보 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/statusChangeRecovery/components/detail/StatusChangeRecoveryDetailSection.tsx#L266) |
| 선택 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/statusChangeRecovery/components/detail/StatusChangeRecoveryDetailSection.tsx#L308) |
| 국세청 전송 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/statusChangeRecovery/components/comparison/StatusChangeRecoveryComparisonSection.tsx#L367) |
| 수신승인, 미승인 체크 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/statusChangeRecovery/components/comparison/StatusChangeRecoveryComparisonSection.tsx#L371) |
| 구분 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/statusChangeRecovery/components/notice/StatusChangeRecoveryNoticeSection.tsx#L12) |
| 내용 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/statusChangeRecovery/components/notice/StatusChangeRecoveryNoticeSection.tsx#L13) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| [구연동] 복구솔루션 단건 조회 | `GET /api/v1/hub-service/status-change-recovery/search` · `/hub-service/status-change-recovery` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/statuschangerecovery/StatusChangeRecoveryController.kt#L62) | `StatusChangeRecoverySearchRequest` `searchType`, `searchValue` · 서버 필수 `searchValue` → `success`, `data`, `error`, `content`, `totalElements` | 코드 연계 트랜잭션 |
| [구연동] 복구솔루션 일괄 조회 샘플 다운로드 | `GET /api/v1/hub-service/status-change-recovery/template` · `/hub-service/status-change-recovery` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/statuschangerecovery/StatusChangeRecoveryController.kt#L89) | `searchType: String` → 파일 또는 오류 응답 | 직접 DB 호출이 연결된 경로는 현재 소스에서 미확인. 세부 저장소는 Controller와 Service 참조. |
| [구연동] 복구솔루션 일괄 조회 | `POST /api/v1/hub-service/status-change-recovery/batch-search` · `/hub-service/status-change-recovery` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/statuschangerecovery/StatusChangeRecoveryController.kt#L75) | `file: MultipartFile` · `searchType: String` → `success`, `data`, `error`, `processedCount`, `failedCount`, `results`, `errors` | 직접 DB 호출이 연결된 경로는 현재 소스에서 미확인. 세부 저장소는 Controller와 Service 참조. |
| [구연동] 복구솔루션 상태비교 | `POST /api/v1/hub-service/status-change-recovery/status-comparison` · `/hub-service/status-change-recovery` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/statuschangerecovery/StatusChangeRecoveryController.kt#L123) | `StatusChangeRecoveryComparisonRequest` `referenceNumber`, `selectedTargetKeys` · 서버 필수 `referenceNumber` → `success`, `data`, `error`, `rows`, `statusChangeOptions` | 직접 DB 호출이 연결된 경로는 현재 소스에서 미확인. 세부 저장소는 Controller와 Service 참조. |
| [구연동] 복구솔루션 상태변경 | `POST /api/v1/hub-service/status-change-recovery/status-change` · `/hub-service/status-change-recovery` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/statuschangerecovery/StatusChangeRecoveryController.kt#L109) | `StatusChangeRecoveryStatusChangeRequest` `referenceNumber`, `targetSystem`, `targetKey`, `statusChangeCode`, `oldStatus`, `checkNtsTransmission`, `checkReceiptApproval`, `selectedTargetKeys` · 서버 필수 `referenceNumber`, `targetSystem`, `statusChangeCode` → `success`, `data`, `error`, `outcome`, `history`, `returnCode`, `operationId`, `historyId`, `audit`, `message` | `smartwork.dbo.usp_sw_log_access_event_insert` · 정의에서 확인한 쓰기 `smartwork.dbo.sw_log_access_event` · 코드 연계 트랜잭션 |
| [구연동] 복구솔루션 등록번호 원문 조회 | `POST /api/v1/hub-service/status-change-recovery/{referenceNumber}/sensitive-values/reveal` · `/hub-service/status-change-recovery` / `UNMASK` · [화면 컴포넌트](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/statusChangeRecovery/components/StatusChangeRecoverySearchSection.tsx#L353) · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/statuschangerecovery/StatusChangeRecoveryController.kt#L133) | `referenceNumber`, `field` → 요청한 항목의 원문 응답 | 권한 검사 후 대상 값을 조회하고 감사 기록을 남긴다. |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.usp_sw_log_access_event_insert` | @EVENT_TYPE varchar(30), @STATUS varchar(20), @USER_ID bigint = NULL, @MEMBER_ID nvarchar(50) = NULL, @USER_NAME nvarchar(100) = NULL, @DEPARTMENT_NAME nvarchar(100) = NULL, @PAGE_TITLE nvarchar(200) = NULL, @PATH nvarchar(500) = NULL, @MENU_PATH nvarchar(500) = NULL, @MENU_LABEL nvarchar(200) = NULL, @CATEGORY_NAME nvarchar(200) = NULL, @SUB_CATEGORY_NAME nvarchar(200) = NULL, @MENU_ORDER int = NULL, @IP_ADDRESS varchar(45) = NULL, @USER_AGENT nvarchar(1000) = NULL, @BROWSER varchar(100) = NULL, @OS varchar(100) = NULL, @REFERRER nvarchar(500) = NULL, @DETAIL nvarchar(1000) = NULL, @RESULT int OUT, @COUNTS_AS_VISIT bit = 1 | 정의 참조 `smartwork.dbo.sw_log_access_event` · 정적 쓰기 `smartwork.dbo.sw_log_access_event` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/logmanagement/repository/LogManagementMapper.kt#L92) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b7ba94e0cc2f35c0) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 공급자, 공급받는자, 프로세스, 사업자번호, 회사명, 연동여부 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 연동 서비스 관리 > 연동 서비스 관리 > [구연동] 복구솔루션의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 참조번호/승인번호가 존재하지 않습니다. | 공급자, 공급받는자, 프로세스, 사업자번호, 회사명, 연동여부 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 검색 중 오류가 발생했습니다. | 공급자, 공급받는자, 프로세스, 사업자번호, 회사명, 연동여부 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 조회된 결과가 없습니다. | 공급자, 공급받는자, 프로세스, 사업자번호, 회사명, 연동여부 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 파일 업로드 중 오류가 발생했습니다. | 공급자, 공급받는자, 프로세스, 사업자번호, 회사명, 연동여부 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/IntegrationRoutes.tsx#L159) · [StatusChangeRecoveryPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/StatusChangeRecoveryPage.tsx#L24) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/statusChangeRecovery/api/statusChangeRecoveryApi.ts#L28) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/statusChangeRecovery/api/statusChangeRecoveryApi.ts#L54) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/statusChangeRecovery/api/statusChangeRecoveryApi.ts#L44) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/statusChangeRecovery/api/statusChangeRecoveryApi.ts#L67) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/statusChangeRecovery/api/statusChangeRecoveryApi.ts#L60) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 1개 중 개발 메타데이터 확인 1개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-512d6980bd74082a) | Demo 메타데이터 1/1개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

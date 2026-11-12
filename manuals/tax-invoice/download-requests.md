# [수신 변경·알림·다운로드] 다운로드 요청/처리 조회 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

요청일자, 처리일자, 업체 조건, 처리 상태 기준으로 세금계산서 다운로드 요청 내역을 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 수신 변경·알림·다운로드 |
| 언제 사용하는가 | 세금계산서 다운로드 요청/처리 조회 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 번호, 요청일자, 사업자번호, 회사명, 요청자, 업체수 |
| 업무 흐름 | 세금계산서 다운로드 요청/처리 조회 |
| 이 페이지의 역할 | 조회 · 세금계산서 다운로드 요청/처리 조회 |
| 판단 결과·다음 업무 | 현재 화면에서 결과를 확인한다. |
| 다른 화면과의 구분 | 같은 경로에서 열리는 조회·팝업은 이 문서에서 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 요청일자, 처리일자, 업체 조건, 처리 상태 기준으로 세금계산서 다운로드 요청 내역을 조회한다. |
| 메뉴·화면 경로 | SB 서비스관리 > 전자세금계산서 > 다운로드 요청/처리 조회 · `/tax-invoice/download-requests` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | 현재 화면에서 결과를 확인한다. |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/tax-invoice/download-requests` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 세금계산서 다운로드 요청/처리 조회 | `/tax-invoice/download-requests` `VIEW` | `DownloadRequestSearchRequest` `requestFrom`, `requestTo`, `processFrom`, `processTo`, `searchType`, `keyword`, `status` |
| 다운로드 요청자명 원문 조회 | `/tax-invoice/download-requests` / `UNMASK` | `requestId`, `field` |

코드에서 확인한 버튼·작업명은 **검색**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **SB 서비스관리 > 전자세금계산서 > 다운로드 요청/처리 조회**를 연다. `/tax-invoice/download-requests`를 연다.
2. **회사명**, **요청 기간**, **처리 기간**, **업체 조건**, **전체**, **처리 상태**, **요청접수** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색** 중 해당 버튼을 선택한다.
3. **세금계산서 다운로드 요청/처리 조회** 처리 결과를 확인하고 받은 파일의 대상과 적용 조건을 대조한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 번호 | 출력 | 조회 응답 기준 | 화면 필드 `requestId` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/DownloadRequests.tsx#L32) |
| 요청일자 | 출력 | 조회 응답 기준 | 화면 필드 `requestDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/DownloadRequests.tsx#L33) |
| 사업자번호 | 출력 | 조회 응답 기준 | 화면 필드 `businessNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/DownloadRequests.tsx#L34) |
| 회사명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `companyName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/DownloadRequests.tsx#L124) |
| 요청자 | 출력 | 조회 응답 기준 | 화면 필드 `requester` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/DownloadRequests.tsx#L38) |
| 업체수 | 출력 | 조회 응답 기준 | 화면 필드 `companyCount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/DownloadRequests.tsx#L53) |
| 세금계산서수 | 출력 | 조회 응답 기준 | 화면 필드 `taxInvoiceCount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/DownloadRequests.tsx#L60) |
| 처리일자 | 출력 | 조회 응답 기준 | 화면 필드 `processedDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/DownloadRequests.tsx#L67) |
| 상태 | 출력 | 조회 응답 기준 | 화면 필드 `statusLabel` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/DownloadRequests.tsx#L72) |
| 요청 기간 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/DownloadRequests.tsx#L94) |
| 처리 기간 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/DownloadRequests.tsx#L104) |
| 업체 조건 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/DownloadRequests.tsx#L114) |
| 전체 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `all` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/DownloadRequests.tsx#L141) |
| 처리 상태 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/DownloadRequests.tsx#L135) |
| 요청접수 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `요청접수` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/DownloadRequests.tsx#L142) |
| 처리완료 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `처리완료` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/DownloadRequests.tsx#L143) |
| 배송완료 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `배송완료` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/DownloadRequests.tsx#L144) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 세금계산서 다운로드 요청/처리 조회 | `GET /api/v1/tax-invoice/download-requests` · `/tax-invoice/download-requests` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/taxinvoice/downloadrequest/DownloadRequestController.kt#L65) | `DownloadRequestSearchRequest` `requestFrom`, `requestTo`, `processFrom`, `processTo`, `searchType`, `keyword`, `status` → `success`, `data`, `error`, `content`, `totalElements` | `smartwork.dbo.upAdmSB_LstDownload01` · 코드 연계 트랜잭션 |
| 다운로드 요청자명 원문 조회 | `POST /api/v1/tax-invoice/download-requests/{requestId}/sensitive-values/reveal` · `/tax-invoice/download-requests` / `UNMASK` · [화면 컴포넌트](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/DownloadRequests.tsx#L43) · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/taxinvoice/downloadrequest/DownloadRequestController.kt#L78) | `requestId`, `field` → 요청한 항목의 원문 응답 | 권한 검사 후 대상 값을 조회하고 감사 기록을 남긴다. |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.upAdmSB_LstDownload01` | @fromDate varchar(20), @toDate varchar(20), @fromDate2 varchar(20), @toDate2 varchar(20), @strItem varchar(100), @strContents varchar(100), @cStatus varchar(2) | 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/downloadrequest/repository/DownloadRequestMapper.kt#L32) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-ba3c5e0f3f606602) |
| `SB_DTI.dbo.DTI_DOWNLOAD_REQUEST` | 개발 컬럼 메타데이터 확인 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/downloadrequest/repository/DownloadRequestMapper.kt#L44) |
| `SmartBill3.dbo.MEMBER` | 개발 컬럼 메타데이터 확인 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/downloadrequest/repository/DownloadRequestMapper.kt#L44) |
| `SmartBill3.dbo.COMPANY` | 개발 컬럼 메타데이터 확인 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/downloadrequest/repository/DownloadRequestMapper.kt#L44) |
| `smartwork.dbo.usp_sw_log_access_event_insert` | @EVENT_TYPE varchar(30) IN, @STATUS varchar(20) IN, @USER_ID bigint IN, @MEMBER_ID nvarchar(50) IN, @USER_NAME nvarchar(100) IN, @DEPARTMENT_NAME nvarchar(100) IN, @PAGE_TITLE nvarchar(200) IN, @PATH nvarchar(500) IN, @MENU_PATH nvarchar(500) IN, @MENU_LABEL nvarchar(200) IN, @CATEGORY_NAME nvarchar(200) IN, @SUB_CATEGORY_NAME nvarchar(200) IN, @MENU_ORDER int IN, @IP_ADDRESS varchar(45) IN, @USER_AGENT nvarchar(1000) IN, @BROWSER varchar(100) IN, @OS varchar(100) IN, @REFERRER nvarchar(500) IN, @DETAIL nvarchar(1000) IN, @RESULT int OUT, @COUNTS_AS_VISIT bit IN | 원문 조회 또는 감사 흐름에서 호출 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/logmanagement/repository/LogManagementMapper.kt#L92) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 번호, 요청일자, 사업자번호, 회사명, 요청자, 업체수 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 서비스관리 > 전자세금계산서 > 다운로드 요청/처리 조회의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 검색 결과가 없습니다. | 번호, 요청일자, 사업자번호, 회사명, 요청자, 업체수 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/TaxInvoiceRoutes.tsx#L41) · [DownloadRequests.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/DownloadRequests.tsx#L170) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/api/etaxSettingsApi.ts#L30) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 1개 중 개발 메타데이터 확인 1개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-05aa4d0c3fb354b7) | Demo 메타데이터 5/5개 확인 · Dev와 계약 차이 1개 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

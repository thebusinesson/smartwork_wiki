# [세금계산서·거래명세서 원문과 증빙] 지로 원본 다운로드 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

발행일자와 업체 조건으로 지로 원본 다운로드 대상을 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 세금계산서·거래명세서 원문과 증빙 |
| 언제 사용하는가 | 지로 원본 다운로드 목록 조회 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 번호, 발행일자, 사업자번호, 회사명, 요청자, 세금계산서수 |
| 업무 흐름 | 지로 원본 다운로드 목록 조회 |
| 이 페이지의 역할 | 조회 · 지로 원본 다운로드 목록 조회 |
| 판단 결과·다음 업무 | 현재 화면에서 결과를 확인한다. |
| 다른 화면과의 구분 | 같은 경로에서 열리는 조회·팝업은 이 문서에서 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 발행일자와 업체 조건으로 지로 원본 다운로드 대상을 조회한다. |
| 메뉴·화면 경로 | SB 서비스관리 > 전자세금계산서 > 지로 원본 다운로드 · `/tax-invoice/giro-original-download` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | 현재 화면에서 결과를 확인한다. |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/tax-invoice/giro-original-download` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 지로 원본 다운로드 목록 조회 | `/tax-invoice/giro-original-download` `VIEW` | `GiroDownloadSearchRequest` `startDate`, `endDate`, `includeAllCompanies`, `companySearchType`, `companyValue`, `page`, `size` |
| 지로 원본 요청자명 원문 조회 | `/tax-invoice/giro-original-download` / `UNMASK` | `uploadId`, `field` |

코드에서 확인한 버튼·작업명은 **다운로드**, **검색**, **선택 지로 원본 일괄 생성**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **SB 서비스관리 > 전자세금계산서 > 지로 원본 다운로드**를 연다. `/tax-invoice/giro-original-download`를 연다.
2. **업체 조건**, **전체** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **다운로드**, **검색** 중 해당 버튼을 선택한다.
3. **지로 원본 다운로드 목록 조회** 처리 결과를 확인하고 받은 파일의 대상과 적용 조건을 대조한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 번호 | 출력 | 조회 응답 기준 | 화면 필드 `rowNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/GiroOriginalDownloadPage.tsx#L264) |
| 발행일자 | 출력 | 조회 응답 기준 | 화면 필드 `issuanceDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/GiroOriginalDownloadPage.tsx#L269) |
| 사업자번호 | 출력 | 조회 응답 기준 | 화면 필드 `businessNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/GiroOriginalDownloadPage.tsx#L270) |
| 회사명 | 출력 | 조회 응답 기준 | 화면 필드 `companyName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/GiroOriginalDownloadPage.tsx#L271) |
| 요청자 | 출력 | 조회 응답 기준 | 화면 필드 `requester` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/GiroOriginalDownloadPage.tsx#L274) |
| 세금계산서수 | 출력 | 조회 응답 기준 | 화면 필드 `taxInvoiceCount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/GiroOriginalDownloadPage.tsx#L289) |
| 처리일자 | 출력 | 조회 응답 기준 | 화면 필드 `processedDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/GiroOriginalDownloadPage.tsx#L294) |
| 원본생성 | 출력 | 조회 응답 기준 | 화면 필드 `download` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/GiroOriginalDownloadPage.tsx#L297) |
| 업체 조건 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/GiroOriginalDownloadPage.tsx#L65) |
| 전체 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `all` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/GiroOriginalDownloadPage.tsx#L73) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 지로 원본 다운로드 목록 조회 | `GET /api/v1/tax-invoice/giro-downloads` · `/tax-invoice/giro-original-download` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/taxinvoice/girodownload/GiroDownloadController.kt#L57) | `GiroDownloadSearchRequest` `startDate`, `endDate`, `includeAllCompanies`, `companySearchType`, `companyValue`, `page`, `size` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `currentPage`, `size` | `smartwork.dbo.upSelect_CD_Request_LIST` · 코드 연계 트랜잭션 |
| 지로 원본 요청자명 원문 조회 | `POST /api/v1/tax-invoice/giro-downloads/{uploadId}/sensitive-values/reveal` · `/tax-invoice/giro-original-download` / `UNMASK` · [화면 컴포넌트](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/GiroOriginalDownloadPage.tsx#L279) · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/taxinvoice/girodownload/GiroDownloadController.kt#L67) | `uploadId`, `field` → 요청한 항목의 원문 응답 | 권한 검사 후 대상 값을 조회하고 감사 기록을 남긴다. |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.upSelect_CD_Request_LIST` | @Start_IssueDate varchar(10), @End_IssueDate varchar(10), @Com_Name varchar(100), @Com_Regno varchar(10), @Status varchar(10), @START_ROW varchar(10), @PAGE_SIZE varchar(10) | 정의 참조 `SB_DTI.dbo.BULK_FILE_UPLOAD`, `SmartBill3.dbo.COMPANY`, `SB_DTI.dbo.COMPANY_DTICONFIG`, `SB_DTI.dbo.DTI_HEADER_GIRO_CUB`, `SB_DTI.dbo.DTI_SIGN_GIRO_CUB` 외 1개 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/girodownload/repository/GiroDownloadMapper.kt#L48) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3fb4f9a3ddfd7b74) |
| `SB_DTI.dbo.BULK_FILE_UPLOAD` | 개발 컬럼 메타데이터 확인 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/girodownload/repository/GiroDownloadMapper.kt#L92) |
| `SmartBill3.dbo.MEMBER` | 개발 컬럼 메타데이터 확인 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/girodownload/repository/GiroDownloadMapper.kt#L92) |
| `smartwork.dbo.usp_sw_log_access_event_insert` | @EVENT_TYPE varchar(30) IN, @STATUS varchar(20) IN, @USER_ID bigint IN, @MEMBER_ID nvarchar(50) IN, @USER_NAME nvarchar(100) IN, @DEPARTMENT_NAME nvarchar(100) IN, @PAGE_TITLE nvarchar(200) IN, @PATH nvarchar(500) IN, @MENU_PATH nvarchar(500) IN, @MENU_LABEL nvarchar(200) IN, @CATEGORY_NAME nvarchar(200) IN, @SUB_CATEGORY_NAME nvarchar(200) IN, @MENU_ORDER int IN, @IP_ADDRESS varchar(45) IN, @USER_AGENT nvarchar(1000) IN, @BROWSER varchar(100) IN, @OS varchar(100) IN, @REFERRER nvarchar(500) IN, @DETAIL nvarchar(1000) IN, @RESULT int OUT, @COUNTS_AS_VISIT bit IN | 원문 조회 또는 감사 흐름에서 호출 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/logmanagement/repository/LogManagementMapper.kt#L92) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 번호, 발행일자, 사업자번호, 회사명, 요청자, 세금계산서수 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 서비스관리 > 전자세금계산서 > 지로 원본 다운로드의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 전체 선택 중 오류가 발생했습니다. 검색 후 다시 시도해 주세요. | 번호, 발행일자, 사업자번호, 회사명, 요청자, 세금계산서수 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 팝업이 차단되었습니다. 팝업 차단을 해제한 뒤 다시 시도해 주세요. | 번호, 발행일자, 사업자번호, 회사명, 요청자, 세금계산서수 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 원본 생성할 항목을 선택해 주세요. | 번호, 발행일자, 사업자번호, 회사명, 요청자, 세금계산서수 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 선택한 항목을 확인할 수 없습니다. 다시 선택해 주세요. | 번호, 발행일자, 사업자번호, 회사명, 요청자, 세금계산서수 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/TaxInvoiceRoutes.tsx#L49) · [GiroOriginalDownloadPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/GiroOriginalDownloadPage.tsx#L88) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/api/giroApi.ts#L111) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 1개 중 개발 메타데이터 확인 1개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-7b73dcf1239bb9d8) | Demo 메타데이터 4/4개 확인 · Dev와 계약 차이 2개 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

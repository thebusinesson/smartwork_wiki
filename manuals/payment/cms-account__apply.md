# [CMS·카드 자동결제와 예외] (EB13/EB14) CMS 계좌 관리 조회·관리 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

EB13 등록 화면을 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | CMS·카드 자동결제와 예외 |
| 언제 사용하는가 | EB13 등록 정보 조회, 계좌신청 대상 Excel 다운로드, EB13 등록 생성, EB13 오류 데이터 삭제 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 신청일자, 사업자번호, 회사명, 이체은행, 계좌번호, 예금주 |
| 업무 흐름 | EB13 등록 정보 조회, 계좌신청 대상 Excel 다운로드, EB13 등록 생성, EB13 오류 데이터 삭제 |
| 이 페이지의 역할 | 조회·관리 · EB13 등록 정보 조회 |
| 판단 결과·다음 업무 | [(EB13/EB14) CMS 계좌 관리](cms-account.md) |
| 다른 화면과의 구분 | 서비스 현황 > 입금관리 > (EB13/EB14) CMS 계좌 관리에서 사용하는 조회·관리 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 확인 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/AccountApplyPage.tsx#L381) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | EB13 등록 화면을 조회한다. |
| 메뉴·화면 경로 | 서비스 현황 > 입금관리 > (EB13/EB14) CMS 계좌 관리 · `/payment/cms-account/apply` |
| 화면 유형·담당 | 조회·관리 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [(EB13/EB14) CMS 계좌 관리](cms-account.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/payment/cms-account` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| EB13 등록 정보 조회 | `/payment/cms-account` `VIEW` | `Eb13RegistrationSearchRequest` `fromDate`, `toDate`, `appDate` |
| 계좌신청 대상 Excel 다운로드 | `/payment/cms-account` `EXCEL_DOWNLOAD` | `AccountApplyDownloadRequest` `autoTransferStartDate`, `autoTransferEndDate`, `receiptDate` |
| EB13 등록 생성 | `/payment/cms-account` `PROCESS` | `Eb13CreateRequest?` `fromDate`, `toDate`, `appDate` |
| EB13 오류 데이터 삭제 | `/payment/cms-account` `DELETE` | 추가 입력은 Controller 서명 참조 |
| EB13 작성 대상 계좌번호 원문 조회 | `/payment/cms-account` / `UNMASK` | `accountId`, `field` |

코드에서 확인한 버튼·작업명은 **검색**, **검색결과 엑셀다운로드**, **계좌신청생성**, **오류데이터삭제**, **확인**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [(EB13/EB14) CMS 계좌 관리](cms-account.md)에서 대상 또는 작업을 선택한다. `/payment/cms-account/apply`를 연다.
2. **자동이체 신청일**, **접수 신청일** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색**, **검색결과 엑셀다운로드**, **확인** 중 해당 버튼을 선택한다.
3. **EB13 등록 정보 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [(EB13/EB14) CMS 계좌 관리](cms-account.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 신청일자 | 출력 | 조회 응답 기준 | 화면 필드 `requestDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/AccountApplyPage.tsx#L89) |
| 사업자번호 | 출력 | 조회 응답 기준 | 화면 필드 `bizNo` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/AccountApplyPage.tsx#L90) |
| 회사명 | 출력 | 조회 응답 기준 | 화면 필드 `companyName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/AccountApplyPage.tsx#L91) |
| 이체은행 | 출력 | 조회 응답 기준 | 화면 필드 `bankName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/AccountApplyPage.tsx#L92) |
| 계좌번호 | 출력 | 조회 응답 기준 | 화면 필드 `accountNo` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/AccountApplyPage.tsx#L95) |
| 예금주 | 출력 | 조회 응답 기준 | 화면 필드 `depositor` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/AccountApplyPage.tsx#L108) |
| 처리구분 | 출력 | 조회 응답 기준 | 화면 필드 `processType` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/AccountApplyPage.tsx#L109) |
| 자동이체 신청일 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/AccountApplyPage.tsx#L56) |
| 접수 신청일 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/AccountApplyPage.tsx#L65) |
| 날짜 선택 | 입력 또는 선택 | API 기본값 null | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/AccountApplyPage.tsx#L70) |
| 파일생성일 | 출력 | 조회 응답 기준 | 화면 필드 `fileCreatedAt` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/AccountApplyPage.tsx#L82) |
| 접수신청일 | 출력 | 조회 응답 기준 | 화면 필드 `receiptRequestAt` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/AccountApplyPage.tsx#L83) |
| 파일명 | 출력 | 조회 응답 기준 | 화면 필드 `fileName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/AccountApplyPage.tsx#L84) |
| 전송여부 | 출력 | 조회 응답 기준 | 화면 필드 `sentYn` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/AccountApplyPage.tsx#L85) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| EB13 등록 정보 조회 | `GET /api/v1/payment/cms-account/eb13/registration` · `/payment/cms-account` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/cmsaccount/CmsAccountEb13Controller.kt#L152) | `Eb13RegistrationSearchRequest` `fromDate`, `toDate`, `appDate` → `success`, `data`, `error`, `fromDate`, `toDate`, `appDate`, `dnFailCount`, `fileCount`, `unSentFileCount`, `unSentFileName`, `generatedFiles`, `targets` | `SmartBill3.dbo.upCMS_Lst_EA13`, `SmartBill3.dbo.upCMS_Lst_AppAccount01`, `SmartBill3.dbo.upCMS_Lst_AppAccount02` |
| 계좌신청 대상 Excel 다운로드 | `GET /api/v1/payment/account-apply/download` · `/payment/cms-account` `EXCEL_DOWNLOAD` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/cmsaccount/CmsAccountApplyDownloadController.kt#L34) | `AccountApplyDownloadRequest` `autoTransferStartDate`, `autoTransferEndDate`, `receiptDate` → 파일 또는 오류 응답 | `SmartBill3.dbo.upCMS_Lst_EA13`, `SmartBill3.dbo.upCMS_Lst_AppAccount01`, `SmartBill3.dbo.upCMS_Lst_AppAccount02` |
| EB13 등록 생성 | `POST /api/v1/payment/cms-account/eb13/registration/create` · `/payment/cms-account` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/cmsaccount/CmsAccountEb13Controller.kt#L191) | `Eb13CreateRequest?` `fromDate`, `toDate`, `appDate` → `success`, `data`, `error` | `SmartBill3.dbo.upCMS_Lst_AppAccount01`, `SmartBill3.dbo.upCMS_Lst_AppAccount02`, `SmartBill3.dbo.upCMS_Sav_AppAccountMain01`, `SmartBill3.dbo.upCMS_Sav_AppAccountMain02`, `SmartBill3.dbo.upCMS_Sav_EA13File01` 외 2개 · 정의에서 확인한 쓰기 `SmartBill3.dbo.CMS_ACCOUNT_MAIN_TMP_CUB`, `SmartBill3.dbo.CMS_ACCOUNT_MAIN_CUB`, `SmartBill3.dbo.CMS_Withdrawal_Agreement`, `SmartBill3.dbo.CMS_EA13` 외 3개 · 코드 연계 트랜잭션 |
| EB13 오류 데이터 삭제 | `DELETE /api/v1/payment/cms-account/eb13/error-data` · `/payment/cms-account` `DELETE` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/cmsaccount/CmsAccountEb13Controller.kt#L234) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `message` | 코드 연계 트랜잭션 |
| EB13 작성 대상 계좌번호 원문 조회 | `POST /api/v1/payment/cms-account/eb13/registration/targets/{accountId}/sensitive-values/reveal` · `/payment/cms-account` / `UNMASK` · [화면 컴포넌트](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/AccountApplyPage.tsx#L100) · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/cmsaccount/CmsAccountEb13Controller.kt#L162) | `accountId`, `field` → 요청한 항목의 원문 응답 | 권한 검사 후 대상 값을 조회하고 감사 기록을 남긴다. |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `SmartBill3.dbo.upCMS_Lst_EA13` | @fromdate varchar(10), @todate varchar(10) | 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb13AccountMapper.kt#L49) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-a0539bac0c9dd014) |
| `SmartBill3.dbo.upCMS_Lst_AppAccount01` | @fromdate varchar(10), @todate varchar(10) | 정의 참조 `SB_BILL.dbo.BILL_COMMON_CODE`, `SmartBill3.dbo.CMS_ACCOUNT`, `SmartBill3.dbo.COMPANY` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb13AccountMapper.kt#L72) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-7c2cee1b46e9919c) |
| `SmartBill3.dbo.upCMS_Lst_AppAccount02` | @fromdate varchar(10), @todate varchar(10) | 정의 참조 `SB_BILL.dbo.BILL_COMMON_CODE`, `SmartBill3.dbo.CMS_ACCOUNT`, `SmartBill3.dbo.CMS_EA14_DETAIL`, `SmartBill3.dbo.COMPANY` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb13AccountMapper.kt#L91) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-30ec80228b5d8902) |
| `SmartBill3.dbo.upCMS_Sav_AppAccountMain01` | @FROMDATE varchar(10), @TODATE varchar(10) | 정의 참조 `SmartBill3.dbo.CMS_ACCOUNT_CUB`, `SmartBill3.dbo.CMS_ACCOUNT_MAIN_CUB`, `SmartBill3.dbo.CMS_ACCOUNT_MAIN_TMP_CUB`, `smartbill3.dbo.cms_identity_count`, `SmartBill3.dbo.CMS_IDENTITY_NEXT_VALUE` 외 2개 · 정적 쓰기 `SmartBill3.dbo.CMS_ACCOUNT_MAIN_TMP_CUB`, `SmartBill3.dbo.CMS_ACCOUNT_MAIN_CUB`, `SmartBill3.dbo.CMS_Withdrawal_Agreement` · 하위 호출 `SmartBill3.dbo.CMS_IDENTITY_NEXT_VALUE` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb13AccountMapper.kt#L173) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-72ca8d49fba6df63) |
| `SmartBill3.dbo.upCMS_Sav_AppAccountMain02` | @FROMDATE varchar(10), @TODATE varchar(10) | 정의 참조 `SmartBill3.dbo.CMS_ACCOUNT_CUB`, `SmartBill3.dbo.CMS_ACCOUNT_MAIN_CUB`, `SmartBill3.dbo.CMS_ACCOUNT_MAIN_TMP_CUB`, `SmartBill3.dbo.CMS_EA14_DETAIL` · 정적 쓰기 `SmartBill3.dbo.CMS_ACCOUNT_MAIN_TMP_CUB`, `SmartBill3.dbo.CMS_ACCOUNT_MAIN_CUB` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb13AccountMapper.kt#L177) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-1f2829c87cac53f4) |
| `SmartBill3.dbo.upCMS_Sav_EA13File01` | @APPDATE varchar(6), @EA13FILE_NAME varchar(8) | 정의 참조 `SmartBill3.dbo.CMS_ACCOUNT_MAIN`, `SmartBill3.dbo.CMS_ACCOUNT_MAIN_CUB`, `SmartBill3.dbo.CMS_EA13`, `SmartBill3.dbo.CMS_EA13_DETAIL_CUB`, `SmartBill3.dbo.fnFillDigit` · 정적 쓰기 `SmartBill3.dbo.CMS_EA13`, `SmartBill3.dbo.CMS_EA13_DETAIL_CUB` · 하위 호출 `SmartBill3.dbo.fnFillDigit` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb13AccountMapper.kt#L181) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-7da8ca9d6aceb63d) |
| `SmartBill3.dbo.UPCMS_SAV_EI13FILE01` | @APPDATE varchar(6), @EI13FILE_NAME varchar(8) | 정의 참조 `SmartBill3.dbo.CMS_ACCOUNT_CUB`, `SmartBill3.dbo.CMS_ACCOUNT_MAIN`, `SmartBill3.dbo.CMS_ACCOUNT_MAIN_CUB`, `SmartBill3.dbo.CMS_EA13`, `SmartBill3.dbo.CMS_EA13_DETAIL_CUB` 외 4개 · 정적 쓰기 `SmartBill3.dbo.CMS_EI13`, `SmartBill3.dbo.CMS_EI13_DETAIL_CUB` · 하위 호출 `SmartBill3.dbo.fnFillDigit` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb13AccountMapper.kt#L185) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-bb622e9d1a2faaf0) |
| `SmartBill3.dbo.CMS_ACCOUNT` | 개발 컬럼 메타데이터 확인 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb13AccountMapper.kt#L247) |
| `SmartBill3.dbo.COMPANY` | 개발 컬럼 메타데이터 확인 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb13AccountMapper.kt#L247) |
| `smartwork.dbo.usp_sw_log_access_event_insert` | @EVENT_TYPE varchar(30) IN, @STATUS varchar(20) IN, @USER_ID bigint IN, @MEMBER_ID nvarchar(50) IN, @USER_NAME nvarchar(100) IN, @DEPARTMENT_NAME nvarchar(100) IN, @PAGE_TITLE nvarchar(200) IN, @PATH nvarchar(500) IN, @MENU_PATH nvarchar(500) IN, @MENU_LABEL nvarchar(200) IN, @CATEGORY_NAME nvarchar(200) IN, @SUB_CATEGORY_NAME nvarchar(200) IN, @MENU_ORDER int IN, @IP_ADDRESS varchar(45) IN, @USER_AGENT nvarchar(1000) IN, @BROWSER varchar(100) IN, @OS varchar(100) IN, @REFERRER nvarchar(500) IN, @DETAIL nvarchar(1000) IN, @RESULT int OUT, @COUNTS_AS_VISIT bit IN | 원문 조회 또는 감사 흐름에서 호출 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/logmanagement/repository/LogManagementMapper.kt#L92) |

### 매퍼 호출 추가 확인

| DB 객체 | 호출 근거 | 개발 DB 확인 범위 |
| --- | --- | --- |
| [SmartBill3.dbo.upCMS_Sch_AppDNCount](../../references/all-pages-demo.md#object-c60b1001ebf2a0f5) | [getDnFailCount](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb13AccountMapper.kt#L56) | 개발 카탈로그 확인 |
| [SmartBill3.dbo.upCMS_Lst_AppAccountMain03](../../references/all-pages-demo.md#object-c28155ad8fff63ef) | [fetchEb13FileRecords](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb13AccountMapper.kt#L198) | 개발 카탈로그 확인 |
| [SmartBill3.dbo.UPCMS_LST_APPACCOUNTMAIN04](../../references/all-pages-demo.md#object-4c57e294527ae97d) | [fetchEi13FileRecords](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb13AccountMapper.kt#L210) | 개발 카탈로그 확인 |
| [SmartBill3.dbo.UPCMS_DEL_ERRORlIST_CMS_ACCOUNT_MAIN](../../references/all-pages-demo.md#object-747953402a4eea6d) | [deleteErrorData](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb13AccountMapper.kt#L218) | 개발 카탈로그 확인 |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 신청일자, 사업자번호, 회사명, 이체은행, 계좌번호, 예금주 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 서비스 현황 > 입금관리 > (EB13/EB14) CMS 계좌 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 엑셀 다운로드에 실패했습니다. | 신청일자, 사업자번호, 회사명, 이체은행, 계좌번호, 예금주 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 데이터가 없습니다. | 신청일자, 사업자번호, 회사명, 이체은행, 계좌번호, 예금주 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/PaymentRoutes.tsx#L77) · [AccountApplyPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/AccountApplyPage.tsx#L176) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/accountApplyApi.ts#L77) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/accountApplyApi.ts#L169) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/accountApplyApi.ts#L123) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/accountApplyApi.ts#L143) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 7개 중 개발 메타데이터 확인 7개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-ec36eedfe501adb5) | Demo 메타데이터 14/14개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

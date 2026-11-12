# [위택스 납부대상 등록·이력] Wetax 납부대상 관리 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

납부대상 자료를 파일 또는 클립보드로 등록하고 업로드 단위로 처리 이력을 조회한다. 검증 오류가 있으면 해당 등록 전체가 취소된다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 위택스 납부대상 등록·이력 |
| 언제 사용하는가 | Wetax 납부대상 업로드 이력 조회, Wetax 납부대상 엑셀 등록, Wetax 납부대상 클립보드 등록 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 엑셀 원본 또는 엑셀에서 복사한 21개 열, 업로드 번호와 건수 |
| 업무 흐름 | Wetax 납부대상 업로드 이력 조회, Wetax 납부대상 엑셀 등록, Wetax 납부대상 클립보드 등록 |
| 이 페이지의 역할 | 조회 · Wetax 납부대상 업로드 이력 조회 |
| 판단 결과·다음 업무 | [Wetax 납부대상 관리 업로드 이력](wetax-payment-targets__uploads__by-uploadSeq.md) |
| 다른 화면과의 구분 | 이 경로에서 볼 수 있는 조건·결과를 기준으로 사용한다. 독립 경로의 상세·등록은 관련 화면에 연결한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 납부대상 등록 | 자료를 새로 등록할 때 | 엑셀 원본 또는 클립보드 21열 | 검증 오류를 수정하고 이력에서 반영 결과를 확인한다. |
| 업로드 이력 | 이미 등록한 자료를 찾을 때 | 업로드 단위의 원본·등록자와 결과 | 로그보기에서 행별 처리를 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 납부대상 자료를 파일 또는 클립보드로 등록하고 업로드 단위로 처리 이력을 조회한다. 검증 오류가 있으면 해당 등록 전체가 취소된다. |
| 메뉴·화면 경로 | SB 서비스관리 > 홈택스 DTI 수집 > Wetax 납부대상 관리 · `/hometax-dti/wetax-payment-targets` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [Wetax 납부대상 관리 업로드 이력](wetax-payment-targets__uploads__by-uploadSeq.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/hometax-dti/wetax-payment-targets` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| Wetax 납부대상 업로드 이력 조회 | `/hometax-dti/wetax-payment-targets` `VIEW` | `page: Int` · `size: Int` |
| Wetax 납부대상 엑셀 등록 | `/hometax-dti/wetax-payment-targets` `EXCEL_UPLOAD` | `file: MultipartFile` |
| Wetax 납부대상 클립보드 등록 | `/hometax-dti/wetax-payment-targets` `PROCESS` | `WetaxClipboardUploadRequest` `rows` · 서버 필수 `rows` |
| Wetax 업로드 이력 등록자명 원문 조회 | `/hometax-dti/wetax-payment-targets` / `UNMASK` | `uploadSeq`, `field` |

코드에서 확인한 버튼·작업명은 **로그보기**, **파일 등록**, **클립보드 등록**, **취소**, **등록**, **확인**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **납부대상 등록**에서 .xlsx 원본을 **파일 첨부**에 선택하고 **파일 등록**을 누른다. 전자납부번호는 엑셀에서 텍스트 형식으로 유지한다.
2. 엑셀에서 직접 복사할 때는 21개 열을 복사하고 **클립보드 등록**을 연다. 미리보기에서 등록 대상 건수를 확인하고 등록을 진행한다.
3. 검증 오류가 있으면 오류가 난 행과 항목을 수정한 후 다시 등록한다. 오류 없이 끝난 경우 **업로드 이력**에서 새 등록을 찾아 **로그보기**로 상세를 연다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 허브명 | 출력 | 조회 응답 기준 | API 응답 `hubName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/WetaxPaymentTargetsPage.tsx#L121) |
| 사업자번호 | 출력 | 조회 응답 기준 | API 응답 `businessNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/WetaxPaymentTargetsPage.tsx#L123) |
| 등록건수 | 출력 | 조회 응답 기준 | API 응답 `totalCount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/WetaxPaymentTargetsPage.tsx#L127) |
| 등록자 | 출력 | 조회 응답 기준 | API 응답 `creatorName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/WetaxPaymentTargetsPage.tsx#L131) |
| 등록일 | 출력 | 조회 응답 기준 | API 응답 `createdAt` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/WetaxPaymentTargetsPage.tsx#L142) |
| 원본 파일 | 출력 | 조회 응답 기준 | API 응답 `originalFileName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/WetaxPaymentTargetsPage.tsx#L144) |
| 파일 첨부 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/WetaxPaymentTargetsPage.tsx#L172) |
| 행 | 출력 | 조회 응답 기준 | 화면 필드 `rowNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/wetax/WetaxClipboardUploadDialog.tsx#L39) |
| 전자납부번호 | 출력 | 조회 응답 기준 | 화면 필드 `electronicPaymentNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/wetax/WetaxValidationResultDialog.tsx#L25) |
| 오류 내용 | 출력 | 조회 응답 기준 | 화면 필드 `errors` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/wetax/WetaxValidationResultDialog.tsx#L32) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| Wetax 납부대상 업로드 이력 조회 | `GET /api/v1/sb-service/hometax-dti-installed/wetax-payment-targets/uploads` · `/hometax-dti/wetax-payment-targets` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/hometaxdti/wetax/WetaxPaymentTargetController.kt#L71) | `page: Int` · `size: Int` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `page`, `size`, `uploadSeq`, `hubName`, `businessNumber`, `totalCount` | `SB_SCRAPER.dbo.USP_WETAX_UPLOAD_HISTORY_LIST_GET` |
| Wetax 납부대상 엑셀 등록 | `POST /api/v1/sb-service/hometax-dti-installed/wetax-payment-targets/uploads` · `/hometax-dti/wetax-payment-targets` `EXCEL_UPLOAD` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/hometaxdti/wetax/WetaxPaymentTargetController.kt#L51) | `file: MultipartFile` → `success`, `data`, `error`, `uploadSeq`, `originalFileName`, `totalCount` | `SB_SCRAPER.dbo.USP_WETAX_UPLOAD_MST_INS`, `SB_SCRAPER.dbo.USP_WETAX_UPLOAD_DUP_SKIP`, `SB_SCRAPER.dbo.WETAX_UPLOAD_HISTORY` · 정의에서 확인한 쓰기 `SB_SCRAPER.dbo.WETAX_UPLOAD_HISTORY` · 코드 연계 트랜잭션 |
| Wetax 납부대상 클립보드 등록 | `POST /api/v1/sb-service/hometax-dti-installed/wetax-payment-targets/clipboard-uploads` · `/hometax-dti/wetax-payment-targets` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/hometaxdti/wetax/WetaxPaymentTargetController.kt#L61) | `WetaxClipboardUploadRequest` `rows` · 서버 필수 `rows` → `success`, `data`, `error`, `uploadSeq`, `originalFileName`, `totalCount` | `SB_SCRAPER.dbo.USP_WETAX_UPLOAD_MST_INS`, `SB_SCRAPER.dbo.USP_WETAX_UPLOAD_DUP_SKIP` · 정의에서 확인한 쓰기 `SB_SCRAPER.dbo.WETAX_UPLOAD_HISTORY` · 코드 연계 트랜잭션 |
| Wetax 업로드 이력 등록자명 원문 조회 | `POST /api/v1/sb-service/hometax-dti-installed/wetax-payment-targets/uploads/{uploadSeq}/sensitive-values/reveal` · `/hometax-dti/wetax-payment-targets` / `UNMASK` · [화면 컴포넌트](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/WetaxPaymentTargetsPage.tsx#L134) · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/hometaxdti/wetax/WetaxPaymentTargetController.kt#L81) | `uploadSeq`, `field` → 요청한 항목의 원문 응답 | 권한 검사 후 대상 값을 조회하고 감사 기록을 남긴다. |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `SB_SCRAPER.dbo.USP_WETAX_UPLOAD_HISTORY_LIST_GET` | @PAGE_NO int = 1, @PAGE_SIZE int = 10, @TOTAL_CNT int OUT | 정의 참조 `office.dbo.SAWON`, `SB_SCRAPER.dbo.USE_COMPANY_INFO`, `SB_SCRAPER.dbo.WETAX_UPLOAD_HISTORY` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/hometaxdti/wetax/repository/WetaxPaymentTargetMapper.kt#L37) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-436f30b9dd1077f1) |
| `SB_SCRAPER.dbo.USP_WETAX_UPLOAD_MST_INS` | @SB_KEY varchar(36), @COM_REGNO varchar(10), @UP_FILE_NAME varchar(100), @MGN_FILE_NAME varchar(200), @TOTAL_CNT int, @CUSER int, @NEW_UPLOAD_SEQ int OUT | 정의 참조 `SB_SCRAPER.dbo.WETAX_UPLOAD_HISTORY` · 정적 쓰기 `SB_SCRAPER.dbo.WETAX_UPLOAD_HISTORY` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/hometaxdti/wetax/repository/WetaxPaymentTargetMapper.kt#L56) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-4d2bd4c7403a0e1b) |
| `SB_SCRAPER.dbo.USP_WETAX_UPLOAD_DUP_SKIP` | @UPLOAD_SEQ int | 정의 참조 `SB_SCRAPER.dbo.WETAX_UPLOAD_DETAIL` · 쓰기 구문 존재 · 대상 별칭 또는 하위 정의 확인 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/hometaxdti/wetax/repository/WetaxPaymentTargetMapper.kt#L84) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-271e7a0c98f010de) |
| `SB_SCRAPER.dbo.WETAX_UPLOAD_HISTORY` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/hometaxdti/wetax/repository/WetaxPaymentTargetMapper.kt#L98) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-fdf9892814e03fe5) |
| `office.dbo.SAWON` | 개발 컬럼 메타데이터 확인 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/hometaxdti/wetax/repository/WetaxPaymentTargetMapper.kt#L109) |
| `smartwork.dbo.usp_sw_log_access_event_insert` | @EVENT_TYPE varchar(30) IN, @STATUS varchar(20) IN, @USER_ID bigint IN, @MEMBER_ID nvarchar(50) IN, @USER_NAME nvarchar(100) IN, @DEPARTMENT_NAME nvarchar(100) IN, @PAGE_TITLE nvarchar(200) IN, @PATH nvarchar(500) IN, @MENU_PATH nvarchar(500) IN, @MENU_LABEL nvarchar(200) IN, @CATEGORY_NAME nvarchar(200) IN, @SUB_CATEGORY_NAME nvarchar(200) IN, @MENU_ORDER int IN, @IP_ADDRESS varchar(45) IN, @USER_AGENT nvarchar(1000) IN, @BROWSER varchar(100) IN, @OS varchar(100) IN, @REFERRER nvarchar(500) IN, @DETAIL nvarchar(1000) IN, @RESULT int OUT, @COUNTS_AS_VISIT bit IN | 원문 조회 또는 감사 흐름에서 호출 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/logmanagement/repository/LogManagementMapper.kt#L92) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 엑셀 원본 또는 엑셀에서 복사한 21개 열, 업로드 번호와 건수 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 서비스관리 > 홈택스 DTI 수집 > Wetax 납부대상 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 업로드 이력이 없습니다. | 엑셀 원본 또는 엑셀에서 복사한 21개 열, 업로드 번호와 건수 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 붙여넣은 데이터가 없습니다. | 엑셀 원본 또는 엑셀에서 복사한 21개 열, 업로드 번호와 건수 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/HometaxDtiRoutes.tsx#L23) · [WetaxPaymentTargetsPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/WetaxPaymentTargetsPage.tsx#L28) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/wetax/api.ts#L13) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/wetax/api.ts#L23) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/wetax/api.ts#L30) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 4개 중 개발 메타데이터 확인 4개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-a20c2daea9cef4e2) | Demo 메타데이터 6/6개 확인 · 2026-11-11 |
| 화면 재현 | [로컬 Playwright 표본](../../evidence/browser/all-pages-sample-2026-11-11.json) | 진입 및 표시 확인 · 표시 납부대상 등록, 업로드 이력 · 2026-11-11 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

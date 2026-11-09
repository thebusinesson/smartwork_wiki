# [SB 운영관리] 전체 오류 조회/처리 (조회·관리) 관리자 매뉴얼

작성 기준: `dc216b313` · 확인일 2026-11-09 · 조사 상태 **검토 대기**. 코드·개발 DB 정의 확인. 브라우저: **화면 대조**; 저장·발송 등 업무 실행 결과는 미검증이다.

## 1) 화면 기본 정보

| 항목 | 작성 내용 |
|---|---|
| 업무 도메인·목적 | 접수된 서비스 오류를 등록하고 처리 상태·처리내역·참조 정보를 관리한다. |
| 메뉴·화면 경로 | SB 운영관리 > 오류 관리 > 전체 오류 조회/처리; `/error-management/error-reports`; 메뉴 또는 관련 화면에서 진입한다. |
| 화면 유형·담당 | 조회·관리; WBS 작업자 유지윤. 업무·기술 담당 팀명은 원문에 없어 배포 전 해당 도메인 담당자가 확정한다. |
| 관련 화면 | [등록](error-reports__new.md); [상세](error-reports__by-id.md); [오류 처리내역 등록](error-reports__by-id__process.md) |

WBS 근거: No. 150, 151, 152, 153, 154 (사용자가 제공한 텍스트 행 189, 190, 191, 192, 193). API 개발/화면 개발의 중복 행은 같은 화면으로 통합했다.

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
|---|---|---|
| 화면 진입·조회 | `/error-management/error-reports` 메뉴 접근·하위 경로 작업 권한. 조회 API는 VIEW, 등록/수정 경로는 PROCESS 등 아래 서버 액션과 라우트 가드를 함께 적용한다. | 로그인된 관리자 계정; 아래 검색·입력 항목을 준비한다. |
| 다운로드 | `/error-management/error-reports`; 엑셀 download 화면 게이트. 다운로드/업로드 API의 서버 권한과 사유 입력을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |

서버가 최종 권한을 검사한다. 버튼 모양(kind)으로 권한을 추정하지 않는다. 특히 등록·수정이 PROCESS를 사용하는 API와 EXECUTE·UNMASK·EXCEL_DOWNLOAD는 서로 구분한다.

## 3) 화면 사용 절차

**검증 시 화면 버튼**: 검색, 초기화, 다운로드. 화면 상태·대상에 따라 달라지며 아래 작업 절차와 권한 조건을 함께 확인한다.

1. `SB 운영관리 > 오류 관리 > 전체 오류 조회/처리` 메뉴를 연다. 경로 변수는 주소에서 임의로 바꾸지 않고 이전 화면이 전달한 식별자를 사용한다.
2. 현재 검색 조건과 아래 기본값을 확인한다. **접수일자, 진행상태, 문의 업체, 허브업체명, 연동형태, 오류 서비스, 오류 종류, 오류코드** 항목에 필요한 값을 입력하고 **검색**을 누른다.
3. 결과 행에서 업무 대상을 선택하여 관련 상세 화면으로 이동한다. 페이지 이동·검색 조건 변경 후에는 현재 조건과 조회 대상을 다시 확인한다.

**이 화면에서 유의할 업무 규칙**: 목록에서 접수일자·진행상태·문의 업체·허브업체·오류 서비스/종류/코드로 검색한다. 오류 접수/등록에서 문의업체와 담당자를 선택하고 문의 내용을 입력한다. 상세에서는 업체 접수내역과 처리내역을 확인하고 별도 처리 등록 화면에서 상태와 처리 내용을 저장한다. 미처리 오류/상태불일치 팝업은 같은 문서에서 다룬다.

**반출**: 적용된 검색 조건과 반출 범위를 확인한 후 다운로드한다. 사유 입력창이 표시되면 업무 사유를 입력한다. 사유 등록 실패·파일 오류는 성공으로 간주하지 않고 다운로드 결과를 확인한다.

## 4) 입력·표시 데이터

**검증 시 표시된 날짜 필터**: 시작일 `2026-03-01`, 종료일 `2026-11-09`. 검증 날짜·조건 복원에 따른 표시값이며 모든 실행의 고정 기본값을 뜻하지 않는다.

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
|---|---|---|---|
| 접수일자 | 입력·선택(조건부 검증 별도) | 화면 타입 toggleableDateRange; 초기값 isAllDates=꺼짐; dateRange={getTodayDateRange()} | `receptionDate`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/error/ErrorListPage.tsx#L71) |
| 진행상태 | 입력·선택(조건부 검증 별도) | 화면 타입 radio; API 타입 String?; 기본 null; 선택: 전체=, 접수=접수, 처리중=처리중, 타팀요청=타팀요청, 처리완료=처리완료; 초기값 빈값 | `status`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/error/ErrorListPage.tsx#L81) |
| 문의 업체 | 입력·선택(조건부 검증 별도) | 화면 타입 selectWithInput; 선택: 전체=all, 사업자번호=사업자번호, 회사명=회사명; 초기값 selectValue=사업자번호; inputValue=빈값 | `companyCondition`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/error/ErrorListPage.tsx#L97) |
| 허브업체명 | 입력·필수 | 화면 타입 checkboxWithInput; 선택: 전체=all; 초기값 checked=all; inputValue=빈값 | `hubCompanyNames`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/error/ErrorListPage.tsx#L118) |
| 연동형태 | 입력·선택(조건부 검증 별도) | 화면 타입 checkbox; API 타입 List<String>?; 기본 null; 초기값 {...CONNECTION_OPTIONS} | `connectionTypes`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/error/ErrorListPage.tsx#L130) |
| 오류 서비스 | 입력·선택(조건부 검증 별도) | 화면 타입 checkbox; API 타입 List<String>?; 기본 null; 초기값 {...SERVICE_OPTIONS} | `serviceTypes`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/error/ErrorListPage.tsx#L140) |
| 오류 종류 | 입력·선택(조건부 검증 별도) | 화면 타입 checkbox; API 타입 List<String>?; 기본 null; 초기값 {...ERROR_TYPE_OPTIONS} | `errorTypes`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/error/ErrorListPage.tsx#L150) |
| 오류코드 | 입력·필수 | 화면 타입 checkboxWithInput; 선택: 전체=all; 초기값 checked=all; inputValue=빈값 | `errorCodes`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/error/ErrorListPage.tsx#L160) |
| 오류번호 | 출력 | API 타입 String | `errorNumber`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/error/errorTableHeaders.tsx#L17) |
| 오류접수 일시 | 출력 | API 타입 String? | `errorDate`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/error/errorTableHeaders.tsx#L25) |
| 문의 업체 | 출력 | API 타입 String?; 기본 null | `companyName`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/error/errorTableHeaders.tsx#L32) |
| 제목 | 출력 | API 타입 String | `inquiryTitle`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/error/errorTableHeaders.tsx#L36) |
| 상태 | 출력 | API 타입 String?; 기본 null; 초기값 빈값 | `status`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/error/errorTableHeaders.tsx#L40) |
| 처리자 | 출력 | API 타입 String | `processor`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/error/errorTableHeaders.tsx#L46) |
| 경과시간 | 출력 | API 타입 String | `elapsedTime`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/error/errorTableHeaders.tsx#L65) |
| 처리시간 | 출력 | API 타입 String | `processingTime`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/error/errorTableHeaders.tsx#L72) |
| SEQ | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `seq`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/error/components/DtiMismatchAlarmDialog.tsx#L20) |
| 참조번호 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `referenceNumber`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/error/components/DtiMismatchAlarmDialog.tsx#L21) |
| 승인번호 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `approvalNumber`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/error/components/DtiMismatchAlarmDialog.tsx#L22) |
| 공급자 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `supplierName`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/error/components/DtiMismatchAlarmDialog.tsx#L23) |
| 모니터 시간 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `monitoredAt`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/error/components/DtiMismatchAlarmDialog.tsx#L24) |

**복합 검색·폼의 초기 상태**

| 초기값 근거 | 기본 상태 |
|---|---|
| [getDefaultFilterValues](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/error/ErrorListPage.tsx#L197) | receptionDate=isAllDates=꺼짐; dateRange={getTodayDateRange()}; status=빈값; companyCondition=selectValue=사업자번호; inputValue=빈값; hubCompanyNames=checked=all; inputValue=빈값; connectionTypes={...CONNECTION_OPTIONS}; serviceTypes={...SERVICE_OPTIONS}; errorTypes={...ERROR_TYPE_OPTIONS}; errorCodes=checked=all; inputValue=빈값 |

화면 필드 키와 API 필드명이 다른 경우 변환은 Hook/API의 검색·저장 매핑에서 수행된다. 요청·응답 필드와 DB 컬럼 매핑은 아래 API 계약 및 DB 객체 계약에 연결했다.

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
|---|---|---|---|
| 오류 목록 조회 | [GET /api/v1/tax-operations/error-reports/list](../../references/api-contracts.md#api176); `/error-management/error-reports` / `VIEW` | `startDate, endDate, status, companyName, businessNumber, hubCompanyName, connectionTypes, serviceTypes, errorTypes, errorCode, page, size` → `data, pagination, statusCounts, id, errorNumber, companyName, inquiryTitle, status, processor, elapsedTime, processingTime, errorDate, hubCompanyName, attachmentFileName, endDate, ` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 오류 목록 다운로드 | [GET /api/v1/tax-operations/error-reports/download](../../references/api-contracts.md#api173); `/error-management/error-reports` / `EXCEL_DOWNLOAD` | `startDate, endDate, status, companyName, businessNumber, hubCompanyName, connectionTypes, serviceTypes, errorTypes, errorCode, page, size` → `응답 DTO·파일/처리 결과 계약 참조` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 실시간 상태불일치 모니터링 목록 | [GET /api/v1/tax-operations/error-reports/dti-mismatch-alarm](../../references/api-contracts.md#api174); `/error-management/error-reports` / `VIEW` | `경로·쿼리·본문 계약 참조` → `응답 DTO·파일/처리 결과 계약 참조` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 미처리 오류 조회 목록 | [GET /api/v1/tax-operations/error-reports/unresolved](../../references/api-contracts.md#api179); `/error-management/error-reports` / `VIEW` | `경로·쿼리·본문 계약 참조` → `응답 DTO·파일/처리 결과 계약 참조` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 미처리 오류 목록 다운로드 | [GET /api/v1/tax-operations/error-reports/unresolved/download](../../references/api-contracts.md#api180); `/error-management/error-reports` / `EXCEL_DOWNLOAD` | `경로·쿼리·본문 계약 참조` → `응답 DTO·파일/처리 결과 계약 참조` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 오류 처리자 원문 조회 | [POST /api/v1/tax-operations/error-reports/{id}/sensitive-values/reveal](../../references/api-contracts.md#api252); `/error-management/error-reports` / `UNMASK` | `field` → `field, value` | 쓰기 대상 smartwork.dbo.sw_log_access_event |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
|---|---|---|---|
| [smartwork.dbo.usp_error_receipt_list_all](../../references/database-contracts.md#db288) | `@from_date varchar(10) IN, @to_date varchar(23) IN, @status varchar(10) IN, @company_name varchar(50) IN, @bns_name varchar(50) IN, @routing_csv varchar(100) IN, @svc_concat varchar(20) IN, @type_concat varchar(20) IN, @err_code varchar(20) IN, @business_number varchar(13) IN` | 확정한 테이블 쓰기 없음. 참조: office.dbo.error_deal, office.dbo.error_managemennt, office.dbo.sawon | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.usp_error_receipt_download](../../references/database-contracts.md#db287) | `@from_date varchar(10) IN, @to_date varchar(23) IN, @status varchar(10) IN, @company_name varchar(50) IN, @bns_name varchar(50) IN, @routing_csv varchar(100) IN, @svc_concat varchar(20) IN, @type_concat varchar(20) IN, @err_code varchar(20) IN, @business_number varchar(13) IN` | 확정한 테이블 쓰기 없음. 참조: office.dbo.error_deal, office.dbo.error_managemennt, office.dbo.function_code, office.dbo.sawon | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Office.dbo.upGW_LstDTIMismatch](../../references/database-contracts.md#db023) | IN 파라미터 없음 | 확정한 테이블 쓰기 없음. 참조: office.dbo.dti_mismatch_alarm, sb_dti.dbo.dti_header_cub, sb_dti.dbo.dti_header_cub_2023_07, sb_dti.dbo.dti_header_cub_part, sb_dti.dbo.dti_header_cub_prev_buffer | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.usp_sw_log_access_event_insert](../../references/database-contracts.md#db294) | `@EVENT_TYPE varchar(30) IN, @STATUS varchar(20) IN, @USER_ID bigint IN, @MEMBER_ID nvarchar(50) IN, @USER_NAME nvarchar(100) IN, @DEPARTMENT_NAME nvarchar(100) IN, @PAGE_TITLE nvarchar(200) IN, @PATH nvarchar(500) IN, @MENU_PATH nvarchar(500) IN, @MENU_LABEL nvarchar(200) IN, @CATEGORY_NAME nvarchar(200) IN, @SUB_CATEGORY_NAME nvarchar(200) IN, @MENU_ORDER int IN, @IP_ADDRESS varchar(45) IN, @USER_AGENT nvarchar(1000) IN, @BROWSER varchar(100) IN, @OS varchar(100) IN, @REFERRER nvarchar(500) IN, @DETAIL nvarchar(1000) IN, @RESULT int OUT, @COUNTS_AS_VISIT bit IN` | 쓰기: smartwork.dbo.sw_log_access_event. 참조: smartwork.dbo.sw_log_access_event | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.usp_error_receipt_detail](../../references/database-contracts.md#db286) | `@err_idx int IN` | 확정한 테이블 쓰기 없음. 참조: office.dbo.dept, office.dbo.error_managemennt, office.dbo.function_code, office.dbo.sawon | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| 파일: storage.attachments | error-receipt 하위 첨부파일 및 저장 파일 식별자 | 오류 접수의 첨부 저장·다운로드. 기존 경로 prefix 호환과 실제 파일 존재·접근 권한 확인 | [ErrorReceiptAttachmentService.kt](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/error/service/ErrorReceiptAttachmentService.kt) |

위 DB 계약 링크에는 실제 파라미터 타입·기본값·IN/OUT, Mapper 결과 컬럼, RETURN 바인딩, 참조 테이블·하위 프로시저·정의 필터/정렬을 기록했다. DTO·Service·Repository·Mapper의 상세 호출 경로는 각 API 계약에서 확인한다.

**민감정보**: 기본 응답의 마스킹 값을 유지한다. 원문은 전용 reveal API와 UNMASK 등 추가 권한·사유·감사 로그를 확인한 뒤 조회한다. 화면·캡처·문의 문서에 원문을 남기지 않는다.

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
|---|---|---|
| 검색 결과가 없습니다. | [문구·처리 코드](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/error/ErrorListPage.tsx#L383); 현재 조건·대상·권한 확인 | 검색·조회 오류면 조건을 확인 후 재조회. 변경·발송 결과가 불명확하면 처리 여부와 이력을 확인한 뒤 재시도 여부를 판단한다. |
| 상태불일치 세금계산서가 없습니다. | [문구·처리 코드](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/error/components/DtiMismatchAlarmDialog.tsx#L78); 현재 조건·대상·권한 확인 | 검색·조회 오류면 조건을 확인 후 재조회. 변경·발송 결과가 불명확하면 처리 여부와 이력을 확인한 뒤 재시도 여부를 판단한다. |
| 미처리 오류가 없습니다. | [문구·처리 코드](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/error/components/UnresolvedErrorDialog.tsx#L125); 현재 조건·대상·권한 확인 | 검색·조회 오류면 조건을 확인 후 재조회. 변경·발송 결과가 불명확하면 처리 여부와 이력을 확인한 뒤 재시도 여부를 판단한다. |
| 결과가 없거나 기대 건수와 다름 | 적용된 검색 기준·기간·탭·대상 상태·서버 필터·페이징·목록/다운로드 조건 | 조건을 다시 확인하고 조회한다. 지속되면 경로·작업 시각·마스킹한 식별자·필터를 업무/기술 담당에게 전달한다. |
| 메뉴·버튼 미표시 또는 접근 거부 | 사용자 그룹의 메뉴 접근·VIEW 및 API별 PROCESS/EXECUTE/DELETE/EXCEL_DOWNLOAD/UNMASK 등 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. 프런트 버튼 표시만으로 서버 권한을 판단하지 않는다. |
| 저장·삭제·외부 실행의 결과가 불명확 | 대상 현재 상태·중복 요청·감사 이력·API 오류·파일/외부 소비 로그 | 기존 반영 여부를 먼저 조회한다. 중복 발송·초기화·금액 처리를 피하기 위해 기술 담당 확인 후 재시도한다. |

## 7) 검증·출처

**브라우저 검증(2026-11-09)**: 화면 대조. [경로별 결과와 제한](../../references/browser-verification.md#page055). 역할별 권한 거부·저장 성공·파일 반출·외부 연계 완료는 이 결과로 보장하지 않는다.

| 검증 항목 | 근거·환경 | 상태·확인일 |
|---|---|---|
| 대상 선정 | 사용자가 WBS 탭 내용으로 제공한 텍스트의 No. 150, 151, 152, 153, 154; [선정 태스크](../../inventory/wbs-tasks.csv) | 제공 텍스트 확인 2026-11-09. 원본 Excel의 탭/병합 셀을 독립 재열람한 것은 아님. |
| 메뉴·라우트·화면 | [menuConfig.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts); [OperationsRoutes.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/OperationsRoutes.tsx); [ErrorListPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/error/ErrorListPage.tsx) | 코드 확인 2026-11-09, 기준 dc216b313 |
| 기능·권한·API | 이 문서의 API 계약 링크 및 연결 Hook/API·Controller·DTO·Service·Repository·Mapper | 코드 확인 2026-11-09. 조회 요청·화면 대조 범위는 아래 브라우저 근거 참조. 권한 계정별 허용·거부 및 변경 요청 실행은 미확인. |
| DB 정의 | [개발 DB 계약](../../references/database-contracts.md), 이 문서의 연결 객체 | 개발 DB 정의 확인 2026-11-09. 동적 SQL·CLR 내부·정의 미공개 참조의 미확정 범위는 객체별 기록; 후속 확인 DB 담당. |
| 브라우저 화면·배포 환경 | 로컬 인증 계정·Playwright CLI; [화면별 검증표](../../references/browser-verification.md#page055) | 화면 대조, 2026-11-09. 배포본·타 역할·업무 변경 결과는 미확인. |
| 업무 프로시저·쓰기·외부 결과 | 격리된 검증 환경·테스트 데이터의 실행 결과 | 미확인: 명시적인 저장·삭제·발송·초기화 요청은 실행하지 않음. 브라우저 GET의 업무 조회 프로시저·조회수·감사 기록은 별도 영향으로 구분. 격리 환경에서 기술 담당 확인. |

코드 확인과 DB 정의 확인은 실행 성공·업무 승인·다른 환경 적용을 보장하지 않는다. 업무·기술 담당 검토 후 조사 목록의 상태를 완료로 변경한다.

브라우저 직접 근거: [settled-static-recheck](../../evidence/browser/static-stable.json). 경로·고정 버튼명·입력 속성·표 머리글·API 상태를 보관했고 실제 데이터 값·식별자·인증정보는 제외했다.

# [SB 운영관리] 오류 접수/등록 (등록) 관리자 매뉴얼

작성 기준: `dc216b313` · 확인일 2026-11-09 · 조사 상태 **검토 대기**. 코드·개발 DB 정의 확인. 브라우저: **화면 대조**; 저장·발송 등 업무 실행 결과는 미검증이다.

## 1) 화면 기본 정보

### 도메인 이해

문의 업체와 증상·문서 제목·문의 내용을 입력해 새로운 오류 접수 건을 만든다.

| 구분 | 설명 |
|---|---|
| 업무 영역 | 서비스 오류 접수·처리 > 오류 접수/등록 등록 |
| 언제 사용하는가 | 아직 접수 번호가 없는 서비스 문제를 운영 업무로 등록해야 할 때 |
| 주요 대상·데이터 | 업체·제목·문의내용·분류·처리요청팀 등 접수 입력이 대상이다. 화면의 메일요청·추가 입력 일부는 API 변환 후 실제 요청에 포함되는지 별도로 확인해야 한다. |
| 업무 흐름 | 문의 업체 확인 → 증상·분류·내용 입력 → 필수값·요청 조건 확인 → 등록 결과 조회 |
| 이 페이지의 역할 | 개별 오류 접수 건 중 **오류 접수/등록 등록** 단계. 문의 업체와 증상·문서 제목·문의 내용을 입력해 새로운 오류 접수 건을 만든다. |
| 판단 결과·다음 업무 | 새 오류 번호·상태를 확인한 뒤 전체 오류 목록에서 경과를 추적한다. |
| 다른 화면과의 구분 | 새 오류 접수와 기존 오류 처리기록은 다른 단계다. 메일요청 체크값(emailRequest/emailRequestText)은 현재 createErrorReport의 POST 본문·서버 등록 DTO에 없으므로 이 체크에 따른 메일 요청 전달·발송을 확정하지 않는다. |

설명 근거: [ErrorReportRegisterPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/error/ErrorReportRegisterPage.tsx), 이 문서 4·5·7번의 항목·API·업무 규칙. [상위 업무 영역](../../references/domain-overview.md#error)은 공통 배경이며 현재 화면의 데이터·동작은 위 설명을 따른다. 설명 수정일 **2026-11-10**; 새 업무 실행 검증을 수행한 것은 아니다.

### 화면 정보

| 항목 | 작성 내용 |
|---|---|
| 업무 도메인·목적 | 문의 업체와 증상·문서 제목·문의 내용을 입력해 새로운 오류 접수 건을 만든다. |
| 메뉴·화면 경로 | SB 운영관리 > 오류 관리 > 오류 접수/등록; `/error-management/error-reports/new`; 메뉴 또는 관련 화면에서 진입한다. |
| 화면 유형·담당 | 등록; WBS 작업자 유지윤. 업무·기술 담당 팀명은 원문에 없어 배포 전 해당 도메인 담당자가 확정한다. |
| 관련 화면 | [조회·관리](error-reports.md); [상세](error-reports__by-id.md); [오류 처리내역 등록](error-reports__by-id__process.md) |

WBS 근거: No. 150, 151, 152, 153, 154 (사용자가 제공한 텍스트 행 189, 190, 191, 192, 193). API 개발/화면 개발의 중복 행은 같은 화면으로 통합했다.

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
|---|---|---|
| 화면 진입·조회 | `/error-management/error-reports/new` 메뉴 접근·하위 경로 작업 권한. 조회 API는 VIEW, 등록/수정 경로는 PROCESS 등 아래 서버 액션과 라우트 가드를 함께 적용한다. | 로그인된 관리자 계정; 아래 검색·입력 항목을 준비한다. |

서버가 최종 권한을 검사한다. 버튼 모양(kind)으로 권한을 추정하지 않는다. 특히 등록·수정이 PROCESS를 사용하는 API와 EXECUTE·UNMASK·EXCEL_DOWNLOAD는 서로 구분한다.

## 3) 화면 사용 절차

**검증 시 화면 버튼**: 검색, 초기화, 등록. 화면 상태·대상에 따라 달라지며 아래 작업 절차와 권한 조건을 함께 확인한다.

1. 관련 화면에서 대상 또는 작업을 선택하여 `/error-management/error-reports/new`로 이동한다. 경로 변수는 주소에서 임의로 바꾸지 않고 이전 화면이 전달한 식별자를 사용한다.
2. **업체 조건, 업체 조건**의 입력값을 확인한다. 신규 값을 입력한다. 필수값과 형식 오류가 표시되면 해당 항목을 수정한다.
3. 화면의 등록·처리 버튼을 누르고 확인창이 있으면 대상·작업을 확인한다. 첨부가 있으면 기존 파일의 유지·삭제·교체 선택을 함께 확인한다.
4. 처리 결과 메시지를 확인한 뒤 목록 또는 상세에서 결과를 다시 조회한다. 오류가 나면 아래 예외 대응과 API 오류를 확인하고 중복 저장 전에 기존 처리 여부를 확인한다.

**이 화면에서 유의할 업무 규칙**: 목록에서 접수일자·진행상태·문의 업체·허브업체·오류 서비스/종류/코드로 검색한다. 오류 접수/등록에서 문의업체와 담당자를 선택하고 문의 내용을 입력한다. 상세에서는 업체 접수내역과 처리내역을 확인하고 별도 처리 등록 화면에서 상태와 처리 내용을 저장한다. 미처리 오류/상태불일치 팝업은 같은 문서에서 다룬다.

공통 폼이 등록·수정·상세 입력값 조회 함수를 함께 포함할 수 있다. 아래 API 표에 공통 구현의 다른 모드가 표시되어도 현재 경로의 작업으로 모두 실행하는 것은 아니다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
|---|---|---|---|
| 업체 조건 | 입력·선택(조건부 검증 별도) | 화면 타입 selectWithInput; 최대 100자; 선택: 사업자번호=businessNumber, 회사명=companyName, 담당자명=managerName, 스마트빌ID=smartbillId | `companySearch`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/error/ErrorReportRegisterPage.tsx#L187) |
| 업체 조건 | 입력·선택(조건부 검증 별도) | 화면 타입 checkbox; 선택: 업체정보 직접 입력=true | `directInput`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/error/ErrorReportRegisterPage.tsx#L187) |
| 사용 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `sms-used`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/error/ErrorReportRegisterPage.tsx#L570) |
| 미사용 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `sms-unused`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/error/ErrorReportRegisterPage.tsx#L576) |
| 메일요청 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `emailRequest`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/error/ErrorReportRegisterPage.tsx#L608) |

입력 검증 근거: [ErrorReportRegisterPage.schema.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/operations/error/ErrorReportRegisterPage.schema.ts). 프런트 검증과 서버 DTO 제약이 다르면 서버 검증이 최종 기준이다.

화면 필드 키와 API 필드명이 다른 경우 변환은 Hook/API의 검색·저장 매핑에서 수행된다. 요청·응답 필드와 DB 컬럼 매핑은 아래 API 계약 및 DB 객체 계약에 연결했다.

## 5) API·DB·연계

**등록 계약 차이(코드 확인 2026-11-10)**: 화면은 `emailRequest`, `emailRequestText`를 폼 객체에 모으지만 `errorReportApi.createErrorReport`는 이 값을 POST body에 넣지 않고 `ErrorReceiptCreateRequest`에도 해당 필드가 없다. UI 주석의 메일 안내를 실제 전달·발송 구현으로 간주하지 않는다. 접수 저장 성공과 메일요청은 구분하며 FE/API 담당의 구현 확인 대상이다.

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
|---|---|---|---|
| 오류 단건 조회 | [GET /api/v1/tax-operations/error-reports/{id}](../../references/api-contracts.md#api182); `/error-management/error-reports` / `VIEW` | `경로·쿼리·본문 계약 참조` → `id, errorNumber, status, title, content, errorDate, endDate, totalProcessingTime, registrant, processor, processingTeam, processingTeamNo, smsReceive, businessNumber, companyName, ` | 기존 항목 입력값 조회 공통 구현; 신규 진입에서는 대상 없음. Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 오류 접수 등록 | [POST /api/v1/tax-operations/error-reports](../../references/api-contracts.md#api250); `/error-management/error-reports/new` / `PROCESS` | `title, content, errorCode, errorType, routingType, businessNumber, companyName, managerName, contactNumber, processorSwNo, processingTeamNo, smsReceive, callNo, attachmentFileName` → `errorNumber` | 쓰기 대상 office.dbo.error_managemennt |
| 오류 접수 수정 | [PUT /api/v1/tax-operations/error-reports/{id}](../../references/api-contracts.md#api275); `/error-management/error-reports` / `PROCESS` | `status, processingTeamNo, hubCompanyId, hubCompanyName, routingType, errorCode, errorType, serviceType, errorDetailCode, errorEtc` → `응답 DTO·파일/처리 결과 계약 참조` | 공통 구현의 기존 항목 작업; 신규 저장에서 실행하지 않음. 쓰기 대상 office.dbo.error_managemennt |
| 사용자 목록 | [GET /api/v1/tax-operations/error-reports/users](../../references/api-contracts.md#api181); `/error-management/error-reports/new` / `VIEW` | `경로·쿼리·본문 계약 참조` → `응답 DTO·파일/처리 결과 계약 참조` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 처리요청팀 목록 | [GET /api/v1/tax-operations/error-reports/teams](../../references/api-contracts.md#api178); `/error-management/error-reports/new` / `VIEW` | `경로·쿼리·본문 계약 참조` → `응답 DTO·파일/처리 결과 계약 참조` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 첨부파일 업로드 | [POST /api/v1/tax-operations/error-reports/attachments](../../references/api-contracts.md#api251); `/error-management/error-reports/new` / `PROCESS` | `경로·쿼리·본문 계약 참조` → `fileName, originalFileName, fileSize, message` | 쓰기 대상 smartwork.dbo.error_receipt_attachment_meta |
| 다음 오류번호 미리보기 | [GET /api/v1/tax-operations/error-reports/next-error-number](../../references/api-contracts.md#api177); `/error-management/error-reports/new` / `VIEW` | `경로·쿼리·본문 계약 참조` → `errorNumber` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 현재 사용자 정보 | [GET /api/v1/tax-operations/error-reports/current-user](../../references/api-contracts.md#api170); `/error-management/error-reports/new` / `VIEW` | `경로·쿼리·본문 계약 참조` → `id, name, team` | 파일·외부 연계·공통 저장소/검사 호출: 상세 계약 참조 |
| 고객 다건 검색 | [GET /api/v1/tax-operations/error-reports/customers/search](../../references/api-contracts.md#api171); `/error-management/error-reports/new` / `VIEW` | `경로·쿼리·본문 계약 참조` → `응답 DTO·파일/처리 결과 계약 참조` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
|---|---|---|---|
| [smartwork.dbo.error_receipt_attachment_meta](../../references/database-contracts.md#db271) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 쓰기: smartwork.dbo.error_receipt_attachment_meta. 참조: smartwork.dbo.error_receipt_attachment_meta | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.usp_error_receipt_detail](../../references/database-contracts.md#db286) | `@err_idx int IN` | 확정한 테이블 쓰기 없음. 참조: office.dbo.dept, office.dbo.error_managemennt, office.dbo.function_code, office.dbo.sawon | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Office.dbo.upGW_CntErrCode](../../references/database-contracts.md#db017) | `@today varchar(10) IN` | 확정한 테이블 쓰기 없음. 참조: office.dbo.error_managemennt | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Office.dbo.upGW_SaveError](../../references/database-contracts.md#db032) | `@err_num varchar(20) IN, @write_sw_no int IN, @sw_no int IN, @err_com_regno varchar(13) IN, @err_com_name varchar(50) IN, @err_com_admin varchar(20) IN, @err_com_phone varchar(15) IN, @err_title varchar(256) IN, @err_content text IN, @err_file varchar(50) IN, @err_type char(1) IN, @routing_type varchar(10) IN, @err_code varchar(20) IN, @err_status char(1) IN, @req_team int IN, @sms_chk int IN, @call_no int IN` | 쓰기: office.dbo.error_managemennt. 참조: office.dbo.error_managemennt | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Office.dbo.upGW_ModError](../../references/database-contracts.md#db028) | `@err_idx int IN, @err_status char(1) IN, @req_team int IN, @err_bns_name varchar(50) IN, @err_bns_id int IN, @routing_type varchar(10) IN, @err_code varchar(20) IN, @err_type char(1) IN, @svc_type char(1) IN, @err_detail_code varchar(10) IN, @error_etc varchar(500) IN` | 쓰기: office.dbo.error_managemennt. 참조: office.dbo.error_managemennt | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Office.dbo.sawon](../../references/database-contracts.md#db009) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: office.dbo.sawon | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Office.dbo.dept_detail](../../references/database-contracts.md#db006) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: office.dbo.dept_detail | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Office.dbo.dept](../../references/database-contracts.md#db005) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: office.dbo.dept | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Office.dbo.upGW_ErrREqTeamGroupList](../../references/database-contracts.md#db020) | IN 파라미터 없음 | 확정한 테이블 쓰기 없음. 참조: office.dbo.dept, office.dbo.function_code | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SmartBill3.dbo.MEMBER](../../references/database-contracts.md#db203) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.member | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SmartBill3.dbo.COMPANY](../../references/database-contracts.md#db197) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.company | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DTI.dbo.COMPANY_LINK_OUT](../../references/database-contracts.md#db136) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: sb_dti.dbo.company_link_out | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Office.dbo.MNG_HUB_DETAIL](../../references/database-contracts.md#db008) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: office.dbo.mng_hub_detail | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Office.dbo.MNG_HUB](../../references/database-contracts.md#db007) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: office.dbo.mng_hub | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| 파일: storage.attachments | error-receipt 하위 첨부파일 및 저장 파일 식별자 | 오류 접수의 첨부 저장·다운로드. 기존 경로 prefix 호환과 실제 파일 존재·접근 권한 확인 | [ErrorReceiptAttachmentService.kt](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/error/service/ErrorReceiptAttachmentService.kt) |

위 DB 계약 링크에는 실제 파라미터 타입·기본값·IN/OUT, Mapper 결과 컬럼, RETURN 바인딩, 참조 테이블·하위 프로시저·정의 필터/정렬을 기록했다. DTO·Service·Repository·Mapper의 상세 호출 경로는 각 API 계약에서 확인한다.

**파일**: 업로드·다운로드의 소유 대상, 원래 파일명, 저장 경로 설정, 파일 존재 여부를 구분한다. 저장소 경로와 비밀값은 사용자 입력으로 대체하지 않는다. 파일·외부 연계 상세는 API의 연결 Service·설정 키 근거를 참조한다.

## 6) 예외 상황과 운영 확인

**빈값 입력 재현**: 업체 정보를 입력해주세요.; 문서 제목을 입력해주세요.; 문의 내용을 입력해주세요.. 빈 입력에서 확인한 클라이언트 오류이며 저장 요청 성공·서버 검증 재현은 아니다.

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
|---|---|---|
| 결과가 없거나 기대 건수와 다름 | 적용된 검색 기준·기간·탭·대상 상태·서버 필터·페이징·목록/다운로드 조건 | 조건을 다시 확인하고 조회한다. 지속되면 경로·작업 시각·마스킹한 식별자·필터를 업무/기술 담당에게 전달한다. |
| 메뉴·버튼 미표시 또는 접근 거부 | 사용자 그룹의 메뉴 접근·VIEW 및 API별 PROCESS/EXECUTE/DELETE/EXCEL_DOWNLOAD/UNMASK 등 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. 프런트 버튼 표시만으로 서버 권한을 판단하지 않는다. |
| 저장·삭제·외부 실행의 결과가 불명확 | 대상 현재 상태·중복 요청·감사 이력·API 오류·파일/외부 소비 로그 | 기존 반영 여부를 먼저 조회한다. 중복 발송·초기화·금액 처리를 피하기 위해 기술 담당 확인 후 재시도한다. |

## 7) 검증·출처

**브라우저 검증(2026-11-09)**: 화면 대조. [경로별 결과와 제한](../../references/browser-verification.md#page058). 역할별 권한 거부·저장 성공·파일 반출·외부 연계 완료는 이 결과로 보장하지 않는다.

| 검증 항목 | 근거·환경 | 상태·확인일 |
|---|---|---|
| 대상 선정 | 사용자가 WBS 탭 내용으로 제공한 텍스트의 No. 150, 151, 152, 153, 154; [선정 태스크](../../inventory/wbs-tasks.csv) | 제공 텍스트 확인 2026-11-09. 원본 Excel의 탭/병합 셀을 독립 재열람한 것은 아님. |
| 메뉴·라우트·화면 | [menuConfig.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts); [OperationsRoutes.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/OperationsRoutes.tsx); [ErrorReportRegisterPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/error/ErrorReportRegisterPage.tsx) | 코드 확인 2026-11-09, 기준 dc216b313 |
| 기능·권한·API | 이 문서의 API 계약 링크 및 연결 Hook/API·Controller·DTO·Service·Repository·Mapper | 코드 확인 2026-11-09. 조회 요청·화면 대조 범위는 아래 브라우저 근거 참조. 권한 계정별 허용·거부 및 변경 요청 실행은 미확인. |
| DB 정의 | [개발 DB 계약](../../references/database-contracts.md), 이 문서의 연결 객체 | 개발 DB 정의 확인 2026-11-09. 동적 SQL·CLR 내부·정의 미공개 참조의 미확정 범위는 객체별 기록; 후속 확인 DB 담당. |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-f80982df149c7ffd) | Demo 메타데이터 14/14개 확인 · Dev와 계약 차이 2개 · 2026-11-11 |
| 브라우저 화면·배포 환경 | 로컬 인증 계정·Playwright CLI; [화면별 검증표](../../references/browser-verification.md#page058) | 화면 대조, 2026-11-09. 배포본·타 역할·업무 변경 결과는 미확인. |
| 업무 프로시저·쓰기·외부 결과 | 격리된 검증 환경·테스트 데이터의 실행 결과 | 미확인: 명시적인 저장·삭제·발송·초기화 요청은 실행하지 않음. 브라우저 GET의 업무 조회 프로시저·조회수·감사 기록은 별도 영향으로 구분. 격리 환경에서 기술 담당 확인. |

코드 확인과 DB 정의 확인은 실행 성공·업무 승인·다른 환경 적용을 보장하지 않는다. 업무·기술 담당 검토 후 조사 목록의 상태를 완료로 변경한다.

브라우저 직접 근거: [settled-static-recheck](../../evidence/browser/static-stable.json). 경로·고정 버튼명·입력 속성·표 머리글·API 상태를 보관했고 실제 데이터 값·식별자·인증정보는 제외했다.

# [SB 운영관리] 전체 오류 조회/처리 (오류 처리내역 등록) 관리자 매뉴얼

작성 기준: `dc216b313` · 확인일 2026-11-09 · 조사 상태 **검토 대기**. 코드·개발 DB 정의 확인. 브라우저: **진입 미재현**; 저장·발송 등 업무 실행 결과는 미검증이다.

## 1) 화면 기본 정보

### 도메인 이해

서비스 이용 중 발생한 문제를 접수하고 처리 경과를 남기는 업무다. 개별 오류 건의 문의 업체·증상·처리 상태와, 여러 오류에서 공통으로 사용하는 오류 코드 설명을 나누어 관리한다.

| 구분 | 설명 |
|---|---|
| 업무 영역 | 서비스 오류 접수·처리 · SB 운영관리 > 오류 관리 > 전체 오류 조회/처리 |
| 주요 대상·용어 | 오류 접수 건: 실제 조사·처리할 개별 문제 / 처리내역: 해당 건에 남기는 대응 기록 / 오류 코드: 문제 유형과 설명을 식별하는 공통 코드 |
| 업무 흐름 | 문의·증상 접수 → 오류 목록에서 대상 확인 → 원인·처리내역 기록 → 상태 확인 |
| 이 페이지의 역할 | 접수 오류 상세에서 처리내역을 작성하는 단계다. 문의 원문 조회와 구분하며 처리 내용·상태를 해당 오류 건에 연결한다. |
| 관련 업무와 구분 | 오류 코드 정의를 바꾸는 일과 접수 건을 처리하는 일은 다르다. 처리내역 저장만으로 실제 서비스 장애가 해결되었다고 판단하지 않는다. |

도메인 설명 근거: 이 문서 7번의 현재 메뉴·라우트·화면 및 API·업무 규칙 소스. [전체 도메인 지도](../../references/domain-overview.md#error). 설명 보강일 2026-11-09; 기존 실행 검증 범위와 미확인 상태는 변경하지 않았다.

### 화면 정보

| 항목 | 작성 내용 |
|---|---|
| 업무 도메인·목적 | 접수된 서비스 오류를 등록하고 처리 상태·처리내역·참조 정보를 관리한다. |
| 메뉴·화면 경로 | SB 운영관리 > 오류 관리 > 전체 오류 조회/처리; `/error-management/error-reports/:id/process`; 목록에서 선택한 대상의 경로 변수를 유지하여 진입한다. |
| 화면 유형·담당 | 오류 처리내역 등록; WBS 작업자 유지윤. 업무·기술 담당 팀명은 원문에 없어 배포 전 해당 도메인 담당자가 확정한다. |
| 관련 화면 | [조회·관리](error-reports.md); [등록](error-reports__new.md); [상세](error-reports__by-id.md) |

WBS 근거: No. 150, 151, 152, 153, 154 (사용자가 제공한 텍스트 행 189, 190, 191, 192, 193). API 개발/화면 개발의 중복 행은 같은 화면으로 통합했다.

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
|---|---|---|
| 화면 진입·조회 | `/error-management/error-reports` 메뉴 접근·하위 경로 작업 권한. 조회 API는 VIEW, 등록/수정 경로는 PROCESS 등 아래 서버 액션과 라우트 가드를 함께 적용한다. | 로그인된 관리자 계정; id 식별자는 이전 화면에서 선택한다. |
| 선택 | `/error-management/error-reports`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 삭제 | `/error-management/error-reports`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 저장 | `/error-management/error-reports`; 화면 게이트 PROCESS. 실제 서버 액션은 API별 표 참조. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 목록 | `/error-management/error-reports`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |

서버가 최종 권한을 검사한다. 버튼 모양(kind)으로 권한을 추정하지 않는다. 특히 등록·수정이 PROCESS를 사용하는 API와 EXECUTE·UNMASK·EXCEL_DOWNLOAD는 서로 구분한다.

## 3) 화면 사용 절차

**처리내역 진입**: 전체 오류 조회/처리에서 대상을 열고 상세의 **처리내역 작성**을 선택하면 `/error-management/error-reports/:id/process`로 이동한다. 해당 버튼의 작업 권한과 대상 상태를 확인한다. 화면 이동 자체로 처리내역이 저장되지는 않는다.

1. 관련 화면에서 대상 또는 작업을 선택하여 `/error-management/error-reports/:id/process`로 이동한다. 경로 변수는 주소에서 임의로 바꾸지 않고 이전 화면이 전달한 식별자를 사용한다.
2. 입력값과 선택된 업체·대상을 확인한다. 기존 정보와 원문을 확인한 뒤 변경한다. 필수값과 형식 오류가 표시되면 해당 항목을 수정한다.
3. **저장**을 누르고 확인창이 있으면 대상·작업을 확인한다. 첨부가 있으면 기존 파일의 유지·삭제·교체 선택을 함께 확인한다.
4. 처리 결과 메시지를 확인한 뒤 목록 또는 상세에서 결과를 다시 조회한다. 오류가 나면 아래 예외 대응과 API 오류를 확인하고 중복 저장 전에 기존 처리 여부를 확인한다.

**이 화면에서 유의할 업무 규칙**: 목록에서 접수일자·진행상태·문의 업체·허브업체·오류 서비스/종류/코드로 검색한다. 오류 접수/등록에서 문의업체와 담당자를 선택하고 문의 내용을 입력한다. 상세에서는 업체 접수내역과 처리내역을 확인하고 별도 처리 등록 화면에서 상태와 처리 내용을 저장한다. 미처리 오류/상태불일치 팝업은 같은 문서에서 다룬다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
|---|---|---|---|
| 오류 접수 정보 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/error/ErrorProcessRegisterPage.tsx#L382) |
| 문의 업체 정보 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/error/ErrorProcessRegisterPage.tsx#L414) |
| 문의 사항 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/error/ErrorProcessRegisterPage.tsx#L436) |
| 처리 내역 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/error/ErrorProcessRegisterPage.tsx#L500) |
| 오류 원인 분석 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/error/ErrorProcessRegisterPage.tsx#L666) |

입력 검증 근거: [ErrorProcessRegisterPage.schema.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/operations/error/ErrorProcessRegisterPage.schema.ts). 프런트 검증과 서버 DTO 제약이 다르면 서버 검증이 최종 기준이다.

화면 필드 키와 API 필드명이 다른 경우 변환은 Hook/API의 검색·저장 매핑에서 수행된다. 요청·응답 필드와 DB 컬럼 매핑은 아래 API 계약 및 DB 객체 계약에 연결했다.

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
|---|---|---|---|
| 오류 상세 조회 | [GET /api/v1/tax-operations/error-reports/detail/{id}](../../references/api-contracts.md#api172); `/error-management/error-reports` / `VIEW` | `경로·쿼리·본문 계약 참조` → `id, errorNumber, status, title, content, errorDate, endDate, totalProcessingTime, registrant, processor, processingTeam, processingTeamNo, smsReceive, businessNumber, companyName, ` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 첨부파일 업로드 | [POST /api/v1/tax-operations/error-reports/attachments](../../references/api-contracts.md#api251); `/error-management/error-reports/new` / `PROCESS` | `경로·쿼리·본문 계약 참조` → `fileName, originalFileName, fileSize, message` | 쓰기 대상 smartwork.dbo.error_receipt_attachment_meta |
| 첨부파일 다운로드 | [GET /api/v1/tax-operations/error-reports/attachments/{*relativePath}](../../references/api-contracts.md#api169); `/error-management/error-reports` / `VIEW` | `경로·쿼리·본문 계약 참조` → `응답 DTO·파일/처리 결과 계약 참조` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 처리상태 저장 | [POST /api/v1/tax-operations/error-reports/{id}/status](../../references/api-contracts.md#api253); `/error-management/error-reports` / `PROCESS` | `status, dealContent, dealTimeH, dealTeamNo, requestTeamNo, hubCompanyId, hubCompanyName, routingType, errorCode, errorType, serviceType, errorDetailCode, errorEtc, attachmentFileNa` → `ctiStatus, warningMessage` | 쓰기 대상 office.dbo.cti_requestmessage, office.dbo.error_deal, office.dbo.error_managemennt, smartbill3.dbo.admin_call, smartbill3.dbo.admin_call_detail |
| 허브업체 검색 | [GET /api/v1/tax-operations/error-reports/hub-companies/search](../../references/api-contracts.md#api175); `/error-management/error-reports/new` / `VIEW` | `경로·쿼리·본문 계약 참조` → `응답 DTO·파일/처리 결과 계약 참조` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
|---|---|---|---|
| [smartwork.dbo.error_receipt_attachment_meta](../../references/database-contracts.md#db271) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 쓰기: smartwork.dbo.error_receipt_attachment_meta. 참조: smartwork.dbo.error_receipt_attachment_meta | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.usp_error_receipt_detail](../../references/database-contracts.md#db286) | `@err_idx int IN` | 확정한 테이블 쓰기 없음. 참조: office.dbo.dept, office.dbo.error_managemennt, office.dbo.function_code, office.dbo.sawon | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Office.dbo.CTI_RequestMessage](../../references/database-contracts.md#db004) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: office.dbo.cti_requestmessage | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Office.dbo.upGW_ViewErrorHistory](../../references/database-contracts.md#db045) | `@err_num varchar(20) IN` | 확정한 테이블 쓰기 없음. 참조: office.dbo.error_managemennt | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.usp_error_deal_time_sum](../../references/database-contracts.md#db285) | `@err_idx int IN` | 확정한 테이블 쓰기 없음. 참조: office.dbo.error_deal | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Office.dbo.upGW_ViewErrorReply](../../references/database-contracts.md#db046) | `@err_idx int IN` | 확정한 테이블 쓰기 없음. 참조: office.dbo.error_reply, office.dbo.sawon | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Office.dbo.upGW_ViewErrorDetail](../../references/database-contracts.md#db044) | `@err_idx int IN` | 확정한 테이블 쓰기 없음. 참조: office.dbo.dept, office.dbo.error_deal, office.dbo.sawon | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Office.dbo.upCTI_SaveRequestMessage](../../references/database-contracts.md#db016) | `@TRANSFER_ID varchar(50) IN, @PROCESS_ID varchar(30) IN, @CUser varchar(10) IN, @InOut varchar(1) IN` | 쓰기: office.dbo.cti_requestmessage. 참조: office.dbo.cti_requestmessage | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SMARTBILL3.dbo.upAdmSB_QSav](../../references/database-contracts.md#db237) | `@mod varchar(5) IN, @no no IN, @id varchar(20) IN, @com_no no IN, @mem_no no IN, @tel_no tel IN, @kind varchar(3) IN, @title title IN, @contents contents IN, @status varchar(5) IN, @req_name varchar(30) IN, @slvcontents contents IN, @dept varchar(30) IN, @name varchar(30) IN, @com_name varchar(70) IN, @com_regno varchar(13) IN, @callback_date varchar(10) IN, @div_market char(2) IN, @err_bns_id int IN, @calsubkind varchar(4) IN, @remote_yn varchar(1) IN` | 쓰기: smartbill3.dbo.admin_call, smartbill3.dbo.admin_call_detail. 참조: smartbill3.dbo.admin_call, smartbill3.dbo.admin_call_detail | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Office.dbo.SAWON](../../references/database-contracts.md#db009) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: office.dbo.sawon | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Office.dbo.upGW_ModErrorEndDate](../../references/database-contracts.md#db029) | `@err_idx int IN` | 쓰기: office.dbo.error_managemennt. 참조: office.dbo.error_managemennt | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Office.dbo.upGW_SaveErrorDetail](../../references/database-contracts.md#db033) | `@err_idx int IN, @sw_no int IN, @deal_time_h varchar(50) IN, @deal_content text IN, @deal_status char(1) IN, @deal_team int IN, @str_file varchar(100) IN` | 쓰기: office.dbo.error_deal. 참조: office.dbo.error_deal | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Office.dbo.upGW_ModError](../../references/database-contracts.md#db028) | `@err_idx int IN, @err_status char(1) IN, @req_team int IN, @err_bns_name varchar(50) IN, @err_bns_id int IN, @routing_type varchar(10) IN, @err_code varchar(20) IN, @err_type char(1) IN, @svc_type char(1) IN, @err_detail_code varchar(10) IN, @error_etc varchar(500) IN` | 쓰기: office.dbo.error_managemennt. 참조: office.dbo.error_managemennt | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Office.dbo.BUSINESS](../../references/database-contracts.md#db003) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: office.dbo.business | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| 파일: storage.attachments | error-receipt 하위 첨부파일 및 저장 파일 식별자 | 오류 접수의 첨부 저장·다운로드. 기존 경로 prefix 호환과 실제 파일 존재·접근 권한 확인 | [ErrorReceiptAttachmentService.kt](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/error/service/ErrorReceiptAttachmentService.kt) |

위 DB 계약 링크에는 실제 파라미터 타입·기본값·IN/OUT, Mapper 결과 컬럼, RETURN 바인딩, 참조 테이블·하위 프로시저·정의 필터/정렬을 기록했다. DTO·Service·Repository·Mapper의 상세 호출 경로는 각 API 계약에서 확인한다.

**파일**: 업로드·다운로드의 소유 대상, 원래 파일명, 저장 경로 설정, 파일 존재 여부를 구분한다. 저장소 경로와 비밀값은 사용자 입력으로 대체하지 않는다. 파일·외부 연계 상세는 API의 연결 Service·설정 키 근거를 참조한다.

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
|---|---|---|
| 결과가 없거나 기대 건수와 다름 | 적용된 검색 기준·기간·탭·대상 상태·서버 필터·페이징·목록/다운로드 조건 | 조건을 다시 확인하고 조회한다. 지속되면 경로·작업 시각·마스킹한 식별자·필터를 업무/기술 담당에게 전달한다. |
| 메뉴·버튼 미표시 또는 접근 거부 | 사용자 그룹의 메뉴 접근·VIEW 및 API별 PROCESS/EXECUTE/DELETE/EXCEL_DOWNLOAD/UNMASK 등 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. 프런트 버튼 표시만으로 서버 권한을 판단하지 않는다. |
| 저장·삭제·외부 실행의 결과가 불명확 | 대상 현재 상태·중복 요청·감사 이력·API 오류·파일/외부 소비 로그 | 기존 반영 여부를 먼저 조회한다. 중복 발송·초기화·금액 처리를 피하기 위해 기술 담당 확인 후 재시도한다. |

## 7) 검증·출처

**브라우저 검증(2026-11-09)**: 진입 미재현. 목록·기간·회사명 조건에서 상세 진입 가능한 테스트 행을 확보하지 못함. 임의 ID 사용·데이터 생성은 하지 않음. [경로별 결과와 제한](../../references/browser-verification.md#page057). 역할별 권한 거부·저장 성공·파일 반출·외부 연계 완료는 이 결과로 보장하지 않는다.

| 검증 항목 | 근거·환경 | 상태·확인일 |
|---|---|---|
| 대상 선정 | 사용자가 WBS 탭 내용으로 제공한 텍스트의 No. 150, 151, 152, 153, 154; [선정 태스크](../../inventory/wbs-tasks.csv) | 제공 텍스트 확인 2026-11-09. 원본 Excel의 탭/병합 셀을 독립 재열람한 것은 아님. |
| 메뉴·라우트·화면 | [menuConfig.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts); [OperationsRoutes.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/OperationsRoutes.tsx); [ErrorProcessRegisterPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/error/ErrorProcessRegisterPage.tsx) | 코드 확인 2026-11-09, 기준 dc216b313 |
| 기능·권한·API | 이 문서의 API 계약 링크 및 연결 Hook/API·Controller·DTO·Service·Repository·Mapper | 코드 확인 2026-11-09. 조회 요청·화면 대조 범위는 아래 브라우저 근거 참조. 권한 계정별 허용·거부 및 변경 요청 실행은 미확인. |
| DB 정의 | [개발 DB 계약](../../references/database-contracts.md), 이 문서의 연결 객체 | 개발 DB 정의 확인 2026-11-09. 동적 SQL·CLR 내부·정의 미공개 참조의 미확정 범위는 객체별 기록; 후속 확인 DB 담당. |
| 브라우저 화면·배포 환경 | 로컬 인증 계정·Playwright CLI; [화면별 검증표](../../references/browser-verification.md#page057) | 진입 미재현, 2026-11-09. 배포본·타 역할·업무 변경 결과는 미확인. |
| 업무 프로시저·쓰기·외부 결과 | 격리된 검증 환경·테스트 데이터의 실행 결과 | 미확인: 명시적인 저장·삭제·발송·초기화 요청은 실행하지 않음. 브라우저 GET의 업무 조회 프로시저·조회수·감사 기록은 별도 영향으로 구분. 격리 환경에서 기술 담당 확인. |

코드 확인과 DB 정의 확인은 실행 성공·업무 승인·다른 환경 적용을 보장하지 않는다. 업무·기술 담당 검토 후 조사 목록의 상태를 완료로 변경한다.

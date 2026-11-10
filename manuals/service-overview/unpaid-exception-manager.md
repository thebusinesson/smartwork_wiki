# [서비스 현황] 미납 예외업체 관리 (조회·관리) 관리자 매뉴얼

작성 기준: `dc216b313` · 확인일 2026-11-09 · 조사 상태 **검토 대기**. 코드·개발 DB 정의 확인. 브라우저: **화면 대조**; 저장·발송 등 업무 실행 결과는 미검증이다.

## 1) 화면 기본 정보

### 도메인 이해

미납 업체에 대해 이용 제한 예외가 어느 기간 동안 적용되는지 관리한다.

| 구분 | 설명 |
|---|---|
| 업무 영역 | 미납 업체의 이용 제한 예외 > 미납 예외업체 관리 조회·관리 |
| 언제 사용하는가 | 고객의 이용 제한 문의에서 예외 등록·기간·상태를 확인할 때 |
| 주요 대상·데이터 | 업체·예외 적용 기간·사용 상태가 제한 예외 기록을 결정한다. |
| 업무 흐름 | 업체·기간·상태 검색 → 기존 예외 확인 → 등록/상세 팝업에서 기간·상태 관리 |
| 이 페이지의 역할 | 업체별 미납 예외 중 **미납 예외업체 관리 조회·관리** 단계. 미납 업체에 대해 이용 제한 예외가 어느 기간 동안 적용되는지 관리한다. |
| 판단 결과·다음 업무 | 중복·기간 오류를 확인한 뒤 같은 업체의 예외 결과를 재조회한다. |
| 다른 화면과의 구분 | 예외 허용은 미납 금액의 수납·감면·정산 처리가 아니다. |

설명 근거: [UnpaidExceptionManager.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/serviceoverview/UnpaidExceptionManager.tsx), 이 문서 4·5·7번의 항목·API·업무 규칙. [상위 업무 영역](../../references/domain-overview.md#unpaid)은 공통 배경이며 현재 화면의 데이터·동작은 위 설명을 따른다. 설명 수정일 **2026-11-10**; 새 업무 실행 검증을 수행한 것은 아니다.

### 화면 정보

| 항목 | 작성 내용 |
|---|---|
| 업무 도메인·목적 | 미납 업체에 대해 이용 제한 예외가 어느 기간 동안 적용되는지 관리한다. |
| 메뉴·화면 경로 | 서비스 현황 > 미납 예외업체 관리 > 미납 예외업체 관리; `/service-overview/unpaid-exception-manager`; 메뉴 또는 관련 화면에서 진입한다. |
| 화면 유형·담당 | 조회·관리; WBS 작업자 유지윤. 업무·기술 담당 팀명은 원문에 없어 배포 전 해당 도메인 담당자가 확정한다. |
| 관련 화면 | 같은 메뉴에 별도 독립 경로 없음. 팝업·탭은 이 문서 참조. |

WBS 근거: No. 219, 220 (사용자가 제공한 텍스트 행 278, 279). API 개발/화면 개발의 중복 행은 같은 화면으로 통합했다.

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
|---|---|---|
| 화면 진입·조회 | `/service-overview/unpaid-exception-manager` 메뉴 접근·하위 경로 작업 권한. 조회 API는 VIEW, 등록/수정 경로는 PROCESS 등 아래 서버 액션과 라우트 가드를 함께 적용한다. | 로그인된 관리자 계정; 아래 검색·입력 항목을 준비한다. |
| 미납 예외 신규 등록 | `/service-overview/unpaid-exception-manager`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 취소 | `/service-overview/unpaid-exception-manager`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 삭제 | `/service-overview/unpaid-exception-manager`; 화면 게이트 DELETE. 실제 서버 액션은 API별 표 참조. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 저장 | `/service-overview/unpaid-exception-manager`; 화면 게이트 PROCESS. 실제 서버 액션은 API별 표 참조. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 수정 | `/service-overview/unpaid-exception-manager`; 화면 게이트 PROCESS. 실제 서버 액션은 API별 표 참조. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 목록 | `/service-overview/unpaid-exception-manager`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |

서버가 최종 권한을 검사한다. 버튼 모양(kind)으로 권한을 추정하지 않는다. 특히 등록·수정이 PROCESS를 사용하는 API와 EXECUTE·UNMASK·EXCEL_DOWNLOAD는 서로 구분한다.

## 3) 화면 사용 절차

**검증 시 화면 버튼**: 검색, 미납 예외 신규 등록. 화면 상태·대상에 따라 달라지며 아래 작업 절차와 권한 조건을 함께 확인한다.

1. `서비스 현황 > 미납 예외업체 관리 > 미납 예외업체 관리` 메뉴를 연다. 경로 변수는 주소에서 임의로 바꾸지 않고 이전 화면이 전달한 식별자를 사용한다.
2. 현재 검색 조건과 아래 기본값을 확인한다. **예외 기간, 업체 조건, 미납 예외** 항목에 필요한 값을 입력하고 **검색**을 누른다.
3. 결과 표·탭·팝업에서 대상의 상태와 합계·이력을 확인한다. 다른 조회 조건으로 바꾼 경우 다시 검색하여 결과를 갱신한다.

**이 화면에서 유의할 업무 규칙**: 업체 조건 기본은 사업자번호다. 등록/수정은 같은 화면의 팝업에서 수행하며 예외 기간은 YYYY-MM 입력과 년월 달력을 사용한다. 미사용 상태와 사용정지 표기를 혼동하지 않는다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
|---|---|---|---|
| 예외 기간 | 입력·필수 | 화면 타입 toggleableMonthRange | `dateCondition`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/serviceoverview/UnpaidExceptionManager.tsx#L26) |
| 업체 조건 | 입력·선택(조건부 검증 별도) | 화면 타입 selectWithInput; 선택: 전체=ALL, 회사명=N, 사업자번호=R | `companyCondition`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/serviceoverview/UnpaidExceptionManager.tsx#L37) |
| 미납 예외 | 입력·선택(조건부 검증 별도) | 화면 타입 checkbox; 선택: 사용=Y, 미사용=N | `status`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/serviceoverview/UnpaidExceptionManager.tsx#L58) |
| 회사명 | 출력 | API 타입 String | `companyName`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/serviceoverview/UnpaidExceptionManager.tsx#L210) |
| 사업자번호 | 출력 | API 타입 String | `businessNumber`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/serviceoverview/UnpaidExceptionManager.tsx#L211) |
| 기간 | 출력 | API 타입 String?; 기본 null | `fromMonth`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/serviceoverview/UnpaidExceptionManager.tsx#L222) |

입력 검증 근거: [createUnpaidExceptionSchema.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/status/serviceoverview/createUnpaidExceptionSchema.ts), [UnpaidExceptionRegistrationDialog.schema.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/status/serviceoverview/UnpaidExceptionRegistrationDialog.schema.ts). 프런트 검증과 서버 DTO 제약이 다르면 서버 검증이 최종 기준이다.

**복합 검색·폼의 초기 상태**

| 초기값 근거 | 기본 상태 |
|---|---|
| [createInitialForm](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/serviceoverview/UnpaidExceptionDetailDialog.tsx#L57) | startDate={undefined}; endDate={undefined}; isStartDateValid=켜짐; isEndDateValid=켜짐; reason=빈값; useYn=Y; detail=미지정; isEditing=꺼짐; deleteOpen=꺼짐 |

화면 필드 키와 API 필드명이 다른 경우 변환은 Hook/API의 검색·저장 매핑에서 수행된다. 요청·응답 필드와 DB 컬럼 매핑은 아래 API 계약 및 DB 객체 계약에 연결했다.

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
|---|---|---|---|
| 미납 예외업체 목록 조회 | [GET /api/v1/service-status/unpaid-exceptions](../../references/api-contracts.md#api121); `/service-overview/unpaid-exception-manager` / `VIEW` | `searchCode, searchText, useYn, fromMonth, toMonth, page, size` → `content, totalElements, totalPages, currentPage, size, comNo, companyName, businessNumber, fromMonth, toMonth, registrant` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 미납 예외업체 상세 조회 | [GET /api/v1/service-status/unpaid-exceptions/{comNo}](../../references/api-contracts.md#api123); `/service-overview/unpaid-exception-manager` / `VIEW` | `경로·쿼리·본문 계약 참조` → `comNo, companyName, businessNumber, fromMonth, toMonth, reason, useYn, registrant` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 미납 예외업체 수정 | [PUT /api/v1/service-status/unpaid-exceptions/{comNo}](../../references/api-contracts.md#api268); `/service-overview/unpaid-exception-manager` / `PROCESS` | `fromMonth, toMonth, reason, useYn` → `응답 DTO·파일/처리 결과 계약 참조` | 쓰기 대상 sb_bill.dbo.unpaid_charge_clear, sb_bill.dbo.unpaid_charge_clear_his |
| 미납 예외업체 삭제 | [DELETE /api/v1/service-status/unpaid-exceptions](../../references/api-contracts.md#api003); `/service-overview/unpaid-exception-manager` / `DELETE` | `comNoList` → `응답 DTO·파일/처리 결과 계약 참조` | 쓰기 대상 sb_bill.dbo.unpaid_charge_clear, sb_bill.dbo.unpaid_charge_clear_his |
| 업체 검색 | [GET /api/v1/service-status/unpaid-exceptions/companies/search](../../references/api-contracts.md#api122); `/service-overview/unpaid-exception-manager` / `VIEW` | `경로·쿼리·본문 계약 참조` → `응답 DTO·파일/처리 결과 계약 참조` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 미납 예외업체 등록 | [POST /api/v1/service-status/unpaid-exceptions](../../references/api-contracts.md#api237); `/service-overview/unpaid-exception-manager` / `PROCESS` | `comNo, fromMonth, toMonth, reason, useYn` → `응답 DTO·파일/처리 결과 계약 참조` | 쓰기 대상 sb_bill.dbo.unpaid_charge_clear, sb_bill.dbo.unpaid_charge_clear_his |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
|---|---|---|---|
| [smartwork.dbo.usp_unpaid_exception_list_select](../../references/database-contracts.md#db295) | `@PAGE int IN, @PAGESIZE int IN, @FROM_MONTH varchar(10) IN, @TO_MONTH varchar(10) IN, @SEARCH_CODE varchar(1) IN, @SEARCH_TEXT varchar(50) IN, @USE_YN varchar(1) IN` | 확정한 테이블 쓰기 없음. 참조: office.dbo.sawon, sb_bill.dbo.unpaid_charge_clear, smartbill3.dbo.company | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_BILL.dbo.UspBill_UnPaidCompanyClearInfo_SELECT](../../references/database-contracts.md#db090) | `@COM_NO int IN` | 확정한 테이블 쓰기 없음. 참조: office.dbo.sawon, sb_bill.dbo.unpaid_charge_clear, smartbill3.dbo.company | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_BILL.dbo.UspBill_UnPaidCompanyClearInfo_UPDATE](../../references/database-contracts.md#db091) | `@COM_NO int IN, @FROM_MONTH varchar(10) IN, @TO_MONTH varchar(10) IN, @REASON varchar(500) IN, @USE_YN varchar(1) IN, @SW_NO int IN, @RESULT varchar(1) OUT` | 쓰기: sb_bill.dbo.unpaid_charge_clear, sb_bill.dbo.unpaid_charge_clear_his. 참조: sb_bill.dbo.unpaid_charge_clear, sb_bill.dbo.unpaid_charge_clear_his | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_BILL.dbo.UspBill_UnPaidCompanyClearInfo_DELETE](../../references/database-contracts.md#db089) | `@COM_NO int IN, @SW_NO int IN, @RESULT varchar(1) OUT` | 쓰기: sb_bill.dbo.unpaid_charge_clear, sb_bill.dbo.unpaid_charge_clear_his. 참조: sb_bill.dbo.unpaid_charge_clear, sb_bill.dbo.unpaid_charge_clear_his | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.UspUnpaidException_CompanySearch_SELECT](../../references/database-contracts.md#db341) | `@SEARCH_TERM nvarchar(100) IN` | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.company | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_BILL.dbo.UspBill_UnPaidClearCompanyInfo_INSERT](../../references/database-contracts.md#db088) | `@COM_NO int IN, @FROM_MONTH varchar(10) IN, @TO_MONTH varchar(10) IN, @REASON varchar(500) IN, @USE_YN varchar(1) IN, @SW_NO int IN, @RESULT varchar(1) OUT` | 쓰기: sb_bill.dbo.unpaid_charge_clear, sb_bill.dbo.unpaid_charge_clear_his. 참조: sb_bill.dbo.unpaid_charge_clear, sb_bill.dbo.unpaid_charge_clear_his | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |

위 DB 계약 링크에는 실제 파라미터 타입·기본값·IN/OUT, Mapper 결과 컬럼, RETURN 바인딩, 참조 테이블·하위 프로시저·정의 필터/정렬을 기록했다. DTO·Service·Repository·Mapper의 상세 호출 경로는 각 API 계약에서 확인한다.

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
|---|---|---|
| 데이터가 없습니다. | [문구·처리 코드](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/serviceoverview/UnpaidExceptionManager.tsx#L208); 현재 조건·대상·권한 확인 | 검색·조회 오류면 조건을 확인 후 재조회. 변경·발송 결과가 불명확하면 처리 여부와 이력을 확인한 뒤 재시도 여부를 판단한다. |
| 결과가 없거나 기대 건수와 다름 | 적용된 검색 기준·기간·탭·대상 상태·서버 필터·페이징·목록/다운로드 조건 | 조건을 다시 확인하고 조회한다. 지속되면 경로·작업 시각·마스킹한 식별자·필터를 업무/기술 담당에게 전달한다. |
| 메뉴·버튼 미표시 또는 접근 거부 | 사용자 그룹의 메뉴 접근·VIEW 및 API별 PROCESS/EXECUTE/DELETE/EXCEL_DOWNLOAD/UNMASK 등 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. 프런트 버튼 표시만으로 서버 권한을 판단하지 않는다. |
| 저장·삭제·외부 실행의 결과가 불명확 | 대상 현재 상태·중복 요청·감사 이력·API 오류·파일/외부 소비 로그 | 기존 반영 여부를 먼저 조회한다. 중복 발송·초기화·금액 처리를 피하기 위해 기술 담당 확인 후 재시도한다. |

## 7) 검증·출처

**브라우저 검증(2026-11-09)**: 화면 대조. [경로별 결과와 제한](../../references/browser-verification.md#page079). 역할별 권한 거부·저장 성공·파일 반출·외부 연계 완료는 이 결과로 보장하지 않는다.

| 검증 항목 | 근거·환경 | 상태·확인일 |
|---|---|---|
| 대상 선정 | 사용자가 WBS 탭 내용으로 제공한 텍스트의 No. 219, 220; [선정 태스크](../../inventory/wbs-tasks.csv) | 제공 텍스트 확인 2026-11-09. 원본 Excel의 탭/병합 셀을 독립 재열람한 것은 아님. |
| 메뉴·라우트·화면 | [menuConfig.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts); [ServiceOverviewRoutes.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/ServiceOverviewRoutes.tsx); [UnpaidExceptionManager.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/serviceoverview/UnpaidExceptionManager.tsx) | 코드 확인 2026-11-09, 기준 dc216b313 |
| 기능·권한·API | 이 문서의 API 계약 링크 및 연결 Hook/API·Controller·DTO·Service·Repository·Mapper | 코드 확인 2026-11-09. 조회 요청·화면 대조 범위는 아래 브라우저 근거 참조. 권한 계정별 허용·거부 및 변경 요청 실행은 미확인. |
| DB 정의 | [개발 DB 계약](../../references/database-contracts.md), 이 문서의 연결 객체 | 개발 DB 정의 확인 2026-11-09. 동적 SQL·CLR 내부·정의 미공개 참조의 미확정 범위는 객체별 기록; 후속 확인 DB 담당. |
| 브라우저 화면·배포 환경 | 로컬 인증 계정·Playwright CLI; [화면별 검증표](../../references/browser-verification.md#page079) | 화면 대조, 2026-11-09. 배포본·타 역할·업무 변경 결과는 미확인. |
| 업무 프로시저·쓰기·외부 결과 | 격리된 검증 환경·테스트 데이터의 실행 결과 | 미확인: 명시적인 저장·삭제·발송·초기화 요청은 실행하지 않음. 브라우저 GET의 업무 조회 프로시저·조회수·감사 기록은 별도 영향으로 구분. 격리 환경에서 기술 담당 확인. |

코드 확인과 DB 정의 확인은 실행 성공·업무 승인·다른 환경 적용을 보장하지 않는다. 업무·기술 담당 검토 후 조사 목록의 상태를 완료로 변경한다.

브라우저 직접 근거: [settled-static-recheck](../../evidence/browser/static-stable.json). 경로·고정 버튼명·입력 속성·표 머리글·API 상태를 보관했고 실제 데이터 값·식별자·인증정보는 제외했다.

# [SB 고객관리] 회원 정보 (조회·관리) 관리자 매뉴얼

작성 기준: `dc216b313` · 확인일 2026-11-09 · 조사 상태 **검토 대기**. 코드·개발 DB 정의 확인. 브라우저: **화면 대조**; 저장·발송 등 업무 실행 결과는 미검증이다.

## 1) 화면 기본 정보

### 도메인 이해

글로싸인에서 문제가 발생한 사용자를 회사 정보와 개인 정보로 찾아 소속·계정 상태를 확인한다.

| 구분 | 설명 |
|---|---|
| 업무 영역 | 글로싸인 엔터프라이즈 고객·인증 관리 > 회원 정보 조회·관리 |
| 언제 사용하는가 | 사용자 아이디·이메일 또는 소속 회사로 글로싸인 회원을 식별해야 할 때 |
| 주요 대상·데이터 | 회사명·사업자번호는 소속, 회원명·아이디·연락처·이메일은 개인, 블록체인 주소는 별도 식별 정보다. |
| 업무 흐름 | 업체/개인 조건 지정 → 회원 행 확인 → 소속·가입/탈퇴 정보 비교 |
| 이 페이지의 역할 | 회원 현황 중 **회원 정보 조회·관리** 단계. 글로싸인에서 문제가 발생한 사용자를 회사 정보와 개인 정보로 찾아 소속·계정 상태를 확인한다. |
| 판단 결과·다음 업무 | 확인한 회사나 계정을 기준으로 회사 소속 회원 확인 또는 해당 종류의 인증 문제 조사로 이어간다. |
| 다른 화면과의 구분 | 회사 목록의 포인트·회사 상태 조사와 달리 사용자 한 명의 소속·연락·계정 상태가 중심이다. |

설명 근거: [GlosignEnterpriseMemberListPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/glosign/GlosignEnterpriseMemberListPage.tsx), 이 문서 4·5·7번의 항목·API·업무 규칙. [상위 업무 영역](../../references/domain-overview.md#glosign)은 공통 배경이며 현재 화면의 데이터·동작은 위 설명을 따른다. 설명 수정일 **2026-11-10**; 새 업무 실행 검증을 수행한 것은 아니다.

### 화면 정보

| 항목 | 작성 내용 |
|---|---|
| 업무 도메인·목적 | 글로싸인에서 문제가 발생한 사용자를 회사 정보와 개인 정보로 찾아 소속·계정 상태를 확인한다. |
| 메뉴·화면 경로 | SB 고객관리 > 글로싸인 엔터프라이즈 > 회원 정보; `/glosign-enterprise/members`; 메뉴 또는 관련 화면에서 진입한다. |
| 화면 유형·담당 | 조회·관리; WBS 작업자 유지윤. 업무·기술 담당 팀명은 원문에 없어 배포 전 해당 도메인 담당자가 확정한다. |
| 관련 화면 | 같은 메뉴에 별도 독립 경로 없음. 팝업·탭은 이 문서 참조. |

WBS 근거: No. 37 (사용자가 제공한 텍스트 행 60). API 개발/화면 개발의 중복 행은 같은 화면으로 통합했다.

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
|---|---|---|
| 화면 진입·조회 | `/glosign-enterprise/members` 메뉴 접근·하위 경로 작업 권한. 조회 API는 VIEW, 등록/수정 경로는 PROCESS 등 아래 서버 액션과 라우트 가드를 함께 적용한다. | 로그인된 관리자 계정; 아래 검색·입력 항목을 준비한다. |
| 다운로드 | `/glosign-enterprise/members`; 엑셀 download 화면 게이트. 다운로드/업로드 API의 서버 권한과 사유 입력을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |

서버가 최종 권한을 검사한다. 버튼 모양(kind)으로 권한을 추정하지 않는다. 특히 등록·수정이 PROCESS를 사용하는 API와 EXECUTE·UNMASK·EXCEL_DOWNLOAD는 서로 구분한다.

## 3) 화면 사용 절차

**검증 시 화면 버튼**: 검색, 초기화, 다운로드 (비활성). 화면 상태·대상에 따라 달라지며 아래 작업 절차와 권한 조건을 함께 확인한다.

1. `SB 고객관리 > 글로싸인 엔터프라이즈 > 회원 정보` 메뉴를 연다. 경로 변수는 주소에서 임의로 바꾸지 않고 이전 화면이 전달한 식별자를 사용한다.
2. 최초 진입 시 자동조회하지 않는다. 아래 검색 항목을 입력한 후 **검색**을 누른다.
3. 결과 표·탭·팝업에서 대상의 상태와 합계·이력을 확인한다. 다른 조회 조건으로 바꾼 경우 다시 검색하여 결과를 갱신한다.

**이 화면에서 유의할 업무 규칙**: 날짜 조건과 업체/개인 조건을 입력하고 검색한다. 날짜 정렬 기능과 다운로드는 각각 적용된 정렬·조건을 확인한 뒤 사용한다.

**반출**: 적용된 검색 조건과 반출 범위를 확인한 후 다운로드한다. 사유 입력창이 표시되면 업무 사유를 입력한다. 사유 등록 실패·파일 오류는 성공으로 간주하지 않고 다운로드 결과를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
|---|---|---|---|
| 날짜 조건 | 입력·선택(조건부 검증 별도) | 화면 타입 selectWithDateRange; 선택: 전체=all, 가입일=joinDate; 초기값 selectValue=all; dateRange=startDate=빈값; endDate=빈값 | `dateCondition`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/glosign/GlosignEnterpriseMemberListPage.tsx#L56) |
| 업체 조건 | 입력·선택(조건부 검증 별도) | 화면 타입 selectWithInput; 선택: 전체=all, 사업자번호=businessNumber, 회사명=companyName; 초기값 selectValue=businessNumber; inputValue=빈값 | `companyCondition`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/glosign/GlosignEnterpriseMemberListPage.tsx#L70) |
| 개인 조건 | 입력·선택(조건부 검증 별도) | 화면 타입 radioWithInput; 선택: 전체=, 성명=name, 아이디=userId, 이메일=email, 핸드폰=phone; 초기값 radioValue=빈값; inputValue=빈값 | `personalCondition`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/glosign/GlosignEnterpriseMemberListPage.tsx#L91) |
| No | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `no`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/glosign/GlosignEnterpriseMemberListPage.tsx#L300) |
| 회사명 | 출력 | API 타입 String | `companyName`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/glosign/GlosignEnterpriseMemberListPage.tsx#L308) |
| 사업자번호 | 출력 | API 타입 String | `businessNumber`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/glosign/GlosignEnterpriseMemberListPage.tsx#L317) |
| 회원명 | 출력 | API 타입 String | `userName`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/glosign/GlosignEnterpriseMemberListPage.tsx#L335) |
| 아이디 | 출력 | API 타입 String | `userId`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/glosign/GlosignEnterpriseMemberListPage.tsx#L349) |
| 연락처 | 출력 | API 타입 String | `phone`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/glosign/GlosignEnterpriseMemberListPage.tsx#L385) |
| 이메일 | 출력 | API 타입 String | `email`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/glosign/GlosignEnterpriseMemberListPage.tsx#L399) |
| 블록체인 주소 | 출력 | API 타입 String | `blockchainAddress`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/glosign/GlosignEnterpriseMemberListPage.tsx#L416) |
| 가입일 | 출력 | API 타입 String | `joinDate`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/glosign/GlosignEnterpriseMemberListPage.tsx#L427) |
| 탈퇴일 | 출력 | API 타입 String | `withdrawalDate`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/glosign/GlosignEnterpriseMemberListPage.tsx#L436) |
| 검색허용 | 출력 | API 타입 String | `searchAllowed`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/glosign/GlosignEnterpriseMemberListPage.tsx#L447) |

입력 검증 근거: [useGlosignSearchForm.schema.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/customer/glosign/hooks/useGlosignSearchForm.schema.ts). 프런트 검증과 서버 DTO 제약이 다르면 서버 검증이 최종 기준이다.

**복합 검색·폼의 초기 상태**

| 초기값 근거 | 기본 상태 |
|---|---|
| [DEFAULT_FILTER_VALUES](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/glosign/GlosignEnterpriseMemberListPage.tsx#L43) | dateCondition=selectValue=all; dateRange=startDate=빈값; endDate=빈값; companyCondition=selectValue=businessNumber; inputValue=빈값; personalCondition=radioValue=빈값; inputValue=빈값 |

화면 필드 키와 API 필드명이 다른 경우 변환은 Hook/API의 검색·저장 매핑에서 수행된다. 요청·응답 필드와 DB 컬럼 매핑은 아래 API 계약 및 DB 객체 계약에 연결했다.

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
|---|---|---|---|
| 블록체인 회원 목록 조회 | [GET /api/v1/glosign-enterprise/members](../../references/api-contracts.md#api071); `/glosign-enterprise/members` / `VIEW` | `fromDate, toDate, companySearchType, companyKeyword, memberSearchType, memberKeyword, page, size, sortOrder` → `content, totalElements, totalPages, currentPage, size, usrSeq, userName, userId, phone, email, blockchainAddress, searchAllowed, companyName, businessNumber, joinDate, withdrawalDa` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 블록체인 회원 엑셀/CSV 다운로드 | [POST /api/v1/glosign-enterprise/members/download](../../references/api-contracts.md#api217); `/glosign-enterprise/members` / `EXCEL_DOWNLOAD` | `fromDate, toDate, companySearchType, companyKeyword, memberSearchType, memberKeyword, downloadReason, downloadFormat` → `응답 DTO·파일/처리 결과 계약 참조` | 쓰기 대상 smartwork.dbo.action_reason |
| 글로싸인 회원 원문 조회 | [POST /api/v1/glosign-enterprise/members/{usrSeq}/sensitive-values/reveal](../../references/api-contracts.md#api218); `/glosign-enterprise/members` / `UNMASK` | `field` → `field, value` | 쓰기 대상 smartwork.dbo.sw_log_access_event |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
|---|---|---|---|
| [smartwork.dbo.UspGlosignMember_Select](../../references/database-contracts.md#db337) | `@PAGE int IN, @TOP int IN, @FROMDATE varchar(10) IN, @TODATE varchar(10) IN, @MITEM varchar(80) IN, @MTEXT varchar(100) IN, @MITEM2 varchar(80) IN, @MTEXT2 varchar(100) IN, @SortOrder varchar(4) IN` | 확정한 테이블 쓰기 없음. 참조: sec_pt.dbo.tbl_pt_org, sec_pt.dbo.tbl_pt_org_usr, sec_pt.dbo.tbl_pt_usr | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.action_reason](../../references/database-contracts.md#db266) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 쓰기: smartwork.dbo.action_reason. 참조: smartwork.dbo.action_reason | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.usp_sw_log_access_event_insert](../../references/database-contracts.md#db294) | `@EVENT_TYPE varchar(30) IN, @STATUS varchar(20) IN, @USER_ID bigint IN, @MEMBER_ID nvarchar(50) IN, @USER_NAME nvarchar(100) IN, @DEPARTMENT_NAME nvarchar(100) IN, @PAGE_TITLE nvarchar(200) IN, @PATH nvarchar(500) IN, @MENU_PATH nvarchar(500) IN, @MENU_LABEL nvarchar(200) IN, @CATEGORY_NAME nvarchar(200) IN, @SUB_CATEGORY_NAME nvarchar(200) IN, @MENU_ORDER int IN, @IP_ADDRESS varchar(45) IN, @USER_AGENT nvarchar(1000) IN, @BROWSER varchar(100) IN, @OS varchar(100) IN, @REFERRER nvarchar(500) IN, @DETAIL nvarchar(1000) IN, @RESULT int OUT, @COUNTS_AS_VISIT bit IN` | 쓰기: smartwork.dbo.sw_log_access_event. 참조: smartwork.dbo.sw_log_access_event | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SEC_PT.dbo.TBL_PT_ORG_USR](../../references/database-contracts.md#db185) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: sec_pt.dbo.tbl_pt_org_usr | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SEC_PT.dbo.TBL_PT_ORG](../../references/database-contracts.md#db184) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: sec_pt.dbo.tbl_pt_org | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SEC_PT.dbo.TBL_PT_USR](../../references/database-contracts.md#db186) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: sec_pt.dbo.tbl_pt_usr | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |

위 DB 계약 링크에는 실제 파라미터 타입·기본값·IN/OUT, Mapper 결과 컬럼, RETURN 바인딩, 참조 테이블·하위 프로시저·정의 필터/정렬을 기록했다. DTO·Service·Repository·Mapper의 상세 호출 경로는 각 API 계약에서 확인한다.

**민감정보**: 기본 응답의 마스킹 값을 유지한다. 원문은 전용 reveal API와 UNMASK 등 추가 권한·사유·감사 로그를 확인한 뒤 조회한다. 화면·캡처·문의 문서에 원문을 남기지 않는다.

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
|---|---|---|
| 결과가 없거나 기대 건수와 다름 | 적용된 검색 기준·기간·탭·대상 상태·서버 필터·페이징·목록/다운로드 조건 | 조건을 다시 확인하고 조회한다. 지속되면 경로·작업 시각·마스킹한 식별자·필터를 업무/기술 담당에게 전달한다. |
| 메뉴·버튼 미표시 또는 접근 거부 | 사용자 그룹의 메뉴 접근·VIEW 및 API별 PROCESS/EXECUTE/DELETE/EXCEL_DOWNLOAD/UNMASK 등 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. 프런트 버튼 표시만으로 서버 권한을 판단하지 않는다. |
| 저장·삭제·외부 실행의 결과가 불명확 | 대상 현재 상태·중복 요청·감사 이력·API 오류·파일/외부 소비 로그 | 기존 반영 여부를 먼저 조회한다. 중복 발송·초기화·금액 처리를 피하기 위해 기술 담당 확인 후 재시도한다. |

## 7) 검증·출처

**브라우저 검증(2026-11-09)**: 화면 대조. [경로별 결과와 제한](../../references/browser-verification.md#page010). 역할별 권한 거부·저장 성공·파일 반출·외부 연계 완료는 이 결과로 보장하지 않는다.

| 검증 항목 | 근거·환경 | 상태·확인일 |
|---|---|---|
| 대상 선정 | 사용자가 WBS 탭 내용으로 제공한 텍스트의 No. 37; [선정 태스크](../../inventory/wbs-tasks.csv) | 제공 텍스트 확인 2026-11-09. 원본 Excel의 탭/병합 셀을 독립 재열람한 것은 아님. |
| 메뉴·라우트·화면 | [menuConfig.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts); [CustomerRoutes.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/CustomerRoutes.tsx); [GlosignEnterpriseMemberListPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/glosign/GlosignEnterpriseMemberListPage.tsx) | 코드 확인 2026-11-09, 기준 dc216b313 |
| 기능·권한·API | 이 문서의 API 계약 링크 및 연결 Hook/API·Controller·DTO·Service·Repository·Mapper | 코드 확인 2026-11-09. 조회 요청·화면 대조 범위는 아래 브라우저 근거 참조. 권한 계정별 허용·거부 및 변경 요청 실행은 미확인. |
| DB 정의 | [개발 DB 계약](../../references/database-contracts.md), 이 문서의 연결 객체 | 개발 DB 정의 확인 2026-11-09. 동적 SQL·CLR 내부·정의 미공개 참조의 미확정 범위는 객체별 기록; 후속 확인 DB 담당. |
| 브라우저 화면·배포 환경 | 로컬 인증 계정·Playwright CLI; [화면별 검증표](../../references/browser-verification.md#page010) | 화면 대조, 2026-11-09. 배포본·타 역할·업무 변경 결과는 미확인. |
| 업무 프로시저·쓰기·외부 결과 | 격리된 검증 환경·테스트 데이터의 실행 결과 | 미확인: 명시적인 저장·삭제·발송·초기화 요청은 실행하지 않음. 브라우저 GET의 업무 조회 프로시저·조회수·감사 기록은 별도 영향으로 구분. 격리 환경에서 기술 담당 확인. |

코드 확인과 DB 정의 확인은 실행 성공·업무 승인·다른 환경 적용을 보장하지 않는다. 업무·기술 담당 검토 후 조사 목록의 상태를 완료로 변경한다.

브라우저 직접 근거: [settled-static-recheck](../../evidence/browser/static-stable.json). 경로·고정 버튼명·입력 속성·표 머리글·API 상태를 보관했고 실제 데이터 값·식별자·인증정보는 제외했다.

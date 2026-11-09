# [SB 서비스관리] 회사 정보 (조회·관리) 관리자 매뉴얼

작성 기준: `dc216b313` · 확인일 2026-11-09 · 조사 상태 **검토 대기**. 코드·개발 DB 정의 확인. 브라우저: **화면 대조**; 저장·발송 등 업무 실행 결과는 미검증이다.

## 1) 화면 기본 정보

### 도메인 이해

보나뱅크 구분으로 관리되는 회사·회원과 전자세금계산서 업무를 운영하는 영역이다. 고객 정보, 문서 현황, 국세청 신고 실패, 이용 통계와 공지를 함께 확인하되 현재 메뉴의 보나뱅크 범위를 유지한다.

| 구분 | 설명 |
|---|---|
| 업무 영역 | 보나뱅크 서비스 운영 · SB 서비스관리 > 보나뱅크 > 회사 정보 |
| 주요 대상·용어 | 보나뱅크 회사·회원: 이 서비스 구분의 고객 정보 / 신고 실패: 국세청 관련 처리에서 실패로 분류된 내역 / 공지: 서비스 안내 게시물 |
| 업무 흐름 | 보나뱅크 고객 식별 → 회사·회원 또는 문서·통계 선택 → 상태·이력 확인 → 필요한 지원 작업 |
| 이 페이지의 역할 | 보나뱅크 회사 업무의 진입 화면이다. 보나뱅크 회사의 가입·서비스 설정과 소속 회원·변경 이력을 확인한다. 같은 메뉴의 팝업·탭은 이 문서에서, 독립 상세·등록·수정 화면은 관련 문서에서 다룬다. |
| 관련 업무와 구분 | 스마트빌 전체 고객 목록과 보나뱅크 목록은 범위가 다를 수 있다. 세금계산서 목록의 상세 이동은 공통 세금계산서 화면으로 연결되는 현재 구현을 따른다. |

도메인 설명 근거: 이 문서 7번의 현재 메뉴·라우트·화면 및 API·업무 규칙 소스. [전체 도메인 지도](../../references/domain-overview.md#bonabank). 설명 보강일 2026-11-09; 기존 실행 검증 범위와 미확인 상태는 변경하지 않았다.

### 화면 정보

| 항목 | 작성 내용 |
|---|---|
| 업무 도메인·목적 | 보나뱅크 회사의 가입 상태와 서비스 설정을 조회한다. |
| 메뉴·화면 경로 | SB 서비스관리 > 보나뱅크 > 회사 정보; `/bonabank/company`; 메뉴 또는 관련 화면에서 진입한다. |
| 화면 유형·담당 | 조회·관리; WBS 작업자 유지윤. 업무·기술 담당 팀명은 원문에 없어 배포 전 해당 도메인 담당자가 확정한다. |
| 관련 화면 | [상세](company__by-id.md); [변경 이력](company__by-id__change-history.md); [전체 회원 조회](company__by-companyId__members.md) |

WBS 근거: No. 138, 139 (사용자가 제공한 텍스트 행 174, 175). API 개발/화면 개발의 중복 행은 같은 화면으로 통합했다.

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
|---|---|---|
| 화면 진입·조회 | `/bonabank/company` 메뉴 접근·하위 경로 작업 권한. 조회 API는 VIEW, 등록/수정 경로는 PROCESS 등 아래 서버 액션과 라우트 가드를 함께 적용한다. | 로그인된 관리자 계정; 아래 검색·입력 항목을 준비한다. |
| 다운로드 | `/bonabank/company`; 엑셀 download 화면 게이트. 다운로드/업로드 API의 서버 권한과 사유 입력을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |

서버가 최종 권한을 검사한다. 버튼 모양(kind)으로 권한을 추정하지 않는다. 특히 등록·수정이 PROCESS를 사용하는 API와 EXECUTE·UNMASK·EXCEL_DOWNLOAD는 서로 구분한다.

## 3) 화면 사용 절차

**검증 시 화면 버튼**: 검색, 초기화, 다운로드. 화면 상태·대상에 따라 달라지며 아래 작업 절차와 권한 조건을 함께 확인한다.

1. `SB 서비스관리 > 보나뱅크 > 회사 정보` 메뉴를 연다. 경로 변수는 주소에서 임의로 바꾸지 않고 이전 화면이 전달한 식별자를 사용한다.
2. 현재 검색 조건과 아래 기본값을 확인한다. **날짜 조건, 업체 조건, 가입 상태** 항목에 필요한 값을 입력하고 **검색**을 누른다.
3. 결과의 **회사명** 링크를 눌러 해당 회사 상세로 이동한다. 페이지 이동·검색 조건 변경 후에는 현재 조건과 조회 대상을 다시 확인한다.

**이 화면에서 유의할 업무 규칙**: 날짜·업체·가입 상태 조건으로 검색한다. 상세에서 회사 설정을 확인하며 회사정보 변경내역과 전체 회원 조회는 연결된 별도 화면으로 이동한다.

**반출**: 적용된 검색 조건과 반출 범위를 확인한 후 다운로드한다. 사유 입력창이 표시되면 업무 사유를 입력한다. 사유 등록 실패·파일 오류는 성공으로 간주하지 않고 다운로드 결과를 확인한다.

**상세 진입 지점**: 검색 결과의 **회사명 링크**를 누른다. 회사 상세의 **회사정보 변경내역**, **전체 회원 조회**는 각각 별도 문서의 경로로 이동한다.

## 4) 입력·표시 데이터

**검증 시 표시된 날짜 필터**: 시작일 `2026-10-09`, 종료일 `2026-11-09`. 검증 날짜·조건 복원에 따른 표시값이며 모든 실행의 고정 기본값을 뜻하지 않는다.

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
|---|---|---|---|
| 날짜 조건 | 입력·선택(조건부 검증 별도) | 화면 타입 selectWithDateRange; 선택: 전체=ALL, 가입일=JOIN_DATE; 초기값 selectValue=ALL; dateRange=startDate=오늘부터 1개월 전; endDate=오늘 | `dateCondition`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/BonabankCompanyListPage.tsx#L110) |
| 업체 조건 | 입력·선택(조건부 검증 별도) | 화면 타입 selectWithInput; 선택: 전체=ALL, 회사명=COMPANY_NAME, 사업자번호=BUSINESS_NUMBER; 초기값 selectValue=BUSINESS_NUMBER; inputValue=빈값 | `companyCondition`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/BonabankCompanyListPage.tsx#L124) |
| 가입 상태 | 입력·선택(조건부 검증 별도) | 화면 타입 checkbox; API 타입 String?; 선택: 회원사=MEMBER, 탈퇴 회원사=WITHDRAWN; 초기값 MEMBER, WITHDRAWN | `joinStatus`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/BonabankCompanyListPage.tsx#L151) |
| 번호 | 출력 | API 타입 Int | `rowNumber`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/BonabankCompanyListPage.tsx#L186) |
| 사업자번호 | 출력 | API 타입 String? | `businessNumber`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/BonabankCompanyListPage.tsx#L193) |
| 회사명 | 출력 | API 타입 String? | `companyName`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/BonabankCompanyListPage.tsx#L209) |
| 가입일 | 출력 | API 타입 String? | `joinDate`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/BonabankCompanyListPage.tsx#L227) |
| 가입상태 | 출력 | API 타입 String?; 초기값 MEMBER, WITHDRAWN | `joinStatus`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/BonabankCompanyListPage.tsx#L234) |
| 사용가능여부 | 출력 | API 타입 String? | `isAvailable`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/BonabankCompanyListPage.tsx#L241) |

**복합 검색·폼의 초기 상태**

| 초기값 근거 | 기본 상태 |
|---|---|
| [createDefaultFilters](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/BonabankCompanyListPage.tsx#L51) | dateCondition=selectValue=ALL; dateRange=startDate=오늘부터 1개월 전; endDate=오늘; companyCondition=selectValue=BUSINESS_NUMBER; inputValue=빈값; joinStatus=MEMBER, WITHDRAWN |

화면 필드 키와 API 필드명이 다른 경우 변환은 Hook/API의 검색·저장 매핑에서 수행된다. 요청·응답 필드와 DB 컬럼 매핑은 아래 API 계약 및 DB 객체 계약에 연결했다.

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
|---|---|---|---|
| 보나뱅크 회사 정보 목록 (SP-side 페이징) | [GET /api/v1/bonabank/companies](../../references/api-contracts.md#api012); `/bonabank/company` / `VIEW` | `dateConditionType, startDate, endDate, companyConditionType, companyConditionValue, joinStatuses, page, size` → `content, totalElements, totalPages, page, size, rowNumber, companyId, businessNumber, companyName, joinDate, joinStatus, isAvailable` | Mapper 프로시저의 정적 테이블 쓰기 미검출; 동적 SQL의 런타임 대상은 미확정 |
| 보나뱅크 회사 정보 엑셀 다운로드 | [GET /api/v1/bonabank/companies/download](../../references/api-contracts.md#api013); `/bonabank/company` / `EXCEL_DOWNLOAD` | `dateConditionType, startDate, endDate, companyConditionType, companyConditionValue, joinStatuses, page, size` → `응답 DTO·파일/처리 결과 계약 참조` | Mapper 프로시저의 정적 테이블 쓰기 미검출; 동적 SQL의 런타임 대상은 미확정 |
| 보나뱅크 회사 등록번호 원문 조회 | [POST /api/v1/bonabank/companies/{id}/sensitive-values/reveal](../../references/api-contracts.md#api191); `/bonabank/company` / `UNMASK` | `field` → `field, value` | 쓰기 대상 smartwork.dbo.sw_log_access_event |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
|---|---|---|---|
| [SmartBill3.dbo.upAdmSB_SchCom_bona](../../references/database-contracts.md#db245) | `@page int IN, @top int IN, @fromDate varchar(10) IN, @toDate varchar(10) IN, @strItem varchar(100) IN, @strContents varchar(100) IN, @cStatus varchar(1) IN` | 확정한 테이블 쓰기 없음. 참조: migration_etcasp.dbo.migration_mapping_company, smartbill3.dbo.company, smartbill3.dbo.member 동적 SQL 포함, 런타임 조합 대상 미확정. | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SmartBill3.dbo.upAdmSB_SchCom_bona_Excel](../../references/database-contracts.md#db246) | `@fromDate varchar(10) IN, @toDate varchar(10) IN, @strItem varchar(100) IN, @strContents varchar(100) IN, @cStatus varchar(1) IN` | 확정한 테이블 쓰기 없음. 참조: migration_etcasp.dbo.migration_mapping_company, sb_dti.dbo.company_dticonfig, smartbill3.dbo.company, smartbill3.dbo.member 동적 SQL 포함, 런타임 조합 대상 미확정. | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.usp_sw_log_access_event_insert](../../references/database-contracts.md#db294) | `@EVENT_TYPE varchar(30) IN, @STATUS varchar(20) IN, @USER_ID bigint IN, @MEMBER_ID nvarchar(50) IN, @USER_NAME nvarchar(100) IN, @DEPARTMENT_NAME nvarchar(100) IN, @PAGE_TITLE nvarchar(200) IN, @PATH nvarchar(500) IN, @MENU_PATH nvarchar(500) IN, @MENU_LABEL nvarchar(200) IN, @CATEGORY_NAME nvarchar(200) IN, @SUB_CATEGORY_NAME nvarchar(200) IN, @MENU_ORDER int IN, @IP_ADDRESS varchar(45) IN, @USER_AGENT nvarchar(1000) IN, @BROWSER varchar(100) IN, @OS varchar(100) IN, @REFERRER nvarchar(500) IN, @DETAIL nvarchar(1000) IN, @RESULT int OUT, @COUNTS_AS_VISIT bit IN` | 쓰기: smartwork.dbo.sw_log_access_event. 참조: smartwork.dbo.sw_log_access_event | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SMARTBILL3.dbo.COMPANY](../../references/database-contracts.md#db197) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.company | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [MIGRATION_ETCASP.dbo.MIGRATION_MAPPING_COMPANY](../../references/database-contracts.md#db001) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: migration_etcasp.dbo.migration_mapping_company | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |

위 DB 계약 링크에는 실제 파라미터 타입·기본값·IN/OUT, Mapper 결과 컬럼, RETURN 바인딩, 참조 테이블·하위 프로시저·정의 필터/정렬을 기록했다. DTO·Service·Repository·Mapper의 상세 호출 경로는 각 API 계약에서 확인한다.

**민감정보**: 기본 응답의 마스킹 값을 유지한다. 원문은 전용 reveal API와 UNMASK 등 추가 권한·사유·감사 로그를 확인한 뒤 조회한다. 화면·캡처·문의 문서에 원문을 남기지 않는다.

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
|---|---|---|
| 결과가 없거나 기대 건수와 다름 | 적용된 검색 기준·기간·탭·대상 상태·서버 필터·페이징·목록/다운로드 조건 | 조건을 다시 확인하고 조회한다. 지속되면 경로·작업 시각·마스킹한 식별자·필터를 업무/기술 담당에게 전달한다. |
| 메뉴·버튼 미표시 또는 접근 거부 | 사용자 그룹의 메뉴 접근·VIEW 및 API별 PROCESS/EXECUTE/DELETE/EXCEL_DOWNLOAD/UNMASK 등 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. 프런트 버튼 표시만으로 서버 권한을 판단하지 않는다. |
| 저장·삭제·외부 실행의 결과가 불명확 | 대상 현재 상태·중복 요청·감사 이력·API 오류·파일/외부 소비 로그 | 기존 반영 여부를 먼저 조회한다. 중복 발송·초기화·금액 처리를 피하기 위해 기술 담당 확인 후 재시도한다. |

## 7) 검증·출처

**브라우저 검증(2026-11-09)**: 화면 대조. [경로별 결과와 제한](../../references/browser-verification.md#page041). 역할별 권한 거부·저장 성공·파일 반출·외부 연계 완료는 이 결과로 보장하지 않는다.

| 검증 항목 | 근거·환경 | 상태·확인일 |
|---|---|---|
| 대상 선정 | 사용자가 WBS 탭 내용으로 제공한 텍스트의 No. 138, 139; [선정 태스크](../../inventory/wbs-tasks.csv) | 제공 텍스트 확인 2026-11-09. 원본 Excel의 탭/병합 셀을 독립 재열람한 것은 아님. |
| 메뉴·라우트·화면 | [menuConfig.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts); [BonabankRoutes.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/BonabankRoutes.tsx); [BonabankCompanyListPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/BonabankCompanyListPage.tsx) | 코드 확인 2026-11-09, 기준 dc216b313 |
| 기능·권한·API | 이 문서의 API 계약 링크 및 연결 Hook/API·Controller·DTO·Service·Repository·Mapper | 코드 확인 2026-11-09. 조회 요청·화면 대조 범위는 아래 브라우저 근거 참조. 권한 계정별 허용·거부 및 변경 요청 실행은 미확인. |
| DB 정의 | [개발 DB 계약](../../references/database-contracts.md), 이 문서의 연결 객체 | 개발 DB 정의 확인 2026-11-09. 동적 SQL·CLR 내부·정의 미공개 참조의 미확정 범위는 객체별 기록; 후속 확인 DB 담당. |
| 브라우저 화면·배포 환경 | 로컬 인증 계정·Playwright CLI; [화면별 검증표](../../references/browser-verification.md#page041) | 화면 대조, 2026-11-09. 배포본·타 역할·업무 변경 결과는 미확인. |
| 업무 프로시저·쓰기·외부 결과 | 격리된 검증 환경·테스트 데이터의 실행 결과 | 미확인: 명시적인 저장·삭제·발송·초기화 요청은 실행하지 않음. 브라우저 GET의 업무 조회 프로시저·조회수·감사 기록은 별도 영향으로 구분. 격리 환경에서 기술 담당 확인. |

코드 확인과 DB 정의 확인은 실행 성공·업무 승인·다른 환경 적용을 보장하지 않는다. 업무·기술 담당 검토 후 조사 목록의 상태를 완료로 변경한다.

브라우저 직접 근거: [settled-static-recheck](../../evidence/browser/static-stable.json). 경로·고정 버튼명·입력 속성·표 머리글·API 상태를 보관했고 실제 데이터 값·식별자·인증정보는 제외했다.

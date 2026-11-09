# [SB 고객관리] 회사 정보 (조회·관리) 관리자 매뉴얼

작성 기준: `dc216b313` · 확인일 2026-11-09 · 조사 상태 **검토 대기**. 코드·개발 DB 정의 확인. 브라우저: **화면 대조**; 저장·발송 등 업무 실행 결과는 미검증이다.

## 1) 화면 기본 정보

### 도메인 이해

스마트빌을 이용하는 회사와 그 회사에 속한 회원의 가입 상태·서비스 설정을 관리하는 업무다. 고객 문의가 들어왔을 때 어느 회사·회원의 문제인지 식별하고, 회사 단위 설정과 회원 단위 권한을 나누어 확인한다.

| 구분 | 설명 |
|---|---|
| 업무 영역 | 스마트빌 회사·회원 관리 · SB 고객관리 > 스마트빌 회원·회사정보 관리 > 회사 정보 |
| 주요 대상·용어 | 회사: 서비스를 이용하는 사업자 / 회원: 회사에 소속된 사용자 / 사업자번호: 회사를 찾는 업무 식별값 |
| 업무 흐름 | 회사 또는 업로드 결과 찾기 → 가입·소속·설정 확인 → 필요한 관리 작업 → 결과·이력 확인 |
| 이 페이지의 역할 | 회사 정보 업무의 진입 화면이다. 회사별 가입·미납·발행 예정 상태와 서비스 설정·소속 회원을 확인한다. 같은 메뉴의 팝업·탭은 이 문서에서, 독립 상세·등록·수정 화면은 관련 문서에서 다룬다. |
| 관련 업무와 구분 | 거래업체 파일의 가입 여부 확인과 회사·회원의 실제 신규 가입은 다른 작업이다. 회사 번호와 회원 번호를 서로 대신 사용하지 않는다. |

도메인 설명 근거: 이 문서 7번의 현재 메뉴·라우트·화면 및 API·업무 규칙 소스. [전체 도메인 지도](../../references/domain-overview.md#company). 설명 보강일 2026-11-09; 기존 실행 검증 범위와 미확인 상태는 변경하지 않았다.

### 화면 정보

| 항목 | 작성 내용 |
|---|---|
| 업무 도메인·목적 | 스마트빌 회사의 가입·미납·발행 예정 상태를 조회하고 회사별 서비스 설정과 관리자 정보를 관리한다. |
| 메뉴·화면 경로 | SB 고객관리 > 스마트빌 회원·회사정보 관리 > 회사 정보; `/company-management/company-info`; 메뉴 또는 관련 화면에서 진입한다. |
| 화면 유형·담당 | 조회·관리; WBS 작업자 유지윤. 업무·기술 담당 팀명은 원문에 없어 배포 전 해당 도메인 담당자가 확정한다. |
| 관련 화면 | [상세](company-info__by-id.md); [변경 이력](company-info__by-id__change-history.md); [전체 회원 조회](company-info__by-companyId__members.md); [회원 권한 조회](company-info__by-companyKey__member-permissions.md) |

WBS 근거: No. 17, 18, 19, 20, 21, 22, 23, 24 (사용자가 제공한 텍스트 행 36, 37, 38, 39, 40, 41, 42, 43). API 개발/화면 개발의 중복 행은 같은 화면으로 통합했다.

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
|---|---|---|
| 화면 진입·조회 | `/company-management/company-info` 메뉴 접근·하위 경로 작업 권한. 조회 API는 VIEW, 등록/수정 경로는 PROCESS 등 아래 서버 액션과 라우트 가드를 함께 적용한다. | 로그인된 관리자 계정; 아래 검색·입력 항목을 준비한다. |
| 다운로드 | `/company-management/company-info`; 엑셀 download 화면 게이트. 다운로드/업로드 API의 서버 권한과 사유 입력을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |

서버가 최종 권한을 검사한다. 버튼 모양(kind)으로 권한을 추정하지 않는다. 특히 등록·수정이 PROCESS를 사용하는 API와 EXECUTE·UNMASK·EXCEL_DOWNLOAD는 서로 구분한다.

## 3) 화면 사용 절차

**검증 시 화면 버튼**: 검색, 초기화. 화면 상태·대상에 따라 달라지며 아래 작업 절차와 권한 조건을 함께 확인한다.

1. `SB 고객관리 > 스마트빌 회원·회사정보 관리 > 회사 정보` 메뉴를 연다. 경로 변수는 주소에서 임의로 바꾸지 않고 이전 화면이 전달한 식별자를 사용한다.
2. 최초 진입 시 자동조회하지 않는다. 아래 검색 항목을 입력한 후 **검색**을 누른다.
3. 결과 행에서 업무 대상을 선택하여 관련 상세 화면으로 이동한다. 페이지 이동·검색 조건 변경 후에는 현재 조건과 조회 대상을 다시 확인한다.

**이 화면에서 유의할 업무 규칙**: 진입 시 자동조회하지 않는다. 업체 조건 또는 가입일 기간 중 하나 이상을 입력하고 검색한다. 회사 상세에서는 SSO·WEB-HOOK·요금제 변경내역·자동이체 이력 팝업과 전체 회원·회원 권한·회사정보 변경내역 화면을 구분하여 사용한다.

**반출**: 적용된 검색 조건과 반출 범위를 확인한 후 다운로드한다. 사유 입력창이 표시되면 업무 사유를 입력한다. 사유 등록 실패·파일 오류는 성공으로 간주하지 않고 다운로드 결과를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
|---|---|---|---|
| 날짜 조건 | 입력·선택(조건부 검증 별도) | 화면 타입 selectWithDateRange; 선택: 전체=all, 가입일=registrationDate; 초기값 selectValue=all; dateRange=startDate=빈값; endDate=빈값 | `dateCondition`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/pages/CompanyInfoPage.tsx#L128) |
| 업체 조건 | 입력·선택(조건부 검증 별도) | 화면 타입 selectWithInput; 선택: 전체=all, 사업자번호=comRegno, 회사명=comName; 초기값 selectValue=comRegno; inputValue=빈값 | `companyCondition`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/pages/CompanyInfoPage.tsx#L140) |
| 미납 상태 | 입력·선택(조건부 검증 별도) | 화면 타입 radio; API 타입 List<String>?; 기본 null; 선택: 전체=all, 사용가능=01, 사용 불가 (미납)=0299; 초기값 all | `unpaidStatus`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/pages/CompanyInfoPage.tsx#L161) |
| 가입 상태 | 입력·선택(조건부 검증 별도) | 화면 타입 radio; API 타입 List<String>?; 기본 null; 선택: 전체=all, 회원사=N, 탈퇴 회원사=Y; 초기값 all | `membershipStatus`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/pages/CompanyInfoPage.tsx#L172) |
| 발행 예정 | 입력·선택(조건부 검증 별도) | 화면 타입 radio; API 타입 String?; 기본 null; 선택: 전체=all, 사용=used, 미사용=unused; 초기값 all | `issuanceSchedule`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/pages/CompanyInfoPage.tsx#L183) |
| No | 출력 | API 타입 Int | `no`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CompanyInfoTable.tsx#L68) |
| 사업자번호 | 출력 | API 타입 String | `businessNumber`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CompanyInfoTable.tsx#L69) |
| 회사명 | 출력 | API 타입 String | `companyName`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CompanyInfoTable.tsx#L88) |
| 가입일 | 출력 | API 타입 String | `registrationDate`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CompanyInfoTable.tsx#L89) |
| 가입상태 | 출력 | API 타입 List<String>?; 기본 null; 초기값 all | `membershipStatus`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CompanyInfoTable.tsx#L93) |
| 사용가능여부 | 출력 | API 타입 List<String>?; 기본 null; 초기값 all | `unpaidStatus`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CompanyInfoTable.tsx#L94) |
| 전자세금계산서 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `pricingPlan.etax`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CompanyInfoTable.tsx#L98) |
| 전자계약 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `pricingPlan.econtract`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CompanyInfoTable.tsx#L99) |
| 자동이체 | 출력 | API 타입 String | `autoPayment`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CompanyInfoTable.tsx#L100) |
| 전자계약 추가용량 | 출력 | API 타입 Int | `econtractAdditionalCapacity`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CompanyInfoTable.tsx#L101) |
| 요금제 | 출력 | API 타입 PricingPlanDto | `pricingPlan`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CompanyInfoTable.tsx#L116) |

**복합 검색·폼의 초기 상태**

| 초기값 근거 | 기본 상태 |
|---|---|
| [getDefaultFilterValues](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/pages/CompanyInfoPage.tsx#L73) | dateCondition=selectValue=all; dateRange=startDate=빈값; endDate=빈값; companyCondition=selectValue=comRegno; inputValue=빈값; unpaidStatus=all; membershipStatus=all; issuanceSchedule=all |

화면 필드 키와 API 필드명이 다른 경우 변환은 Hook/API의 검색·저장 매핑에서 수행된다. 요청·응답 필드와 DB 컬럼 매핑은 아래 API 계약 및 DB 객체 계약에 연결했다.

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
|---|---|---|---|
| 회사 정보 목록 조회 | [GET /api/v1/company-management/company-info](../../references/api-contracts.md#api044); `/company-management/company-info` / `VIEW` | `dateConditionType, companyConditionType, searchKeyword, fromDate, toDate, unpaidStatus, membershipStatus, issuanceSchedule` → `content, totalElements, id, no, companyName, businessNumber, registrationDate, membershipStatus, unpaidStatus, unpaidStatusCode, pricingPlan, autoPayment, econtractAdditionalCapaci` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 사용불가 해제 | [POST /api/v1/company-management/company-info/{companyId}/unpaid-release](../../references/api-contracts.md#api208); `/company-management/company-info` / `PROCESS` | `reason` → `응답 DTO·파일/처리 결과 계약 참조` | 쓰기 대상 smartbill3.dbo.com_result_text, smartbill3.dbo.company, smartbill3.dbo.company_history |
| 회사 정보 CSV 다운로드 | [GET /api/v1/company-management/company-info/download](../../references/api-contracts.md#api045); `/company-management/company-info` / `EXCEL_DOWNLOAD` | `dateConditionType, companyConditionType, searchKeyword, fromDate, toDate, unpaidStatus, membershipStatus, issuanceSchedule` → `응답 DTO·파일/처리 결과 계약 참조` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 회사 등록번호 원문 조회 | [POST /api/v1/company-management/company-info/{comNo}/sensitive-values/reveal](../../references/api-contracts.md#api203); `/company-management/company-info` / `UNMASK` | `field` → `field, value` | 쓰기 대상 smartwork.dbo.sw_log_access_event |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
|---|---|---|---|
| [smartwork.dbo.usp_company_info_list_select](../../references/database-contracts.md#db284) | `@STRITEM varchar(100) IN, @STRCONTENTS varchar(100) IN, @FROMDATE varchar(10) IN, @TODATE varchar(10) IN, @CSTATUS varchar(10) IN, @CSTATUS2 varchar(10) IN, @DTI_BILLTYPE varchar(10) IN, @DCT_BILLTYPE varchar(10) IN, @ISSUANCE_SCHEDULE varchar(10) IN` | 확정한 테이블 쓰기 없음. 참조: sb_dti.dbo.company_dticonfig, smartbill3.dbo.cms_account_cub, smartbill3.dbo.company, smartbill3.dbo.settlement | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SmartBill3.dbo.upAdmSB_PaymentRevocation](../../references/database-contracts.md#db236) | `@com_no int IN, @sw_no int IN, @rlstTxt varchar(200) IN` | 쓰기: smartbill3.dbo.com_result_text, smartbill3.dbo.company, smartbill3.dbo.company_history. 참조: smartbill3.dbo.com_result_text, smartbill3.dbo.company, smartbill3.dbo.company_history | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.usp_sw_log_access_event_insert](../../references/database-contracts.md#db294) | `@EVENT_TYPE varchar(30) IN, @STATUS varchar(20) IN, @USER_ID bigint IN, @MEMBER_ID nvarchar(50) IN, @USER_NAME nvarchar(100) IN, @DEPARTMENT_NAME nvarchar(100) IN, @PAGE_TITLE nvarchar(200) IN, @PATH nvarchar(500) IN, @MENU_PATH nvarchar(500) IN, @MENU_LABEL nvarchar(200) IN, @CATEGORY_NAME nvarchar(200) IN, @SUB_CATEGORY_NAME nvarchar(200) IN, @MENU_ORDER int IN, @IP_ADDRESS varchar(45) IN, @USER_AGENT nvarchar(1000) IN, @BROWSER varchar(100) IN, @OS varchar(100) IN, @REFERRER nvarchar(500) IN, @DETAIL nvarchar(1000) IN, @RESULT int OUT, @COUNTS_AS_VISIT bit IN` | 쓰기: smartwork.dbo.sw_log_access_event. 참조: smartwork.dbo.sw_log_access_event | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SMARTBILL3.dbo.COMPANY](../../references/database-contracts.md#db197) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.company | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |

위 DB 계약 링크에는 실제 파라미터 타입·기본값·IN/OUT, Mapper 결과 컬럼, RETURN 바인딩, 참조 테이블·하위 프로시저·정의 필터/정렬을 기록했다. DTO·Service·Repository·Mapper의 상세 호출 경로는 각 API 계약에서 확인한다.

**민감정보**: 기본 응답의 마스킹 값을 유지한다. 원문은 전용 reveal API와 UNMASK 등 추가 권한·사유·감사 로그를 확인한 뒤 조회한다. 화면·캡처·문의 문서에 원문을 남기지 않는다.

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
|---|---|---|
| 검색 결과가 없습니다. | [문구·처리 코드](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CompanyInfoTable.tsx#L132); 현재 조건·대상·권한 확인 | 검색·조회 오류면 조건을 확인 후 재조회. 변경·발송 결과가 불명확하면 처리 여부와 이력을 확인한 뒤 재시도 여부를 판단한다. |
| 결과가 없거나 기대 건수와 다름 | 적용된 검색 기준·기간·탭·대상 상태·서버 필터·페이징·목록/다운로드 조건 | 조건을 다시 확인하고 조회한다. 지속되면 경로·작업 시각·마스킹한 식별자·필터를 업무/기술 담당에게 전달한다. |
| 메뉴·버튼 미표시 또는 접근 거부 | 사용자 그룹의 메뉴 접근·VIEW 및 API별 PROCESS/EXECUTE/DELETE/EXCEL_DOWNLOAD/UNMASK 등 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. 프런트 버튼 표시만으로 서버 권한을 판단하지 않는다. |
| 저장·삭제·외부 실행의 결과가 불명확 | 대상 현재 상태·중복 요청·감사 이력·API 오류·파일/외부 소비 로그 | 기존 반영 여부를 먼저 조회한다. 중복 발송·초기화·금액 처리를 피하기 위해 기술 담당 확인 후 재시도한다. |

## 7) 검증·출처

**브라우저 검증(2026-11-09)**: 화면 대조. [경로별 결과와 제한](../../references/browser-verification.md#page001). 역할별 권한 거부·저장 성공·파일 반출·외부 연계 완료는 이 결과로 보장하지 않는다.

| 검증 항목 | 근거·환경 | 상태·확인일 |
|---|---|---|
| 대상 선정 | 사용자가 WBS 탭 내용으로 제공한 텍스트의 No. 17, 18, 19, 20, 21, 22, 23, 24; [선정 태스크](../../inventory/wbs-tasks.csv) | 제공 텍스트 확인 2026-11-09. 원본 Excel의 탭/병합 셀을 독립 재열람한 것은 아님. |
| 메뉴·라우트·화면 | [menuConfig.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts); [CustomerRoutes.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/CustomerRoutes.tsx); [CompanyInfoPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/pages/CompanyInfoPage.tsx) | 코드 확인 2026-11-09, 기준 dc216b313 |
| 기능·권한·API | 이 문서의 API 계약 링크 및 연결 Hook/API·Controller·DTO·Service·Repository·Mapper | 코드 확인 2026-11-09. 조회 요청·화면 대조 범위는 아래 브라우저 근거 참조. 권한 계정별 허용·거부 및 변경 요청 실행은 미확인. |
| DB 정의 | [개발 DB 계약](../../references/database-contracts.md), 이 문서의 연결 객체 | 개발 DB 정의 확인 2026-11-09. 동적 SQL·CLR 내부·정의 미공개 참조의 미확정 범위는 객체별 기록; 후속 확인 DB 담당. |
| 브라우저 화면·배포 환경 | 로컬 인증 계정·Playwright CLI; [화면별 검증표](../../references/browser-verification.md#page001) | 화면 대조, 2026-11-09. 배포본·타 역할·업무 변경 결과는 미확인. |
| 업무 프로시저·쓰기·외부 결과 | 격리된 검증 환경·테스트 데이터의 실행 결과 | 미확인: 명시적인 저장·삭제·발송·초기화 요청은 실행하지 않음. 브라우저 GET의 업무 조회 프로시저·조회수·감사 기록은 별도 영향으로 구분. 격리 환경에서 기술 담당 확인. |

코드 확인과 DB 정의 확인은 실행 성공·업무 승인·다른 환경 적용을 보장하지 않는다. 업무·기술 담당 검토 후 조사 목록의 상태를 완료로 변경한다.

브라우저 직접 근거: [settled-static-recheck](../../evidence/browser/static-stable.json). 경로·고정 버튼명·입력 속성·표 머리글·API 상태를 보관했고 실제 데이터 값·식별자·인증정보는 제외했다.

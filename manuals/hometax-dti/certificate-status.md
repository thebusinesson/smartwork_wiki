# [SB 서비스관리] 인증서 등록 현황 조회 (조회·관리) 관리자 매뉴얼

작성 기준: `dc216b313` · 확인일 2026-11-09 · 조사 상태 **검토 대기**. 코드·개발 DB 정의 확인. 브라우저: **화면 대조**; 저장·발송 등 업무 실행 결과는 미검증이다.

## 1) 화면 기본 정보

### 도메인 이해

홈택스 수집을 위해 등록된 업체 인증서와 수집·과금 연계 등록 상태를 함께 점검한다.

| 구분 | 설명 |
|---|---|
| 업무 영역 | 설치형 홈택스 세금계산서 수집 > 인증서 등록 현황 조회 조회·관리 |
| 언제 사용하는가 | 인증서를 등록했는데 수집이나 관련 서비스 등록이 확인되지 않을 때 |
| 주요 대상·데이터 | 등록일·스크래핑 허브업체·등록 회사·사업자번호·과금등록·영업대표가 등록 대상과 연결 상태를 나타낸다. |
| 업무 흐름 | 등록 기간·업체·과금 조건 검색 → 인증서 등록 대상 확인 → 연계 등록 상태 비교 |
| 이 페이지의 역할 | 수집 인증서 등록 중 **인증서 등록 현황 조회 조회·관리** 단계. 홈택스 수집을 위해 등록된 업체 인증서와 수집·과금 연계 등록 상태를 함께 점검한다. |
| 판단 결과·다음 업무 | 미등록·연계 누락 여부를 확인한 후 인증키 설정 또는 해당 업무 담당에게 전달한다. |
| 다른 화면과의 구분 | 등록되어 있다는 사실은 인증서가 현재 유효하거나 로그인에 성공한다는 뜻이 아니다. |

설명 근거: [CertificateRegistrationStatusPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/CertificateRegistrationStatusPage.tsx), 이 문서 4·5·7번의 항목·API·업무 규칙. [상위 업무 영역](../../references/domain-overview.md#hometax)은 공통 배경이며 현재 화면의 데이터·동작은 위 설명을 따른다. 설명 수정일 **2026-11-10**; 새 업무 실행 검증을 수행한 것은 아니다.

### 화면 정보

| 항목 | 작성 내용 |
|---|---|
| 업무 도메인·목적 | 홈택스 수집을 위해 등록된 업체 인증서와 수집·과금 연계 등록 상태를 함께 점검한다. |
| 메뉴·화면 경로 | SB 서비스관리 > 홈택스 DTI 수집 > 인증서 등록 현황 조회; `/hometax-dti/certificate-status`; 메뉴 또는 관련 화면에서 진입한다. |
| 화면 유형·담당 | 조회·관리; WBS 작업자 유지윤. 업무·기술 담당 팀명은 원문에 없어 배포 전 해당 도메인 담당자가 확정한다. |
| 관련 화면 | 같은 메뉴에 별도 독립 경로 없음. 팝업·탭은 이 문서 참조. |

WBS 근거: No. 128 (사용자가 제공한 텍스트 행 162). API 개발/화면 개발의 중복 행은 같은 화면으로 통합했다.

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
|---|---|---|
| 화면 진입·조회 | `/hometax-dti/certificate-status` 메뉴 접근·하위 경로 작업 권한. 조회 API는 VIEW, 등록/수정 경로는 PROCESS 등 아래 서버 액션과 라우트 가드를 함께 적용한다. | 로그인된 관리자 계정; 아래 검색·입력 항목을 준비한다. |
| 엑셀 다운로드 | `/hometax-dti/certificate-status`; 엑셀 download 화면 게이트. 다운로드/업로드 API의 서버 권한과 사유 입력을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |

서버가 최종 권한을 검사한다. 버튼 모양(kind)으로 권한을 추정하지 않는다. 특히 등록·수정이 PROCESS를 사용하는 API와 EXECUTE·UNMASK·EXCEL_DOWNLOAD는 서로 구분한다.

## 3) 화면 사용 절차

**검증 시 화면 버튼**: 검색, 초기화, 엑셀 다운로드. 화면 상태·대상에 따라 달라지며 아래 작업 절차와 권한 조건을 함께 확인한다.

1. `SB 서비스관리 > 홈택스 DTI 수집 > 인증서 등록 현황 조회` 메뉴를 연다. 경로 변수는 주소에서 임의로 바꾸지 않고 이전 화면이 전달한 식별자를 사용한다.
2. 현재 검색 조건과 아래 기본값을 확인한다. **등록일자, 스크래핑 허브업체명, 등록 회사명, 사업자번호, 매입통합/스크래핑 과금등록, 영업대표, 허브업체명, 운영여부** 항목에 필요한 값을 입력하고 **검색**을 누른다.
3. 결과 표·탭·팝업에서 대상의 상태와 합계·이력을 확인한다. 다른 조회 조건으로 바꾼 경우 다시 검색하여 결과를 갱신한다.

**이 화면에서 유의할 업무 규칙**: 등록일자는 기본 한 달 전~오늘이다. 회사명·사업자번호·영업대표·운영여부 등을 지정하고 인증서 등록 현황을 검색한다. 엑셀 반출 시 화면 조건과 반출 사유를 확인한다.

**반출**: 적용된 검색 조건과 반출 범위를 확인한 후 다운로드한다. 사유 입력창이 표시되면 업무 사유를 입력한다. 사유 등록 실패·파일 오류는 성공으로 간주하지 않고 다운로드 결과를 확인한다.

## 4) 입력·표시 데이터

**검증 시 표시된 날짜 필터**: 시작일 `2026-10-09`, 종료일 `2026-11-09`. 검증 날짜·조건 복원에 따른 표시값이며 모든 실행의 고정 기본값을 뜻하지 않는다.

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
|---|---|---|---|
| 등록일자 | 입력·선택(조건부 검증 별도) | 화면 타입 dateRange; 초기값 startDate=오늘부터 1개월 전; endDate=오늘 | `dateRange`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/CertificateRegistrationStatusPage.tsx#L101) |
| 스크래핑 허브업체명 | 입력·선택(조건부 검증 별도) | 화면 타입 text; API 타입 String?; 기본 null; 서버 검증 @field:Size(max = 50); 초기값 빈값 | `scrapHubName`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/CertificateRegistrationStatusPage.tsx#L102) |
| 등록 회사명 | 입력·선택(조건부 검증 별도) | 화면 타입 text; API 타입 String?; 기본 null; 서버 검증 @field:Size(max = 50); 초기값 빈값 | `comName`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/CertificateRegistrationStatusPage.tsx#L108) |
| 사업자번호 | 입력·선택(조건부 검증 별도) | 화면 타입 text; 최대 10자; API 타입 String?; 기본 null; 서버 검증 @field:Size(max = 13); 초기값 빈값 | `comRegno`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/CertificateRegistrationStatusPage.tsx#L109) |
| 매입통합/스크래핑 과금등록 | 입력·선택(조건부 검증 별도) | 화면 타입 radio; API 타입 String?; 기본 null; 서버 검증 @field:Pattern(regexp = "^(Y\|N\|)$", message = "usecount 는 Y/N 또는 빈값이어야 합니다."); 선택: 전체=all, 등록=Y, 미등록=N; 초기값 all | `usecount`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/CertificateRegistrationStatusPage.tsx#L121) |
| 영업대표 | 입력·선택(조건부 검증 별도) | 화면 타입 select; API 타입 Int; 기본 0; 서버 검증 @field:Min(value = 0, message = "swNo 는 0 이상이어야 합니다."); 선택: 전체=0; 초기값 0 | `swNo`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/CertificateRegistrationStatusPage.tsx#L126) |
| 허브업체명 | 입력·선택(조건부 검증 별도) | 화면 타입 text; API 타입 String?; 기본 null; 서버 검증 @field:Size(max = 50); 초기값 빈값 | `hubName`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/CertificateRegistrationStatusPage.tsx#L127) |
| 운영여부 | 입력·선택(조건부 검증 별도) | 화면 타입 select; API 타입 String?; 기본 null; 서버 검증 @field:Pattern(regexp = "^(O\|T\|)$", message = "klass 는 O/T 또는 빈값이어야 합니다."); 선택: 전체=all, 운영=O, 테스트=T; 초기값 all | `klass`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/CertificateRegistrationStatusPage.tsx#L133) |
| 스크래핑 허브업체명 | 출력 | API 타입 String? | `hubRealname`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/CertificateRegistrationStatusPage.tsx#L234) |
| 등록 회사명 | 출력 | API 타입 String?; 기본 null; 서버 검증 @field:Size(max = 50); 초기값 빈값 | `comName`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/CertificateRegistrationStatusPage.tsx#L241) |
| 사업자번호 | 출력 | API 타입 String?; 기본 null; 서버 검증 @field:Size(max = 13); 초기값 빈값 | `comRegno`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/CertificateRegistrationStatusPage.tsx#L248) |
| 등록일 | 출력 | API 타입 String? | `cdate`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/CertificateRegistrationStatusPage.tsx#L255) |
| 과금등록 | 출력 | API 타입 String?; 기본 null; 서버 검증 @field:Pattern(regexp = "^(Y\|N\|)$", message = "usecount 는 Y/N 또는 빈값이어야 합니다."); 초기값 all | `usecount`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/CertificateRegistrationStatusPage.tsx#L262) |
| 허브업체명 | 출력 | API 타입 String? | `bnsSite`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/CertificateRegistrationStatusPage.tsx#L269) |
| 영업대표 | 출력 | API 타입 String? | `sname`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/CertificateRegistrationStatusPage.tsx#L276) |
| 운영여부 | 출력 | API 타입 String?; 기본 null; 서버 검증 @field:Pattern(regexp = "^(O\|T\|)$", message = "klass 는 O/T 또는 빈값이어야 합니다."); 초기값 all | `klass`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/CertificateRegistrationStatusPage.tsx#L291) |

입력 검증 근거: [CertificateRegistrationStatusPage.checks.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/service/hometaxdti/CertificateRegistrationStatusPage.checks.ts). 프런트 검증과 서버 DTO 제약이 다르면 서버 검증이 최종 기준이다.

**복합 검색·폼의 초기 상태**

| 초기값 근거 | 기본 상태 |
|---|---|
| [createDefaultFilters](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/CertificateRegistrationStatusPage.tsx#L42) | dateRange=startDate=오늘부터 1개월 전; endDate=오늘; scrapHubName=빈값; comName=빈값; comRegno=빈값; usecount=all; swNo=0; hubName=빈값; klass=all |

화면 필드 키와 API 필드명이 다른 경우 변환은 Hook/API의 검색·저장 매핑에서 수행된다. 요청·응답 필드와 DB 컬럼 매핑은 아래 API 계약 및 DB 객체 계약에 연결했다.

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
|---|---|---|---|
| 인증서 등록 현황 목록 조회 (in-memory 페이징) | [GET /api/v1/sb-service/hometax-dti-installed/certificate-registration](../../references/api-contracts.md#api085); `/hometax-dti/certificate-status` / `VIEW` | `fromDate, toDate, scrapHubName, comRegno, comName, usecount, hubName, swNo, klass, page, size` → `content, totalElements, totalPages, page, size, sbKey, comRegno, comName, hubName, hubRealname, cdate, usecount, bnsSite, sname, swNo, klass` | Mapper 프로시저의 정적 테이블 쓰기 미검출; 동적 SQL의 런타임 대상은 미확정 |
| 영업대표 콤보 옵션 조회 | [GET /api/v1/sb-service/hometax-dti-installed/certificate-registration/sales-reps](../../references/api-contracts.md#api087); `/hometax-dti/certificate-status` / `VIEW` | `경로·쿼리·본문 계약 참조` → `응답 DTO·파일/처리 결과 계약 참조` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 인증서 등록 현황 엑셀 다운로드 | [GET /api/v1/sb-service/hometax-dti-installed/certificate-registration/download](../../references/api-contracts.md#api086); `/hometax-dti/certificate-status` / `EXCEL_DOWNLOAD` | `fromDate, toDate, scrapHubName, comRegno, comName, usecount, hubName, swNo, klass, page, size` → `응답 DTO·파일/처리 결과 계약 참조` | Mapper 프로시저의 정적 테이블 쓰기 미검출; 동적 SQL의 런타임 대상은 미확정 |
| 영업대표명 원문 조회 | [POST /api/v1/sb-service/hometax-dti-installed/certificate-registration/{sbKey}/sensitive-values/reveal](../../references/api-contracts.md#api225); `/hometax-dti/certificate-status` / `UNMASK` | `field` → `field, value` | 쓰기 대상 smartwork.dbo.sw_log_access_event |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
|---|---|---|---|
| [SB_SCRAPER.dbo.SSP_VIEW_BILL_MANAGEMENT](../../references/database-contracts.md#db180) | `@FROM_DATE varchar(10) IN, @TO_DATE varchar(10) IN, @SCRAPHUB_NAME varchar(50) IN, @COM_REGNO varchar(10) IN, @COM_NAME varchar(50) IN, @USECOUNT char(1) IN, @HUB_NAME varchar(50) IN, @SW_NO int IN, @CLASS char(1) IN` | 확정한 테이블 쓰기 없음. 참조: office.dbo.business, office.dbo.mng_hub, office.dbo.sawon, sb_bill.dbo.dti_share_auto_charge, sb_scraper.dbo.use_company_detail, sb_scraper.dbo.use_company_info, smartbill3.dbo.company 동적 SQL 포함, 런타임 조합 대상 미확정. | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [OFFICE.dbo.upApp_BusinessSawonList](../../references/database-contracts.md#db011) | IN 파라미터 없음 | 확정한 테이블 쓰기 없음. 참조: office.dbo.dept_detail, office.dbo.dept_manager, office.dbo.sawon | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.usp_sw_log_access_event_insert](../../references/database-contracts.md#db294) | `@EVENT_TYPE varchar(30) IN, @STATUS varchar(20) IN, @USER_ID bigint IN, @MEMBER_ID nvarchar(50) IN, @USER_NAME nvarchar(100) IN, @DEPARTMENT_NAME nvarchar(100) IN, @PAGE_TITLE nvarchar(200) IN, @PATH nvarchar(500) IN, @MENU_PATH nvarchar(500) IN, @MENU_LABEL nvarchar(200) IN, @CATEGORY_NAME nvarchar(200) IN, @SUB_CATEGORY_NAME nvarchar(200) IN, @MENU_ORDER int IN, @IP_ADDRESS varchar(45) IN, @USER_AGENT nvarchar(1000) IN, @BROWSER varchar(100) IN, @OS varchar(100) IN, @REFERRER nvarchar(500) IN, @DETAIL nvarchar(1000) IN, @RESULT int OUT, @COUNTS_AS_VISIT bit IN` | 쓰기: smartwork.dbo.sw_log_access_event. 참조: smartwork.dbo.sw_log_access_event | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_SCRAPER.dbo.USE_COMPANY_INFO](../../references/database-contracts.md#db181) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: sb_scraper.dbo.use_company_info | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [OFFICE.dbo.MNG_HUB](../../references/database-contracts.md#db007) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: office.dbo.mng_hub | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [OFFICE.dbo.BUSINESS](../../references/database-contracts.md#db003) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: office.dbo.business | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [OFFICE.dbo.SAWON](../../references/database-contracts.md#db009) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: office.dbo.sawon | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |

위 DB 계약 링크에는 실제 파라미터 타입·기본값·IN/OUT, Mapper 결과 컬럼, RETURN 바인딩, 참조 테이블·하위 프로시저·정의 필터/정렬을 기록했다. DTO·Service·Repository·Mapper의 상세 호출 경로는 각 API 계약에서 확인한다.

**민감정보**: 기본 응답의 마스킹 값을 유지한다. 원문은 전용 reveal API와 UNMASK 등 추가 권한·사유·감사 로그를 확인한 뒤 조회한다. 화면·캡처·문의 문서에 원문을 남기지 않는다.

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
|---|---|---|
| 결과가 없거나 기대 건수와 다름 | 적용된 검색 기준·기간·탭·대상 상태·서버 필터·페이징·목록/다운로드 조건 | 조건을 다시 확인하고 조회한다. 지속되면 경로·작업 시각·마스킹한 식별자·필터를 업무/기술 담당에게 전달한다. |
| 메뉴·버튼 미표시 또는 접근 거부 | 사용자 그룹의 메뉴 접근·VIEW 및 API별 PROCESS/EXECUTE/DELETE/EXCEL_DOWNLOAD/UNMASK 등 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. 프런트 버튼 표시만으로 서버 권한을 판단하지 않는다. |
| 저장·삭제·외부 실행의 결과가 불명확 | 대상 현재 상태·중복 요청·감사 이력·API 오류·파일/외부 소비 로그 | 기존 반영 여부를 먼저 조회한다. 중복 발송·초기화·금액 처리를 피하기 위해 기술 담당 확인 후 재시도한다. |

## 7) 검증·출처

**브라우저 검증(2026-11-09)**: 화면 대조. [경로별 결과와 제한](../../references/browser-verification.md#page037). 역할별 권한 거부·저장 성공·파일 반출·외부 연계 완료는 이 결과로 보장하지 않는다.

| 검증 항목 | 근거·환경 | 상태·확인일 |
|---|---|---|
| 대상 선정 | 사용자가 WBS 탭 내용으로 제공한 텍스트의 No. 128; [선정 태스크](../../inventory/wbs-tasks.csv) | 제공 텍스트 확인 2026-11-09. 원본 Excel의 탭/병합 셀을 독립 재열람한 것은 아님. |
| 메뉴·라우트·화면 | [menuConfig.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts); [HometaxDtiRoutes.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/HometaxDtiRoutes.tsx); [CertificateRegistrationStatusPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/CertificateRegistrationStatusPage.tsx) | 코드 확인 2026-11-09, 기준 dc216b313 |
| 기능·권한·API | 이 문서의 API 계약 링크 및 연결 Hook/API·Controller·DTO·Service·Repository·Mapper | 코드 확인 2026-11-09. 조회 요청·화면 대조 범위는 아래 브라우저 근거 참조. 권한 계정별 허용·거부 및 변경 요청 실행은 미확인. |
| DB 정의 | [개발 DB 계약](../../references/database-contracts.md), 이 문서의 연결 객체 | 개발 DB 정의 확인 2026-11-09. 동적 SQL·CLR 내부·정의 미공개 참조의 미확정 범위는 객체별 기록; 후속 확인 DB 담당. |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-9c4bedaaecd96d4d) | Demo 메타데이터 7/7개 확인 · Dev와 계약 차이 2개 · 2026-11-11 |
| 브라우저 화면·배포 환경 | 로컬 인증 계정·Playwright CLI; [화면별 검증표](../../references/browser-verification.md#page037) | 화면 대조, 2026-11-09. 배포본·타 역할·업무 변경 결과는 미확인. |
| 업무 프로시저·쓰기·외부 결과 | 격리된 검증 환경·테스트 데이터의 실행 결과 | 미확인: 명시적인 저장·삭제·발송·초기화 요청은 실행하지 않음. 브라우저 GET의 업무 조회 프로시저·조회수·감사 기록은 별도 영향으로 구분. 격리 환경에서 기술 담당 확인. |

코드 확인과 DB 정의 확인은 실행 성공·업무 승인·다른 환경 적용을 보장하지 않는다. 업무·기술 담당 검토 후 조사 목록의 상태를 완료로 변경한다.

브라우저 직접 근거: [settled-static-recheck](../../evidence/browser/static-stable.json). 경로·고정 버튼명·입력 속성·표 머리글·API 상태를 보관했고 실제 데이터 값·식별자·인증정보는 제외했다.

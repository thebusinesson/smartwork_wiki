# [SB 서비스관리] 연동업체 관리 (등록) 관리자 매뉴얼

작성 기준: `dc216b313` · 확인일 2026-11-09 · 조사 상태 **검토 대기**. 코드·개발 DB 정의 확인. 브라우저: **화면 대조**; 저장·발송 등 업무 실행 결과는 미검증이다.

## 1) 화면 기본 정보

### 도메인 이해

거래 상대방과 확인할 채권잔액 문서 및 이를 주고받는 연동 상태를 관리하는 업무다. 확인서 조회, 이용 담당자의 권한, 연동업체 설정, 송수신 장애를 같은 업무 흐름 안에서 조사한다.

| 구분 | 설명 |
|---|---|
| 업무 영역 | 채권잔액 확인 서비스 · SB 서비스관리 > 채권잔액 확인 서비스 > 연동업체 관리 |
| 주요 대상·용어 | 채권잔액 확인서: 거래 잔액 확인에 쓰는 문서 / 연동업체: 시스템 연결 대상 업체 / 참조번호·conversation ID: 문서 또는 송수신 건을 추적하는 값 |
| 업무 흐름 | 확인서·연동업체 찾기 → 담당 권한·송수신 상태 확인 → 로그·전문·장애 정보 조사 → 필요한 조치 |
| 이 페이지의 역할 | 채권잔액 연동업체 업무에 새 항목을 등록하는 단계다. 조회 목록과 구분하여 필수 입력·대상 정보를 준비하고 저장 결과를 확인한다. |
| 관련 업무와 구분 | 문서의 잔액 확인과 실제 입금·환불 처리는 다른 업무다. 송신 요청·접수·상대방 처리 결과를 한 상태로 간주하지 않는다. |

도메인 설명 근거: 이 문서 7번의 현재 메뉴·라우트·화면 및 API·업무 규칙 소스. [전체 도메인 지도](../../references/domain-overview.md#bond). 설명 보강일 2026-11-09; 기존 실행 검증 범위와 미확인 상태는 변경하지 않았다.

### 화면 정보

| 항목 | 작성 내용 |
|---|---|
| 업무 도메인·목적 | 채권잔액 서비스 연동업체와 연동 기간·라우팅을 등록하고 관리한다. |
| 메뉴·화면 경로 | SB 서비스관리 > 채권잔액 확인 서비스 > 연동업체 관리; `/bond-service/drc-company-link/new`; 메뉴 또는 관련 화면에서 진입한다. |
| 화면 유형·담당 | 등록; WBS 작업자 유지윤. 업무·기술 담당 팀명은 원문에 없어 배포 전 해당 도메인 담당자가 확정한다. |
| 관련 화면 | [조회·관리](drc-company-link.md); [상세](drc-company-link__by-comNo.md) |

WBS 근거: No. 111, 112, 113 (사용자가 제공한 텍스트 행 142, 143, 144). API 개발/화면 개발의 중복 행은 같은 화면으로 통합했다.

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
|---|---|---|
| 화면 진입·조회 | `/bond-service/drc-company-link` 메뉴 접근·하위 경로 작업 권한. 조회 API는 VIEW, 등록/수정 경로는 PROCESS 등 아래 서버 액션과 라우트 가드를 함께 적용한다. | 로그인된 관리자 계정; 아래 검색·입력 항목을 준비한다. |
| 등록업체 추가 | `/bond-service/drc-company-link`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 등록업체 삭제 | `/bond-service/drc-company-link`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 선택 | `/bond-service/drc-company-link`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 저장 | `/bond-service/drc-company-link`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 목록 | `/bond-service/drc-company-link`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 취소 | `/bond-service/drc-company-link`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |

서버가 최종 권한을 검사한다. 버튼 모양(kind)으로 권한을 추정하지 않는다. 특히 등록·수정이 PROCESS를 사용하는 API와 EXECUTE·UNMASK·EXCEL_DOWNLOAD는 서로 구분한다.

## 3) 화면 사용 절차

**검증 시 화면 버튼**: 검색, 선택, 저장, 목록. 화면 상태·대상에 따라 달라지며 아래 작업 절차와 권한 조건을 함께 확인한다.

1. 관련 화면에서 대상 또는 작업을 선택하여 `/bond-service/drc-company-link/new`로 이동한다. 경로 변수는 주소에서 임의로 바꾸지 않고 이전 화면이 전달한 식별자를 사용한다.
2. **사업자 번호/회사명, 시스템 정보, SYSTEM ID:, CLIENT CODE:, COMPANY CODE:, URL:, PORT:, 관련 허브업체 / 업체 코드, 비회원 발송 사용 여부**의 입력값을 확인한다. 신규 값을 입력한다. 필수값과 형식 오류가 표시되면 해당 항목을 수정한다.
3. **저장**을 누르고 확인창이 있으면 대상·작업을 확인한다. 첨부가 있으면 기존 파일의 유지·삭제·교체 선택을 함께 확인한다.
4. 처리 결과 메시지를 확인한 뒤 목록 또는 상세에서 결과를 다시 조회한다. 오류가 나면 아래 예외 대응과 API 오류를 확인하고 중복 저장 전에 기존 처리 여부를 확인한다.

**이 화면에서 유의할 업무 규칙**: 신규 등록과 기존 업체 상세/수정이 같은 컴포넌트를 사용한다. 업체·시스템·연동 기간·라우팅 정보를 확인하고, 허브업체 선택 팝업에서 등록 대상을 지정한 뒤 저장한다.

공통 폼이 등록·수정·상세 입력값 조회 함수를 함께 포함할 수 있다. 아래 API 표에 공통 구현의 다른 모드가 표시되어도 현재 경로의 작업으로 모두 실행하는 것은 아니다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
|---|---|---|---|
| 사업자 번호/회사명 | 입력·필수 | 화면 타입 text; API 타입 String; 기본 ""; 서버 검증 @field:Size(min = 2, max = 50, message = "검색어는 2~50자여야 합니다."); 초기값 빈값 | `keyword`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/DrcCompanyLinkWritePage.tsx#L50) |
| 업체 검색결과 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/DrcCompanyLinkWritePage.tsx#L380) |
| 연동 등록 업체 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/DrcCompanyLinkWritePage.tsx#L399) |
| 업체 정보 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/DrcCompanyLinkWritePage.tsx#L425) |
| 시스템 정보 | 입력·선택(조건부 검증 별도) | 길이·형식·조건부 필수는 검증 코드와 API DTO 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/DrcCompanyLinkWritePage.tsx#L449) |
| SYSTEM ID: | 입력·선택(조건부 검증 별도) | 길이·형식·조건부 필수는 검증 코드와 API DTO 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/DrcCompanyLinkWritePage.tsx#L479) |
| CLIENT CODE: | 입력·선택(조건부 검증 별도) | 길이·형식·조건부 필수는 검증 코드와 API DTO 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/DrcCompanyLinkWritePage.tsx#L483) |
| COMPANY CODE: | 입력·선택(조건부 검증 별도) | 길이·형식·조건부 필수는 검증 코드와 API DTO 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/DrcCompanyLinkWritePage.tsx#L487) |
| URL: | 입력·선택(조건부 검증 별도) | 길이·형식·조건부 필수는 검증 코드와 API DTO 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/DrcCompanyLinkWritePage.tsx#L517) |
| PORT: | 입력·선택(조건부 검증 별도) | 길이·형식·조건부 필수는 검증 코드와 API DTO 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/DrcCompanyLinkWritePage.tsx#L524) |
| 관련 허브업체 / 업체 코드 | 입력·선택(조건부 검증 별도) | 길이·형식·조건부 필수는 검증 코드와 API DTO 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/DrcCompanyLinkWritePage.tsx#L561) |
| 비회원 발송 사용 여부 | 입력·선택(조건부 검증 별도) | 길이·형식·조건부 필수는 검증 코드와 API DTO 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/DrcCompanyLinkWritePage.tsx#L582) |

입력 검증 근거: [DrcCompanyLinkWritePage.checks.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/service/bondservice/DrcCompanyLinkWritePage.checks.ts), [DrcCompanyLinkWritePage.schema.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/service/bondservice/DrcCompanyLinkWritePage.schema.ts). 프런트 검증과 서버 DTO 제약이 다르면 서버 검증이 최종 기준이다.

화면 필드 키와 API 필드명이 다른 경우 변환은 Hook/API의 검색·저장 매핑에서 수행된다. 요청·응답 필드와 DB 컬럼 매핑은 아래 API 계약 및 DB 객체 계약에 연결했다.

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
|---|---|---|---|
| 허브업체 목록 조회 | [GET /api/v1/bond-service/drc-company-links/hub-companies](../../references/api-contracts.md#api033); `/bond-service/drc-company-link` / `VIEW` | `경로·쿼리·본문 계약 참조` → `응답 DTO·파일/처리 결과 계약 참조` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 등록용 업체 검색 | [GET /api/v1/bond-service/drc-company-links/company-search](../../references/api-contracts.md#api032); `/bond-service/drc-company-link` / `VIEW` | `keyword` → `응답 DTO·파일/처리 결과 계약 참조` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 연동업체 상세 조회 | [GET /api/v1/bond-service/drc-company-links/{comNo}](../../references/api-contracts.md#api034); `/bond-service/drc-company-link` / `VIEW` | `경로·쿼리·본문 계약 참조` → `comNo, comName, comRegno, systemId, startRoutingDate, endRoutingDate, routingUrl, port, activeYn, sapClientCode, sapCompanyCode, sapSystemId, hubId, nmYn, outYn, modifiedBy, modifi` | 기존 항목 입력값 조회 공통 구현; 신규 진입에서는 대상 없음. Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 연동업체 저장 (등록/수정) | [POST /api/v1/bond-service/drc-company-links](../../references/api-contracts.md#api195); `/bond-service/drc-company-link` / `PROCESS` | `comNos, systemId, startRoutingDate, endRoutingDate, routingUrl, port, activeYn, sapClientCode, sapCompanyCode, sapSystemId, hubId, nmYn, outYn` → `응답 DTO·파일/처리 결과 계약 참조` | 쓰기 대상 office.dbo.mng_company_except, office.dbo.mng_hub_etc_detail, sb_drc.dbo.drc_company_link |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
|---|---|---|---|
| [OFFICE.dbo.upPJT_BNSHubList_mnghub](../../references/database-contracts.md#db058) | `@BNS_PRODUCT varchar(20) IN` | 확정한 테이블 쓰기 없음. 참조: office.dbo.business, office.dbo.function_code, office.dbo.mng_hub | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.UspDrcCompanySearchForRegist](../../references/database-contracts.md#db326) | `@Keyword varchar(50) IN` | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.company, smartbill3.dbo.settlement | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DRC.dbo.upStm_LstDRCCompanyLinkInfo](../../references/database-contracts.md#db132) | `@Com_No varchar(10) IN` | 확정한 테이블 쓰기 없음. 참조: sb_drc.dbo.drc_company_link | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [OFFICE.dbo.upGW_SawonInfo](../../references/database-contracts.md#db035) | `@sw_no int IN` | 확정한 테이블 쓰기 없음. 참조: office.dbo.sawon | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.UspDrcCompanyLinkSearch](../../references/database-contracts.md#db324) | `@SchCode char(1) IN, @SchContent varchar(50) IN` | 확정한 테이블 쓰기 없음. 참조: sb_drc.dbo.drc_company_link, smartbill3.dbo.company | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DRC.dbo.upStm_SavDRCCompanyLink](../../references/database-contracts.md#db133) | `@Com_No int IN, @System_ID varchar(10) IN, @Start_RoutingDate datetime IN, @End_RoutingDate datetime IN, @RoutingURL varchar(100) IN, @Port varchar(5) IN, @Active_YN varchar(1) IN, @SAPClientCode varchar(3) IN, @SAPCompanyCode varchar(4) IN, @SAPSystemId varchar(10) IN, @Biz_UUser varchar(12) IN, @Hub_Id int IN, @Trouble_Yn varchar(1) IN, @Trouble_Msg varchar(1000) IN, @NM_YN varchar(4) IN, @OUT_YN varchar(4) IN` | 쓰기: office.dbo.mng_company_except, office.dbo.mng_hub_etc_detail, sb_drc.dbo.drc_company_link. 참조: office.dbo.mng_company_except, office.dbo.mng_hub_etc_detail, sb_drc.dbo.drc_company_link, smartbill3.dbo.company | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |

위 DB 계약 링크에는 실제 파라미터 타입·기본값·IN/OUT, Mapper 결과 컬럼, RETURN 바인딩, 참조 테이블·하위 프로시저·정의 필터/정렬을 기록했다. DTO·Service·Repository·Mapper의 상세 호출 경로는 각 API 계약에서 확인한다.

## 6) 예외 상황과 운영 확인

**빈값 입력 재현**: 연동 등록 업체를 1개 이상 선택해주세요.; 시스템을 선택해주세요.; 연동기간을 선택해주세요.; 라우팅 URL을 입력해주세요.; PORT 번호를 입력해주세요.. 빈 입력에서 확인한 클라이언트 오류이며 저장 요청 성공·서버 검증 재현은 아니다.

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
|---|---|---|
| 결과가 없거나 기대 건수와 다름 | 적용된 검색 기준·기간·탭·대상 상태·서버 필터·페이징·목록/다운로드 조건 | 조건을 다시 확인하고 조회한다. 지속되면 경로·작업 시각·마스킹한 식별자·필터를 업무/기술 담당에게 전달한다. |
| 메뉴·버튼 미표시 또는 접근 거부 | 사용자 그룹의 메뉴 접근·VIEW 및 API별 PROCESS/EXECUTE/DELETE/EXCEL_DOWNLOAD/UNMASK 등 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. 프런트 버튼 표시만으로 서버 권한을 판단하지 않는다. |
| 저장·삭제·외부 실행의 결과가 불명확 | 대상 현재 상태·중복 요청·감사 이력·API 오류·파일/외부 소비 로그 | 기존 반영 여부를 먼저 조회한다. 중복 발송·초기화·금액 처리를 피하기 위해 기술 담당 확인 후 재시도한다. |

## 7) 검증·출처

**브라우저 검증(2026-11-09)**: 화면 대조. [경로별 결과와 제한](../../references/browser-verification.md#page027). 역할별 권한 거부·저장 성공·파일 반출·외부 연계 완료는 이 결과로 보장하지 않는다.

| 검증 항목 | 근거·환경 | 상태·확인일 |
|---|---|---|
| 대상 선정 | 사용자가 WBS 탭 내용으로 제공한 텍스트의 No. 111, 112, 113; [선정 태스크](../../inventory/wbs-tasks.csv) | 제공 텍스트 확인 2026-11-09. 원본 Excel의 탭/병합 셀을 독립 재열람한 것은 아님. |
| 메뉴·라우트·화면 | [menuConfig.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts); [BondServiceRoutes.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/BondServiceRoutes.tsx); [DrcCompanyLinkWritePage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/DrcCompanyLinkWritePage.tsx) | 코드 확인 2026-11-09, 기준 dc216b313 |
| 기능·권한·API | 이 문서의 API 계약 링크 및 연결 Hook/API·Controller·DTO·Service·Repository·Mapper | 코드 확인 2026-11-09. 조회 요청·화면 대조 범위는 아래 브라우저 근거 참조. 권한 계정별 허용·거부 및 변경 요청 실행은 미확인. |
| DB 정의 | [개발 DB 계약](../../references/database-contracts.md), 이 문서의 연결 객체 | 개발 DB 정의 확인 2026-11-09. 동적 SQL·CLR 내부·정의 미공개 참조의 미확정 범위는 객체별 기록; 후속 확인 DB 담당. |
| 브라우저 화면·배포 환경 | 로컬 인증 계정·Playwright CLI; [화면별 검증표](../../references/browser-verification.md#page027) | 화면 대조, 2026-11-09. 배포본·타 역할·업무 변경 결과는 미확인. |
| 업무 프로시저·쓰기·외부 결과 | 격리된 검증 환경·테스트 데이터의 실행 결과 | 미확인: 명시적인 저장·삭제·발송·초기화 요청은 실행하지 않음. 브라우저 GET의 업무 조회 프로시저·조회수·감사 기록은 별도 영향으로 구분. 격리 환경에서 기술 담당 확인. |

코드 확인과 DB 정의 확인은 실행 성공·업무 승인·다른 환경 적용을 보장하지 않는다. 업무·기술 담당 검토 후 조사 목록의 상태를 완료로 변경한다.

브라우저 직접 근거: [settled-static-recheck](../../evidence/browser/static-stable.json). 경로·고정 버튼명·입력 속성·표 머리글·API 상태를 보관했고 실제 데이터 값·식별자·인증정보는 제외했다.

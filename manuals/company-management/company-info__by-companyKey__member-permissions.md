# [SB 고객관리] 회사 정보 (회원 권한 조회) 관리자 매뉴얼

작성 기준: `dc216b313` · 확인일 2026-11-09 · 조사 상태 **검토 대기**. 코드·개발 DB 정의 확인. 브라우저: **화면 대조**; 저장·발송 등 업무 실행 결과는 미검증이다.

## 1) 화면 기본 정보

### 도메인 이해

한 회사의 회원에게 전자세금계산서·전자계약 업무 권한이 어떻게 부여되어 있는지 서비스별로 확인·관리한다.

| 구분 | 설명 |
|---|---|
| 업무 영역 | 스마트빌 회사·회원 관리 > 회사 정보 회원 권한 조회 |
| 언제 사용하는가 | 회원이 회사에는 속해 있지만 특정 서비스의 조회·처리 권한에 문제가 있을 때 |
| 주요 대상·데이터 | 회사 키·회원과 전자세금계산서/전자계약 권한 정보가 대상이다. tab 쿼리는 두 서비스 중 현재 보는 권한을 구분한다. |
| 업무 흐름 | 회사·회원 확인 → 서비스 권한 탭 선택 → 회원별 권한 내용 확인 → 필요한 권한 보완 |
| 이 페이지의 역할 | 회사 정보 중 **회사 정보 회원 권한 조회** 단계. 한 회사의 회원에게 전자세금계산서·전자계약 업무 권한이 어떻게 부여되어 있는지 서비스별로 확인·관리한다. |
| 판단 결과·다음 업무 | 문제 서비스의 권한을 확인하고 저장 작업은 결과를 재조회한다. 회사 정보 또는 이전 화면으로 복귀한다. |
| 다른 화면과의 구분 | 회원 가입·탈퇴 상태와 서비스별 업무 권한은 다르며 두 탭의 권한을 서로 같은 값으로 취급하지 않는다. |

**탭·영역·팝업별 업무 구분**

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
|---|---|---|---|
| 전자세금계산서 권한 정보 | 세금계산서 업무 접근 문제를 확인할 때 | 선택 회사의 회원별 세금계산서 권한; tab=etax | 문제 회원의 이 서비스 권한을 확인·보완하고 저장 후 재조회한다. |
| 전자계약 권한 정보 | 전자계약 업무 접근 문제를 확인할 때 | 같은 회사의 회원별 전자계약 권한; tab=econtract | 회원 소속이 같아도 세금계산서 권한으로 대신 판단하지 않는다. |

설명 근거: [MemberPermissionsPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/pages/MemberPermissionsPage.tsx), 이 문서 4·5·7번의 항목·API·업무 규칙. [상위 업무 영역](../../references/domain-overview.md#company)은 공통 배경이며 현재 화면의 데이터·동작은 위 설명을 따른다. 설명 수정일 **2026-11-10**; 새 업무 실행 검증을 수행한 것은 아니다.

### 화면 정보

| 항목 | 작성 내용 |
|---|---|
| 업무 도메인·목적 | 한 회사의 회원에게 전자세금계산서·전자계약 업무 권한이 어떻게 부여되어 있는지 서비스별로 확인·관리한다. |
| 메뉴·화면 경로 | SB 고객관리 > 스마트빌 회원·회사정보 관리 > 회사 정보; `/company-management/company-info/:companyKey/member-permissions`; 목록에서 선택한 대상의 경로 변수를 유지하여 진입한다. |
| 화면 유형·담당 | 회원 권한 조회; WBS 작업자 유지윤. 업무·기술 담당 팀명은 원문에 없어 배포 전 해당 도메인 담당자가 확정한다. |
| 관련 화면 | [조회·관리](company-info.md); [상세](company-info__by-id.md); [변경 이력](company-info__by-id__change-history.md); [전체 회원 조회](company-info__by-companyId__members.md) |

WBS 근거: No. 17, 18, 19, 20, 21, 22, 23, 24 (사용자가 제공한 텍스트 행 36, 37, 38, 39, 40, 41, 42, 43). API 개발/화면 개발의 중복 행은 같은 화면으로 통합했다.

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
|---|---|---|
| 화면 진입·조회 | `/company-management/company-info` 메뉴 접근·하위 경로 작업 권한. 조회 API는 VIEW, 등록/수정 경로는 PROCESS 등 아래 서버 액션과 라우트 가드를 함께 적용한다. | 로그인된 관리자 계정; companyKey 식별자는 이전 화면에서 선택한다. |
| 변경 | `/company-management/company-info`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 이전 | `/company-management/company-info`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 권한 변경 | `/company-management/company-info`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |

서버가 최종 권한을 검사한다. 버튼 모양(kind)으로 권한을 추정하지 않는다. 특히 등록·수정이 PROCESS를 사용하는 API와 EXECUTE·UNMASK·EXCEL_DOWNLOAD는 서로 구분한다.

## 3) 화면 사용 절차

**검증 시 화면 버튼**: 권한 변경, 변경. 화면 상태·대상에 따라 달라지며 아래 작업 절차와 권한 조건을 함께 확인한다.

1. 관련 화면에서 대상 또는 작업을 선택하여 `/company-management/company-info/:companyKey/member-permissions`로 이동한다. 경로 변수는 주소에서 임의로 바꾸지 않고 이전 화면이 전달한 식별자를 사용한다.
2. 대상의 기본 정보·상태·표시 항목을 확인한다. 목록의 식별자와 상세 대상이 일치하는지 확인한다.
3. **변경, 권한 변경** 중 필요한 작업을 선택한다. 버튼의 표시·활성 조건과 아래 API별 권한을 확인한다. 저장·삭제·외부 호출 전에는 대상과 현재 상태를 재확인한다.
4. 작업 결과 또는 다운로드 파일을 확인하고 관련 목록으로 돌아가 변경된 상태를 다시 조회한다.

**이 화면에서 유의할 업무 규칙**: 진입 시 자동조회하지 않는다. 업체 조건 또는 가입일 기간 중 하나 이상을 입력하고 검색한다. 회사 상세에서는 SSO·WEB-HOOK·요금제 변경내역·자동이체 이력 팝업과 전체 회원·회원 권한·회사정보 변경내역 화면을 구분하여 사용한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
|---|---|---|---|
| 화면 표시·작업 입력 | 복합 컴포넌트 | 세부 항목은 [MemberPermissionsPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/pages/MemberPermissionsPage.tsx)의 구성 요소·검증 규칙과 API 계약 표 참조 | 정적으로 추출한 고정 label/key 쌍 없음. 업무 담당 화면 검토 필요 |

입력 검증 근거: [PermissionSectionCard.schema.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/customer/company/components/PermissionSectionCard.schema.ts). 프런트 검증과 서버 DTO 제약이 다르면 서버 검증이 최종 기준이다.

화면 필드 키와 API 필드명이 다른 경우 변환은 Hook/API의 검색·저장 매핑에서 수행된다. 요청·응답 필드와 DB 컬럼 매핑은 아래 API 계약 및 DB 객체 계약에 연결했다.

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
|---|---|---|---|
| 회원 권한 조회 | [GET /api/v1/company-management/company-info/{companyKey}/member-permissions](../../references/api-contracts.md#api054); `/company-management/company-info` / `VIEW` | `경로·쿼리·본문 계약 참조` → `응답 DTO·파일/처리 결과 계약 참조` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 회원 권한 수정 | [PUT /api/v1/company-management/company-info/{companyKey}/member-permissions](../../references/api-contracts.md#api265); `/company-management/company-info` / `PROCESS` | `경로·쿼리·본문 계약 참조` → `응답 DTO·파일/처리 결과 계약 참조` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 회사 등록번호 원문 조회 | [POST /api/v1/company-management/company-info/{comNo}/sensitive-values/reveal](../../references/api-contracts.md#api203); `/company-management/company-info` / `UNMASK` | `field` → `field, value` | 쓰기 대상 smartwork.dbo.sw_log_access_event |
| 회사 소속 회원 민감정보 원문 조회 | [POST /api/v1/company-management/company-info/{comNo}/members/{memNo}/sensitive-values/reveal](../../references/api-contracts.md#api202); `/company-management/company-info` / `UNMASK` | `field` → `field, value` | 쓰기 대상 smartwork.dbo.sw_log_access_event |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
|---|---|---|---|
| [SmartBill3.dbo.COMPANY](../../references/database-contracts.md#db197) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.company | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Office.dbo.upGW_MemAdminInfo4](../../references/database-contracts.md#db027) | `@comId varchar(10) IN` | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.company, smartbill3.dbo.dept_manager, smartbill3.dbo.member | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Office.dbo.upGW_MemAdminInfo3](../../references/database-contracts.md#db026) | `@com_no int IN` | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.member, smartbill3.dbo.tax_admin | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Office.dbo.upGW_MemAdminInfo2](../../references/database-contracts.md#db025) | `@service_type varchar(3) IN, @com_no int IN` | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.company, smartbill3.dbo.dept_manager, smartbill3.dbo.member | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_COMMON.dbo.upSBAdm_LstDeptMng](../../references/database-contracts.md#db101) | `@DIVISION varchar(3) IN, @COM_NO varchar(10) IN, @DEPT_NO varchar(10) IN` | 확정한 테이블 쓰기 없음. 참조: sb_dti.dbo.dept_admin, sb_dti.dbo.dept_member, sb_dti.dbo.service_admin, smartbill3.dbo.member | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Office.dbo.upGW_MemAdminInfo1](../../references/database-contracts.md#db024) | `@com_no int IN` | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.company, smartbill3.dbo.member | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.UspMemberPermissions_Select](../../references/database-contracts.md#db339) | `@COM_NO int IN` | 확정한 테이블 쓰기 없음. 참조: sb_dti.dbo.dept_admin, sb_dti.dbo.dept_member, sb_dti.dbo.dti_right, sb_dti.dbo.service_admin, smartbill3.dbo.member, smartwork.dbo.dct_member_right | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DTI.dbo.COMPANY_QUIT_STATUS](../../references/database-contracts.md#db138) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: sb_dti.dbo.company_quit_status | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SMARTBILL3.dbo.COMPANY](../../references/database-contracts.md#db197) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.company | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Office.dbo.upGW_CompanyINFO](../../references/database-contracts.md#db018) | `@COM_NO varchar(10) IN` | 확정한 테이블 쓰기 없음. 참조: migration_etcasp.dbo.migration_mapping_company, smartbill3.dbo.company, smartbill3.dbo.member | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.usp_sw_log_access_event_insert](../../references/database-contracts.md#db294) | `@EVENT_TYPE varchar(30) IN, @STATUS varchar(20) IN, @USER_ID bigint IN, @MEMBER_ID nvarchar(50) IN, @USER_NAME nvarchar(100) IN, @DEPARTMENT_NAME nvarchar(100) IN, @PAGE_TITLE nvarchar(200) IN, @PATH nvarchar(500) IN, @MENU_PATH nvarchar(500) IN, @MENU_LABEL nvarchar(200) IN, @CATEGORY_NAME nvarchar(200) IN, @SUB_CATEGORY_NAME nvarchar(200) IN, @MENU_ORDER int IN, @IP_ADDRESS varchar(45) IN, @USER_AGENT nvarchar(1000) IN, @BROWSER varchar(100) IN, @OS varchar(100) IN, @REFERRER nvarchar(500) IN, @DETAIL nvarchar(1000) IN, @RESULT int OUT, @COUNTS_AS_VISIT bit IN` | 쓰기: smartwork.dbo.sw_log_access_event. 참조: smartwork.dbo.sw_log_access_event | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SMARTBILL3.dbo.MEMBER](../../references/database-contracts.md#db203) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.member | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |

위 DB 계약 링크에는 실제 파라미터 타입·기본값·IN/OUT, Mapper 결과 컬럼, RETURN 바인딩, 참조 테이블·하위 프로시저·정의 필터/정렬을 기록했다. DTO·Service·Repository·Mapper의 상세 호출 경로는 각 API 계약에서 확인한다.

**민감정보**: 기본 응답의 마스킹 값을 유지한다. 원문은 전용 reveal API와 UNMASK 등 추가 권한·사유·감사 로그를 확인한 뒤 조회한다. 화면·캡처·문의 문서에 원문을 남기지 않는다.

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
|---|---|---|
| 결과가 없거나 기대 건수와 다름 | 적용된 검색 기준·기간·탭·대상 상태·서버 필터·페이징·목록/다운로드 조건 | 조건을 다시 확인하고 조회한다. 지속되면 경로·작업 시각·마스킹한 식별자·필터를 업무/기술 담당에게 전달한다. |
| 메뉴·버튼 미표시 또는 접근 거부 | 사용자 그룹의 메뉴 접근·VIEW 및 API별 PROCESS/EXECUTE/DELETE/EXCEL_DOWNLOAD/UNMASK 등 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. 프런트 버튼 표시만으로 서버 권한을 판단하지 않는다. |
| 저장·삭제·외부 실행의 결과가 불명확 | 대상 현재 상태·중복 요청·감사 이력·API 오류·파일/외부 소비 로그 | 기존 반영 여부를 먼저 조회한다. 중복 발송·초기화·금액 처리를 피하기 위해 기술 담당 확인 후 재시도한다. |

## 7) 검증·출처

**브라우저 검증(2026-11-09)**: 화면 대조. [경로별 결과와 제한](../../references/browser-verification.md#page003). 역할별 권한 거부·저장 성공·파일 반출·외부 연계 완료는 이 결과로 보장하지 않는다.

| 검증 항목 | 근거·환경 | 상태·확인일 |
|---|---|---|
| 대상 선정 | 사용자가 WBS 탭 내용으로 제공한 텍스트의 No. 17, 18, 19, 20, 21, 22, 23, 24; [선정 태스크](../../inventory/wbs-tasks.csv) | 제공 텍스트 확인 2026-11-09. 원본 Excel의 탭/병합 셀을 독립 재열람한 것은 아님. |
| 메뉴·라우트·화면 | [menuConfig.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts); [CustomerRoutes.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/CustomerRoutes.tsx); [MemberPermissionsPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/pages/MemberPermissionsPage.tsx) | 코드 확인 2026-11-09, 기준 dc216b313 |
| 기능·권한·API | 이 문서의 API 계약 링크 및 연결 Hook/API·Controller·DTO·Service·Repository·Mapper | 코드 확인 2026-11-09. 조회 요청·화면 대조 범위는 아래 브라우저 근거 참조. 권한 계정별 허용·거부 및 변경 요청 실행은 미확인. |
| DB 정의 | [개발 DB 계약](../../references/database-contracts.md), 이 문서의 연결 객체 | 개발 DB 정의 확인 2026-11-09. 동적 SQL·CLR 내부·정의 미공개 참조의 미확정 범위는 객체별 기록; 후속 확인 DB 담당. |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-295028eb964e856c) | Demo 메타데이터 11/11개 확인 · Dev와 계약 차이 1개 · 2026-11-11 |
| 브라우저 화면·배포 환경 | 로컬 인증 계정·Playwright CLI; [화면별 검증표](../../references/browser-verification.md#page003) | 화면 대조, 2026-11-09. 배포본·타 역할·업무 변경 결과는 미확인. |
| 업무 프로시저·쓰기·외부 결과 | 격리된 검증 환경·테스트 데이터의 실행 결과 | 미확인: 명시적인 저장·삭제·발송·초기화 요청은 실행하지 않음. 브라우저 GET의 업무 조회 프로시저·조회수·감사 기록은 별도 영향으로 구분. 격리 환경에서 기술 담당 확인. |

코드 확인과 DB 정의 확인은 실행 성공·업무 승인·다른 환경 적용을 보장하지 않는다. 업무·기술 담당 검토 후 조사 목록의 상태를 완료로 변경한다.

브라우저 직접 근거: [settled-detail-revisit](../../evidence/browser/ready-details-stable.json). 경로·고정 버튼명·입력 속성·표 머리글·API 상태를 보관했고 실제 데이터 값·식별자·인증정보는 제외했다.

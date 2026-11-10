# [SB 서비스관리] 회사 정보 (전체 회원 조회) 관리자 매뉴얼

작성 기준: `dc216b313` · 확인일 2026-11-09 · 조사 상태 **검토 대기**. 코드·개발 DB 정의 확인. 브라우저: **화면 대조**; 저장·발송 등 업무 실행 결과는 미검증이다.

## 1) 화면 기본 정보

### 도메인 이해

선택한 보나뱅크 회사의 소속 회원과 상태를 조회하고, 대상 회원의 관리자 역할 변경·탈퇴를 조건과 권한에 따라 처리한다.

| 구분 | 설명 |
|---|---|
| 업무 영역 | 보나뱅크 서비스 운영 > 회사 정보 전체 회원 조회 |
| 언제 사용하는가 | 회사 자체는 맞지만 특정 사용자의 이용·소속·관리자 여부를 확인해야 할 때 |
| 주요 대상·데이터 | 회사·소속 회원 식별값, 가입·휴면·탈퇴 상태와 기업·세금계산서·전자계약·SCM·채권확인 관리자 종류가 대상이다. |
| 업무 흐름 | 회사·회원 확인 → 조회 또는 관리자 변경/탈퇴 작업 구분 → 변경할 관리자 종류와 회원 한 명 또는 탈퇴 대상 확인 → 확인창 처리 → 결과 재조회 |
| 이 페이지의 역할 | 선택한 보나뱅크 회사의 소속 회원과 상태를 조회하고, 대상 회원의 관리자 역할 변경·탈퇴를 조건과 권한에 따라 처리한다. |
| 판단 결과·다음 업무 | 관리자 변경은 관리자 종류를 정하고 회원 한 명을 선택한다. 탈퇴는 선택 회원의 별도 작업이다. PROCESS·대상 상태와 기존 처리 결과를 확인한다. |
| 다른 화면과의 구분 | 회사 설정·서비스별 권한 편집과 다른 회원 역할·탈퇴 처리다. 보나뱅크 진입에서도 회원 목록·관리자 변경·탈퇴는 공통 /company-management/company-info API의 VIEW·PROCESS를 검사하므로 보나뱅크 메뉴 접근·프런트 버튼 권한만으로 서버 권한을 보장하지 않는다. ?mode=admin-change 직접 진입도 처리 권한을 우회하지 않는다. |

설명 근거: [CompanyMembersPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/pages/CompanyMembersPage.tsx), 이 문서 4·5·7번의 항목·API·업무 규칙. [상위 업무 영역](../../references/domain-overview.md#bonabank)은 공통 배경이며 현재 화면의 데이터·동작은 위 설명을 따른다. 설명 수정일 **2026-11-10**; 새 업무 실행 검증을 수행한 것은 아니다.

### 화면 정보

| 항목 | 작성 내용 |
|---|---|
| 업무 도메인·목적 | 선택한 보나뱅크 회사의 소속 회원과 상태를 조회하고, 대상 회원의 관리자 역할 변경·탈퇴를 조건과 권한에 따라 처리한다. |
| 메뉴·화면 경로 | SB 서비스관리 > 보나뱅크 > 회사 정보; `/bonabank/company/:companyId/members`; 목록에서 선택한 대상의 경로 변수를 유지하여 진입한다. |
| 화면 유형·담당 | 전체 회원 조회; WBS 작업자 유지윤. 업무·기술 담당 팀명은 원문에 없어 배포 전 해당 도메인 담당자가 확정한다. |
| 관련 화면 | [조회·관리](company.md); [상세](company__by-id.md); [변경 이력](company__by-id__change-history.md) |

WBS 근거: No. 138, 139 (사용자가 제공한 텍스트 행 174, 175). API 개발/화면 개발의 중복 행은 같은 화면으로 통합했다.

## 2) 사용 권한과 사전 준비

**공통 회원 API 권한**: 보나뱅크 진입에서도 회원 목록은 `/company-management/company-info` VIEW, 관리자 변경·탈퇴는 같은 경로 PROCESS를 서버가 검사한다. 화면의 현재 경로 권한과 공통 API 권한을 함께 확인한다. 원문 조회는 각 실제 호출 endpoint의 권한을 별도로 따른다.

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
|---|---|---|
| 화면 진입·조회 | `/bonabank/company` 메뉴 접근·하위 경로 작업 권한. 조회 API는 VIEW, 등록/수정 경로는 PROCESS 등 아래 서버 액션과 라우트 가드를 함께 적용한다. | 로그인된 관리자 계정; companyId 식별자는 이전 화면에서 선택한다. |
| 변경 | `/bonabank/company`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 이전 | `/bonabank/company`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 탈퇴처리 | `/bonabank/company`; 화면 게이트 PROCESS. 실제 서버 액션은 API별 표 참조. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 회사 관리자 변경 | `/bonabank/company`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |

서버가 최종 권한을 검사한다. 버튼 모양(kind)으로 권한을 추정하지 않는다. 특히 등록·수정이 PROCESS를 사용하는 API와 EXECUTE·UNMASK·EXCEL_DOWNLOAD는 서로 구분한다.

## 3) 화면 사용 절차

**검증 시 화면 버튼**: 회사 관리자 변경. 화면 상태·대상에 따라 달라지며 아래 작업 절차와 권한 조건을 함께 확인한다.

1. 관련 화면에서 대상 또는 작업을 선택하여 `/bonabank/company/:companyId/members`로 이동한다. 경로 변수는 주소에서 임의로 바꾸지 않고 이전 화면이 전달한 식별자를 사용한다.
2. 대상의 기본 정보·상태·표시 항목을 확인한다. 목록의 식별자와 상세 대상이 일치하는지 확인한다.
3. **변경, 탈퇴처리, 회사 관리자 변경** 중 필요한 작업을 선택한다. 버튼의 표시·활성 조건과 아래 API별 권한을 확인한다. 저장·삭제·외부 호출 전에는 대상과 현재 상태를 재확인한다.
4. 작업 결과 또는 다운로드 파일을 확인하고 관련 목록으로 돌아가 변경된 상태를 다시 조회한다.

**이 화면에서 유의할 업무 규칙**: 날짜·업체·가입 상태 조건으로 검색한다. 상세에서 회사 설정을 확인하며 회사정보 변경내역과 전체 회원 조회는 연결된 별도 화면으로 이동한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
|---|---|---|---|
| 실명 | 출력 | API 타입 String | `realName`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CompanyMembersTable.tsx#L72) |
| 닉네임 | 출력 | API 타입 String | `nickname`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CompanyMembersTable.tsx#L78) |
| 아이디 | 출력 | API 타입 String | `userId`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CompanyMembersTable.tsx#L84) |
| 연락처 | 출력 | API 타입 String | `phone`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CompanyMembersTable.tsx#L90) |
| 이메일 | 출력 | API 타입 String | `email`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CompanyMembersTable.tsx#L96) |
| 이관 | 출력 | API 타입 String | `transfer`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CompanyMembersTable.tsx#L102) |
| 가입일 | 출력 | API 타입 String | `joinDate`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CompanyMembersTable.tsx#L112) |
| 탈퇴일 | 출력 | API 타입 String? | `withdrawalDate`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CompanyMembersTable.tsx#L113) |
| 휴면여부 | 출력 | API 타입 String | `dormant`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CompanyMembersTable.tsx#L119) |
| 탈퇴처리 | 출력 | API 타입 Int | `id`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CompanyMembersTable.tsx#L121) |

화면 필드 키와 API 필드명이 다른 경우 변환은 Hook/API의 검색·저장 매핑에서 수행된다. 요청·응답 필드와 DB 컬럼 매핑은 아래 API 계약 및 DB 객체 계약에 연결했다.

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
|---|---|---|---|
| 회사 소속 전체 회원 조회 | [GET /api/v1/company-management/company-info/{companyId}/members](../../references/api-contracts.md#api048); `/company-management/company-info` / `VIEW` | `경로·쿼리·본문 계약 참조` → `companyName, businessNumber, content, totalElements, totalPages, page, size, administrators, id, realName, nickname, userId, email, transfer, phone, joinDate, withdrawalDate, dorma` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 회원 탈퇴처리 | [POST /api/v1/company-management/company-info/{companyId}/members/withdraw](../../references/api-contracts.md#api205); `/company-management/company-info` / `PROCESS` | `memberIds` → `success, data, error` | 쓰기 대상 sb_dti_log.dbo.dormant_member, smartbill3.dbo.member, smartwork.dbo.company_change_log |
| 회사 관리자 변경 | [POST /api/v1/company-management/company-info/{companyId}/members/change-administrator](../../references/api-contracts.md#api204); `/company-management/company-info` / `PROCESS` | `memberIds, roleTypes` → `success, data, error` | 쓰기 대상 sb_dti.dbo.service_admin, smartbill3.dbo.dept_manager, smartbill3.dbo.member, smartbill3.dbo.tax_admin, smartwork.dbo.company_change_log |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
|---|---|---|---|
| [SB_COMMON.dbo.DOCUBILL_SBJOIN_HIS](../../references/database-contracts.md#db094) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: sb_common.dbo.docubill_sbjoin_his | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_COMMON.dbo.MIGRATION_SBJOIN_HIS](../../references/database-contracts.md#db095) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: sb_common.dbo.migration_sbjoin_his | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [MIGRATION_ETCASP.dbo.MIGRATION_MAPPING_MEMBER](../../references/database-contracts.md#db002) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: migration_etcasp.dbo.migration_mapping_member | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SmartBill3.dbo.MEMBER](../../references/database-contracts.md#db203) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.member | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DTI_LOG.dbo.DORMANT_MEMBER](../../references/database-contracts.md#db165) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: sb_dti_log.dbo.dormant_member | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Office.dbo.upGW_MemAdminInfo4](../../references/database-contracts.md#db027) | `@comId varchar(10) IN` | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.company, smartbill3.dbo.dept_manager, smartbill3.dbo.member | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Office.dbo.upGW_MemAdminInfo3](../../references/database-contracts.md#db026) | `@com_no int IN` | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.member, smartbill3.dbo.tax_admin | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Office.dbo.upGW_MemAdminInfo2](../../references/database-contracts.md#db025) | `@service_type varchar(3) IN, @com_no int IN` | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.company, smartbill3.dbo.dept_manager, smartbill3.dbo.member | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_COMMON.dbo.upSBAdm_LstDeptMng](../../references/database-contracts.md#db101) | `@DIVISION varchar(3) IN, @COM_NO varchar(10) IN, @DEPT_NO varchar(10) IN` | 확정한 테이블 쓰기 없음. 참조: sb_dti.dbo.dept_admin, sb_dti.dbo.dept_member, sb_dti.dbo.service_admin, smartbill3.dbo.member | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Office.dbo.upGW_MemAdminInfo1](../../references/database-contracts.md#db024) | `@com_no int IN` | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.company, smartbill3.dbo.member | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Office.dbo.upGW_CompanyINFO](../../references/database-contracts.md#db018) | `@COM_NO varchar(10) IN` | 확정한 테이블 쓰기 없음. 참조: migration_etcasp.dbo.migration_mapping_company, smartbill3.dbo.company, smartbill3.dbo.member | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.COMPANY_CHANGE_LOG](../../references/database-contracts.md#db267) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 쓰기: smartwork.dbo.company_change_log. 참조: smartwork.dbo.company_change_log | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.UspCompanyMember_Withdraw](../../references/database-contracts.md#db322) | `@MEM_NO bigint IN` | 쓰기: sb_dti_log.dbo.dormant_member, smartbill3.dbo.member. 참조: sb_dti_log.dbo.dormant_member, smartbill3.dbo.member | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.UspCompanyAdmin_ChangeTaxCafe](../../references/database-contracts.md#db319) | `@COM_NO int IN, @MEM_NO int IN` | 쓰기: smartbill3.dbo.tax_admin. 참조: smartbill3.dbo.member, smartbill3.dbo.tax_admin | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.UspCompanyAdmin_ChangeDeptManager](../../references/database-contracts.md#db318) | `@COM_NO bigint IN, @SERVICE_TYPE varchar(3) IN, @MEM_NO bigint IN` | 쓰기: smartbill3.dbo.dept_manager. 참조: smartbill3.dbo.dept_manager | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.UspCompanyAdmin_ChangeTaxInvoice](../../references/database-contracts.md#db320) | `@COM_NO bigint IN, @MEM_NO bigint IN` | 쓰기: sb_dti.dbo.service_admin. 참조: sb_dti.dbo.service_admin | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.UspCompanyAdmin_ChangeCorporate](../../references/database-contracts.md#db317) | `@COM_NO bigint IN, @MEM_NO bigint IN` | 쓰기: smartbill3.dbo.member. 참조: smartbill3.dbo.member | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |

위 DB 계약 링크에는 실제 파라미터 타입·기본값·IN/OUT, Mapper 결과 컬럼, RETURN 바인딩, 참조 테이블·하위 프로시저·정의 필터/정렬을 기록했다. DTO·Service·Repository·Mapper의 상세 호출 경로는 각 API 계약에서 확인한다.

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
|---|---|---|
| 검색 결과가 존재하지 않습니다. | [문구·처리 코드](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CompanyMembersTable.tsx#L160); 현재 조건·대상·권한 확인 | 검색·조회 오류면 조건을 확인 후 재조회. 변경·발송 결과가 불명확하면 처리 여부와 이력을 확인한 뒤 재시도 여부를 판단한다. |
| 결과가 없거나 기대 건수와 다름 | 적용된 검색 기준·기간·탭·대상 상태·서버 필터·페이징·목록/다운로드 조건 | 조건을 다시 확인하고 조회한다. 지속되면 경로·작업 시각·마스킹한 식별자·필터를 업무/기술 담당에게 전달한다. |
| 메뉴·버튼 미표시 또는 접근 거부 | 사용자 그룹의 메뉴 접근·VIEW 및 API별 PROCESS/EXECUTE/DELETE/EXCEL_DOWNLOAD/UNMASK 등 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. 프런트 버튼 표시만으로 서버 권한을 판단하지 않는다. |
| 저장·삭제·외부 실행의 결과가 불명확 | 대상 현재 상태·중복 요청·감사 이력·API 오류·파일/외부 소비 로그 | 기존 반영 여부를 먼저 조회한다. 중복 발송·초기화·금액 처리를 피하기 위해 기술 담당 확인 후 재시도한다. |

## 7) 검증·출처

**브라우저 검증(2026-11-09)**: 화면 대조. [경로별 결과와 제한](../../references/browser-verification.md#page042). 역할별 권한 거부·저장 성공·파일 반출·외부 연계 완료는 이 결과로 보장하지 않는다.

| 검증 항목 | 근거·환경 | 상태·확인일 |
|---|---|---|
| 대상 선정 | 사용자가 WBS 탭 내용으로 제공한 텍스트의 No. 138, 139; [선정 태스크](../../inventory/wbs-tasks.csv) | 제공 텍스트 확인 2026-11-09. 원본 Excel의 탭/병합 셀을 독립 재열람한 것은 아님. |
| 메뉴·라우트·화면 | [menuConfig.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts); [BonabankRoutes.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/BonabankRoutes.tsx); [CompanyMembersPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/pages/CompanyMembersPage.tsx) | 코드 확인 2026-11-09, 기준 dc216b313 |
| 기능·권한·API | 이 문서의 API 계약 링크 및 연결 Hook/API·Controller·DTO·Service·Repository·Mapper | 코드 확인 2026-11-09. 조회 요청·화면 대조 범위는 아래 브라우저 근거 참조. 권한 계정별 허용·거부 및 변경 요청 실행은 미확인. |
| DB 정의 | [개발 DB 계약](../../references/database-contracts.md), 이 문서의 연결 객체 | 개발 DB 정의 확인 2026-11-09. 동적 SQL·CLR 내부·정의 미공개 참조의 미확정 범위는 객체별 기록; 후속 확인 DB 담당. |
| 브라우저 화면·배포 환경 | 로컬 인증 계정·Playwright CLI; [화면별 검증표](../../references/browser-verification.md#page042) | 화면 대조, 2026-11-09. 배포본·타 역할·업무 변경 결과는 미확인. |
| 업무 프로시저·쓰기·외부 결과 | 격리된 검증 환경·테스트 데이터의 실행 결과 | 미확인: 명시적인 저장·삭제·발송·초기화 요청은 실행하지 않음. 브라우저 GET의 업무 조회 프로시저·조회수·감사 기록은 별도 영향으로 구분. 격리 환경에서 기술 담당 확인. |

코드 확인과 DB 정의 확인은 실행 성공·업무 승인·다른 환경 적용을 보장하지 않는다. 업무·기술 담당 검토 후 조사 목록의 상태를 완료로 변경한다.

브라우저 직접 근거: [settled-detail-revisit](../../evidence/browser/ready-details-stable.json). 경로·고정 버튼명·입력 속성·표 머리글·API 상태를 보관했고 실제 데이터 값·식별자·인증정보는 제외했다.

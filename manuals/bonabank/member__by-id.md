# [SB 서비스관리] 회원 정보 (상세) 관리자 매뉴얼

작성 기준: `dc216b313` · 확인일 2026-11-09 · 조사 상태 **검토 대기**. 코드·개발 DB 정의 확인. 브라우저: **화면 대조**; 저장·발송 등 업무 실행 결과는 미검증이다.

## 1) 화면 기본 정보

| 항목 | 작성 내용 |
|---|---|
| 업무 도메인·목적 | 보나뱅크 회원을 회사·개인·회원 구분으로 검색하고 회원 정보를 관리한다. |
| 메뉴·화면 경로 | SB 서비스관리 > 보나뱅크 > 회원 정보; `/bonabank/member/:id`; 목록에서 선택한 대상의 경로 변수를 유지하여 진입한다. |
| 화면 유형·담당 | 상세; WBS 작업자 유지윤. 업무·기술 담당 팀명은 원문에 없어 배포 전 해당 도메인 담당자가 확정한다. |
| 관련 화면 | [조회·관리](member.md) |

WBS 근거: No. 140, 141 (사용자가 제공한 텍스트 행 176, 177). API 개발/화면 개발의 중복 행은 같은 화면으로 통합했다.

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
|---|---|---|
| 화면 진입·조회 | `/bonabank/member` 메뉴 접근·하위 경로 작업 권한. 조회 API는 VIEW, 등록/수정 경로는 PROCESS 등 아래 서버 액션과 라우트 가드를 함께 적용한다. | 로그인된 관리자 계정; id 식별자는 이전 화면에서 선택한다. |
| 목록 | `/bonabank/member`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 수정 | `/bonabank/member`; 화면 게이트 PROCESS. 실제 서버 액션은 API별 표 참조. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 탈퇴처리 | `/bonabank/member`; 화면 게이트 PROCESS. 실제 서버 액션은 API별 표 참조. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 회원정보 변경내역 | `/bonabank/member`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 기업관리자 변경 | `/bonabank/member`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |

서버가 최종 권한을 검사한다. 버튼 모양(kind)으로 권한을 추정하지 않는다. 특히 등록·수정이 PROCESS를 사용하는 API와 EXECUTE·UNMASK·EXCEL_DOWNLOAD는 서로 구분한다.

## 3) 화면 사용 절차

**검증 시 화면 버튼**: 회원정보 변경내역, 기업관리자 변경, 수정 (비활성), 탈퇴처리, 목록. 화면 상태·대상에 따라 달라지며 아래 작업 절차와 권한 조건을 함께 확인한다.

1. 관련 화면에서 대상 또는 작업을 선택하여 `/bonabank/member/:id`로 이동한다. 경로 변수는 주소에서 임의로 바꾸지 않고 이전 화면이 전달한 식별자를 사용한다.
2. 대상의 기본 정보·상태·표시 항목을 확인한다. 목록의 식별자와 상세 대상이 일치하는지 확인한다.
3. **수정, 탈퇴처리, 회원정보 변경내역, 기업관리자 변경** 중 필요한 작업을 선택한다. 버튼의 표시·활성 조건과 아래 API별 권한을 확인한다. 저장·삭제·외부 호출 전에는 대상과 현재 상태를 재확인한다.
4. 작업 결과 또는 다운로드 파일을 확인하고 관련 목록으로 돌아가 변경된 상태를 다시 조회한다.

**이 화면에서 유의할 업무 규칙**: 목록의 업체/개인 조건 중 필요한 값을 입력한다. 회원 상세의 정보 변경·기업관리자 변경·탈퇴처리는 각각 권한과 대상 상태를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
|---|---|---|---|
| 변경일시 | 출력 | API 타입 String | `historyDate`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/detail/BonabankMemberChangeHistoryDialog.tsx#L115) |
| 변경항목 | 출력 | API 타입 String | `fieldName`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/detail/BonabankMemberChangeHistoryDialog.tsx#L123) |
| 변경 전 | 출력 | API 타입 String? | `previousValue`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/detail/BonabankMemberChangeHistoryDialog.tsx#L130) |
| 변경 후 | 출력 | API 타입 String? | `currentValue`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/detail/BonabankMemberChangeHistoryDialog.tsx#L137) |
| 변경 담당자 | 출력 | API 타입 String? | `updatedBy`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/detail/BonabankMemberChangeHistoryDialog.tsx#L144) |

**복합 검색·폼의 초기 상태**

| 초기값 근거 | 기본 상태 |
|---|---|
| [initialValues](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/BonabankMemberDetailPage.tsx#L58) | realName={data?.basicInfo.realName ?? ''}; birthDate={data?.basicInfo.birthDate ?? ''}; email={data?.basicInfo.email ?? ''} |

화면 필드 키와 API 필드명이 다른 경우 변환은 Hook/API의 검색·저장 매핑에서 수행된다. 요청·응답 필드와 DB 컬럼 매핑은 아래 API 계약 및 DB 객체 계약에 연결했다.

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
|---|---|---|---|
| 보나뱅크 회원 정보 상세 (4 섹션) | [GET /api/v1/bonabank/members/{id}](../../references/api-contracts.md#api016); `/bonabank/member` / `VIEW` | `경로·쿼리·본문 계약 참조` → `basicInfo, serviceUsage, prepayInfo, invoiceInfo, memberId, realName, nickname, birthDate, joinDate, joinStatusCode, joinStatusLabel, withdrawalDate, userId, memberRoleCode, member` | Mapper 프로시저의 정적 테이블 쓰기 미검출; 동적 SQL의 런타임 대상은 미확정 |
| 보나뱅크 회원 탈퇴 | [POST /api/v1/bonabank/members/{id}/withdraw](../../references/api-contracts.md#api193); `/bonabank/member` / `PROCESS` | `경로·쿼리·본문 계약 참조` → `응답 DTO·파일/처리 결과 계약 참조` | 쓰기 대상 smartbill3.dbo.company, smartbill3.dbo.company_history, smartbill3.dbo.dct_premium, smartbill3.dbo.dct_premium_balance, smartbill3.dbo.dct_premium_his, smartbill3.dbo.dept_admin, smartbill3.dbo.dept_admin_history, smartbill3.dbo.dept_manager, smartbill3.dbo.dept_manager_history, smartbill3.dbo.dept_member, smartbill3.dbo.dept_member_history, smartbill3.dbo.member, smartbill3.dbo.member_history, smartbill3.dbo.member_right, smartbill3.dbo.tax_member, smartbill3.dbo.tax_memgroup_detail; 동적 SQL의 런타임 대상은 미확정 |
| 보나뱅크 회원 종류 변경 (→ 기업관리자) | [PUT /api/v1/bonabank/members/{id}/role-corporate-admin](../../references/api-contracts.md#api258); `/bonabank/member` / `PROCESS` | `경로·쿼리·본문 계약 참조` → `응답 DTO·파일/처리 결과 계약 참조` | 쓰기 대상 smartbill3.dbo.member, smartbill3.dbo.member_history; 동적 SQL의 런타임 대상은 미확정 |
| 보나뱅크 회원 실명/생년월일/이메일 수정 | [PUT /api/v1/bonabank/members/{id}/profile](../../references/api-contracts.md#api257); `/bonabank/member` / `PROCESS` | `realName, birthDate, email` → `응답 DTO·파일/처리 결과 계약 참조` | 쓰기 대상 smartbill3.dbo.member, smartbill3.dbo.member_agreement, smartbill3.dbo.member_history |
| 회원 변경 이력 조회 | [GET /api/v1/members/{memNo}/history](../../references/api-contracts.md#api073); `/member-management/member` / `VIEW` | `경로·쿼리·본문 계약 참조` → `content, totalElements, totalPages, currentPage, size` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 보나뱅크 회원 민감정보 원문 조회 | [POST /api/v1/bonabank/members/{id}/sensitive-values/reveal](../../references/api-contracts.md#api192); `/bonabank/member` / `UNMASK` | `field` → `field, value` | 쓰기 대상 smartwork.dbo.sw_log_access_event |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
|---|---|---|---|
| [SmartBill3.dbo.upAdmSB_SchInvAmt](../../references/database-contracts.md#db248) | `@COM_NO int IN` | 확정한 테이블 쓰기 없음. 참조: sb_bill.dbo.invoice, sb_bill.dbo.payment, smartbill3.dbo.company | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SmartBill3.dbo.upAdmSB_memSchPay](../../references/database-contracts.md#db234) | `@no varchar(50) IN` | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.company, smartbill3.dbo.service_prepay, smartbill3.dbo.service_refund 동적 SQL 포함, 런타임 조합 대상 미확정. | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SmartBill3.dbo.upAdmSB_MemOutUse](../../references/database-contracts.md#db233) | `@service_type varchar(3) IN, @mem_no no IN` | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.dct_main, smartbill3.dbo.tax_admin, smartbill3.dbo.tax_main | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SmartBill3.dbo.upAdmSB_LstMem](../../references/database-contracts.md#db229) | `@no varchar(10) IN, @GUBUN varchar(10) IN` | 확정한 테이블 쓰기 없음. 참조: sb_dti_log.dbo.dormant_member, sb_dti_log.dbo.member_login_his, sb_mobile.dbo.member, smartbill3.dbo.company, smartbill3.dbo.member, smartbill3.dbo.member_agreement | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SmartBill3.dbo.upAdmSB_memOut](../../references/database-contracts.md#db232) | `@mem_no varchar(10) IN` | 쓰기: smartbill3.dbo.company, smartbill3.dbo.company_history, smartbill3.dbo.dct_premium, smartbill3.dbo.dct_premium_balance, smartbill3.dbo.dct_premium_his, smartbill3.dbo.dept_admin, smartbill3.dbo.dept_admin_history, smartbill3.dbo.dept_manager, smartbill3.dbo.dept_manager_history, smartbill3.dbo.dept_member, smartbill3.dbo.dept_member_history, smartbill3.dbo.member, smartbill3.dbo.member_history, smartbill3.dbo.member_right, smartbill3.dbo.tax_member, smartbill3.dbo.tax_memgroup_detail. 참조: smartbill3.dbo.company, smartbill3.dbo.company_history, smartbill3.dbo.dct_premium, smartbill3.dbo.dct_premium_balance, smartbill3.dbo.dct_premium_his, smartbill3.dbo.dept_admin, smartbill3.dbo.dept_admin_history, smartbill3.dbo.dept_manager 외 9개 | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SmartBill3.dbo.UPADMSB_CHGMEMTYPE](../../references/database-contracts.md#db213) | `@NO varchar(10) IN, @SW_NO varchar(20) IN` | 쓰기: smartbill3.dbo.member, smartbill3.dbo.member_history. 참조: smartbill3.dbo.company, smartbill3.dbo.member, smartbill3.dbo.member_history | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.usp_member_info_update](../../references/database-contracts.md#db290) | `@NO bigint IN, @REALNAME varchar(35) IN, @MEM_REGNO varchar(8) IN, @RESULT_EMAIL char(1) IN, @INFO_MAIL char(1) IN, @INFO_SNS char(1) IN, @INFO_TEL char(1) IN, @UPDATE_SW_NO int IN, @EMAIL varchar(200) IN` | 쓰기: smartbill3.dbo.member, smartbill3.dbo.member_agreement, smartbill3.dbo.member_history. 참조: smartbill3.dbo.member, smartbill3.dbo.member_agreement, smartbill3.dbo.member_history | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.usp_member_history_list_select](../../references/database-contracts.md#db289) | `@PAGE int IN, @PAGESIZE int IN, @MEM_NO int IN` | 확정한 테이블 쓰기 없음. 참조: office.dbo.sawon, smartbill3.dbo.member, smartbill3.dbo.member_history | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.usp_sw_log_access_event_insert](../../references/database-contracts.md#db294) | `@EVENT_TYPE varchar(30) IN, @STATUS varchar(20) IN, @USER_ID bigint IN, @MEMBER_ID nvarchar(50) IN, @USER_NAME nvarchar(100) IN, @DEPARTMENT_NAME nvarchar(100) IN, @PAGE_TITLE nvarchar(200) IN, @PATH nvarchar(500) IN, @MENU_PATH nvarchar(500) IN, @MENU_LABEL nvarchar(200) IN, @CATEGORY_NAME nvarchar(200) IN, @SUB_CATEGORY_NAME nvarchar(200) IN, @MENU_ORDER int IN, @IP_ADDRESS varchar(45) IN, @USER_AGENT nvarchar(1000) IN, @BROWSER varchar(100) IN, @OS varchar(100) IN, @REFERRER nvarchar(500) IN, @DETAIL nvarchar(1000) IN, @RESULT int OUT, @COUNTS_AS_VISIT bit IN` | 쓰기: smartwork.dbo.sw_log_access_event. 참조: smartwork.dbo.sw_log_access_event | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SmartBill3.dbo.MEMBER](../../references/database-contracts.md#db203) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.member | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SmartBill3.dbo.COMPANY](../../references/database-contracts.md#db197) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.company | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [MIGRATION_ETCASP.dbo.MIGRATION_MAPPING_COMPANY](../../references/database-contracts.md#db001) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: migration_etcasp.dbo.migration_mapping_company | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [sb_dti_log.dbo.dormant_MEMBER](../../references/database-contracts.md#db165) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: sb_dti_log.dbo.dormant_member | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |

위 DB 계약 링크에는 실제 파라미터 타입·기본값·IN/OUT, Mapper 결과 컬럼, RETURN 바인딩, 참조 테이블·하위 프로시저·정의 필터/정렬을 기록했다. DTO·Service·Repository·Mapper의 상세 호출 경로는 각 API 계약에서 확인한다.

**민감정보**: 기본 응답의 마스킹 값을 유지한다. 원문은 전용 reveal API와 UNMASK 등 추가 권한·사유·감사 로그를 확인한 뒤 조회한다. 화면·캡처·문의 문서에 원문을 남기지 않는다.

**파일**: 업로드·다운로드의 소유 대상, 원래 파일명, 저장 경로 설정, 파일 존재 여부를 구분한다. 저장소 경로와 비밀값은 사용자 입력으로 대체하지 않는다. 파일·외부 연계 상세는 API의 연결 Service·설정 키 근거를 참조한다.

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
|---|---|---|
| 변경 내역이 없습니다. | [문구·처리 코드](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/detail/BonabankMemberChangeHistoryDialog.tsx#L170); 현재 조건·대상·권한 확인 | 검색·조회 오류면 조건을 확인 후 재조회. 변경·발송 결과가 불명확하면 처리 여부와 이력을 확인한 뒤 재시도 여부를 판단한다. |
| 결과가 없거나 기대 건수와 다름 | 적용된 검색 기준·기간·탭·대상 상태·서버 필터·페이징·목록/다운로드 조건 | 조건을 다시 확인하고 조회한다. 지속되면 경로·작업 시각·마스킹한 식별자·필터를 업무/기술 담당에게 전달한다. |
| 메뉴·버튼 미표시 또는 접근 거부 | 사용자 그룹의 메뉴 접근·VIEW 및 API별 PROCESS/EXECUTE/DELETE/EXCEL_DOWNLOAD/UNMASK 등 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. 프런트 버튼 표시만으로 서버 권한을 판단하지 않는다. |
| 저장·삭제·외부 실행의 결과가 불명확 | 대상 현재 상태·중복 요청·감사 이력·API 오류·파일/외부 소비 로그 | 기존 반영 여부를 먼저 조회한다. 중복 발송·초기화·금액 처리를 피하기 위해 기술 담당 확인 후 재시도한다. |

## 7) 검증·출처

**브라우저 검증(2026-11-09)**: 화면 대조. [경로별 결과와 제한](../../references/browser-verification.md#page046). 역할별 권한 거부·저장 성공·파일 반출·외부 연계 완료는 이 결과로 보장하지 않는다.

| 검증 항목 | 근거·환경 | 상태·확인일 |
|---|---|---|
| 대상 선정 | 사용자가 WBS 탭 내용으로 제공한 텍스트의 No. 140, 141; [선정 태스크](../../inventory/wbs-tasks.csv) | 제공 텍스트 확인 2026-11-09. 원본 Excel의 탭/병합 셀을 독립 재열람한 것은 아님. |
| 메뉴·라우트·화면 | [menuConfig.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts); [BonabankRoutes.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/BonabankRoutes.tsx); [BonabankMemberDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/BonabankMemberDetailPage.tsx) | 코드 확인 2026-11-09, 기준 dc216b313 |
| 기능·권한·API | 이 문서의 API 계약 링크 및 연결 Hook/API·Controller·DTO·Service·Repository·Mapper | 코드 확인 2026-11-09. 조회 요청·화면 대조 범위는 아래 브라우저 근거 참조. 권한 계정별 허용·거부 및 변경 요청 실행은 미확인. |
| DB 정의 | [개발 DB 계약](../../references/database-contracts.md), 이 문서의 연결 객체 | 개발 DB 정의 확인 2026-11-09. 동적 SQL·CLR 내부·정의 미공개 참조의 미확정 범위는 객체별 기록; 후속 확인 DB 담당. |
| 브라우저 화면·배포 환경 | 로컬 인증 계정·Playwright CLI; [화면별 검증표](../../references/browser-verification.md#page046) | 화면 대조, 2026-11-09. 배포본·타 역할·업무 변경 결과는 미확인. |
| 업무 프로시저·쓰기·외부 결과 | 격리된 검증 환경·테스트 데이터의 실행 결과 | 미확인: 명시적인 저장·삭제·발송·초기화 요청은 실행하지 않음. 브라우저 GET의 업무 조회 프로시저·조회수·감사 기록은 별도 영향으로 구분. 격리 환경에서 기술 담당 확인. |

코드 확인과 DB 정의 확인은 실행 성공·업무 승인·다른 환경 적용을 보장하지 않는다. 업무·기술 담당 검토 후 조사 목록의 상태를 완료로 변경한다.

브라우저 직접 근거: [settled-detail-revisit](../../evidence/browser/ready-details-stable.json). 경로·고정 버튼명·입력 속성·표 머리글·API 상태를 보관했고 실제 데이터 값·식별자·인증정보는 제외했다.

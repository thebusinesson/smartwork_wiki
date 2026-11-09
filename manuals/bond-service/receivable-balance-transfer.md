# [SB 서비스관리] 채권잔액 전송 관리 (조회·관리) 관리자 매뉴얼

작성 기준: `dc216b313` · 확인일 2026-11-09 · 조사 상태 **검토 대기**. 코드·개발 DB 정의 확인. 브라우저: **화면 대조**; 저장·발송 등 업무 실행 결과는 미검증이다.

## 1) 화면 기본 정보

### 도메인 이해

거래 상대방과 확인할 채권잔액 문서 및 이를 주고받는 연동 상태를 관리하는 업무다. 확인서 조회, 이용 담당자의 권한, 연동업체 설정, 송수신 장애를 같은 업무 흐름 안에서 조사한다.

| 구분 | 설명 |
|---|---|
| 업무 영역 | 채권잔액 확인 서비스 · SB 서비스관리 > 채권잔액 확인 서비스 > 채권잔액 전송 관리 |
| 주요 대상·용어 | 채권잔액 확인서: 거래 잔액 확인에 쓰는 문서 / 연동업체: 시스템 연결 대상 업체 / 참조번호·conversation ID: 문서 또는 송수신 건을 추적하는 값 |
| 업무 흐름 | 확인서·연동업체 찾기 → 담당 권한·송수신 상태 확인 → 로그·전문·장애 정보 조사 → 필요한 조치 |
| 이 페이지의 역할 | 채권잔액 송수신 업무의 진입 화면이다. 송수신 건별 상태·전문·로그를 확인하고 재전송 판단에 필요한 정보를 조사한다. 같은 메뉴의 팝업·탭은 이 문서에서, 독립 상세·등록·수정 화면은 관련 문서에서 다룬다. |
| 관련 업무와 구분 | 문서의 잔액 확인과 실제 입금·환불 처리는 다른 업무다. 송신 요청·접수·상대방 처리 결과를 한 상태로 간주하지 않는다. |

도메인 설명 근거: 이 문서 7번의 현재 메뉴·라우트·화면 및 API·업무 규칙 소스. [전체 도메인 지도](../../references/domain-overview.md#bond). 설명 보강일 2026-11-09; 기존 실행 검증 범위와 미확인 상태는 변경하지 않았다.

### 화면 정보

| 항목 | 작성 내용 |
|---|---|
| 업무 도메인·목적 | 채권잔액 송수신 상태를 조회하고 conversation별 로그와 전문을 확인한다. |
| 메뉴·화면 경로 | SB 서비스관리 > 채권잔액 확인 서비스 > 채권잔액 전송 관리; `/bond-service/receivable-balance-transfer`; 메뉴 또는 관련 화면에서 진입한다. |
| 화면 유형·담당 | 조회·관리; WBS 작업자 유지윤. 업무·기술 담당 팀명은 원문에 없어 배포 전 해당 도메인 담당자가 확정한다. |
| 관련 화면 | [상세](receivable-balance-transfer__by-conversationId.md) |

WBS 근거: No. 117, 118 (사용자가 제공한 텍스트 행 148, 149). API 개발/화면 개발의 중복 행은 같은 화면으로 통합했다.

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
|---|---|---|
| 화면 진입·조회 | `/bond-service/receivable-balance-transfer` 메뉴 접근·하위 경로 작업 권한. 조회 API는 VIEW, 등록/수정 경로는 PROCESS 등 아래 서버 액션과 라우트 가드를 함께 적용한다. | 로그인된 관리자 계정; 아래 검색·입력 항목을 준비한다. |
| Send | `/bond-service/receivable-balance-transfer`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |

서버가 최종 권한을 검사한다. 버튼 모양(kind)으로 권한을 추정하지 않는다. 특히 등록·수정이 PROCESS를 사용하는 API와 EXECUTE·UNMASK·EXCEL_DOWNLOAD는 서로 구분한다.

## 3) 화면 사용 절차

**검증 시 화면 버튼**: 검색, 초기화. 화면 상태·대상에 따라 달라지며 아래 작업 절차와 권한 조건을 함께 확인한다.

1. `SB 서비스관리 > 채권잔액 확인 서비스 > 채권잔액 전송 관리` 메뉴를 연다. 경로 변수는 주소에서 임의로 바꾸지 않고 이전 화면이 전달한 식별자를 사용한다.
2. 최초 진입 시 자동조회하지 않는다. 아래 검색 항목을 입력한 후 **검색**을 누른다.
3. 결과 행에서 업무 대상을 선택하여 관련 상세 화면으로 이동한다. 페이지 이동·검색 조건 변경 후에는 현재 조건과 조회 대상을 다시 확인한다.

**이 화면에서 유의할 업무 규칙**: 기준일·거래처·conversation ID·진행/전송 상태로 조회한다. 상세의 로그에서 WholeMsg/BodyMsg를 선택해 전문을 확인한다. 재전송은 SOAP 외부 요청을 발생시키므로 대상 방향·상태를 확인하고 결과가 불명확하면 중복 실행 전에 로그를 확인한다.

## 4) 입력·표시 데이터

**검증 시 표시된 날짜 필터**: 시작일 `2026-10-09`, 종료일 `2026-11-09`. 검증 날짜·조건 복원에 따른 표시값이며 모든 실행의 고정 기본값을 뜻하지 않는다.

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
|---|---|---|---|
| 기준일 | 입력·선택(조건부 검증 별도) | 화면 타입 dateRange; 초기값 startDate=빈값; endDate=빈값 | `dateRange`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/ReceivableBalanceTransferPage.tsx#L90) |
| 거래처 | 입력·선택(조건부 검증 별도) | 화면 타입 selectWithInput; 선택: 전체=ALL, 사업자번호=bizNo, 회사명=companyName; 초기값 selectValue=bizNo; inputValue=빈값 | `partnerCondition`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/ReceivableBalanceTransferPage.tsx#L91) |
| conversation ID | 입력·선택(조건부 검증 별도) | 화면 타입 text; API 타입 String?; 초기값 빈값 | `conversationId`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/ReceivableBalanceTransferPage.tsx#L106) |
| 진행상태 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/ReceivableBalanceTransferPage.tsx#L268) |
| 전송상태 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/ReceivableBalanceTransferPage.tsx#L295) |
| 기준일 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `baseDate`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/ReceivableBalanceTransferPage.tsx#L322) |
| DrcNo | 출력 | API 타입 Int | `drcNo`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/ReceivableBalanceTransferPage.tsx#L323) |
| conversation id | 출력 | API 타입 String?; 초기값 빈값 | `conversationId`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/ReceivableBalanceTransferPage.tsx#L324) |
| 채권 잔액 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `receivableAmount`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/ReceivableBalanceTransferPage.tsx#L325) |
| 구분 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `division`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/ReceivableBalanceTransferPage.tsx#L331) |
| 회사 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `company`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/ReceivableBalanceTransferPage.tsx#L342) |
| 담당자 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `manager`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/ReceivableBalanceTransferPage.tsx#L353) |
| 상태 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `progressStatus`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/ReceivableBalanceTransferPage.tsx#L364) |
| 재전송 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `resend`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/ReceivableBalanceTransferPage.tsx#L370) |

입력 검증 근거: [ReceivableBalanceTransferPage.checks.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/service/bondservice/ReceivableBalanceTransferPage.checks.ts). 프런트 검증과 서버 DTO 제약이 다르면 서버 검증이 최종 기준이다.

**복합 검색·폼의 초기 상태**

| 초기값 근거 | 기본 상태 |
|---|---|
| [DEFAULT_FILTER_VALUES](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/ReceivableBalanceTransferPage.tsx#L111) | dateRange=startDate=빈값; endDate=빈값; partnerCondition=selectValue=bizNo; inputValue=빈값; conversationId=빈값; progressChecks=PENDING=켜짐; APPROVED=켜짐; REJECTED=켜짐; CANCELED=켜짐; SAVED=켜짐; sendStatus=ALL |

화면 필드 키와 API 필드명이 다른 경우 변환은 Hook/API의 검색·저장 매핑에서 수행된다. 요청·응답 필드와 DB 컬럼 매핑은 아래 API 계약 및 DB 객체 계약에 연결했다.

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
|---|---|---|---|
| 채권잔액 전송 모니터링 목록 조회 | [GET /api/v1/bond-service/receivable-balance-transfers](../../references/api-contracts.md#api041); `/bond-service/receivable-balance-transfer` / `VIEW` | `startDate, endDate, searchType, searchText, convId, statusCodes, transferStatuses, page, size` → `content, totalElements, totalPages, page, size, drcNo, conversationId, basicDate, receivableBalance, creditorComRegno, creditorComName, creditorMemName, creditorComNo, debetorComRe` | Mapper 프로시저의 정적 테이블 쓰기 미검출; 동적 SQL의 런타임 대상은 미확정 |
| 확인서 재전송 | [POST /api/v1/bond-service/receivable-balance-transfers/{drcNo}/resend](../../references/api-contracts.md#api198); `/bond-service/receivable-balance-transfer` / `PROCESS` | `status, transferStatus, creditorComNo, debetorComNo, conversationId, isMember` → `drcNo, resultCode, resultMessage, success` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
|---|---|---|---|
| [SB_DRC.dbo.upAdmSB_Lst_DRC_MoniteringLst_NM](../../references/database-contracts.md#db128) | `@StartDate varchar(10) IN, @EndDate varchar(10) IN, @SearchType char(1) IN, @SearchText varchar(200) IN, @Com_Type varchar(100) IN, @Status_Code varchar(100) IN, @ConvId varchar(35) IN, @TransferStatus varchar(100) IN` | 확정한 테이블 쓰기 없음. 참조: sb_drc.dbo.drc_company_link, sb_drc.dbo.drc_company_nm, sb_drc.dbo.drc_main, sb_drc.dbo.drc_status_nm, sb_drc.dbo.drc_use, smartbill3.dbo.company, smartbill3.dbo.member 동적 SQL 포함, 런타임 조합 대상 미확정. | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DRC.dbo.upAdmSB_Lst_DRC_MoniteringLst](../../references/database-contracts.md#db127) | `@StartDate varchar(10) IN, @EndDate varchar(10) IN, @SearchType char(1) IN, @SearchText varchar(200) IN, @Com_Type varchar(100) IN, @Status_Code varchar(100) IN, @ConvId varchar(35) IN, @TransferStatus varchar(100) IN` | 확정한 테이블 쓰기 없음. 참조: sb_drc.dbo.drc_company, sb_drc.dbo.drc_company_link, sb_drc.dbo.drc_main, sb_drc.dbo.drc_status, sb_drc.dbo.drc_use, smartbill3.dbo.company, smartbill3.dbo.member 동적 SQL 포함, 런타임 조합 대상 미확정. | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.UspDrcMonitoringLogList](../../references/database-contracts.md#db334) | `@ConversationId varchar(35) IN, @LogIdx int IN, @ActionStatus varchar(10) IN, @TransferStatus varchar(10) IN, @DrcNo int IN` | 확정한 테이블 쓰기 없음. 참조: sb_drc.dbo.drc_log, sb_drc.dbo.drc_main | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DRC.dbo.upStm_LstDRCCompanyLinkInfo](../../references/database-contracts.md#db132) | `@Com_No varchar(10) IN` | 확정한 테이블 쓰기 없음. 참조: sb_drc.dbo.drc_company_link | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| 외부 SOAP: drc-resend.* | enabled, rcv-endpoint-url, snd-endpoint-url, default-target-url, connect/read-timeout-seconds | 설정 클래스 기본 enabled=false이며 비활성은 501. C/Q는 수신 서비스, A/R은 송신 서비스 분기. 요청 성공과 외부 반영을 구분 | [DrcResendProperties.kt](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/infra/config/DrcResendProperties.kt) |

위 DB 계약 링크에는 실제 파라미터 타입·기본값·IN/OUT, Mapper 결과 컬럼, RETURN 바인딩, 참조 테이블·하위 프로시저·정의 필터/정렬을 기록했다. DTO·Service·Repository·Mapper의 상세 호출 경로는 각 API 계약에서 확인한다.

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
|---|---|---|
| 결과가 없거나 기대 건수와 다름 | 적용된 검색 기준·기간·탭·대상 상태·서버 필터·페이징·목록/다운로드 조건 | 조건을 다시 확인하고 조회한다. 지속되면 경로·작업 시각·마스킹한 식별자·필터를 업무/기술 담당에게 전달한다. |
| 메뉴·버튼 미표시 또는 접근 거부 | 사용자 그룹의 메뉴 접근·VIEW 및 API별 PROCESS/EXECUTE/DELETE/EXCEL_DOWNLOAD/UNMASK 등 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. 프런트 버튼 표시만으로 서버 권한을 판단하지 않는다. |
| 저장·삭제·외부 실행의 결과가 불명확 | 대상 현재 상태·중복 요청·감사 이력·API 오류·파일/외부 소비 로그 | 기존 반영 여부를 먼저 조회한다. 중복 발송·초기화·금액 처리를 피하기 위해 기술 담당 확인 후 재시도한다. |

## 7) 검증·출처

**브라우저 검증(2026-11-09)**: 화면 대조. [경로별 결과와 제한](../../references/browser-verification.md#page031). 역할별 권한 거부·저장 성공·파일 반출·외부 연계 완료는 이 결과로 보장하지 않는다.

| 검증 항목 | 근거·환경 | 상태·확인일 |
|---|---|---|
| 대상 선정 | 사용자가 WBS 탭 내용으로 제공한 텍스트의 No. 117, 118; [선정 태스크](../../inventory/wbs-tasks.csv) | 제공 텍스트 확인 2026-11-09. 원본 Excel의 탭/병합 셀을 독립 재열람한 것은 아님. |
| 메뉴·라우트·화면 | [menuConfig.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts); [BondServiceRoutes.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/BondServiceRoutes.tsx); [ReceivableBalanceTransferPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/ReceivableBalanceTransferPage.tsx) | 코드 확인 2026-11-09, 기준 dc216b313 |
| 기능·권한·API | 이 문서의 API 계약 링크 및 연결 Hook/API·Controller·DTO·Service·Repository·Mapper | 코드 확인 2026-11-09. 조회 요청·화면 대조 범위는 아래 브라우저 근거 참조. 권한 계정별 허용·거부 및 변경 요청 실행은 미확인. |
| DB 정의 | [개발 DB 계약](../../references/database-contracts.md), 이 문서의 연결 객체 | 개발 DB 정의 확인 2026-11-09. 동적 SQL·CLR 내부·정의 미공개 참조의 미확정 범위는 객체별 기록; 후속 확인 DB 담당. |
| 브라우저 화면·배포 환경 | 로컬 인증 계정·Playwright CLI; [화면별 검증표](../../references/browser-verification.md#page031) | 화면 대조, 2026-11-09. 배포본·타 역할·업무 변경 결과는 미확인. |
| 업무 프로시저·쓰기·외부 결과 | 격리된 검증 환경·테스트 데이터의 실행 결과 | 미확인: 명시적인 저장·삭제·발송·초기화 요청은 실행하지 않음. 브라우저 GET의 업무 조회 프로시저·조회수·감사 기록은 별도 영향으로 구분. 격리 환경에서 기술 담당 확인. |

코드 확인과 DB 정의 확인은 실행 성공·업무 승인·다른 환경 적용을 보장하지 않는다. 업무·기술 담당 검토 후 조사 목록의 상태를 완료로 변경한다.

브라우저 직접 근거: [test-company-search](../../evidence/browser/targeted-stable.json). 경로·고정 버튼명·입력 속성·표 머리글·API 상태를 보관했고 실제 데이터 값·식별자·인증정보는 제외했다.

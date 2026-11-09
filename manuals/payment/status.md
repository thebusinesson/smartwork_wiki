# [서비스 현황] 입금 현황 조회 (조회·관리) 관리자 매뉴얼

작성 기준: `dc216b313` · 확인일 2026-11-09 · 조사 상태 **검토 대기**. 코드·개발 DB 정의 확인. 브라우저: **화면 대조**; 저장·발송 등 업무 실행 결과는 미검증이다.

## 1) 화면 기본 정보

### 도메인 이해

고객의 서비스 요금 입금과 미리 보유한 금액, 환불 신청을 관리하는 업무다. 입금 내역이 어느 업체·청구에 연결되는지, 예치금이 어떻게 늘거나 줄었는지, 환불 가능한 금액과 처리 상태가 무엇인지 확인한다.

| 구분 | 설명 |
|---|---|
| 업무 영역 | 입금·예치금·환불 관리 · 서비스 현황 > 입금관리 > 입금 현황 조회 |
| 주요 대상·용어 | 입금: 접수된 납부 내역 / 예치금: 서비스 이용을 위해 보유·차감되는 금액 / 청구월: 요금을 청구한 월 / 환불 신청: 환불 대상·금액·계좌·처리 상태 기록 |
| 업무 흐름 | 업체·기간·청구 찾기 → 입금·잔액·이력 확인 → 허용된 입금/예치금/환불 처리 → 상태·금액 재확인 |
| 이 페이지의 역할 | 요금 입금 내역 업무의 진입 화면이다. 청구월·입금일·방식·상태로 납부 내역과 처리 상태를 확인한다. 같은 메뉴의 팝업·탭은 이 문서에서, 독립 상세·등록·수정 화면은 관련 문서에서 다룬다. |
| 관련 업무와 구분 | 예치금 잔액·환불 가능 금액·환불 신청 금액은 같은 값이 아니다. 화면의 처리 완료와 실제 은행 송금 완료의 확인 범위를 구분한다. |

도메인 설명 근거: 이 문서 7번의 현재 메뉴·라우트·화면 및 API·업무 규칙 소스. [전체 도메인 지도](../../references/domain-overview.md#payment). 설명 보강일 2026-11-09; 기존 실행 검증 범위와 미확인 상태는 변경하지 않았다.

### 화면 정보

| 항목 | 작성 내용 |
|---|---|
| 업무 도메인·목적 | 청구월·입금일·입금 방식·상태별 입금 내역과 처리 상태를 확인한다. |
| 메뉴·화면 경로 | 서비스 현황 > 입금관리 > 입금 현황 조회; `/payment/status`; 메뉴 또는 관련 화면에서 진입한다. |
| 화면 유형·담당 | 조회·관리; WBS 작업자 유지윤. 업무·기술 담당 팀명은 원문에 없어 배포 전 해당 도메인 담당자가 확정한다. |
| 관련 화면 | [상세](status__by-id.md) |

WBS 근거: No. 184 (사용자가 제공한 텍스트 행 230). API 개발/화면 개발의 중복 행은 같은 화면으로 통합했다.

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
|---|---|---|
| 화면 진입·조회 | `/payment/status` 메뉴 접근·하위 경로 작업 권한. 조회 API는 VIEW, 등록/수정 경로는 PROCESS 등 아래 서버 액션과 라우트 가드를 함께 적용한다. | 로그인된 관리자 계정; 아래 검색·입력 항목을 준비한다. |
| 다운로드 | `/payment/status`; 엑셀 download 화면 게이트. 다운로드/업로드 API의 서버 권한과 사유 입력을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |

서버가 최종 권한을 검사한다. 버튼 모양(kind)으로 권한을 추정하지 않는다. 특히 등록·수정이 PROCESS를 사용하는 API와 EXECUTE·UNMASK·EXCEL_DOWNLOAD는 서로 구분한다.

## 3) 화면 사용 절차

**검증 시 화면 버튼**: 검색, 다운로드. 화면 상태·대상에 따라 달라지며 아래 작업 절차와 권한 조건을 함께 확인한다.

1. `서비스 현황 > 입금관리 > 입금 현황 조회` 메뉴를 연다. 경로 변수는 주소에서 임의로 바꾸지 않고 이전 화면이 전달한 식별자를 사용한다.
2. 최초 진입 시 자동조회하지 않는다. 아래 검색 항목을 입력한 후 **검색**을 누른다.
3. 결과 행에서 업무 대상을 선택하여 관련 상세 화면으로 이동한다. 페이지 이동·검색 조건 변경 후에는 현재 조건과 조회 대상을 다시 확인한다.

**이 화면에서 유의할 업무 규칙**: 업체 조건은 사업자번호가 기본이며 입금 방식·상태는 기본 전체 선택이다. 상세에서 입금 취소와 예치금 처리 가능 상태를 확인한다. 입금자 원문은 별도 UNMASK 권한과 감사 절차가 있는 경우에만 확인한다.

**반출**: 적용된 검색 조건과 반출 범위를 확인한 후 다운로드한다. 사유 입력창이 표시되면 업무 사유를 입력한다. 사유 등록 실패·파일 오류는 성공으로 간주하지 않고 다운로드 결과를 확인한다.

## 4) 입력·표시 데이터

**검증 시 표시된 날짜 필터**: 시작월 `2026-09`, 종료월 `2026-11`, 시작일 `2026-10-01`, 종료일 `2026-11-30`. 검증 날짜·조건 복원에 따른 표시값이며 모든 실행의 고정 기본값을 뜻하지 않는다.

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
|---|---|---|---|
| 청구월 | 출력 | API 타입 String | `billingMonth`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/PaymentStatusPage.tsx#L64) |
| 회사명 | 출력 | API 타입 String?; 기본 null; 초기값 빈값 | `companyName`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/PaymentStatusPage.tsx#L65) |
| 사업자번호 | 출력 | API 타입 String?; 기본 null; 초기값 빈값 | `businessNumber`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/PaymentStatusPage.tsx#L66) |
| 입금일 | 출력 | API 타입 String | `paymentDate`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/PaymentStatusPage.tsx#L67) |
| 입금상태 | 출력 | API 타입 String | `paymentStatus`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/PaymentStatusPage.tsx#L74) |
| 입금방식 | 출력 | API 타입 String | `paymentMethod`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/PaymentStatusPage.tsx#L90) |
| 청구액 | 출력 | API 타입 Long | `billingAmount`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/PaymentStatusPage.tsx#L91) |
| 입금액 | 출력 | API 타입 Long | `paymentAmount`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/PaymentStatusPage.tsx#L98) |
| 입금자 | 출력 | API 타입 String | `payer`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/PaymentStatusPage.tsx#L105) |
| 청구월 | 입력·선택(조건부 검증 별도) | 화면 타입 toggleableMonthRange; API 타입 String | `billingMonth`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/PaymentStatusPage.tsx#L228) |
| 입금일 | 입력·선택(조건부 검증 별도) | 화면 타입 toggleableDateRange; API 타입 String | `paymentDate`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/PaymentStatusPage.tsx#L242) |
| 업체 조건 | 입력·선택(조건부 검증 별도) | 화면 타입 selectWithInput; API 타입 String?; 기본 null; 초기값 사업자번호 | `companyCondition`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/PaymentStatusPage.tsx#L256) |
| 입금 방식 | 입력·선택(조건부 검증 별도) | 화면 타입 checkbox; API 타입 List<String>?; 기본 null; 초기값 {...PAYMENT_METHOD_OPTIONS} | `paymentMethods`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/PaymentStatusPage.tsx#L280) |
| 입금 상태 | 입력·선택(조건부 검증 별도) | 화면 타입 checkbox; API 타입 List<String>?; 기본 null; 초기값 {...PAYMENT_STATUS_OPTIONS} | `paymentStatuses`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/PaymentStatusPage.tsx#L291) |

입력 검증 근거: [PaymentStatusPage.checks.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/status/payment/PaymentStatusPage.checks.ts). 프런트 검증과 서버 DTO 제약이 다르면 서버 검증이 최종 기준이다.

**복합 검색·폼의 초기 상태**

| 초기값 근거 | 기본 상태 |
|---|---|
| [getDefaultSearchForm](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/PaymentStatusPage.tsx#L118) | billingMonthStart={billingRange.startMonth}; billingMonthEnd={billingRange.endMonth}; paymentDateStart={getLastMonthFirstDay()}; paymentDateEnd={getCurrentMonthLastDay()}; companyCondition=사업자번호; companyName=빈값; businessNumber=빈값; paymentMethods={...PAYMENT_METHOD_OPTIONS}; paymentStatuses={...PAYMENT_STATUS_OPTIONS}; billingMonthAll=꺼짐; paymentDateAll=꺼짐 |

화면 필드 키와 API 필드명이 다른 경우 변환은 Hook/API의 검색·저장 매핑에서 수행된다. 요청·응답 필드와 DB 컬럼 매핑은 아래 API 계약 및 DB 객체 계약에 연결했다.

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
|---|---|---|---|
| 입금 현황 목록 조회 | [GET /api/v1/service-status/deposits/status](../../references/api-contracts.md#api109); `/payment/status` / `VIEW` | `billingMonthStart, billingMonthEnd, paymentDateStart, paymentDateEnd, companyCondition, companyName, businessNumber, paymentMethods, paymentStatuses, page, size` → `content, totalElements, totalPages, currentPage, size, id, billingMonth, companyName, businessNumber, paymentDate, paymentStatus, paymentMethod, billingAmount, paymentAmount, payer` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 입금 현황 엑셀 다운로드 | [GET /api/v1/service-status/deposits/status/download](../../references/api-contracts.md#api110); `/payment/status` / `EXCEL_DOWNLOAD` | `billingMonthStart, billingMonthEnd, paymentDateStart, paymentDateEnd, companyCondition, companyName, businessNumber, paymentMethods, paymentStatuses, page, size` → `응답 DTO·파일/처리 결과 계약 참조` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 입금 현황 입금자명 원문 조회 | [POST /api/v1/service-status/deposits/status/{id}/sensitive-values/reveal](../../references/api-contracts.md#api232); `/payment/status` / `UNMASK` | `field` → `field, value` | 쓰기 대상 smartwork.dbo.sw_log_access_event |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
|---|---|---|---|
| [smartwork.dbo.UspBill_PayMentWaitingDeposit_SELECT](../../references/database-contracts.md#db313) | `@IDX_LIST nvarchar(max) IN` | 확정한 테이블 쓰기 없음. 참조: sb_bill.dbo.headoffice_deposit, sb_bill.dbo.headoffice_deposit_his, sb_bill.dbo.payment, smartbill3.dbo.account_bulk, smartbill3.dbo.account_bulk_app, smartbill3.dbo.company | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.UspBill_PayMentList_SELECT](../../references/database-contracts.md#db311) | `@PAGE int IN, @TOP int IN, @GUBUN1 varchar(3) IN, @GUBUN2 varchar(3) IN, @SCH_TEXT varchar(70) IN, @FROM_DATE datetime IN, @TO_DATE datetime IN, @PAY_DIV varchar(30) IN, @GUBUN3 varchar(3) IN, @FROM_MONTH varchar(6) IN, @TO_MONTH varchar(6) IN, @STATUSES nvarchar(200) IN` | 확정한 테이블 쓰기 없음. 참조: sb_bill.dbo.invoice, sb_bill.dbo.payment, smartbill3.dbo.company, smartbill3.dbo.member | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.UspBill_PayMentList_SELECT_Excel](../../references/database-contracts.md#db312) | `@GUBUN1 varchar(3) IN, @GUBUN2 varchar(3) IN, @SCH_TEXT varchar(70) IN, @FROM_DATE datetime IN, @TO_DATE datetime IN, @PAY_DIV varchar(30) IN, @GUBUN3 varchar(3) IN, @FROM_MONTH varchar(6) IN, @TO_MONTH varchar(6) IN, @STATUSES nvarchar(200) IN` | 확정한 테이블 쓰기 없음. 참조: sb_bill.dbo.invoice, sb_bill.dbo.payment, smartbill3.dbo.company, smartbill3.dbo.member | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.usp_sw_log_access_event_insert](../../references/database-contracts.md#db294) | `@EVENT_TYPE varchar(30) IN, @STATUS varchar(20) IN, @USER_ID bigint IN, @MEMBER_ID nvarchar(50) IN, @USER_NAME nvarchar(100) IN, @DEPARTMENT_NAME nvarchar(100) IN, @PAGE_TITLE nvarchar(200) IN, @PATH nvarchar(500) IN, @MENU_PATH nvarchar(500) IN, @MENU_LABEL nvarchar(200) IN, @CATEGORY_NAME nvarchar(200) IN, @SUB_CATEGORY_NAME nvarchar(200) IN, @MENU_ORDER int IN, @IP_ADDRESS varchar(45) IN, @USER_AGENT nvarchar(1000) IN, @BROWSER varchar(100) IN, @OS varchar(100) IN, @REFERRER nvarchar(500) IN, @DETAIL nvarchar(1000) IN, @RESULT int OUT, @COUNTS_AS_VISIT bit IN` | 쓰기: smartwork.dbo.sw_log_access_event. 참조: smartwork.dbo.sw_log_access_event | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_BILL.dbo.PAYMENT](../../references/database-contracts.md#db064) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: sb_bill.dbo.payment | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SMARTBILL3.dbo.COMPANY](../../references/database-contracts.md#db197) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.company | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
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

**브라우저 검증(2026-11-09)**: 화면 대조. [경로별 결과와 제한](../../references/browser-verification.md#page066). 역할별 권한 거부·저장 성공·파일 반출·외부 연계 완료는 이 결과로 보장하지 않는다.

| 검증 항목 | 근거·환경 | 상태·확인일 |
|---|---|---|
| 대상 선정 | 사용자가 WBS 탭 내용으로 제공한 텍스트의 No. 184; [선정 태스크](../../inventory/wbs-tasks.csv) | 제공 텍스트 확인 2026-11-09. 원본 Excel의 탭/병합 셀을 독립 재열람한 것은 아님. |
| 메뉴·라우트·화면 | [menuConfig.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts); [PaymentRoutes.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/PaymentRoutes.tsx); [PaymentStatusPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/PaymentStatusPage.tsx) | 코드 확인 2026-11-09, 기준 dc216b313 |
| 기능·권한·API | 이 문서의 API 계약 링크 및 연결 Hook/API·Controller·DTO·Service·Repository·Mapper | 코드 확인 2026-11-09. 조회 요청·화면 대조 범위는 아래 브라우저 근거 참조. 권한 계정별 허용·거부 및 변경 요청 실행은 미확인. |
| DB 정의 | [개발 DB 계약](../../references/database-contracts.md), 이 문서의 연결 객체 | 개발 DB 정의 확인 2026-11-09. 동적 SQL·CLR 내부·정의 미공개 참조의 미확정 범위는 객체별 기록; 후속 확인 DB 담당. |
| 브라우저 화면·배포 환경 | 로컬 인증 계정·Playwright CLI; [화면별 검증표](../../references/browser-verification.md#page066) | 화면 대조, 2026-11-09. 배포본·타 역할·업무 변경 결과는 미확인. |
| 업무 프로시저·쓰기·외부 결과 | 격리된 검증 환경·테스트 데이터의 실행 결과 | 미확인: 명시적인 저장·삭제·발송·초기화 요청은 실행하지 않음. 브라우저 GET의 업무 조회 프로시저·조회수·감사 기록은 별도 영향으로 구분. 격리 환경에서 기술 담당 확인. |

코드 확인과 DB 정의 확인은 실행 성공·업무 승인·다른 환경 적용을 보장하지 않는다. 업무·기술 담당 검토 후 조사 목록의 상태를 완료로 변경한다.

브라우저 직접 근거: [settled-static-recheck](../../evidence/browser/static-stable.json). 경로·고정 버튼명·입력 속성·표 머리글·API 상태를 보관했고 실제 데이터 값·식별자·인증정보는 제외했다.

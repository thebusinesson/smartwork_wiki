# [서비스 현황] 환불 관리 (등록) 관리자 매뉴얼

작성 기준: `dc216b313` · 확인일 2026-11-09 · 조사 상태 **검토 대기**. 코드·개발 DB 정의 확인. 브라우저: **화면 대조**; 저장·발송 등 업무 실행 결과는 미검증이다.

## 1) 화면 기본 정보

### 도메인 이해

업체를 먼저 조회한 뒤 환불받을 은행·계좌·신청 금액을 새 신청으로 기록한다.

| 구분 | 설명 |
|---|---|
| 업무 영역 | 입금·예치금·환불 관리 > 환불 관리 등록 |
| 언제 사용하는가 | 환불 가능 범위·기존 신청을 확인하고 신규 접수가 필요할 때 |
| 주요 대상·데이터 | 처음에는 사업자번호 검색, 업체 조회 후 회사·잔액·환불가능금액·은행·계좌·신청금액을 다룬다. |
| 업무 흐름 | 사업자번호 검색 → 업체·가능 금액 확인 → 환불 입력 → 저장 후 신청 목록 확인 |
| 이 페이지의 역할 | 환불 신청 중 **환불 관리 등록** 단계. 업체를 먼저 조회한 뒤 환불받을 은행·계좌·신청 금액을 새 신청으로 기록한다. |
| 판단 결과·다음 업무 | 새 신청이 맞는 업체·금액·계좌로 등록되었는지 확인하고 기존 신청 상세에서 경과를 추적한다. |
| 다른 화면과의 구분 | 최초 진입 시 저장 폼이 바로 나오지 않는다. 업체 검색 성공·신청 저장·실제 송금은 서로 다른 단계다. |

**탭·영역·팝업별 업무 구분**

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
|---|---|---|---|
| 업체 검색 단계 | 어느 업체의 환불 신청인지 확정할 때 | 사업자번호와 조회된 업체·가능 금액 | 업체 조회 실패 상태에서는 환불 입력 단계가 성립하지 않는다. |
| 환불 입력 단계 | 업체 확인 뒤 새 신청 정보를 기록할 때 | 환불은행·계좌·신청금액과 표시된 가능 금액 | 저장 결과를 기존 신청 목록과 대조한다. 가능 금액 조회 자체는 신청 저장이 아니다. |

설명 근거: [RefundRegistrationPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/RefundRegistrationPage.tsx), 이 문서 4·5·7번의 항목·API·업무 규칙. [상위 업무 영역](../../references/domain-overview.md#payment)은 공통 배경이며 현재 화면의 데이터·동작은 위 설명을 따른다. 설명 수정일 **2026-11-10**; 새 업무 실행 검증을 수행한 것은 아니다.

### 화면 정보

| 항목 | 작성 내용 |
|---|---|
| 업무 도메인·목적 | 업체를 먼저 조회한 뒤 환불받을 은행·계좌·신청 금액을 새 신청으로 기록한다. |
| 메뉴·화면 경로 | 서비스 현황 > 입금관리 > 환불 관리; `/payment/refund-management/new`; 메뉴 또는 관련 화면에서 진입한다. |
| 화면 유형·담당 | 등록; WBS 작업자 유지윤. 업무·기술 담당 팀명은 원문에 없어 배포 전 해당 도메인 담당자가 확정한다. |
| 관련 화면 | [조회·관리](refund-management.md); [환불 가능 금액 조회](refund-management__inquiry.md); [상세](refund-management__by-refundNo.md) |

WBS 근거: No. 213, 214, 215 (사용자가 제공한 텍스트 행 270, 271, 272). API 개발/화면 개발의 중복 행은 같은 화면으로 통합했다.

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
|---|---|---|
| 화면 진입·조회 | `/payment/refund-management` 메뉴 접근·하위 경로 작업 권한. 조회 API는 VIEW, 등록/수정 경로는 PROCESS 등 아래 서버 액션과 라우트 가드를 함께 적용한다. | 로그인된 관리자 계정; 아래 검색·입력 항목을 준비한다. |
| 저장 | `/payment/refund-management`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 목록 | `/payment/refund-management`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |

서버가 최종 권한을 검사한다. 버튼 모양(kind)으로 권한을 추정하지 않는다. 특히 등록·수정이 PROCESS를 사용하는 API와 EXECUTE·UNMASK·EXCEL_DOWNLOAD는 서로 구분한다.

## 3) 화면 사용 절차

**검증 시 화면 버튼**: 검색, 목록. 화면 상태·대상에 따라 달라지며 아래 작업 절차와 권한 조건을 함께 확인한다.

1. 환불 관리 목록에서 **환불 신규 등록**으로 이동한다. 처음에는 사업자번호 검색 단계가 표시된다.
2. 사업자번호 10자리를 입력하고 **검색**한다. 업체를 찾지 못하면 검색값을 확인하고 환불 정보 입력을 진행하지 않는다.
3. 조회된 업체·잔액·환불가능금액을 확인한 뒤 **환불은행, 환불계좌, 환불신청금액**을 입력한다.
4. 입력값과 환불 대상·금액을 재확인하고 **저장**한다. 정상 저장 결과와 목록의 신청 내역을 확인한다. 저장 결과가 불명확하면 재등록 전에 기존 신청 반영 여부를 확인한다. 이 저장 성공 단계는 격리 환경 후속 검증 대상이다.

**이 화면에서 유의할 업무 규칙**: 목록의 기본 기간은 7일 전~오늘이다. 환불 가능 금액 조회와 신규 등록은 별도 화면이다. 환불 가능 금액은 잔액·사용량·기환불·수수료 등의 규칙이 적용되므로 표시 금액과 상세 이력을 확인한다. 기존 신청의 정보 수정과 상태 변경은 상세 화면에서 수행한다.

공통 폼이 등록·수정·상세 입력값 조회 함수를 함께 포함할 수 있다. 아래 API 표에 공통 구현의 다른 모드가 표시되어도 현재 경로의 작업으로 모두 실행하는 것은 아니다.

**최초 화면의 선행 단계**: 처음에는 사업자번호 검색 영역과 **검색**, **목록**만 표시된다. 사업자번호로 업체 정보를 먼저 조회해야 환불 입력 폼이 표시된다. 업체 조회 전의 빈 검색에서는 **사업자번호를 입력해 주세요.**가 표시된다. 조회된 업체·환불 가능 금액을 확인한 다음 환불 정보를 입력하고 저장한다. 업체 조회 실패 상태에서 환불 등록 단계로 넘어가지 않는다.

비식별 화면 캡처: [초기 화면·빈값 검증](../../evidence/screenshots/refund-company-lookup.png). 입력·사용자 영역·표 본문은 마스킹했다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
|---|---|---|---|
| 사업자번호 | 입력·필수 | 화면 타입 text; 최대 10자; API 타입 String; 초기값 빈값 | `businessNumber`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/RefundRegistrationPage.tsx#L43) |
| 회사명 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/RefundRegistrationForm.tsx#L85) |
| 사업자 번호 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/RefundRegistrationForm.tsx#L91) |
| 담당자 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/RefundRegistrationForm.tsx#L97) |
| 연락처 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/RefundRegistrationForm.tsx#L103) |
| 환불은행 | 입력·선택(조건부 검증 별도) | 최대 50자 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/RefundRegistrationForm.tsx#L122) |
| 환불계좌 | 입력·선택(조건부 검증 별도) | 최대 20자 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/RefundRegistrationForm.tsx#L136) |
| 잔액 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/RefundRegistrationForm.tsx#L151) |
| 환불가능금액 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/RefundRegistrationForm.tsx#L157) |
| 환불신청금액 | 입력·선택(조건부 검증 별도) | 최대 10자 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/RefundRegistrationForm.tsx#L163) |

입력 검증 근거: [RefundRegistrationPage.rules.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/status/payment/RefundRegistrationPage.rules.ts). 프런트 검증과 서버 DTO 제약이 다르면 서버 검증이 최종 기준이다.

**복합 검색·폼의 초기 상태**

| 초기값 근거 | 기본 상태 |
|---|---|
| [DEFAULT_REFUND_FORM](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/RefundRegistrationPage.tsx#L34) | businessNumber=빈값; refundBank=빈값; refundAccount=빈값; refundApplicationAmount=0 |

화면 필드 키와 API 필드명이 다른 경우 변환은 Hook/API의 검색·저장 매핑에서 수행된다. 요청·응답 필드와 DB 컬럼 매핑은 아래 API 계약 및 DB 객체 계약에 연결했다.

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
|---|---|---|---|
| 환불 등록 사업자 정보 조회 | [GET /api/v1/service-status/refunds/registration/business-info](../../references/api-contracts.md#api118); `/payment/refund-management` / `VIEW` | `경로·쿼리·본문 계약 참조` → `businessInfo, refundInfo` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 환불 등록 | [POST /api/v1/service-status/refunds/registration/save](../../references/api-contracts.md#api236); `/payment/refund-management` / `PROCESS` | `businessNumber, refundBank, refundAccount, refundApplicationAmount, refundableAmount` → `success, message` | 쓰기 대상 smartbill3.dbo.service_refund, smartbill3.dbo.service_refund_his |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
|---|---|---|---|
| [Sb_Bill.dbo.UspBill_RefundCheck_ComRegNo](../../references/database-contracts.md#db080) | `@COM_REGNO varchar(16) IN` | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.company, smartbill3.dbo.member, smartbill3.dbo.service_prepay | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Sb_Bill.dbo.UspBill_refundInfo_INSERT](../../references/database-contracts.md#db083) | `@PREPAY_NO varchar(10) IN, @PRINCIPAL_AMT varchar(10) IN, @REFUND_AMT varchar(10) IN, @REFUND_NAME varchar(35) IN, @REFUND_TEL varchar(20) IN, @MEM_NO varchar(10) IN, @COM_NO varchar(10) IN, @BANK_NAME varchar(30) IN, @BANK_NO varchar(30) IN, @SW_ID varchar(10) IN, @REFUND_IDX int OUT` | 쓰기: smartbill3.dbo.service_refund, smartbill3.dbo.service_refund_his. 참조: smartbill3.dbo.service_refund, smartbill3.dbo.service_refund_his | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |

위 DB 계약 링크에는 실제 파라미터 타입·기본값·IN/OUT, Mapper 결과 컬럼, RETURN 바인딩, 참조 테이블·하위 프로시저·정의 필터/정렬을 기록했다. DTO·Service·Repository·Mapper의 상세 호출 경로는 각 API 계약에서 확인한다.

## 6) 예외 상황과 운영 확인

**빈값 입력 재현**: 사업자번호를 입력해 주세요.. 빈 입력에서 확인한 클라이언트 오류이며 저장 요청 성공·서버 검증 재현은 아니다.

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
|---|---|---|
| 결과가 없거나 기대 건수와 다름 | 적용된 검색 기준·기간·탭·대상 상태·서버 필터·페이징·목록/다운로드 조건 | 조건을 다시 확인하고 조회한다. 지속되면 경로·작업 시각·마스킹한 식별자·필터를 업무/기술 담당에게 전달한다. |
| 메뉴·버튼 미표시 또는 접근 거부 | 사용자 그룹의 메뉴 접근·VIEW 및 API별 PROCESS/EXECUTE/DELETE/EXCEL_DOWNLOAD/UNMASK 등 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. 프런트 버튼 표시만으로 서버 권한을 판단하지 않는다. |
| 저장·삭제·외부 실행의 결과가 불명확 | 대상 현재 상태·중복 요청·감사 이력·API 오류·파일/외부 소비 로그 | 기존 반영 여부를 먼저 조회한다. 중복 발송·초기화·금액 처리를 피하기 위해 기술 담당 확인 후 재시도한다. |

## 7) 검증·출처

**브라우저 검증(2026-11-09)**: 화면 대조. [경로별 결과와 제한](../../references/browser-verification.md#page078). 역할별 권한 거부·저장 성공·파일 반출·외부 연계 완료는 이 결과로 보장하지 않는다.

| 검증 항목 | 근거·환경 | 상태·확인일 |
|---|---|---|
| 대상 선정 | 사용자가 WBS 탭 내용으로 제공한 텍스트의 No. 213, 214, 215; [선정 태스크](../../inventory/wbs-tasks.csv) | 제공 텍스트 확인 2026-11-09. 원본 Excel의 탭/병합 셀을 독립 재열람한 것은 아님. |
| 메뉴·라우트·화면 | [menuConfig.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts); [PaymentRoutes.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/PaymentRoutes.tsx); [RefundRegistrationPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/RefundRegistrationPage.tsx) | 코드 확인 2026-11-09, 기준 dc216b313 |
| 기능·권한·API | 이 문서의 API 계약 링크 및 연결 Hook/API·Controller·DTO·Service·Repository·Mapper | 코드 확인 2026-11-09. 조회 요청·화면 대조 범위는 아래 브라우저 근거 참조. 권한 계정별 허용·거부 및 변경 요청 실행은 미확인. |
| DB 정의 | [개발 DB 계약](../../references/database-contracts.md), 이 문서의 연결 객체 | 개발 DB 정의 확인 2026-11-09. 동적 SQL·CLR 내부·정의 미공개 참조의 미확정 범위는 객체별 기록; 후속 확인 DB 담당. |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-e26f1d50aa7d3811) | Demo 메타데이터 2/2개 확인 · 2026-11-11 |
| 브라우저 화면·배포 환경 | 로컬 인증 계정·Playwright CLI; [화면별 검증표](../../references/browser-verification.md#page078) | 화면 대조, 2026-11-09. 배포본·타 역할·업무 변경 결과는 미확인. |
| 업무 프로시저·쓰기·외부 결과 | 격리된 검증 환경·테스트 데이터의 실행 결과 | 미확인: 명시적인 저장·삭제·발송·초기화 요청은 실행하지 않음. 브라우저 GET의 업무 조회 프로시저·조회수·감사 기록은 별도 영향으로 구분. 격리 환경에서 기술 담당 확인. |

코드 확인과 DB 정의 확인은 실행 성공·업무 승인·다른 환경 적용을 보장하지 않는다. 업무·기술 담당 검토 후 조사 목록의 상태를 완료로 변경한다.

브라우저 직접 근거: [settled-static-recheck](../../evidence/browser/static-stable.json). 경로·고정 버튼명·입력 속성·표 머리글·API 상태를 보관했고 실제 데이터 값·식별자·인증정보는 제외했다.

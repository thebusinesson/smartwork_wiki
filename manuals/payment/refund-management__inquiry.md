# [서비스 현황] 환불 관리 (환불 가능 금액 조회) 관리자 매뉴얼

작성 기준: `dc216b313` · 확인일 2026-11-09 · 조사 상태 **검토 대기**. 코드·개발 DB 정의 확인. 브라우저: **화면 대조**; 저장·발송 등 업무 실행 결과는 미검증이다.

## 1) 화면 기본 정보

### 도메인 이해

고객의 서비스 요금 입금과 미리 보유한 금액, 환불 신청을 관리하는 업무다. 입금 내역이 어느 업체·청구에 연결되는지, 예치금이 어떻게 늘거나 줄었는지, 환불 가능한 금액과 처리 상태가 무엇인지 확인한다.

| 구분 | 설명 |
|---|---|
| 업무 영역 | 입금·예치금·환불 관리 · 서비스 현황 > 입금관리 > 환불 관리 |
| 주요 대상·용어 | 입금: 접수된 납부 내역 / 예치금: 서비스 이용을 위해 보유·차감되는 금액 / 청구월: 요금을 청구한 월 / 환불 신청: 환불 대상·금액·계좌·처리 상태 기록 |
| 업무 흐름 | 업체·기간·청구 찾기 → 입금·잔액·이력 확인 → 허용된 입금/예치금/환불 처리 → 상태·금액 재확인 |
| 이 페이지의 역할 | 환불을 신청하기 전에 업체별 환불 가능 금액을 확인하는 화면이다. 금액 조회 자체로 환불 신청이나 은행 송금이 완료되지 않는다. |
| 관련 업무와 구분 | 예치금 잔액·환불 가능 금액·환불 신청 금액은 같은 값이 아니다. 화면의 처리 완료와 실제 은행 송금 완료의 확인 범위를 구분한다. |

도메인 설명 근거: 이 문서 7번의 현재 메뉴·라우트·화면 및 API·업무 규칙 소스. [전체 도메인 지도](../../references/domain-overview.md#payment). 설명 보강일 2026-11-09; 기존 실행 검증 범위와 미확인 상태는 변경하지 않았다.

### 화면 정보

| 항목 | 작성 내용 |
|---|---|
| 업무 도메인·목적 | 환불 신청을 조회·등록하고 환불 가능 금액과 처리 상태를 관리한다. |
| 메뉴·화면 경로 | 서비스 현황 > 입금관리 > 환불 관리; `/payment/refund-management/inquiry`; 메뉴 또는 관련 화면에서 진입한다. |
| 화면 유형·담당 | 환불 가능 금액 조회; WBS 작업자 유지윤. 업무·기술 담당 팀명은 원문에 없어 배포 전 해당 도메인 담당자가 확정한다. |
| 관련 화면 | [조회·관리](refund-management.md); [등록](refund-management__new.md); [상세](refund-management__by-refundNo.md) |

WBS 근거: No. 213, 214, 215 (사용자가 제공한 텍스트 행 270, 271, 272). API 개발/화면 개발의 중복 행은 같은 화면으로 통합했다.

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
|---|---|---|
| 화면 진입·조회 | `/payment/refund-management` 메뉴 접근·하위 경로 작업 권한. 조회 API는 VIEW, 등록/수정 경로는 PROCESS 등 아래 서버 액션과 라우트 가드를 함께 적용한다. | 로그인된 관리자 계정; 아래 검색·입력 항목을 준비한다. |
| 목록 | `/payment/refund-management`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |

서버가 최종 권한을 검사한다. 버튼 모양(kind)으로 권한을 추정하지 않는다. 특히 등록·수정이 PROCESS를 사용하는 API와 EXECUTE·UNMASK·EXCEL_DOWNLOAD는 서로 구분한다.

## 3) 화면 사용 절차

**검증 시 화면 버튼**: 검색, 초기화, 목록. 화면 상태·대상에 따라 달라지며 아래 작업 절차와 권한 조건을 함께 확인한다.

1. 관련 화면에서 대상 또는 작업을 선택하여 `/payment/refund-management/inquiry`로 이동한다. 경로 변수는 주소에서 임의로 바꾸지 않고 이전 화면이 전달한 식별자를 사용한다.
2. 대상의 기본 정보·상태·표시 항목을 확인한다. 목록의 식별자와 상세 대상이 일치하는지 확인한다.
3. 표·탭·이력 영역에서 필요한 내역을 확인한다. 버튼의 표시·활성 조건과 아래 API별 권한을 확인한다. 저장·삭제·외부 호출 전에는 대상과 현재 상태를 재확인한다.
4. 작업 결과 또는 다운로드 파일을 확인하고 관련 목록으로 돌아가 변경된 상태를 다시 조회한다.

**이 화면에서 유의할 업무 규칙**: 목록의 기본 기간은 7일 전~오늘이다. 환불 가능 금액 조회와 신규 등록은 별도 화면이다. 환불 가능 금액은 잔액·사용량·기환불·수수료 등의 규칙이 적용되므로 표시 금액과 상세 이력을 확인한다. 기존 신청의 정보 수정과 상태 변경은 상세 화면에서 수행한다.

## 4) 입력·표시 데이터

**검증 시 표시된 날짜 필터**: YYYY-MM-DD `2026-11-09`. 검증 날짜·조건 복원에 따른 표시값이며 모든 실행의 고정 기본값을 뜻하지 않는다.

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
|---|---|---|---|
| 사업자번호 | 입력·선택(조건부 검증 별도) | 화면 타입 text; 최대 10자; API 타입 String?; 기본 null; 초기값 빈값 | `businessNumber`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/RefundAmountInquiryPage.tsx#L40) |
| 환불요청 일자 | 입력·선택(조건부 검증 별도) | 화면 타입 date; API 타입 String?; 기본 null; 초기값 {getCurrentDate()} | `refundApplicationDate`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/RefundAmountInquiryPage.tsx#L54) |
| 충전일자 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `chargeDateFormatted`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/RefundAmountTable.tsx#L49) |
| 충전금액 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `chargeAmountFormatted`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/RefundAmountTable.tsx#L50) |
| 잔액 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `balanceFormatted`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/RefundAmountTable.tsx#L51) |
| 환불신청일 | 출력 | API 타입 String?; 기본 null; 초기값 {getCurrentDate()} | `refundApplicationDate`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/RefundAmountTable.tsx#L52) |
| 차감율 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `deductionRateFormatted`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/RefundAmountTable.tsx#L53) |
| 수수료 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `feeFormatted`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/RefundAmountTable.tsx#L54) |
| 환불가능금액 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `refundableAmountFormatted`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/RefundAmountTable.tsx#L55) |

**복합 검색·폼의 초기 상태**

| 초기값 근거 | 기본 상태 |
|---|---|
| [createDefaultFilterValues](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/RefundAmountInquiryPage.tsx#L32) | businessNumber=빈값; refundApplicationDate={getCurrentDate()} |

화면 필드 키와 API 필드명이 다른 경우 변환은 Hook/API의 검색·저장 매핑에서 수행된다. 요청·응답 필드와 DB 컬럼 매핑은 아래 API 계약 및 DB 객체 계약에 연결했다.

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
|---|---|---|---|
| 환불 가능 금액 조회 | [GET /api/v1/service-status/refunds/available-amount](../../references/api-contracts.md#api117); `/payment/refund-management` / `VIEW` | `businessNumber, refundApplicationDate` → `data, totalFee, totalRefundableAmount, id, chargeDate, chargeAmount, balance, refundApplicationDate, deductionRate, fee, refundableAmount, expired` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
|---|---|---|---|
| [smartwork.dbo.UspBill_RefundExpiredCharge_SELECT](../../references/database-contracts.md#db315) | `@COM_REGNO varchar(16) IN, @REFUND_DATE varchar(10) IN` | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.company, smartbill3.dbo.service_prepay | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_COMMON.dbo.upSBAdm_RefundBillList](../../references/database-contracts.md#db112) | `@COM_REGNO varchar(16) IN, @REFUNDDATE varchar(10) IN` | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.company, smartbill3.dbo.service_prepay, smartbill3.dbo.service_prepay_his | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |

위 DB 계약 링크에는 실제 파라미터 타입·기본값·IN/OUT, Mapper 결과 컬럼, RETURN 바인딩, 참조 테이블·하위 프로시저·정의 필터/정렬을 기록했다. DTO·Service·Repository·Mapper의 상세 호출 경로는 각 API 계약에서 확인한다.

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
|---|---|---|
| 검색 결과가 없습니다. | [문구·처리 코드](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/RefundAmountTable.tsx#L95); 현재 조건·대상·권한 확인 | 검색·조회 오류면 조건을 확인 후 재조회. 변경·발송 결과가 불명확하면 처리 여부와 이력을 확인한 뒤 재시도 여부를 판단한다. |
| 결과가 없거나 기대 건수와 다름 | 적용된 검색 기준·기간·탭·대상 상태·서버 필터·페이징·목록/다운로드 조건 | 조건을 다시 확인하고 조회한다. 지속되면 경로·작업 시각·마스킹한 식별자·필터를 업무/기술 담당에게 전달한다. |
| 메뉴·버튼 미표시 또는 접근 거부 | 사용자 그룹의 메뉴 접근·VIEW 및 API별 PROCESS/EXECUTE/DELETE/EXCEL_DOWNLOAD/UNMASK 등 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. 프런트 버튼 표시만으로 서버 권한을 판단하지 않는다. |
| 저장·삭제·외부 실행의 결과가 불명확 | 대상 현재 상태·중복 요청·감사 이력·API 오류·파일/외부 소비 로그 | 기존 반영 여부를 먼저 조회한다. 중복 발송·초기화·금액 처리를 피하기 위해 기술 담당 확인 후 재시도한다. |

## 7) 검증·출처

**브라우저 검증(2026-11-09)**: 화면 대조. [경로별 결과와 제한](../../references/browser-verification.md#page077). 역할별 권한 거부·저장 성공·파일 반출·외부 연계 완료는 이 결과로 보장하지 않는다.

| 검증 항목 | 근거·환경 | 상태·확인일 |
|---|---|---|
| 대상 선정 | 사용자가 WBS 탭 내용으로 제공한 텍스트의 No. 213, 214, 215; [선정 태스크](../../inventory/wbs-tasks.csv) | 제공 텍스트 확인 2026-11-09. 원본 Excel의 탭/병합 셀을 독립 재열람한 것은 아님. |
| 메뉴·라우트·화면 | [menuConfig.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts); [PaymentRoutes.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/PaymentRoutes.tsx); [RefundAmountInquiryPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/RefundAmountInquiryPage.tsx) | 코드 확인 2026-11-09, 기준 dc216b313 |
| 기능·권한·API | 이 문서의 API 계약 링크 및 연결 Hook/API·Controller·DTO·Service·Repository·Mapper | 코드 확인 2026-11-09. 조회 요청·화면 대조 범위는 아래 브라우저 근거 참조. 권한 계정별 허용·거부 및 변경 요청 실행은 미확인. |
| DB 정의 | [개발 DB 계약](../../references/database-contracts.md), 이 문서의 연결 객체 | 개발 DB 정의 확인 2026-11-09. 동적 SQL·CLR 내부·정의 미공개 참조의 미확정 범위는 객체별 기록; 후속 확인 DB 담당. |
| 브라우저 화면·배포 환경 | 로컬 인증 계정·Playwright CLI; [화면별 검증표](../../references/browser-verification.md#page077) | 화면 대조, 2026-11-09. 배포본·타 역할·업무 변경 결과는 미확인. |
| 업무 프로시저·쓰기·외부 결과 | 격리된 검증 환경·테스트 데이터의 실행 결과 | 미확인: 명시적인 저장·삭제·발송·초기화 요청은 실행하지 않음. 브라우저 GET의 업무 조회 프로시저·조회수·감사 기록은 별도 영향으로 구분. 격리 환경에서 기술 담당 확인. |

코드 확인과 DB 정의 확인은 실행 성공·업무 승인·다른 환경 적용을 보장하지 않는다. 업무·기술 담당 검토 후 조사 목록의 상태를 완료로 변경한다.

브라우저 직접 근거: [settled-static-recheck](../../evidence/browser/static-stable.json). 경로·고정 버튼명·입력 속성·표 머리글·API 상태를 보관했고 실제 데이터 값·식별자·인증정보는 제외했다.

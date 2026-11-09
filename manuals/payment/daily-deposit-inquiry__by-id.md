# [서비스 현황] 일별 예치금 조회 (상세) 관리자 매뉴얼

작성 기준: `dc216b313` · 확인일 2026-11-09 · 조사 상태 **검토 대기**. 코드와 개발 DB 정의를 확인했으며 실제 화면·업무 실행은 미재현이다.

## 1) 화면 기본 정보

| 항목 | 작성 내용 |
|---|---|
| 업무 도메인·목적 | 발생일 기준의 예치금 충전·차감 내역을 조회한다. |
| 메뉴·화면 경로 | 서비스 현황 > 입금관리 > 일별 예치금 조회; `/payment/daily-deposit-inquiry/:id`; 목록에서 선택한 대상의 경로 변수를 유지하여 진입한다. |
| 화면 유형·담당 | 상세; WBS 작업자 유지윤. 업무·기술 담당 팀명은 원문에 없어 배포 전 해당 도메인 담당자가 확정한다. |
| 관련 화면 | [조회·관리](daily-deposit-inquiry.md) |

WBS 근거: No. 186 (사용자가 제공한 텍스트 행 233). API 개발/화면 개발의 중복 행은 같은 화면으로 통합했다.

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
|---|---|---|
| 화면 진입·조회 | `/payment/daily-deposit-inquiry` 메뉴 접근·하위 경로 작업 권한. 조회 API는 VIEW, 등록/수정 경로는 PROCESS 등 아래 서버 액션과 라우트 가드를 함께 적용한다. | 로그인된 관리자 계정; id 식별자는 이전 화면에서 선택한다. |
| 입금 취소 | `/payment/daily-deposit-inquiry`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 입금 처리 | `/payment/daily-deposit-inquiry`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 소멸 처리 | `/payment/daily-deposit-inquiry`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 목록 | `/payment/daily-deposit-inquiry`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |

서버가 최종 권한을 검사한다. 버튼 모양(kind)으로 권한을 추정하지 않는다. 특히 등록·수정이 PROCESS를 사용하는 API와 EXECUTE·UNMASK·EXCEL_DOWNLOAD는 서로 구분한다.

## 3) 화면 사용 절차

1. 관련 화면에서 대상 또는 작업을 선택하여 `/payment/daily-deposit-inquiry/:id`로 이동한다. 경로 변수는 주소에서 임의로 바꾸지 않고 이전 화면이 전달한 식별자를 사용한다.
2. 대상의 기본 정보·상태·표시 항목을 확인한다. 목록의 식별자와 상세 대상이 일치하는지 확인한다.
3. **입금 취소, 입금 처리, 소멸 처리** 중 필요한 작업을 선택한다. 버튼의 표시·활성 조건과 아래 API별 권한을 확인한다. 저장·삭제·외부 호출 전에는 대상과 현재 상태를 재확인한다.
4. 작업 결과 또는 다운로드 파일을 확인하고 관련 목록으로 돌아가 변경된 상태를 다시 조회한다.

**이 화면에서 유의할 업무 규칙**: 기본 구분은 충전, 업체 조건은 사업자번호다. 충전방식과 기간을 지정하여 검색한다. 상세는 예치금 관리 상세와 공통 구현이지만 진입 경로와 복귀 목록이 다르다. 날짜 종료일의 당일 누락 여부는 현재 개발 DB 정의의 범위 조건과 함께 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
|---|---|---|---|
| 등록일시 | 출력 | API 타입 String | `registrationDate`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/DepositManagementDetailPage.tsx#L193) |
| 구분 | 출력 | API 타입 String | `type`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/DepositManagementDetailPage.tsx#L203) |
| 담당자 | 출력 | API 타입 String | `manager`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/DepositManagementDetailPage.tsx#L217) |
| 충전액 | 출력 | API 타입 Long | `chargeAmount`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/DepositManagementDetailPage.tsx#L218) |
| 차감액 | 출력 | API 타입 Long | `deductionAmount`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/DepositManagementDetailPage.tsx#L221) |
| 이월액 | 출력 | API 타입 Long | `availableAmount`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/DepositManagementDetailPage.tsx#L223) |
| ORDER-ID | 출력 | API 타입 String? | `orderId`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/DepositManagementDetailPage.tsx#L230) |
| 회사명 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/DepositManagementDetailPage.tsx#L275) |
| 사업자 번호 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/DepositManagementDetailPage.tsx#L279) |
| 사용가능 금액 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/DepositManagementDetailPage.tsx#L297) |
| 최종 충전일 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/DepositManagementDetailPage.tsx#L303) |
| 서비스 사용내역 제외 | 출력 | API 타입 Boolean?; 기본 false | `excludeServiceUsage`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/DepositManagementDetailPage.tsx#L323) |

입력 검증 근거: [DepositManagementProcessingDialog.rules.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/status/payment/components/DepositManagementProcessingDialog.rules.ts), [DepositManagementProcessingDialog.schema.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/status/payment/components/DepositManagementProcessingDialog.schema.ts), [validationUtils.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/status/payment/utils/validationUtils.ts), [DepositLapseProcessingDialog.rules.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/status/payment/components/DepositLapseProcessingDialog.rules.ts), [DepositLapseProcessingDialog.schema.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/status/payment/components/DepositLapseProcessingDialog.schema.ts). 프런트 검증과 서버 DTO 제약이 다르면 서버 검증이 최종 기준이다.

화면 필드 키와 API 필드명이 다른 경우 변환은 Hook/API의 검색·저장 매핑에서 수행된다. 요청·응답 필드와 DB 컬럼 매핑은 아래 API 계약 및 DB 객체 계약에 연결했다.

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
|---|---|---|---|
| 예치금 사업자번호 lookup | [GET /api/v1/service-status/prepayment/lookup](../../references/api-contracts.md#api113); `/payment/deposit` / `VIEW` | `경로·쿼리·본문 계약 참조` → `companyInfo, transactions, totalElements, totalPages, currentPage, size, canProcess, prepayNo, comNo, companyName, businessNumber, availableAmount, lastChargeDate, id, registration` | Mapper 프로시저의 정적 테이블 쓰기 미검출; 동적 SQL의 런타임 대상은 미확정 |
| 입금처리 대상 업체 조회 | [GET /api/v1/service-status/prepayment/target-company](../../references/api-contracts.md#api114); `/payment/deposit` / `VIEW` | `경로·쿼리·본문 계약 참조` → `comNo, companyName` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 예치금 상세 조회 | [GET /api/v1/service-status/prepayment/{businessNumber}](../../references/api-contracts.md#api115); `/payment/deposit` / `VIEW` | `prepayNo, comNo, excludeServiceUsage, page, size` → `companyInfo, transactions, totalElements, totalPages, currentPage, size, canProcess, prepayNo, comNo, companyName, businessNumber, availableAmount, lastChargeDate, id, registration` | Mapper 프로시저의 정적 테이블 쓰기 미검출; 동적 SQL의 런타임 대상은 미확정 |
| 예치금 일괄 입금 처리 | [POST /api/v1/service-status/prepayment/process](../../references/api-contracts.md#api234); `/payment/deposit` / `PROCESS` | `prepayNo, comNo, businessNumber, amount, type, reason, cloverBusinessNumber, cloverCount, remark` → `응답 DTO·파일/처리 결과 계약 참조` | 쓰기 대상 sb_common.dbo.free_service, sb_common.dbo.free_service_his, smartbill3.dbo.service_prepay, smartbill3.dbo.service_prepay_his |
| 예치금 입금 취소 | [POST /api/v1/service-status/prepayment/cancel](../../references/api-contracts.md#api233); `/payment/deposit` / `PROCESS` | `comNo, businessNumber, transactionId, orderId, reason` → `응답 DTO·파일/처리 결과 계약 참조` | 쓰기 대상 sb_bill.dbo.invoice, sb_bill.dbo.payment, sb_bill.dbo.payment_his, sb_bill.dbo.service_prepay_monthly_remain, sb_bill.dbo.service_prepay_monthly_remain_card_cancle_history, smartbill3.dbo.accinfo_cancel, smartbill3.dbo.accinfo_history, smartbill3.dbo.company, smartbill3.dbo.service_prepay, smartbill3.dbo.service_prepay_his |
| 청구 금액 조회 | [GET /api/v1/service-status/prepayment/{businessNumber}/charge-amount](../../references/api-contracts.md#api116); `/payment/deposit` / `VIEW` | `경로·쿼리·본문 계약 참조` → `chargeMonth, invoiceAmount` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 예치금 입금 처리 | [POST /api/v1/service-status/prepayment/{businessNumber}/process](../../references/api-contracts.md#api235); `/payment/deposit` / `PROCESS` | `prepayNo, comNo, chargeMonth, processAmount, remark` → `응답 DTO·파일/처리 결과 계약 참조` | 쓰기 대상 sb_bill.dbo.invoice, sb_bill.dbo.payment, sb_bill.dbo.payment_his, smartbill3.dbo.company, smartbill3.dbo.company_history, smartbill3.dbo.service_prepay, smartbill3.dbo.service_prepay_his |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
|---|---|---|---|
| [SB_BILL.dbo.UspBill_BalanceDetailInfo_SELECT_WITH_USEAGE_HIS](../../references/database-contracts.md#db070) | `@PAGE int IN, @TOP int IN, @COM_NO int IN` | 확정한 테이블 쓰기 없음. 참조: office.dbo.sawon, sb_bill.dbo.payment, sb_dti.dbo.dti_sign_cub, sb_dti.dbo.dti_sign_cub_2023_07, sb_dti.dbo.dti_sign_cub_part, sb_dti.dbo.dti_sign_cub_prev_buffer, smartbill3.dbo.company, smartbill3.dbo.member 외 2개 동적 SQL 포함, 런타임 조합 대상 미확정. | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_BILL.dbo.UspBill_BalanceDetailInfo_SELECT_WITHOUT_USEAGE_HIS](../../references/database-contracts.md#db071) | `@PAGE int IN, @TOP int IN, @COM_NO int IN` | 확정한 테이블 쓰기 없음. 참조: office.dbo.sawon, sb_bill.dbo.payment, smartbill3.dbo.company, smartbill3.dbo.member, smartbill3.dbo.service_prepay, smartbill3.dbo.service_prepay_his 동적 SQL 포함, 런타임 조합 대상 미확정. | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.UspBill_DepositCancelDate_SELECT](../../references/database-contracts.md#db303) | `@IDX_LIST varchar(max) IN` | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.service_prepay_his | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_BILL.dbo.UspBill_BalanceTopInfo_SELECT](../../references/database-contracts.md#db073) | `@PREPAY_NO int IN, @RESULT varchar(1) OUT` | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.service_prepay | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_BILL.dbo.UspBill_BalanceInfo_SELECT](../../references/database-contracts.md#db072) | `@PREPAY_NO int IN` | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.company, smartbill3.dbo.service_prepay | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SMARTBILL3.dbo.SERVICE_PREPAY](../../references/database-contracts.md#db207) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.service_prepay | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SMARTBILL3.dbo.COMPANY](../../references/database-contracts.md#db197) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.company | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.UspBill_BalanceDepositProcess2](../../references/database-contracts.md#db298) | `@IDX int IN, @AMOUNT int IN, @SW_NO int IN, @RESULT varchar(5) OUT` | 쓰기: smartbill3.dbo.service_prepay, smartbill3.dbo.service_prepay_his. 참조: smartbill3.dbo.service_prepay, smartbill3.dbo.service_prepay_his | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_BILL.dbo.UspBill_LapseDepositSaveCloverProcess](../../references/database-contracts.md#db076) | `@IDX int IN, @AMOUNT int IN, @SW_NO int IN, @CLOVER_COM_NO int IN, @CLOVER_CNT int IN, @REMARK varchar(300) IN, @RESULT varchar(5) OUT` | 쓰기: sb_common.dbo.free_service, sb_common.dbo.free_service_his, smartbill3.dbo.service_prepay, smartbill3.dbo.service_prepay_his. 참조: sb_common.dbo.free_service, sb_common.dbo.free_service_his, smartbill3.dbo.service_prepay, smartbill3.dbo.service_prepay_his | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Sb_Bill.dbo.UspBill_SearchCompanyRegno_SELECT](../../references/database-contracts.md#db087) | `@COMREGNO varchar(13) IN` | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.company | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Sb_Bill.dbo.UspBill_BalanceDepositAmountInfo_SELECT](../../references/database-contracts.md#db068) | `@IDX int IN` | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.service_prepay | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_BILL.dbo.UPMEM_ACCETC_CANCEL](../../references/database-contracts.md#db065) | `@COM_NO int IN, @MEM_NO int IN, @ORDER_ID varchar(64) IN, @PREPAYNO int IN, @RESULT varchar(5) OUT` | 쓰기: sb_bill.dbo.invoice, sb_bill.dbo.payment, sb_bill.dbo.payment_his, sb_bill.dbo.service_prepay_monthly_remain, sb_bill.dbo.service_prepay_monthly_remain_card_cancle_history, smartbill3.dbo.accinfo_cancel, smartbill3.dbo.accinfo_history, smartbill3.dbo.company, smartbill3.dbo.service_prepay, smartbill3.dbo.service_prepay_his. 참조: sb_bill.dbo.close, sb_bill.dbo.invoice, sb_bill.dbo.payment, sb_bill.dbo.payment_his, sb_bill.dbo.service_prepay_monthly_remain, sb_bill.dbo.service_prepay_monthly_remain_card_cancle_history, smartbill3.dbo.accinfo_cancel, smartbill3.dbo.accinfo_history 외 4개 | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_BILL.dbo.UspBill_HeadOfficeDepositProcessChargeAmount_SELECT](../../references/database-contracts.md#db075) | `@COM_NO varchar(10) IN, @CHARGE_MONTH varchar(10) IN` | 확정한 테이블 쓰기 없음. 참조: sb_bill.dbo.invoice, sb_bill.dbo.payment, smartbill3.dbo.company | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_BILL.dbo.UspBill_BalanceDepositProcessInfo_INSERT](../../references/database-contracts.md#db069) | `@IDX varchar(20) IN, @COM_NO int IN, @CHARGE_MONTH varchar(10) IN, @AMOUNT int IN, @STATE varchar(10) IN, @REMARK varchar(200) IN, @SW_NO int IN, @RESULT varchar(1) OUT` | 쓰기: sb_bill.dbo.invoice, sb_bill.dbo.payment, sb_bill.dbo.payment_his, smartbill3.dbo.company, smartbill3.dbo.company_history, smartbill3.dbo.service_prepay, smartbill3.dbo.service_prepay_his. 참조: sb_bill.dbo.invoice, sb_bill.dbo.payment, sb_bill.dbo.payment_his, smartbill3.dbo.company, smartbill3.dbo.company_history, smartbill3.dbo.member, smartbill3.dbo.service_prepay, smartbill3.dbo.service_prepay_his | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |

위 DB 계약 링크에는 실제 파라미터 타입·기본값·IN/OUT, Mapper 결과 컬럼, RETURN 바인딩, 참조 테이블·하위 프로시저·정의 필터/정렬을 기록했다. DTO·Service·Repository·Mapper의 상세 호출 경로는 각 API 계약에서 확인한다.

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
|---|---|---|
| 결과가 없거나 기대 건수와 다름 | 적용된 검색 기준·기간·탭·대상 상태·서버 필터·페이징·목록/다운로드 조건 | 조건을 다시 확인하고 조회한다. 지속되면 경로·작업 시각·마스킹한 식별자·필터를 업무/기술 담당에게 전달한다. |
| 메뉴·버튼 미표시 또는 접근 거부 | 사용자 그룹의 메뉴 접근·VIEW 및 API별 PROCESS/EXECUTE/DELETE/EXCEL_DOWNLOAD/UNMASK 등 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. 프런트 버튼 표시만으로 서버 권한을 판단하지 않는다. |
| 저장·삭제·외부 실행의 결과가 불명확 | 대상 현재 상태·중복 요청·감사 이력·API 오류·파일/외부 소비 로그 | 기존 반영 여부를 먼저 조회한다. 중복 발송·초기화·금액 처리를 피하기 위해 기술 담당 확인 후 재시도한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
|---|---|---|
| 대상 선정 | 사용자가 WBS 탭 내용으로 제공한 텍스트의 No. 186; [선정 태스크](../../inventory/wbs-tasks.csv) | 제공 텍스트 확인 2026-11-09. 원본 Excel의 탭/병합 셀을 독립 재열람한 것은 아님. |
| 메뉴·라우트·화면 | [menuConfig.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts); [PaymentRoutes.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/PaymentRoutes.tsx); [DepositManagementDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/DepositManagementDetailPage.tsx) | 코드 확인 2026-11-09, 기준 dc216b313 |
| 기능·권한·API | 이 문서의 API 계약 링크 및 연결 Hook/API·Controller·DTO·Service·Repository·Mapper | 코드 확인 2026-11-09. 요청 실행·권한 계정별 재현은 미확인. |
| DB 정의 | [개발 DB 계약](../../references/database-contracts.md), 이 문서의 연결 객체 | 개발 DB 정의 확인 2026-11-09. 동적 SQL·CLR 내부·정의 미공개 참조의 미확정 범위는 객체별 기록; 후속 확인 DB 담당. |
| 브라우저 화면·배포 환경 | 실제 검증 계정의 정상·빈 결과·권한 부족·입력 오류 및 현재 배포본 | 미확인: 브라우저 실행 검증을 수행하지 않음. 배포 전 업무 담당·QA·기술 담당 확인. |
| 업무 프로시저·쓰기·외부 결과 | 격리된 검증 환경·테스트 데이터의 실행 결과 | 미확인: 공유 개발 DB의 업무 프로시저·쓰기·발송을 실행하지 않음. 격리 환경에서 기술 담당 확인. |

코드 확인과 DB 정의 확인은 실행 성공·업무 승인·다른 환경 적용을 보장하지 않는다. 업무·기술 담당 검토 후 조사 목록의 상태를 완료로 변경한다.

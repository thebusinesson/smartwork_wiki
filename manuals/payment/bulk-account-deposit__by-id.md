# [서비스 현황] 벌크식계좌 입금 관리 (상세) 관리자 매뉴얼

작성 기준: `dc216b313` · 확인일 2026-11-09 · 조사 상태 **검토 대기**. 코드와 개발 DB 정의를 확인했으며 실제 화면·업무 실행은 미재현이다.

## 1) 화면 기본 정보

| 항목 | 작성 내용 |
|---|---|
| 업무 도메인·목적 | 벌크식 계좌 입금의 처리 상태와 청구 구분을 조회하고 입금·예치금 처리를 수행한다. |
| 메뉴·화면 경로 | 서비스 현황 > 입금관리 > 벌크식계좌 입금 관리; `/payment/bulk-account-deposit/:id`; 목록에서 선택한 대상의 경로 변수를 유지하여 진입한다. |
| 화면 유형·담당 | 상세; WBS 작업자 유지윤. 업무·기술 담당 팀명은 원문에 없어 배포 전 해당 도메인 담당자가 확정한다. |
| 관련 화면 | [조회·관리](bulk-account-deposit.md) |

WBS 근거: No. 187, 188, 189 (사용자가 제공한 텍스트 행 235, 236, 237). API 개발/화면 개발의 중복 행은 같은 화면으로 통합했다.

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
|---|---|---|
| 화면 진입·조회 | `/payment/bulk-account-deposit` 메뉴 접근·하위 경로 작업 권한. 조회 API는 VIEW, 등록/수정 경로는 PROCESS 등 아래 서버 액션과 라우트 가드를 함께 적용한다. | 로그인된 관리자 계정; id 식별자는 이전 화면에서 선택한다. |
| 입금처리 | `/payment/bulk-account-deposit`; 화면 게이트 PROCESS. 실제 서버 액션은 API별 표 참조. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 예치금처리 | `/payment/bulk-account-deposit`; 화면 게이트 PROCESS. 실제 서버 액션은 API별 표 참조. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 목록 | `/payment/bulk-account-deposit`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 조회 중... | `/payment/bulk-account-deposit`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 검색 | `/payment/bulk-account-deposit`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 추가 | `/payment/bulk-account-deposit`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 취소 | `/payment/bulk-account-deposit`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 처리 중... | `/payment/bulk-account-deposit`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 차감 취소 | `/payment/bulk-account-deposit`; 화면 게이트 PROCESS. 실제 서버 액션은 API별 표 참조. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 차감 | `/payment/bulk-account-deposit`; 화면 게이트 PROCESS. 실제 서버 액션은 API별 표 참조. | 작업 대상과 현재 상태·변경 내용을 확인한다. |

서버가 최종 권한을 검사한다. 버튼 모양(kind)으로 권한을 추정하지 않는다. 특히 등록·수정이 PROCESS를 사용하는 API와 EXECUTE·UNMASK·EXCEL_DOWNLOAD는 서로 구분한다.

## 3) 화면 사용 절차

1. 관련 화면에서 대상 또는 작업을 선택하여 `/payment/bulk-account-deposit/:id`로 이동한다. 경로 변수는 주소에서 임의로 바꾸지 않고 이전 화면이 전달한 식별자를 사용한다.
2. 대상의 기본 정보·상태·표시 항목을 확인한다. 목록의 식별자와 상세 대상이 일치하는지 확인한다.
3. **입금처리, 예치금처리, 조회 중..., 검색, 추가, 처리 중..., 차감 취소, 차감** 중 필요한 작업을 선택한다. 버튼의 표시·활성 조건과 아래 API별 권한을 확인한다. 저장·삭제·외부 호출 전에는 대상과 현재 상태를 재확인한다.
4. 작업 결과 또는 다운로드 파일을 확인하고 관련 목록으로 돌아가 변경된 상태를 다시 조회한다.

**이 화면에서 유의할 업무 규칙**: 입금일·업체·처리상태·청구구분으로 검색한다. 상세에서 업체·청구월·처리금액을 확인한다. 입금대기와 잔액 조건에 따라 처리 버튼이 달라지며 처리 요청의 중복 실행은 잔액과 이력을 확인한 후 판단한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
|---|---|---|---|
| 사업자번호 | 출력 | API 타입 String | `businessNumber`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/BulkAccountDepositManagementDetailPage.tsx#L39) |
| 회사명 | 출력 | API 타입 String | `companyName`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/BulkAccountDepositManagementDetailPage.tsx#L46) |
| 청구구분 | 출력 | API 타입 String | `chargeGubun`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/BulkAccountDepositManagementDetailPage.tsx#L53) |
| 청구월 | 출력 | API 타입 String | `chargeMonth`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/BulkAccountDepositManagementDetailPage.tsx#L60) |
| 청구금액 | 출력 | API 타입 Long? | `chargeAmount`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/BulkAccountDepositManagementDetailPage.tsx#L67) |
| 처리금액 | 출력 | API 타입 Long | `processedAmount`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/BulkAccountDepositManagementDetailPage.tsx#L76) |
| 처리상태 | 출력 | API 타입 String | `processStatus`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/BulkAccountDepositManagementDetailPage.tsx#L85) |
| 처리일자 | 출력 | API 타입 String | `processDate`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/BulkAccountDepositManagementDetailPage.tsx#L92) |
| 처리자 | 출력 | API 타입 String | `processor`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/BulkAccountDepositManagementDetailPage.tsx#L99) |
| 선택 | 출력 | API 타입 Int | `comNo`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/BulkAccountDepositProcessingDialog.tsx#L452) |
| 회사명 | 출력 | API 타입 String | `comName`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/BulkAccountDepositProcessingDialog.tsx#L467) |
| 사업자번호 | 출력 | API 타입 String | `comRegno`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/BulkAccountDepositProcessingDialog.tsx#L472) |
| 청구구분 | 출력 | API 타입 String | `gubun`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/BulkAccountDepositProcessingDialog.tsx#L478) |
| 청구금액 (잔액) | 출력 | API 타입 Long | `billingAmount`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/BulkAccountDepositProcessingDialog.tsx#L491) |
| 입금 처리 금액 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `processAmountInput`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/BulkAccountDepositProcessingDialog.tsx#L500) |
| 청구 구분 | 출력 | API 타입 String | `gubun`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/BulkAccountDepositProcessingDialog.tsx#L547) |
| 청구금액 | 출력 | API 타입 Long | `billingAmount`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/BulkAccountDepositProcessingDialog.tsx#L561) |
| 처리금액 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `processAmount`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/BulkAccountDepositProcessingDialog.tsx#L571) |
| 단발성 | 입력·선택(조건부 검증 별도) | 길이·형식·조건부 필수는 검증 코드와 API DTO 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/BulkAccountDepositProcessingDialog.tsx#L684) |

입력 검증 근거: [createProcessAmountSchema.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/status/payment/components/createProcessAmountSchema.ts), [validationUtils.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/status/payment/utils/validationUtils.ts), [CommonPrepaidProcessingDialog.schema.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/status/payment/components/CommonPrepaidProcessingDialog.schema.ts), [depositTargetSchemas.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/status/payment/components/depositTargetSchemas.ts), [companySearchSchema.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/status/payment/components/companySearchSchema.ts), [DepositDeductionDialog.rules.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/status/payment/components/DepositDeductionDialog.rules.ts). 프런트 검증과 서버 DTO 제약이 다르면 서버 검증이 최종 기준이다.

화면 필드 키와 API 필드명이 다른 경우 변환은 Hook/API의 검색·저장 매핑에서 수행된다. 요청·응답 필드와 DB 컬럼 매핑은 아래 API 계약 및 DB 객체 계약에 연결했다.

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
|---|---|---|---|
| 벌크식계좌 입금 상세 조회 | [GET /api/v1/service-status/deposits/bulk-account/{id}](../../references/api-contracts.md#api101); `/payment/bulk-account-deposit` / `VIEW` | `경로·쿼리·본문 계약 참조` → `companyInfo, depositInfo, processHistory, companyName, businessNumber, comNo, depositDate, depositAmount, bank, accountNumber, availableAmount, status, deduction, id, businessNumbe` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 사업자번호 → 회사 조회 | [GET /api/v1/service-status/deposits/bulk-account/company-by-regno](../../references/api-contracts.md#api099); `/payment/bulk-account-deposit` / `VIEW` | `경로·쿼리·본문 계약 참조` → `comNo, companyName` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 청구 대상 업체 검색 | [GET /api/v1/service-status/deposits/bulk-account/companies/search](../../references/api-contracts.md#api098); `/payment/bulk-account-deposit` / `VIEW` | `searchMode, searchText, page, pageSize` → `content, totalElements` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 벌크식계좌 입금 처리 | [POST /api/v1/service-status/deposits/bulk-account/{id}/process](../../references/api-contracts.md#api226); `/payment/bulk-account-deposit` / `PROCESS` | `chargeMonth, amount, state, remark, customApplyDate, comNo` → `응답 DTO·파일/처리 결과 계약 참조` | 쓰기 대상 sb_bill.dbo.invoice, sb_bill.dbo.payment, sb_bill.dbo.payment_his, smartbill3.dbo.account_bulk_app_his_new, smartbill3.dbo.company, smartbill3.dbo.company_history, smartbill3.dbo.service_prepay, smartbill3.dbo.service_prepay_his |
| 단발성 청구월 목록 조회(벌크) | [GET /api/v1/status/payment/os-iv-deposit/bulk/charge-months](../../references/api-contracts.md#api137); `/payment/bulk-account-deposit` / `VIEW` | `경로·쿼리·본문 계약 참조` → `months` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 청구월별 단발성 청구 목록 조회(벌크) | [GET /api/v1/status/payment/os-iv-deposit/bulk/charges-by-month](../../references/api-contracts.md#api138); `/payment/bulk-account-deposit` / `VIEW` | `경로·쿼리·본문 계약 참조` → `content, totalElements` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 단발성 벌크 입금 처리 | [POST /api/v1/status/payment/os-iv-deposit/bulk/{idx}/process](../../references/api-contracts.md#api238); `/payment/bulk-account-deposit` / `PROCESS` | `crCd, serviceCd, seq, comNo, depositName, amount, icDt, remark` → `osIvPaymentIdx, crmNotified, crmMessage` | 쓰기 대상 sb_bill.dbo.headoffice_deposit_his, sb_bill_linked.dbo.crm_api_log, sb_bill_linked.dbo.crm_t_cr_os_iv, smartbill3.dbo.account_bulk_app_his_new, smartwork.dbo.os_iv_payment |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
|---|---|---|---|
| [smartwork.dbo.deposit_deduction](../../references/database-contracts.md#db270) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: smartwork.dbo.deposit_deduction | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [OFFICE.dbo.SAWON](../../references/database-contracts.md#db009) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: office.dbo.sawon | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SMARTBILL3.dbo.COMPANY](../../references/database-contracts.md#db197) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.company | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.UspBill_HeadOfficeDepositCompanySearch_SELECT](../../references/database-contracts.md#db305) | `@SEARCH_TEXT varchar(100) IN, @DEPOSIT_AMOUNT money IN, @SEARCH_MODE varchar(10) IN, @PAGE int IN, @PAGESIZE int IN` | 확정한 테이블 쓰기 없음. 참조: sb_bill.dbo.invoice, sb_bill.dbo.payment, sb_bill_linked.dbo.crm_t_cr_os_iv, smartbill3.dbo.company | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.headoffice_deposit_register](../../references/database-contracts.md#db272) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: smartwork.dbo.headoffice_deposit_register | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.UspBill_BulkAccountDepositProcessInfo_INSERT](../../references/database-contracts.md#db301) | `@IDX int IN, @COM_NO int IN, @CHARGE_MONTH varchar(10) IN, @AMOUNT int IN, @STATE varchar(10) IN, @REMARK varchar(200) IN, @SW_NO int IN, @CUSTOM_APPLY_DATE datetime IN, @RESULT varchar(1) OUT` | 쓰기: sb_bill.dbo.invoice, sb_bill.dbo.payment, sb_bill.dbo.payment_his, smartbill3.dbo.account_bulk_app_his_new, smartbill3.dbo.company, smartbill3.dbo.company_history, smartbill3.dbo.service_prepay, smartbill3.dbo.service_prepay_his. 참조: sb_bill.dbo.invoice, sb_bill.dbo.payment, sb_bill.dbo.payment_his, smartbill3.dbo.account_bulk_app, smartbill3.dbo.account_bulk_app_his_new, smartbill3.dbo.company, smartbill3.dbo.company_history, smartbill3.dbo.member 외 3개 | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.UspBill_BulkAccountDepositHistoryInfo](../../references/database-contracts.md#db299) | `@IDX int IN` | 확정한 테이블 쓰기 없음. 참조: office.dbo.sawon, sb_bill_linked.dbo.crm_t_cr_os_iv, smartbill3.dbo.account_bulk_app_his_new, smartbill3.dbo.company, smartwork.dbo.os_iv_payment | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Sb_Bill.dbo.UspBill_BulkAccountDepositAmountInfo_SELECT](../../references/database-contracts.md#db074) | `@IDX int IN` | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.account_bulk_app, smartbill3.dbo.account_bulk_app_his_new | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [OFFICE.dbo.upApp_Account_Payment_View](../../references/database-contracts.md#db010) | `@IDX int IN` | 확정한 테이블 쓰기 없음. 참조: office.dbo.sawon, smartbill3.dbo.account_bulk, smartbill3.dbo.account_bulk_app, smartbill3.dbo.common_code, smartbill3.dbo.company | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_BILL_LINKED.dbo.CRM_T_CR_OS_IV](../../references/database-contracts.md#db093) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: sb_bill_linked.dbo.crm_t_cr_os_iv | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.OS_IV_PAYMENT](../../references/database-contracts.md#db273) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 쓰기: smartwork.dbo.os_iv_payment. 참조: smartwork.dbo.os_iv_payment | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_BILL_LINKED.dbo.CRM_API_LOG](../../references/database-contracts.md#db092) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 쓰기: sb_bill_linked.dbo.crm_api_log. 참조: sb_bill_linked.dbo.crm_api_log | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.UspBill_OsIvHeadOfficeProcess_INSERT](../../references/database-contracts.md#db307) | `@DEPOSIT_IDX int IN, @CR_CD varchar(20) IN, @SERVICE_CD varchar(20) IN, @SEQ smallint IN, @COM_NO int IN, @DEPOSIT_NAME varchar(30) IN, @AMOUNT money IN, @IC_DT varchar(8) IN, @SW_NO int IN, @REMARK varchar(200) IN, @RESULT varchar(1) OUT, @OS_IV_PAYMENT_IDX bigint OUT` | 쓰기: sb_bill.dbo.headoffice_deposit_his, sb_bill_linked.dbo.crm_t_cr_os_iv, smartwork.dbo.os_iv_payment. 참조: sb_bill.dbo.headoffice_deposit, sb_bill.dbo.headoffice_deposit_his, sb_bill_linked.dbo.crm_t_cr_os_iv, smartwork.dbo.deposit_deduction, smartwork.dbo.os_iv_payment | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.UspBill_OsIvBulkProcess_INSERT](../../references/database-contracts.md#db306) | `@DEPOSIT_IDX int IN, @CR_CD varchar(20) IN, @SERVICE_CD varchar(20) IN, @SEQ smallint IN, @COM_NO int IN, @DEPOSIT_NAME varchar(30) IN, @AMOUNT money IN, @IC_DT varchar(8) IN, @SW_NO int IN, @REMARK varchar(200) IN, @RESULT varchar(1) OUT, @OS_IV_PAYMENT_IDX bigint OUT` | 쓰기: sb_bill_linked.dbo.crm_t_cr_os_iv, smartbill3.dbo.account_bulk_app_his_new, smartwork.dbo.os_iv_payment. 참조: sb_bill_linked.dbo.crm_t_cr_os_iv, smartbill3.dbo.account_bulk_app, smartbill3.dbo.account_bulk_app_his_new, smartwork.dbo.deposit_deduction, smartwork.dbo.os_iv_payment | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |

위 DB 계약 링크에는 실제 파라미터 타입·기본값·IN/OUT, Mapper 결과 컬럼, RETURN 바인딩, 참조 테이블·하위 프로시저·정의 필터/정렬을 기록했다. DTO·Service·Repository·Mapper의 상세 호출 경로는 각 API 계약에서 확인한다.

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
|---|---|---|
| 처리 내역이 없습니다. | [문구·처리 코드](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/BulkAccountDepositManagementDetailPage.tsx#L276); 현재 조건·대상·권한 확인 | 검색·조회 오류면 조건을 확인 후 재조회. 변경·발송 결과가 불명확하면 처리 여부와 이력을 확인한 뒤 재시도 여부를 판단한다. |
| 추가된 업체가 없습니다. | [문구·처리 코드](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/BulkAccountDepositProcessingDialog.tsx#L743); 현재 조건·대상·권한 확인 | 검색·조회 오류면 조건을 확인 후 재조회. 변경·발송 결과가 불명확하면 처리 여부와 이력을 확인한 뒤 재시도 여부를 판단한다. |
| 결과가 없거나 기대 건수와 다름 | 적용된 검색 기준·기간·탭·대상 상태·서버 필터·페이징·목록/다운로드 조건 | 조건을 다시 확인하고 조회한다. 지속되면 경로·작업 시각·마스킹한 식별자·필터를 업무/기술 담당에게 전달한다. |
| 메뉴·버튼 미표시 또는 접근 거부 | 사용자 그룹의 메뉴 접근·VIEW 및 API별 PROCESS/EXECUTE/DELETE/EXCEL_DOWNLOAD/UNMASK 등 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. 프런트 버튼 표시만으로 서버 권한을 판단하지 않는다. |
| 저장·삭제·외부 실행의 결과가 불명확 | 대상 현재 상태·중복 요청·감사 이력·API 오류·파일/외부 소비 로그 | 기존 반영 여부를 먼저 조회한다. 중복 발송·초기화·금액 처리를 피하기 위해 기술 담당 확인 후 재시도한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
|---|---|---|
| 대상 선정 | 사용자가 WBS 탭 내용으로 제공한 텍스트의 No. 187, 188, 189; [선정 태스크](../../inventory/wbs-tasks.csv) | 제공 텍스트 확인 2026-11-09. 원본 Excel의 탭/병합 셀을 독립 재열람한 것은 아님. |
| 메뉴·라우트·화면 | [menuConfig.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts); [PaymentRoutes.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/PaymentRoutes.tsx); [BulkAccountDepositManagementDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/BulkAccountDepositManagementDetailPage.tsx) | 코드 확인 2026-11-09, 기준 dc216b313 |
| 기능·권한·API | 이 문서의 API 계약 링크 및 연결 Hook/API·Controller·DTO·Service·Repository·Mapper | 코드 확인 2026-11-09. 요청 실행·권한 계정별 재현은 미확인. |
| DB 정의 | [개발 DB 계약](../../references/database-contracts.md), 이 문서의 연결 객체 | 개발 DB 정의 확인 2026-11-09. 동적 SQL·CLR 내부·정의 미공개 참조의 미확정 범위는 객체별 기록; 후속 확인 DB 담당. |
| 브라우저 화면·배포 환경 | 실제 검증 계정의 정상·빈 결과·권한 부족·입력 오류 및 현재 배포본 | 미확인: 브라우저 실행 검증을 수행하지 않음. 배포 전 업무 담당·QA·기술 담당 확인. |
| 업무 프로시저·쓰기·외부 결과 | 격리된 검증 환경·테스트 데이터의 실행 결과 | 미확인: 공유 개발 DB의 업무 프로시저·쓰기·발송을 실행하지 않음. 격리 환경에서 기술 담당 확인. |

코드 확인과 DB 정의 확인은 실행 성공·업무 승인·다른 환경 적용을 보장하지 않는다. 업무·기술 담당 검토 후 조사 목록의 상태를 완료로 변경한다.

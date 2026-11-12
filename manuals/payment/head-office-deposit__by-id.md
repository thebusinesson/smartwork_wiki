# [입금·예치금·배분·취소·환불] 본사 입금 관리 상세 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

본사 입금 상세를 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 입금·예치금·배분·취소·환불 |
| 언제 사용하는가 | 본사 입금 상세 조회, 업체 검색, 단발성 청구월 목록 조회, 청구월별 단발성 청구 목록 조회, 본사 입금 처리 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 회사명, 사업자번호, 청구구분, 청구월, 청구금액, 처리금액 |
| 업무 흐름 | 본사 입금 상세 조회, 업체 검색, 단발성 청구월 목록 조회, 청구월별 단발성 청구 목록 조회, 본사 입금 처리 |
| 이 페이지의 역할 | 상세 · 본사 입금 상세 조회 |
| 판단 결과·다음 업무 | [본사 입금 관리](head-office-deposit.md) |
| 다른 화면과의 구분 | 서비스 현황 > 입금관리 > 본사 입금 관리에서 사용하는 상세 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 확인 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/DepositDeductionDialog.tsx#L96) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 본사 입금 상세를 조회한다. |
| 메뉴·화면 경로 | 서비스 현황 > 입금관리 > 본사 입금 관리 · `/payment/head-office-deposit/:id` · 경로 변수 `id` |
| 화면 유형·담당 | 상세 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [본사 입금 관리](head-office-deposit.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/payment/head-office-deposit` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `id` |
| 본사 입금 상세 조회 | `/payment/head-office-deposit` `VIEW` | `idx: Long` |
| 업체 검색 | `/payment/head-office-deposit` `VIEW` | `HeadOfficeDepositCompanySearchRequest` `depositAmount`, `searchMode`, `searchText`, `registerItemId`, `page`, `pageSize` |
| 단발성 청구월 목록 조회 | `/payment/head-office-deposit` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 청구월별 단발성 청구 목록 조회 | `/payment/head-office-deposit` `VIEW` | `chargeMonth: String` · `page: Int` · `pageSize: Int` |
| 본사 입금 처리 | `/payment/head-office-deposit` `PROCESS` | `idx: Long` · `HeadOfficeDepositProcessRequest` `comNo`, `chargeMonth`, `amount`, `state`, `remark` |
| 본사 입금 삭제 | `/payment/head-office-deposit` `DELETE` | `HeadOfficeDepositDeleteRequest` `idxList`, `reason` · 서버 필수 `idxList`, `reason` |
| 단발성 본사 입금 처리 | `/payment/head-office-deposit` `PROCESS` | `idx: Long` · `OsIvProcessRequest` `crCd`, `serviceCd`, `seq`, `comNo`, `depositName`, `amount`, `icDt`, `remark` · 서버 필수 `crCd`, `serviceCd`, `icDt` |
| 본사 입금 업체 등록 | `/payment/head-office-deposit` `PROCESS` | `idx: Long` · `HeadOfficeDepositRegisterCompanyRequest` `comNo`, `comRegno`, `chargeMonth`, `depositAmount`, `billingAmount`, `status`, `processAmount` |

코드에서 확인한 버튼·작업명은 **차감 취소**, **차감**, **확인**, **입금처리**, **예치금처리**, **삭제**, **목록**, **검색**, **추가**, **취소**, **입금 처리**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [본사 입금 관리](head-office-deposit.md)에서 대상 또는 작업을 선택한다. `/payment/head-office-deposit/:id`에서 이전 화면이 전달한 `id`와 현재 대상을 확인한다.
2. **단발성** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **확인**, **검색** 중 해당 버튼을 선택한다.
3. **본사 입금 상세 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [본사 입금 관리](head-office-deposit.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `id` |
| 회사명 | 출력 | 조회 응답 기준 | 화면 필드 `companyName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositManagementDetailPage.tsx#L94) |
| 사업자번호 | 출력 | 조회 응답 기준 | 화면 필드 `businessNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositManagementDetailPage.tsx#L104) |
| 청구구분 | 출력 | 조회 응답 기준 | 화면 필드 `chargeGubun` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositManagementDetailPage.tsx#L114) |
| 청구월 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | API 요청 `chargeMonth` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositManagementDetailPage.tsx#L138) |
| 청구금액 | 출력 | 조회 응답 기준 | 화면 필드 `chargeAmount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositManagementDetailPage.tsx#L149) |
| 처리금액 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | API 요청 `amount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositManagementDetailPage.tsx#L158) |
| 처리상태 | 출력 | 조회 응답 기준 | 화면 필드 `division` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositManagementDetailPage.tsx#L165) |
| 처리일자 | 출력 | 조회 응답 기준 | 화면 필드 `processedAt` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositManagementDetailPage.tsx#L186) |
| 처리자 | 출력 | 조회 응답 기준 | 화면 필드 `processedBy` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositManagementDetailPage.tsx#L192) |
| 입금자명 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositManagementDetailPage.tsx#L221) |
| 입금일 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositManagementDetailPage.tsx#L223) |
| 입금액 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositManagementDetailPage.tsx#L227) |
| 차감금액 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/DepositDeductionDialog.tsx#L109) |
| 사유 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/DepositDeductionDialog.tsx#L123) |
| 차감 사유를 입력하세요 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/DepositDeductionDialog.tsx#L129) |
| 잔액 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositManagementDetailPage.tsx#L253) |
| 선택 | 출력 | 조회 응답 기준 | API 응답 `comNo` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/HeadOfficeDepositProcessingDialog.tsx#L452) |
| 입금처리금액 | 출력 | 조회 응답 기준 | 화면 필드 `processAmountInput` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/HeadOfficeDepositProcessingDialog.tsx#L504) |
| 청구 구분 | 출력 | 조회 응답 기준 | 화면 필드 `gubun` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/HeadOfficeDepositProcessingDialog.tsx#L551) |
| 단발성 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/HeadOfficeDepositProcessingDialog.tsx#L692) |
| 청구월 선택 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/HeadOfficeDepositProcessingDialog.tsx#L705) |
| 사업자 번호 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/HeadOfficePrepaidProcessingDialog.tsx#L118) |
| 처리가능 금액 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/HeadOfficePrepaidProcessingDialog.tsx#L127) |
| 예치금 처리 금액 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/HeadOfficePrepaidProcessingDialog.tsx#L129) |
| 비 고 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/HeadOfficePrepaidProcessingDialog.tsx#L146) |
| 비고를 입력하세요 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/HeadOfficePrepaidProcessingDialog.tsx#L151) |
| 삭제 사유 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/HeadOfficeDepositDeleteDialog.tsx#L88) |
| 삭제 사유를 입력하세요 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/HeadOfficeDepositDeleteDialog.tsx#L94) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 본사 입금 상세 조회 | `GET /api/v1/status/payment/head-office-deposit/{idx}` · `/payment/head-office-deposit` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/headofficedeposit/HeadOfficeDepositController.kt#L146) | `idx: Long` → `success`, `data`, `error`, `comNo`, `comName`, `comRegno`, `depositorName`, `depositDate`, `chargeDate`, `depositAmount`, `processedAmount`, `balanceAmount` | `smartwork.dbo.UspBill_HeadOfficeDepositDetailInfo_SELECT`, `smartwork.dbo.UspBill_HeadOfficeDepositHistoryInfo_SELECT`, `smartwork.dbo.deposit_deduction`, `office.dbo.SAWON` · 코드 연계 트랜잭션 |
| 업체 검색 | `GET /api/v1/status/payment/head-office-deposit/companies/search` · `/payment/head-office-deposit` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/headofficedeposit/HeadOfficeDepositController.kt#L209) | `HeadOfficeDepositCompanySearchRequest` `depositAmount`, `searchMode`, `searchText`, `registerItemId`, `page`, `pageSize` → `success`, `data`, `error`, `content`, `totalElements` | `smartwork.dbo.headoffice_deposit_register`, `smartwork.dbo.UspBill_HeadOfficeDepositCompanySearch_SELECT` |
| 단발성 청구월 목록 조회 | `GET /api/v1/status/payment/os-iv-deposit/charge-months` · `/payment/head-office-deposit` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/osivdeposit/OsIvDepositController.kt#L148) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `months` | `SB_BILL_LINKED.dbo.CRM_T_CR_OS_IV` |
| 청구월별 단발성 청구 목록 조회 | `GET /api/v1/status/payment/os-iv-deposit/charges-by-month` · `/payment/head-office-deposit` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/osivdeposit/OsIvDepositController.kt#L164) | `chargeMonth: String` · `page: Int` · `pageSize: Int` → `success`, `data`, `error`, `content`, `totalElements` | `SB_BILL_LINKED.dbo.CRM_T_CR_OS_IV`, `SmartBill3.dbo.COMPANY` |
| 본사 입금 처리 | `POST /api/v1/status/payment/head-office-deposit/{idx}/process` · `/payment/head-office-deposit` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/headofficedeposit/HeadOfficeDepositController.kt#L242) | `idx: Long` · `HeadOfficeDepositProcessRequest` `comNo`, `chargeMonth`, `amount`, `state`, `remark` → `success`, `data`, `error` | `smartwork.dbo.UspBill_HeadOfficeDepositProcessInfo_INSERT` · 정의에서 확인한 쓰기 `SB_BILL.dbo.HEADOFFICE_DEPOSIT_HIS`, `SB_BILL.dbo.PAYMENT`, `SB_BILL.dbo.PAYMENT_HIS`, `SB_BILL.dbo.INVOICE` 외 4개 · 코드 연계 트랜잭션 |
| 본사 입금 삭제 | `DELETE /api/v1/status/payment/head-office-deposit` · `/payment/head-office-deposit` `DELETE` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/headofficedeposit/HeadOfficeDepositController.kt#L259) | `HeadOfficeDepositDeleteRequest` `idxList`, `reason` · 서버 필수 `idxList`, `reason` → `success`, `data`, `error` | `SB_BILL.dbo.UspBill_PaymentBalanceDepositProcessInfo_DELETE`, `smartwork.dbo.deposit_deduction`, `smartwork.dbo.action_reason` · 정의에서 확인한 쓰기 `smartwork.dbo.deposit_deduction`, `smartwork.dbo.action_reason` · 코드 연계 트랜잭션 |
| 단발성 본사 입금 처리 | `POST /api/v1/status/payment/os-iv-deposit/head-office/{idx}/process` · `/payment/head-office-deposit` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/osivdeposit/OsIvDepositController.kt#L216) | `idx: Long` · `OsIvProcessRequest` `crCd`, `serviceCd`, `seq`, `comNo`, `depositName`, `amount`, `icDt`, `remark` · 서버 필수 `crCd`, `serviceCd`, `icDt` → `success`, `data`, `error`, `osIvPaymentIdx`, `crmNotified`, `crmMessage` | `smartwork.dbo.UspBill_OsIvBulkProcess_INSERT`, `smartwork.dbo.UspBill_OsIvHeadOfficeProcess_INSERT`, `SB_BILL_LINKED.dbo.CRM_API_LOG`, `smartwork.dbo.OS_IV_PAYMENT` · 정의에서 확인한 쓰기 `SmartBill3.dbo.ACCOUNT_BULK_APP_HIS_NEW`, `SB_BILL_LINKED.dbo.CRM_T_CR_OS_IV`, `smartwork.dbo.OS_IV_PAYMENT`, `SB_BILL.dbo.HEADOFFICE_DEPOSIT_HIS` 외 1개 · 코드 연계 CrmOsIvApiClient, 트랜잭션 |
| 본사 입금 업체 등록 | `POST /api/v1/status/payment/head-office-deposit/{idx}/register-company` · `/payment/head-office-deposit` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/headofficedeposit/HeadOfficeDepositController.kt#L225) | `idx: Long` · `HeadOfficeDepositRegisterCompanyRequest` `comNo`, `comRegno`, `chargeMonth`, `depositAmount`, `billingAmount`, `status`, `processAmount` → `success`, `data`, `error` | `SB_BILL.dbo.HEADOFFICE_DEPOSIT`, `smartwork.dbo.UspBill_HeadOfficeDepositProcessInfo_INSERT` · 정의에서 확인한 쓰기 `SB_BILL.dbo.HEADOFFICE_DEPOSIT`, `SB_BILL.dbo.HEADOFFICE_DEPOSIT_HIS`, `SB_BILL.dbo.PAYMENT`, `SB_BILL.dbo.PAYMENT_HIS` 외 5개 · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.UspBill_HeadOfficeDepositDetailInfo_SELECT` | @IDX bigint | 정의 참조 `SmartBill3.dbo.COMPANY`, `SB_BILL_LINKED.dbo.CRM_T_CR_OS_IV`, `smartwork.dbo.deposit_deduction`, `SB_BILL.dbo.HEADOFFICE_DEPOSIT`, `SB_BILL.dbo.HEADOFFICE_DEPOSIT_HIS` 외 1개 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/headofficedeposit/repository/HeadOfficeDepositMapper.kt#L70) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-eaad9580b68411ee) |
| `smartwork.dbo.UspBill_HeadOfficeDepositHistoryInfo_SELECT` | @IDX bigint | 정의 참조 `SmartBill3.dbo.COMPANY`, `SB_BILL_LINKED.dbo.CRM_T_CR_OS_IV`, `SB_BILL.dbo.HEADOFFICE_DEPOSIT`, `SB_BILL.dbo.HEADOFFICE_DEPOSIT_HIS`, `SB_BILL.dbo.INVOICE` 외 2개 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/headofficedeposit/repository/HeadOfficeDepositMapper.kt#L90) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3c9421f683bba8eb) |
| `smartwork.dbo.deposit_deduction` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/depositdeduction/repository/DepositDeductionMapper.kt#L40) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-cc106276f1e9c83e) |
| `office.dbo.SAWON` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/depositdeduction/repository/DepositDeductionMapper.kt#L40) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3a9ea6e368df5cb3) |
| `smartwork.dbo.headoffice_deposit_register` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/headofficedeposit/repository/HeadOfficeDepositMapper.kt#L156) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-748cfdfef3387e76) |
| `smartwork.dbo.UspBill_HeadOfficeDepositCompanySearch_SELECT` | @SEARCH_TEXT varchar(100), @DEPOSIT_AMOUNT money, @SEARCH_MODE varchar(10), @PAGE int = 1, @PAGESIZE int = 20 | 정의 참조 `smartwork.dbo.cd`, `SmartBill3.dbo.COMPANY`, `SB_BILL_LINKED.dbo.CRM_T_CR_OS_IV`, `SB_BILL.dbo.INVOICE`, `SB_BILL.dbo.PAYMENT` · 쓰기 구문 존재 · 대상 별칭 또는 하위 정의 확인 · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/headofficedeposit/repository/HeadOfficeDepositMapper.kt#L152) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-faef42b6d524fb65) |
| `SB_BILL_LINKED.dbo.CRM_T_CR_OS_IV` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/osivdeposit/repository/OsIvDepositMapper.kt#L145) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-d49e19cdab81cd25) |
| `SmartBill3.dbo.COMPANY` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/osivdeposit/repository/OsIvDepositMapper.kt#L181) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-0e6fcaa6b5086c07) |
| `smartwork.dbo.UspBill_HeadOfficeDepositProcessInfo_INSERT` | @IDX int, @COM_NO int, @CHARGE_MONTH varchar(10), @AMOUNT int, @STATE varchar(10), @REMARK varchar(200), @SW_NO int, @RESULT varchar(1) OUT | 정의 참조 `SmartBill3.dbo.COMPANY`, `SmartBill3.dbo.COMPANY_HISTORY`, `smartwork.dbo.deposit_deduction`, `SB_BILL.dbo.HEADOFFICE_DEPOSIT`, `SB_BILL.dbo.HEADOFFICE_DEPOSIT_HIS` 외 6개 · 정적 쓰기 `SB_BILL.dbo.HEADOFFICE_DEPOSIT_HIS`, `SB_BILL.dbo.PAYMENT`, `SB_BILL.dbo.PAYMENT_HIS`, `SB_BILL.dbo.INVOICE` 외 4개 · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/headofficedeposit/repository/HeadOfficeDepositMapper.kt#L118) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-7969da77e22bdd34) |
| `SB_BILL.dbo.UspBill_PaymentBalanceDepositProcessInfo_DELETE` | @IDXS varchar(max), @RESULT varchar(5) OUT | 동적 SQL 포함 · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/headofficedeposit/repository/HeadOfficeDepositMapper.kt#L126) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-2103318b4929b1e6) |
| `smartwork.dbo.action_reason` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL INSERT INTO | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/shared/actionreason/repository/ActionReasonMapper.kt#L16) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b0430106ffe0743f) |
| `smartwork.dbo.UspBill_OsIvBulkProcess_INSERT` | @DEPOSIT_IDX int, @CR_CD varchar(20), @SERVICE_CD varchar(20), @SEQ smallint, @COM_NO int, @DEPOSIT_NAME varchar(30), @AMOUNT money, @IC_DT varchar(8), @SW_NO int, @REMARK varchar(200), @RESULT varchar(1) OUT, @OS_IV_PAYMENT_IDX bigint OUT | 정의 참조 `SmartBill3.dbo.ACCOUNT_BULK_APP`, `SmartBill3.dbo.ACCOUNT_BULK_APP_HIS_NEW`, `SB_BILL_LINKED.dbo.CRM_T_CR_OS_IV`, `smartwork.dbo.deposit_deduction`, `smartwork.dbo.OS_IV_PAYMENT` · 정적 쓰기 `SmartBill3.dbo.ACCOUNT_BULK_APP_HIS_NEW`, `SB_BILL_LINKED.dbo.CRM_T_CR_OS_IV`, `smartwork.dbo.OS_IV_PAYMENT` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/osivdeposit/repository/OsIvDepositMapper.kt#L53) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-7a115df60c14b17d) |
| `smartwork.dbo.UspBill_OsIvHeadOfficeProcess_INSERT` | @DEPOSIT_IDX int, @CR_CD varchar(20), @SERVICE_CD varchar(20), @SEQ smallint, @COM_NO int, @DEPOSIT_NAME varchar(30), @AMOUNT money, @IC_DT varchar(8), @SW_NO int, @REMARK varchar(200), @RESULT varchar(1) OUT, @OS_IV_PAYMENT_IDX bigint OUT | 정의 참조 `SB_BILL_LINKED.dbo.CRM_T_CR_OS_IV`, `smartwork.dbo.deposit_deduction`, `SB_BILL.dbo.HEADOFFICE_DEPOSIT`, `SB_BILL.dbo.HEADOFFICE_DEPOSIT_HIS`, `smartwork.dbo.OS_IV_PAYMENT` · 정적 쓰기 `SB_BILL.dbo.HEADOFFICE_DEPOSIT_HIS`, `SB_BILL_LINKED.dbo.CRM_T_CR_OS_IV`, `smartwork.dbo.OS_IV_PAYMENT` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/osivdeposit/repository/OsIvDepositMapper.kt#L39) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-e05a1ee89fcda2c0) |
| `SB_BILL_LINKED.dbo.CRM_API_LOG` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL INSERT INTO | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/osivdeposit/repository/CrmApiLogMapper.kt#L25) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-49c412a8654ee2db) |
| `smartwork.dbo.OS_IV_PAYMENT` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL UPDATE | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/osivdeposit/repository/OsIvDepositMapper.kt#L59) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-11a2c0b6456c84a6) |
| `SB_BILL.dbo.HEADOFFICE_DEPOSIT` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL UPDATE | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/headofficedeposit/repository/HeadOfficeDepositMapper.kt#L132) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-729ca08029e7d734) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 회사명, 사업자번호, 청구구분, 청구월, 청구금액, 처리금액 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 서비스 현황 > 입금관리 > 본사 입금 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 삭제 중 오류가 발생했습니다. | 회사명, 사업자번호, 청구구분, 청구월, 청구금액, 처리금액 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 차감 취소 중 오류가 발생했습니다. | 회사명, 사업자번호, 청구구분, 청구월, 청구금액, 처리금액 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 업체 검색 중 오류가 발생했습니다. | 회사명, 사업자번호, 청구구분, 청구월, 청구금액, 처리금액 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 청구월 목록 조회 중 오류가 발생했습니다. | 회사명, 사업자번호, 청구구분, 청구월, 청구금액, 처리금액 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/PaymentRoutes.tsx#L66) · [HeadOfficeDepositManagementDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositManagementDetailPage.tsx#L35) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/headOfficeDepositManagementApi.ts#L71) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/headOfficeDepositRegistrationApi.ts#L145) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/osIvDepositApi.ts#L32) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/osIvDepositApi.ts#L45) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/headOfficeDepositManagementApi.ts#L96) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/headOfficeDepositManagementApi.ts#L106) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/osIvDepositApi.ts#L80) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/headOfficeDepositRegistrationApi.ts#L159) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 16개 중 개발 메타데이터 확인 16개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-ec80c6fa419fbbc0) | Demo 메타데이터 14/16개 확인 · 미확인 2개 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

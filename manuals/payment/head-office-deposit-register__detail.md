# [입금·예치금·배분·취소·환불] 본사 입금 등록 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

등록 상세 목록을 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 입금·예치금·배분·취소·환불 |
| 언제 사용하는가 | 등록 상세 목록 조회, 업체 검색, 단발성 청구월 목록 조회, 청구월별 단발성 청구 목록 조회, 등록 상세 목록 다운로드 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 업로드 일자, 파일명, 총 건수, 업체확인, 미확인, 입금 등록 |
| 업무 흐름 | 등록 상세 목록 조회, 업체 검색, 단발성 청구월 목록 조회, 청구월별 단발성 청구 목록 조회, 등록 상세 목록 다운로드 |
| 이 페이지의 역할 | 상세 · 등록 상세 목록 조회 |
| 판단 결과·다음 업무 | [본사 입금 등록](head-office-deposit-register.md) |
| 다른 화면과의 구분 | 서비스 현황 > 입금관리 > 본사 입금 등록에서 사용하는 상세 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 확인 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositRegistrationDetailPage.tsx#L857) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 등록 상세 목록을 조회한다. |
| 메뉴·화면 경로 | 서비스 현황 > 입금관리 > 본사 입금 등록 · `/payment/head-office-deposit-register/detail` |
| 화면 유형·담당 | 상세 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [본사 입금 등록](head-office-deposit-register.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/payment/head-office-deposit-register` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 등록 상세 목록 조회 | `/payment/head-office-deposit-register` `VIEW` | `DepositRegistrationDetailSearchRequest` `fileId`, `matchingType`, `depositorName`, `page`, `size` |
| 업체 검색 | `/payment/head-office-deposit` `VIEW` | `HeadOfficeDepositCompanySearchRequest` `depositAmount`, `searchMode`, `searchText`, `registerItemId`, `page`, `pageSize` |
| 단발성 청구월 목록 조회 | `/payment/head-office-deposit` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 청구월별 단발성 청구 목록 조회 | `/payment/head-office-deposit` `VIEW` | `chargeMonth: String` · `page: Int` · `pageSize: Int` |
| 등록 상세 목록 다운로드 | `/payment/head-office-deposit-register` `EXCEL_DOWNLOAD` | `DepositRegistrationDetailSearchRequest` `fileId`, `matchingType`, `depositorName`, `page`, `size` |
| 입금 등록 | `/payment/head-office-deposit-register` `EXCEL_UPLOAD` | `DepositRegistrationRequest` `fileId` |
| 등록 항목 저장 | `/payment/head-office-deposit-register` `PROCESS` | `DepositRegistrationItemsSaveRequest` `fileId`, `items` |
| 등록 항목 삭제 | `/payment/head-office-deposit-register` `DELETE` | `DepositRegistrationItemsDeleteRequest` `itemIds`, `reason` |
| 등록 상세 입금자명 원문 조회 | `/payment/head-office-deposit-register` / `UNMASK` | `itemId`, `field` |

코드에서 확인한 버튼·작업명은 **다운로드**, **입금 등록**, **검색**, **저장**, **삭제**, **목록**, **확인**, **차감 취소**, **차감**, **추가**, **취소**, **업체 등록**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [본사 입금 등록](head-office-deposit-register.md)에서 대상 또는 작업을 선택한다. `/payment/head-office-deposit-register/detail`를 연다.
2. **단발성** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **다운로드**, **입금 등록**, **검색**, **저장**, **확인** 중 해당 버튼을 선택한다.
3. **등록 상세 목록 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [본사 입금 등록](head-office-deposit-register.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 업로드 일자 | 출력 | 조회 응답 기준 | 화면 필드 `uploadDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositRegistrationDetailPage.tsx#L80) |
| 파일명 | 출력 | 조회 응답 기준 | 화면 필드 `fileName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositRegistrationDetailPage.tsx#L86) |
| 총 건수 | 출력 | 조회 응답 기준 | API 응답 `totalCount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositRegistrationDetailPage.tsx#L97) |
| 업체확인 | 출력 | 조회 응답 기준 | 화면 필드 `companyConfirmed` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositRegistrationDetailPage.tsx#L104) |
| 미확인 | 출력 | 조회 응답 기준 | 화면 필드 `unconfirmed` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositRegistrationDetailPage.tsx#L111) |
| 입금 등록 | 출력 | 조회 응답 기준 | 화면 필드 `depositRegistration` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositRegistrationDetailPage.tsx#L118) |
| 입금자명 검색 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositRegistrationDetailPage.tsx#L788) |
| 입금일 | 출력 | 조회 응답 기준 | 화면 필드 `depositDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositRegistrationDetailPage.tsx#L152) |
| 입금자명 | 입력 또는 선택 | API 기본값 null | API 요청 `depositorName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositRegistrationDetailPage.tsx#L159) |
| 입금액 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | API 요청 `depositAmount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositRegistrationDetailPage.tsx#L166) |
| 회사명 | 출력 | 조회 응답 기준 | 화면 필드 `processes.companyName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositRegistrationDetailPage.tsx#L173) |
| 사업자번호 | 출력 | 조회 응답 기준 | 화면 필드 `processes.businessNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositRegistrationDetailPage.tsx#L187) |
| 청구구분 | 출력 | 조회 응답 기준 | 화면 필드 `processes.chargeGubun` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositRegistrationDetailPage.tsx#L197) |
| 청구월 | 출력 | 조회 응답 기준 | 화면 필드 `processes.chargeMonth` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositRegistrationDetailPage.tsx#L224) |
| 청구금액 | 출력 | 조회 응답 기준 | 화면 필드 `processes.billingAmount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositRegistrationDetailPage.tsx#L235) |
| 처리금액 | 출력 | 조회 응답 기준 | 화면 필드 `processes.processAmount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositRegistrationDetailPage.tsx#L245) |
| 매칭 | 입력 또는 선택 | 초기 `'all'` · API 기본값 null | API 요청 `matchingType` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositRegistrationDetailPage.tsx#L255) |
| 처리상태 | 출력 | 조회 응답 기준 | 화면 필드 `processes.processStatus` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositRegistrationDetailPage.tsx#L262) |
| 선택 건수 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/HeadOfficeDepositRegistrationDeleteDialog.tsx#L84) |
| 삭제 사유 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/HeadOfficeDepositRegistrationDeleteDialog.tsx#L88) |
| 삭제 사유를 입력하세요 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/HeadOfficeDepositRegistrationDeleteDialog.tsx#L94) |
| 선택 | 출력 | 조회 응답 기준 | 화면 필드 `comNo` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/HeadOfficeDepositRegistrationDialog.tsx#L480) |
| 입금 처리 금액 | 출력 | 조회 응답 기준 | 화면 필드 `processAmountInput` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/HeadOfficeDepositRegistrationDialog.tsx#L545) |
| 청구 구분 | 출력 | 조회 응답 기준 | 화면 필드 `gubun` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/HeadOfficeDepositRegistrationDialog.tsx#L616) |
| 차감금액 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/DepositDeductionDialog.tsx#L109) |
| 사유 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/DepositDeductionDialog.tsx#L123) |
| 차감 사유를 입력하세요 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/DepositDeductionDialog.tsx#L129) |
| 단발성 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/HeadOfficeDepositRegistrationDialog.tsx#L778) |
| 청구월 선택 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/HeadOfficeDepositRegistrationDialog.tsx#L791) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 등록 상세 목록 조회 | `GET /api/v1/status/payment/head-office-deposit/registration/detail` · `/payment/head-office-deposit-register` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/headofficedeposit/HeadOfficeDepositRegistrationController.kt#L137) | `DepositRegistrationDetailSearchRequest` `fileId`, `matchingType`, `depositorName`, `page`, `size` → `success`, `data`, `error`, `fileSummary`, `content`, `totalElements` | `SB_BILL.dbo.HEADOFFICE_DEPOSIT`, `SB_BILL.dbo.HEADOFFICE_DEPOSIT_UPLOAD`, `smartwork.dbo.headoffice_deposit_register`, `smartwork.dbo.usp_bill_head_office_deposit_registration_detail_select`, `smartwork.dbo.deposit_deduction` 외 1개 |
| 업체 검색 | `GET /api/v1/status/payment/head-office-deposit/companies/search` · `/payment/head-office-deposit` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/headofficedeposit/HeadOfficeDepositController.kt#L209) | `HeadOfficeDepositCompanySearchRequest` `depositAmount`, `searchMode`, `searchText`, `registerItemId`, `page`, `pageSize` → `success`, `data`, `error`, `content`, `totalElements` | `smartwork.dbo.headoffice_deposit_register`, `smartwork.dbo.UspBill_HeadOfficeDepositCompanySearch_SELECT` |
| 단발성 청구월 목록 조회 | `GET /api/v1/status/payment/os-iv-deposit/charge-months` · `/payment/head-office-deposit` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/osivdeposit/OsIvDepositController.kt#L148) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `months` | `SB_BILL_LINKED.dbo.CRM_T_CR_OS_IV` |
| 청구월별 단발성 청구 목록 조회 | `GET /api/v1/status/payment/os-iv-deposit/charges-by-month` · `/payment/head-office-deposit` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/osivdeposit/OsIvDepositController.kt#L164) | `chargeMonth: String` · `page: Int` · `pageSize: Int` → `success`, `data`, `error`, `content`, `totalElements` | `SB_BILL_LINKED.dbo.CRM_T_CR_OS_IV`, `SmartBill3.dbo.COMPANY` |
| 등록 상세 목록 다운로드 | `GET /api/v1/status/payment/head-office-deposit/registration/detail/download` · `/payment/head-office-deposit-register` `EXCEL_DOWNLOAD` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/headofficedeposit/HeadOfficeDepositRegistrationController.kt#L293) | `DepositRegistrationDetailSearchRequest` `fileId`, `matchingType`, `depositorName`, `page`, `size` → 파일 또는 오류 응답 | `smartwork.dbo.usp_bill_head_office_deposit_registration_detail_select`, `smartwork.dbo.deposit_deduction`, `office.dbo.SAWON` |
| 입금 등록 | `POST /api/v1/status/payment/head-office-deposit/registration/register` · `/payment/head-office-deposit-register` `EXCEL_UPLOAD` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/headofficedeposit/HeadOfficeDepositRegistrationController.kt#L266) | `DepositRegistrationRequest` `fileId` → `success`, `data`, `error`, `totalCount`, `successCount`, `failureCount`, `failedItems` | `smartwork.dbo.headoffice_deposit_register`, `smartwork.dbo.headoffice_deposit_register_process`, `SB_BILL.dbo.HEADOFFICE_DEPOSIT`, `smartwork.dbo.deposit_deduction`, `smartwork.dbo.UspBill_OsIvBulkProcess_INSERT` 외 4개 · 정의에서 확인한 쓰기 `SB_BILL.dbo.HEADOFFICE_DEPOSIT`, `smartwork.dbo.deposit_deduction`, `SmartBill3.dbo.ACCOUNT_BULK_APP_HIS_NEW`, `SB_BILL_LINKED.dbo.CRM_T_CR_OS_IV` 외 10개 · 코드 연계 CrmOsIvApiClient, 트랜잭션 |
| 등록 항목 저장 | `PUT /api/v1/status/payment/head-office-deposit/registration/items` · `/payment/head-office-deposit-register` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/headofficedeposit/HeadOfficeDepositRegistrationController.kt#L183) | `DepositRegistrationItemsSaveRequest` `fileId`, `items` → `success`, `data`, `error` | `smartwork.dbo.headoffice_deposit_register`, `smartwork.dbo.headoffice_deposit_register_process`, `smartwork.dbo.deposit_deduction` · 정의에서 확인한 쓰기 `smartwork.dbo.headoffice_deposit_register`, `smartwork.dbo.headoffice_deposit_register_process` · 코드 연계 트랜잭션 |
| 등록 항목 삭제 | `DELETE /api/v1/status/payment/head-office-deposit/registration/items` · `/payment/head-office-deposit-register` `DELETE` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/headofficedeposit/HeadOfficeDepositRegistrationController.kt#L221) | `DepositRegistrationItemsDeleteRequest` `itemIds`, `reason` → `success`, `data`, `error` | `smartwork.dbo.headoffice_deposit_register`, `smartwork.dbo.deposit_deduction`, `smartwork.dbo.headoffice_deposit_register_process`, `smartwork.dbo.action_reason` · 정의에서 확인한 쓰기 `smartwork.dbo.deposit_deduction`, `smartwork.dbo.headoffice_deposit_register_process`, `smartwork.dbo.action_reason` · 코드 연계 트랜잭션 |
| 등록 상세 입금자명 원문 조회 | `POST /api/v1/status/payment/head-office-deposit/registration/items/{itemId}/sensitive-values/reveal` · `/payment/head-office-deposit-register` / `UNMASK` · [화면 컴포넌트](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositRegistrationDetailPage.tsx#L140) · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/headofficedeposit/HeadOfficeDepositRegistrationController.kt#L158) | `itemId`, `field` → 요청한 항목의 원문 응답 | 권한 검사 후 대상 값을 조회하고 감사 기록을 남긴다. |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `SB_BILL.dbo.HEADOFFICE_DEPOSIT` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/headofficedeposit/repository/HeadOfficeDepositRegistrationMapper.kt#L255) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-729ca08029e7d734) |
| `SB_BILL.dbo.HEADOFFICE_DEPOSIT_UPLOAD` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/headofficedeposit/repository/HeadOfficeDepositRegistrationMapper.kt#L255) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-c7e863ba93448043) |
| `smartwork.dbo.headoffice_deposit_register` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/headofficedeposit/repository/HeadOfficeDepositRegistrationMapper.kt#L255) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-748cfdfef3387e76) |
| `smartwork.dbo.usp_bill_head_office_deposit_registration_detail_select` | @file_id bigint, @matching_type varchar(10), @depositor_name varchar(30), @page int, @pagesize int | 정의 참조 `smartwork.dbo.deposit_deduction`, `SB_BILL.dbo.HEADOFFICE_DEPOSIT_HIS`, `smartwork.dbo.headoffice_deposit_register`, `smartwork.dbo.headoffice_deposit_register_process` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/headofficedeposit/repository/HeadOfficeDepositRegistrationMapper.kt#L288) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-bd264f923eb63c91) |
| `smartwork.dbo.deposit_deduction` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/depositdeduction/repository/DepositDeductionMapper.kt#L63) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-cc106276f1e9c83e) |
| `office.dbo.SAWON` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/depositdeduction/repository/DepositDeductionMapper.kt#L63) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3a9ea6e368df5cb3) |
| `smartwork.dbo.UspBill_HeadOfficeDepositCompanySearch_SELECT` | @SEARCH_TEXT varchar(100), @DEPOSIT_AMOUNT money, @SEARCH_MODE varchar(10), @PAGE int = 1, @PAGESIZE int = 20 | 정의 참조 `smartwork.dbo.cd`, `SmartBill3.dbo.COMPANY`, `SB_BILL_LINKED.dbo.CRM_T_CR_OS_IV`, `SB_BILL.dbo.INVOICE`, `SB_BILL.dbo.PAYMENT` · 쓰기 구문 존재 · 대상 별칭 또는 하위 정의 확인 · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/headofficedeposit/repository/HeadOfficeDepositMapper.kt#L152) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-faef42b6d524fb65) |
| `SB_BILL_LINKED.dbo.CRM_T_CR_OS_IV` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/osivdeposit/repository/OsIvDepositMapper.kt#L145) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-d49e19cdab81cd25) |
| `SmartBill3.dbo.COMPANY` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/osivdeposit/repository/OsIvDepositMapper.kt#L181) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-0e6fcaa6b5086c07) |
| `smartwork.dbo.headoffice_deposit_register_process` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/headofficedeposit/repository/HeadOfficeDepositRegistrationMapper.kt#L371) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-d5b2a63e22e82e4e) |
| `smartwork.dbo.UspBill_OsIvBulkProcess_INSERT` | @DEPOSIT_IDX int, @CR_CD varchar(20), @SERVICE_CD varchar(20), @SEQ smallint, @COM_NO int, @DEPOSIT_NAME varchar(30), @AMOUNT money, @IC_DT varchar(8), @SW_NO int, @REMARK varchar(200), @RESULT varchar(1) OUT, @OS_IV_PAYMENT_IDX bigint OUT | 정의 참조 `SmartBill3.dbo.ACCOUNT_BULK_APP`, `SmartBill3.dbo.ACCOUNT_BULK_APP_HIS_NEW`, `SB_BILL_LINKED.dbo.CRM_T_CR_OS_IV`, `smartwork.dbo.deposit_deduction`, `smartwork.dbo.OS_IV_PAYMENT` · 정적 쓰기 `SmartBill3.dbo.ACCOUNT_BULK_APP_HIS_NEW`, `SB_BILL_LINKED.dbo.CRM_T_CR_OS_IV`, `smartwork.dbo.OS_IV_PAYMENT` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/osivdeposit/repository/OsIvDepositMapper.kt#L53) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-7a115df60c14b17d) |
| `smartwork.dbo.UspBill_OsIvHeadOfficeProcess_INSERT` | @DEPOSIT_IDX int, @CR_CD varchar(20), @SERVICE_CD varchar(20), @SEQ smallint, @COM_NO int, @DEPOSIT_NAME varchar(30), @AMOUNT money, @IC_DT varchar(8), @SW_NO int, @REMARK varchar(200), @RESULT varchar(1) OUT, @OS_IV_PAYMENT_IDX bigint OUT | 정의 참조 `SB_BILL_LINKED.dbo.CRM_T_CR_OS_IV`, `smartwork.dbo.deposit_deduction`, `SB_BILL.dbo.HEADOFFICE_DEPOSIT`, `SB_BILL.dbo.HEADOFFICE_DEPOSIT_HIS`, `smartwork.dbo.OS_IV_PAYMENT` · 정적 쓰기 `SB_BILL.dbo.HEADOFFICE_DEPOSIT_HIS`, `SB_BILL_LINKED.dbo.CRM_T_CR_OS_IV`, `smartwork.dbo.OS_IV_PAYMENT` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/osivdeposit/repository/OsIvDepositMapper.kt#L39) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-e05a1ee89fcda2c0) |
| `SB_BILL_LINKED.dbo.CRM_API_LOG` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL INSERT INTO | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/osivdeposit/repository/CrmApiLogMapper.kt#L25) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-49c412a8654ee2db) |
| `smartwork.dbo.OS_IV_PAYMENT` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL UPDATE | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/osivdeposit/repository/OsIvDepositMapper.kt#L59) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-11a2c0b6456c84a6) |
| `smartwork.dbo.UspBill_HeadOfficeDepositProcessInfo_INSERT` | @IDX int, @COM_NO int, @CHARGE_MONTH varchar(10), @AMOUNT int, @STATE varchar(10), @REMARK varchar(200), @SW_NO int, @RESULT varchar(1) OUT | 정의 참조 `SmartBill3.dbo.COMPANY`, `SmartBill3.dbo.COMPANY_HISTORY`, `smartwork.dbo.deposit_deduction`, `SB_BILL.dbo.HEADOFFICE_DEPOSIT`, `SB_BILL.dbo.HEADOFFICE_DEPOSIT_HIS` 외 6개 · 정적 쓰기 `SB_BILL.dbo.HEADOFFICE_DEPOSIT_HIS`, `SB_BILL.dbo.PAYMENT`, `SB_BILL.dbo.PAYMENT_HIS`, `SB_BILL.dbo.INVOICE` 외 4개 · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/headofficedeposit/repository/HeadOfficeDepositMapper.kt#L118) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-7969da77e22bdd34) |
| `smartwork.dbo.action_reason` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL INSERT INTO | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/shared/actionreason/repository/ActionReasonMapper.kt#L16) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b0430106ffe0743f) |
| `smartwork.dbo.usp_sw_log_access_event_insert` | @EVENT_TYPE varchar(30) IN, @STATUS varchar(20) IN, @USER_ID bigint IN, @MEMBER_ID nvarchar(50) IN, @USER_NAME nvarchar(100) IN, @DEPARTMENT_NAME nvarchar(100) IN, @PAGE_TITLE nvarchar(200) IN, @PATH nvarchar(500) IN, @MENU_PATH nvarchar(500) IN, @MENU_LABEL nvarchar(200) IN, @CATEGORY_NAME nvarchar(200) IN, @SUB_CATEGORY_NAME nvarchar(200) IN, @MENU_ORDER int IN, @IP_ADDRESS varchar(45) IN, @USER_AGENT nvarchar(1000) IN, @BROWSER varchar(100) IN, @OS varchar(100) IN, @REFERRER nvarchar(500) IN, @DETAIL nvarchar(1000) IN, @RESULT int OUT, @COUNTS_AS_VISIT bit IN | 원문 조회 또는 감사 흐름에서 호출 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/logmanagement/repository/LogManagementMapper.kt#L92) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 업로드 일자, 파일명, 총 건수, 업체확인, 미확인, 입금 등록 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 서비스 현황 > 입금관리 > 본사 입금 등록의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 다운로드할 데이터가 없습니다. | 업로드 일자, 파일명, 총 건수, 업체확인, 미확인, 입금 등록 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 저장되지 않은 변경사항이 있습니다. 먼저 저장해주세요. | 업로드 일자, 파일명, 총 건수, 업체확인, 미확인, 입금 등록 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 단발성은 입금대기로 보류할 수 없습니다. | 업로드 일자, 파일명, 총 건수, 업체확인, 미확인, 입금 등록 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 변경된 항목이 없습니다. | 업로드 일자, 파일명, 총 건수, 업체확인, 미확인, 입금 등록 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/PaymentRoutes.tsx#L65) · [HeadOfficeDepositRegistrationDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositRegistrationDetailPage.tsx#L316) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/headOfficeDepositRegistrationApi.ts#L94) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/headOfficeDepositRegistrationApi.ts#L145) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/osIvDepositApi.ts#L32) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/osIvDepositApi.ts#L45) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/headOfficeDepositRegistrationApi.ts#L188) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/headOfficeDepositRegistrationApi.ts#L104) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/headOfficeDepositRegistrationApi.ts#L116) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/headOfficeDepositRegistrationApi.ts#L126) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 16개 중 개발 메타데이터 확인 16개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-351be4a556c4814c) | Demo 메타데이터 15/17개 확인 · 미확인 2개 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

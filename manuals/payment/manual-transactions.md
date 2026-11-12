# [입금·예치금·배분·취소·환불] 단발성 매출·입금 등록 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

검색 조건에 맞는 단발성 매출·입금 목록을 20건 단위로 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 입금·예치금·배분·취소·환불 |
| 언제 사용하는가 | 단발성 매출유형 조회, 단발성 매출·입금 목록 조회, 단발성 매출·입금 복사작성, 단발성 매출·입금 목록 다운로드 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 매출 발생일자, 업체조건, 전체, 회사명, 사업자번호, 구분 |
| 업무 흐름 | 단발성 매출유형 조회, 단발성 매출·입금 목록 조회, 단발성 매출·입금 복사작성, 단발성 매출·입금 목록 다운로드 |
| 이 페이지의 역할 | 조회 · 단발성 매출·입금 목록 조회 |
| 판단 결과·다음 업무 | [단발성 매출·입금 등록 상세](manual-transactions__by-id.md) · [단발성 매출·입금 등록](manual-transactions__new.md) · [단발성 매출·입금 등록 수정](manual-transactions__by-id__edit.md) |
| 다른 화면과의 구분 | 이 경로에서 볼 수 있는 조건·결과를 기준으로 사용한다. 독립 경로의 상세·등록은 관련 화면에 연결한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 복사 등록 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/ManualTransactionCopyDialog.tsx#L55) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 검색 조건에 맞는 단발성 매출·입금 목록을 20건 단위로 조회한다. |
| 메뉴·화면 경로 | 서비스 현황 > 입금관리 > 단발성 매출·입금 등록 · `/payment/manual-transactions` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [단발성 매출·입금 등록 상세](manual-transactions__by-id.md) · [단발성 매출·입금 등록](manual-transactions__new.md) · [단발성 매출·입금 등록 수정](manual-transactions__by-id__edit.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/payment/manual-transactions` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 단발성 매출유형 조회 | `/payment/manual-transactions` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 단발성 매출·입금 목록 조회 | `/payment/manual-transactions` `VIEW` | `ManualTransactionSearchRequest` `page`, `size`, `startDate`, `endDate`, `companyCondition`, `keyword`, `transactionTypes`, `salesClassCodes` |
| 단발성 매출·입금 복사작성 | `/payment/manual-transactions` `PROCESS` | `ManualTransactionCopyRequest` `search`, `selectionMode`, `selectedIds`, `excludedIds`, `salesDate` |
| 단발성 매출·입금 목록 다운로드 | `/payment/manual-transactions` `EXCEL_DOWNLOAD` | `ManualTransactionDownloadRequest` `search`, `selectionMode`, `selectedIds`, `excludedIds` |

코드에서 확인한 버튼·작업명은 **검색**, **다운로드**, **매출 등록**, **복사작성**, **복사 등록**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **서비스 현황 > 입금관리 > 단발성 매출·입금 등록**를 연다. `/payment/manual-transactions`를 연다.
2. **매출 발생일자**, **업체조건**, **전체**, **회사명**, **사업자번호**, **구분**, **매출** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색**, **다운로드**, **매출 등록**, **복사 등록** 중 해당 버튼을 선택한다.
3. **단발성 매출·입금 목록 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [단발성 매출·입금 등록 상세](manual-transactions__by-id.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 매출 발생일자 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/ManualTransactionListPage.tsx#L66) |
| 업체조건 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/ManualTransactionListPage.tsx#L76) |
| 전체 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `ALL` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/ManualTransactionListPage.tsx#L83) |
| 회사명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `COMPANY_NAME` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/ManualTransactionListPage.tsx#L84) |
| 사업자번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `BUSINESS_NUMBER` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/ManualTransactionListPage.tsx#L85) |
| 구분 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/ManualTransactionListPage.tsx#L97) |
| 매출 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `S` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/ManualTransactionListPage.tsx#L104) |
| 입금 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `D` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/ManualTransactionListPage.tsx#L105) |
| 매출유형 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/ManualTransactionListPage.tsx#L111) |
| 매출발생일자 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | API 요청 `salesDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/ManualTransactionListPage.tsx#L319) |
| 공급가액 | 출력 | 조회 응답 기준 | 화면 필드 `supplyAmount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/ManualTransactionListPage.tsx#L342) |
| 부가세액 | 출력 | 조회 응답 기준 | 화면 필드 `taxAmount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/ManualTransactionListPage.tsx#L349) |
| 합계금액 | 출력 | 조회 응답 기준 | 화면 필드 `totalAmount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/ManualTransactionListPage.tsx#L356) |
| 적요 | 출력 | 조회 응답 기준 | 화면 필드 `remark` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/ManualTransactionListPage.tsx#L363) |
| 복사 등록 건수 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/ManualTransactionCopyDialog.tsx#L73) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 단발성 매출유형 조회 | `GET /api/v1/status/payment/manual-transactions/sales-classes` · `/payment/manual-transactions` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/manualtransaction/ManualTransactionController.kt#L68) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `code`, `label` | `SB_BILL.dbo.USPBILL_MANUALLY_SALES_CLASSCODE_USE` |
| 단발성 매출·입금 목록 조회 | `GET /api/v1/status/payment/manual-transactions` · `/payment/manual-transactions` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/manualtransaction/ManualTransactionController.kt#L60) | `ManualTransactionSearchRequest` `page`, `size`, `startDate`, `endDate`, `companyCondition`, `keyword`, `transactionTypes`, `salesClassCodes` → `success`, `data`, `error`, `content`, `totalElements`, `currentPage` | `smartwork.dbo.UspBill_ManuallySalesList_SELECT`, `SB_BILL.dbo.USPBILL_MANUALLY_SALES_CLASSCODE_USE` · 코드 연계 트랜잭션 |
| 단발성 매출·입금 복사작성 | `POST /api/v1/status/payment/manual-transactions/copy` · `/payment/manual-transactions` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/manualtransaction/ManualTransactionController.kt#L124) | `ManualTransactionCopyRequest` `search`, `selectionMode`, `selectedIds`, `excludedIds`, `salesDate` → `success`, `data`, `error`, `copiedCount` | `SB_BILL.dbo.UPSAVE_MANUALLY_SALES_MNG_COPY`, `smartwork.dbo.UspBill_ManuallySalesList_SELECT_Excel`, `SB_BILL.dbo.USPBILL_MANUALLY_SALES_CLASSCODE_USE`, `SB_BILL.dbo.MANUALLY_SALES` · 정의에서 확인한 쓰기 `SB_BILL.dbo.MANUALLY_SALES` · 코드 연계 트랜잭션 |
| 단발성 매출·입금 목록 다운로드 | `POST /api/v1/status/payment/manual-transactions/download` · `/payment/manual-transactions` `EXCEL_DOWNLOAD` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/manualtransaction/ManualTransactionController.kt#L135) | `ManualTransactionDownloadRequest` `search`, `selectionMode`, `selectedIds`, `excludedIds` → 파일 또는 오류 응답 | `smartwork.dbo.UspBill_ManuallySalesList_SELECT_Excel`, `SB_BILL.dbo.USPBILL_MANUALLY_SALES_CLASSCODE_USE` |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `SB_BILL.dbo.USPBILL_MANUALLY_SALES_CLASSCODE_USE` | @PAGE int, @TOP int, @CODE_TYPE varchar(20) | 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/manualtransaction/repository/ManualTransactionMapper.kt#L110) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-1b3cb1f5c77f8846) |
| `smartwork.dbo.UspBill_ManuallySalesList_SELECT` | @PAGE int, @TOP int, @SALES_DATE varchar(1), @FROM_DATE datetime, @TO_DATE datetime, @SALES_CLIENT varchar(1), @CLIENTINFO varchar(70), @SALES_TYPE varchar(10), @SALES_CLASS varchar(max) | 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/manualtransaction/repository/ManualTransactionMapper.kt#L50) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-a0740d2ccfe2dc5d) |
| `SB_BILL.dbo.UPSAVE_MANUALLY_SALES_MNG_COPY` | @COPY_IDX int, @SALES_DATE datetime, @CUSER int, @ERR_CODE varchar(10) OUT | 정의 참조 `SB_BILL.dbo.MANUALLY_SALES` · 정적 쓰기 `SB_BILL.dbo.MANUALLY_SALES` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/manualtransaction/repository/ManualTransactionMapper.kt#L185) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-397f6f6bcc068ce7) |
| `smartwork.dbo.UspBill_ManuallySalesList_SELECT_Excel` | @SALES_DATE varchar(1), @FROM_DATE datetime, @TO_DATE datetime, @SALES_CLIENT varchar(1), @CLIENTINFO varchar(70), @SALES_TYPE varchar(10), @SALES_CLASS varchar(max) | 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/manualtransaction/repository/ManualTransactionMapper.kt#L74) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-51699feec8452413) |
| `SB_BILL.dbo.MANUALLY_SALES` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/manualtransaction/repository/ManualTransactionMapper.kt#L153) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-5d3bd90a9d6765f9) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 매출 발생일자, 업체조건, 전체, 회사명, 사업자번호, 구분 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 서비스 현황 > 입금관리 > 단발성 매출·입금 등록의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 복사 작성할 매출·입금 건을 선택해 주세요. | 매출 발생일자, 업체조건, 전체, 회사명, 사업자번호, 구분 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 단발성 매출 복사 작성을 취소하였습니다. | 매출 발생일자, 업체조건, 전체, 회사명, 사업자번호, 구분 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 다운로드할 항목을 선택해 주세요. | 매출 발생일자, 업체조건, 전체, 회사명, 사업자번호, 구분 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 다운로드할 데이터가 없습니다. | 매출 발생일자, 업체조건, 전체, 회사명, 사업자번호, 구분 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/PaymentRoutes.tsx#L68) · [ManualTransactionListPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/ManualTransactionListPage.tsx#L53) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/manualTransactionApi.ts#L64) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/manualTransactionApi.ts#L58) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/manualTransactionApi.ts#L106) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/manualTransactionApi.ts#L116) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 5개 중 개발 메타데이터 확인 5개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-498b89b8758ad9b1) | Demo 메타데이터 5/5개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

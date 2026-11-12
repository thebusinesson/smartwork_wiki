# [입금·예치금·배분·취소·환불] 단발성 매출·입금 등록 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

단발성 매출 또는 입금 거래를 등록한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 입금·예치금·배분·취소·환불 |
| 언제 사용하는가 | 단발성 매출유형 조회, 단발성 거래처 검색, 단발성 매출·입금 등록 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 매출발생일자, 거래처, 회사명, 사업자번호, 구분, 매출 |
| 업무 흐름 | 단발성 매출유형 조회, 단발성 거래처 검색, 단발성 매출·입금 등록 |
| 이 페이지의 역할 | 등록 · 단발성 매출·입금 등록 |
| 판단 결과·다음 업무 | [단발성 매출·입금 등록](manual-transactions.md) · [단발성 매출·입금 등록 상세](manual-transactions__by-id.md) |
| 다른 화면과의 구분 | 서비스 현황 > 입금관리 > 단발성 매출·입금 등록에서 사용하는 등록 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 단발성 매출 또는 입금 거래를 등록한다. |
| 메뉴·화면 경로 | 서비스 현황 > 입금관리 > 단발성 매출·입금 등록 · `/payment/manual-transactions/new` |
| 화면 유형·담당 | 등록 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [단발성 매출·입금 등록](manual-transactions.md) · [단발성 매출·입금 등록 상세](manual-transactions__by-id.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/payment/manual-transactions` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 단발성 매출유형 조회 | `/payment/manual-transactions` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 단발성 거래처 검색 | `/payment/manual-transactions` `VIEW` | `ManualTransactionCompanySearchRequest` `searchType`, `keyword`, `page`, `size` |
| 단발성 매출·입금 등록 | `/payment/manual-transactions` `PROCESS` | `ManualTransactionUpsertRequest` `salesDate`, `companyId`, `transactionType`, `salesClassCode`, `supplyAmount`, `taxAmount`, `totalAmount`, `remark`, `autoCalculate` |

코드에서 확인한 버튼·작업명은 **검색**, **목록**, **저장**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [단발성 매출·입금 등록](manual-transactions.md)에서 대상 또는 작업을 선택한다. `/payment/manual-transactions/new`를 연다.
2. **매출발생일자**, **거래처**, **회사명**, **사업자번호**, **구분**, **매출**, **입금** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **거래처 검색 방식**, **검색**, **저장** 중 해당 버튼을 선택한다.
3. **단발성 매출·입금 등록**을 실행하기 전에 변경 대상과 입력값을 확인한다. 처리 응답을 확인하고 관련 조회에서 대상의 상태를 확인한다.
4. 후속 조회나 목록 복귀가 필요하면 [단발성 매출·입금 등록 상세](manual-transactions__by-id.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 매출발생일자 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/ManualTransactionForm.tsx#L302) |
| 거래처 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/ManualTransactionForm.tsx#L310) |
| 회사명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/ManualTransactionForm.tsx#L318) |
| 사업자번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/ManualTransactionForm.tsx#L322) |
| 회사명 입력 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/ManualTransactionForm.tsx#L344) |
| 구분 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/ManualTransactionForm.tsx#L410) |
| 매출 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/ManualTransactionForm.tsx#L419) |
| 입금 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/ManualTransactionForm.tsx#L423) |
| 매출유형 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/ManualTransactionForm.tsx#L431) |
| 매출유형 선택 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/ManualTransactionForm.tsx#L434) |
| 공급가액 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/ManualTransactionForm.tsx#L447) |
| 자동계산 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/ManualTransactionForm.tsx#L459) |
| 공급가액 기준 부가세·합계 자동계산 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/ManualTransactionForm.tsx#L460) |
| 부가세액 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/ManualTransactionForm.tsx#L469) |
| 합계금액 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/ManualTransactionForm.tsx#L484) |
| 적요 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/ManualTransactionForm.tsx#L500) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 단발성 매출유형 조회 | `GET /api/v1/status/payment/manual-transactions/sales-classes` · `/payment/manual-transactions` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/manualtransaction/ManualTransactionController.kt#L68) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `code`, `label` | `SB_BILL.dbo.USPBILL_MANUALLY_SALES_CLASSCODE_USE` |
| 단발성 거래처 검색 | `GET /api/v1/status/payment/manual-transactions/companies` · `/payment/manual-transactions` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/manualtransaction/ManualTransactionController.kt#L74) | `ManualTransactionCompanySearchRequest` `searchType`, `keyword`, `page`, `size` → `success`, `data`, `error`, `content`, `totalElements` | `SB_BILL.dbo.USPBILL_MANUALLY_SALES_CLIENT_LIST_NEW` |
| 단발성 매출·입금 등록 | `POST /api/v1/status/payment/manual-transactions` · `/payment/manual-transactions` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/manualtransaction/ManualTransactionController.kt#L90) | `ManualTransactionUpsertRequest` `salesDate`, `companyId`, `transactionType`, `salesClassCode`, `supplyAmount`, `taxAmount`, `totalAmount`, `remark`, `autoCalculate` → `success`, `data`, `error` | `SB_BILL.dbo.UPSAVE_MANUALLY_SALES_MNG`, `SB_BILL.dbo.USPBILL_MANUALLY_SALES_CLIENT_DETAIL`, `SB_BILL.dbo.USPBILL_MANUALLY_SALES_CLASSCODE_USE` · 정의에서 확인한 쓰기 `SB_BILL.dbo.MANUALLY_SALES` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `SB_BILL.dbo.USPBILL_MANUALLY_SALES_CLASSCODE_USE` | @PAGE int, @TOP int, @CODE_TYPE varchar(20) | 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/manualtransaction/repository/ManualTransactionMapper.kt#L110) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-1b3cb1f5c77f8846) |
| `SB_BILL.dbo.USPBILL_MANUALLY_SALES_DETAIL` | @IDX int | 정의 참조 `SB_BILL.dbo.BILL_COMMON_CODE`, `SB_BILL.dbo.MANUALLY_SALES`, `SB_BILL.dbo.MANUALLY_SALES_CLIENT`, `office.dbo.SAWON` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/manualtransaction/repository/ManualTransactionMapper.kt#L101) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-8ee5b12ce4ae32dc) |
| `SB_BILL.dbo.MANUALLY_SALES` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/manualtransaction/repository/ManualTransactionMapper.kt#L153) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-5d3bd90a9d6765f9) |
| `SB_BILL.dbo.USPBILL_MANUALLY_SALES_CLIENT_LIST_NEW` | @PAGE int, @TOP int, @SEARCHCODE varchar(1), @KEYWORD varchar(70) | 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/manualtransaction/repository/ManualTransactionMapper.kt#L124) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b518915b55af230b) |
| `SB_BILL.dbo.UPMODIFY_MANUALLY_SALES_MNG` | @IDX int, @SALES_DATE datetime, @COM_NO int, @SALES_TYPE varchar(10), @SALES_CLASS varchar(20), @SUP_AMT money, @TAX_AMT money, @TOT_AMT money, @REMARK varchar(max), @UUSER int, @AUTOCAL_YN varchar(1), @ERR_CODE varchar(10) OUT | 정의 참조 `SB_BILL.dbo.MANUALLY_SALES` · 정적 쓰기 `SB_BILL.dbo.MANUALLY_SALES` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/manualtransaction/repository/ManualTransactionMapper.kt#L171) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-a74ad1d4781bc5dc) |
| `SB_BILL.dbo.USPBILL_MANUALLY_SALES_CLIENT_DETAIL` | @COM_NO int | 정의 참조 `SB_BILL.dbo.MANUALLY_SALES_CLIENT` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/manualtransaction/repository/ManualTransactionMapper.kt#L134) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-d09cbac1a39f5469) |
| `SB_BILL.dbo.UPSAVE_MANUALLY_SALES_MNG` | @SALES_DATE datetime, @COM_NO int, @SALES_TYPE varchar(10), @SALES_CLASS varchar(20), @SUP_AMT money, @TAX_AMT money, @TOT_AMT money, @REMARK varchar(max), @CUSER int, @AUTOCAL_YN varchar(1), @ERR_CODE varchar(10) OUT | 정의 참조 `SB_BILL.dbo.MANUALLY_SALES` · 정적 쓰기 `SB_BILL.dbo.MANUALLY_SALES` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/manualtransaction/repository/ManualTransactionMapper.kt#L162) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-d2f87bcce81115b4) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 매출발생일자, 거래처, 회사명, 사업자번호, 구분, 매출 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 서비스 현황 > 입금관리 > 단발성 매출·입금 등록의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/PaymentRoutes.tsx#L69) · [ManualTransactionFormPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/ManualTransactionFormPage.tsx#L20) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/manualTransactionApi.ts#L64) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/manualTransactionApi.ts#L86) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/manualTransactionApi.ts#L76) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/manualTransactionApi.ts#L97) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/manualTransactionApi.ts#L91) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 7개 중 개발 메타데이터 확인 7개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-df726387e1aac0e1) | Demo 메타데이터 7/7개 확인 · 2026-11-11 |
| 화면 재현 | [로컬 Playwright 등록 화면 대조](../../evidence/browser/all-pages-accuracy-2026-11-11.json) | 등록 경로 진입 확인 · 2026-11-11 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

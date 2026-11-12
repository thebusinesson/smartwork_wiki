# [세금계산서·거래명세서 원문과 증빙] 거래명세서 조회 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

검색조건에 맞는 거래명세서 목록과 페이징 정보를 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 세금계산서·거래명세서 원문과 증빙 |
| 언제 사용하는가 | 거래명세서 목록 조회 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 작성일자, 공급자 사업자번호, 공급받는자 사업자번호, 종류, 공급가액, 현재상태 |
| 업무 흐름 | 거래명세서 목록 조회 |
| 이 페이지의 역할 | 조회 · 거래명세서 목록 조회 |
| 판단 결과·다음 업무 | [거래명세서 조회 상세](transaction-statement__by-id.md) |
| 다른 화면과의 구분 | 이 경로에서 볼 수 있는 조건·결과를 기준으로 사용한다. 독립 경로의 상세·등록은 관련 화면에 연결한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 검색조건에 맞는 거래명세서 목록과 페이징 정보를 조회한다. |
| 메뉴·화면 경로 | SB 서비스관리 > 전자세금계산서 > 거래명세서 조회 · `/tax-invoice/transaction-statement` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [거래명세서 조회 상세](transaction-statement__by-id.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/tax-invoice/transaction-statement` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 거래명세서 목록 조회 | `/tax-invoice/transaction-statement` `VIEW` | `TransactionStatementSearchRequest` `startDate`, `endDate`, `supplierSearchType`, `supplierValue`, `buyerSearchType`, `buyerValue`, `documentStatus`, `page`, `size` |

코드에서 확인한 버튼·작업명은 **검색**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **SB 서비스관리 > 전자세금계산서 > 거래명세서 조회**를 연다. `/tax-invoice/transaction-statement`를 연다.
2. **공급자 사업자번호**, **공급받는자 사업자번호**, **공급자**, **전체**, **사업자번호**, **회사명**, **공급받는자** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색** 중 해당 버튼을 선택한다.
3. **거래명세서 목록 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [거래명세서 조회 상세](transaction-statement__by-id.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 작성일자 | 출력 | 조회 응답 기준 | 화면 필드 `writeDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TransactionStatementListPage.tsx#L195) |
| 공급자 사업자번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `SUPPLIER_BUSINESS_NUMBER` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TransactionStatementListPage.tsx#L204) |
| 공급받는자 사업자번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `BUYER_BUSINESS_NUMBER` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TransactionStatementListPage.tsx#L220) |
| 종류 | 출력 | 조회 응답 기준 | 화면 필드 `type` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TransactionStatementListPage.tsx#L228) |
| 공급가액 | 출력 | 조회 응답 기준 | 화면 필드 `supplyAmount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TransactionStatementListPage.tsx#L229) |
| 현재상태 | 출력 | 조회 응답 기준 | 화면 필드 `currentStatus` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TransactionStatementListPage.tsx#L230) |
| 공급자 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TransactionStatementListPage.tsx#L54) |
| 전체 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `all` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TransactionStatementListPage.tsx#L103) |
| 사업자번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `business-number` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TransactionStatementListPage.tsx#L85) |
| 회사명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `company-name` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TransactionStatementListPage.tsx#L86) |
| 공급받는자 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TransactionStatementListPage.tsx#L76) |
| 문서 상태 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TransactionStatementListPage.tsx#L97) |
| 발행 요청 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `request` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TransactionStatementListPage.tsx#L105) |
| 발행 거부 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `rejected` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TransactionStatementListPage.tsx#L106) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 거래명세서 목록 조회 | `GET /api/v1/sb-service/transaction-statements` · `/tax-invoice/transaction-statement` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/taxinvoice/transactionstatement/TransactionStatementController.kt#L50) | `TransactionStatementSearchRequest` `startDate`, `endDate`, `supplierSearchType`, `supplierValue`, `buyerSearchType`, `buyerValue`, `documentStatus`, `page`, `size` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `currentPage`, `size` | `smartwork.dbo.UspTransactionStatementListSelect` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.UspTransactionStatementListSelect` | @START_DATE varchar(10), @END_DATE varchar(10), @SUPCOM char(1), @SUBKEYWORD varchar(100), @BYRCOM char(1), @BYRKEYWORD varchar(100), @CHKSTATUS char(1), @CHKDTITYPE varchar(11) | 정의 참조 `SB_COMMON.dbo.upSBAdm_LstDTT` · 쓰기 구문 존재 · 대상 별칭 또는 하위 정의 확인 · 하위 호출 `SB_COMMON.dbo.upSBAdm_LstDTT` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/transactionstatement/repository/TransactionStatementMapper.kt#L50) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-a70de6cc9b5ab402) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 작성일자, 공급자 사업자번호, 공급받는자 사업자번호, 종류, 공급가액, 현재상태 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 서비스관리 > 전자세금계산서 > 거래명세서 조회의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 검색 결과가 없습니다. | 작성일자, 공급자 사업자번호, 공급받는자 사업자번호, 종류, 공급가액, 현재상태 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/TaxInvoiceRoutes.tsx#L46) · [TransactionStatementListPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TransactionStatementListPage.tsx#L120) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/api/transactionStatementApi.ts#L46) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 1개 중 개발 메타데이터 확인 1개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-a13041c8d65ad4d1) | Demo 메타데이터 1/1개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

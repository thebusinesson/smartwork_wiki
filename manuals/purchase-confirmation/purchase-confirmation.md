# [구매확인서 원문과 품목·참조] 구매확인서 조회 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

구매확인서 목록을 조회한다. mode=SUPPLIER_OPEN_COMPLETE 시 dateType/docNumberType/statusFilter/cancelOnly 는 무시됩니다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 구매확인서 원문과 품목·참조 |
| 언제 사용하는가 | 구매확인서 조회 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 저장일자, 신청일자, 개설일자, 전체, 사업자번호, 회사명 |
| 업무 흐름 | 구매확인서 조회 |
| 이 페이지의 역할 | 조회 · 구매확인서 조회 |
| 판단 결과·다음 업무 | [구매확인서 조회 상세](purchase-confirmation__by-id.md) |
| 다른 화면과의 구분 | 이 경로에서 볼 수 있는 조건·결과를 기준으로 사용한다. 독립 경로의 상세·등록은 관련 화면에 연결한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 구매확인서 목록을 조회한다. mode=SUPPLIER_OPEN_COMPLETE 시 dateType/docNumberType/statusFilter/cancelOnly 는 무시됩니다. |
| 메뉴·화면 경로 | SB 서비스관리 > 구매확인서 > 구매확인서 조회 · `/purchase-confirmation/purchase-confirmation` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [구매확인서 조회 상세](purchase-confirmation__by-id.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/purchase-confirmation/purchase-confirmation` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 구매확인서 조회 | `/purchase-confirmation/purchase-confirmation` `VIEW` | `PurchaseConfirmationLookupSearchRequest` `mode`, `dateType`, `startDate`, `endDate`, `supplierType`, `supplierKeyword`, `purchaserType`, `purchaserKeyword`, `docNumberType`, `docNumberKeyword`, `statusFilter`, `cancelOnly`, `page`, `size` · 서버 필수 `startDate`, `endDate` |
| 구매확인서 전송자 원문 조회 | `/purchase-confirmation/purchase-confirmation` / `UNMASK` | `smartbillMainkey`, `field` |

코드에서 확인한 버튼·작업명은 **검색**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **SB 서비스관리 > 구매확인서 > 구매확인서 조회**를 연다. `/purchase-confirmation/purchase-confirmation`를 연다.
2. **저장일자**, **신청일자**, **개설일자**, **전체**, **사업자번호**, **회사명**, **스마트빌 문서번호** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색** 중 해당 버튼을 선택한다.
3. **구매확인서 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [구매확인서 조회 상세](purchase-confirmation__by-id.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 저장일자 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `저장일자` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/PurchaseConfirmationPage.tsx#L112) |
| 신청일자 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `신청일자` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/PurchaseConfirmationPage.tsx#L113) |
| 개설일자 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `개설일자` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/PurchaseConfirmationPage.tsx#L114) |
| 전체 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `all` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/PurchaseConfirmationPage.tsx#L124) |
| 사업자번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `사업자번호` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/PurchaseConfirmationPage.tsx#L119) |
| 회사명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `회사명` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/PurchaseConfirmationPage.tsx#L120) |
| 스마트빌 문서번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `documentNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/PurchaseConfirmationPage.tsx#L125) |
| KTNET 개설완료 번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `ktnetOpenCompleteNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/PurchaseConfirmationPage.tsx#L126) |
| 날짜 조건 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/PurchaseConfirmationPage.tsx#L134) |
| 공급자 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/PurchaseConfirmationPage.tsx#L146) |
| 구매신청 업체 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/PurchaseConfirmationPage.tsx#L172) |
| 문서 번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/PurchaseConfirmationPage.tsx#L197) |
| 구분 | 출력 | 조회 응답 기준 | 화면 필드 `gubun` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/PurchaseConfirmationPage.tsx#L405) |
| 문서번호 | 출력 | 조회 응답 기준 | 화면 필드 `smartbillDocNo` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/PurchaseConfirmationPage.tsx#L406) |
| 공급자 회사명 | 출력 | 조회 응답 기준 | 화면 필드 `supplierName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/PurchaseConfirmationPage.tsx#L416) |
| 구매신청업체 회사명 | 출력 | 조회 응답 기준 | 화면 필드 `purchaserComName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/PurchaseConfirmationPage.tsx#L423) |
| 금액 | 출력 | 조회 응답 기준 | 화면 필드 `totalAmount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/PurchaseConfirmationPage.tsx#L430) |
| 확인은행 | 출력 | 조회 응답 기준 | 화면 필드 `confirmBankName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/PurchaseConfirmationPage.tsx#L438) |
| 공급자확인 | 출력 | 조회 응답 기준 | 화면 필드 `supplierConfirmYn` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/PurchaseConfirmationPage.tsx#L441) |
| 전송자 | 출력 | 조회 응답 기준 | 화면 필드 `senderName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/PurchaseConfirmationPage.tsx#L452) |
| 전송자 실명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `SENDER_NAME` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/PurchaseConfirmationPage.tsx#L475) |
| 동보전송 유무 | 출력 | 조회 응답 기준 | 화면 필드 `notified` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/PurchaseConfirmationPage.tsx#L488) |
| 오류내용 | 출력 | 조회 응답 기준 | 화면 필드 `errorMessage` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/PurchaseConfirmationPage.tsx#L493) |
| 공급자 구매확인서(개설완료) 조회 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/PurchaseConfirmationPage.tsx#L511) |
| 신청 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/PurchaseConfirmationPage.tsx#L540) |
| 개설 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/PurchaseConfirmationPage.tsx#L550) |
| 취소신청여부 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/PurchaseConfirmationPage.tsx#L557) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 구매확인서 조회 | `GET /api/v1/purchase-confirmation/purchase-confirmations` · `/purchase-confirmation/purchase-confirmation` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/purchaseconfirmation/lookup/PurchaseConfirmationLookupController.kt#L70) | `PurchaseConfirmationLookupSearchRequest` `mode`, `dateType`, `startDate`, `endDate`, `supplierType`, `supplierKeyword`, `purchaserType`, `purchaserKeyword`, `docNumberType`, `docNumberKeyword`, `statusFilter`, `cancelOnly`, `page`, `size` · 서버 필수 `startDate`, `endDate` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `currentPage`, `size` | `smartwork.dbo.sp_GetPurchaseConfirmationList`, `smartwork.dbo.sp_GetSupplierPurchaseConfirmationList` · 코드 연계 트랜잭션 |
| 구매확인서 전송자 원문 조회 | `POST /api/v1/purchase-confirmation/purchase-confirmations/{smartbillMainkey}/sensitive-values/reveal` · `/purchase-confirmation/purchase-confirmation` / `UNMASK` · [화면 컴포넌트](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/PurchaseConfirmationPage.tsx#L473) · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/purchaseconfirmation/lookup/PurchaseConfirmationLookupController.kt#L114) | `smartbillMainkey`, `field` → 요청한 항목의 원문 응답 | 권한 검사 후 대상 값을 조회하고 감사 기록을 남긴다. |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.sp_GetPurchaseConfirmationList` | @DateType char(1), @StartDate datetime, @EndDate datetime, @SupplierType char(1), @SupplierKeyword varchar(70) = NULL, @PurchaserType char(1), @PurchaserKeyword varchar(70) = NULL, @DocNumberType char(1), @DocNumberKeyword varchar(50) = NULL, @StatusFilter varchar(10), @CancelOnly char(1), @PageNumber int, @PageSize int | 정의 참조 `SmartBill3.dbo.COMPANY`, `KT_Net.dbo.GENRES_M`, `SmartBill3.dbo.MEMBER`, `KT_Net.dbo.PCRLIC_M`, `SmartBill3.dbo.SB_APPPCR_M` 외 1개 · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/purchaseconfirmation/lookup/repository/PurchaseConfirmationLookupMapper.kt#L70) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-85be7a7d92a7a358) |
| `smartwork.dbo.sp_GetSupplierPurchaseConfirmationList` | @StartDate datetime, @EndDate datetime, @SupplierType char(1), @SupplierKeyword varchar(70) = NULL, @PurchaserType char(1), @PurchaserKeyword varchar(70) = NULL, @DocNumberKeyword varchar(50) = NULL, @PageNumber int, @PageSize int | 정의 참조 `SmartBill3.dbo.COMPANY`, `KT_Net.dbo.GENRES_M`, `SmartBill3.dbo.MEMBER`, `KT_Net.dbo.PCRLIC_M`, `SmartBill3.dbo.SB_APPPCR_M` 외 1개 · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/purchaseconfirmation/lookup/repository/PurchaseConfirmationLookupMapper.kt#L109) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-258c871c3a0d2515) |
| `SmartBill3.dbo.SB_APPPCR_M` | 개발 컬럼 메타데이터 확인 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/purchaseconfirmation/lookup/repository/PurchaseConfirmationLookupMapper.kt#L120) |
| `SmartBill3.dbo.MEMBER` | 개발 컬럼 메타데이터 확인 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/purchaseconfirmation/lookup/repository/PurchaseConfirmationLookupMapper.kt#L120) |
| `smartwork.dbo.usp_sw_log_access_event_insert` | @EVENT_TYPE varchar(30) IN, @STATUS varchar(20) IN, @USER_ID bigint IN, @MEMBER_ID nvarchar(50) IN, @USER_NAME nvarchar(100) IN, @DEPARTMENT_NAME nvarchar(100) IN, @PAGE_TITLE nvarchar(200) IN, @PATH nvarchar(500) IN, @MENU_PATH nvarchar(500) IN, @MENU_LABEL nvarchar(200) IN, @CATEGORY_NAME nvarchar(200) IN, @SUB_CATEGORY_NAME nvarchar(200) IN, @MENU_ORDER int IN, @IP_ADDRESS varchar(45) IN, @USER_AGENT nvarchar(1000) IN, @BROWSER varchar(100) IN, @OS varchar(100) IN, @REFERRER nvarchar(500) IN, @DETAIL nvarchar(1000) IN, @RESULT int OUT, @COUNTS_AS_VISIT bit IN | 원문 조회 또는 감사 흐름에서 호출 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/logmanagement/repository/LogManagementMapper.kt#L92) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 저장일자, 신청일자, 개설일자, 전체, 사업자번호, 회사명 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 서비스관리 > 구매확인서 > 구매확인서 조회의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 데이터를 불러오는 중 오류가 발생했습니다. | 저장일자, 신청일자, 개설일자, 전체, 사업자번호, 회사명 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 데이터가 없습니다. | 저장일자, 신청일자, 개설일자, 전체, 사업자번호, 회사명 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/PurchaseConfirmationRoutes.tsx#L14) · [PurchaseConfirmationPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/PurchaseConfirmationPage.tsx#L90) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/api/purchaseConfirmationApi.ts#L44) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 2개 중 개발 메타데이터 확인 2개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-20b46d73fae496c3) | Demo 메타데이터 5/5개 확인 · Dev와 계약 차이 1개 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

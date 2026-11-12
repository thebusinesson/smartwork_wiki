# [오픈스크랩 대상·수집과 결과] 매출/매입 조회 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

검색조건으로 오픈스크랩 수집함의 매출/매입 세금계산서 목록과 합계를 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 오픈스크랩 대상·수집과 결과 |
| 언제 사용하는가 | 매출/매입 목록, 허브업체 드롭다운, 매출/매입 엑셀 다운로드 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 작성일자, 공급자 사업자번호, 공급자 회사명, 공급받는자 사업자번호, 공급받는자 회사명, 공급가액 |
| 업무 흐름 | 매출/매입 목록, 허브업체 드롭다운, 매출/매입 엑셀 다운로드 |
| 이 페이지의 역할 | 조회 · 매출/매입 목록 |
| 판단 결과·다음 업무 | [매출/매입 조회 상세](sales-purchases__by-issueId.md) |
| 다른 화면과의 구분 | 이 경로에서 볼 수 있는 조건·결과를 기준으로 사용한다. 독립 경로의 상세·등록은 관련 화면에 연결한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 검색조건으로 오픈스크랩 수집함의 매출/매입 세금계산서 목록과 합계를 조회한다. |
| 메뉴·화면 경로 | SB 서비스관리 > 오픈스크랩 > 매출/매입 조회 · `/openscrap/sales-purchases` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [매출/매입 조회 상세](sales-purchases__by-issueId.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/openscrap/sales-purchases` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 매출/매입 목록 | `/openscrap/sales-purchases` `VIEW` | `OpenscrapSalesPurchaseSearchRequest` `dateType`, `startDate`, `endDate`, `hubRegno`, `supplierSearchType`, `supplierKeyword`, `buyerSearchType`, `buyerKeyword`, `approvalNumber`, `collectionStartDate`, `collectionEndDate`, `division`, `taxType`, `consignment` |
| 허브업체 드롭다운 | `/openscrap/sales-purchases` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 매출/매입 엑셀 다운로드 | `/openscrap/sales-purchases` `EXCEL_DOWNLOAD` | `OpenscrapSalesPurchaseDownloadRequest` `dateType`, `startDate`, `endDate`, `hubRegno`, `supplierSearchType`, `supplierKeyword`, `buyerSearchType`, `buyerKeyword`, `approvalNumber`, `collectionStartDate`, `collectionEndDate`, `division`, `taxType`, `consignment` |

코드에서 확인한 버튼·작업명은 **검색**, **다운로드**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **SB 서비스관리 > 오픈스크랩 > 매출/매입 조회**를 연다. `/openscrap/sales-purchases`를 연다.
2. **날짜 조건**, **작성 일자**, **발행 일자**, **전송 일자**, **허브업체**, **전체**, **승인번호** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색**, **다운로드** 중 해당 버튼을 선택한다.
3. **매출/매입 목록** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [매출/매입 조회 상세](sales-purchases__by-issueId.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 작성일자 | 출력 | 조회 응답 기준 | 화면 필드 `writeDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/SalesPurchasesListPage.tsx#L428) |
| 공급자 사업자번호 | 출력 | 조회 응답 기준 | 화면 필드 `supplierRegno` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/SalesPurchasesListPage.tsx#L436) |
| 공급자 회사명 | 출력 | 조회 응답 기준 | 화면 필드 `supplierName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/SalesPurchasesListPage.tsx#L452) |
| 공급받는자 사업자번호 | 출력 | 조회 응답 기준 | 화면 필드 `buyerRegno` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/SalesPurchasesListPage.tsx#L460) |
| 공급받는자 회사명 | 출력 | 조회 응답 기준 | 화면 필드 `buyerName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/SalesPurchasesListPage.tsx#L475) |
| 공급가액 | 출력 | 조회 응답 기준 | 화면 필드 `supplyAmount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/SalesPurchasesListPage.tsx#L490) |
| 수집일자 | 출력 | 조회 응답 기준 | 화면 필드 `collectionDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/SalesPurchasesListPage.tsx#L499) |
| OpenAPI 조회여부 | 출력 | 조회 응답 기준 | 화면 필드 `openApiSearchDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/SalesPurchasesListPage.tsx#L507) |
| 공급자 | 출력 | 조회 응답 기준 | 화면 필드 `공급자-group` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/SalesPurchasesListPage.tsx#L528) |
| 공급받는자 | 출력 | 조회 응답 기준 | 화면 필드 `공급받는자-group` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/SalesPurchasesListPage.tsx#L535) |
| 사업자번호 | 출력 | 조회 응답 기준 | 화면 필드 `공급자사업자번호-header` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/SalesPurchasesListPage.tsx#L573) |
| 회사명 | 출력 | 조회 응답 기준 | 화면 필드 `공급자회사명-header` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/SalesPurchasesListPage.tsx#L579) |
| 날짜 조건 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/SalesPurchasesListPage.tsx#L139) |
| 작성 일자 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `작성 일자` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/SalesPurchasesListPage.tsx#L145) |
| 발행 일자 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `발행 일자` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/SalesPurchasesListPage.tsx#L146) |
| 전송 일자 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `전송 일자` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/SalesPurchasesListPage.tsx#L147) |
| 허브업체 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/SalesPurchasesListPage.tsx#L153) |
| 전체 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `전체` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/SalesPurchasesListPage.tsx#L196) |
| 승인번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/SalesPurchasesListPage.tsx#L210) |
| 구분 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/SalesPurchasesListPage.tsx#L230) |
| 매출 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `매출` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/SalesPurchasesListPage.tsx#L236) |
| 매입 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `매입` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/SalesPurchasesListPage.tsx#L237) |
| 세액 종류 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/SalesPurchasesListPage.tsx#L243) |
| 과(영)세 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `과영세` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/SalesPurchasesListPage.tsx#L249) |
| 면세 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `면세` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/SalesPurchasesListPage.tsx#L250) |
| 위수탁 여부 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/SalesPurchasesListPage.tsx#L256) |
| 스마트빌 발행제외 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/SalesPurchasesListPage.tsx#L269) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 매출/매입 목록 | `GET /api/v1/openscrap/sales-purchases` · `/openscrap/sales-purchases` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/openscrap/salespurchase/OpenscrapSalesPurchaseController.kt#L66) | `OpenscrapSalesPurchaseSearchRequest` `dateType`, `startDate`, `endDate`, `hubRegno`, `supplierSearchType`, `supplierKeyword`, `buyerSearchType`, `buyerKeyword`, `approvalNumber`, `collectionStartDate`, `collectionEndDate`, `division`, `taxType`, `consignment` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `currentPage`, `size`, `summary` | `smartwork.dbo.upSW_OpenScrap_Select_DTIList` · 코드 연계 트랜잭션 |
| 허브업체 드롭다운 | `GET /api/v1/openscrap/hub-vendors` · `/openscrap/sales-purchases` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/openscrap/salespurchase/OpenscrapHubVendorController.kt#L30) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `regno`, `name` | `SB_DTI.dbo.NEOBILL_AUTHCODE`, `SB_OPENSCRAP.dbo.OS_COMPANY_INFO`, `SmartBill3.dbo.COMPANY` · 코드 연계 트랜잭션 |
| 매출/매입 엑셀 다운로드 | `GET /api/v1/openscrap/sales-purchases/download` · `/openscrap/sales-purchases` `EXCEL_DOWNLOAD` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/openscrap/salespurchase/OpenscrapSalesPurchaseController.kt#L114) | `OpenscrapSalesPurchaseDownloadRequest` `dateType`, `startDate`, `endDate`, `hubRegno`, `supplierSearchType`, `supplierKeyword`, `buyerSearchType`, `buyerKeyword`, `approvalNumber`, `collectionStartDate`, `collectionEndDate`, `division`, `taxType`, `consignment` → 파일 또는 오류 응답 | `smartwork.dbo.upSW_OpenScrap_Select_DTIList_Excel` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.upSW_OpenScrap_Select_DTIList` | @DATE_SEARCH_TYPE varchar(10), @FROM_DATE varchar(10), @TO_DATE varchar(10), @HUB_SEARCH_TYPE varchar(10), @SUP_SEARCH_TYPE varchar(15), @SUP_SEARCH_KEYWORD varchar(50), @BYR_SEARCH_TYPE varchar(15), @BYR_SEARCH_KEYWORD varchar(100), @ISSUE_ID varchar(24), @SCRAP_FROM_DATE varchar(10), @SCRAP_TO_DATE varchar(10), @SUPBUY_TYPE varchar(3), @DTI_TYPE varchar(3), @BRK_YN varchar(3), @SB_ISSUE_EXCEPT_YN varchar(1), @PAGE_NUM int, @PAGE_SIZE int | 정의 참조 `master.dbo.enc_index_char_sel_tc` · 하위 호출 `master.dbo.enc_index_char_sel_tc` · 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/openscrap/salespurchase/repository/OpenscrapSalesPurchaseMapper.kt#L61) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-41289676f9f51921) |
| `SB_DTI.dbo.NEOBILL_AUTHCODE` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/openscrap/salespurchase/repository/OpenscrapSalesPurchaseMapper.kt#L121) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b68e76fce93cd20e) |
| `SB_OPENSCRAP.dbo.OS_COMPANY_INFO` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN · 정의 참조 `master.dbo.dec_lob_sel`, `sb_openscrap.dbo.os_company_info_cub` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/openscrap/salespurchase/repository/OpenscrapSalesPurchaseMapper.kt#L121) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-f93fd8a9746c6d74) |
| `SmartBill3.dbo.COMPANY` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/openscrap/salespurchase/repository/OpenscrapSalesPurchaseMapper.kt#L121) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-0e6fcaa6b5086c07) |
| `smartwork.dbo.upSW_OpenScrap_Select_DTIList_Excel` | @DATE_SEARCH_TYPE varchar(10), @FROM_DATE varchar(10), @TO_DATE varchar(10), @HUB_SEARCH_TYPE varchar(10), @SUP_SEARCH_TYPE varchar(15), @SUP_SEARCH_KEYWORD varchar(50), @BYR_SEARCH_TYPE varchar(15), @BYR_SEARCH_KEYWORD varchar(100), @ISSUE_ID varchar(24), @SCRAP_FROM_DATE varchar(10), @SCRAP_TO_DATE varchar(10), @SUPBUY_TYPE varchar(3), @DTI_TYPE varchar(3), @BRK_YN varchar(3), @SB_ISSUE_EXCEPT_YN varchar(1) | 정의 참조 `master.dbo.enc_index_char_sel_tc` · 하위 호출 `master.dbo.enc_index_char_sel_tc` · 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/openscrap/salespurchase/repository/OpenscrapSalesPurchaseMapper.kt#L103) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-342f6c3626121661) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 작성일자, 공급자 사업자번호, 공급자 회사명, 공급받는자 사업자번호, 공급받는자 회사명, 공급가액 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 서비스관리 > 오픈스크랩 > 매출/매입 조회의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 다운로드 중 오류가 발생했습니다. | 작성일자, 공급자 사업자번호, 공급자 회사명, 공급받는자 사업자번호, 공급받는자 회사명, 공급가액 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/OpenscrapRoutes.tsx#L16) · [SalesPurchasesListPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/SalesPurchasesListPage.tsx#L284) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/api/salesPurchasesApi.ts#L53) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/api/salesPurchasesApi.ts#L85) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/api/salesPurchasesApi.ts#L101) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 5개 중 개발 메타데이터 확인 5개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-5ec9ec1343e6d424) | Demo 메타데이터 5/5개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

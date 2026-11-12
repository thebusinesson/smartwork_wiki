# [연동 영업과 프로젝트 완료] 영업 관리 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

영업 관리에서 **영업대표 목록 조회** 결과를 확인한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 연동 영업과 프로젝트 완료 |
| 언제 사용하는가 | 영업구분 코드 조회, 영업경로 코드 조회, 영업상품 코드 조회, 업종 코드 조회, 영업대표 목록 조회 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 전체, 업체 조건, 업체명, 수주 예상월, 영업종료일, 우선순위 |
| 업무 흐름 | 영업구분 코드 조회, 영업경로 코드 조회, 영업상품 코드 조회, 업종 코드 조회, 영업대표 목록 조회 |
| 이 페이지의 역할 | 조회 · 영업대표 목록 조회 |
| 판단 결과·다음 업무 | [영업 관리 업체 등록](sales-management__new.md) · [영업 관리 상세](sales-management__by-id.md) · [영업 관리 업체 등록](sales-management__by-id__edit.md) |
| 다른 화면과의 구분 | 이 경로에서 볼 수 있는 조건·결과를 기준으로 사용한다. 독립 경로의 상세·등록은 관련 화면에 연결한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 영업 관리에서 **영업대표 목록 조회** 결과를 확인한다. |
| 메뉴·화면 경로 | 연동 협업 관리 > 연동 협업 관리 > 영업 관리 · `/hub-collab/sales-management` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [영업 관리 업체 등록](sales-management__new.md) · [영업 관리 상세](sales-management__by-id.md) · [영업 관리 업체 등록](sales-management__by-id__edit.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/hub-collab/sales-management` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 영업구분 코드 조회 | `/hub-collab/sales-management` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 영업경로 코드 조회 | `/hub-collab/sales-management` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 영업상품 코드 조회 | `/hub-collab/sales-management` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 업종 코드 조회 | `/hub-collab/sales-management` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 영업대표 목록 조회 | `/hub-collab/sales-management` `VIEW` | `includeRetired: Boolean` |
| 영업 목록 조회 | `/hub-collab/sales-management` `VIEW` | `SalesSearchRequest` `page`, `size`, `orderBy`, `companyCondition`, `companyName`, `expectedOrderMonthStart`, `expectedOrderMonthEnd`, `salesEndDateStart`, `salesEndDateEnd`, `priorities`, `salesGrades`, `salesStatuses`, `integrationStatuses`, `integrationMethods` |
| 영업 목록 다운로드 | `/hub-collab/sales-management` `EXCEL_DOWNLOAD` | `SalesSearchRequest` `page`, `size`, `orderBy`, `companyCondition`, `companyName`, `expectedOrderMonthStart`, `expectedOrderMonthEnd`, `salesEndDateStart`, `salesEndDateEnd`, `priorities`, `salesGrades`, `salesStatuses`, `integrationStatuses`, `integrationMethods` · `format: DownloadFormat` |
| 영업 목록 영업대표 원문 조회 | `/hub-collab/sales-management` / `UNMASK` | `id`, `field` |

코드에서 확인한 버튼·작업명은 **검색**, **영업 등록**, **다운로드**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **연동 협업 관리 > 연동 협업 관리 > 영업 관리**를 연다. `/hub-collab/sales-management`를 연다.
2. **전체**, **업체 조건**, **업체명**, **수주 예상월**, **영업종료일**, **우선순위**, **영업구분** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색**, **영업 등록**, **다운로드** 중 해당 버튼을 선택한다.
3. **영업대표 목록 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [영업 관리 업체 등록](sales-management__new.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 전체 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/SalesManagementPage.tsx#L112) |
| 업체 조건 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/SalesManagementPage.tsx#L133) |
| 업체명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `업체명` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/constants/salesManagement.ts#L85) |
| 수주 예상월 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/SalesManagementPage.tsx#L151) |
| 영업종료일 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/SalesManagementPage.tsx#L168) |
| 우선순위 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/SalesManagementPage.tsx#L185) |
| 영업구분 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/SalesManagementPage.tsx#L195) |
| 영업경로 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/SalesManagementPage.tsx#L201) |
| 영업상품 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/SalesManagementPage.tsx#L207) |
| 업종 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/SalesManagementPage.tsx#L213) |
| 영업대표 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/SalesManagementPage.tsx#L219) |
| 영업등급 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/SalesManagementPage.tsx#L225) |
| 영업상태 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/SalesManagementPage.tsx#L235) |
| 연동진행 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/SalesManagementPage.tsx#L245) |
| 연동방식 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/SalesManagementPage.tsx#L255) |
| 번호 | 출력 | 조회 응답 기준 | 화면 필드 `id` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/SalesTable.tsx#L57) |
| 수주예상월 | 출력 | 조회 응답 기준 | 화면 필드 `expectedOrderMonth` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/SalesTable.tsx#L71) |
| 사용시기 | 출력 | 조회 응답 기준 | 화면 필드 `usageTimeSales` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/SalesTable.tsx#L183) |
| 예상매출업체수 | 출력 | 조회 응답 기준 | 화면 필드 `expectedSalesCompanies` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/SalesTable.tsx#L192) |
| 예상매입업체수 | 출력 | 조회 응답 기준 | 화면 필드 `expectedPurchaseCompanies` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/SalesTable.tsx#L201) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 영업구분 코드 조회 | `GET /api/v1/sales/codes/categories` · `/hub-collab/sales-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/sales/SalesCodeController.kt#L112) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `code`, `title` | 직접 DB 호출이 연결된 경로는 현재 소스에서 미확인. 세부 저장소는 Controller와 Service 참조. |
| 영업경로 코드 조회 | `GET /api/v1/sales/codes/channels` · `/hub-collab/sales-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/sales/SalesCodeController.kt#L94) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `code`, `title` | `office.dbo.upBNS_BusinessRoute` |
| 영업상품 코드 조회 | `GET /api/v1/sales/codes/products` · `/hub-collab/sales-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/sales/SalesCodeController.kt#L75) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `code`, `title` | `office.dbo.upBNS_BusinessRoute` |
| 업종 코드 조회 | `GET /api/v1/sales/codes/industries` · `/hub-collab/sales-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/sales/SalesCodeController.kt#L103) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `code`, `title` | `office.dbo.upBNS_BusinessRoute` |
| 영업대표 목록 조회 | `GET /api/v1/sales/codes/representatives` · `/hub-collab/sales-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/sales/SalesCodeController.kt#L121) | `includeRetired: Boolean` → `success`, `data`, `error`, `swNo`, `name`, `leaveYn` | `office.dbo.DEPT_MANAGER`, `office.dbo.SAWON`, `office.dbo.DEPT_DETAIL` |
| 영업 목록 조회 | `GET /api/v1/sales` · `/hub-collab/sales-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/sales/SalesController.kt#L79) | `SalesSearchRequest` `page`, `size`, `orderBy`, `companyCondition`, `companyName`, `expectedOrderMonthStart`, `expectedOrderMonthEnd`, `salesEndDateStart`, `salesEndDateEnd`, `priorities`, `salesGrades`, `salesStatuses`, `integrationStatuses`, `integrationMethods` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `currentPage`, `size` | `smartwork.dbo.usp_sales_list_select` · 코드 연계 트랜잭션 |
| 영업 목록 다운로드 | `GET /api/v1/sales/download` · `/hub-collab/sales-management` `EXCEL_DOWNLOAD` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/sales/SalesController.kt#L116) | `SalesSearchRequest` `page`, `size`, `orderBy`, `companyCondition`, `companyName`, `expectedOrderMonthStart`, `expectedOrderMonthEnd`, `salesEndDateStart`, `salesEndDateEnd`, `priorities`, `salesGrades`, `salesStatuses`, `integrationStatuses`, `integrationMethods` · `format: DownloadFormat` → 파일 또는 오류 응답 | `smartwork.dbo.usp_sales_list_excel_select` |
| 영업 목록 영업대표 원문 조회 | `POST /api/v1/sales/{id}/sensitive-values/reveal` · `/hub-collab/sales-management` / `UNMASK` · [화면 컴포넌트](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/SalesTable.tsx#L116) · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/sales/SalesController.kt#L89) | `id`, `field` → 요청한 항목의 원문 응답 | 권한 검사 후 대상 값을 조회하고 감사 기록을 남긴다. |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `office.dbo.upBNS_BusinessRoute` | @cate01 varchar(15), @cate02 varchar(7), @flag varchar(5), @orderby varchar(10) = NULL | 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesCodeMapper.kt#L59) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-9f917ea22b3cc4fc) |
| `office.dbo.DEPT_MANAGER` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesCodeMapper.kt#L116) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-6bd350bbf4a76a9a) |
| `office.dbo.SAWON` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesCodeMapper.kt#L116) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3a9ea6e368df5cb3) |
| `office.dbo.DEPT_DETAIL` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesCodeMapper.kt#L116) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-f1473984f53ebe9a) |
| `smartwork.dbo.usp_sales_list_select` | @PAGE int, @PAGE_SIZE int, @ORDER_BY varchar(50) = NULL, @COMPANY_CONDITION varchar(20) = NULL, @COMPANY_NAME varchar(100) = NULL, @EXPECTED_ORDER_MONTH_START varchar(7) = NULL, @EXPECTED_ORDER_MONTH_END varchar(7) = NULL, @SALES_END_DATE_START varchar(10) = NULL, @SALES_END_DATE_END varchar(10) = NULL, @PRIORITIES varchar(50) = NULL, @SALES_GRADES varchar(20) = NULL, @SALES_STATUSES varchar(20) = NULL, @INTEGRATION_STATUSES varchar(50) = NULL, @INTEGRATION_METHODS varchar(100) = NULL, @SALES_CATEGORY varchar(10) = NULL, @SALES_CHANNEL varchar(10) = NULL, @SALES_PRODUCT varchar(10) = NULL, @INDUSTRY varchar(50) = NULL, @SALES_REP_SW_NO int = NULL | 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesMapper.kt#L76) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-aafa6b5c55d02205) |
| `smartwork.dbo.usp_sales_list_excel_select` | @ORDER_BY varchar(50) = NULL, @COMPANY_CONDITION varchar(20) = NULL, @COMPANY_NAME varchar(100) = NULL, @EXPECTED_ORDER_MONTH_START varchar(7) = NULL, @EXPECTED_ORDER_MONTH_END varchar(7) = NULL, @SALES_END_DATE_START varchar(10) = NULL, @SALES_END_DATE_END varchar(10) = NULL, @PRIORITIES varchar(50) = NULL, @SALES_GRADES varchar(20) = NULL, @SALES_STATUSES varchar(20) = NULL, @INTEGRATION_STATUSES varchar(50) = NULL, @INTEGRATION_METHODS varchar(100) = NULL, @SALES_CATEGORY varchar(10) = NULL, @SALES_CHANNEL varchar(10) = NULL, @SALES_PRODUCT varchar(10) = NULL, @INDUSTRY varchar(50) = NULL, @SALES_REP_SW_NO int = NULL | 정의 참조 `office.dbo.BUSINESS`, `office.dbo.BUSINESS_CONTRACT_HIS`, `office.dbo.BUSINESS_STEP`, `office.dbo.BUSINESS_STRATEGY`, `office.dbo.FUNCTION_CODE` 외 1개 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesMapper.kt#L128) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-73c87223fb20b12a) |
| `office.dbo.BUSINESS_STEP` | 개발 컬럼 메타데이터 확인 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesMapper.kt#L500) |
| `smartwork.dbo.usp_sw_log_access_event_insert` | @EVENT_TYPE varchar(30) IN, @STATUS varchar(20) IN, @USER_ID bigint IN, @MEMBER_ID nvarchar(50) IN, @USER_NAME nvarchar(100) IN, @DEPARTMENT_NAME nvarchar(100) IN, @PAGE_TITLE nvarchar(200) IN, @PATH nvarchar(500) IN, @MENU_PATH nvarchar(500) IN, @MENU_LABEL nvarchar(200) IN, @CATEGORY_NAME nvarchar(200) IN, @SUB_CATEGORY_NAME nvarchar(200) IN, @MENU_ORDER int IN, @IP_ADDRESS varchar(45) IN, @USER_AGENT nvarchar(1000) IN, @BROWSER varchar(100) IN, @OS varchar(100) IN, @REFERRER nvarchar(500) IN, @DETAIL nvarchar(1000) IN, @RESULT int OUT, @COUNTS_AS_VISIT bit IN | 원문 조회 또는 감사 흐름에서 호출 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/logmanagement/repository/LogManagementMapper.kt#L92) |

### 매퍼 호출 추가 확인

| DB 객체 | 호출 근거 | 개발 DB 확인 범위 |
| --- | --- | --- |
| [office.dbo.SSP_BNS_DIVISION_LIST](../../references/all-pages-demo.md#object-59b44da4cea2d1dc) | [findCategories](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesCodeMapper.kt#L77) | 개발 카탈로그 확인 |
| [office.dbo.upApp_BusinessSawonList](../../references/all-pages-demo.md#object-ac2a9723e4fad5c2) | [findRepresentatives](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesCodeMapper.kt#L87) | 개발 카탈로그 확인 |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 전체, 업체 조건, 업체명, 수주 예상월, 영업종료일, 우선순위 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 연동 협업 관리 > 연동 협업 관리 > 영업 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 영업 목록을 불러오는데 실패했습니다. | 전체, 업체 조건, 업체명, 수주 예상월, 영업종료일, 우선순위 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 영업 목록 다운로드에 실패했습니다. | 전체, 업체 조건, 업체명, 수주 예상월, 영업종료일, 우선순위 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 검색 결과가 없습니다. | 전체, 업체 조건, 업체명, 수주 예상월, 영업종료일, 우선순위 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/IntegrationRoutes.tsx#L82) · [SalesManagementPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/SalesManagementPage.tsx#L39) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/salesManagementApi.ts#L286) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/salesManagementApi.ts#L274) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/salesManagementApi.ts#L220) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/salesManagementApi.ts#L280) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/salesManagementApi.ts#L229) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/salesManagementApi.ts#L60) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/salesManagementApi.ts#L101) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 6개 중 개발 메타데이터 확인 6개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-fb66c846f23718d2) | Demo 메타데이터 10/10개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

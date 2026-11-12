# [고객·매출·연동과 외부 호출 지표] 허브업체 이용 현황 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

허브업체 이용 현황에서 **허브업체 이용 현황 목록 조회** 결과를 확인한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 고객·매출·연동과 외부 호출 지표 |
| 언제 사용하는가 | 허브업체 이용 현황 목록 조회, 허브업체 이용 현황 영업대표 옵션 조회, 허브업체 이용 현황 CSV 다운로드 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 영업대표, 전체, 허브업체명, 서비스 구분, 이용기간, 기간 |
| 업무 흐름 | 허브업체 이용 현황 목록 조회, 허브업체 이용 현황 영업대표 옵션 조회, 허브업체 이용 현황 CSV 다운로드 |
| 이 페이지의 역할 | 조회 · 허브업체 이용 현황 목록 조회 |
| 판단 결과·다음 업무 | [허브업체 이용 현황 상세](hub-company-usage__by-id.md) |
| 다른 화면과의 구분 | 이 경로에서 볼 수 있는 조건·결과를 기준으로 사용한다. 독립 경로의 상세·등록은 관련 화면에 연결한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 허브업체 이용 현황에서 **허브업체 이용 현황 목록 조회** 결과를 확인한다. |
| 메뉴·화면 경로 | 서비스 현황 > 통계 정보 > 허브업체 이용 현황 · `/statistics/hub-company-usage` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [허브업체 이용 현황 상세](hub-company-usage__by-id.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/statistics/hub-company-usage` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 허브업체 이용 현황 목록 조회 | `/statistics/hub-company-usage` `VIEW` | `HubCompanyUsageSearchRequest` `serviceType`, `salesRepId`, `hubCompanyAll`, `hubCompanyName`, `usageMonthAll`, `usageMonthStart`, `usageMonthEnd` |
| 허브업체 이용 현황 영업대표 옵션 조회 | `/statistics/hub-company-usage` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 허브업체 이용 현황 CSV 다운로드 | `/statistics/hub-company-usage` `EXCEL_DOWNLOAD` | `HubCompanyUsageSearchRequest` `serviceType`, `salesRepId`, `hubCompanyAll`, `hubCompanyName`, `usageMonthAll`, `usageMonthStart`, `usageMonthEnd` |
| 허브업체 이용 현황 영업대표 원문 조회 | `/statistics/hub-company-usage` / `UNMASK` | `hubId`, `field` |

코드에서 확인한 버튼·작업명은 **검색**, **다운로드**, **허브업체 이용 현황 다운로드**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **서비스 현황 > 통계 정보 > 허브업체 이용 현황**를 연다. `/statistics/hub-company-usage`를 연다.
2. **영업대표**, **전체**, **허브업체명**, **서비스 구분**, **이용기간** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색**, **다운로드**, **허브업체 이용 현황 다운로드** 중 해당 버튼을 선택한다.
3. **허브업체 이용 현황 목록 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [허브업체 이용 현황 상세](hub-company-usage__by-id.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 영업대표 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/HubCompanyUsagePage.tsx#L64) |
| 전체 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `0` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/HubCompanyUsagePage.tsx#L70) |
| 허브업체명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/HubCompanyUsagePage.tsx#L78) |
| 서비스 구분 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/HubCompanyUsagePage.tsx#L89) |
| 이용기간 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/HubCompanyUsagePage.tsx#L99) |
| 기간 | 출력 | 조회 응답 기준 | 화면 필드 `periodMonth` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/HubCompanyUsageTable.tsx#L247) |
| 업체수 | 출력 | 조회 응답 기준 | 화면 필드 `salesCompanyCount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/HubCompanyUsageTable.tsx#L123) |
| 전월대비 | 출력 | 조회 응답 기준 | 화면 필드 `salesCompanyDiff` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/HubCompanyUsageTable.tsx#L133) |
| 건수 | 출력 | 조회 응답 기준 | 화면 필드 `salesCount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/HubCompanyUsageTable.tsx#L143) |
| 매출 | 출력 | 조회 응답 기준 | 화면 필드 `sales-group` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/HubCompanyUsageTable.tsx#L211) |
| 매입 | 출력 | 조회 응답 기준 | 화면 필드 `purchase-group` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/HubCompanyUsageTable.tsx#L212) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 허브업체 이용 현황 목록 조회 | `GET /api/v1/service-status/usage/hub-companies/usage` · `/statistics/hub-company-usage` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/statistics/hubcompanyusage/HubCompanyUsageController.kt#L63) | `HubCompanyUsageSearchRequest` `serviceType`, `salesRepId`, `hubCompanyAll`, `hubCompanyName`, `usageMonthAll`, `usageMonthStart`, `usageMonthEnd` → `success`, `data`, `error`, `content`, `totalElements` | 코드 연계 트랜잭션 |
| 허브업체 이용 현황 영업대표 옵션 조회 | `GET /api/v1/service-status/usage/hub-companies/sales-representatives` · `/statistics/hub-company-usage` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/statistics/hubcompanyusage/HubCompanyUsageController.kt#L76) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `swNo`, `name`, `leaveYn` | `office.dbo.BUSINESS`, `office.dbo.SAWON`, `office.dbo.MNG_HUB`, `office.dbo.HUB_USAGE_DCT` |
| 허브업체 이용 현황 CSV 다운로드 | `GET /api/v1/service-status/usage/hub-companies/download` · `/statistics/hub-company-usage` `EXCEL_DOWNLOAD` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/statistics/hubcompanyusage/HubCompanyUsageController.kt#L124) | `HubCompanyUsageSearchRequest` `serviceType`, `salesRepId`, `hubCompanyAll`, `hubCompanyName`, `usageMonthAll`, `usageMonthStart`, `usageMonthEnd` → 파일 또는 오류 응답 | 코드 연계 트랜잭션 |
| 허브업체 이용 현황 영업대표 원문 조회 | `POST /api/v1/service-status/usage/hub-companies/{hubId}/sensitive-values/reveal` · `/statistics/hub-company-usage` / `UNMASK` · [화면 컴포넌트](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/HubCompanyUsageTable.tsx#L48) · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/statistics/hubcompanyusage/HubCompanyUsageController.kt#L99) | `hubId`, `field` → 요청한 항목의 원문 응답 | 권한 검사 후 대상 값을 조회하고 감사 기록을 남긴다. |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `office.dbo.BUSINESS` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/statistics/hubcompanyusage/repository/HubCompanyUsageMapper.kt#L152) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-1c6a832844bf01aa) |
| `office.dbo.SAWON` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/statistics/hubcompanyusage/repository/HubCompanyUsageMapper.kt#L152) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3a9ea6e368df5cb3) |
| `office.dbo.MNG_HUB` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/statistics/hubcompanyusage/repository/HubCompanyUsageMapper.kt#L152) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-bb97dfe4e2b8c3b3) |
| `office.dbo.HUB_USAGE_DCT` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/statistics/hubcompanyusage/repository/HubCompanyUsageMapper.kt#L152) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b7f9524a83438697) |
| `office.dbo.upHub_ViewHubMainInfo` | @hub_id int IN | 원문 조회 또는 감사 흐름에서 호출 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/statistics/hubcompanyusage/repository/HubCompanyUsageMapper.kt#L161) |
| `smartwork.dbo.usp_sw_log_access_event_insert` | @EVENT_TYPE varchar(30) IN, @STATUS varchar(20) IN, @USER_ID bigint IN, @MEMBER_ID nvarchar(50) IN, @USER_NAME nvarchar(100) IN, @DEPARTMENT_NAME nvarchar(100) IN, @PAGE_TITLE nvarchar(200) IN, @PATH nvarchar(500) IN, @MENU_PATH nvarchar(500) IN, @MENU_LABEL nvarchar(200) IN, @CATEGORY_NAME nvarchar(200) IN, @SUB_CATEGORY_NAME nvarchar(200) IN, @MENU_ORDER int IN, @IP_ADDRESS varchar(45) IN, @USER_AGENT nvarchar(1000) IN, @BROWSER varchar(100) IN, @OS varchar(100) IN, @REFERRER nvarchar(500) IN, @DETAIL nvarchar(1000) IN, @RESULT int OUT, @COUNTS_AS_VISIT bit IN | 원문 조회 또는 감사 흐름에서 호출 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/logmanagement/repository/LogManagementMapper.kt#L92) |

### 매퍼 호출 추가 확인

| DB 객체 | 호출 근거 | 개발 DB 확인 범위 |
| --- | --- | --- |
| [office.dbo.upHub_ResultsList](../../references/all-pages-demo.md#object-e0e62804d86039b7) | [selectDtiUsage](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/statistics/hubcompanyusage/repository/HubCompanyUsageMapper.kt#L77) | @bns_choice char(1) IN · @hub_choice char(1) IN · @leaderId int IN · @hub_name varchar(50) IN · @fromMonth varchar(10) IN · @toMonth varchar(10) IN |
| [office.dbo.upHub_DCTResultsList](../../references/all-pages-demo.md#object-a333f3c11cc4f514) | [selectDctUsage](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/statistics/hubcompanyusage/repository/HubCompanyUsageMapper.kt#L117) | @bns_choice char(1) IN · @hub_choice char(1) IN · @leaderId int IN · @hub_name varchar(50) IN · @fromMonth varchar(10) IN · @toMonth varchar(10) IN |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 영업대표, 전체, 허브업체명, 서비스 구분, 이용기간, 기간 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 서비스 현황 > 통계 정보 > 허브업체 이용 현황의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 영업대표 목록을 불러오지 못했습니다. | 영업대표, 전체, 허브업체명, 서비스 구분, 이용기간, 기간 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 데이터를 불러오는 중 오류가 발생했습니다. | 영업대표, 전체, 허브업체명, 서비스 구분, 이용기간, 기간 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 검색 결과가 없습니다. 조회 후 다운로드해 주세요. | 영업대표, 전체, 허브업체명, 서비스 구분, 이용기간, 기간 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 다운로드에 실패했습니다. | 영업대표, 전체, 허브업체명, 서비스 구분, 이용기간, 기간 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/StatisticsRoutes.tsx#L33) · [HubCompanyUsagePage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/HubCompanyUsagePage.tsx#L37) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/api/hubCompanyUsageApi.ts#L30) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/api/hubCompanyUsageApi.ts#L34) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/api/hubCompanyUsageApi.ts#L46) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 4개 중 개발 메타데이터 확인 4개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-9459f31fc5f6f7ec) | Demo 메타데이터 8/8개 확인 · Dev와 계약 차이 2개 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

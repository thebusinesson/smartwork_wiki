# [업체·비회원 예외와 SMS 수신거부] [업체]예외 처리 정보 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

[업체]예외 처리 정보에서 **예외 업체 목록 조회** 결과를 확인한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 업체·비회원 예외와 SMS 수신거부 |
| 언제 사용하는가 | 예외 업체 목록 조회 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 서비스 구분, 업체 조건, 전체, 사업자번호, 회사명, 사업자 번호 |
| 업무 흐름 | 예외 업체 목록 조회 |
| 이 페이지의 역할 | 조회 · 예외 업체 목록 조회 |
| 판단 결과·다음 업무 | [[업체]예외 처리 정보 등록](exception-vendor__new.md) · [[업체]예외 처리 정보 상세](exception-vendor__by-businessNumber.md) |
| 다른 화면과의 구분 | 이 경로에서 볼 수 있는 조건·결과를 기준으로 사용한다. 독립 경로의 상세·등록은 관련 화면에 연결한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | [업체]예외 처리 정보에서 **예외 업체 목록 조회** 결과를 확인한다. |
| 메뉴·화면 경로 | SB 고객관리 > 예외 관리 > [업체]예외 처리 정보 · `/exception-management/exception-vendor` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [[업체]예외 처리 정보 등록](exception-vendor__new.md) · [[업체]예외 처리 정보 상세](exception-vendor__by-businessNumber.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/exception-management/exception-vendor` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 예외 업체 목록 조회 | `/exception-management/exception-vendor` `VIEW` | `serviceType: String?` · `searchType: String?` · `keyword: String?` · `page: Int` · `size: Int` |
| 예외 업체 등록번호 원문 조회 | `/exception-management/exception-vendor` / `UNMASK` | `revealId`, `field` |
| 예외 업체 처리자 원문 조회 | `/exception-management/exception-vendor` / `UNMASK` | `businessNumber`, `field` |

코드에서 확인한 버튼·작업명은 **검색**, **예외 서비스 등록**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **SB 고객관리 > 예외 관리 > [업체]예외 처리 정보**를 연다. `/exception-management/exception-vendor`를 연다.
2. **서비스 구분**, **업체 조건**, **전체**, **사업자번호**, **회사명** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색**, **예외 서비스 등록** 중 해당 버튼을 선택한다.
3. **예외 업체 목록 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [[업체]예외 처리 정보 등록](exception-vendor__new.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 서비스 구분 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/exception/ExceptionVendorPage.tsx#L81) |
| 업체 조건 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/exception/ExceptionVendorPage.tsx#L93) |
| 전체 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `all` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/exception/ExceptionVendorPage.tsx#L101) |
| 사업자번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `사업자번호` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/exception/ExceptionVendorPage.tsx#L102) |
| 회사명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `회사명` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/exception/ExceptionVendorPage.tsx#L103) |
| 사업자 번호 | 출력 | 조회 응답 기준 | 화면 필드 `businessNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/exception/components/ExceptionVendorTable.tsx#L38) |
| 예외 처리 여부 | 출력 | 조회 응답 기준 | 화면 필드 `exceptionStatus` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/exception/components/ExceptionVendorTable.tsx#L65) |
| 처리자 | 출력 | 조회 응답 기준 | 화면 필드 `processor` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/exception/components/ExceptionVendorTable.tsx#L72) |
| 예외 처리 일시 | 출력 | 조회 응답 기준 | 화면 필드 `exceptionProcessDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/exception/components/ExceptionVendorTable.tsx#L88) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 예외 업체 목록 조회 | `GET /api/v1/customer/exception-companies` · `/exception-management/exception-vendor` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/customer/exception/ExceptionVendorController.kt#L77) | `serviceType: String?` · `searchType: String?` · `keyword: String?` · `page: Int` · `size: Int` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `currentPage`, `size` | `smartwork.dbo.usp_except_company_select`, `office.dbo.MNG_COMPANY_EXCEPT` |
| 예외 업체 등록번호 원문 조회 | `POST /api/v1/customer/exception-companies/records/{revealId}/sensitive-values/reveal` · `/exception-management/exception-vendor` / `UNMASK` · [화면 컴포넌트](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/exception/components/ExceptionVendorTable.tsx#L43) · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/customer/exception/ExceptionVendorController.kt#L128) | `revealId`, `field` → 요청한 항목의 원문 응답 | 권한 검사 후 대상 값을 조회하고 감사 기록을 남긴다. |
| 예외 업체 처리자 원문 조회 | `POST /api/v1/customer/exception-companies/{businessNumber}/sensitive-values/reveal` · `/exception-management/exception-vendor` / `UNMASK` · [화면 컴포넌트](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/exception/components/ExceptionVendorTable.tsx#L77) · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/customer/exception/ExceptionVendorController.kt#L103) | `businessNumber`, `field` → 요청한 항목의 원문 응답 | 권한 검사 후 대상 값을 조회하고 감사 기록을 남긴다. |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.usp_except_company_select` | @ServiceType varchar(30), @SearchType char(1), @Keyword varchar(400), @PageNum int, @PageSize int | 정의 참조 `SmartBill3.dbo.COMPANY`, `office.dbo.MNG_COMPANY_EXCEPT`, `office.dbo.SAWON` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/exception/repository/ExceptCompanyMapper.kt#L47) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-7b37b0fef1b20bac) |
| `office.dbo.MNG_COMPANY_EXCEPT` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/exception/repository/ExceptCompanyMapper.kt#L120) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3d8c0e9716c73ec8) |
| `smartwork.dbo.usp_sw_log_access_event_insert` | @EVENT_TYPE varchar(30) IN, @STATUS varchar(20) IN, @USER_ID bigint IN, @MEMBER_ID nvarchar(50) IN, @USER_NAME nvarchar(100) IN, @DEPARTMENT_NAME nvarchar(100) IN, @PAGE_TITLE nvarchar(200) IN, @PATH nvarchar(500) IN, @MENU_PATH nvarchar(500) IN, @MENU_LABEL nvarchar(200) IN, @CATEGORY_NAME nvarchar(200) IN, @SUB_CATEGORY_NAME nvarchar(200) IN, @MENU_ORDER int IN, @IP_ADDRESS varchar(45) IN, @USER_AGENT nvarchar(1000) IN, @BROWSER varchar(100) IN, @OS varchar(100) IN, @REFERRER nvarchar(500) IN, @DETAIL nvarchar(1000) IN, @RESULT int OUT, @COUNTS_AS_VISIT bit IN | 원문 조회 또는 감사 흐름에서 호출 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/logmanagement/repository/LogManagementMapper.kt#L92) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 서비스 구분, 업체 조건, 전체, 사업자번호, 회사명, 사업자 번호 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 고객관리 > 예외 관리 > [업체]예외 처리 정보의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 데이터를 불러오는데 실패했습니다. | 서비스 구분, 업체 조건, 전체, 사업자번호, 회사명, 사업자 번호 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 검색 결과가 없습니다. | 서비스 구분, 업체 조건, 전체, 사업자번호, 회사명, 사업자 번호 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/CustomerRoutes.tsx#L51) · [ExceptionVendorPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/exception/ExceptionVendorPage.tsx#L42) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/exception/api/exceptionVendorApi.ts#L131) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 2개 중 개발 메타데이터 확인 2개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-6c8342d6a68c57c8) | Demo 메타데이터 3/3개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

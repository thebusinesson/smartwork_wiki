# [서비스 도입·제휴 문의와 제한] 서비스 도입 문의 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

서비스 도입 문의에서 **서비스 도입 문의 목록** 결과를 확인한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 서비스 도입·제휴 문의와 제한 |
| 언제 사용하는가 | 서비스 도입 문의 목록, 서비스 구분 코드 목록, 서비스 도입 문의 검색 선택지, 서비스 도입 문의 검색결과 엑셀 다운로드, 블랙리스트 등록 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 서비스 구분, 전체, 회사명, 접수경로, 영업대표, 기간 설정 |
| 업무 흐름 | 서비스 도입 문의 목록, 서비스 구분 코드 목록, 서비스 도입 문의 검색 선택지, 서비스 도입 문의 검색결과 엑셀 다운로드, 블랙리스트 등록 |
| 이 페이지의 역할 | 조회 · 서비스 도입 문의 목록 |
| 판단 결과·다음 업무 | [서비스 도입 문의 등록](service-inquiry__new.md) · [서비스 도입 문의 상세](service-inquiry__by-id.md) |
| 다른 화면과의 구분 | 이 경로에서 볼 수 있는 조건·결과를 기준으로 사용한다. 독립 경로의 상세·등록은 관련 화면에 연결한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 확인 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/customersupport/components/ServiceInquiryTable.tsx#L179) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 서비스 도입 문의에서 **서비스 도입 문의 목록** 결과를 확인한다. |
| 메뉴·화면 경로 | 고객지원 > 고객 문의 관리 > 서비스 도입 문의 · `/customer-support/service-inquiry` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [서비스 도입 문의 등록](service-inquiry__new.md) · [서비스 도입 문의 상세](service-inquiry__by-id.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/customer-support/service-inquiry` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 서비스 도입 문의 목록 | `/customer-support/service-inquiry` `VIEW` | `ServiceInquirySearchRequest` `serviceType`, `companyName`, `receiptPath`, `salesLeaderId`, `allPeriod`, `fromMonth`, `toMonth`, `page`, `size` |
| 서비스 구분 코드 목록 | `/customer-support/service-inquiry` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 서비스 도입 문의 검색 선택지 | `/customer-support/service-inquiry` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 서비스 도입 문의 검색결과 엑셀 다운로드 | `/customer-support/service-inquiry` `EXCEL_DOWNLOAD` | `ServiceInquirySearchRequest` `serviceType`, `companyName`, `receiptPath`, `salesLeaderId`, `allPeriod`, `fromMonth`, `toMonth`, `page`, `size` |
| 블랙리스트 등록 | `/customer-support/service-inquiry` `PROCESS` | `id: Long` |
| 서비스 도입 문의 민감정보 원문 조회 | `/customer-support/service-inquiry` / `UNMASK` | `id`, `field` |

코드에서 확인한 버튼·작업명은 **선택지 다시 불러오기**, **검색**, **등록**, **다운로드**, **추가**, **확인**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **고객지원 > 고객 문의 관리 > 서비스 도입 문의**를 연다. `/customer-support/service-inquiry`를 연다.
2. **서비스 구분**, **전체**, **회사명**, **접수경로**, **영업대표**, **기간 설정**, **월별** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색**, **등록**, **다운로드**, **확인** 중 해당 버튼을 선택한다.
3. **서비스 도입 문의 목록** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [서비스 도입 문의 등록](service-inquiry__new.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 서비스 구분 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/customersupport/ServiceInquiryListPage.tsx#L238) |
| 전체 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/customersupport/ServiceInquiryListPage.tsx#L296) |
| 회사명 | 입력 또는 선택 | 길이·개수 최대 80 · API 기본값 null | API 요청 `companyName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/customersupport/ServiceInquiryListPage.tsx#L254) |
| 회사명 입력 | 입력 또는 선택 | 길이·개수 최대 80 · API 기본값 null | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/customersupport/ServiceInquiryListPage.tsx#L255) |
| 접수경로 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/customersupport/ServiceInquiryListPage.tsx#L260) |
| 영업대표 | 입력 또는 선택 | API 기본값 null | API 요청 `salesLeaderId` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/customersupport/ServiceInquiryListPage.tsx#L277) |
| 기간 설정 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/customersupport/ServiceInquiryListPage.tsx#L290) |
| 월별 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `MONTH` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/customersupport/ServiceInquiryListPage.tsx#L297) |
| 등록일 | 출력 | 조회 응답 기준 | 화면 필드 `registeredAt` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/customersupport/components/ServiceInquiryTable.tsx#L83) |
| 접수 경로 | 출력 | 조회 응답 기준 | 화면 필드 `receiptPathLabel` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/customersupport/components/ServiceInquiryTable.tsx#L84) |
| 담당자 | 출력 | 조회 응답 기준 | 화면 필드 `managerName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/customersupport/components/ServiceInquiryTable.tsx#L103) |
| 담당자명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `MANAGER_NAME` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/customersupport/components/ServiceInquiryTable.tsx#L107) |
| 답변 받을 E-mail | 출력 | 조회 응답 기준 | 화면 필드 `email` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/customersupport/components/ServiceInquiryTable.tsx#L114) |
| 이메일 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `EMAIL` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/customersupport/components/ServiceInquiryTable.tsx#L122) |
| 연락처 | 출력 | 조회 응답 기준 | 화면 필드 `phone` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/customersupport/components/ServiceInquiryTable.tsx#L130) |
| 블랙리스트 | 출력 | 조회 응답 기준 | 화면 필드 `blacklisted` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/customersupport/components/ServiceInquiryTable.tsx#L142) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 서비스 도입 문의 목록 | `GET /api/v1/customer-support/service-inquiries` · `/customer-support/service-inquiry` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/support/customersupport/serviceinquiry/ServiceInquiryController.kt#L89) | `ServiceInquirySearchRequest` `serviceType`, `companyName`, `receiptPath`, `salesLeaderId`, `allPeriod`, `fromMonth`, `toMonth`, `page`, `size` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `currentPage`, `size` | `office.dbo.SSP_SERVICE_INTRODUCTION`, `smartwork.dbo.usp_service_inquiry_blacklist_select` · 코드 연계 트랜잭션 |
| 서비스 구분 코드 목록 | `GET /api/v1/customer-support/service-inquiries/service-types` · `/customer-support/service-inquiry` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/support/customersupport/serviceinquiry/ServiceInquiryController.kt#L243) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `code`, `label` | `office.dbo.SSP_SB_SVC_ASK_CODE` |
| 서비스 도입 문의 검색 선택지 | `GET /api/v1/customer-support/service-inquiries/search-options` · `/customer-support/service-inquiry` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/support/customersupport/serviceinquiry/ServiceInquiryController.kt#L252) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `receiptPaths`, `salesLeaders` | `office.dbo.DEPT_MANAGER`, `office.dbo.SAWON`, `office.dbo.DEPT_DETAIL` |
| 서비스 도입 문의 검색결과 엑셀 다운로드 | `GET /api/v1/customer-support/service-inquiries/download` · `/customer-support/service-inquiry` `EXCEL_DOWNLOAD` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/support/customersupport/serviceinquiry/ServiceInquiryController.kt#L114) | `ServiceInquirySearchRequest` `serviceType`, `companyName`, `receiptPath`, `salesLeaderId`, `allPeriod`, `fromMonth`, `toMonth`, `page`, `size` → 파일 또는 오류 응답 | `office.dbo.SSP_SERVICE_INTRODUCTION_XLS` |
| 블랙리스트 등록 | `POST /api/v1/customer-support/service-inquiries/{id}/blacklist` · `/customer-support/service-inquiry` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/support/customersupport/serviceinquiry/ServiceInquiryController.kt#L262) | `id: Long` → `success`, `data`, `error` | `office.dbo.upSW_SAVE_SB_BLACKLIST`, `office.dbo.SSP_SERVICE_INTRODUCTION_DETAIL`, `smartwork.dbo.usp_service_inquiry_blacklist_select` · 정의에서 확인한 쓰기 `office.dbo.SB_BLACKLIST` · 코드 연계 트랜잭션 |
| 서비스 도입 문의 민감정보 원문 조회 | `POST /api/v1/customer-support/service-inquiries/{id}/sensitive-values/reveal` · `/customer-support/service-inquiry` / `UNMASK` · [화면 컴포넌트](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/customersupport/components/ServiceInquiryTable.tsx#L132) · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/support/customersupport/serviceinquiry/ServiceInquiryController.kt#L200) | `id`, `field` → 요청한 항목의 원문 응답 | 권한 검사 후 대상 값을 조회하고 감사 기록을 남긴다. |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `office.dbo.SSP_SERVICE_INTRODUCTION` | @GUBUN varchar(10), @SEARCHTEXT varchar(80), @CLASS_CODE varchar(10), @SERVICE_LEADER varchar(10), @DATEALL varchar(10), @FROMMONTH varchar(10), @TOMONTH varchar(10) | 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/customersupport/serviceinquiry/repository/ServiceInquiryMapper.kt#L64) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-d4c4c07f8a6c93b4) |
| `smartwork.dbo.usp_service_inquiry_blacklist_select` | @IDX int = NULL | 정의 참조 `office.dbo.SB_BLACKLIST`, `SB_COMMON.dbo.SB_Svc_Ask` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/customersupport/serviceinquiry/repository/ServiceInquiryMapper.kt#L158) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-7e96740dba18d5b6) |
| `office.dbo.SSP_SB_SVC_ASK_CODE` | 컬럼·결과 계약은 매퍼 참조 | 정의 참조 `SB_COMMON.dbo.sb_Svc_Ask_Code` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/customersupport/serviceinquiry/repository/ServiceInquiryMapper.kt#L143) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-14a191f0280599f6) |
| `office.dbo.DEPT_MANAGER` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesCodeMapper.kt#L116) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-6bd350bbf4a76a9a) |
| `office.dbo.SAWON` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesCodeMapper.kt#L116) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3a9ea6e368df5cb3) |
| `office.dbo.DEPT_DETAIL` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesCodeMapper.kt#L116) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-f1473984f53ebe9a) |
| `office.dbo.SSP_SERVICE_INTRODUCTION_XLS` | @GUBUN varchar(10), @SEARCHTEXT varchar(80), @CLASS_CODE varchar(10), @SERVICE_LEADER varchar(10), @DATEALL varchar(10), @FROMMONTH varchar(10), @TOMONTH varchar(10) | 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/customersupport/serviceinquiry/repository/ServiceInquiryMapper.kt#L90) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-c08883d40e3d5834) |
| `office.dbo.upSW_SAVE_SB_BLACKLIST` | @IDX int, @SW_NO int, @GUBUN nvarchar(50) | 정의 참조 `office.dbo.SB_BLACKLIST`, `SB_COMMON.dbo.SB_Svc_Ask` · 정적 쓰기 `office.dbo.SB_BLACKLIST` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/customersupport/serviceinquiry/repository/ServiceInquiryMapper.kt#L170) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-a123eaa70ffb2254) |
| `office.dbo.SSP_SERVICE_INTRODUCTION_DETAIL` | @IDX int | 정의 참조 `SB_COMMON.dbo.SB_Svc_Ask`, `SB_COMMON.dbo.sb_Svc_Ask_Code` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/customersupport/serviceinquiry/repository/ServiceInquiryMapper.kt#L129) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-0450a1949ac0c530) |
| `smartwork.dbo.usp_sw_log_access_event_insert` | @EVENT_TYPE varchar(30) IN, @STATUS varchar(20) IN, @USER_ID bigint IN, @MEMBER_ID nvarchar(50) IN, @USER_NAME nvarchar(100) IN, @DEPARTMENT_NAME nvarchar(100) IN, @PAGE_TITLE nvarchar(200) IN, @PATH nvarchar(500) IN, @MENU_PATH nvarchar(500) IN, @MENU_LABEL nvarchar(200) IN, @CATEGORY_NAME nvarchar(200) IN, @SUB_CATEGORY_NAME nvarchar(200) IN, @MENU_ORDER int IN, @IP_ADDRESS varchar(45) IN, @USER_AGENT nvarchar(1000) IN, @BROWSER varchar(100) IN, @OS varchar(100) IN, @REFERRER nvarchar(500) IN, @DETAIL nvarchar(1000) IN, @RESULT int OUT, @COUNTS_AS_VISIT bit IN | 원문 조회 또는 감사 흐름에서 호출 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/logmanagement/repository/LogManagementMapper.kt#L92) |

### 매퍼 호출 추가 확인

| DB 객체 | 호출 근거 | 개발 DB 확인 범위 |
| --- | --- | --- |
| [office.dbo.upApp_BusinessSawonList](../../references/all-pages-demo.md#object-ac2a9723e4fad5c2) | [findRepresentatives](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesCodeMapper.kt#L87) | 개발 카탈로그 확인 |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 서비스 구분, 전체, 회사명, 접수경로, 영업대표, 기간 설정 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 고객지원 > 고객 문의 관리 > 서비스 도입 문의의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 월별 기간을 설정해주세요. | 서비스 구분, 전체, 회사명, 접수경로, 영업대표, 기간 설정 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 다운로드할 검색 결과가 없습니다. | 서비스 구분, 전체, 회사명, 접수경로, 영업대표, 기간 설정 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 다운로드 중 오류가 발생했습니다. | 서비스 구분, 전체, 회사명, 접수경로, 영업대표, 기간 설정 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 블랙리스트 추가 중 오류가 발생했습니다. | 서비스 구분, 전체, 회사명, 접수경로, 영업대표, 기간 설정 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/CustomerSupportRoutes.tsx#L99) · [ServiceInquiryListPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/customersupport/ServiceInquiryListPage.tsx#L67) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/customersupport/api/serviceInquiryApi.ts#L51) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/customersupport/api/serviceInquiryApi.ts#L64) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/customersupport/api/serviceInquiryApi.ts#L68) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/customersupport/api/serviceInquiryApi.ts#L95) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/customersupport/api/serviceInquiryApi.ts#L72) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 9개 중 개발 메타데이터 확인 9개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-74fc2edf69c8750f) | Demo 메타데이터 11/11개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

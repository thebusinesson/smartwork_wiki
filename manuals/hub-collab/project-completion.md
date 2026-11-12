# [연동 영업과 프로젝트 완료] 프로젝트 완료 관리 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

영업관리 BNS_SALES_STATUS='E' 영업건만 대상.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 연동 영업과 프로젝트 완료 |
| 언제 사용하는가 | 프로젝트 완료 관리 목록 조회, 영업대표 목록 조회, 전체 사원 목록 조회 (진행내역 담당자 콤보용), 프로젝트 완료 관리 목록 다운로드 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 계약기간, 업체 조건, 영업대표, 전체, 담당PM, 연동진행 |
| 업무 흐름 | 프로젝트 완료 관리 목록 조회, 영업대표 목록 조회, 전체 사원 목록 조회 (진행내역 담당자 콤보용), 프로젝트 완료 관리 목록 다운로드 |
| 이 페이지의 역할 | 조회 · 프로젝트 완료 관리 목록 조회 |
| 판단 결과·다음 업무 | [영업 관리 상세](sales-management__by-id.md) |
| 다른 화면과의 구분 | 이 경로에서 볼 수 있는 조건·결과를 기준으로 사용한다. 독립 경로의 상세·등록은 관련 화면에 연결한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 확인 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/projectCompletion/components/BillingRegistrationDialog.tsx#L29) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 영업관리 BNS_SALES_STATUS='E' 영업건만 대상. |
| 메뉴·화면 경로 | 연동 협업 관리 > 연동 협업 관리 > 프로젝트 완료 관리 · `/hub-collab/project-completion` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [영업 관리 상세](sales-management__by-id.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/hub-collab/project-completion` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 프로젝트 완료 관리 목록 조회 | `/hub-collab/project-completion` `VIEW` | `ProjectCompletionSearchRequest` `page`, `size`, `orderBy`, `contractPeriodStart`, `contractPeriodEnd`, `vendorCondition`, `vendorKeyword`, `salesRep`, `pmInCharge`, `integrationProgress`, `integrationMethod`, `projectCompletion` |
| 영업대표 목록 조회 | `/hub-collab/sales-management` `VIEW` | `includeRetired: Boolean` |
| 전체 사원 목록 조회 (진행내역 담당자 콤보용) | `/hub-collab/sales-management` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 프로젝트 완료 관리 목록 다운로드 | `/hub-collab/project-completion` `EXCEL_DOWNLOAD` | `ProjectCompletionSearchRequest` `page`, `size`, `orderBy`, `contractPeriodStart`, `contractPeriodEnd`, `vendorCondition`, `vendorKeyword`, `salesRep`, `pmInCharge`, `integrationProgress`, `integrationMethod`, `projectCompletion` · `format: DownloadFormat` |
| 프로젝트 완료 관리 직원 이름 원문 조회 | `/hub-collab/project-completion` / `UNMASK` | `id`, `field` |

코드에서 확인한 버튼·작업명은 **검색**, **다운로드**, **프로젝트 완료 관리 다운로드**, **연동 요청**, **빌링등록 요청**, **확인**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **연동 협업 관리 > 연동 협업 관리 > 프로젝트 완료 관리**를 연다. 화면 경로는 `/hub-collab/project-completion`이다.
2. **계약기간**, **업체 조건**, **영업대표**, **담당PM**, **연동진행**, **연동방식** 중 필요한 조건을 지정하고 **검색**을 누른다.
3. 목록에서 대상 업체와 프로젝트 상태를 확인한다. 영업 정보를 더 확인하려면 [영업 관리 상세](sales-management__by-id.md)를 참고한다.
4. 조회 결과를 반출하려면 **다운로드**를 누른 뒤 **프로젝트 완료 목록 다운로드** 창에서 반출 사유를 입력하고 **확인**을 누른다. 사유 등록이 성공하면 엑셀 다운로드가 시작된다.

**연동 요청**과 **빌링등록 요청**은 화면 코드에 있으나 대응 서버 경로와 완료 결과는 미확인이다. 운영 처리 전에 기술 담당에게 지원 여부를 확인한다. 호출 근거는 [서버 경로 대조가 필요한 호출](#서버-경로-대조가-필요한-호출)에서 확인할 수 있다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 계약기간 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/projectCompletion/ProjectCompletionPage.tsx#L146) |
| 업체 조건 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/projectCompletion/ProjectCompletionPage.tsx#L160) |
| 영업대표 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/projectCompletion/ProjectCompletionPage.tsx#L188) |
| 전체 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/projectCompletion/ProjectCompletionPage.tsx#L204) |
| 담당PM | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/projectCompletion/ProjectCompletionPage.tsx#L199) |
| 연동진행 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/projectCompletion/ProjectCompletionPage.tsx#L210) |
| 연동방식 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/projectCompletion/ProjectCompletionPage.tsx#L223) |
| 프로젝트 완료 (빌링등록) | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/projectCompletion/ProjectCompletionPage.tsx#L236) |
| 업체명 | 입력 또는 선택 | API 기본값 null | API 요청 `vendorCondition` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/projectCompletion/components/ProjectCompletionTable.tsx#L94) |
| 사업자번호 | 출력 | 조회 응답 기준 | 화면 필드 `businessNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/projectCompletion/components/ProjectCompletionTable.tsx#L101) |
| 완료요청일 | 출력 | 조회 응답 기준 | 화면 필드 `completionRequestedAt` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/projectCompletion/components/ProjectCompletionTable.tsx#L146) |
| 프로젝트 완료 | 입력 또는 선택 | API 기본값 null | API 요청 `projectCompletion` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/projectCompletion/components/ProjectCompletionTable.tsx#L155) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 프로젝트 완료 관리 목록 조회 | `GET /api/v1/hub-collab/project-completion` · `/hub-collab/project-completion` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/projectcompletion/ProjectCompletionController.kt#L85) | `ProjectCompletionSearchRequest` `page`, `size`, `orderBy`, `contractPeriodStart`, `contractPeriodEnd`, `vendorCondition`, `vendorKeyword`, `salesRep`, `pmInCharge`, `integrationProgress`, `integrationMethod`, `projectCompletion` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `number`, `size`, `first`, `last` | `smartwork.dbo.usp_project_completion_list_select` · 코드 연계 트랜잭션 |
| 영업대표 목록 조회 | `GET /api/v1/sales/codes/representatives` · `/hub-collab/sales-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/sales/SalesCodeController.kt#L121) | `includeRetired: Boolean` → `success`, `data`, `error`, `swNo`, `name`, `leaveYn` | `office.dbo.DEPT_MANAGER`, `office.dbo.SAWON`, `office.dbo.DEPT_DETAIL` |
| 전체 사원 목록 조회 (진행내역 담당자 콤보용) | `GET /api/v1/sales/codes/employees` · `/hub-collab/sales-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/sales/SalesCodeController.kt#L133) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `swNo`, `name` | 직접 DB 호출이 연결된 경로는 현재 소스에서 미확인. 세부 저장소는 Controller와 Service 참조. |
| 프로젝트 완료 관리 목록 다운로드 | `GET /api/v1/hub-collab/project-completion/download` · `/hub-collab/project-completion` `EXCEL_DOWNLOAD` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/projectcompletion/ProjectCompletionController.kt#L125) | `ProjectCompletionSearchRequest` `page`, `size`, `orderBy`, `contractPeriodStart`, `contractPeriodEnd`, `vendorCondition`, `vendorKeyword`, `salesRep`, `pmInCharge`, `integrationProgress`, `integrationMethod`, `projectCompletion` · `format: DownloadFormat` → 파일 또는 오류 응답 | `smartwork.dbo.usp_project_completion_list_select` |
| 프로젝트 완료 관리 직원 이름 원문 조회 | `POST /api/v1/hub-collab/project-completion/{id}/sensitive-values/reveal` · `/hub-collab/project-completion` / `UNMASK` · [화면 컴포넌트](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/projectCompletion/components/ProjectCompletionTable.tsx#L60) · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/projectcompletion/ProjectCompletionController.kt#L95) | `id`, `field` → 요청한 항목의 원문 응답 | 권한 검사 후 대상 값을 조회하고 감사 기록을 남긴다. |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.usp_project_completion_list_select` | @PAGE int, @PAGE_SIZE int, @ORDER_BY varchar(50) = NULL, @CONTRACT_FROM_MONTH varchar(7) = NULL, @CONTRACT_TO_MONTH varchar(7) = NULL, @VENDOR_CONDITION varchar(20) = NULL, @VENDOR_KEYWORD varchar(100) = NULL, @SALES_REP_SW_NO int = NULL, @PM_SW_NO int = NULL, @INTEGRATION_PROGRESS varchar(50) = NULL, @INTEGRATION_METHODS varchar(100) = NULL, @PROJECT_COMPLETION varchar(5) = NULL | 정의 참조 `office.dbo.BUSINESS`, `office.dbo.BUSINESS_CONTRACT_HIS`, `SB_BILL.dbo.CHARGEPOLICY_SPECIAL_MAPPING`, `SmartBill3.dbo.COMPANY`, `office.dbo.SAWON` 외 1개 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/projectcompletion/repository/ProjectCompletionMapper.kt#L56) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-cd1d2c1361dddc24) |
| `office.dbo.DEPT_MANAGER` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesCodeMapper.kt#L116) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-6bd350bbf4a76a9a) |
| `office.dbo.SAWON` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesCodeMapper.kt#L116) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3a9ea6e368df5cb3) |
| `office.dbo.DEPT_DETAIL` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesCodeMapper.kt#L116) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-f1473984f53ebe9a) |
| `office.dbo.BUSINESS` | 개발 컬럼 메타데이터 확인 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/projectcompletion/repository/ProjectCompletionMapper.kt#L68) |
| `smartwork.dbo.usp_sw_log_access_event_insert` | @EVENT_TYPE varchar(30) IN, @STATUS varchar(20) IN, @USER_ID bigint IN, @MEMBER_ID nvarchar(50) IN, @USER_NAME nvarchar(100) IN, @DEPARTMENT_NAME nvarchar(100) IN, @PAGE_TITLE nvarchar(200) IN, @PATH nvarchar(500) IN, @MENU_PATH nvarchar(500) IN, @MENU_LABEL nvarchar(200) IN, @CATEGORY_NAME nvarchar(200) IN, @SUB_CATEGORY_NAME nvarchar(200) IN, @MENU_ORDER int IN, @IP_ADDRESS varchar(45) IN, @USER_AGENT nvarchar(1000) IN, @BROWSER varchar(100) IN, @OS varchar(100) IN, @REFERRER nvarchar(500) IN, @DETAIL nvarchar(1000) IN, @RESULT int OUT, @COUNTS_AS_VISIT bit IN | 원문 조회 또는 감사 흐름에서 호출 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/logmanagement/repository/LogManagementMapper.kt#L92) |

### 서버 경로 대조가 필요한 호출

| 프런트엔드 경로 | 근거 | 상태 |
| --- | --- | --- |
| POST /hub-collab/project-completion/integration-request | [프런트엔드 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/hubCollabProjectCompletionApi.ts#L62) | 같은 메서드와 경로의 현재 Controller 연결 미확인. 실제 활성 조건과 서버 적용은 기술 담당이 확인한다. |
| POST /hub-collab/project-completion/billing-registration | [프런트엔드 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/hubCollabProjectCompletionApi.ts#L55) | 같은 메서드와 경로의 현재 Controller 연결 미확인. 실제 활성 조건과 서버 적용은 기술 담당이 확인한다. |

### 매퍼 호출 추가 확인

| DB 객체 | 호출 근거 | 개발 DB 확인 범위 |
| --- | --- | --- |
| [office.dbo.upApp_BusinessSawonList](../../references/all-pages-demo.md#object-ac2a9723e4fad5c2) | [findRepresentatives](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesCodeMapper.kt#L87) | 개발 카탈로그 확인 |
| [office.dbo.upApp_SawonList](../../references/all-pages-demo.md#object-a7f6826ec54e8008) | [findEmployees](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesCodeMapper.kt#L125) | 개발 카탈로그 확인 |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 계약기간, 업체 조건, 영업대표, 전체, 담당PM, 연동진행 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 연동 협업 관리 > 연동 협업 관리 > 프로젝트 완료 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 전체 선택에 실패했습니다. | 계약기간, 업체 조건, 영업대표, 전체, 담당PM, 연동진행 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 다운로드할 데이터가 없습니다. | 계약기간, 업체 조건, 영업대표, 전체, 담당PM, 연동진행 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 파일 다운로드에 실패했습니다. | 계약기간, 업체 조건, 영업대표, 전체, 담당PM, 연동진행 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 연동 요청할 프로젝트를 선택해주세요. | 계약기간, 업체 조건, 영업대표, 전체, 담당PM, 연동진행 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/IntegrationRoutes.tsx#L86) · [ProjectCompletionPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/projectCompletion/ProjectCompletionPage.tsx#L57) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/hubCollabProjectCompletionApi.ts#L48) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/hubCollabProjectCompletionApi.ts#L103) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/hubCollabProjectCompletionApi.ts#L116) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/hubCollabProjectCompletionApi.ts#L94) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 4개 중 개발 메타데이터 확인 4개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-ab114a72fc89f0bf) | Demo 메타데이터 8/8개 확인 · Dev와 계약 차이 1개 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

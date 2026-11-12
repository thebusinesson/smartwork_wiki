# [운영자 계정·조직·권한 그룹] 조직 관리 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

마스킹된 목록 대신 원문 이름·아이디로 검색해 일치하는 임직원 번호만 반환한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 운영자 계정·조직·권한 그룹 |
| 언제 사용하는가 | 조직 트리 조회, 조직 상세 조회, 조직 배치용 임직원 조회, 조직 배치용 임직원 이름·아이디 검색, 조직 등록 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 상위 부서 명, 부서 명, 부서 코드, 부서원 수, 이름, 전체 |
| 업무 흐름 | 조직 트리 조회, 조직 상세 조회, 조직 배치용 임직원 조회, 조직 배치용 임직원 이름·아이디 검색, 조직 등록 |
| 이 페이지의 역할 | 조회·관리 · 조직 배치용 임직원 이름·아이디 검색 |
| 판단 결과·다음 업무 | 현재 화면에서 결과를 확인한다. |
| 다른 화면과의 구분 | 같은 경로에서 열리는 조회·팝업은 이 문서에서 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 교체 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/organization/OrganizationManagementPage.tsx#L492) |
| 등록 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/organization/OrganizationManagementPage.tsx#L504) |
| 확인 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/organization/OrganizationManagementPage.tsx#L537) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 마스킹된 목록 대신 원문 이름·아이디로 검색해 일치하는 임직원 번호만 반환한다. |
| 메뉴·화면 경로 | SmartWork 관리 > 조직 관리 · `/settings/organization-management` |
| 화면 유형·담당 | 조회·관리 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | 현재 화면에서 결과를 확인한다. |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/settings/organization-management` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 조직 트리 조회 | `/settings/organization-management` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 조직 상세 조회 | `/settings/organization-management` `VIEW` | `nodeType: OrganizationNodeType` · `id: Int` |
| 조직 배치용 임직원 조회 | `/settings/organization-management` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 조직 배치용 임직원 이름·아이디 검색 | `/settings/organization-management` `VIEW` | `keyword: String` |
| 조직 등록 | `/settings/organization-management` `PROCESS` | `OrganizationCreateRequest` `parentType`, `parentId`, `departmentName` · 서버 필수 `departmentName` |
| 조직 수정 | `/settings/organization-management` `PROCESS` | `nodeType: OrganizationNodeType` · `id: Int` · `OrganizationUpdateRequest` `departmentName` · 서버 필수 `departmentName` |
| 조직 삭제 | `/settings/organization-management` `DELETE` | `nodeType: OrganizationNodeType` · `id: Int` |
| 임직원 소속팀 변경 | `/settings/organization-management` `PROCESS` | `id: Long` · `OrganizationMemberDepartmentRequest` `departmentId`, `expectedDepartmentId` |
| 조직장 지정 및 교체 | `/settings/organization-management` `PROCESS` | `nodeType: OrganizationNodeType` · `id: Int` · `OrganizationManagerRequest` `memberId`, `approvedReplacementManagerIds` |
| 조직 배치용 임직원 원문 조회 | `/settings/organization-management` / `UNMASK` | `id`, `field` |

코드에서 확인한 버튼·작업명은 **선택한 조직 상세**, **수정**, **최상위 조직 추가**, **다시 조회**, **임직원 목록**, **임직원 소속 필터**, **다시 불러오기**, **교체**, **등록**, **확인**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **SmartWork 관리 > 조직 관리**를 연다. `/settings/organization-management`를 연다.
2. **상위 부서 명**, **부서 명**, **부서 코드**, **부서원 수**, **이름**, **전체**, **소속팀 미배정** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **다시 조회**, **임직원 검색**, **등록**, **확인** 중 해당 버튼을 선택한다.
3. **조직 배치용 임직원 이름·아이디 검색** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 상위 부서 명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/organization/OrganizationManagementPage.tsx#L335) |
| 부서 명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/organization/OrganizationManagementPage.tsx#L348) |
| 부서 코드 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/organization/OrganizationManagementPage.tsx#L370) |
| 부서원 수 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/organization/OrganizationManagementPage.tsx#L382) |
| 이름 | 출력 | 조회 응답 기준 | API 응답 `userName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/organization/components/OrganizationTree.tsx#L93) |
| 이름, 아이디, 직급, 조직 검색 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/organization/components/OrganizationMemberList.tsx#L72) |
| 전체 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/organization/components/OrganizationMemberList.tsx#L78) |
| 소속팀 미배정 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/organization/components/OrganizationMemberList.tsx#L78) |
| 등록 위치 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/organization/components/OrganizationForm.tsx#L35) |
| 입력 | 출력 | 조회 응답 기준 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/organization/components/OrganizationForm.tsx#L54) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 조직 트리 조회 | `GET /api/v1/settings/organizations/tree` · `/settings/organization-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/settings/organization/OrganizationController.kt#L41) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `nodeType`, `id`, `departmentName`, `departmentCode`, `memberCount`, `parentType`, `parentId`, `canAddChild`, `canDelete` | `office.dbo.GROUP_MANAGER`, `office.dbo.PART_MANAGER`, `office.dbo.PART_INFO`, `office.dbo.DEPT_MANAGER`, `office.dbo.DEPT` 외 3개 · 코드 연계 트랜잭션 |
| 조직 상세 조회 | `GET /api/v1/settings/organizations/{nodeType}/{id}` · `/settings/organization-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/settings/organization/OrganizationController.kt#L48) | `nodeType: OrganizationNodeType` · `id: Int` → `success`, `data`, `error`, `nodeType`, `id`, `departmentName`, `departmentCode`, `memberCount`, `parentType`, `parentId`, `parentDepartmentName`, `canAddChild` | `office.dbo.GROUP_MANAGER`, `office.dbo.PART_MANAGER`, `office.dbo.PART_INFO`, `office.dbo.DEPT_MANAGER`, `office.dbo.DEPT` 외 3개 |
| 조직 배치용 임직원 조회 | `GET /api/v1/settings/organizations/members` · `/settings/organization-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/settings/organization/OrganizationPlacementController.kt#L49) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `id`, `userName`, `userId`, `positionDescription`, `titleDescription`, `departmentId`, `departmentName`, `organizationAssignments`, `canAssign` | `office.dbo.SAWON`, `office.dbo.DEPT_DETAIL`, `office.dbo.DEPT`, `office.dbo.GROUP_MANAGER`, `office.dbo.GROUP_INFO` 외 3개 · 코드 연계 트랜잭션 |
| 조직 배치용 임직원 이름·아이디 검색 | `GET /api/v1/settings/organizations/members/matches` · `/settings/organization-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/settings/organization/OrganizationPlacementController.kt#L75) | `keyword: String` → `success`, `data`, `error` | 직접 DB 호출이 연결된 경로는 현재 소스에서 미확인. 세부 저장소는 Controller와 Service 참조. |
| 조직 등록 | `POST /api/v1/settings/organizations` · `/settings/organization-management` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/settings/organization/OrganizationController.kt#L60) | `OrganizationCreateRequest` `parentType`, `parentId`, `departmentName` · 서버 필수 `departmentName` → `success`, `data`, `error` | `office.dbo.GROUP_MANAGER`, `office.dbo.PART_MANAGER`, `office.dbo.PART_INFO`, `office.dbo.DEPT_MANAGER`, `office.dbo.DEPT` 외 3개 · 코드 연계 트랜잭션 |
| 조직 수정 | `PUT /api/v1/settings/organizations/{nodeType}/{id}` · `/settings/organization-management` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/settings/organization/OrganizationController.kt#L72) | `nodeType: OrganizationNodeType` · `id: Int` · `OrganizationUpdateRequest` `departmentName` · 서버 필수 `departmentName` → `success`, `data`, `error` | `office.dbo.GROUP_MANAGER`, `office.dbo.PART_MANAGER`, `office.dbo.PART_INFO`, `office.dbo.DEPT_MANAGER`, `office.dbo.DEPT` 외 3개 · 코드 연계 트랜잭션 |
| 조직 삭제 | `DELETE /api/v1/settings/organizations/{nodeType}/{id}` · `/settings/organization-management` `DELETE` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/settings/organization/OrganizationController.kt#L88) | `nodeType: OrganizationNodeType` · `id: Int` → `success`, `data`, `error`, `canDelete` | `office.dbo.GROUP_MANAGER`, `office.dbo.PART_MANAGER`, `office.dbo.PART_INFO`, `office.dbo.DEPT_MANAGER`, `office.dbo.DEPT` 외 4개 · 정의에서 확인한 쓰기 `office.dbo.SW_MENU` · 코드 연계 트랜잭션 |
| 임직원 소속팀 변경 | `PUT /api/v1/settings/organizations/members/{id}/department` · `/settings/organization-management` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/settings/organization/OrganizationPlacementController.kt#L108) | `id: Long` · `OrganizationMemberDepartmentRequest` `departmentId`, `expectedDepartmentId` → `success`, `data`, `error` | `office.dbo.DEPT_DETAIL`, `office.dbo.SW_MENU`, `office.dbo.SAWON`, `office.dbo.GROUP_INFO`, `office.dbo.PART_INFO` 외 1개 · 정의에서 확인한 쓰기 `office.dbo.SW_MENU` · 코드 연계 트랜잭션 |
| 조직장 지정 및 교체 | `PUT /api/v1/settings/organizations/{nodeType}/{id}/manager` · `/settings/organization-management` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/settings/organization/OrganizationPlacementController.kt#L119) | `nodeType: OrganizationNodeType` · `id: Int` · `OrganizationManagerRequest` `memberId`, `approvedReplacementManagerIds` → `success`, `data`, `error` | `office.dbo.GROUP_MANAGER`, `office.dbo.SAWON`, `office.dbo.PART_MANAGER`, `office.dbo.DEPT_MANAGER`, `office.dbo.GROUP_INFO` 외 2개 · 코드 연계 트랜잭션 |
| 조직 배치용 임직원 원문 조회 | `POST /api/v1/settings/organizations/members/{id}/sensitive-values/reveal` · `/settings/organization-management` / `UNMASK` · [화면 컴포넌트](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/organization/components/OrganizationTree.tsx#L91) · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/settings/organization/OrganizationPlacementController.kt#L81) | `id`, `field` → 요청한 항목의 원문 응답 | 권한 검사 후 대상 값을 조회하고 감사 기록을 남긴다. |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `office.dbo.GROUP_MANAGER` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/organization/repository/OrganizationMapper.kt#L59) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-74bd137c16c3e256) |
| `office.dbo.PART_MANAGER` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/organization/repository/OrganizationMapper.kt#L59) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-272a73b3400fa0e4) |
| `office.dbo.PART_INFO` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/organization/repository/OrganizationMapper.kt#L59) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-55373887260bf623) |
| `office.dbo.DEPT_MANAGER` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/organization/repository/OrganizationMapper.kt#L59) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-6bd350bbf4a76a9a) |
| `office.dbo.DEPT` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/organization/repository/OrganizationMapper.kt#L59) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-cac428eda173d0f6) |
| `office.dbo.DEPT_DETAIL` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/organization/repository/OrganizationMapper.kt#L59) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-f1473984f53ebe9a) |
| `office.dbo.SAWON` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/organization/repository/OrganizationMapper.kt#L59) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3a9ea6e368df5cb3) |
| `office.dbo.GROUP_INFO` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/organization/repository/OrganizationMapper.kt#L59) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-f03382fc93536aac) |
| `office.dbo.SW_MENU` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL DELETE FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/organization/repository/OrganizationMapper.kt#L173) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-04b9d6afa210256e) |
| `smartwork.dbo.usp_sw_log_access_event_insert` | @EVENT_TYPE varchar(30) IN, @STATUS varchar(20) IN, @USER_ID bigint IN, @MEMBER_ID nvarchar(50) IN, @USER_NAME nvarchar(100) IN, @DEPARTMENT_NAME nvarchar(100) IN, @PAGE_TITLE nvarchar(200) IN, @PATH nvarchar(500) IN, @MENU_PATH nvarchar(500) IN, @MENU_LABEL nvarchar(200) IN, @CATEGORY_NAME nvarchar(200) IN, @SUB_CATEGORY_NAME nvarchar(200) IN, @MENU_ORDER int IN, @IP_ADDRESS varchar(45) IN, @USER_AGENT nvarchar(1000) IN, @BROWSER varchar(100) IN, @OS varchar(100) IN, @REFERRER nvarchar(500) IN, @DETAIL nvarchar(1000) IN, @RESULT int OUT, @COUNTS_AS_VISIT bit IN | 원문 조회 또는 감사 흐름에서 호출 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/logmanagement/repository/LogManagementMapper.kt#L92) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 상위 부서 명, 부서 명, 부서 코드, 부서원 수, 이름, 전체 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SmartWork 관리 > 조직 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 저장은 완료되었지만 최신 정보를 불러오지 못했습니다. 다시 조회해주세요. | 상위 부서 명, 부서 명, 부서 코드, 부서원 수, 이름, 전체 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 조직 배치를 저장하지 못했습니다. | 상위 부서 명, 부서 명, 부서 코드, 부서원 수, 이름, 전체 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/SettingsRoutes.tsx#L30) · [OrganizationManagementPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/organization/OrganizationManagementPage.tsx#L68) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/organization/api/organizationManagementApi.ts#L34) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/organization/api/organizationManagementApi.ts#L42) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/organization/api/organizationManagementApi.ts#L19) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/organization/api/organizationManagementApi.ts#L23) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/organization/api/organizationManagementApi.ts#L49) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/organization/api/organizationManagementApi.ts#L58) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/organization/api/organizationManagementApi.ts#L66) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/organization/api/organizationManagementApi.ts#L26) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 9개 중 개발 메타데이터 확인 9개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-56dfe568224e2740) | Demo 메타데이터 10/10개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

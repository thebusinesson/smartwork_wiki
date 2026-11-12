# [운영자 계정·조직·권한 그룹] 권한 관리 상세 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

선택한 권한 그룹의 이름·소속 사용자·메뉴별 권한을 조회한다. 처리 권한이 있는 운영자는 같은 화면에서 수정 모드로 전환할 수 있다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 운영자 계정·조직·권한 그룹 |
| 언제 사용하는가 | 기존 권한 그룹의 구성원을 확인하거나 메뉴별 권한을 변경할 때 사용한다. |
| 주요 대상·데이터 | 권한 그룹명, 권한 그룹 사용자, 권한 설정, 부서 명, 사용자명, 직원 명 |
| 업무 흐름 | 권한 그룹 상세 조회 → 수정 전환 → 변경 내용 확인 → 저장 |
| 이 페이지의 역할 | 상세 조회 · 같은 경로에서 권한 그룹 수정 |
| 판단 결과·다음 업무 | [권한 관리](permissions.md) |
| 다른 화면과의 구분 | 상세 조회와 수정은 같은 경로에서 진행한다. 신규 등록은 별도 경로다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 메뉴 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/permissions/components/PermissionTable.tsx#L321) |
| 권한 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/permissions/components/PermissionTable.tsx#L322) |
| 분류 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/permissions/components/PermissionTable.tsx#L325) |
| 메뉴명 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/permissions/components/PermissionTable.tsx#L326) |
| 표시할 권한 메뉴가 없습니다. | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/permissions/components/PermissionTable.tsx#L341) |
| 추가 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/permissions/components/UserAddModal.tsx#L205) |
| 확인 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/permissions/PermissionGroupDetailPage.tsx#L338) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 선택한 권한 그룹의 이름·소속 사용자·메뉴별 권한을 조회한다. 처리 권한이 있는 운영자는 같은 화면에서 수정 모드로 전환할 수 있다. |
| 메뉴·화면 경로 | SmartWork 관리 > 권한 관리 · `/settings/permissions/:id` · 경로 변수 `id` |
| 화면 유형·담당 | 상세 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [권한 관리](permissions.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/settings/permissions` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `id` |
| 권한 그룹 상세 조회 | `/settings/permissions` `VIEW` | `groupId: Long` |
| 권한 그룹 사용자 검색 | `/settings/permissions` `VIEW` | `PermissionGroupUserSearchRequest` `departmentName`, `searchKeyword`, `page`, `size` |
| 현재 사용자 부트스트랩 조회 | 인증·계정 상태 및 보안 설정 확인 | 추가 입력은 Controller 서명 참조 |
| 권한 그룹 옵션 조회 | `/settings/account-management` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 권한 그룹 수정 | `/settings/permissions` `PROCESS` | `groupId: Long` · `PermissionGroupUpdateRequest` `permissionSchemaVersion`, `groupName`, `userIds`, `menuPermissions` |

코드에서 확인한 버튼·작업명은 **권한 가이드**, **닫기**, **수정**, **목록**, **저장**, **추가**, **삭제**, **전체 펼치기**, **전체 접기**, **불러오기**, **초기화**, **더보기**, **확인**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. 권한 관리 목록에서 그룹을 열어 **권한 그룹명**, **권한 그룹 사용자**, **권한 설정**을 확인한다.
2. 변경이 필요한 경우 **수정**을 선택한다. 이 버튼은 처리 권한이 있는 운영자에게 표시된다.
3. 그룹명·사용자·메뉴 권한을 변경하고 **저장**을 누른다. 확인창에서 대상 그룹과 변경 내용을 확인한다.
4. 저장한 설정을 상세에서 확인한다. **목록**을 누르면 권한 그룹 목록으로 돌아간다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `id` |
| 권한 그룹명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/permissions/components/PermissionGroupFormSection.tsx#L61) |
| 권한 그룹 사용자 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/permissions/components/PermissionGroupFormSection.tsx#L82) |
| 권한 설정 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/permissions/components/PermissionGroupFormSection.tsx#L130) |
| 권한 그룹 선택 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/permissions/components/PermissionSourceLoader.tsx#L44) |
| 부서 명 | 입력 또는 선택 | API 기본값 null | API 요청 `departmentName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/permissions/components/UserAddModal.tsx#L144) |
| 사용자명 | 입력 또는 선택 | API 기본값 null | API 요청 `userName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/permissions/components/UserAddModal.tsx#L145) |
| 직원 명 | 출력 | 조회 응답 기준 | 화면 필드 `userInfo` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/permissions/components/UserAddModal.tsx#L159) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 권한 그룹 상세 조회 | `GET /api/v1/settings/permission-groups/{groupId}` · `/settings/permissions` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/settings/permissions/PermissionGroupController.kt#L81) | `groupId: Long` → `success`, `data`, `error`, `id`, `groupName`, `users`, `menuPermissions`, `registrationDate`, `registrant`, `registrantEmail` | `smartwork.dbo.usp_sw_permission_group_detail_select` |
| 권한 그룹 사용자 검색 | `GET /api/v1/settings/permission-groups/users` · `/settings/permissions` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/settings/permissions/PermissionGroupController.kt#L155) | `PermissionGroupUserSearchRequest` `departmentName`, `searchKeyword`, `page`, `size` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `currentPage`, `size` | `smartwork.dbo.usp_sw_permission_group_users_select` |
| 현재 사용자 부트스트랩 조회 | `GET /api/v1/me/bootstrap` · 인증·계정 상태 및 보안 설정 확인 · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/identity/MeController.kt#L36) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `permissionSchemaVersion`, `user`, `groups`, `menuPermissions`, `authzVersion`, `superAdmin` | 직접 DB 호출이 연결된 경로는 현재 소스에서 미확인. 세부 저장소는 Controller와 Service 참조. |
| 권한 그룹 옵션 조회 | `GET /api/v1/settings/permission-groups/options` · `/settings/account-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/settings/permissions/PermissionGroupController.kt#L75) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `id`, `groupName` | `smartwork.dbo.sw_permission_group` |
| 권한 그룹 수정 | `PUT /api/v1/settings/permission-groups/{groupId}` · `/settings/permissions` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/settings/permissions/PermissionGroupController.kt#L99) | `groupId: Long` · `PermissionGroupUpdateRequest` `permissionSchemaVersion`, `groupName`, `userIds`, `menuPermissions` → `success`, `data`, `error`, `message` | `smartwork.dbo.usp_sw_permission_group_update`, `smartwork.dbo.usp_sw_permission_group_detail_select` · 정의에서 확인한 쓰기 `smartwork.dbo.sw_permission_group`, `smartwork.dbo.sw_permission_group_user`, `smartwork.dbo.sw_permission_group_menu_permission` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.usp_sw_permission_group_list_select` | @GROUP_NAME nvarchar(20) = NULL, @REGISTRANT_NAME nvarchar(100) = NULL, @USER_NAME nvarchar(100) = NULL, @PAGE int = 1, @PAGE_SIZE int = 10 | 정의 참조 `office.dbo.SAWON`, `smartwork.dbo.sw_permission_group`, `smartwork.dbo.sw_permission_group_user` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/permissions/repository/PermissionGroupMapper.kt#L44) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-fa2bea67985b79ce) |
| `smartwork.dbo.usp_sw_permission_group_detail_select` | @GROUP_ID bigint, @RESULT_TYPE varchar(20) | 정의 참조 `office.dbo.DEPT`, `office.dbo.DEPT_DETAIL`, `office.dbo.SAWON`, `smartwork.dbo.sw_permission_group`, `smartwork.dbo.sw_permission_group_menu_permission` 외 1개 · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/permissions/repository/PermissionGroupMapper.kt#L116) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-f07bb0ba7916f3e4) |
| `smartwork.dbo.usp_sw_permission_group_users_select` | @DEPARTMENT_NAME nvarchar(100) = NULL, @SEARCH_KEYWORD nvarchar(100) = NULL, @PAGE int = 1, @PAGE_SIZE int = 20 | 정의 참조 `office.dbo.DEPT`, `office.dbo.DEPT_DETAIL`, `office.dbo.SAWON` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/permissions/repository/PermissionGroupMapper.kt#L129) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-693fb06ae0ee65d3) |
| `smartwork.dbo.sw_permission_group` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/permissions/repository/PermissionGroupMapper.kt#L55) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-7e8619e24b7beced) |
| `smartwork.dbo.usp_sw_permission_group_create` | @GROUP_NAME nvarchar(20), @CREATED_BY_SW_NO bigint, @CREATED_BY_SID nvarchar(100), @USER_IDS_JSON nvarchar(max), @MENU_PERMISSIONS_JSON nvarchar(max), @GROUP_ID bigint OUT, @RESULT int OUT | 정의 참조 `smartwork.dbo.sw_permission_group`, `smartwork.dbo.sw_permission_group_menu_permission`, `smartwork.dbo.sw_permission_group_user` · 정적 쓰기 `smartwork.dbo.sw_permission_group`, `smartwork.dbo.sw_permission_group_user`, `smartwork.dbo.sw_permission_group_menu_permission` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/permissions/repository/PermissionGroupMapper.kt#L145) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-5c795a1f4c8555b6) |
| `smartwork.dbo.usp_sw_permission_group_update` | @GROUP_ID bigint, @GROUP_NAME nvarchar(20), @UPDATED_BY_SW_NO bigint, @USER_IDS_JSON nvarchar(max), @MENU_PERMISSIONS_JSON nvarchar(max), @RESULT int OUT | 정의 참조 `smartwork.dbo.sw_permission_group`, `smartwork.dbo.sw_permission_group_menu_permission`, `smartwork.dbo.sw_permission_group_user` · 정적 쓰기 `smartwork.dbo.sw_permission_group`, `smartwork.dbo.sw_permission_group_user`, `smartwork.dbo.sw_permission_group_menu_permission` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/permissions/repository/PermissionGroupMapper.kt#L160) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3414a1b15e1a4799) |
| `smartwork.dbo.usp_sw_permission_group_delete` | @GROUP_ID bigint, @RESULT int OUT | 정의 참조 `smartwork.dbo.sw_permission_group`, `smartwork.dbo.sw_permission_group_menu_permission`, `smartwork.dbo.sw_permission_group_user` · 정적 쓰기 `smartwork.dbo.sw_permission_group`, `smartwork.dbo.sw_permission_group_menu_permission` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/permissions/repository/PermissionGroupMapper.kt#L171) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-02b922c90e2a92a8) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 권한 그룹명, 권한 그룹 사용자, 권한 설정, 부서 명, 사용자명, 직원 명 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SmartWork 관리 > 권한 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 삭제할 사용자를 선택해주세요. | 권한 그룹명, 권한 그룹 사용자, 권한 설정, 부서 명, 사용자명, 직원 명 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 권한 그룹 수정 중 오류가 발생했습니다. | 권한 그룹명, 권한 그룹 사용자, 권한 설정, 부서 명, 사용자명, 직원 명 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/SettingsRoutes.tsx#L33) · [PermissionGroupDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/permissions/PermissionGroupDetailPage.tsx#L34) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/permissions/api/permissionManagementApi.ts#L83) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/permissions/api/permissionManagementApi.ts#L95) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/permissions/api/permissionManagementApi.ts#L170) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/permissions/api/permissionManagementApi.ts#L188) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/permissions/api/permissionManagementApi.ts#L52) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/permissions/api/permissionManagementApi.ts#L109) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/permissions/api/permissionManagementApi.ts#L126) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/permissions/api/permissionManagementApi.ts#L142) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 7개 중 개발 메타데이터 확인 7개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-386cdb1663e96784) | Demo 메타데이터 7/7개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

# [운영자 계정·조직·권한 그룹] 권한 관리 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

권한 그룹 목록을 검색 조건과 페이지 기준으로 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 운영자 계정·조직·권한 그룹 |
| 언제 사용하는가 | 현재 사용자 부트스트랩 조회, 권한 그룹 목록 조회, 권한 그룹 삭제 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 전체, 권한 그룹 명, 등록자 명, 사용자 명, 권한 그룹, 사용자 수 |
| 업무 흐름 | 현재 사용자 부트스트랩 조회, 권한 그룹 목록 조회, 권한 그룹 삭제 |
| 이 페이지의 역할 | 조회·관리 · 권한 그룹 목록 조회 |
| 판단 결과·다음 업무 | [권한 관리 등록](permissions__new.md) · [권한 관리 상세](permissions__by-id.md) |
| 다른 화면과의 구분 | 이 경로에서 볼 수 있는 조건·결과를 기준으로 사용한다. 독립 경로의 상세·등록은 관련 화면에 연결한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 확인 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/permissions/PermissionManagementPage.tsx#L341) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 권한 그룹 목록을 검색 조건과 페이지 기준으로 조회한다. |
| 메뉴·화면 경로 | SmartWork 관리 > 권한 관리 · `/settings/permissions` |
| 화면 유형·담당 | 조회·관리 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [권한 관리 등록](permissions__new.md) · [권한 관리 상세](permissions__by-id.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/settings/permissions` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 현재 사용자 부트스트랩 조회 | 인증·계정 상태 및 보안 설정 확인 | 추가 입력은 Controller 서명 참조 |
| 권한 그룹 목록 조회 | `/settings/permissions` `VIEW` | `PermissionGroupSearchRequest` `groupName`, `registrantName`, `userName`, `page`, `size` |
| 권한 그룹 삭제 | `/settings/permissions` `DELETE` | `groupId: Long` |
| 권한 그룹 등록자 원문 조회 | `/settings/permissions` / `UNMASK` | `groupId`, `field` |

코드에서 확인한 버튼·작업명은 **검색**, **권한 그룹 복제**, **권한 그룹 생성**, **삭제**, **확인**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **SmartWork 관리 > 권한 관리**를 연다. `/settings/permissions`를 연다.
2. **전체**, **권한 그룹 명**, **등록자 명**, **사용자 명** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색**, **확인** 중 해당 버튼을 선택한다.
3. **권한 그룹 목록 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [권한 관리 등록](permissions__new.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 전체 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `all` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/permissions/PermissionManagementPage.tsx#L46) |
| 권한 그룹 명 | 입력 또는 선택 | API 기본값 null | API 요청 `groupName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/permissions/PermissionManagementPage.tsx#L47) |
| 등록자 명 | 입력 또는 선택 | API 기본값 null | API 요청 `registrantName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/permissions/PermissionManagementPage.tsx#L48) |
| 사용자 명 | 입력 또는 선택 | API 기본값 null | API 요청 `userName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/permissions/PermissionManagementPage.tsx#L49) |
| 권한 그룹 | 입력 또는 선택 | API 기본값 null | API 요청 `groupName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/permissions/components/PermissionGroupTable.tsx#L70) |
| 사용자 수 | 출력 | 조회 응답 기준 | 화면 필드 `userCount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/permissions/components/PermissionGroupTable.tsx#L81) |
| 등록일자 | 출력 | 조회 응답 기준 | 화면 필드 `registrationDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/permissions/components/PermissionGroupTable.tsx#L86) |
| 등록자 | 출력 | 조회 응답 기준 | 화면 필드 `registrant` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/permissions/components/PermissionGroupTable.tsx#L89) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 현재 사용자 부트스트랩 조회 | `GET /api/v1/me/bootstrap` · 인증·계정 상태 및 보안 설정 확인 · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/identity/MeController.kt#L36) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `permissionSchemaVersion`, `user`, `groups`, `menuPermissions`, `authzVersion`, `superAdmin` | 직접 DB 호출이 연결된 경로는 현재 소스에서 미확인. 세부 저장소는 Controller와 Service 참조. |
| 권한 그룹 목록 조회 | `GET /api/v1/settings/permission-groups` · `/settings/permissions` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/settings/permissions/PermissionGroupController.kt#L67) | `PermissionGroupSearchRequest` `groupName`, `registrantName`, `userName`, `page`, `size` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `currentPage`, `size` | `smartwork.dbo.usp_sw_permission_group_list_select` · 코드 연계 트랜잭션 |
| 권한 그룹 삭제 | `DELETE /api/v1/settings/permission-groups/{groupId}` · `/settings/permissions` `DELETE` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/settings/permissions/PermissionGroupController.kt#L110) | `groupId: Long` → `success`, `data`, `error`, `message`, `canDelete` | `smartwork.dbo.usp_sw_permission_group_delete` · 정의에서 확인한 쓰기 `smartwork.dbo.sw_permission_group`, `smartwork.dbo.sw_permission_group_menu_permission` · 코드 연계 트랜잭션 |
| 권한 그룹 등록자 원문 조회 | `POST /api/v1/settings/permission-groups/{groupId}/sensitive-values/reveal` · `/settings/permissions` / `UNMASK` · [화면 컴포넌트](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/permissions/components/PermissionGroupTable.tsx#L39) · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/settings/permissions/PermissionGroupController.kt#L119) | `groupId`, `field` → 요청한 항목의 원문 응답 | 권한 검사 후 대상 값을 조회하고 감사 기록을 남긴다. |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.usp_sw_permission_group_list_select` | @GROUP_NAME nvarchar(20) = NULL, @REGISTRANT_NAME nvarchar(100) = NULL, @USER_NAME nvarchar(100) = NULL, @PAGE int = 1, @PAGE_SIZE int = 10 | 정의 참조 `office.dbo.SAWON`, `smartwork.dbo.sw_permission_group`, `smartwork.dbo.sw_permission_group_user` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/permissions/repository/PermissionGroupMapper.kt#L44) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-fa2bea67985b79ce) |
| `smartwork.dbo.usp_sw_permission_group_delete` | @GROUP_ID bigint, @RESULT int OUT | 정의 참조 `smartwork.dbo.sw_permission_group`, `smartwork.dbo.sw_permission_group_menu_permission`, `smartwork.dbo.sw_permission_group_user` · 정적 쓰기 `smartwork.dbo.sw_permission_group`, `smartwork.dbo.sw_permission_group_menu_permission` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/permissions/repository/PermissionGroupMapper.kt#L171) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-02b922c90e2a92a8) |
| `smartwork.dbo.usp_sw_permission_group_detail_select` | @GROUP_ID bigint IN, @RESULT_TYPE varchar(20) IN | 원문 조회 또는 감사 흐름에서 호출 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/permissions/repository/PermissionGroupMapper.kt#L116) |
| `smartwork.dbo.usp_sw_log_access_event_insert` | @EVENT_TYPE varchar(30) IN, @STATUS varchar(20) IN, @USER_ID bigint IN, @MEMBER_ID nvarchar(50) IN, @USER_NAME nvarchar(100) IN, @DEPARTMENT_NAME nvarchar(100) IN, @PAGE_TITLE nvarchar(200) IN, @PATH nvarchar(500) IN, @MENU_PATH nvarchar(500) IN, @MENU_LABEL nvarchar(200) IN, @CATEGORY_NAME nvarchar(200) IN, @SUB_CATEGORY_NAME nvarchar(200) IN, @MENU_ORDER int IN, @IP_ADDRESS varchar(45) IN, @USER_AGENT nvarchar(1000) IN, @BROWSER varchar(100) IN, @OS varchar(100) IN, @REFERRER nvarchar(500) IN, @DETAIL nvarchar(1000) IN, @RESULT int OUT, @COUNTS_AS_VISIT bit IN | 원문 조회 또는 감사 흐름에서 호출 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/logmanagement/repository/LogManagementMapper.kt#L92) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 전체, 권한 그룹 명, 등록자 명, 사용자 명, 권한 그룹, 사용자 수 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SmartWork 관리 > 권한 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 권한 그룹을 삭제할 권한이 없습니다. | 전체, 권한 그룹 명, 등록자 명, 사용자 명, 권한 그룹, 사용자 수 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 삭제할 권한 그룹을 선택해주세요. | 전체, 권한 그룹 명, 등록자 명, 사용자 명, 권한 그룹, 사용자 수 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 권한 그룹 삭제에 실패했습니다. | 전체, 권한 그룹 명, 등록자 명, 사용자 명, 권한 그룹, 사용자 수 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 권한 그룹 삭제 중 오류가 발생했습니다. | 전체, 권한 그룹 명, 등록자 명, 사용자 명, 권한 그룹, 사용자 수 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/SettingsRoutes.tsx#L31) · [PermissionManagementPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/permissions/PermissionManagementPage.tsx#L58) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/permissions/api/permissionManagementApi.ts#L188) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/permissions/api/permissionManagementApi.ts#L83) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/permissions/api/permissionManagementApi.ts#L142) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 2개 중 개발 메타데이터 확인 2개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-1084d316052b392a) | Demo 메타데이터 4/4개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

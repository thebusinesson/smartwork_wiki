# [운영자 계정·조직·권한 그룹] 계정 관리 등록 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

새 SmartWork 운영자 계정을 만들고 조직과 권한 그룹의 배정을 설정한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 운영자 계정·조직·권한 그룹 |
| 언제 사용하는가 | 계정 조직 배치 옵션 조회, 권한 그룹 옵션 조회, 계정 등록 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 운영자 계정 정보, 소속 조직, 권한 그룹 |
| 업무 흐름 | 계정 조직 배치 옵션 조회, 권한 그룹 옵션 조회, 계정 등록 |
| 이 페이지의 역할 | 등록 · 계정 등록 |
| 판단 결과·다음 업무 | [계정 관리](account-management.md) |
| 다른 화면과의 구분 | SmartWork 관리 > 계정 관리에서 사용하는 등록 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 교체 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/account/components/OrganizationDepartmentPickerDialog.tsx#L258) |
| 확인 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/account/AccountRegistrationPage.tsx#L132) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 새 SmartWork 운영자 계정을 만들고 조직과 권한 그룹의 배정을 설정한다. |
| 메뉴·화면 경로 | SmartWork 관리 > 계정 관리 · `/settings/account-management/new` |
| 화면 유형·담당 | 등록 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [계정 관리](account-management.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/settings/account-management` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 계정 조직 배치 옵션 조회 | `/settings/account-management` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 권한 그룹 옵션 조회 | `/settings/account-management` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 계정 등록 | `/settings/account-management` `PROCESS` | `AdminMemberCreateRequest` `userId`, `userName`, `email`, `phone`, `birthDate`, `position`, `title`, `employmentYear`, `departmentId`, `managedOrganizations`, `userLevel`, `permissionGroup`, `permissionGroupIds` · 서버 필수 `userId`, `userName`, `email`, `phone`, `employmentYear`, `permissionGroupIds` |

코드에서 확인한 버튼·작업명은 **취소**, **확인**, **교체**, **저장**, **목록**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [계정 관리](account-management.md)에서 대상 또는 작업을 선택한다. `/settings/account-management/new`를 연다.
2. **사용자 명**, **아이디**, **이메일**, **생년월일**, **직급**, **비밀번호**, **핸드폰** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **확인**, **저장** 중 해당 버튼을 선택한다.
3. **계정 등록**을 실행하기 전에 변경 대상과 입력값을 확인한다. 표시되는 **신규 계정이 생성되었습니다.** 메시지와 대상 상태를 확인한다.
4. 후속 조회나 목록 복귀가 필요하면 [계정 관리](account-management.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 사용자 명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/account/components/AccountForm.tsx#L281) |
| 입력 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/account/components/AccountForm.tsx#L325) |
| 아이디 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/account/components/AccountForm.tsx#L298) |
| 이메일 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/account/components/AccountForm.tsx#L321) |
| 생년월일 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/account/components/AccountForm.tsx#L338) |
| 직급 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/account/components/AccountForm.tsx#L356) |
| 비밀번호 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/account/components/AccountForm.tsx#L375) |
| 핸드폰 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/account/components/AccountForm.tsx#L384) |
| 입사일 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/account/components/AccountForm.tsx#L408) |
| 조직 배치 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/account/components/AccountForm.tsx#L429) |
| 선택 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/account/components/AccountForm.tsx#L435) |
| 권한 그룹 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/account/components/AccountForm.tsx#L480) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 계정 조직 배치 옵션 조회 | `GET /api/v1/settings/admin-members/organization-options` · `/settings/account-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/settings/account/AdminMemberController.kt#L80) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `nodeType`, `id`, `name`, `path`, `memberCount`, `currentManagers`, `children` | `office.dbo.GROUP_MANAGER`, `office.dbo.PART_MANAGER`, `office.dbo.PART_INFO`, `office.dbo.DEPT_MANAGER`, `office.dbo.DEPT` 외 3개 |
| 권한 그룹 옵션 조회 | `GET /api/v1/settings/permission-groups/options` · `/settings/account-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/settings/permissions/PermissionGroupController.kt#L75) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `id`, `groupName` | `smartwork.dbo.sw_permission_group` |
| 계정 등록 | `POST /api/v1/settings/admin-members` · `/settings/account-management` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/settings/account/AdminMemberController.kt#L87) | `AdminMemberCreateRequest` `userId`, `userName`, `email`, `phone`, `birthDate`, `position`, `title`, `employmentYear`, `departmentId`, `managedOrganizations`, `userLevel`, `permissionGroup`, `permissionGroupIds` · 서버 필수 `userId`, `userName`, `email`, `phone`, `employmentYear`, `permissionGroupIds` → `success`, `data`, `error`, `message` | `office.dbo.SAWON`, `office.dbo.upGW_SavSawon`, `SmartBill3.dbo.ADMIN_INFO`, `office.dbo.SW_MENU`, `office.dbo.DEPT_DETAIL` 외 12개 · 정의에서 확인한 쓰기 `office.dbo.SAWON`, `SmartBill3.dbo.ADMIN_INFO`, `office.dbo.SW_MENU`, `office.dbo.DEPT_DETAIL` 외 2개 · 코드 연계 NxapiMailClient, 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `office.dbo.GROUP_MANAGER` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/account/repository/AdminMemberMapper.kt#L316) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-74bd137c16c3e256) |
| `office.dbo.PART_MANAGER` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/account/repository/AdminMemberMapper.kt#L316) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-272a73b3400fa0e4) |
| `office.dbo.PART_INFO` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/account/repository/AdminMemberMapper.kt#L316) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-55373887260bf623) |
| `office.dbo.DEPT_MANAGER` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/account/repository/AdminMemberMapper.kt#L316) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-6bd350bbf4a76a9a) |
| `office.dbo.DEPT` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/account/repository/AdminMemberMapper.kt#L316) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-cac428eda173d0f6) |
| `office.dbo.DEPT_DETAIL` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/account/repository/AdminMemberMapper.kt#L316) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-f1473984f53ebe9a) |
| `office.dbo.SAWON` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/account/repository/AdminMemberMapper.kt#L316) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3a9ea6e368df5cb3) |
| `office.dbo.GROUP_INFO` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/account/repository/AdminMemberMapper.kt#L316) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-f03382fc93536aac) |
| `smartwork.dbo.sw_permission_group` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/permissions/repository/PermissionGroupMapper.kt#L55) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-7e8619e24b7beced) |
| `office.dbo.upGW_SavSawon` | @MOD varchar(3), @SID varchar(15), @PW varchar(100), @SNAME varchar(20), @CLASS varchar(4), @JOB varchar(4), @SW_EMAIL varchar(50), @HP varchar(20), @BIRTHDAY_TYPE char(1), @BIRTHDAY varchar(8), @ADMIN_TYPE char(1), @JOIN_DATE varchar(10), @LEAVE_DATE varchar(10), @LEAVE_YN char(1), @SW_NO int, @CHKPW_YN char(1) | 정의 참조 `office.dbo.SAWON` · 정적 쓰기 `office.dbo.SAWON` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/account/repository/AdminMemberMapper.kt#L384) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-647ebb9dc9a6eb9c) |
| `SmartBill3.dbo.ADMIN_INFO` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL INSERT INTO | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/account/repository/AdminMemberMapper.kt#L517) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-61a4c49cd623d819) |
| `office.dbo.SW_MENU` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL DELETE FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/account/repository/AdminMemberMapper.kt#L417) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-04b9d6afa210256e) |
| `smartwork.dbo.usp_sw_permission_group_user_replace` | @SW_NO bigint, @GROUP_IDS_JSON nvarchar(max), @UPDATED_BY_SW_NO bigint, @RESULT int OUT | 정의 참조 `smartwork.dbo.sw_permission_group`, `smartwork.dbo.sw_permission_group_user` · 정적 쓰기 `smartwork.dbo.sw_permission_group_user` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/permissions/repository/PermissionGroupMapper.kt#L184) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-00e0e6f11da9e056) |
| `smartwork.dbo.sw_permission_group_user` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/permissions/repository/PermissionGroupMapper.kt#L70) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-29b81717598eadd5) |
| `smartwork.dbo.usp_sw_permission_group_current_select` | @SW_NO bigint | 정의 참조 `smartwork.dbo.sw_permission_group`, `smartwork.dbo.sw_permission_group_menu_permission`, `smartwork.dbo.sw_permission_group_user` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/permissions/repository/PermissionGroupMapper.kt#L203) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-d4980d8cd8dcad8b) |
| `smartwork.dbo.sw_auth_password_history` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL INSERT INTO | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/identity/repository/PasswordSecurityMapper.kt#L162) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b08bc145648dbf22) |
| `smartwork.dbo.sw_auth_account_security` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/identity/repository/PasswordSecurityMapper.kt#L70) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-d2c8f8592d4942ff) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 운영자 계정 정보, 소속 조직, 권한 그룹 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SmartWork 관리 > 계정 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 계정 생성 중 오류가 발생했습니다. | 운영자 계정 정보, 소속 조직, 권한 그룹 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/SettingsRoutes.tsx#L27) · [AccountRegistrationPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/account/AccountRegistrationPage.tsx#L23) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/account/api/accountManagementApi.ts#L84) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/permissions/api/permissionManagementApi.ts#L52) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/account/api/accountManagementApi.ts#L96) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 17개 중 개발 메타데이터 확인 17개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-bb43fe629cc103ae) | Demo 메타데이터 17/17개 확인 · Dev와 계약 차이 1개 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

# [운영자 계정·조직·권한 그룹] 계정 관리 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

SmartWork 로그인 계정 목록을 사용자명/아이디/조직으로 검색하고 페이지네이션한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 운영자 계정·조직·권한 그룹 |
| 언제 사용하는가 | 계정 목록 조회, 계정 삭제 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 아이디, 사용자 명, 조직 배치, 권한, 등록일자, 이메일 |
| 업무 흐름 | 계정 목록 조회, 계정 삭제 |
| 이 페이지의 역할 | 조회·관리 · 계정 목록 조회 |
| 판단 결과·다음 업무 | [계정 관리 등록](account-management__new.md) · [계정 관리 수정](account-management__by-id__edit.md) · [권한 관리 상세](permissions__by-id.md) |
| 다른 화면과의 구분 | 이 경로에서 볼 수 있는 조건·결과를 기준으로 사용한다. 독립 경로의 상세·등록은 관련 화면에 연결한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 확인 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/account/AccountManagementPage.tsx#L176) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | SmartWork 로그인 계정 목록을 사용자명/아이디/조직으로 검색하고 페이지네이션한다. |
| 메뉴·화면 경로 | SmartWork 관리 > 계정 관리 · `/settings/account-management` |
| 화면 유형·담당 | 조회·관리 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [계정 관리 등록](account-management__new.md) · [계정 관리 수정](account-management__by-id__edit.md) · [권한 관리 상세](permissions__by-id.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/settings/account-management` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 계정 목록 조회 | `/settings/account-management` `VIEW` | `AdminMemberSearchRequest` `searchKeyword`, `page`, `size` |
| 계정 삭제 | `/settings/account-management` `DELETE` | `adminNo: Long` |
| 계정 개인정보 원문 조회 | `/settings/account-management` / `UNMASK` | `adminNo`, `field` |

코드에서 확인한 버튼·작업명은 **검색**, **신규 등록**, **수정**, **삭제**, **확인**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **SmartWork 관리 > 계정 관리**를 연다. `/settings/account-management`를 연다.
2. **계정 목록 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
3. 후속 조회나 목록 복귀가 필요하면 [계정 관리 등록](account-management__new.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 사용자명, 아이디, 조직 입력 | 입력 또는 선택 | API 기본값 null | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/account/AccountManagementPage.tsx#L31) |
| 아이디 | 출력 | 조회 응답 기준 | 화면 필드 `userId` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/account/components/AccountTable.tsx#L48) |
| 사용자 명 | 출력 | 조회 응답 기준 | 화면 필드 `userName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/account/components/AccountTable.tsx#L59) |
| 조직 배치 | 출력 | 조회 응답 기준 | 화면 필드 `organizationDisplay` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/account/components/AccountTable.tsx#L70) |
| 권한 | 출력 | 조회 응답 기준 | 화면 필드 `permissionGroups` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/account/components/AccountTable.tsx#L80) |
| 등록일자 | 출력 | 조회 응답 기준 | 화면 필드 `registrationDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/account/components/AccountTable.tsx#L99) |
| 이메일 | 출력 | 조회 응답 기준 | 화면 필드 `email` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/account/components/AccountTable.tsx#L105) |
| 핸드폰 | 출력 | 조회 응답 기준 | 화면 필드 `phone` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/account/components/AccountTable.tsx#L115) |
| 처리 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/account/components/AccountTable.tsx#L122) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 계정 목록 조회 | `GET /api/v1/settings/admin-members` · `/settings/account-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/settings/account/AdminMemberController.kt#L61) | `AdminMemberSearchRequest` `searchKeyword`, `page`, `size` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `currentPage`, `size` | `office.dbo.SAWON`, `office.dbo.DEPT_DETAIL`, `office.dbo.DEPT`, `office.dbo.GROUP_MANAGER`, `office.dbo.GROUP_INFO` 외 5개 · 코드 연계 트랜잭션 |
| 계정 삭제 | `DELETE /api/v1/settings/admin-members/{adminNo}` · `/settings/account-management` `DELETE` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/settings/account/AdminMemberController.kt#L147) | `adminNo: Long` → `success`, `data`, `error`, `message` | `office.dbo.SW_MENU`, `office.dbo.DEPT_DETAIL`, `office.dbo.GROUP_MANAGER`, `office.dbo.PART_MANAGER`, `office.dbo.DEPT_MANAGER` 외 9개 · 정의에서 확인한 쓰기 `office.dbo.SW_MENU`, `office.dbo.DEPT_DETAIL`, `office.dbo.GROUP_MANAGER`, `office.dbo.PART_MANAGER` 외 2개 · 코드 연계 트랜잭션 |
| 계정 개인정보 원문 조회 | `POST /api/v1/settings/admin-members/{adminNo}/sensitive-values/reveal` · `/settings/account-management` / `UNMASK` · [화면 컴포넌트](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/account/components/AccountTable.tsx#L36) · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/settings/account/AdminMemberController.kt#L159) | `adminNo`, `field` → 요청한 항목의 원문 응답 | 권한 검사 후 대상 값을 조회하고 감사 기록을 남긴다. |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `office.dbo.SAWON` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/account/repository/AdminMemberMapper.kt#L119) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3a9ea6e368df5cb3) |
| `office.dbo.DEPT_DETAIL` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/account/repository/AdminMemberMapper.kt#L119) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-f1473984f53ebe9a) |
| `office.dbo.DEPT` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/account/repository/AdminMemberMapper.kt#L119) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-cac428eda173d0f6) |
| `office.dbo.GROUP_MANAGER` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/account/repository/AdminMemberMapper.kt#L119) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-74bd137c16c3e256) |
| `office.dbo.GROUP_INFO` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/account/repository/AdminMemberMapper.kt#L119) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-f03382fc93536aac) |
| `office.dbo.PART_MANAGER` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/account/repository/AdminMemberMapper.kt#L119) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-272a73b3400fa0e4) |
| `office.dbo.PART_INFO` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/account/repository/AdminMemberMapper.kt#L119) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-55373887260bf623) |
| `office.dbo.DEPT_MANAGER` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/account/repository/AdminMemberMapper.kt#L119) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-6bd350bbf4a76a9a) |
| `smartwork.dbo.sw_permission_group_user` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/permissions/repository/PermissionGroupMapper.kt#L89) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-29b81717598eadd5) |
| `smartwork.dbo.sw_permission_group` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/permissions/repository/PermissionGroupMapper.kt#L89) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-7e8619e24b7beced) |
| `office.dbo.SW_MENU` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL DELETE FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/account/repository/AdminMemberMapper.kt#L485) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-04b9d6afa210256e) |
| `office.dbo.upGW_OutSawon` | @idx int | 정의 참조 `office.dbo.SAWON` · 정적 쓰기 `office.dbo.SAWON` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/account/repository/AdminMemberMapper.kt#L489) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-6da8a5eb116fc6c3) |
| `smartwork.dbo.usp_sw_permission_group_current_select` | @SW_NO bigint | 정의 참조 `smartwork.dbo.sw_permission_group`, `smartwork.dbo.sw_permission_group_menu_permission`, `smartwork.dbo.sw_permission_group_user` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/permissions/repository/PermissionGroupMapper.kt#L203) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-d4980d8cd8dcad8b) |
| `smartwork.dbo.sw_auth_account_security` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/identity/repository/PasswordSecurityMapper.kt#L70) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-d2c8f8592d4942ff) |
| `smartwork.dbo.usp_sw_log_access_event_insert` | @EVENT_TYPE varchar(30) IN, @STATUS varchar(20) IN, @USER_ID bigint IN, @MEMBER_ID nvarchar(50) IN, @USER_NAME nvarchar(100) IN, @DEPARTMENT_NAME nvarchar(100) IN, @PAGE_TITLE nvarchar(200) IN, @PATH nvarchar(500) IN, @MENU_PATH nvarchar(500) IN, @MENU_LABEL nvarchar(200) IN, @CATEGORY_NAME nvarchar(200) IN, @SUB_CATEGORY_NAME nvarchar(200) IN, @MENU_ORDER int IN, @IP_ADDRESS varchar(45) IN, @USER_AGENT nvarchar(1000) IN, @BROWSER varchar(100) IN, @OS varchar(100) IN, @REFERRER nvarchar(500) IN, @DETAIL nvarchar(1000) IN, @RESULT int OUT, @COUNTS_AS_VISIT bit IN | 원문 조회 또는 감사 흐름에서 호출 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/logmanagement/repository/LogManagementMapper.kt#L92) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 아이디, 사용자 명, 조직 배치, 권한, 등록일자, 이메일 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SmartWork 관리 > 계정 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 계정 삭제 중 오류가 발생했습니다. | 아이디, 사용자 명, 조직 배치, 권한, 등록일자, 이메일 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/SettingsRoutes.tsx#L26) · [AccountManagementPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/account/AccountManagementPage.tsx#L38) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/account/api/accountManagementApi.ts#L61) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/account/api/accountManagementApi.ts#L146) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 14개 중 개발 메타데이터 확인 14개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-d353a65f587382f0) | Demo 메타데이터 15/15개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

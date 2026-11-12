# [직원 인증·내 계정·세션] 로그인 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

SmartWork 관리자 계정으로 인증하고, 계정 상태에 따라 초기 설정·비밀번호 변경 또는 대시보드로 이동한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 직원 인증·내 계정·세션 |
| 언제 사용하는가 | 로그인, 로그인 인증코드 확인, 로그인 인증코드 재발송 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 로그인 ID와 비밀번호 |
| 업무 흐름 | 로그인, 로그인 인증코드 확인, 로그인 인증코드 재발송 |
| 이 페이지의 역할 | 인증 · 로그인 |
| 판단 결과·다음 업무 | [비밀번호 재설정](forgot-password.md) |
| 다른 화면과의 구분 | SmartWork 공통 > 로그인에서 사용하는 인증 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | SmartWork 관리자 계정으로 인증하고, 계정 상태에 따라 초기 설정·비밀번호 변경 또는 대시보드로 이동한다. |
| 메뉴·화면 경로 | SmartWork 공통 > 로그인 · `/` |
| 화면 유형·담당 | 인증 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [비밀번호 재설정](forgot-password.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | 로그인 전 또는 계정의 인증·초기 설정 상태에서 진입한다. 계정 정책에 따라 사용 가능한 절차가 달라진다. | SmartWork 계정 |
| 로그인 | 인증·계정 상태 및 보안 설정 확인 | `LoginRequest` `memberId`, `password` |
| 로그인 인증코드 확인 | 인증·계정 상태 및 보안 설정 확인 | `LoginVerifyRequest` `challengeId`, `code` |
| 로그인 인증코드 재발송 | 인증·계정 상태 및 보안 설정 확인 | `LoginResendRequest` `challengeId` |

코드에서 확인한 버튼·작업명은 **확인**, **인증코드 재발송**, **처음으로**, **로그인**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. SmartWork 로그인 화면을 열고 **아이디**와 **비밀번호**를 입력한다. 필요한 경우 **아이디 저장**을 선택한다.
2. **로그인**을 선택한다. 인증코드 화면이 나타나면 안내에 따라 6자리 숫자를 입력하고 확인한다.
3. 초기 계정 설정 또는 비밀번호 변경이 요구되면 해당 화면을 진행한다. 정상 인증 뒤에는 대시보드에서 업무 메뉴로 이동한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 인증코드 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/identity/login/VerificationCodeForm.tsx#L63) |
| 6자리 숫자 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/identity/login/VerificationCodeForm.tsx#L66) |
| 아이디 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/identity/login/LoginPage.tsx#L232) |
| 아이디를 입력하세요 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/identity/login/LoginPage.tsx#L235) |
| 비밀번호 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/identity/login/LoginPage.tsx#L248) |
| 비밀번호를 입력하세요 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/identity/login/LoginPage.tsx#L251) |
| 아이디 저장 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/identity/login/LoginPage.tsx#L269) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 로그인 | `POST /api/v1/auth/login` · 인증·계정 상태 및 보안 설정 확인 · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/identity/controller/AuthController.kt#L63) | `LoginRequest` `memberId`, `password` → `success`, `data`, `error` | `office.dbo.SAWON`, `smartwork.dbo.sw_auth_account_security`, `office.dbo.upGW_Login`, `SmartBill3.dbo.upAdmSB_LoginFail`, `smartwork.dbo.sw_permission_group_user` 외 15개 · 정의에서 확인한 쓰기 `office.dbo.SAWON`, `SmartBill3.dbo.ADMIN_LOGIN_HIS`, `smartwork.dbo.sw_log_access_event`, `smartwork.dbo.sw_log_system_event` 외 1개 · 코드 연계 NxapiMailClient, 트랜잭션 |
| 로그인 인증코드 확인 | `POST /api/v1/auth/login/verify` · 인증·계정 상태 및 보안 설정 확인 · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/identity/controller/AuthController.kt#L84) | `LoginVerifyRequest` `challengeId`, `code` → `success`, `data`, `error`, `accessToken`, `tokenType`, `expiresIn`, `user`, `passwordChangeReason`, `initialAccountSetupRequired`, `verificationRequired` | `SmartBill3.dbo.upAdmSB_LoginFail`, `office.dbo.SAWON`, `smartwork.dbo.sw_permission_group_user`, `smartwork.dbo.sw_permission_group`, `smartwork.dbo.usp_sw_permission_group_current_select` 외 14개 · 정의에서 확인한 쓰기 `SmartBill3.dbo.ADMIN_LOGIN_HIS`, `smartwork.dbo.sw_log_access_event`, `smartwork.dbo.sw_log_system_event`, `office.dbo.Login_History` · 코드 연계 트랜잭션 |
| 로그인 인증코드 재발송 | `POST /api/v1/auth/login/resend` · 인증·계정 상태 및 보안 설정 확인 · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/identity/controller/AuthController.kt#L100) | `LoginResendRequest` `challengeId` → `success`, `data`, `error`, `challengeId`, `maskedEmail`, `expiresInSeconds`, `resendAvailableInSeconds`, `verificationRequired` | 코드 연계 NxapiMailClient |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `office.dbo.SAWON` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/identity/repository/PasswordSecurityMapper.kt#L59) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3a9ea6e368df5cb3) |
| `smartwork.dbo.sw_auth_account_security` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/identity/repository/PasswordSecurityMapper.kt#L70) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-d2c8f8592d4942ff) |
| `office.dbo.upGW_Login` | @ID varchar(15), @PW varchar(35), @shapw varchar(100) | 정의 참조 `SmartBill3.dbo.ADMIN_LOGIN_HIS`, `office.dbo.DEPT`, `office.dbo.DEPT_DETAIL`, `office.dbo.SAWON` · 정적 쓰기 `office.dbo.SAWON` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/identity/repository/LoginMapper.kt#L39) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-c6f53c1d84c362e8) |
| `SmartBill3.dbo.upAdmSB_LoginFail` | @ID varchar(20), @LOGIN_ROUTE varchar(10) | 정의 참조 `SmartBill3.dbo.ADMIN_LOGIN_HIS` · 정적 쓰기 `SmartBill3.dbo.ADMIN_LOGIN_HIS` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/identity/repository/LoginMapper.kt#L137) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-738bc7dc57a3b2a6) |
| `smartwork.dbo.sw_permission_group_user` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/permissions/repository/PermissionGroupMapper.kt#L70) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-29b81717598eadd5) |
| `smartwork.dbo.sw_permission_group` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/permissions/repository/PermissionGroupMapper.kt#L70) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-7e8619e24b7beced) |
| `smartwork.dbo.usp_sw_permission_group_current_select` | @SW_NO bigint | 정의 참조 `smartwork.dbo.sw_permission_group`, `smartwork.dbo.sw_permission_group_menu_permission`, `smartwork.dbo.sw_permission_group_user` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/permissions/repository/PermissionGroupMapper.kt#L203) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-d4980d8cd8dcad8b) |
| `smartwork.dbo.sw_auth_password_history` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/identity/repository/PasswordSecurityMapper.kt#L153) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b08bc145648dbf22) |
| `smartwork.dbo.sw_system_setting` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/loginauthentication/repository/LoginAuthenticationMapper.kt#L26) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3292242ed1c8a635) |
| `smartwork.dbo.usp_sw_log_access_event_insert` | @EVENT_TYPE varchar(30), @STATUS varchar(20), @USER_ID bigint = NULL, @MEMBER_ID nvarchar(50) = NULL, @USER_NAME nvarchar(100) = NULL, @DEPARTMENT_NAME nvarchar(100) = NULL, @PAGE_TITLE nvarchar(200) = NULL, @PATH nvarchar(500) = NULL, @MENU_PATH nvarchar(500) = NULL, @MENU_LABEL nvarchar(200) = NULL, @CATEGORY_NAME nvarchar(200) = NULL, @SUB_CATEGORY_NAME nvarchar(200) = NULL, @MENU_ORDER int = NULL, @IP_ADDRESS varchar(45) = NULL, @USER_AGENT nvarchar(1000) = NULL, @BROWSER varchar(100) = NULL, @OS varchar(100) = NULL, @REFERRER nvarchar(500) = NULL, @DETAIL nvarchar(1000) = NULL, @RESULT int OUT, @COUNTS_AS_VISIT bit = 1 | 정의 참조 `smartwork.dbo.sw_log_access_event` · 정적 쓰기 `smartwork.dbo.sw_log_access_event` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/logmanagement/repository/LogManagementMapper.kt#L92) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b7ba94e0cc2f35c0) |
| `smartwork.dbo.usp_sw_log_system_event_insert` | @LEVEL varchar(10), @CATEGORY varchar(30), @SOURCE nvarchar(200) = NULL, @MESSAGE nvarchar(1000), @REQUEST_PATH nvarchar(500) = NULL, @HTTP_METHOD varchar(10) = NULL, @USER_ID bigint = NULL, @MEMBER_ID nvarchar(50) = NULL, @STATUS_CODE int = NULL, @DURATION_MS bigint = NULL, @IP_ADDRESS varchar(45) = NULL, @USER_AGENT nvarchar(1000) = NULL, @DETAIL nvarchar(max) = NULL, @RESULT int OUT | 정의 참조 `smartwork.dbo.sw_log_system_event` · 정적 쓰기 `smartwork.dbo.sw_log_system_event` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/logmanagement/repository/LogManagementMapper.kt#L115) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-30344bbc069b2be3) |
| `office.dbo.GROUP_MANAGER` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/identity/repository/LoginMapper.kt#L123) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-74bd137c16c3e256) |
| `office.dbo.PART_MANAGER` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/identity/repository/LoginMapper.kt#L123) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-272a73b3400fa0e4) |
| `office.dbo.DEPT_MANAGER` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/identity/repository/LoginMapper.kt#L123) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-6bd350bbf4a76a9a) |
| `office.dbo.DEPT_DETAIL` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/identity/repository/LoginMapper.kt#L123) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-f1473984f53ebe9a) |
| `office.dbo.DEPT` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/identity/repository/LoginMapper.kt#L123) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-cac428eda173d0f6) |
| `office.dbo.PART_INFO` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/identity/repository/LoginMapper.kt#L123) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-55373887260bf623) |
| `office.dbo.GROUP_INFO` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/identity/repository/LoginMapper.kt#L123) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-f03382fc93536aac) |
| `office.dbo.SP_INSERTLOGINLOG` | @LOGIN_IP varchar(15), @LOGIN_ID varchar(50), @PREVIOUSLY_ROUTE varchar(200), @ACCESS_ROUTE varchar(200), @KEYSTRING varchar(400), @DIVISION varchar(15) | 정의 참조 `office.dbo.Login_History` · 정적 쓰기 `office.dbo.Login_History` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/identity/repository/LoginMapper.kt#L149) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-8ce17574a6ee3429) |
| `smartwork.dbo.sw_user_preference` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/identity/repository/UserPreferenceMapper.kt#L17) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-96130f50927e2542) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 인증 또는 계정 처리에 실패함 | 입력 내용, 계정 상태와 화면 메시지 | 화면 안내를 확인한다. 계속 실패하면 계정 관리 담당에게 오류와 시각을 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/index.tsx) · [LoginPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/identity/login/LoginPage.tsx#L32) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/api/loginApi.ts#L72) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/api/loginApi.ts#L76) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/api/loginApi.ts#L80) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 20개 중 개발 메타데이터 확인 20개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-8a5edab282632443) | Demo 메타데이터 20/20개 확인 · 2026-11-11 |
| 화면 재현 | [로컬 Playwright 표본](../../evidence/browser/all-pages-sample-2026-11-11.json) | 입력 화면 재현 · 로그인 후 대시보드 이동 확인 · 표시 아이디, 비밀번호 · 2026-11-11 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

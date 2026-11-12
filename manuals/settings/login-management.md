# [운영 공지·인증 정책과 감사 로그] 로그인 관리 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

중복 로그인 방지를 적용하지 않는 계정 목록을 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 운영 공지·인증 정책과 감사 로그 |
| 언제 사용하는가 | 로그인 이메일 인증 정책 조회, 예외 계정 목록 조회, 중복 로그인 방지 정책 조회, 조직도 사원 목록 조회, 로그인 이메일 인증 정책 변경 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 사용, 미사용, 아이디, 이름, 소속, 등록자 |
| 업무 흐름 | 로그인 이메일 인증 정책 조회, 예외 계정 목록 조회, 중복 로그인 방지 정책 조회, 조직도 사원 목록 조회, 로그인 이메일 인증 정책 변경 |
| 이 페이지의 역할 | 조회·관리 · 예외 계정 목록 조회 |
| 판단 결과·다음 업무 | 현재 화면에서 결과를 확인한다. |
| 다른 화면과의 구분 | 같은 경로에서 열리는 조회·팝업은 이 문서에서 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 추가 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/duplicate-login/components/ExemptAccountAddModal.tsx#L74) |
| 삭제 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/duplicate-login/DuplicateLoginSettings.tsx#L159) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 중복 로그인 방지를 적용하지 않는 계정 목록을 조회한다. |
| 메뉴·화면 경로 | SmartWork 관리 > 로그인 관리 · `/settings/login-management` |
| 화면 유형·담당 | 조회·관리 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | 현재 화면에서 결과를 확인한다. |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/settings/login-management` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 로그인 이메일 인증 정책 조회 | `/settings/login-management` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 예외 계정 목록 조회 | `/settings/login-management` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 중복 로그인 방지 정책 조회 | `/settings/login-management` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 조직도 사원 목록 조회 | 정적 메뉴 액션 미확인 · Controller·공통 보안 검사 확인 | `OrganizationDirectoryMemberSearchRequest` `nodeType`, `nodeId`, `searchKeyword` |
| 로그인 이메일 인증 정책 변경 | `/settings/login-management` `PROCESS` | `LoginAuthenticationPolicyUpdateRequest` `enabled` |
| 중복 로그인 방지 정책 변경 | `/settings/login-management` `PROCESS` | `DuplicateLoginPolicyUpdateRequest` `enabled` |
| 예외 계정 추가 | `/settings/login-management` `PROCESS` | `DuplicateLoginExemptAccountAddRequest` `userIds` |
| 예외 계정 삭제 | `/settings/login-management` `DELETE` | `userId: Long` |

코드에서 확인한 버튼·작업명은 **로그인 이메일 인증 (OTP) 설정**, **저장**, **중복 로그인 방지 설정**, **중복 로그인 예외 계정**, **예외 계정 추가**, **삭제**, **추가**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **SmartWork 관리 > 로그인 관리**를 연다. `/settings/login-management`를 연다.
2. **사용**, **미사용**, **이름·아이디·소속** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **저장** 중 해당 버튼을 선택한다.
3. **예외 계정 목록 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 사용 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/login-authentication/LoginAuthenticationSettings.tsx#L53) |
| 미사용 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/login-authentication/LoginAuthenticationSettings.tsx#L57) |
| 아이디 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/duplicate-login/DuplicateLoginSettings.tsx#L132) |
| 이름 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/duplicate-login/DuplicateLoginSettings.tsx#L132) |
| 소속 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/duplicate-login/DuplicateLoginSettings.tsx#L132) |
| 등록자 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/duplicate-login/DuplicateLoginSettings.tsx#L133) |
| 등록일시 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/duplicate-login/DuplicateLoginSettings.tsx#L133) |
| 관리 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/duplicate-login/DuplicateLoginSettings.tsx#L133) |
| 이름·아이디·소속 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `keyword` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/duplicate-login/components/ExemptAccountAddModal.tsx#L45) |
| 직원 명 | 출력 | 조회 응답 기준 | 화면 필드 `member` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/duplicate-login/components/ExemptAccountAddModal.tsx#L57) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 로그인 이메일 인증 정책 조회 | `GET /api/v1/settings/login-authentication/policy` · `/settings/login-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/settings/loginauthentication/LoginAuthenticationController.kt#L31) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `enabled` | `smartwork.dbo.sw_system_setting` · 코드 연계 트랜잭션 |
| 예외 계정 목록 조회 | `GET /api/v1/settings/duplicate-login/exempt-accounts` · `/settings/login-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/settings/duplicatelogin/DuplicateLoginController.kt#L68) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `userId`, `memberId`, `userName`, `departmentName`, `registrant`, `registrationDate` | `smartwork.dbo.sw_system_setting`, `office.dbo.SAWON`, `office.dbo.DEPT_DETAIL`, `office.dbo.DEPT`, `office.dbo.DEPT_MANAGER` 외 4개 |
| 중복 로그인 방지 정책 조회 | `GET /api/v1/settings/duplicate-login/policy` · `/settings/login-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/settings/duplicatelogin/DuplicateLoginController.kt#L48) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `enabled` | `smartwork.dbo.sw_system_setting` |
| 조직도 사원 목록 조회 | `GET /api/v1/identity/organization-directory/members` · 정적 메뉴 액션 미확인 · Controller·공통 보안 검사 확인 · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/identity/organizationdirectory/OrganizationDirectoryController.kt#L42) | `OrganizationDirectoryMemberSearchRequest` `nodeType`, `nodeId`, `searchKeyword` → `success`, `data`, `error`, `content`, `totalElements` | 직접 DB 호출이 연결된 경로는 현재 소스에서 미확인. 세부 저장소는 Controller와 Service 참조. |
| 로그인 이메일 인증 정책 변경 | `PUT /api/v1/settings/login-authentication/policy` · `/settings/login-management` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/settings/loginauthentication/LoginAuthenticationController.kt#L40) | `LoginAuthenticationPolicyUpdateRequest` `enabled` → `success`, `data`, `error`, `enabled` | 코드 연계 트랜잭션 |
| 중복 로그인 방지 정책 변경 | `PUT /api/v1/settings/duplicate-login/policy` · `/settings/login-management` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/settings/duplicatelogin/DuplicateLoginController.kt#L57) | `DuplicateLoginPolicyUpdateRequest` `enabled` → `success`, `data`, `error`, `enabled` | 코드 연계 트랜잭션 |
| 예외 계정 추가 | `POST /api/v1/settings/duplicate-login/exempt-accounts` · `/settings/login-management` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/settings/duplicatelogin/DuplicateLoginController.kt#L74) | `DuplicateLoginExemptAccountAddRequest` `userIds` → `success`, `data`, `error`, `addedCount` | `smartwork.dbo.sw_system_setting`, `office.dbo.SAWON` · 정의에서 확인한 쓰기 `smartwork.dbo.sw_system_setting` · 코드 연계 트랜잭션 |
| 예외 계정 삭제 | `DELETE /api/v1/settings/duplicate-login/exempt-accounts/{userId}` · `/settings/login-management` `DELETE` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/settings/duplicatelogin/DuplicateLoginController.kt#L89) | `userId: Long` → `success`, `data`, `error` | `smartwork.dbo.sw_system_setting` · 정의에서 확인한 쓰기 `smartwork.dbo.sw_system_setting` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.sw_system_setting` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/loginauthentication/repository/LoginAuthenticationMapper.kt#L26) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3292242ed1c8a635) |
| `office.dbo.SAWON` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/duplicatelogin/repository/DuplicateLoginMapper.kt#L114) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3a9ea6e368df5cb3) |
| `office.dbo.DEPT_DETAIL` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/duplicatelogin/repository/DuplicateLoginMapper.kt#L114) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-f1473984f53ebe9a) |
| `office.dbo.DEPT` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/duplicatelogin/repository/DuplicateLoginMapper.kt#L114) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-cac428eda173d0f6) |
| `office.dbo.DEPT_MANAGER` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/duplicatelogin/repository/DuplicateLoginMapper.kt#L114) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-6bd350bbf4a76a9a) |
| `office.dbo.PART_MANAGER` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/duplicatelogin/repository/DuplicateLoginMapper.kt#L114) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-272a73b3400fa0e4) |
| `office.dbo.PART_INFO` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/duplicatelogin/repository/DuplicateLoginMapper.kt#L114) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-55373887260bf623) |
| `office.dbo.GROUP_MANAGER` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/duplicatelogin/repository/DuplicateLoginMapper.kt#L114) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-74bd137c16c3e256) |
| `office.dbo.GROUP_INFO` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/duplicatelogin/repository/DuplicateLoginMapper.kt#L114) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-f03382fc93536aac) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 사용, 미사용, 아이디, 이름, 소속, 등록자 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SmartWork 관리 > 로그인 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 로그인 이메일 인증 설정을 불러오지 못했습니다. | 사용, 미사용, 아이디, 이름, 소속, 등록자 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 로그인 이메일 인증 설정을 저장하지 못했습니다. | 사용, 미사용, 아이디, 이름, 소속, 등록자 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 예외 계정 목록을 불러오지 못했습니다. | 사용, 미사용, 아이디, 이름, 소속, 등록자 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 중복 로그인 방지 설정을 불러오지 못했습니다. | 사용, 미사용, 아이디, 이름, 소속, 등록자 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/SettingsRoutes.tsx#L36) · [LoginManagementPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/login-management/LoginManagementPage.tsx#L6) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/login-authentication/api/loginAuthenticationApi.ts#L9) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/duplicate-login/api/duplicateLoginApi.ts#L23) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/duplicate-login/api/duplicateLoginApi.ts#L21) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/identity/organization-directory/api/organizationDirectoryApi.ts#L29) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/login-authentication/api/loginAuthenticationApi.ts#L10) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/duplicate-login/api/duplicateLoginApi.ts#L22) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/duplicate-login/api/duplicateLoginApi.ts#L24) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/duplicate-login/api/duplicateLoginApi.ts#L25) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 9개 중 개발 메타데이터 확인 9개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-5fec2fde4525616e) | Demo 메타데이터 9/9개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

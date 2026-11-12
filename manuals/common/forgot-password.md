# [직원 인증·내 계정·세션] 비밀번호 재설정 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

비밀번호를 잊은 사용자가 계정 확인 절차를 거쳐 새 비밀번호를 정한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 직원 인증·내 계정·세션 |
| 언제 사용하는가 | 비밀번호 찾기 인증코드 요청, 비밀번호 찾기 인증코드 확인, 비밀번호 찾기 인증코드 재발송 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 재설정 대상 계정 |
| 업무 흐름 | 비밀번호 찾기 인증코드 요청, 비밀번호 찾기 인증코드 확인, 비밀번호 찾기 인증코드 재발송 |
| 이 페이지의 역할 | 인증 · 비밀번호 찾기 인증코드 요청 |
| 판단 결과·다음 업무 | [로그인](login.md) |
| 다른 화면과의 구분 | SmartWork 공통 > 비밀번호 재설정에서 사용하는 인증 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 비밀번호를 잊은 사용자가 계정 확인 절차를 거쳐 새 비밀번호를 정한다. |
| 메뉴·화면 경로 | SmartWork 공통 > 비밀번호 재설정 · `/forgot-password` |
| 화면 유형·담당 | 인증 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [로그인](login.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | 로그인 전 또는 계정의 인증·초기 설정 상태에서 진입한다. 계정 정책에 따라 사용 가능한 절차가 달라진다. | SmartWork 계정 |
| 비밀번호 찾기 인증코드 요청 | 인증·계정 상태 및 보안 설정 확인 | `PasswordResetRequest` `memberId`, `email` |
| 비밀번호 찾기 인증코드 확인 | 인증·계정 상태 및 보안 설정 확인 | `PasswordResetVerifyRequest` `challengeId`, `code` |
| 비밀번호 찾기 인증코드 재발송 | 인증·계정 상태 및 보안 설정 확인 | `LoginResendRequest` `challengeId` |

코드에서 확인한 버튼·작업명은 **로그인으로**, **확인**, **인증코드 재발송**, **처음으로**, **인증코드 받기**, **로그인으로 돌아가기**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. `/forgot-password`를 연다.
2. **인증코드**, **아이디**, **등록 이메일** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **확인** 중 해당 버튼을 선택한다.
3. **비밀번호 찾기 인증코드 요청**을 실행하기 전에 변경 대상과 입력값을 확인한다. 처리 응답을 확인하고 관련 조회에서 대상의 상태를 확인한다.
4. 후속 조회나 목록 복귀가 필요하면 [로그인](login.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 인증코드 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/identity/login/VerificationCodeForm.tsx#L63) |
| 6자리 숫자 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/identity/login/VerificationCodeForm.tsx#L66) |
| 아이디 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/identity/forgot-password/ForgotPasswordPage.tsx#L163) |
| 등록 이메일 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/identity/forgot-password/ForgotPasswordPage.tsx#L178) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 비밀번호 찾기 인증코드 요청 | `POST /api/v1/auth/password-reset/request` · 인증·계정 상태 및 보안 설정 확인 · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/identity/controller/AuthController.kt#L110) | `PasswordResetRequest` `memberId`, `email` → `success`, `data`, `error`, `challengeId`, `maskedEmail`, `expiresInSeconds`, `resendAvailableInSeconds`, `verificationRequired` | `office.dbo.SAWON` · 코드 연계 NxapiMailClient |
| 비밀번호 찾기 인증코드 확인 | `POST /api/v1/auth/password-reset/verify` · 인증·계정 상태 및 보안 설정 확인 · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/identity/controller/AuthController.kt#L132) | `PasswordResetVerifyRequest` `challengeId`, `code` → `success`, `data`, `error`, `maskedEmail`, `message` | `office.dbo.SAWON`, `smartwork.dbo.sw_permission_group_user`, `smartwork.dbo.sw_permission_group`, `smartwork.dbo.usp_sw_permission_group_current_select`, `smartwork.dbo.sw_auth_password_history` · 정의에서 확인한 쓰기 `smartwork.dbo.sw_auth_password_history` · 코드 연계 NxapiMailClient, 트랜잭션 |
| 비밀번호 찾기 인증코드 재발송 | `POST /api/v1/auth/password-reset/resend` · 인증·계정 상태 및 보안 설정 확인 · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/identity/controller/AuthController.kt#L122) | `LoginResendRequest` `challengeId` → `success`, `data`, `error`, `challengeId`, `maskedEmail`, `expiresInSeconds`, `resendAvailableInSeconds`, `verificationRequired` | 코드 연계 NxapiMailClient |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `office.dbo.SAWON` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/identity/repository/PasswordSecurityMapper.kt#L59) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3a9ea6e368df5cb3) |
| `smartwork.dbo.sw_permission_group_user` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/permissions/repository/PermissionGroupMapper.kt#L70) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-29b81717598eadd5) |
| `smartwork.dbo.sw_permission_group` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/permissions/repository/PermissionGroupMapper.kt#L70) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-7e8619e24b7beced) |
| `smartwork.dbo.usp_sw_permission_group_current_select` | @SW_NO bigint | 정의 참조 `smartwork.dbo.sw_permission_group`, `smartwork.dbo.sw_permission_group_menu_permission`, `smartwork.dbo.sw_permission_group_user` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/permissions/repository/PermissionGroupMapper.kt#L203) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-d4980d8cd8dcad8b) |
| `smartwork.dbo.sw_auth_password_history` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL INSERT INTO | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/identity/repository/PasswordSecurityMapper.kt#L162) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b08bc145648dbf22) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 인증 또는 계정 처리에 실패함 | 입력 내용, 계정 상태와 화면 메시지 | 화면 안내를 확인한다. 계속 실패하면 계정 관리 담당에게 오류와 시각을 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/index.tsx) · [ForgotPasswordPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/identity/forgot-password/ForgotPasswordPage.tsx#L20) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/api/loginApi.ts#L90) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/api/loginApi.ts#L99) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/api/loginApi.ts#L94) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 5개 중 개발 메타데이터 확인 5개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-b798fcee2a650446) | Demo 메타데이터 5/5개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

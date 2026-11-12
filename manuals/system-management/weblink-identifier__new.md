# [업무·개선 요청·식별자·접속 기록] 웹링크 식별자 등록 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

웹링크 식별자를 등록한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 업무·개선 요청·식별자·접속 기록 |
| 언제 사용하는가 | 웹링크식별자 현재 사용자, 웹링크식별자 키 중복 확인, 웹링크식별자 키 자동 생성, 웹링크식별자 회원 확인, 웹링크식별자 등록 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 웹링크식별자 등록 |
| 업무 흐름 | 웹링크식별자 현재 사용자, 웹링크식별자 키 중복 확인, 웹링크식별자 키 자동 생성, 웹링크식별자 회원 확인, 웹링크식별자 등록 |
| 이 페이지의 역할 | 등록 · 웹링크식별자 등록 |
| 판단 결과·다음 업무 | [웹링크 식별자 관리](weblink-identifier.md) |
| 다른 화면과의 구분 | SB 운영관리 > 시스템 관리 > 웹링크 식별자 관리에서 사용하는 등록 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 저장 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/WeblinkIdentifierRegisterPage.tsx#L497) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 웹링크 식별자를 등록한다. |
| 메뉴·화면 경로 | SB 운영관리 > 시스템 관리 > 웹링크 식별자 관리 · `/system-management/weblink-identifier/new` |
| 화면 유형·담당 | 등록 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [웹링크 식별자 관리](weblink-identifier.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/system-management/weblink-identifier` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 웹링크식별자 현재 사용자 | `/system-management/weblink-identifier` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 웹링크식별자 키 중복 확인 | `/system-management/weblink-identifier` `VIEW` | `key: String` |
| 웹링크식별자 키 자동 생성 | `/system-management/weblink-identifier` `VIEW` | `comRegno: String` |
| 웹링크식별자 회원 확인 | `/system-management/weblink-identifier` `VIEW` | `comRegno: String` |
| 웹링크식별자 등록 | `/system-management/weblink-identifier` `PROCESS` | `WeblinkIdentifierCreateRequest` `confirmKey`, `comRegno`, `buttonControl`, `viewType`, `callDomain`, `returnPage` · 서버 필수 `confirmKey`, `comRegno`, `buttonControl`, `viewType`, `callDomain` |

코드에서 확인한 버튼·작업명은 **중복확인**, **자동생성**, **회원 확인**, **저장**, **목록**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [웹링크 식별자 관리](weblink-identifier.md)에서 대상 또는 작업을 선택한다. `/system-management/weblink-identifier/new`를 연다.
2. **웹링크식별자 등록**을 실행하기 전에 변경 대상과 입력값을 확인한다. 처리 응답을 확인하고 관련 조회에서 대상의 상태를 확인한다.
3. 후속 조회나 목록 복귀가 필요하면 [웹링크 식별자 관리](weblink-identifier.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| request | API 요청 | 화면과 요청 변환 코드 참조 | `WeblinkIdentifierCreateRequest` `confirmKey`, `comRegno`, `buttonControl`, `viewType`, `callDomain`, `returnPage` · 서버 필수 `confirmKey`, `comRegno`, `buttonControl`, `viewType`, `callDomain` |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 웹링크식별자 현재 사용자 | `GET /api/v1/system-management/weblink-identifier/current-user` · `/system-management/weblink-identifier` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/operations/system/weblinkidentifier/WeblinkIdentifierController.kt#L88) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `id`, `name` | 직접 DB 호출이 연결된 경로는 현재 소스에서 미확인. 세부 저장소는 Controller와 Service 참조. |
| 웹링크식별자 키 중복 확인 | `GET /api/v1/system-management/weblink-identifier/check-key` · `/system-management/weblink-identifier` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/operations/system/weblinkidentifier/WeblinkIdentifierController.kt#L70) | `key: String` → `success`, `data`, `error`, `available` | `SB_DTI.dbo.COMPANY_WEBLINK` |
| 웹링크식별자 키 자동 생성 | `GET /api/v1/system-management/weblink-identifier/generate-key` · `/system-management/weblink-identifier` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/operations/system/weblinkidentifier/WeblinkIdentifierController.kt#L76) | `comRegno: String` → `success`, `data`, `error`, `key` | `SB_DTI.dbo.COMPANY_WEBLINK` |
| 웹링크식별자 회원 확인 | `GET /api/v1/system-management/weblink-identifier/check-member` · `/system-management/weblink-identifier` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/operations/system/weblinkidentifier/WeblinkIdentifierController.kt#L82) | `comRegno: String` → `success`, `data`, `error`, `exists`, `message` | `SmartBill3.dbo.COMPANY` |
| 웹링크식별자 등록 | `POST /api/v1/system-management/weblink-identifier` · `/system-management/weblink-identifier` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/operations/system/weblinkidentifier/WeblinkIdentifierController.kt#L103) | `WeblinkIdentifierCreateRequest` `confirmKey`, `comRegno`, `buttonControl`, `viewType`, `callDomain`, `returnPage` · 서버 필수 `confirmKey`, `comRegno`, `buttonControl`, `viewType`, `callDomain` → `success`, `data`, `error`, `id`, `confirmKey`, `comRegno`, `callDomain`, `buttonControl`, `returnPage`, `viewType`, `createdAt`, `createdBy` | `SB_DTI.dbo.COMPANY_WEBLINK`, `smartwork.dbo.upGW_CONFIRM_KEY_SAV` · 정의에서 확인한 쓰기 `SB_DTI.dbo.COMPANY_WEBLINK` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `SB_DTI.dbo.COMPANY_WEBLINK` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/system/weblinkidentifier/repository/WeblinkIdentifierMapper.kt#L64) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-8d10682b1d32273c) |
| `SmartBill3.dbo.COMPANY` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/system/weblinkidentifier/repository/WeblinkIdentifierMapper.kt#L157) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-0e6fcaa6b5086c07) |
| `smartwork.dbo.upGW_CONFIRM_KEY_SAV` | @CONFIRM_KEY varchar(20), @COMREGNO varchar(10), @CALL_DOMAIN varchar(50), @BUTTON_CONTROL varchar(2), @RETURN_PAGE varchar(50), @VIEW_TYPE varchar(5), @CUSER varchar(12) | 정의 참조 `SB_DTI.dbo.COMPANY_WEBLINK` · 정적 쓰기 `SB_DTI.dbo.COMPANY_WEBLINK` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/system/weblinkidentifier/repository/WeblinkIdentifierMapper.kt#L68) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-7e5bd3b75884bee9) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 웹링크식별자 등록 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 운영관리 > 시스템 관리 > 웹링크 식별자 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 사용중인 CONFIRM_KEY 입니다. | 웹링크식별자 등록 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| CONFIRM_KEY 확인에 실패했습니다. | 웹링크식별자 등록 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| CONFIRM_KEY 자동생성에 실패했습니다. | 웹링크식별자 등록 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 스마트빌 가입정보가 없습니다. | 웹링크식별자 등록 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/OperationsRoutes.tsx#L82) · [WeblinkIdentifierRegisterPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/WeblinkIdentifierRegisterPage.tsx#L32) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/api/weblinkIdentifierApi.ts#L109) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/api/weblinkIdentifierApi.ts#L68) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/api/weblinkIdentifierApi.ts#L79) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/api/weblinkIdentifierApi.ts#L121) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/api/weblinkIdentifierApi.ts#L131) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 3개 중 개발 메타데이터 확인 3개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-81df7b111fa8dde6) | Demo 메타데이터 3/3개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

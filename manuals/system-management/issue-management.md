# [시스템 메시지·발행·이메일 확인] 발행 관리 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

당일 최근 발행 DTI 10건을 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 시스템 메시지·발행·이메일 확인 |
| 언제 사용하는가 | 발행관리 조회, 발행관리 BOCLINK 로그 조회 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 발행일자, 참조번호, 공급자 사업자번호, 공급자 회사명, 공급받는자 사업자번호, 공급받는자 회사명 |
| 업무 흐름 | 발행관리 조회, 발행관리 BOCLINK 로그 조회 |
| 이 페이지의 역할 | 조회 · 발행관리 조회 |
| 판단 결과·다음 업무 | 현재 화면에서 결과를 확인한다. |
| 다른 화면과의 구분 | 같은 경로에서 열리는 조회·팝업은 이 문서에서 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 당일 최근 발행 DTI 10건을 조회한다. |
| 메뉴·화면 경로 | SB 운영관리 > 시스템 관리 > 발행 관리 · `/system-management/issue-management` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | 현재 화면에서 결과를 확인한다. |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/system-management/issue-management` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 발행관리 조회 | `/system-management/issue-management` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 발행관리 BOCLINK 로그 조회 | `/system-management/issue-management` `VIEW` | `kind: String` |
| BOCLINK 로그 등록번호 원문 조회 | `/system-management/issue-management` / `UNMASK` | `kind`, `logIdx`, `field` |

## 3) 화면 사용 절차

1. **SB 운영관리 > 시스템 관리 > 발행 관리**를 연다. `/system-management/issue-management`를 연다.
2. **발행관리 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 발행일자 | 출력 | 조회 응답 기준 | API 응답 `issuedAt` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/components/RecentIssueSection.tsx#L67) |
| 참조번호 | 출력 | 조회 응답 기준 | API 응답 `refNo` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/components/RecentIssueSection.tsx#L73) |
| 공급자 사업자번호 | 출력 | 조회 응답 기준 | API 응답 `supplierBizNo` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/components/RecentIssueSection.tsx#L84) |
| 공급자 회사명 | 출력 | 조회 응답 기준 | API 응답 `supplierName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/components/RecentIssueSection.tsx#L100) |
| 공급받는자 사업자번호 | 출력 | 조회 응답 기준 | API 응답 `receiverBizNo` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/components/RecentIssueSection.tsx#L109) |
| 공급받는자 회사명 | 출력 | 조회 응답 기준 | API 응답 `receiverName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/components/RecentIssueSection.tsx#L125) |
| 방향-유형-상태 | 출력 | 조회 응답 기준 | API 응답 `directionTypeStatus` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/components/RecentIssueSection.tsx#L151) |
| 공급자 | 출력 | 조회 응답 기준 | 화면 필드 `supplier-group` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/components/RecentIssueSection.tsx#L192) |
| 공급받는자 | 출력 | 조회 응답 기준 | 화면 필드 `receiver-group` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/components/RecentIssueSection.tsx#L198) |
| 사업자번호 | 출력 | 조회 응답 기준 | 화면 필드 `supplierBizNo-header` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/components/RecentIssueSection.tsx#L242) |
| 회사명 | 출력 | 조회 응답 기준 | 화면 필드 `supplierName-header` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/components/RecentIssueSection.tsx#L248) |
| 일시 | 출력 | 조회 응답 기준 | API 응답 `datetime` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/components/BoclinkSection.tsx#L83) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 발행관리 조회 | `GET /api/v1/system-management/issue-management/recent-issues` · `/system-management/issue-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/operations/system/issuemanagement/IssueManagementController.kt#L44) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `content`, `totalElements`, `dtiIdx`, `dtiWday`, `issuedAt`, `refNo`, `supplierBizNo`, `supplierName`, `receiverBizNo` | 코드 연계 트랜잭션 |
| 발행관리 BOCLINK 로그 조회 | `GET /api/v1/system-management/issue-management/{kind}/logs` · `/system-management/issue-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/operations/system/issuemanagement/IssueManagementController.kt#L50) | `kind: String` → `success`, `data`, `error`, `content`, `totalElements`, `logIdx`, `datetime`, `signal`, `system`, `supplierBizNo`, `supplierName`, `receiverBizNo` | `office.dbo.SELECT_BCERRORLOG_BY_SERVERIP` |
| BOCLINK 로그 등록번호 원문 조회 | `POST /api/v1/system-management/issue-management/{kind}/logs/{logIdx}/sensitive-values/reveal` · `/system-management/issue-management` / `UNMASK` · [화면 컴포넌트](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/components/BoclinkSection.tsx#L131) · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/operations/system/issuemanagement/IssueManagementController.kt#L82) | `kind`, `logIdx`, `field` → 요청한 항목의 원문 응답 | 권한 검사 후 대상 값을 조회하고 감사 기록을 남긴다. |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `office.dbo.SELECT_BCERRORLOG_BY_SERVERIP` | @SERVERIP varchar(35) | 정의 참조 `SB_DTI_LOG.dbo.BC_ERROR_LOG` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/system/issuemanagement/repository/IssueManagementMapper.kt#L53) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-89a4813a020ed4c3) |
| `SB_DTI_LOG.dbo.BC_ERROR_LOG` | 개발 컬럼 메타데이터 확인 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/system/issuemanagement/repository/IssueManagementMapper.kt#L88) |
| `smartwork.dbo.usp_sw_log_access_event_insert` | @EVENT_TYPE varchar(30) IN, @STATUS varchar(20) IN, @USER_ID bigint IN, @MEMBER_ID nvarchar(50) IN, @USER_NAME nvarchar(100) IN, @DEPARTMENT_NAME nvarchar(100) IN, @PAGE_TITLE nvarchar(200) IN, @PATH nvarchar(500) IN, @MENU_PATH nvarchar(500) IN, @MENU_LABEL nvarchar(200) IN, @CATEGORY_NAME nvarchar(200) IN, @SUB_CATEGORY_NAME nvarchar(200) IN, @MENU_ORDER int IN, @IP_ADDRESS varchar(45) IN, @USER_AGENT nvarchar(1000) IN, @BROWSER varchar(100) IN, @OS varchar(100) IN, @REFERRER nvarchar(500) IN, @DETAIL nvarchar(1000) IN, @RESULT int OUT, @COUNTS_AS_VISIT bit IN | 원문 조회 또는 감사 흐름에서 호출 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/logmanagement/repository/LogManagementMapper.kt#L92) |

### 매퍼 호출 추가 확인

| DB 객체 | 호출 근거 | 개발 DB 확인 범위 |
| --- | --- | --- |
| [office.dbo.SELECT_DTI_LATEST](../../references/all-pages-demo.md#object-7a60afd781cfb8ed) | [selectRecentIssues](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/system/issuemanagement/repository/IssueManagementMapper.kt#L37) | 개발 카탈로그 확인 |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 발행일자, 참조번호, 공급자 사업자번호, 공급자 회사명, 공급받는자 사업자번호, 공급받는자 회사명 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 운영관리 > 시스템 관리 > 발행 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/OperationsRoutes.tsx#L68) · [SystemIssueManagementPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/SystemIssueManagementPage.tsx#L14) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/api/issueManagementApi.ts#L31) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/api/issueManagementApi.ts#L46) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 1개 중 개발 메타데이터 확인 1개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-fe51e098060eb627) | Demo 메타데이터 4/4개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

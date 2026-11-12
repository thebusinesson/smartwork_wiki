# [업무·개선 요청·식별자·접속 기록] 업무 리스트 등록 상세 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

업무 등록 상세를 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 업무·개선 요청·식별자·접속 기록 |
| 언제 사용하는가 | 업무 팀원 조회, 업무리스트등록 상세 조회, 업무리스트등록 수정, 업무리스트등록 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 매월 |
| 업무 흐름 | 업무 팀원 조회, 업무리스트등록 상세 조회, 업무리스트등록 수정, 업무리스트등록 |
| 이 페이지의 역할 | 상세 · 업무리스트등록 상세 조회 |
| 판단 결과·다음 업무 | [업무 리스트 등록](work__register.md) |
| 다른 화면과의 구분 | SB 운영관리 > 시스템 관리 > 업무 리스트 등록에서 사용하는 상세 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 확인 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/TeamWorkRegisterPage.tsx#L488) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 업무 등록 상세를 조회한다. |
| 메뉴·화면 경로 | SB 운영관리 > 시스템 관리 > 업무 리스트 등록 · `/system-management/work/register/:id` · 경로 변수 `id` |
| 화면 유형·담당 | 상세 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [업무 리스트 등록](work__register.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/system-management/work/register` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `id` |
| 업무 팀원 조회 | `/system-management/work/register` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 업무리스트등록 상세 조회 | `/system-management/work/register` `VIEW` | `id: Long` |
| 업무리스트등록 수정 | `/system-management/work/register` `PROCESS` | `id: Long` · `WorkRegisterRequest` `taskName`, `assigneeId`, `repeatType`, `endDate`, `endWeekday`, `endHour`, `note` · 서버 필수 `taskName`, `assigneeId`, `repeatType` |
| 업무리스트등록 | `/system-management/work/register` `PROCESS` | `WorkRegisterRequest` `taskName`, `assigneeId`, `repeatType`, `endDate`, `endWeekday`, `endHour`, `note` · 서버 필수 `taskName`, `assigneeId`, `repeatType` |

코드에서 확인한 버튼·작업명은 **저장**, **목록**, **확인**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [업무 리스트 등록](work__register.md)에서 대상 또는 작업을 선택한다. `/system-management/work/register/:id`에서 이전 화면이 전달한 `id`와 현재 대상을 확인한다.
2. **매월** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **저장**, **확인** 중 해당 버튼을 선택한다.
3. **업무리스트등록 상세 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [업무 리스트 등록](work__register.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `id` |
| 선택 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/TeamWorkRegisterPage.tsx#L370) |
| 매월 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/TeamWorkRegisterPage.tsx#L87) |
| 요일 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/TeamWorkRegisterPage.tsx#L432) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 업무 팀원 조회 | `GET /api/v1/system-management/work/team-members` · `/system-management/work/register` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/operations/system/workregister/WorkRegisterController.kt#L63) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `id`, `name` | `office.dbo.TO_DO_TASK_LIST`, `office.dbo.SAWON` |
| 업무리스트등록 상세 조회 | `GET /api/v1/system-management/work/register/{id}` · `/system-management/work/register` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/operations/system/workregister/WorkRegisterController.kt#L69) | `id: Long` → `success`, `data`, `error`, `id`, `taskName`, `assigneeId`, `assigneeName`, `repeatType`, `endDate`, `endWeekday`, `endHour`, `note` | `office.dbo.upGW_TODOINSERT_LIST_MOD` |
| 업무리스트등록 수정 | `PUT /api/v1/system-management/work/register/{id}` · `/system-management/work/register` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/operations/system/workregister/WorkRegisterController.kt#L87) | `id: Long` · `WorkRegisterRequest` `taskName`, `assigneeId`, `repeatType`, `endDate`, `endWeekday`, `endHour`, `note` · 서버 필수 `taskName`, `assigneeId`, `repeatType` → `success`, `data`, `error`, `message` | `office.dbo.upGW_TODOLIST_INSERT_SAV`, `office.dbo.upGW_TODOLIST_UPDATE_SAV` · 정의에서 확인한 쓰기 `office.dbo.TO_DO_TASK_LIST` · 코드 연계 트랜잭션 |
| 업무리스트등록 | `POST /api/v1/system-management/work/register` · `/system-management/work/register` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/operations/system/workregister/WorkRegisterController.kt#L78) | `WorkRegisterRequest` `taskName`, `assigneeId`, `repeatType`, `endDate`, `endWeekday`, `endHour`, `note` · 서버 필수 `taskName`, `assigneeId`, `repeatType` → `success`, `data`, `error`, `message` | `office.dbo.upGW_TODOLIST_INSERT_SAV`, `office.dbo.upGW_TODOLIST_UPDATE_SAV` · 정의에서 확인한 쓰기 `office.dbo.TO_DO_TASK_LIST` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `office.dbo.TO_DO_TASK_LIST` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/system/workregister/repository/WorkRegisterMapper.kt#L82) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-1866cbc771e224d3) |
| `office.dbo.SAWON` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/system/workregister/repository/WorkRegisterMapper.kt#L82) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3a9ea6e368df5cb3) |
| `office.dbo.upGW_TODOINSERT_LIST_MOD` | @TASK_SEQ varchar(5) | 정의 참조 `office.dbo.SAWON`, `office.dbo.TO_DO_TASK_LIST` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/system/workregister/repository/WorkRegisterMapper.kt#L23) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-7c20654237a80fae) |
| `office.dbo.upGW_TODOLIST_INSERT_SAV` | @TASK_NAME varchar(100), @SW_NO varchar(5), @EDATE varchar(100), @EDATE_TIME varchar(5), @DATE_CHECK varchar(1), @REMARK varchar(500) = NULL, @CHECK_DAY varchar(10) = NULL | 정의 참조 `office.dbo.TO_DO_TASK_LIST` · 정적 쓰기 `office.dbo.TO_DO_TASK_LIST` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/system/workregister/repository/WorkRegisterMapper.kt#L27) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-d235df0a364f3c30) |
| `office.dbo.upGW_TODOLIST_UPDATE_SAV` | @TASK_NAME varchar(100), @SW_NO varchar(5), @EDATE varchar(100), @EDATE_TIME varchar(5), @DATE_CHECK varchar(1), @REMARK varchar(500), @TASK_SEQ varchar(5), @CHECK_DAY varchar(10) | 정의 참조 `office.dbo.TO_DO_TASK_LIST` · 정적 쓰기 `office.dbo.TO_DO_TASK_LIST` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/system/workregister/repository/WorkRegisterMapper.kt#L39) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-8a0b040de4a7259f) |

### 매퍼 호출 추가 확인

| DB 객체 | 호출 근거 | 개발 DB 확인 범위 |
| --- | --- | --- |
| [office.dbo.upGW_TODOLIST_MEMBER](../../references/all-pages-demo.md#object-aaef5c18425c3500) | [selectTeamMembers](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/system/workregister/repository/WorkRegisterMapper.kt#L63) | 개발 카탈로그 확인 |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 매월 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 운영관리 > 시스템 관리 > 업무 리스트 등록의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 팀원 목록을 불러올 수 없습니다. | 매월 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 업무 정보를 불러오는데 실패했습니다. | 매월 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 월간 업무는 현재 화면에서 수정할 수 없습니다. | 매월 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 팀원 업무 저장에 실패했습니다. | 매월 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/OperationsRoutes.tsx#L80) · [TeamWorkRegisterPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/TeamWorkRegisterPage.tsx#L108) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/api/workListApi.ts#L59) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/api/workListApi.ts#L68) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/api/workListApi.ts#L79) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/api/workListApi.ts#L81) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 5개 중 개발 메타데이터 확인 5개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-fbb2c042331b0de9) | Demo 메타데이터 6/6개 확인 · Dev와 계약 차이 2개 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

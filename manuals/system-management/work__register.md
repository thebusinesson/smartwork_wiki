# [업무·개선 요청·식별자·접속 기록] 업무 리스트 등록 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

업무 등록 목록을 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 업무·개선 요청·식별자·접속 기록 |
| 언제 사용하는가 | 업무리스트등록 조회 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 순번, 업 무 명, 업무담당자, 종료예정일, 종료예정시간, 상시체크 |
| 업무 흐름 | 업무리스트등록 조회 |
| 이 페이지의 역할 | 조회 · 업무리스트등록 조회 |
| 판단 결과·다음 업무 | [업무 등록](work__register__new.md) · [업무 리스트 등록 상세](work__register__by-id.md) |
| 다른 화면과의 구분 | 이 경로에서 볼 수 있는 조건·결과를 기준으로 사용한다. 독립 경로의 상세·등록은 관련 화면에 연결한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 업무 등록 목록을 조회한다. |
| 메뉴·화면 경로 | SB 운영관리 > 시스템 관리 > 업무 리스트 등록 · `/system-management/work/register` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [업무 등록](work__register__new.md) · [업무 리스트 등록 상세](work__register__by-id.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/system-management/work/register` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 업무리스트등록 조회 | `/system-management/work/register` `VIEW` | `page: Int?` · `pageSize: Int?` |
| 업무담당자 원문 조회 | `/system-management/work/register` / `UNMASK` | `id`, `field` |

코드에서 확인한 버튼·작업명은 **팀원 업무 등록**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **SB 운영관리 > 시스템 관리 > 업무 리스트 등록**를 연다. `/system-management/work/register`를 연다.
2. **업무리스트등록 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
3. 후속 조회나 목록 복귀가 필요하면 [업무 등록](work__register__new.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 순번 | 출력 | 조회 응답 기준 | 화면 필드 `order` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/WorkListRegisterPage.tsx#L29) |
| 업 무 명 | 출력 | 조회 응답 기준 | 화면 필드 `name` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/WorkListRegisterPage.tsx#L30) |
| 업무담당자 | 출력 | 조회 응답 기준 | 화면 필드 `owner` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/WorkListRegisterPage.tsx#L33) |
| 종료예정일 | 출력 | 조회 응답 기준 | 화면 필드 `dueTypeLabel` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/WorkListRegisterPage.tsx#L47) |
| 종료예정시간 | 출력 | 조회 응답 기준 | 화면 필드 `dueTimeLabel` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/WorkListRegisterPage.tsx#L48) |
| 상시체크 | 출력 | 조회 응답 기준 | 화면 필드 `alwaysCheckLabel` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/WorkListRegisterPage.tsx#L49) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 업무리스트등록 조회 | `GET /api/v1/system-management/work/register` · `/system-management/work/register` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/operations/system/workregister/WorkRegisterController.kt#L49) | `page: Int?` · `pageSize: Int?` → `success`, `data`, `error` | 코드 연계 트랜잭션 |
| 업무담당자 원문 조회 | `POST /api/v1/system-management/work/register/{id}/sensitive-values/reveal` · `/system-management/work/register` / `UNMASK` · [화면 컴포넌트](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/WorkListRegisterPage.tsx#L39) · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/operations/system/workregister/WorkRegisterController.kt#L107) | `id`, `field` → 요청한 항목의 원문 응답 | 권한 검사 후 대상 값을 조회하고 감사 기록을 남긴다. |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
### 매퍼 호출 추가 확인
| `office.dbo.upGW_TODOINSERT_LIST_MOD` | @TASK_SEQ varchar(5) IN | 원문 조회 또는 감사 흐름에서 호출 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/system/workregister/repository/WorkRegisterMapper.kt#L23) |
| `smartwork.dbo.usp_sw_log_access_event_insert` | @EVENT_TYPE varchar(30) IN, @STATUS varchar(20) IN, @USER_ID bigint IN, @MEMBER_ID nvarchar(50) IN, @USER_NAME nvarchar(100) IN, @DEPARTMENT_NAME nvarchar(100) IN, @PAGE_TITLE nvarchar(200) IN, @PATH nvarchar(500) IN, @MENU_PATH nvarchar(500) IN, @MENU_LABEL nvarchar(200) IN, @CATEGORY_NAME nvarchar(200) IN, @SUB_CATEGORY_NAME nvarchar(200) IN, @MENU_ORDER int IN, @IP_ADDRESS varchar(45) IN, @USER_AGENT nvarchar(1000) IN, @BROWSER varchar(100) IN, @OS varchar(100) IN, @REFERRER nvarchar(500) IN, @DETAIL nvarchar(1000) IN, @RESULT int OUT, @COUNTS_AS_VISIT bit IN | 원문 조회 또는 감사 흐름에서 호출 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/logmanagement/repository/LogManagementMapper.kt#L92) |

| DB 객체 | 호출 근거 | 개발 DB 확인 범위 |
| --- | --- | --- |
| [office.dbo.upGW_TODOINSERT_LIST](../../references/all-pages-demo.md#object-7c56efc5579e5e97) | [selectWorkTasks](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/system/workregister/repository/WorkRegisterMapper.kt#L19) | 개발 카탈로그 확인 |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 순번, 업 무 명, 업무담당자, 종료예정일, 종료예정시간, 상시체크 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 운영관리 > 시스템 관리 > 업무 리스트 등록의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/OperationsRoutes.tsx#L78) · [WorkListRegisterPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/WorkListRegisterPage.tsx#L52) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/api/workListApi.ts#L52) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 매퍼 호출 보완 · 개발 메타데이터 1/1개 확인 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-7cd3f572a3cbf723) | Demo 메타데이터 3/3개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

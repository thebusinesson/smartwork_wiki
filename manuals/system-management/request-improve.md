# [업무·개선 요청·식별자·접속 기록] 업무개선 및 요청리스트 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

요청/개선 항목 목록을 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 업무·개선 요청·식별자·접속 기록 |
| 언제 사용하는가 | 업무개선 및 요청리스트 조회 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 구분, 서비스, 제목, 상태, 등록일, 완료일 |
| 업무 흐름 | 업무개선 및 요청리스트 조회 |
| 이 페이지의 역할 | 조회 · 업무개선 및 요청리스트 조회 |
| 판단 결과·다음 업무 | [업무개선 및 요청리스트 상세](request-improve__by-id.md) · [요청 및 개선사항 등록](request-improve__new.md) · [요청 및 개선사항 수정](request-improve__by-id__edit.md) |
| 다른 화면과의 구분 | 이 경로에서 볼 수 있는 조건·결과를 기준으로 사용한다. 독립 경로의 상세·등록은 관련 화면에 연결한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 요청/개선 항목 목록을 조회한다. |
| 메뉴·화면 경로 | SB 운영관리 > 시스템 관리 > 업무개선 및 요청리스트 · `/system-management/request-improve` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [업무개선 및 요청리스트 상세](request-improve__by-id.md) · [요청 및 개선사항 등록](request-improve__new.md) · [요청 및 개선사항 수정](request-improve__by-id__edit.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/system-management/request-improve` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 업무개선 및 요청리스트 조회 | `/system-management/request-improve` `VIEW` | `fromDate: String?` · `toDate: String?` · `schCode: String?` · `status: String?` · `statuses: List<String>?` |
| 처리자·요청자 원문 조회 | `/system-management/request-improve` / `UNMASK` | `id`, `field` |

코드에서 확인한 버튼·작업명은 **검색**, **요청/개선 등록**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **SB 운영관리 > 시스템 관리 > 업무개선 및 요청리스트**를 연다. `/system-management/request-improve`를 연다.
2. **등록 일자**, **검토**, **요청**, **완료**, **폐기** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색**, **요청/개선 등록** 중 해당 버튼을 선택한다.
3. **업무개선 및 요청리스트 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [업무개선 및 요청리스트 상세](request-improve__by-id.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 구분 | 출력 | 조회 응답 기준 | API 응답 `type` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/RequestImproveListPage.tsx#L127) |
| 서비스 | 출력 | 조회 응답 기준 | API 응답 `service` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/RequestImproveListPage.tsx#L128) |
| 제목 | 출력 | 조회 응답 기준 | API 응답 `title` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/RequestImproveListPage.tsx#L129) |
| 상태 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | API 요청 `status` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/RequestImproveListPage.tsx#L132) |
| 등록일 | 출력 | 조회 응답 기준 | API 응답 `registeredAt` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/RequestImproveListPage.tsx#L146) |
| 완료일 | 출력 | 조회 응답 기준 | API 응답 `completedAt` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/RequestImproveListPage.tsx#L147) |
| 처리자 | 출력 | 조회 응답 기준 | API 응답 `handler` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/RequestImproveListPage.tsx#L151) |
| 요청자 | 출력 | 조회 응답 기준 | API 응답 `requester` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/RequestImproveListPage.tsx#L166) |
| 등록 일자 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/RequestImproveListPage.tsx#L48) |
| 검토 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `review` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/RequestImproveListPage.tsx#L63) |
| 요청 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `request` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/RequestImproveListPage.tsx#L64) |
| 완료 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `done` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/RequestImproveListPage.tsx#L65) |
| 폐기 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `discard` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/RequestImproveListPage.tsx#L66) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 업무개선 및 요청리스트 조회 | `GET /api/v1/system-management/request-improve` · `/system-management/request-improve` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/operations/system/requestimprove/RequestImproveController.kt#L57) | `fromDate: String?` · `toDate: String?` · `schCode: String?` · `status: String?` · `statuses: List<String>?` → `success`, `data`, `error`, `content`, `totalElements`, `id`, `type`, `service`, `title`, `status`, `registeredAt`, `completedAt` | 코드 연계 트랜잭션 |
| 처리자·요청자 원문 조회 | `POST /api/v1/system-management/request-improve/{id}/sensitive-values/reveal` · `/system-management/request-improve` / `UNMASK` · [화면 컴포넌트](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/RequestImproveListPage.tsx#L171) · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/operations/system/requestimprove/RequestImproveController.kt#L144) | `id`, `field` → 요청한 항목의 원문 응답 | 권한 검사 후 대상 값을 조회하고 감사 기록을 남긴다. |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
### 매퍼 호출 추가 확인
| `office.dbo.upGW_REQUEST_LIST_DETAIL` | @IDX int IN | 원문 조회 또는 감사 흐름에서 호출 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/system/requestimprove/repository/RequestImproveMapper.kt#L76) |
| `smartwork.dbo.usp_sw_log_access_event_insert` | @EVENT_TYPE varchar(30) IN, @STATUS varchar(20) IN, @USER_ID bigint IN, @MEMBER_ID nvarchar(50) IN, @USER_NAME nvarchar(100) IN, @DEPARTMENT_NAME nvarchar(100) IN, @PAGE_TITLE nvarchar(200) IN, @PATH nvarchar(500) IN, @MENU_PATH nvarchar(500) IN, @MENU_LABEL nvarchar(200) IN, @CATEGORY_NAME nvarchar(200) IN, @SUB_CATEGORY_NAME nvarchar(200) IN, @MENU_ORDER int IN, @IP_ADDRESS varchar(45) IN, @USER_AGENT nvarchar(1000) IN, @BROWSER varchar(100) IN, @OS varchar(100) IN, @REFERRER nvarchar(500) IN, @DETAIL nvarchar(1000) IN, @RESULT int OUT, @COUNTS_AS_VISIT bit IN | 원문 조회 또는 감사 흐름에서 호출 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/logmanagement/repository/LogManagementMapper.kt#L92) |

| DB 객체 | 호출 근거 | 개발 DB 확인 범위 |
| --- | --- | --- |
| [office.dbo.SCH_REQUEST_LIST](../../references/all-pages-demo.md#object-2a6c6e550b1cfa99) | [selectRequestImproveList](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/system/requestimprove/repository/RequestImproveMapper.kt#L54) | @FROM_YYMMDD varchar(10) IN · @TO_YYMMDD varchar(10) IN · @SCHCODE varchar(1) IN |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 구분, 서비스, 제목, 상태, 등록일, 완료일 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 운영관리 > 시스템 관리 > 업무개선 및 요청리스트의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/OperationsRoutes.tsx#L60) · [RequestImproveListPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/RequestImproveListPage.tsx#L74) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/api/requestImproveApi.ts#L31) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 매퍼 호출 보완 · 개발 메타데이터 1/1개 확인 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-42bbbedd46b6fdd4) | Demo 메타데이터 3/3개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

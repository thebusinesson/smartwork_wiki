# [업무·개선 요청·식별자·접속 기록] 요청 및 개선사항 수정 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

요청/개선 항목을 수정한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 업무·개선 요청·식별자·접속 기록 |
| 언제 사용하는가 | 업무개선 및 요청 상세 조회, 업무개선 및 요청 수정 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 업무개선 및 요청 수정 |
| 업무 흐름 | 업무개선 및 요청 상세 조회, 업무개선 및 요청 수정 |
| 이 페이지의 역할 | 수정 · 업무개선 및 요청 수정 |
| 판단 결과·다음 업무 | [업무개선 및 요청리스트](request-improve.md) · [업무개선 및 요청리스트 상세](request-improve__by-id.md) |
| 다른 화면과의 구분 | SB 운영관리 > 시스템 관리 > 업무개선 및 요청리스트에서 사용하는 수정 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 요청/개선 항목을 수정한다. |
| 메뉴·화면 경로 | SB 운영관리 > 시스템 관리 > 업무개선 및 요청리스트 · `/system-management/request-improve/:id/edit` · 경로 변수 `id` |
| 화면 유형·담당 | 수정 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [업무개선 및 요청리스트](request-improve.md) · [업무개선 및 요청리스트 상세](request-improve__by-id.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/system-management/request-improve` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `id` |
| 업무개선 및 요청 상세 조회 | `/system-management/request-improve` `VIEW` | `id: Int` |
| 업무개선 및 요청 수정 | `/system-management/request-improve` `PROCESS` | `id: Int` · `RequestImproveUpdateRequest` `type`, `service`, `status`, `title`, `requestContent`, `processContent`, `handlerEmployeeNo` |

코드에서 확인한 버튼·작업명은 **취소**, **저장**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [업무개선 및 요청리스트](request-improve.md)에서 대상 또는 작업을 선택한다. `/system-management/request-improve/:id/edit`에서 이전 화면이 전달한 `id`와 현재 대상을 확인한다.
2. **업무개선 및 요청 수정**을 실행하기 전에 변경 대상과 입력값을 확인한다. 표시되는 **요청 및 개선사항이 저장되었습니다.** 메시지와 대상 상태를 확인한다.
3. 후속 조회나 목록 복귀가 필요하면 [업무개선 및 요청리스트 상세](request-improve__by-id.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `id` |
| 선택 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/RequestImproveEditPage.tsx#L273) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 업무개선 및 요청 상세 조회 | `GET /api/v1/system-management/request-improve/{id}` · `/system-management/request-improve` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/operations/system/requestimprove/RequestImproveController.kt#L81) | `id: Int` → `success`, `data`, `error`, `id`, `type`, `service`, `title`, `status`, `registeredAt`, `completedAt`, `handler`, `handlerEmployeeNo` | `office.dbo.upGW_REQUEST_LIST_DETAIL` |
| 업무개선 및 요청 수정 | `PUT /api/v1/system-management/request-improve/{id}` · `/system-management/request-improve` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/operations/system/requestimprove/RequestImproveController.kt#L99) | `id: Int` · `RequestImproveUpdateRequest` `type`, `service`, `status`, `title`, `requestContent`, `processContent`, `handlerEmployeeNo` → `success`, `data`, `error`, `id`, `type`, `service`, `title`, `status`, `registeredAt`, `completedAt`, `handler`, `handlerEmployeeNo` | `smartwork.dbo.upGW_REQUEST_LIST_DETAIL_MOD`, `office.dbo.upGW_REQUEST_LIST_DETAIL` · 정의에서 확인한 쓰기 `office.dbo.REQUEST_LIST` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `office.dbo.upGW_REQUEST_LIST_DETAIL` | @IDX int | 정의 참조 `office.dbo.DEPT`, `office.dbo.DEPT_DETAIL`, `office.dbo.REQUEST_LIST`, `office.dbo.SAWON` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/system/requestimprove/repository/RequestImproveMapper.kt#L76) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-0cd36322bbb61a82) |
| `smartwork.dbo.upGW_REQUEST_LIST_DETAIL_MOD` | @IDX int, @TYPE varchar(10), @SERVICE_NAME varchar(50), @TITLE varchar(100), @DETAIL varchar(max), @STATUS varchar(10), @INCHARGE int, @SW_NO int, @PROCESS_DETAIL varchar(max) | 정의 참조 `office.dbo.REQUEST_LIST` · 정적 쓰기 `office.dbo.REQUEST_LIST` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/system/requestimprove/repository/RequestImproveMapper.kt#L92) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-51c737e1a36811a8) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 업무개선 및 요청 수정 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 운영관리 > 시스템 관리 > 업무개선 및 요청리스트의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 저장에 실패했습니다. 다시 시도해 주세요. | 업무개선 및 요청 수정 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/OperationsRoutes.tsx#L63) · [RequestImproveEditPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/RequestImproveEditPage.tsx#L33) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/api/requestImproveApi.ts#L40) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/api/requestImproveApi.ts#L71) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 2개 중 개발 메타데이터 확인 2개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-2a890a9ae2de78ab) | Demo 메타데이터 2/2개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

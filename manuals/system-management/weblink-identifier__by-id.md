# [업무·개선 요청·식별자·접속 기록] 웹링크 식별자 관리 상세 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

웹링크 식별자 상세를 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 업무·개선 요청·식별자·접속 기록 |
| 언제 사용하는가 | 웹링크식별자 상세 조회, 웹링크식별자 변경 이력, 웹링크식별자 삭제 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 등록일, 등록자 |
| 업무 흐름 | 웹링크식별자 상세 조회, 웹링크식별자 변경 이력, 웹링크식별자 삭제 |
| 이 페이지의 역할 | 상세 · 웹링크식별자 상세 조회 |
| 판단 결과·다음 업무 | [웹링크 식별자 관리](weblink-identifier.md) · [웹링크 식별자 수정](weblink-identifier__by-id__edit.md) |
| 다른 화면과의 구분 | SB 운영관리 > 시스템 관리 > 웹링크 식별자 관리에서 사용하는 상세 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 변경일시 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/WeblinkChangeHistoryLayer.tsx#L74) |
| 변경항목 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/WeblinkChangeHistoryLayer.tsx#L77) |
| 변경 전 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/WeblinkChangeHistoryLayer.tsx#L80) |
| 변경 후 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/WeblinkChangeHistoryLayer.tsx#L83) |
| 등록자 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/WeblinkChangeHistoryLayer.tsx#L86) |
| 변경 이력이 없습니다. | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/WeblinkChangeHistoryLayer.tsx#L104) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 웹링크 식별자 상세를 조회한다. |
| 메뉴·화면 경로 | SB 운영관리 > 시스템 관리 > 웹링크 식별자 관리 · `/system-management/weblink-identifier/:id` · 경로 변수 `id` |
| 화면 유형·담당 | 상세 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [웹링크 식별자 관리](weblink-identifier.md) · [웹링크 식별자 수정](weblink-identifier__by-id__edit.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/system-management/weblink-identifier` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `id` |
| 웹링크식별자 상세 조회 | `/system-management/weblink-identifier` `VIEW` | `id: String` |
| 웹링크식별자 변경 이력 | `/system-management/weblink-identifier` `VIEW` | `id: String` |
| 웹링크식별자 삭제 | `/system-management/weblink-identifier` `DELETE` | `id: String` · `WeblinkIdentifierDeleteRequest` `deleteReason` · 서버 필수 `deleteReason` |
| 변경 이력 등록자 원문 조회 | `/system-management/weblink-identifier` / `UNMASK` | `id`, `historyId`, `field` |

코드에서 확인한 버튼·작업명은 **변경 이력 보기**, **수정**, **삭제**, **목록**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [웹링크 식별자 관리](weblink-identifier.md)에서 대상 또는 작업을 선택한다. `/system-management/weblink-identifier/:id`에서 이전 화면이 전달한 `id`와 현재 대상을 확인한다.
2. **웹링크식별자 상세 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
3. 후속 조회나 목록 복귀가 필요하면 [웹링크 식별자 수정](weblink-identifier__by-id__edit.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `id` |
| 등록일 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/WeblinkIdentifierDetailPage.tsx#L167) |
| 등록자 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/WeblinkIdentifierDetailPage.tsx#L169) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 웹링크식별자 상세 조회 | `GET /api/v1/system-management/weblink-identifier/{id}` · `/system-management/weblink-identifier` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/operations/system/weblinkidentifier/WeblinkIdentifierController.kt#L94) | `id: String` → `success`, `data`, `error`, `id`, `confirmKey`, `comRegno`, `callDomain`, `buttonControl`, `returnPage`, `viewType`, `createdAt`, `createdBy` | `SB_DTI.dbo.COMPANY_WEBLINK` |
| 웹링크식별자 변경 이력 | `GET /api/v1/system-management/weblink-identifier/{id}/history` · `/system-management/weblink-identifier` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/operations/system/weblinkidentifier/WeblinkIdentifierController.kt#L136) | `id: String` → `success`, `data`, `error`, `histories` | `smartwork.dbo.system_weblink_identifier_history` |
| 웹링크식별자 삭제 | `DELETE /api/v1/system-management/weblink-identifier/{id}` · `/system-management/weblink-identifier` `DELETE` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/operations/system/weblinkidentifier/WeblinkIdentifierController.kt#L123) | `id: String` · `WeblinkIdentifierDeleteRequest` `deleteReason` · 서버 필수 `deleteReason` → `success`, `data`, `error` | `SB_DTI.dbo.COMPANY_WEBLINK`, `smartwork.dbo.system_weblink_identifier_history` · 정의에서 확인한 쓰기 `SB_DTI.dbo.COMPANY_WEBLINK`, `smartwork.dbo.system_weblink_identifier_history` · 코드 연계 트랜잭션 |
| 변경 이력 등록자 원문 조회 | `POST /api/v1/system-management/weblink-identifier/{id}/history/{historyId}/sensitive-values/reveal` · `/system-management/weblink-identifier` / `UNMASK` · [화면 컴포넌트](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/WeblinkChangeHistoryLayer.tsx#L130) · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/operations/system/weblinkidentifier/WeblinkIdentifierController.kt#L145) | `id`, `historyId`, `field` → 요청한 항목의 원문 응답 | 권한 검사 후 대상 값을 조회하고 감사 기록을 남긴다. |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `SB_DTI.dbo.COMPANY_WEBLINK` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/system/weblinkidentifier/repository/WeblinkIdentifierMapper.kt#L61) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-8d10682b1d32273c) |
| `smartwork.dbo.system_weblink_identifier_history` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/system/weblinkidentifier/repository/WeblinkIdentifierMapper.kt#L141) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-201adaf1cc380c36) |
| `smartwork.dbo.usp_sw_log_access_event_insert` | @EVENT_TYPE varchar(30) IN, @STATUS varchar(20) IN, @USER_ID bigint IN, @MEMBER_ID nvarchar(50) IN, @USER_NAME nvarchar(100) IN, @DEPARTMENT_NAME nvarchar(100) IN, @PAGE_TITLE nvarchar(200) IN, @PATH nvarchar(500) IN, @MENU_PATH nvarchar(500) IN, @MENU_LABEL nvarchar(200) IN, @CATEGORY_NAME nvarchar(200) IN, @SUB_CATEGORY_NAME nvarchar(200) IN, @MENU_ORDER int IN, @IP_ADDRESS varchar(45) IN, @USER_AGENT nvarchar(1000) IN, @BROWSER varchar(100) IN, @OS varchar(100) IN, @REFERRER nvarchar(500) IN, @DETAIL nvarchar(1000) IN, @RESULT int OUT, @COUNTS_AS_VISIT bit IN | 원문 조회 또는 감사 흐름에서 호출 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/logmanagement/repository/LogManagementMapper.kt#L92) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 등록일, 등록자 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 운영관리 > 시스템 관리 > 웹링크 식별자 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 웹링크 식별자 정보를 불러올 수 없습니다. | 등록일, 등록자 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 웹링크 식별자 삭제에 실패했습니다. | 등록일, 등록자 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 웹링크 식별자 삭제가 취소되었습니다. | 등록일, 등록자 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/OperationsRoutes.tsx#L83) · [WeblinkIdentifierDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/WeblinkIdentifierDetailPage.tsx#L18) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/api/weblinkIdentifierApi.ts#L43) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/api/weblinkIdentifierApi.ts#L101) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/api/weblinkIdentifierApi.ts#L58) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 2개 중 개발 메타데이터 확인 2개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-3896ba1b5d87e673) | Demo 메타데이터 3/3개 확인 · Dev와 계약 차이 1개 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

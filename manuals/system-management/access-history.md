# [업무·개선 요청·식별자·접속 기록] 접속이력관리 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

운영 접속 이력을 접속일자와 담당자 기준으로 조회한다. 목록에서 선택한 기록의 상세를 확인할 수 있다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 업무·개선 요청·식별자·접속 기록 |
| 언제 사용하는가 | 접속이력관리 조회 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 접속일자, 담당자 ID와 담당자명 |
| 업무 흐름 | 접속이력관리 조회 |
| 이 페이지의 역할 | 이력 조회 · 접속이력관리 조회 |
| 판단 결과·다음 업무 | [접속이력관리 상세](access-history__by-id.md) |
| 다른 화면과의 구분 | 이 경로에서 볼 수 있는 조건·결과를 기준으로 사용한다. 독립 경로의 상세·등록은 관련 화면에 연결한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 운영 접속 이력을 접속일자와 담당자 기준으로 조회한다. 목록에서 선택한 기록의 상세를 확인할 수 있다. |
| 메뉴·화면 경로 | SB 운영관리 > 시스템 관리 > 접속이력관리 · `/system-management/access-history` |
| 화면 유형·담당 | 이력 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [접속이력관리 상세](access-history__by-id.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/system-management/access-history` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 접속이력관리 조회 | `/system-management/access-history` `VIEW` | `date: String?` |

코드에서 확인한 버튼·작업명은 **검색**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **SB 운영관리 > 시스템 관리 > 접속이력관리**를 연다. `/system-management/access-history`를 연다.
2. **조회 일자** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색** 중 해당 버튼을 선택한다.
3. **접속이력관리 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [접속이력관리 상세](access-history__by-id.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 접속일자 | 출력 | 조회 응답 기준 | API 응답 `accessDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/AccessHistoryPage.tsx#L73) |
| 담당자 ID | 출력 | 조회 응답 기준 | API 응답 `userId` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/AccessHistoryPage.tsx#L76) |
| 담당자명 | 출력 | 조회 응답 기준 | API 응답 `userName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/AccessHistoryPage.tsx#L91) |
| 접속 횟수 | 출력 | 조회 응답 기준 | API 응답 `accessCount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/AccessHistoryPage.tsx#L104) |
| 조회 일자 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/AccessHistoryPage.tsx#L29) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 접속이력관리 조회 | `GET /api/v1/system-management/access-history` · `/system-management/access-history` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/operations/system/accesshistory/AccessHistoryController.kt#L45) | `date: String?` → `success`, `data`, `error`, `content`, `totalElements`, `accessDate`, `userKey`, `userId`, `userName`, `accessCount` | `smartwork.dbo.usp_sw_log_user_visit_rank_select` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.usp_sw_log_user_visit_rank_select` | @START_DATE varchar(10) = NULL, @END_DATE varchar(10) = NULL, @KEYWORD nvarchar(100) = NULL, @PAGE int = 1, @PAGE_SIZE int = 10 | 정의 참조 `smartwork.dbo.sw_log_access_event`, `smartwork.dbo.sw_log_page_visit_daily_fact`, `smartwork.dbo.sw_log_page_visit_total_fact` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/logmanagement/repository/LogManagementMapper.kt#L236) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-8265d7ca9e9b95b2) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 접속일자, 담당자 ID와 담당자명 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 운영관리 > 시스템 관리 > 접속이력관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/OperationsRoutes.tsx#L75) · [AccessHistoryPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/AccessHistoryPage.tsx#L37) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/api/accessHistoryApi.ts#L24) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 1개 중 개발 메타데이터 확인 1개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-711f559411488831) | Demo 메타데이터 1/1개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

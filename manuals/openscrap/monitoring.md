# [오픈스크랩 대상·수집과 결과] 모니터링 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

오픈스크랩 수집 실행을 스케줄러 자동실행과 사용자 수동 실행으로 나누어 조회한다. 사업자·시작·종료·오류 여부로 실행 건을 찾아 로그보기로 이동한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 오픈스크랩 대상·수집과 결과 |
| 언제 사용하는가 | 스케줄러 자동실행 모니터링 목록, 사용자 수동실행 모니터링 목록 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 실행 구분, 사업자번호, 회사명, 시작·종료, 오류발생 |
| 업무 흐름 | 스케줄러 자동실행 모니터링 목록, 사용자 수동실행 모니터링 목록 |
| 이 페이지의 역할 | 모니터링 · 스케줄러 자동실행 모니터링 목록 |
| 판단 결과·다음 업무 | [모니터링 상세](monitoring__by-batchId.md) |
| 다른 화면과의 구분 | 이 경로에서 볼 수 있는 조건·결과를 기준으로 사용한다. 독립 경로의 상세·등록은 관련 화면에 연결한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 스케줄러 자동실행 | 정기 수집을 조사할 때 | 자동으로 요청된 배치 | 로그보기에서 실행 건을 확인한다. |
| 사용자 수동 실행 | 운영자가 요청한 수집을 조사할 때 | 수동 수집 배치 | 로그보기에서 해당 요청의 처리 기록을 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 오픈스크랩 수집 실행을 스케줄러 자동실행과 사용자 수동 실행으로 나누어 조회한다. 사업자·시작·종료·오류 여부로 실행 건을 찾아 로그보기로 이동한다. |
| 메뉴·화면 경로 | SB 서비스관리 > 오픈스크랩 > 모니터링 · `/openscrap/monitoring` |
| 화면 유형·담당 | 모니터링 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [모니터링 상세](monitoring__by-batchId.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/openscrap/monitoring` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 스케줄러 자동실행 모니터링 목록 | `/openscrap/monitoring` `VIEW` | `MonitoringSearchRequest` `executionDate`, `hubVendorName`, `hubVendorSearchType`, `executionStatus`, `usageStatus`, `errorOccurrence`, `page`, `size` · 서버 필수 `executionDate` |
| 사용자 수동실행 모니터링 목록 | `/openscrap/monitoring` `VIEW` | `MonitoringSearchRequest` `executionDate`, `hubVendorName`, `hubVendorSearchType`, `executionStatus`, `usageStatus`, `errorOccurrence`, `page`, `size` · 서버 필수 `executionDate` |

코드에서 확인한 버튼·작업명은 **로그보기**, **검색**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **스케줄러 자동실행**과 **사용자 수동 실행**을 구분해 조사할 실행 구역을 연다.
2. 사업자번호·회사명과 시작·종료 일시를 대조하고 **오류발생** 표시를 확인한다.
3. 조사할 행의 **로그보기**를 눌러 실행 건별 상세 로그를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 사업자번호 | 출력 | 조회 응답 기준 | 화면 필드 `사업자번호` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/MonitoringListPage.tsx#L320) |
| 회사명 | 출력 | 조회 응답 기준 | 화면 필드 `회사명` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/MonitoringListPage.tsx#L323) |
| 시작 | 출력 | 조회 응답 기준 | 화면 필드 `시작일시` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/MonitoringListPage.tsx#L324) |
| 종료 | 출력 | 조회 응답 기준 | 화면 필드 `종료일시` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/MonitoringListPage.tsx#L325) |
| 오류발생 | 출력 | 조회 응답 기준 | 화면 필드 `오류발생여부` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/MonitoringListPage.tsx#L327) |
| 로그보기 | 출력 | 조회 응답 기준 | 화면 필드 `batchId` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/MonitoringListPage.tsx#L335) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 스케줄러 자동실행 모니터링 목록 | `GET /api/v1/openscrap/monitoring/scheduler` · `/openscrap/monitoring` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/openscrap/monitoring/MonitoringController.kt#L38) | `MonitoringSearchRequest` `executionDate`, `hubVendorName`, `hubVendorSearchType`, `executionStatus`, `usageStatus`, `errorOccurrence`, `page`, `size` · 서버 필수 `executionDate` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `page`, `size` | `smartwork.dbo.usp_os_eventlog_select` · 코드 연계 트랜잭션 |
| 사용자 수동실행 모니터링 목록 | `GET /api/v1/openscrap/monitoring/manual` · `/openscrap/monitoring` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/openscrap/monitoring/MonitoringController.kt#L48) | `MonitoringSearchRequest` `executionDate`, `hubVendorName`, `hubVendorSearchType`, `executionStatus`, `usageStatus`, `errorOccurrence`, `page`, `size` · 서버 필수 `executionDate` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `page`, `size` | `smartwork.dbo.usp_os_eventlog_select` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.usp_os_eventlog_select` | @PAGE int = 1, @PAGE_SIZE int = 10, @OS_USEDATE varchar(10), @OS_POLLINGTYPE char(1), @SEARCH_TYPE char(1), @SEARCH_TEXT varchar(50), @OS_USEYN char(1), @OS_STATUS char(1), @OS_RUNYN char(1) | 정의 참조 `SmartBill3.dbo.COMPANY`, `SB_DTI.dbo.NEOBILL_AUTHCODE`, `SB_OPENSCRAP.dbo.OS_COMPANY_INFO`, `SB_OPENSCRAP.dbo.OS_COMPANY_INFO_SCHEDULER`, `SB_OPENSCRAP.dbo.OS_EVENT_LOG` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/openscrap/monitoring/repository/MonitoringMapper.kt#L44) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-57f7fc2539afc4dc) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 실행 구분, 사업자번호, 회사명, 시작·종료, 오류발생 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 서비스관리 > 오픈스크랩 > 모니터링의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/OpenscrapRoutes.tsx#L12) · [MonitoringListPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/MonitoringListPage.tsx#L150) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/MonitoringListPage.tsx#L180) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/MonitoringListPage.tsx#L214) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 1개 중 개발 메타데이터 확인 1개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-b95dcda1f65c94af) | Demo 메타데이터 1/1개 확인 · 2026-11-11 |
| 화면 재현 | [로컬 Playwright 표본](../../evidence/browser/all-pages-sample-2026-11-11.json) | 진입 및 표시 확인 · 표시 스케줄러 자동실행, 사용자 수동 실행 · 2026-11-11 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

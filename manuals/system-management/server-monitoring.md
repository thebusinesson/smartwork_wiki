# [서버·시스템·연동 서버 관측] 연동 서버 모니터링 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

라우팅 결과 비정상 건을 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 서버·시스템·연동 서버 관측 |
| 언제 사용하는가 | 연동서버 모니터링 조회, 연동서버 모니터링 상태 갱신 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 일자/회차, 회차, 1회차, 2회차, 3회차, 4회차 |
| 업무 흐름 | 연동서버 모니터링 조회, 연동서버 모니터링 상태 갱신 |
| 이 페이지의 역할 | 모니터링 · 연동서버 모니터링 조회 |
| 판단 결과·다음 업무 | [허브업체 서비스 점검 관리 상세](../hub-service/maintenance__by-id.md) |
| 다른 화면과의 구분 | 이 경로에서 볼 수 있는 조건·결과를 기준으로 사용한다. 독립 경로의 상세·등록은 관련 화면에 연결한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 라우팅 결과 비정상 건을 조회한다. |
| 메뉴·화면 경로 | SB 운영관리 > 시스템 관리 > 연동 서버 모니터링 · `/system-management/server-monitoring` |
| 화면 유형·담당 | 모니터링 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [허브업체 서비스 점검 관리 상세](../hub-service/maintenance__by-id.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/system-management/server-monitoring` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 연동서버 모니터링 조회 | `/system-management/server-monitoring` `VIEW` | `date: String?` · `round: Int?` |
| 연동서버 모니터링 상태 갱신 | `/system-management/server-monitoring` `PROCESS` | `ServerMonitoringStatusRefreshRequest` `date`, `round` |

코드에서 확인한 버튼·작업명은 **검색**, **상태 갱신**, **목록 갱신**, **전체 보기**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **SB 운영관리 > 시스템 관리 > 연동 서버 모니터링**를 연다. `/system-management/server-monitoring`를 연다.
2. **일자/회차**, **회차**, **1회차**, **2회차**, **3회차**, **4회차** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색** 중 해당 버튼을 선택한다.
3. **연동서버 모니터링 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [허브업체 서비스 점검 관리 상세](../hub-service/maintenance__by-id.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 일자/회차 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/SystemServerMonitoringPage.tsx#L42) |
| 회차 | 입력 또는 선택 | API 기본값 null | API 요청 `round` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/SystemServerMonitoringPage.tsx#L48) |
| 1회차 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `1` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/SystemServerMonitoringPage.tsx#L50) |
| 2회차 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `2` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/SystemServerMonitoringPage.tsx#L51) |
| 3회차 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `3` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/SystemServerMonitoringPage.tsx#L52) |
| 4회차 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `4` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/SystemServerMonitoringPage.tsx#L53) |
| 허브업체명 | 출력 | 조회 응답 기준 | 화면 필드 `hubName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/components/ServerMonitoringTable.tsx#L59) |
| 업체URL | 출력 | 조회 응답 기준 | API 응답 `url` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/components/ServerMonitoringTable.tsx#L78) |
| 모니터링시간 | 출력 | 조회 응답 기준 | 화면 필드 `monitorDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/components/ServerMonitoringTable.tsx#L91) |
| 설명 | 출력 | 조회 응답 기준 | 화면 필드 `description` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/components/ServerMonitoringTable.tsx#L103) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 연동서버 모니터링 조회 | `GET /api/v1/system-management/server-monitoring` · `/system-management/server-monitoring` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/operations/system/servermonitoring/ServerMonitoringController.kt#L31) | `date: String?` · `round: Int?` → `success`, `data`, `error`, `content`, `totalElements`, `bnsSite`, `url`, `result`, `flag`, `cdate`, `udate`, `port` | `smartwork.dbo.upAdmSB_AUTOLstRouting_result_view`, `SB_DTI_LOG.dbo.MonitorRouting_Result`, `SB_DTI.dbo.COMPANY_LINK_OUT`, `SB_DTI.dbo.NEOBILL_COMPANY_LINK_OUT`, `SmartBill3.dbo.COMPANY` 외 5개 · 코드 연계 트랜잭션 |
| 연동서버 모니터링 상태 갱신 | `POST /api/v1/system-management/server-monitoring/status-refresh` · `/system-management/server-monitoring` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/operations/system/servermonitoring/ServerMonitoringController.kt#L40) | `ServerMonitoringStatusRefreshRequest` `date`, `round` → `success`, `data`, `error`, `content`, `totalElements`, `bnsSite`, `url`, `result`, `flag`, `cdate`, `udate`, `port` | `SB_DTI_LOG.dbo.MonitorRouting_Result`, `smartwork.dbo.upAdmSB_AUTOLstRouting_Result`, `smartwork.dbo.usp_sw_log_system_event_insert`, `SB_DTI.dbo.COMPANY_LINK_OUT`, `SB_DTI.dbo.NEOBILL_COMPANY_LINK_OUT` 외 6개 · 정의에서 확인한 쓰기 `SB_DTI_LOG.dbo.MonitorRouting_Result`, `smartwork.dbo.sw_log_system_event` · 코드 연계 비동기 처리, 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.upAdmSB_AUTOLstRouting_result_view` | @TODT varchar(10), @FLAG_NUM int | 정의 참조 `SB_DTI_LOG.dbo.MonitorRouting_Result` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/system/servermonitoring/repository/ServerMonitoringMapper.kt#L31) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-f602902979f98066) |
| `SB_DTI_LOG.dbo.MonitorRouting_Result` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/system/servermonitoring/repository/ServerMonitoringMapper.kt#L41) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-a0e38b80098b52e9) |
| `SB_DTI.dbo.COMPANY_LINK_OUT` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/hubservicemaintenance/repository/HubServiceMaintenanceMapper.kt#L82) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-220f523f160d6282) |
| `SB_DTI.dbo.NEOBILL_COMPANY_LINK_OUT` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/hubservicemaintenance/repository/HubServiceMaintenanceMapper.kt#L82) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b635b6a16ec47328) |
| `SmartBill3.dbo.COMPANY` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/hubservicemaintenance/repository/HubServiceMaintenanceMapper.kt#L82) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-0e6fcaa6b5086c07) |
| `office.dbo.MNG_HUB_DETAIL` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/hubservicemaintenance/repository/HubServiceMaintenanceMapper.kt#L82) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-4bcef15734f3fd87) |
| `office.dbo.MNG_HUB` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/hubservicemaintenance/repository/HubServiceMaintenanceMapper.kt#L82) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-bb97dfe4e2b8c3b3) |
| `office.dbo.BUSINESS` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/hubservicemaintenance/repository/HubServiceMaintenanceMapper.kt#L82) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-1c6a832844bf01aa) |
| `SB_DTI.dbo.DTI_ROUTING_ERROR_REG` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/hubservicemaintenance/repository/HubServiceMaintenanceMapper.kt#L82) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-055030ea1ba4d81a) |
| `office.dbo.SAWON` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/hubservicemaintenance/repository/HubServiceMaintenanceMapper.kt#L82) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3a9ea6e368df5cb3) |
| `smartwork.dbo.upAdmSB_AUTOLstRouting_Result` | @TODT varchar(10), @ROUTINGURL varchar(100), @SYSTYPE varchar(10), @BNS_ID int, @SAPCLIENTCODE varchar(3), @PORT varchar(5), @Result varchar(5), @flag int, @ResultDesc varchar(8000) | 정의 참조 `SB_DTI_LOG.dbo.MonitorRouting_Result` · 정적 쓰기 `SB_DTI_LOG.dbo.MonitorRouting_Result` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/system/servermonitoring/repository/ServerMonitoringMapper.kt#L118) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3465be630c07b1d5) |
| `smartwork.dbo.usp_sw_log_system_event_insert` | @LEVEL varchar(10), @CATEGORY varchar(30), @SOURCE nvarchar(200) = NULL, @MESSAGE nvarchar(1000), @REQUEST_PATH nvarchar(500) = NULL, @HTTP_METHOD varchar(10) = NULL, @USER_ID bigint = NULL, @MEMBER_ID nvarchar(50) = NULL, @STATUS_CODE int = NULL, @DURATION_MS bigint = NULL, @IP_ADDRESS varchar(45) = NULL, @USER_AGENT nvarchar(1000) = NULL, @DETAIL nvarchar(max) = NULL, @RESULT int OUT | 정의 참조 `smartwork.dbo.sw_log_system_event` · 정적 쓰기 `smartwork.dbo.sw_log_system_event` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/logmanagement/repository/LogManagementMapper.kt#L115) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-30344bbc069b2be3) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 일자/회차, 회차, 1회차, 2회차, 3회차, 4회차 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 운영관리 > 시스템 관리 > 연동 서버 모니터링의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/OperationsRoutes.tsx#L71) · [SystemServerMonitoringPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/SystemServerMonitoringPage.tsx#L61) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/api/serverMonitoringApi.ts#L39) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/api/serverMonitoringApi.ts#L79) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 12개 중 개발 메타데이터 확인 12개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-6e5c8934f5137c91) | Demo 메타데이터 12/12개 확인 · Dev와 계약 차이 2개 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

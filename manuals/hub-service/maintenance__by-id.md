# [연동 문의·점검·라우팅·복구] 허브업체 서비스 점검 관리 상세 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

현재 점검상태 + 포트목록(UspSelectHubRoutingPorts) + 이력(upDti_Routing_Error_Reg_history).

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 연동 문의·점검·라우팅·복구 |
| 언제 사용하는가 | 허브업체 점검 상세, 서비스 점검 등록/해제 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 허브업체명, 서버주소, 서비스 점검, 점검등록, 점검해제, 스마트빌 사용 |
| 업무 흐름 | 허브업체 점검 상세, 서비스 점검 등록/해제 |
| 이 페이지의 역할 | 상세 · 허브업체 점검 상세 |
| 판단 결과·다음 업무 | [허브업체 서비스 점검 관리](maintenance.md) |
| 다른 화면과의 구분 | 연동 서비스 관리 > 연동 서비스 관리 > 허브업체 서비스 점검 관리에서 사용하는 상세 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 현재 점검상태 + 포트목록(UspSelectHubRoutingPorts) + 이력(upDti_Routing_Error_Reg_history). |
| 메뉴·화면 경로 | 연동 서비스 관리 > 연동 서비스 관리 > 허브업체 서비스 점검 관리 · `/hub-service/maintenance/:id` · 경로 변수 `id` |
| 화면 유형·담당 | 상세 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [허브업체 서비스 점검 관리](maintenance.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/hub-service/maintenance` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `id` |
| 허브업체 점검 상세 | `/hub-service/maintenance` `VIEW` | `id: String` |
| 서비스 점검 등록/해제 | `/hub-service/maintenance` `PROCESS` | `id: String` · `ServiceCheckSaveRequest` `isActive`, `smartBillUsage`, `notificationMessage`, `startDate`, `startHour`, `endDate`, `endHour`, `port` |

코드에서 확인한 버튼·작업명은 **서비스 점검 등록**, **목록**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [허브업체 서비스 점검 관리](maintenance.md)에서 대상 또는 작업을 선택한다. `/hub-service/maintenance/:id`에서 이전 화면이 전달한 `id`와 현재 대상을 확인한다.
2. **점검등록**, **점검해제** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **서비스 점검 등록** 중 해당 버튼을 선택한다.
3. **허브업체 점검 상세** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [허브업체 서비스 점검 관리](maintenance.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `id` |
| 허브업체명 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/hubServiceMaintenance/components/detail/HubVendorInfoSection.tsx#L30) |
| 서버주소 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/hubServiceMaintenance/components/detail/HubVendorInfoSection.tsx#L36) |
| 선택 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/hubServiceMaintenance/components/detail/HubVendorInfoSection.tsx#L46) |
| 서비스 점검 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/hubServiceMaintenance/components/detail/ServiceMaintenanceFormSection.tsx#L67) |
| 점검등록 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/hubServiceMaintenance/components/detail/ServiceMaintenanceFormSection.tsx#L76) |
| 점검해제 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/hubServiceMaintenance/components/detail/ServiceMaintenanceFormSection.tsx#L82) |
| 스마트빌 사용 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/hubServiceMaintenance/components/detail/ServiceMaintenanceFormSection.tsx#L89) |
| 서비스 점검시간 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/hubServiceMaintenance/components/detail/ServiceMaintenanceFormSection.tsx#L106) |
| 알림 메세지 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/hubServiceMaintenance/components/detail/ServiceMaintenanceFormSection.tsx#L175) |
| 알림 메세지를 입력하세요 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/hubServiceMaintenance/components/detail/ServiceMaintenanceFormSection.tsx#L181) |
| 등록시간 | 출력 | 조회 응답 기준 | 화면 필드 `hisDateTime` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/hubServiceMaintenance/components/detail/MaintenanceHistoryTable.tsx#L19) |
| 등록/해제 | 출력 | 조회 응답 기준 | 화면 필드 `errorYn` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/hubServiceMaintenance/components/detail/MaintenanceHistoryTable.tsx#L20) |
| 시작시간 | 출력 | 조회 응답 기준 | 화면 필드 `fromDateTime` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/hubServiceMaintenance/components/detail/MaintenanceHistoryTable.tsx#L21) |
| 종료시간 | 출력 | 조회 응답 기준 | 화면 필드 `toDateTime` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/hubServiceMaintenance/components/detail/MaintenanceHistoryTable.tsx#L22) |
| SB 미사용(01)/사용(02) | 출력 | 조회 응답 기준 | 화면 필드 `sbUseCode` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/hubServiceMaintenance/components/detail/MaintenanceHistoryTable.tsx#L24) |
| 포트 | 입력 또는 선택 | API 기본값 "A" | API 요청 `port` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/hubServiceMaintenance/components/detail/MaintenanceHistoryTable.tsx#L32) |
| 등록자 | 출력 | 조회 응답 기준 | 화면 필드 `registrant` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/hubServiceMaintenance/components/detail/MaintenanceHistoryTable.tsx#L34) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 허브업체 점검 상세 | `GET /api/v1/hub-service-maintenance/{id}` · `/hub-service/maintenance` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/hubservicemaintenance/HubServiceMaintenanceController.kt#L73) | `id: String` → `success`, `data`, `error`, `maintenance`, `currentCheck`, `ports`, `history` | `SB_DTI.dbo.COMPANY_LINK_OUT`, `SB_DTI.dbo.NEOBILL_COMPANY_LINK_OUT`, `SmartBill3.dbo.COMPANY`, `office.dbo.MNG_HUB_DETAIL`, `office.dbo.MNG_HUB` 외 5개 |
| 서비스 점검 등록/해제 | `POST /api/v1/hub-service-maintenance/{id}/service-check` · `/hub-service/maintenance` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/hubservicemaintenance/HubServiceMaintenanceController.kt#L83) | `id: String` · `ServiceCheckSaveRequest` `isActive`, `smartBillUsage`, `notificationMessage`, `startDate`, `startHour`, `endDate`, `endHour`, `port` → `success`, `data`, `error`, `maintenance`, `currentCheck`, `ports`, `history` | `smartwork.dbo.UspSelectHubRoutingSyncStatus`, `SB_DTI.dbo.upDTI_ROUTING_ERROR_REG`, `SB_DTI.dbo.COMPANY_LINK_OUT`, `SB_DTI.dbo.NEOBILL_COMPANY_LINK_OUT`, `SmartBill3.dbo.COMPANY` 외 7개 · 정의에서 확인한 쓰기 `SB_DTI.dbo.DTI_ROUTING_ERROR_REG_HIS`, `SB_DTI.dbo.DTI_ROUTING_ERROR_REG` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `SB_DTI.dbo.COMPANY_LINK_OUT` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/hubservicemaintenance/repository/HubServiceMaintenanceMapper.kt#L82) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-220f523f160d6282) |
| `SB_DTI.dbo.NEOBILL_COMPANY_LINK_OUT` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/hubservicemaintenance/repository/HubServiceMaintenanceMapper.kt#L82) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b635b6a16ec47328) |
| `SmartBill3.dbo.COMPANY` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/hubservicemaintenance/repository/HubServiceMaintenanceMapper.kt#L82) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-0e6fcaa6b5086c07) |
| `office.dbo.MNG_HUB_DETAIL` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/hubservicemaintenance/repository/HubServiceMaintenanceMapper.kt#L82) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-4bcef15734f3fd87) |
| `office.dbo.MNG_HUB` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/hubservicemaintenance/repository/HubServiceMaintenanceMapper.kt#L82) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-bb97dfe4e2b8c3b3) |
| `office.dbo.BUSINESS` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/hubservicemaintenance/repository/HubServiceMaintenanceMapper.kt#L82) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-1c6a832844bf01aa) |
| `SB_DTI.dbo.DTI_ROUTING_ERROR_REG` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/hubservicemaintenance/repository/HubServiceMaintenanceMapper.kt#L82) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-055030ea1ba4d81a) |
| `office.dbo.SAWON` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/hubservicemaintenance/repository/HubServiceMaintenanceMapper.kt#L82) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3a9ea6e368df5cb3) |
| `smartwork.dbo.UspSelectHubRoutingPorts` | @ROUTINGURL varchar(100) | 정의 참조 `SB_DTI.dbo.COMPANY_LINK_OUT`, `SB_DTI.dbo.NEOBILL_COMPANY_LINK_OUT` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/hubservicemaintenance/repository/HubServiceMaintenanceMapper.kt#L103) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-4bcb9e29f7230af8) |
| `office.dbo.upDti_Routing_Error_Reg_history` | @ROUTINGURL varchar(50) | 정의 참조 `SB_DTI.dbo.DTI_ROUTING_ERROR_REG_HIS`, `office.dbo.SAWON` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/hubservicemaintenance/repository/HubServiceMaintenanceMapper.kt#L98) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-172bed083b168f3f) |
| `smartwork.dbo.UspSelectHubRoutingSyncStatus` | @ROUTINGURL varchar(100) | 정의 참조 `SB_DTI.dbo.DTI_ASYNC`, `SB_DTI.dbo.DTI_ROUTING_ERROR_REG` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/hubservicemaintenance/repository/HubServiceMaintenanceMapper.kt#L109) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-2a182668a5eca98f) |
| `SB_DTI.dbo.upDTI_ROUTING_ERROR_REG` | @ERROR_YN varchar(5), @ERROR_REG_SIG varchar(10), @PORT varchar(10), @ROUTINGURL varchar(50), @SW_NO varchar(10), @SB_USE_CODE varchar(5), @FROM_DATETIME varchar(30), @TO_DATETIME varchar(30), @ERROR_MSG varchar(1000) | 정의 참조 `SB_DTI.dbo.COMPANY_LINK_OUT`, `SB_DTI.dbo.DTI_ROUTING_ERROR_REG`, `SB_DTI.dbo.DTI_ROUTING_ERROR_REG_HIS`, `SB_DTI.dbo.NEOBILL_COMPANY_LINK_OUT` · 정적 쓰기 `SB_DTI.dbo.DTI_ROUTING_ERROR_REG_HIS`, `SB_DTI.dbo.DTI_ROUTING_ERROR_REG` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/hubservicemaintenance/repository/HubServiceMaintenanceSaveMapper.kt#L24) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-066478f0b048e83a) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 허브업체명, 서버주소, 서비스 점검, 점검등록, 점검해제, 스마트빌 사용 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 연동 서비스 관리 > 연동 서비스 관리 > 허브업체 서비스 점검 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 등록된 서비스 점검 이력이 없습니다. | 허브업체명, 서버주소, 서비스 점검, 점검등록, 점검해제, 스마트빌 사용 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/IntegrationRoutes.tsx#L133) · [HubServiceMaintenanceDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/hubServiceMaintenance/HubServiceMaintenanceDetailPage.tsx#L12) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/api/hubServiceMaintenanceApi.ts#L42) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/api/hubServiceMaintenanceApi.ts#L50) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 12개 중 개발 메타데이터 확인 12개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-c92fda7db81be20e) | Demo 메타데이터 12/12개 확인 · Dev와 계약 차이 4개 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

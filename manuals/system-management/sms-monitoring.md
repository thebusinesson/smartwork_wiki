# [시스템 메시지·발행·이메일 확인] 시스템 SMS 모니터링 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

SMS 모니터링 대상 목록을 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 시스템 메시지·발행·이메일 확인 |
| 언제 사용하는가 | 시스템 SMS 모니터링 조회, 시스템 SMS 모니터링 선택 항목 활성 상태 토글, 시스템 SMS 모니터링 대상 신규 등록 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 시스템 SMS 모니터링 조회 |
| 업무 흐름 | 시스템 SMS 모니터링 조회, 시스템 SMS 모니터링 선택 항목 활성 상태 토글, 시스템 SMS 모니터링 대상 신규 등록 |
| 이 페이지의 역할 | 모니터링 · 시스템 SMS 모니터링 조회 |
| 판단 결과·다음 업무 | 현재 화면에서 결과를 확인한다. |
| 다른 화면과의 구분 | 같은 경로에서 열리는 조회·팝업은 이 문서에서 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 저장 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/SmsMonitoringCreateDialog.tsx#L99) |
| 확인 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/SystemSmsMonitoringPage.tsx#L223) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | SMS 모니터링 대상 목록을 조회한다. |
| 메뉴·화면 경로 | SB 운영관리 > 시스템 관리 > 시스템 SMS 모니터링 · `/system-management/sms-monitoring` |
| 화면 유형·담당 | 모니터링 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | 현재 화면에서 결과를 확인한다. |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/system-management/sms-monitoring` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 시스템 SMS 모니터링 조회 | `/system-management/sms-monitoring` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 시스템 SMS 모니터링 선택 항목 활성 상태 토글 | `/system-management/sms-monitoring` `PROCESS` | `SmsMonitoringBulkToggleRequest` `targetAddresses` |
| 시스템 SMS 모니터링 대상 신규 등록 | `/system-management/sms-monitoring` `PROCESS` | `SmsMonitoringCreateRequest` `targetAddress`, `keyword`, `memo` |

코드에서 확인한 버튼·작업명은 **신규 등록**, **수정**, **저장**, **확인**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **SB 운영관리 > 시스템 관리 > 시스템 SMS 모니터링**를 연다. `/system-management/sms-monitoring`를 연다.
2. **시스템 SMS 모니터링 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 화면 표시 항목 | 미확인 | 공통 UI 또는 상태에 따라 표시 | [SystemSmsMonitoringPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/SystemSmsMonitoringPage.tsx#L28) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 시스템 SMS 모니터링 조회 | `GET /api/v1/system-management/sms-monitoring` · `/system-management/sms-monitoring` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/operations/system/smsmonitoring/SmsMonitoringController.kt#L31) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `content`, `totalElements`, `targetAddress`, `active`, `keyword`, `memo` | 코드 연계 트랜잭션 |
| 시스템 SMS 모니터링 선택 항목 활성 상태 토글 | `POST /api/v1/system-management/sms-monitoring/selected-active-toggle` · `/system-management/sms-monitoring` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/operations/system/smsmonitoring/SmsMonitoringController.kt#L37) | `SmsMonitoringBulkToggleRequest` `targetAddresses` → `success`, `data`, `error` | `office.dbo.UPADM_SB_SERVER_SMS_MONITOR_UPT_ONE` · 정의에서 확인한 쓰기 `SmartBill3.dbo.ServerMonitor_TargetsInfo` · 코드 연계 트랜잭션 |
| 시스템 SMS 모니터링 대상 신규 등록 | `POST /api/v1/system-management/sms-monitoring` · `/system-management/sms-monitoring` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/operations/system/smsmonitoring/SmsMonitoringController.kt#L47) | `SmsMonitoringCreateRequest` `targetAddress`, `keyword`, `memo` → `success`, `data`, `error` | `smartwork.dbo.UspInsertSmsMonitoringTarget` · 정의에서 확인한 쓰기 `SmartBill3.dbo.ServerMonitor_TargetsInfo` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `office.dbo.UPADM_SB_SERVER_SMS_MONITOR_UPT_ONE` | @SERVERIP varchar(80) | 정의 참조 `SmartBill3.dbo.ServerMonitor_TargetsInfo` · 정적 쓰기 `SmartBill3.dbo.ServerMonitor_TargetsInfo` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/system/smsmonitoring/repository/SmsMonitoringMapper.kt#L30) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-a95e060267f4c4b7) |
| `smartwork.dbo.UspInsertSmsMonitoringTarget` | @TARGET_ADDRESS varchar(600), @SUCCESS_WORD varchar(50), @MEMO varchar(30), @RESULT int OUT | 정의 참조 `SmartBill3.dbo.ServerMonitor_TargetsInfo` · 정적 쓰기 `SmartBill3.dbo.ServerMonitor_TargetsInfo` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/system/smsmonitoring/repository/SmsMonitoringMapper.kt#L34) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-e1e47be28414bfce) |

### 매퍼 호출 추가 확인

| DB 객체 | 호출 근거 | 개발 DB 확인 범위 |
| --- | --- | --- |
| [office.dbo.upAdm_sb_server_sms_monitor](../../references/all-pages-demo.md#object-844019674d60dd0a) | [selectSmsMonitoring](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/system/smsmonitoring/repository/SmsMonitoringMapper.kt#L26) | 개발 카탈로그 확인 |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 시스템 SMS 모니터링 조회 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 운영관리 > 시스템 관리 > 시스템 SMS 모니터링의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| SMS 모니터링 데이터를 불러오는데 실패했습니다. | 시스템 SMS 모니터링 조회 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| Active 상태 변경에 실패했습니다. | 시스템 SMS 모니터링 조회 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 변경이 취소되었습니다. | 시스템 SMS 모니터링 조회 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 데이터가 없습니다. | 시스템 SMS 모니터링 조회 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/OperationsRoutes.tsx#L67) · [SystemSmsMonitoringPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/SystemSmsMonitoringPage.tsx#L28) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/api/smsMonitoringApi.ts#L37) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/api/smsMonitoringApi.ts#L70) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/operations/system/api/smsMonitoringApi.ts#L56) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 2개 중 개발 메타데이터 확인 2개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-caceb4e9edb2395f) | Demo 메타데이터 3/3개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

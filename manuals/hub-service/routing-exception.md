# [연동 문의·점검·라우팅·복구] [구연동] 라우팅 예외 관리 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

[구연동] 라우팅 예외 관리에서 **라우팅 예외 목록 조회** 결과를 확인한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 연동 문의·점검·라우팅·복구 |
| 언제 사용하는가 | 라우팅 예외 목록 조회, 구연동 라우팅 예외 대상 등록, 라우팅 예외 선택 삭제, 라우팅 예외 완료건 삭제, 라우팅 예외 종료일 경과 건 삭제 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 시작시간, 종료시간, 등록 사유, 시작, 종료 |
| 업무 흐름 | 라우팅 예외 목록 조회, 구연동 라우팅 예외 대상 등록, 라우팅 예외 선택 삭제, 라우팅 예외 완료건 삭제, 라우팅 예외 종료일 경과 건 삭제 |
| 이 페이지의 역할 | 조회·관리 · 라우팅 예외 목록 조회 |
| 판단 결과·다음 업무 | 현재 화면에서 결과를 확인한다. |
| 다른 화면과의 구분 | 같은 경로에서 열리는 조회·팝업은 이 문서에서 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 확인 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/routingException/RoutingExceptionPage.tsx#L229) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | [구연동] 라우팅 예외 관리에서 **라우팅 예외 목록 조회** 결과를 확인한다. |
| 메뉴·화면 경로 | 연동 서비스 관리 > 연동 서비스 관리 > [구연동] 라우팅 예외 관리 · `/hub-service/routing-exception` |
| 화면 유형·담당 | 조회·관리 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | 현재 화면에서 결과를 확인한다. |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/hub-service/routing-exception` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 라우팅 예외 목록 조회 | `/hub-service/routing-exception` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 구연동 라우팅 예외 대상 등록 | `/hub-service/routing-exception` `PROCESS` | `RoutingExceptionCreateRequest` `division`, `conversationId`, `signal`, `ignoreStartDateTime`, `ignoreEndDateTime`, `reason` · 서버 필수 `division`, `conversationId`, `signal`, `ignoreStartDateTime`, `ignoreEndDateTime` |
| 라우팅 예외 선택 삭제 | `/hub-service/routing-exception` `DELETE` | `RoutingExceptionBulkDeleteRequest` `ids`, `reason` · 서버 필수 `ids`, `reason` |
| 라우팅 예외 완료건 삭제 | `/hub-service/routing-exception` `DELETE` | 추가 입력은 Controller 서명 참조 |
| 라우팅 예외 종료일 경과 건 삭제 | `/hub-service/routing-exception` `DELETE` | 추가 입력은 Controller 서명 참조 |

코드에서 확인한 버튼·작업명은 **라우팅 예외 등록**, **새로고침**, **선택 삭제**, **완료건 삭제**, **종료일 경과 건 삭제**, **확인**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **연동 서비스 관리 > 연동 서비스 관리 > [구연동] 라우팅 예외 관리**를 연다. `/hub-service/routing-exception`를 연다.
2. **시작시간**, **종료시간**, **등록 사유** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **라우팅 예외 등록**, **확인** 중 해당 버튼을 선택한다.
3. **라우팅 예외 목록 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| Conversation ID 입력 | 입력·필수 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/routingException/components/registration/RoutingExceptionRegistrationForm.tsx#L106) |
| 선택 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/routingException/components/registration/RoutingExceptionRegistrationForm.tsx#L129) |
| 시작시간 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/routingException/components/registration/RoutingExceptionRegistrationForm.tsx#L153) |
| 날짜 선택 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/routingException/components/registration/RoutingExceptionRegistrationForm.tsx#L195) |
| 시간 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/routingException/components/registration/RoutingExceptionRegistrationForm.tsx#L206) |
| 종료시간 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/routingException/components/registration/RoutingExceptionRegistrationForm.tsx#L189) |
| 등록 사유 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/routingException/components/registration/RoutingExceptionRegistrationForm.tsx#L224) |
| 등록 사유를 입력하세요 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/routingException/components/registration/RoutingExceptionRegistrationForm.tsx#L229) |
| 시작 | 입력·필수 | 화면 상태·입력 조건에 따라 표시 | API 요청 `ignoreStartDateTime` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/routingException/components/history/RoutingExceptionHistoryTable.tsx#L58) |
| 종료 | 입력·필수 | 화면 상태·입력 조건에 따라 표시 | API 요청 `ignoreEndDateTime` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/routingException/components/history/RoutingExceptionHistoryTable.tsx#L64) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 라우팅 예외 목록 조회 | `GET /api/v1/hub-service/routing-exception` · `/hub-service/routing-exception` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/routingexception/RoutingExceptionController.kt#L37) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `content`, `totalElements` | 코드 연계 트랜잭션 |
| 구연동 라우팅 예외 대상 등록 | `POST /api/v1/hub-service/routing-exception` · `/hub-service/routing-exception` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/routingexception/RoutingExceptionController.kt#L45) | `RoutingExceptionCreateRequest` `division`, `conversationId`, `signal`, `ignoreStartDateTime`, `ignoreEndDateTime`, `reason` · 서버 필수 `division`, `conversationId`, `signal`, `ignoreStartDateTime`, `ignoreEndDateTime` → `success`, `data`, `error`, `content`, `totalElements` | `SB_DTI_LOG.dbo.upSav_IGNOREROUTING` · 정의에서 확인한 쓰기 `SB_DTI_LOG.dbo.DTI_ROUTING_IGNORE` · 코드 연계 트랜잭션 |
| 라우팅 예외 선택 삭제 | `DELETE /api/v1/hub-service/routing-exception/bulk` · `/hub-service/routing-exception` `DELETE` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/routingexception/RoutingExceptionController.kt#L56) | `RoutingExceptionBulkDeleteRequest` `ids`, `reason` · 서버 필수 `ids`, `reason` → `success`, `data`, `error` | `SB_DTI_LOG.dbo.upDel_CHECKEDIGNOREROUTING`, `smartwork.dbo.action_reason` · 정의에서 확인한 쓰기 `smartwork.dbo.action_reason` · 코드 연계 트랜잭션 |
| 라우팅 예외 완료건 삭제 | `DELETE /api/v1/hub-service/routing-exception/completed` · `/hub-service/routing-exception` `DELETE` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/routingexception/RoutingExceptionController.kt#L67) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error` | 코드 연계 트랜잭션 |
| 라우팅 예외 종료일 경과 건 삭제 | `DELETE /api/v1/hub-service/routing-exception/old` · `/hub-service/routing-exception` `DELETE` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/routingexception/RoutingExceptionController.kt#L75) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error` | 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `SB_DTI_LOG.dbo.upSav_IGNOREROUTING` | @CONVERSATION_ID varchar(35), @SIGNAL varchar(30), @IGNORE_START_DATE datetime, @IGNORE_END_DATE datetime, @FLAG varchar(5), @CUSER_NAME varchar(50), @REASON varchar(500), @ROUTING_SYSTEM varchar(10) | 정의 참조 `SB_DTI_LOG.dbo.DTI_ROUTING_IGNORE` · 정적 쓰기 `SB_DTI_LOG.dbo.DTI_ROUTING_IGNORE` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/routingexception/repository/RoutingExceptionMapper.kt#L46) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-ec164004f22c2402) |
| `SB_DTI_LOG.dbo.upDel_CHECKEDIGNOREROUTING` | @IDX varchar(4000) | 정의 참조 `master.dbo.CLR_sqlsplit`, `SB_DTI_LOG.dbo.DTI_ROUTING_IGNORE` · 쓰기 구문 존재 · 대상 별칭 또는 하위 정의 확인 · 하위 호출 `master.dbo.CLR_sqlsplit` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/routingexception/repository/RoutingExceptionMapper.kt#L56) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-4be9daa38b0c3ba9) |
| `smartwork.dbo.action_reason` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL INSERT INTO | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/shared/actionreason/repository/ActionReasonMapper.kt#L16) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b0430106ffe0743f) |

### 매퍼 호출 추가 확인

| DB 객체 | 호출 근거 | 개발 DB 확인 범위 |
| --- | --- | --- |
| [SB_DTI_LOG.dbo.upSel_GETIGNOREROUTING](../../references/all-pages-demo.md#object-51e03ddea7dfe5ed) | [findAll](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/routingexception/repository/RoutingExceptionMapper.kt#L35) | 개발 카탈로그 확인 |
| [SB_DTI_LOG.dbo.upDel_FINISHIGNOREROUTING](../../references/all-pages-demo.md#object-ca87422f0b61da43) | [deleteFinished](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/routingexception/repository/RoutingExceptionMapper.kt#L60) | 개발 카탈로그 확인 |
| [SB_DTI_LOG.dbo.upDel_OLDLISTIGNOREROUTING](../../references/all-pages-demo.md#object-2734a5f9aa2c4939) | [deleteOld](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/routingexception/repository/RoutingExceptionMapper.kt#L64) | 개발 카탈로그 확인 |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 시작시간, 종료시간, 등록 사유, 시작, 종료 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 연동 서비스 관리 > 연동 서비스 관리 > [구연동] 라우팅 예외 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 검색 결과가 없습니다. | 시작시간, 종료시간, 등록 사유, 시작, 종료 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/IntegrationRoutes.tsx#L141) · [RoutingExceptionPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/routingException/RoutingExceptionPage.tsx#L23) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/api/routingExceptionApi.ts#L27) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/api/routingExceptionApi.ts#L35) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/api/routingExceptionApi.ts#L39) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/api/routingExceptionApi.ts#L43) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/api/routingExceptionApi.ts#L47) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 3개 중 개발 메타데이터 확인 3개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-3d93e00ab528914e) | Demo 메타데이터 6/6개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

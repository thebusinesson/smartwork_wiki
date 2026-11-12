# [연동 문의·점검·라우팅·복구] 연동업체 라우팅 일괄 변경 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

연동업체 라우팅 일괄 변경에서 **연동업체 라우팅 정보 검색** 결과를 확인한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 연동 문의·점검·라우팅·복구 |
| 언제 사용하는가 | 연동업체 라우팅 정보 검색, 연동업체 라우팅 정보 일괄 변경 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 라우팅 정보 검색 |
| 업무 흐름 | 연동업체 라우팅 정보 검색, 연동업체 라우팅 정보 일괄 변경 |
| 이 페이지의 역할 | 조회·관리 · 연동업체 라우팅 정보 검색 |
| 판단 결과·다음 업무 | 현재 화면에서 결과를 확인한다. |
| 다른 화면과의 구분 | 같은 경로에서 열리는 조회·팝업은 이 문서에서 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 연동업체 라우팅 일괄 변경에서 **연동업체 라우팅 정보 검색** 결과를 확인한다. |
| 메뉴·화면 경로 | 연동 서비스 관리 > 연동 서비스 관리 > 연동업체 라우팅 일괄 변경 · `/hub-service/vendor-routing-bulk-change` |
| 화면 유형·담당 | 조회·관리 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | 현재 화면에서 결과를 확인한다. |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/hub-service/vendor-routing-bulk-change` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 연동업체 라우팅 정보 검색 | `/hub-service/vendor-routing-bulk-change` `VIEW` | `VendorRoutingSearchRequest` `integrationType`, `ip`, `port` · 서버 필수 `ip`, `port` |
| 연동업체 라우팅 정보 일괄 변경 | `/hub-service/vendor-routing-bulk-change` `PROCESS` | `VendorRoutingBulkChangeRequest` `integrationType`, `currentIp`, `currentPort`, `newIp`, `newPort` · 서버 필수 `currentIp`, `currentPort`, `newIp`, `newPort` |

코드에서 확인한 버튼·작업명은 **검색**, **일괄 변경**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **연동 서비스 관리 > 연동 서비스 관리 > 연동업체 라우팅 일괄 변경**를 연다. `/hub-service/vendor-routing-bulk-change`를 연다.
2. **라우팅 정보 검색** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색** 중 해당 버튼을 선택한다.
3. **연동업체 라우팅 정보 검색** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 라우팅 정보 검색 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/vendorRoutingBulkChange/VendorRoutingBulkChangePage.tsx#L54) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 연동업체 라우팅 정보 검색 | `GET /api/v1/hub-service/vendor-routing-bulk-change/routing` · `/hub-service/vendor-routing-bulk-change` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/vendorroutingbulkchange/VendorRoutingBulkChangeController.kt#L41) | `VendorRoutingSearchRequest` `integrationType`, `ip`, `port` · 서버 필수 `ip`, `port` → `success`, `data`, `error`, `integrationType`, `ip`, `port`, `url` | `office.dbo.UPSTM_LSTCOMPANYLINKIP`, `smartwork.dbo.usp_nextgen_vendor_link_routing_groups_select_all` · 코드 연계 트랜잭션 |
| 연동업체 라우팅 정보 일괄 변경 | `PUT /api/v1/hub-service/vendor-routing-bulk-change/routing` · `/hub-service/vendor-routing-bulk-change` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/vendorroutingbulkchange/VendorRoutingBulkChangeController.kt#L54) | `VendorRoutingBulkChangeRequest` `integrationType`, `currentIp`, `currentPort`, `newIp`, `newPort` · 서버 필수 `currentIp`, `currentPort`, `newIp`, `newPort` → `success`, `data`, `error`, `integrationType`, `ip`, `port`, `url` | `SB_DTI.dbo.COMPANY_LINK_OUT`, `office.dbo.Hub_Engineer`, `office.dbo.HUB_VERSION_INFO`, `office.dbo.HUB_DETAIL_INFO`, `SB_DTI.dbo.NEOBILL_COMPANY_LINK_OUT` 외 3개 · 정의에서 확인한 쓰기 `SB_DTI.dbo.COMPANY_LINK_OUT`, `office.dbo.Hub_Engineer`, `office.dbo.HUB_VERSION_INFO`, `office.dbo.HUB_DETAIL_INFO` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `office.dbo.UPSTM_LSTCOMPANYLINKIP` | @SCHIP varchar(100), @SCHPORT varchar(10) | 정의 참조 `SmartBill3.dbo.COMPANY`, `SB_DTI.dbo.COMPANY_LINK_OUT` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/vendorroutingbulkchange/repository/VendorRoutingBulkChangeMapper.kt#L28) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-a16a5834804e5a0d) |
| `smartwork.dbo.usp_nextgen_vendor_link_routing_groups_select_all` | @IP varchar(100), @PORT varchar(10) = NULL | 정의 참조 `SmartBill3.dbo.COMPANY`, `SB_DTI.dbo.NEOBILL_COMPANY_LINK_OUT` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/vendorroutingbulkchange/repository/VendorRoutingBulkChangeMapper.kt#L44) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-1ff33ac495ef2b5d) |
| `SB_DTI.dbo.COMPANY_LINK_OUT` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL UPDATE | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/vendorroutingbulkchange/repository/VendorRoutingBulkChangeMapper.kt#L56) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-220f523f160d6282) |
| `office.dbo.Hub_Engineer` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL UPDATE | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/vendorroutingbulkchange/repository/VendorRoutingBulkChangeMapper.kt#L66) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-a1a29d6d4f48bd89) |
| `office.dbo.HUB_VERSION_INFO` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL UPDATE | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/vendorroutingbulkchange/repository/VendorRoutingBulkChangeMapper.kt#L76) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3723a1854104b2e4) |
| `office.dbo.HUB_DETAIL_INFO` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL UPDATE | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/vendorroutingbulkchange/repository/VendorRoutingBulkChangeMapper.kt#L86) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3a06e947c625b566) |
| `SB_DTI.dbo.NEOBILL_COMPANY_LINK_OUT` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/vendorroutingbulkchange/repository/VendorRoutingBulkChangeMapper.kt#L107) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b635b6a16ec47328) |
| `SmartBill3.dbo.COMPANY` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/vendorroutingbulkchange/repository/VendorRoutingBulkChangeMapper.kt#L107) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-0e6fcaa6b5086c07) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 라우팅 정보 검색 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 연동 서비스 관리 > 연동 서비스 관리 > 연동업체 라우팅 일괄 변경의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 검색 결과가 없습니다. | 라우팅 정보 검색 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 라우팅정보 일괄 변경을 취소하였습니다. | 라우팅 정보 검색 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/IntegrationRoutes.tsx#L140) · [VendorRoutingBulkChangePage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/vendorRoutingBulkChange/VendorRoutingBulkChangePage.tsx#L24) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/api/vendorRoutingBulkChangeApi.ts#L28) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/api/vendorRoutingBulkChangeApi.ts#L39) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 8개 중 개발 메타데이터 확인 8개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-2275fe80f1c0e160) | Demo 메타데이터 8/8개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

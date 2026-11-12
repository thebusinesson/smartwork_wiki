# [시스템 키·벌크계좌·업체 연결 설정] [구연동]연동업체 관리 일괄 수정 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

선택한 라우팅 그룹의 활성 OUT 행과 허브 관리 정보에서 URL/PORT만 변경한다. 한 단계라도 실패하면 전체 롤백한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 시스템 키·벌크계좌·업체 연결 설정 |
| 언제 사용하는가 | 라우팅 그룹 검색, 라우팅 일괄 수정 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 라우팅 일괄 수정 |
| 업무 흐름 | 라우팅 그룹 검색, 라우팅 일괄 수정 |
| 이 페이지의 역할 | 일괄 수정 · 라우팅 일괄 수정 |
| 판단 결과·다음 업무 | [[구연동]연동업체 관리](vendor-management.md) |
| 다른 화면과의 구분 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > [구연동]연동업체 관리에서 사용하는 일괄 수정 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 확인 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/vendorManagement/components/RoutingBulkEditPage.tsx#L218) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 선택한 라우팅 그룹의 활성 OUT 행과 허브 관리 정보에서 URL/PORT만 변경한다. 한 단계라도 실패하면 전체 롤백한다. |
| 메뉴·화면 경로 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > [구연동]연동업체 관리 · `/hub-vendor/vendor-management/bulk-edit` |
| 화면 유형·담당 | 일괄 수정 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [[구연동]연동업체 관리](vendor-management.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/hub-vendor/vendor-management` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 라우팅 그룹 검색 | `/hub-vendor/vendor-management` `VIEW` | `ip: String` · `port: String?` |
| 라우팅 일괄 수정 | `/hub-vendor/vendor-management` `PROCESS` | `BulkVendorUpdateRequest` `routingUrl`, `port`, `newIp`, `newPort` |

코드에서 확인한 버튼·작업명은 **검색**, **검색결과**, **라우팅 정보 변경**, **라우팅 일괄 수정**, **목록**, **확인**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [[구연동]연동업체 관리](vendor-management.md)에서 대상 또는 작업을 선택한다. `/hub-vendor/vendor-management/bulk-edit`를 연다.
2. **라우팅 일괄 수정**을 실행하기 전에 변경 대상과 입력값을 확인한다. 표시되는 **변경내역이 등록되었습니다.** 메시지와 대상 상태를 확인한다.
3. 후속 조회나 목록 복귀가 필요하면 [[구연동]연동업체 관리](vendor-management.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| request | API 요청 | 화면과 요청 변환 코드 참조 | `BulkVendorUpdateRequest` `routingUrl`, `port`, `newIp`, `newPort` |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 라우팅 그룹 검색 | `GET /api/v1/hub-vendor/vendors/routing-groups` · `/hub-vendor/vendor-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/vendormgmt/VendorController.kt#L275) | `ip: String` · `port: String?` → `success`, `data`, `error`, `routingUrl`, `port`, `totalCount`, `sampleCompanyName` | `SB_DTI.dbo.COMPANY_LINK_OUT`, `SmartBill3.dbo.COMPANY` |
| 라우팅 일괄 수정 | `POST /api/v1/hub-vendor/vendors/bulk-update` · `/hub-vendor/vendor-management` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/vendormgmt/VendorController.kt#L319) | `BulkVendorUpdateRequest` `routingUrl`, `port`, `newIp`, `newPort` → `success`, `data`, `error`, `successCount` | `SB_DTI.dbo.COMPANY_LINK_OUT`, `SmartBill3.dbo.COMPANY`, `office.dbo.Hub_Engineer`, `office.dbo.HUB_VERSION_INFO`, `office.dbo.HUB_DETAIL_INFO` · 정의에서 확인한 쓰기 `office.dbo.Hub_Engineer`, `office.dbo.HUB_VERSION_INFO`, `office.dbo.HUB_DETAIL_INFO` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `SB_DTI.dbo.COMPANY_LINK_OUT` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/vendormgmt/repository/VendorMapper.kt#L504) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-220f523f160d6282) |
| `SmartBill3.dbo.COMPANY` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/vendormgmt/repository/VendorMapper.kt#L504) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-0e6fcaa6b5086c07) |
| `office.dbo.Hub_Engineer` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL UPDATE | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/vendormgmt/repository/VendorMapper.kt#L564) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-a1a29d6d4f48bd89) |
| `office.dbo.HUB_VERSION_INFO` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL UPDATE | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/vendormgmt/repository/VendorMapper.kt#L567) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3723a1854104b2e4) |
| `office.dbo.HUB_DETAIL_INFO` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL UPDATE | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/vendormgmt/repository/VendorMapper.kt#L570) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3a06e947c625b566) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 라우팅 일괄 수정 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > [구연동]연동업체 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/IntegrationRoutes.tsx#L103) · [VendorBulkEditPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/vendorManagement/pages/VendorBulkEditPage.tsx#L4) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/vendorManagementApi.ts#L264) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/vendorManagementApi.ts#L310) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 5개 중 개발 메타데이터 확인 5개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-4b83e3d47b3052da) | Demo 메타데이터 5/5개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

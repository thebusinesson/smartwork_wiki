# [시스템 키·벌크계좌·업체 연결 설정] 첨부파일 연동업체관리 상세 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

첨부파일 연동업체관리 상세에서 **세금계산서 첨부파일 연동업체 상세 조회** 결과를 확인한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 시스템 키·벌크계좌·업체 연결 설정 |
| 언제 사용하는가 | 세금계산서 첨부파일 연동업체 상세 조회, 세금계산서 첨부파일 연동업체 저장 (등록/수정) 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 구분, 연동 시작일, 연동 종료일, 사용여부, 수정일자, 수정자 |
| 업무 흐름 | 세금계산서 첨부파일 연동업체 상세 조회, 세금계산서 첨부파일 연동업체 저장 (등록/수정) |
| 이 페이지의 역할 | 상세 · 세금계산서 첨부파일 연동업체 상세 조회 |
| 판단 결과·다음 업무 | [첨부파일 연동업체관리](attachment-vendor-management.md) |
| 다른 화면과의 구분 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > 첨부파일 연동업체관리에서 사용하는 상세 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 저장 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/AttachmentIntegrationVendorDetailPage.tsx#L129) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 첨부파일 연동업체관리 상세에서 **세금계산서 첨부파일 연동업체 상세 조회** 결과를 확인한다. |
| 메뉴·화면 경로 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > 첨부파일 연동업체관리 · `/hub-vendor/attachment-vendor-management/:vendorId` · 경로 변수 `vendorId` |
| 화면 유형·담당 | 상세 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [첨부파일 연동업체관리](attachment-vendor-management.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/hub-vendor/attachment-vendor-management` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `vendorId` |
| 세금계산서 첨부파일 연동업체 상세 조회 | `/hub-vendor/attachment-vendor-management` `VIEW` | `comNo: Int` |
| 세금계산서 첨부파일 연동업체 저장 (등록/수정) | `/hub-vendor/attachment-vendor-management` `PROCESS` | `AttachmentVendorSaveRequest` `comRegno`, `inFileDestination`, `inSystemId`, `inStartRoutingDate`, `inEndRoutingDate`, `inActiveYn`, `inRoutingUrl`, `outFileDestination`, `outSystemId`, `outStartRoutingDate`, `outEndRoutingDate`, `outActiveYn`, `outSapClientCode`, `outSapCompanyCode` |

코드에서 확인한 버튼·작업명은 **저장**, **목록**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [첨부파일 연동업체관리](attachment-vendor-management.md)에서 대상 또는 작업을 선택한다. `/hub-vendor/attachment-vendor-management/:vendorId`에서 이전 화면이 전달한 `vendorId`와 현재 대상을 확인한다.
2. **세금계산서 첨부파일 연동업체 상세 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
3. 후속 조회나 목록 복귀가 필요하면 [첨부파일 연동업체관리](attachment-vendor-management.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `vendorId` |
| 구분 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/attachmentVendorManagement/components/detail/AttachmentVendorSystemInfoSection.tsx#L142) |
| 연동 시작일 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/attachmentVendorManagement/components/detail/AttachmentVendorSystemInfoSection.tsx#L144) |
| 연동 종료일 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/attachmentVendorManagement/components/detail/AttachmentVendorSystemInfoSection.tsx#L145) |
| 사용여부 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/attachmentVendorManagement/components/detail/AttachmentVendorSystemInfoSection.tsx#L146) |
| 수정일자 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/attachmentVendorManagement/components/detail/AttachmentVendorSystemInfoSection.tsx#L147) |
| 수정자 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/attachmentVendorManagement/components/detail/AttachmentVendorSystemInfoSection.tsx#L148) |
| 선택 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/attachmentVendorManagement/components/detail/AttachmentVendorSystemInfoSection.tsx#L164) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 세금계산서 첨부파일 연동업체 상세 조회 | `GET /api/v1/hub-vendor/attachment-vendors/{comNo}` · `/hub-vendor/attachment-vendor-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/attachmentvendormgmt/AttachmentVendorController.kt#L109) | `comNo: Int` → `success`, `data`, `error`, `comNo`, `businessNumber`, `companyName`, `inDirection`, `outDirection`, `hubVendorId`, `hubVendorName` | `office.dbo.upSelect_AttachSystem_LstCustomerInfo02`, `office.dbo.upGW_CompanyINFO`, `office.dbo.upStm_LoadHubView02`, `office.dbo.BUSINESS`, `office.dbo.upGW_SawonInfo` |
| 세금계산서 첨부파일 연동업체 저장 (등록/수정) | `POST /api/v1/hub-vendor/attachment-vendors` · `/hub-vendor/attachment-vendor-management` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/attachmentvendormgmt/AttachmentVendorController.kt#L128) | `AttachmentVendorSaveRequest` `comRegno`, `inFileDestination`, `inSystemId`, `inStartRoutingDate`, `inEndRoutingDate`, `inActiveYn`, `inRoutingUrl`, `outFileDestination`, `outSystemId`, `outStartRoutingDate`, `outEndRoutingDate`, `outActiveYn`, `outSapClientCode`, `outSapCompanyCode` → `success`, `data`, `error`, `message` | `office.dbo.upDeliveryService_ComInfoInsert` · 정의에서 확인한 쓰기 `DeliveryService.dbo.COMPANY_LINK_OUT`, `DeliveryService.dbo.COMPANY_LINK_IN` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `office.dbo.upSelect_AttachSystem_LstCustomerInfo02` | @COM_NO varchar(10) | 정의 참조 `DeliveryService.dbo.COMPANY_LINK_IN`, `DeliveryService.dbo.COMPANY_LINK_OUT` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/attachmentvendormgmt/repository/AttachmentVendorMapper.kt#L79) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-4c4b5a6e0741ae68) |
| `office.dbo.upGW_CompanyINFO` | @COM_NO varchar(10) | 정의 참조 `SmartBill3.dbo.COMPANY`, `SmartBill3.dbo.MEMBER`, `MIGRATION_ETCASP.dbo.MIGRATION_MAPPING_COMPANY` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/attachmentvendormgmt/repository/AttachmentVendorMapper.kt#L91) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-363652a440a227d1) |
| `office.dbo.upStm_LoadHubView02` | @COM_NO int | 정의 참조 `office.dbo.BUSINESS`, `SmartBill3.dbo.COMPANY`, `office.dbo.MNG_HUB`, `office.dbo.MNG_HUB_DETAIL` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/attachmentvendormgmt/repository/AttachmentVendorMapper.kt#L102) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-15432431fc422f05) |
| `office.dbo.BUSINESS` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/attachmentvendormgmt/repository/AttachmentVendorMapper.kt#L128) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-1c6a832844bf01aa) |
| `office.dbo.upGW_SawonInfo` | @sw_no int | 정의 참조 `office.dbo.SAWON` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/attachmentvendormgmt/repository/AttachmentVendorMapper.kt#L139) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-4e991ae32938b48d) |
| `office.dbo.upDeliveryService_ComInfoInsert` | @ComRegno varchar(13), @in_FileDestination varchar(20), @in_SystemID varchar(10), @in_StartRoutingDate varchar(10), @in_EndRoutingDate varchar(10), @in_Active_YN varchar(1), @in_RoutingURL varchar(100), @in_Biz_UUser varchar(12), @out_FileDestination varchar(20), @out_SystemID varchar(10), @out_StartRoutingDate varchar(10), @out_EndRoutingDate varchar(10), @out_Active_YN varchar(1), @out_SAPClientCode varchar(3), @out_SAPCompanyCode varchar(4), @out_RoutingURL varchar(100), @out_Port varchar(5), @out_WSDL_Path varchar(200), @out_Biz_UUser varchar(12) | 정의 참조 `SmartBill3.dbo.COMPANY`, `DeliveryService.dbo.COMPANY_LINK_IN`, `DeliveryService.dbo.COMPANY_LINK_OUT` · 정적 쓰기 `DeliveryService.dbo.COMPANY_LINK_OUT`, `DeliveryService.dbo.COMPANY_LINK_IN` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/attachmentvendormgmt/repository/AttachmentVendorMapper.kt#L153) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-c65d48acdce5b245) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 구분, 연동 시작일, 연동 종료일, 사용여부, 수정일자, 수정자 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > 첨부파일 연동업체관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/IntegrationRoutes.tsx#L117) · [AttachmentIntegrationVendorDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/AttachmentIntegrationVendorDetailPage.tsx#L18) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/api/attachmentIntegrationVendorApi.ts#L44) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/api/attachmentIntegrationVendorApi.ts#L48) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 6개 중 개발 메타데이터 확인 6개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-66a536f4a31e3e5c) | Demo 메타데이터 6/6개 확인 · Dev와 계약 차이 1개 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

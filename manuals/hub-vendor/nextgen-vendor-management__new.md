# [시스템 키·벌크계좌·업체 연결 설정] 차세대 연동업체 등록 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

차세대 연동업체 등록에서 대상과 입력값을 확인해 **차세대 연동업체 신규 등록** 업무를 처리한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 시스템 키·벌크계좌·업체 연결 설정 |
| 언제 사용하는가 | 업체코드 옵션 목록, 비회원 수신 가능 여부 조회, 사업장 검색 (등록 폼 좌측 리스트), 허브업체 후보 목록 (선택 팝업), 차세대 연동업체 신규 등록 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 첨부파일, 구분, 연동(발행) 시작일, 사용여부, 업체코드, 수정일자 |
| 업무 흐름 | 업체코드 옵션 목록, 비회원 수신 가능 여부 조회, 사업장 검색 (등록 폼 좌측 리스트), 허브업체 후보 목록 (선택 팝업), 차세대 연동업체 신규 등록 |
| 이 페이지의 역할 | 등록 · 차세대 연동업체 신규 등록 |
| 판단 결과·다음 업무 | [[차세대]연동업체 관리](nextgen-vendor-management.md) |
| 다른 화면과의 구분 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > [차세대]연동업체 관리에서 사용하는 등록 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 일괄 등록 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/vendorManagement/components/VendorIntegrationSelector.tsx#L431) |
| 확인 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/vendorManagement/components/VendorIntegrationSelector.tsx#L509) |
| 선택 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/vendorManagement/components/HubVendorSelectionDialog.tsx#L113) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 차세대 연동업체 등록에서 대상과 입력값을 확인해 **차세대 연동업체 신규 등록** 업무를 처리한다. |
| 메뉴·화면 경로 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > [차세대]연동업체 관리 · `/hub-vendor/nextgen-vendor-management/new` |
| 화면 유형·담당 | 등록 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [[차세대]연동업체 관리](nextgen-vendor-management.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/hub-vendor/nextgen-vendor-management` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 업체코드 옵션 목록 | `/hub-vendor/nextgen-vendor-management` `VIEW` | `bnsId: Int` |
| 비회원 수신 가능 여부 조회 | `/hub-vendor/nextgen-vendor-management` `VIEW` | `comNo: Int` |
| 사업장 검색 (등록 폼 좌측 리스트) | `/hub-vendor/hub-vendor-management` / `/hub-vendor/vendor-management` / `/hub-vendor/nextgen-vendor-management` `VIEW` | `keyword: String` |
| 허브업체 후보 목록 (선택 팝업) | `/hub-vendor/vendor-management` `VIEW` | `salesProduct: String?` |
| 차세대 연동업체 신규 등록 | `/hub-vendor/nextgen-vendor-management` `PROCESS` | `NextGenVendorCreateRequest` `saleBnsId`, `branches`, `processes`, `organizationChart`, `purchaseAutomation`, `encryption`, `delegationMaster`, `monitoringExceptFlag`, `allComCode` |
| 사업자번호 일괄 등록 (Excel 업로드) | `/hub-vendor/hub-vendor-management` / `/hub-vendor/vendor-management` / `/hub-vendor/nextgen-vendor-management` `VIEW` | 추가 입력은 Controller 서명 참조 |

코드에서 확인한 버튼·작업명은 **검색**, **사업자번호 일괄 등록**, **등록업체 추가**, **등록업체 삭제**, **일괄 등록**, **첨부파일**, **샘플 다운로드**, **확인**, **선택**, **등록**, **목록**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [[차세대]연동업체 관리](nextgen-vendor-management.md)에서 대상 또는 작업을 선택한다. `/hub-vendor/nextgen-vendor-management/new`를 연다.
2. **암호화 설정**, **사용안함**, **XML 암호화**, **스마트빌 회원 가입 데이터 (default)**, **공급받는자 ERP 데이터** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색**, **사업자번호 일괄 등록**, **등록업체 추가**, **등록업체 삭제**, **일괄 등록** 중 해당 버튼을 선택한다.
3. **차세대 연동업체 신규 등록**을 실행하기 전에 변경 대상과 입력값을 확인한다. 처리 응답을 확인하고 관련 조회에서 대상의 상태를 확인한다.
4. 후속 조회나 목록 복귀가 필요하면 [[차세대]연동업체 관리](nextgen-vendor-management.md)에서 후속 절차를 확인한다.

업체 선택에서 하이픈이 포함된 사업자번호도 입력할 수 있다. 화면은 사업자번호 형식의 하이픈을 제거해 검색 API에 전달한다. [검색어 정규화](https://github.com/thebusinesson/smartwork/blob/b923849c5d878772e0de2b67becff0ae511f03b3/frontend/src/feature/integration/hubcollab/vendorManagement/components/VendorIntegrationSelector.tsx)

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 첨부파일 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/vendorManagement/components/VendorIntegrationSelector.tsx#L441) |
| 선택 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/vendorManagement/components/SystemIntegrationToSBTable.tsx#L147) |
| 구분 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/vendorManagement/components/SystemIntegrationToSBTable.tsx#L174) |
| 연동(발행) 시작일 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/vendorManagement/components/SystemIntegrationToSBTable.tsx#L176) |
| 사용여부 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/vendorManagement/components/SystemIntegrationToSBTable.tsx#L177) |
| 업체코드 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/vendorManagement/components/SystemIntegrationToSBTable.tsx#L178) |
| 수정일자 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/vendorManagement/components/SystemIntegrationToSBTable.tsx#L179) |
| 수정자 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/vendorManagement/components/SystemIntegrationToSBTable.tsx#L180) |
| 모니터링제외여부 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/vendorManagement/components/SystemIntegrationFromSBTable.tsx#L239) |
| 자동상태 복구 여부 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/vendorManagement/components/SystemIntegrationFromSBTable.tsx#L241) |
| 암호화 설정 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/vendorManagement/components/EncryptionSettingsSection.tsx#L31) |
| 사용안함 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/vendorManagement/components/EncryptionSettingsSection.tsx#L40) |
| XML 암호화 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/vendorManagement/components/EncryptionSettingsSection.tsx#L46) |
| 스마트빌 회원 가입 데이터 (default) | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/vendorManagement/components/DelegationMasterInfoSection.tsx#L63) |
| 공급받는자 ERP 데이터 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/vendorManagement/components/DelegationMasterInfoSection.tsx#L69) |
| 허브업체명 또는 영업상품명을 입력하세요 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/vendorManagement/components/HubVendorSelectionDialog.tsx#L94) |
| 허브업체명 | 출력 | 조회 응답 기준 | API 응답 `vendorName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/vendorManagement/components/HubVendorSelectionDialog.tsx#L106) |
| 영업상품명 | 출력 | 조회 응답 기준 | API 응답 `salesProductTitle` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/vendorManagement/components/HubVendorSelectionDialog.tsx#L107) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 업체코드 옵션 목록 | `GET /api/v1/hub-vendor/nextgen-vendors/company-codes` · `/hub-vendor/nextgen-vendor-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/nextgenvendormgmt/NextGenVendorController.kt#L168) | `bnsId: Int` → `success`, `data`, `error` | `office.dbo.BUSINESS`, `office.dbo.MNG_HUB`, `office.dbo.MNG_HUB_DETAIL`, `SmartBill3.dbo.COMPANY`, `SB_DTI.dbo.NEOBILL_COMPANY_LINK_IN` |
| 비회원 수신 가능 여부 조회 | `GET /api/v1/hub-vendor/nextgen-vendors/{comNo}/receive-nonmem` · `/hub-vendor/nextgen-vendor-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/nextgenvendormgmt/NextGenVendorController.kt#L158) | `comNo: Int` → `success`, `data`, `error`, `comNo`, `allowed` | `office.dbo.upAdmSB_COMPANY_DTICONFIG` |
| 사업장 검색 (등록 폼 좌측 리스트) | `GET /api/v1/hub-vendor/hub-vendors/companies/search` · `/hub-vendor/hub-vendor-management` / `/hub-vendor/vendor-management` / `/hub-vendor/nextgen-vendor-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/hubvendormgmt/HubVendorController.kt#L249) | `keyword: String` → `success`, `data`, `error`, `id`, `businessNumber`, `companyName`, `joinDate` | `SmartBill3.dbo.COMPANY` |
| 허브업체 후보 목록 (선택 팝업) | `GET /api/v1/hub-vendor/vendors/hub-options` · `/hub-vendor/vendor-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/vendormgmt/VendorController.kt#L182) | `salesProduct: String?` → `success`, `data`, `error`, `bnsId`, `hubId`, `vendorName`, `salesProductTitle` | `office.dbo.upPJT_BNSHubList_mnghub` |
| 차세대 연동업체 신규 등록 | `POST /api/v1/hub-vendor/nextgen-vendors` · `/hub-vendor/nextgen-vendor-management` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/nextgenvendormgmt/NextGenVendorController.kt#L188) | `NextGenVendorCreateRequest` `saleBnsId`, `branches`, `processes`, `organizationChart`, `purchaseAutomation`, `encryption`, `delegationMaster`, `monitoringExceptFlag`, `allComCode` → `success`, `data`, `error`, `createdCount`, `skippedCount`, `skipped` | `SmartBill3.dbo.COMPANY`, `SB_DTI.dbo.COMPANY_LINK_COMCODE`, `office.dbo.MNG_HUB` · 코드 연계 트랜잭션 |
| 사업자번호 일괄 등록 (Excel 업로드) | `POST /api/v1/hub-vendor/hub-vendors/companies/bulk-search` · `/hub-vendor/hub-vendor-management` / `/hub-vendor/vendor-management` / `/hub-vendor/nextgen-vendor-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/hubvendormgmt/HubVendorController.kt#L263) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `totalCount`, `matchedCount`, `notFoundCount`, `items` | `SmartBill3.dbo.COMPANY` |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `office.dbo.BUSINESS` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/nextgenvendormgmt/repository/NextGenVendorMapper.kt#L294) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-1c6a832844bf01aa) |
| `office.dbo.MNG_HUB` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/nextgenvendormgmt/repository/NextGenVendorMapper.kt#L294) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-bb97dfe4e2b8c3b3) |
| `office.dbo.MNG_HUB_DETAIL` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/nextgenvendormgmt/repository/NextGenVendorMapper.kt#L294) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-4bcef15734f3fd87) |
| `SmartBill3.dbo.COMPANY` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/nextgenvendormgmt/repository/NextGenVendorMapper.kt#L294) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-0e6fcaa6b5086c07) |
| `SB_DTI.dbo.NEOBILL_COMPANY_LINK_IN` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/nextgenvendormgmt/repository/NextGenVendorMapper.kt#L294) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-675e2313088d19f2) |
| `office.dbo.upAdmSB_COMPANY_DTICONFIG` | @COM_NO int | 정의 참조 `SB_DTI.dbo.COMPANY_DTICONFIG` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/nextgenvendormgmt/repository/NextGenVendorMapper.kt#L447) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-5efe11cc40c30919) |
| `office.dbo.upPJT_BNSHubList_mnghub` | @BNS_PRODUCT varchar(20) | 정의 참조 `office.dbo.BUSINESS`, `office.dbo.HUBPRODUCT`, `office.dbo.MNG_HUB` · 하위 호출 `office.dbo.HUBPRODUCT` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/vendormgmt/repository/VendorMapper.kt#L272) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-858f4da9c5c5a939) |
| `SB_DTI.dbo.COMPANY_LINK_COMCODE` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/nextgenvendormgmt/repository/NextGenVendorMapper.kt#L49) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-4e185162cbe01c50) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 첨부파일, 구분, 연동(발행) 시작일, 사용여부, 업체코드, 수정일자 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > [차세대]연동업체 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 업체코드 옵션 조회 실패 | 첨부파일, 구분, 연동(발행) 시작일, 사용여부, 업체코드, 수정일자 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 비회원 수신 가능 여부 조회 중 오류가 발생했습니다. | 첨부파일, 구분, 연동(발행) 시작일, 사용여부, 업체코드, 수정일자 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 등록된 항목이 없습니다. | 첨부파일, 구분, 연동(발행) 시작일, 사용여부, 업체코드, 수정일자 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 업체 검색 중 오류가 발생했습니다. | 첨부파일, 구분, 연동(발행) 시작일, 사용여부, 업체코드, 수정일자 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/IntegrationRoutes.tsx#L108) · [NextGenVendorRegistrationPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/nextGenVendorManagement/pages/NextGenVendorRegistrationPage.tsx#L185) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/nextGenVendorManagementApi.ts#L203) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/nextGenVendorManagementApi.ts#L229) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/hubVendorManagementApi.ts#L141) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/vendorManagementApi.ts#L200) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/nextGenVendorManagementApi.ts#L236) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/hubVendorManagementApi.ts#L152) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 8개 중 개발 메타데이터 확인 8개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-75605da76e65bb47) | 2026-11-11 기준으로 Demo 메타데이터 8/8개 확인 · Dev와 계약 차이 2개 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |
| 최신 변경 대조 | [11월 12일 전수 대조](../../references/all-pages-audit-2026-11-12.md) | 현재 코드 b923849c5 · 2026-11-12 |

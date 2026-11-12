# [시스템 키·벌크계좌·업체 연결 설정] [구연동]연동업체 관리 상세 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

회사 ID (COM_NO) 단위. 레거시 write.asp 의 모든 패널 정보 (4 PROCESSID IN/OUT + 허브업체 + 조직도 + 매입자동화 + 암호화 + 위탁자 연동) 를 한 묶음으로 반환. 미존재 시 INTEGRATION_010.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 시스템 키·벌크계좌·업체 연결 설정 |
| 언제 사용하는가 | 연동업체 상세 조회, 업체코드 옵션 목록, 허브업체 후보 목록 (선택 팝업), 연동업체 수정 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 구분, 연동(발행) 시작일, 사용여부, 업체코드, 수정일자, 수정자 |
| 업무 흐름 | 연동업체 상세 조회, 업체코드 옵션 목록, 허브업체 후보 목록 (선택 팝업), 연동업체 수정 |
| 이 페이지의 역할 | 상세 · 연동업체 상세 조회 |
| 판단 결과·다음 업무 | [[구연동]연동업체 관리](vendor-management.md) |
| 다른 화면과의 구분 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > [구연동]연동업체 관리에서 사용하는 상세 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 선택 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/vendorManagement/components/HubVendorSelectionDialog.tsx#L113) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 회사 ID (COM_NO) 단위. 레거시 write.asp 의 모든 패널 정보 (4 PROCESSID IN/OUT + 허브업체 + 조직도 + 매입자동화 + 암호화 + 위탁자 연동) 를 한 묶음으로 반환. 미존재 시 INTEGRATION_010. |
| 메뉴·화면 경로 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > [구연동]연동업체 관리 · `/hub-vendor/vendor-management/:id` · 경로 변수 `id` |
| 화면 유형·담당 | 상세 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [[구연동]연동업체 관리](vendor-management.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/hub-vendor/vendor-management` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `id` |
| 연동업체 상세 조회 | `/hub-vendor/vendor-management` `VIEW` | `comNo: Int` |
| 업체코드 옵션 목록 | `/hub-vendor/vendor-management` `VIEW` | `bnsId: Int` |
| 허브업체 후보 목록 (선택 팝업) | `/hub-vendor/vendor-management` `VIEW` | `salesProduct: String?` |
| 연동업체 수정 | `/hub-vendor/vendor-management` `PROCESS` | `comNo: Int` · `VendorUpdateRequest` `saleBnsId`, `processes`, `organizationChart`, `purchaseAutomation`, `encryption`, `delegationMaster` |

코드에서 확인한 버튼·작업명은 **선택**, **저장**, **목록**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [[구연동]연동업체 관리](vendor-management.md)에서 대상 또는 작업을 선택한다. `/hub-vendor/vendor-management/:id`에서 이전 화면이 전달한 `id`와 현재 대상을 확인한다.
2. **암호화 설정**, **사용안함**, **XML 암호화**, **스마트빌 회원 가입 데이터 (default)**, **공급받는자 ERP 데이터** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **저장** 중 해당 버튼을 선택한다.
3. **연동업체 상세 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [[구연동]연동업체 관리](vendor-management.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `id` |
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
| 허브업체명 또는 영업상품명을 입력하세요 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/vendorManagement/components/HubVendorSelectionDialog.tsx#L94) |
| 허브업체명 | 출력 | 조회 응답 기준 | API 응답 `vendorName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/vendorManagement/components/HubVendorSelectionDialog.tsx#L106) |
| 영업상품명 | 출력 | 조회 응답 기준 | API 응답 `salesProductTitle` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/vendorManagement/components/HubVendorSelectionDialog.tsx#L107) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 연동업체 상세 조회 | `GET /api/v1/hub-vendor/vendors/{comNo}` · `/hub-vendor/vendor-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/vendormgmt/VendorController.kt#L222) | `comNo: Int` → `success`, `data`, `error`, `id`, `businessNumber`, `companyName`, `registrationDate`, `processes`, `hubVendor`, `organizationChart`, `purchaseAutomation`, `encryption` | `SmartBill3.dbo.COMPANY`, `office.dbo.MNG_HUB_DETAIL`, `office.dbo.MNG_HUB`, `office.dbo.BUSINESS`, `SB_COMMON.dbo.ETC_OrganInterface_Setting` 외 6개 |
| 업체코드 옵션 목록 | `GET /api/v1/hub-vendor/vendors/company-codes` · `/hub-vendor/vendor-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/vendormgmt/VendorController.kt#L209) | `bnsId: Int` → `success`, `data`, `error` | `office.dbo.BUSINESS`, `office.dbo.MNG_HUB`, `office.dbo.MNG_HUB_DETAIL`, `SmartBill3.dbo.COMPANY`, `SB_DTI.dbo.COMPANY_LINK_IN` |
| 허브업체 후보 목록 (선택 팝업) | `GET /api/v1/hub-vendor/vendors/hub-options` · `/hub-vendor/vendor-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/vendormgmt/VendorController.kt#L182) | `salesProduct: String?` → `success`, `data`, `error`, `bnsId`, `hubId`, `vendorName`, `salesProductTitle` | `office.dbo.upPJT_BNSHubList_mnghub` |
| 연동업체 수정 | `PUT /api/v1/hub-vendor/vendors/{comNo}` · `/hub-vendor/vendor-management` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/vendormgmt/VendorController.kt#L253) | `comNo: Int` · `VendorUpdateRequest` `saleBnsId`, `processes`, `organizationChart`, `purchaseAutomation`, `encryption`, `delegationMaster` → `success`, `data`, `error`, `message`, `id` | `SmartBill3.dbo.COMPANY`, `office.dbo.MNG_HUB_DETAIL`, `office.dbo.MNG_HUB`, `office.dbo.BUSINESS`, `SB_COMMON.dbo.ETC_OrganInterface_Setting` 외 6개 · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `SmartBill3.dbo.COMPANY` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/vendormgmt/repository/VendorMapper.kt#L196) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-0e6fcaa6b5086c07) |
| `office.dbo.MNG_HUB_DETAIL` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/vendormgmt/repository/VendorMapper.kt#L196) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-4bcef15734f3fd87) |
| `office.dbo.MNG_HUB` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/vendormgmt/repository/VendorMapper.kt#L196) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-bb97dfe4e2b8c3b3) |
| `office.dbo.BUSINESS` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/vendormgmt/repository/VendorMapper.kt#L196) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-1c6a832844bf01aa) |
| `SB_COMMON.dbo.ETC_OrganInterface_Setting` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/vendormgmt/repository/VendorMapper.kt#L196) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3ee512b21dc5782d) |
| `SB_DTI.dbo.EMAIL_COMPANY_LINK_OUT` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/vendormgmt/repository/VendorMapper.kt#L196) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-a13485ec124c7566) |
| `SB_DTI.dbo.COMPANY_DTICONFIG` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/vendormgmt/repository/VendorMapper.kt#L196) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-2fa3ac3de7960ed7) |
| `SB_DTI.dbo.COMPANY_MNG_INFO` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/vendormgmt/repository/VendorMapper.kt#L196) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-229b2f17422cb4f2) |
| `SB_DTI.dbo.COMPANY_LINK_IN` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/vendormgmt/repository/VendorMapper.kt#L251) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-92ea90cdfc3fa872) |
| `SB_DTI.dbo.COMPANY_LINK_OUT` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/vendormgmt/repository/VendorMapper.kt#L251) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-220f523f160d6282) |
| `office.dbo.SAWON` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/vendormgmt/repository/VendorMapper.kt#L251) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3a9ea6e368df5cb3) |
| `office.dbo.upPJT_BNSHubList_mnghub` | @BNS_PRODUCT varchar(20) | 정의 참조 `office.dbo.BUSINESS`, `office.dbo.HUBPRODUCT`, `office.dbo.MNG_HUB` · 하위 호출 `office.dbo.HUBPRODUCT` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/vendormgmt/repository/VendorMapper.kt#L272) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-858f4da9c5c5a939) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 구분, 연동(발행) 시작일, 사용여부, 업체코드, 수정일자, 수정자 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > [구연동]연동업체 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 업체코드 옵션 조회 실패 | 구분, 연동(발행) 시작일, 사용여부, 업체코드, 수정일자, 수정자 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 허브업체 목록 조회 실패 | 구분, 연동(발행) 시작일, 사용여부, 업체코드, 수정일자, 수정자 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 허브업체명 또는 영업상품명을 입력 후 검색해 주세요. | 구분, 연동(발행) 시작일, 사용여부, 업체코드, 수정일자, 수정자 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/IntegrationRoutes.tsx#L104) · [VendorDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/vendorManagement/pages/VendorDetailPage.tsx#L51) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/vendorManagementApi.ts#L183) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/vendorManagementApi.ts#L208) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/vendorManagementApi.ts#L200) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/vendorManagementApi.ts#L191) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 12개 중 개발 메타데이터 확인 12개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-0170ba5709941527) | Demo 메타데이터 12/12개 확인 · Dev와 계약 차이 2개 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

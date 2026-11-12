# [시스템 키·벌크계좌·업체 연결 설정] 연동업체 수정 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

전체 패널 일괄 저장 (레거시 save.asp MOD 동작과 동일). 한 단계라도 실패 시 전체 롤백.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 시스템 키·벌크계좌·업체 연결 설정 |
| 언제 사용하는가 | 연동업체 상세 조회, 영업상품 코드 조회, 사업장 검색 (등록 폼 좌측 리스트) 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 허브업체명, 영업상품, 세금계산서 이용현황 조회, 전자계약 이용현황 조회, 업체명: |
| 업무 흐름 | 연동업체 상세 조회, 영업상품 코드 조회, 사업장 검색 (등록 폼 좌측 리스트), 허브업체 선택 팝업, SYSTEM_KEY 선택 팝업 |
| 이 페이지의 역할 | 수정 · 연동업체 수정 |
| 판단 결과·다음 업무 | [[구연동]연동업체 관리](vendor-management.md) · [[구연동]연동업체 관리 상세](vendor-management__by-id.md) |
| 다른 화면과의 구분 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > [구연동]연동업체 관리에서 사용하는 수정 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 선택 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/hubVendor/components/SelectionLayerPopup.tsx#L102) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 전체 패널 일괄 저장 (레거시 save.asp MOD 동작과 동일). 한 단계라도 실패 시 전체 롤백. |
| 메뉴·화면 경로 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > [구연동]연동업체 관리 · `/hub-vendor/vendor-management/:id/edit` · 경로 변수 `id` |
| 화면 유형·담당 | 수정 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [[구연동]연동업체 관리](vendor-management.md) · [[구연동]연동업체 관리 상세](vendor-management__by-id.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/hub-vendor/vendor-management` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `id` |
| 연동업체 상세 조회 | `/hub-vendor/vendor-management` `VIEW` | `comNo: Int` |
| 영업상품 코드 조회 | `/hub-collab/sales-management` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 사업장 검색 (등록 폼 좌측 리스트) | `/hub-vendor/hub-vendor-management` / `/hub-vendor/vendor-management` / `/hub-vendor/nextgen-vendor-management` `VIEW` | `keyword: String` |
| 허브업체 선택 팝업 | `/hub-vendor/hub-vendor-management` `VIEW` | `keyword: String?` · `registeredOnly: Boolean` · `productCode: String?` |
| SYSTEM_KEY 선택 팝업 | `/hub-vendor/hub-vendor-management` `VIEW` | `keyword: String?` |
| 연동업체 수정 | `/hub-vendor/vendor-management` `PROCESS` | `comNo: Int` · `VendorUpdateRequest` `saleBnsId`, `processes`, `organizationChart`, `purchaseAutomation`, `encryption`, `delegationMaster` |

코드에서 확인한 버튼·작업명은 **선택**, **해제**, **검색**, **등록업체 추가**, **등록업체 삭제**, **저장**, **취소**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [[구연동]연동업체 관리](vendor-management.md)에서 대상 또는 작업을 선택한다. `/hub-vendor/vendor-management/:id/edit`에서 이전 화면이 전달한 `id`와 현재 대상을 확인한다.
2. **업체명:** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색**, **등록업체 추가**, **등록업체 삭제**, **저장** 중 해당 버튼을 선택한다.
3. **연동업체 수정**을 실행하기 전에 변경 대상과 입력값을 확인한다. 처리 응답을 확인하고 관련 조회에서 대상의 상태를 확인한다.
4. 후속 조회나 목록 복귀가 필요하면 [[구연동]연동업체 관리 상세](vendor-management__by-id.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `id` |
| 허브업체명 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/hubVendor/components/HubVendorForm.tsx#L343) |
| 영업상품 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/hubVendor/components/HubVendorForm.tsx#L392) |
| 세금계산서 이용현황 조회 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/hubVendor/components/HubVendorForm.tsx#L401) |
| 전자계약 이용현황 조회 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/hubVendor/components/HubVendorForm.tsx#L421) |
| 업체명: | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/hubVendor/components/HubVendorForm.tsx#L660) |
| 사업자번호 또는 회사명을 입력하세요 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/hubVendor/components/HubVendorForm.tsx#L664) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 연동업체 상세 조회 | `GET /api/v1/hub-vendor/vendors/{comNo}` · `/hub-vendor/vendor-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/vendormgmt/VendorController.kt#L222) | `comNo: Int` → `success`, `data`, `error`, `id`, `businessNumber`, `companyName`, `registrationDate`, `processes`, `hubVendor`, `organizationChart`, `purchaseAutomation`, `encryption` | `SmartBill3.dbo.COMPANY`, `office.dbo.MNG_HUB_DETAIL`, `office.dbo.MNG_HUB`, `office.dbo.BUSINESS`, `SB_COMMON.dbo.ETC_OrganInterface_Setting` 외 6개 |
| 영업상품 코드 조회 | `GET /api/v1/sales/codes/products` · `/hub-collab/sales-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/sales/SalesCodeController.kt#L75) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `code`, `title` | `office.dbo.upBNS_BusinessRoute` |
| 사업장 검색 (등록 폼 좌측 리스트) | `GET /api/v1/hub-vendor/hub-vendors/companies/search` · `/hub-vendor/hub-vendor-management` / `/hub-vendor/vendor-management` / `/hub-vendor/nextgen-vendor-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/hubvendormgmt/HubVendorController.kt#L249) | `keyword: String` → `success`, `data`, `error`, `id`, `businessNumber`, `companyName`, `joinDate` | `SmartBill3.dbo.COMPANY` |
| 허브업체 선택 팝업 | `GET /api/v1/hub-vendor/hub-vendors/selection` · `/hub-vendor/hub-vendor-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/hubvendormgmt/HubVendorController.kt#L220) | `keyword: String?` · `registeredOnly: Boolean` · `productCode: String?` → `success`, `data`, `error`, `id`, `label`, `value`, `salesProduct`, `productCode`, `hubId` | `office.dbo.MNG_HUB`, `office.dbo.BUSINESS` |
| SYSTEM_KEY 선택 팝업 | `GET /api/v1/hub-vendor/hub-vendors/system-keys` · `/hub-vendor/hub-vendor-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/hubvendormgmt/HubVendorController.kt#L236) | `keyword: String?` → `success`, `data`, `error`, `id`, `label`, `value`, `salesProduct`, `productCode`, `hubId` | `office.dbo.MNG_SYSTEM` |
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
| `office.dbo.upBNS_BusinessRoute` | @cate01 varchar(15), @cate02 varchar(7), @flag varchar(5), @orderby varchar(10) = NULL | 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesCodeMapper.kt#L30) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-9f917ea22b3cc4fc) |
| `office.dbo.MNG_SYSTEM` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/hubvendormgmt/repository/HubVendorMapper.kt#L223) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-41fa24c29bca86c9) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 허브업체명, 영업상품, 세금계산서 이용현황 조회, 전자계약 이용현황 조회, 업체명: | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > [구연동]연동업체 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 업체 검색 중 오류가 발생했습니다. | 허브업체명, 영업상품, 세금계산서 이용현황 조회, 전자계약 이용현황 조회, 업체명: | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 일부 항목은 이미 등록된 업체입니다. | 허브업체명, 영업상품, 세금계산서 이용현황 조회, 전자계약 이용현황 조회, 업체명: | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 선택한 항목은 이미 등록된 업체입니다. | 허브업체명, 영업상품, 세금계산서 이용현황 조회, 전자계약 이용현황 조회, 업체명: | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/IntegrationRoutes.tsx#L105) · [VendorEditPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/vendorManagement/pages/VendorEditPage.tsx#L30) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/vendorManagementApi.ts#L183) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/salesManagementApi.ts#L220) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/hubVendorManagementApi.ts#L141) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/hubVendorManagementApi.ts#L128) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/hubVendorManagementApi.ts#L135) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/vendorManagementApi.ts#L317) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/vendorManagementApi.ts#L324) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 13개 중 개발 메타데이터 확인 13개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-139f6eef6351bbc3) | Demo 메타데이터 13/13개 확인 · Dev와 계약 차이 2개 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

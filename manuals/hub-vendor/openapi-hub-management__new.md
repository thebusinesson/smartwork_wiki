# [시스템 키·벌크계좌·업체 연결 설정] OAPI 허브 등록 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

OAPI 허브 등록에서 대상과 입력값을 확인해 **OpenAPI 허브 등록** 업무를 처리한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 시스템 키·벌크계좌·업체 연결 설정 |
| 언제 사용하는가 | 허브 등록 사업자 목록 조회, 허브업체 선택 팝업, SYSTEM_KEY 선택 팝업, 특별요금제 옵션 목록 조회, OpenAPI 허브 등록 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 허브업체명, 통합관리 전송, 도입모델, 인증방식, 개발언어, 서명방식 |
| 업무 흐름 | 허브 등록 사업자 목록 조회, 허브업체 선택 팝업, SYSTEM_KEY 선택 팝업, 특별요금제 옵션 목록 조회, OpenAPI 허브 등록 |
| 이 페이지의 역할 | 등록 · OpenAPI 허브 등록 |
| 판단 결과·다음 업무 | [OpenAPI 허브 관리](openapi-hub-management.md) |
| 다른 화면과의 구분 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > OpenAPI 허브 관리에서 사용하는 등록 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 선택 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/hubVendor/components/SelectionLayerPopup.tsx#L102) |
| 등록 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/OpenApiHubManagementRegistrationPage.tsx#L178) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | OAPI 허브 등록에서 대상과 입력값을 확인해 **OpenAPI 허브 등록** 업무를 처리한다. |
| 메뉴·화면 경로 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > OpenAPI 허브 관리 · `/hub-vendor/openapi-hub-management/new` |
| 화면 유형·담당 | 등록 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [OpenAPI 허브 관리](openapi-hub-management.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/hub-vendor/openapi-hub-management` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 허브 등록 사업자 목록 조회 | `/hub-vendor/openapi-hub-management` `VIEW` | `hubId: Int` |
| 허브업체 선택 팝업 | `/hub-vendor/hub-vendor-management` `VIEW` | `keyword: String?` · `registeredOnly: Boolean` · `productCode: String?` |
| SYSTEM_KEY 선택 팝업 | `/hub-vendor/hub-vendor-management` `VIEW` | `keyword: String?` |
| 특별요금제 옵션 목록 조회 | `/hub-vendor/openapi-hub-management` `VIEW` | 추가 입력은 Controller 서명 참조 |
| OpenAPI 허브 등록 | `/hub-vendor/openapi-hub-management` `PROCESS` | `OpenApiHubSaveRequest` `hubMngId`, `transferMode`, `adoptionModel`, `authenticationMethod`, `signatureMethod`, `developmentLanguage`, `openedAt`, `billingGroupCode`, `memberLinkCallbackUrl`, `memberLinkRefererUrl`, `specialRatePlanCode`, `chargeType`, `vendorContactInfo`, `remarks` |

코드에서 확인한 버튼·작업명은 **선택**, **검색**, **삭제**, **담당자 추가**, **등록**, **취소**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [OpenAPI 허브 관리](openapi-hub-management.md)에서 대상 또는 작업을 선택한다. `/hub-vendor/openapi-hub-management/new`를 연다.
2. **요금제명** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **통합관리 전송**, **검색**, **등록** 중 해당 버튼을 선택한다.
3. **OpenAPI 허브 등록**을 실행하기 전에 변경 대상과 입력값을 확인한다. 표시되는 **OpenAPI 허브가 성공적으로 등록되었습니다.** 메시지와 대상 상태를 확인한다.
4. 후속 조회나 목록 복귀가 필요하면 [OpenAPI 허브 관리](openapi-hub-management.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 허브업체명 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/openApiHubManagement/components/detail/OpenApiHubSummary.tsx#L64) |
| 통합관리 전송 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/openApiHubManagement/components/detail/OpenApiHubSummary.tsx#L91) |
| 도입모델 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/openApiHubManagement/components/detail/OpenApiHubDetailSettingsCard.tsx#L46) |
| 도입모델 선택 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/openApiHubManagement/components/detail/OpenApiHubDetailSettingsCard.tsx#L58) |
| 인증방식 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/openApiHubManagement/components/detail/OpenApiHubDetailSettingsCard.tsx#L69) |
| 인증방식 선택 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/openApiHubManagement/components/detail/OpenApiHubDetailSettingsCard.tsx#L81) |
| 개발언어 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/openApiHubManagement/components/detail/OpenApiHubDetailSettingsCard.tsx#L95) |
| 개발언어 선택 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/openApiHubManagement/components/detail/OpenApiHubDetailSettingsCard.tsx#L107) |
| 서명방식 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/openApiHubManagement/components/detail/OpenApiHubDetailSettingsCard.tsx#L118) |
| 서명방식 선택 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/openApiHubManagement/components/detail/OpenApiHubDetailSettingsCard.tsx#L130) |
| 오픈일 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/openApiHubManagement/components/detail/OpenApiHubDetailSettingsCard.tsx#L144) |
| 업체코드 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/openApiHubManagement/components/detail/OpenApiHubDetailSettingsCard.tsx#L155) |
| 청구방식 회원 연계코드 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/openApiHubManagement/components/detail/OpenApiHubDetailSettingsCard.tsx#L164) |
| 회원연계 Callback URL | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/openApiHubManagement/components/detail/OpenApiHubDetailSettingsCard.tsx#L179) |
| https:// 예) Callback URL | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/openApiHubManagement/components/detail/OpenApiHubDetailSettingsCard.tsx#L187) |
| 회원연계 Referer URL | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/openApiHubManagement/components/detail/OpenApiHubDetailSettingsCard.tsx#L196) |
| https:// 예) Referer URL | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/openApiHubManagement/components/detail/OpenApiHubDetailSettingsCard.tsx#L204) |
| 특별요금제 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/openApiHubManagement/components/detail/OpenApiHubDetailSettingsCard.tsx#L213) |
| 담당자명 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/openApiHubManagement/components/detail/OpenApiHubContactsSection.tsx#L36) |
| 이메일 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/openApiHubManagement/components/detail/OpenApiHubContactsSection.tsx#L37) |
| 연락처1 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/openApiHubManagement/components/detail/OpenApiHubContactsSection.tsx#L38) |
| 연락처2 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/openApiHubManagement/components/detail/OpenApiHubContactsSection.tsx#L39) |
| 비고 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/openApiHubManagement/components/detail/OpenApiHubContactsSection.tsx#L40) |
| 업체 담당자 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/openApiHubManagement/components/detail/OpenApiHubFooterInfo.tsx#L25) |
| 업체 담당자 정보를 입력하세요 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/openApiHubManagement/components/detail/OpenApiHubFooterInfo.tsx#L32) |
| 비고 사항을 입력하세요 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/openApiHubManagement/components/detail/OpenApiHubFooterInfo.tsx#L46) |
| 요금제명 | 출력 | 조회 응답 기준 | API 응답 `name` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/openApiHubManagement/components/detail/PricingPlanSelectionDialog.tsx#L69) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 허브 등록 사업자 목록 조회 | `GET /api/v1/hub-vendor/openapi-hubs/businesses` · `/hub-vendor/openapi-hub-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/openapihubmgmt/OpenApiHubController.kt#L118) | `hubId: Int` → `success`, `data`, `error`, `comNo`, `businessNumber`, `companyName` | `office.dbo.upHub_HubBranchComList_Common` |
| 허브업체 선택 팝업 | `GET /api/v1/hub-vendor/hub-vendors/selection` · `/hub-vendor/hub-vendor-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/hubvendormgmt/HubVendorController.kt#L220) | `keyword: String?` · `registeredOnly: Boolean` · `productCode: String?` → `success`, `data`, `error`, `id`, `label`, `value`, `salesProduct`, `productCode`, `hubId` | `office.dbo.MNG_HUB`, `office.dbo.BUSINESS` |
| SYSTEM_KEY 선택 팝업 | `GET /api/v1/hub-vendor/hub-vendors/system-keys` · `/hub-vendor/hub-vendor-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/hubvendormgmt/HubVendorController.kt#L236) | `keyword: String?` → `success`, `data`, `error`, `id`, `label`, `value`, `salesProduct`, `productCode`, `hubId` | `office.dbo.MNG_SYSTEM` |
| 특별요금제 옵션 목록 조회 | `GET /api/v1/hub-vendor/openapi-hubs/special-rate-plans` · `/hub-vendor/openapi-hub-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/openapihubmgmt/OpenApiHubController.kt#L105) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `id`, `name` | `SB_BILL.dbo.UspBill_SpecialFeePolicyList_SELECT_TOP` |
| OpenAPI 허브 등록 | `POST /api/v1/hub-vendor/openapi-hubs` · `/hub-vendor/openapi-hub-management` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/openapihubmgmt/OpenApiHubController.kt#L138) | `OpenApiHubSaveRequest` `hubMngId`, `transferMode`, `adoptionModel`, `authenticationMethod`, `signatureMethod`, `developmentLanguage`, `openedAt`, `billingGroupCode`, `memberLinkCallbackUrl`, `memberLinkRefererUrl`, `specialRatePlanCode`, `chargeType`, `vendorContactInfo`, `remarks` → `success`, `data`, `error`, `hubId`, `message` | `office.dbo.upGW_GetCompanyCode`, `office.dbo.upGW_OpenApiHubSave`, `smartwork.dbo.upGW_OpenApiHubDetailSave`, `office.dbo.upGW_OpenApiSignalSave`, `smartwork.dbo.OPENAPI_HUB_CONTACT` · 정의에서 확인한 쓰기 `SB_DTI.dbo.COMPANY_LINK_COMCODE`, `SB_DTI.dbo.OPENAPI_HUB`, `SB_DTI.dbo.OPENAPI_HUB_ATTRIBUTE`, `SB_DTI.dbo.OPENAPI_HUB_FEE` 외 3개 · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `office.dbo.upHub_HubBranchComList_Common` | @hub_id int, @bns_product varchar(50) | 정의 참조 `SmartBill3.dbo.COMPANY`, `office.dbo.MNG_HUB_DCT_DETAIL`, `office.dbo.MNG_HUB_DETAIL`, `office.dbo.MNG_HUB_ETC_DETAIL` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/openapihubmgmt/repository/OpenApiHubMapper.kt#L123) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-f4368e431084f539) |
| `office.dbo.MNG_HUB` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/hubvendormgmt/repository/HubVendorMapper.kt#L264) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-bb97dfe4e2b8c3b3) |
| `office.dbo.BUSINESS` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/hubvendormgmt/repository/HubVendorMapper.kt#L264) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-1c6a832844bf01aa) |
| `office.dbo.MNG_SYSTEM` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/hubvendormgmt/repository/HubVendorMapper.kt#L223) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-41fa24c29bca86c9) |
| `SB_BILL.dbo.UspBill_SpecialFeePolicyList_SELECT_TOP` | @PAGE int, @TOP int, @SERVICE_TYPE varchar(20), @CHARGE_TYPE varchar(10), @FROM_MONTH varchar(10), @TO_MONTH varchar(10), @DIVISION varchar(10) | 정의 참조 `SB_BILL.dbo.UspBill_SpecialFeePolicyListCount_SELECT` · 하위 호출 `SB_BILL.dbo.UspBill_SpecialFeePolicyListCount_SELECT` · 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/openapihubmgmt/repository/OpenApiHubMapper.kt#L185) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-6874a9c9a7fc9ef7) |
| `office.dbo.upGW_GetCompanyCode` | @COM_NO varchar(10), @SYSTEM_ID varchar(10), @COM_CODE varchar(10) OUT | 정의 참조 `SB_DTI.dbo.COMPANY_LINK_COMCODE` · 정적 쓰기 `SB_DTI.dbo.COMPANY_LINK_COMCODE` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/openapihubmgmt/repository/OpenApiHubMapper.kt#L253) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-1c8356788d7c3307) |
| `office.dbo.upGW_OpenApiHubSave` | @hub_id int, @platform_type varchar(3), @auth_type varchar(3), @sign_type varchar(3), @lan_type varchar(20), @open_date varchar(10), @customer varchar(8000), @remark varchar(8000), @sw_no int, @com_code char(3), @hub_name varchar(100), @send_link_mng char(1), @result int OUT | 정의 참조 `SB_DTI.dbo.OPENAPI_HUB` · 정적 쓰기 `SB_DTI.dbo.OPENAPI_HUB` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/openapihubmgmt/repository/OpenApiHubMapper.kt#L197) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-e2ed2c65b5caa5ba) |
| `smartwork.dbo.upGW_OpenApiHubDetailSave` | @OAPIID int, @SYSTEMCODE varchar(40), @CALLBACKURL varchar(200), @REFERRERURL varchar(400), @SPECIALCHARGE varchar(10), @CHARGETYPE varchar(10), @SW_NO int, @RESULT int OUT | 정의 참조 `SB_DTI.dbo.OPENAPI_HUB_ATTRIBUTE`, `SB_DTI.dbo.OPENAPI_HUB_FEE`, `SB_COMMON.dbo.VENDOR_MIGRATION_FEE` · 정적 쓰기 `SB_DTI.dbo.OPENAPI_HUB_ATTRIBUTE`, `SB_DTI.dbo.OPENAPI_HUB_FEE`, `SB_COMMON.dbo.VENDOR_MIGRATION_FEE` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/openapihubmgmt/repository/OpenApiHubMapper.kt#L220) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-79f6f3f1f86b8209) |
| `office.dbo.upGW_OpenApiSignalSave` | @oapi_id int, @signal varchar(30), @sw_no int | 정의 참조 `SB_DTI.dbo.OPENAPI_USE_FUNC` · 정적 쓰기 `SB_DTI.dbo.OPENAPI_USE_FUNC` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/openapihubmgmt/repository/OpenApiHubMapper.kt#L225) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-2921784236c7e385) |
| `smartwork.dbo.OPENAPI_HUB_CONTACT` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL UPDATE | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/openapihubmgmt/repository/OpenApiHubMapper.kt#L310) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-bf7efa340d10c6e1) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 허브업체명, 통합관리 전송, 도입모델, 인증방식, 개발언어, 서명방식 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > OpenAPI 허브 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/IntegrationRoutes.tsx#L119) · [OpenApiHubManagementRegistrationPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/OpenApiHubManagementRegistrationPage.tsx#L24) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/openApiHubManagement/api/openApiHubManagementApi.ts#L237) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/hubVendorManagementApi.ts#L128) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/hubVendorManagementApi.ts#L135) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/openApiHubManagement/api/openApiHubManagementApi.ts#L215) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/openApiHubManagement/api/openApiHubManagementApi.ts#L203) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 10개 중 개발 메타데이터 확인 10개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-c3e586679ba8696e) | Demo 메타데이터 10/10개 확인 · Dev와 계약 차이 2개 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

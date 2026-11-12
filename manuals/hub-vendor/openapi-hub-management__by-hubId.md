# [시스템 키·벌크계좌·업체 연결 설정] OpenAPI 허브 관리 상세 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

OpenAPI 허브 관리 상세에서 **OpenAPI 허브 상세 조회** 결과를 확인한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 시스템 키·벌크계좌·업체 연결 설정 |
| 언제 사용하는가 | OpenAPI 허브 상세 조회, 허브업체 선택 팝업, SYSTEM_KEY 선택 팝업, 특별요금제 옵션 목록 조회, OpenAPI 허브 수정 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 허브업체명, 통합관리 전송, 스마트빌 회원 가입 데이터 (default), 공급받는자 ERP 데이터, 도입모델, 인증방식 |
| 업무 흐름 | OpenAPI 허브 상세 조회, 허브업체 선택 팝업, SYSTEM_KEY 선택 팝업, 특별요금제 옵션 목록 조회, OpenAPI 허브 수정 |
| 이 페이지의 역할 | 상세 · OpenAPI 허브 상세 조회 |
| 판단 결과·다음 업무 | [OpenAPI 허브 관리](openapi-hub-management.md) |
| 다른 화면과의 구분 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > OpenAPI 허브 관리에서 사용하는 상세 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 선택 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/hubVendor/components/SelectionLayerPopup.tsx#L102) |
| 저장 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/OpenApiHubManagementDetailPage.tsx#L260) |
| 삭제 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/OpenApiHubManagementDetailPage.tsx#L274) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | OpenAPI 허브 관리 상세에서 **OpenAPI 허브 상세 조회** 결과를 확인한다. |
| 메뉴·화면 경로 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > OpenAPI 허브 관리 · `/hub-vendor/openapi-hub-management/:hubId` · 경로 변수 `hubId` |
| 화면 유형·담당 | 상세 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [OpenAPI 허브 관리](openapi-hub-management.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/hub-vendor/openapi-hub-management` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `hubId` |
| OpenAPI 허브 상세 조회 | `/hub-vendor/openapi-hub-management` `VIEW` | `oapiId: Int` |
| 허브업체 선택 팝업 | `/hub-vendor/hub-vendor-management` `VIEW` | `keyword: String?` · `registeredOnly: Boolean` · `productCode: String?` |
| SYSTEM_KEY 선택 팝업 | `/hub-vendor/hub-vendor-management` `VIEW` | `keyword: String?` |
| 특별요금제 옵션 목록 조회 | `/hub-vendor/openapi-hub-management` `VIEW` | 추가 입력은 Controller 서명 참조 |
| OpenAPI 허브 수정 | `/hub-vendor/openapi-hub-management` `PROCESS` | `oapiId: Int` · `OpenApiHubSaveRequest` `hubMngId`, `transferMode`, `adoptionModel`, `authenticationMethod`, `signatureMethod`, `developmentLanguage`, `openedAt`, `billingGroupCode`, `memberLinkCallbackUrl`, `memberLinkRefererUrl`, `specialRatePlanCode`, `chargeType`, `vendorContactInfo`, `remarks` |
| OpenAPI 허브 삭제 (soft delete + action_reason) | `/hub-vendor/openapi-hub-management` `DELETE` | `oapiId: Int` · `DeleteOpenApiHubRequest` `deleteReason` · 서버 필수 `deleteReason` |

코드에서 확인한 버튼·작업명은 **선택**, **검색**, **삭제**, **담당자 추가**, **저장**, **목록**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [OpenAPI 허브 관리](openapi-hub-management.md)에서 대상 또는 작업을 선택한다. `/hub-vendor/openapi-hub-management/:hubId`에서 이전 화면이 전달한 `hubId`와 현재 대상을 확인한다.
2. **스마트빌 회원 가입 데이터 (default)**, **공급받는자 ERP 데이터**, **요금제명** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **통합관리 전송**, **검색**, **저장** 중 해당 버튼을 선택한다.
3. **OpenAPI 허브 상세 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [OpenAPI 허브 관리](openapi-hub-management.md)에서 후속 절차를 확인한다.

API 설정의 **오픈스크랩** 항목에서 **오픈스크랩 매입통합 부서사용자 리스트 조회**를 선택할 수 있다. 이 화면의 체크 상태는 대상 허브의 설정을 확인·변경하는 데 사용한다. [API 항목 정의](https://github.com/thebusinesson/smartwork/blob/b923849c5d878772e0de2b67becff0ae511f03b3/frontend/src/feature/integration/hubvendor/openApiHubManagement/constants/apiCategories.ts)

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `hubId` |
| 허브업체명 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/openApiHubManagement/components/detail/OpenApiHubSummary.tsx#L64) |
| 통합관리 전송 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/openApiHubManagement/components/detail/OpenApiHubSummary.tsx#L91) |
| 스마트빌 회원 가입 데이터 (default) | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/openApiHubManagement/components/detail/OpenApiHubIntegrationCard.tsx#L154) |
| 공급받는자 ERP 데이터 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/openApiHubManagement/components/detail/OpenApiHubIntegrationCard.tsx#L160) |
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
| OpenAPI 허브 상세 조회 | `GET /api/v1/hub-vendor/openapi-hubs/{oapiId}` · `/hub-vendor/openapi-hub-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/openapihubmgmt/OpenApiHubController.kt#L95) | `oapiId: Int` → `success`, `data`, `error`, `hubId`, `summary`, `businesses`, `detailSettings`, `apiSignals`, `vendorContactInfo`, `remarks`, `contacts`, `updatedAt` | `office.dbo.upGW_CompanyOpenApi_Hub`, `office.dbo.UPGW_COMPANYOPENAPI_HUB_EXTENSION`, `office.dbo.MNG_HUB`, `office.dbo.BUSINESS`, `office.dbo.upGW_CompanyOpenApi` 외 5개 |
| 허브업체 선택 팝업 | `GET /api/v1/hub-vendor/hub-vendors/selection` · `/hub-vendor/hub-vendor-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/hubvendormgmt/HubVendorController.kt#L220) | `keyword: String?` · `registeredOnly: Boolean` · `productCode: String?` → `success`, `data`, `error`, `id`, `label`, `value`, `salesProduct`, `productCode`, `hubId` | `office.dbo.MNG_HUB`, `office.dbo.BUSINESS` |
| SYSTEM_KEY 선택 팝업 | `GET /api/v1/hub-vendor/hub-vendors/system-keys` · `/hub-vendor/hub-vendor-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/hubvendormgmt/HubVendorController.kt#L236) | `keyword: String?` → `success`, `data`, `error`, `id`, `label`, `value`, `salesProduct`, `productCode`, `hubId` | `office.dbo.MNG_SYSTEM` |
| 특별요금제 옵션 목록 조회 | `GET /api/v1/hub-vendor/openapi-hubs/special-rate-plans` · `/hub-vendor/openapi-hub-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/openapihubmgmt/OpenApiHubController.kt#L105) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `id`, `name` | `SB_BILL.dbo.UspBill_SpecialFeePolicyList_SELECT_TOP` |
| OpenAPI 허브 수정 | `PUT /api/v1/hub-vendor/openapi-hubs/{oapiId}` · `/hub-vendor/openapi-hub-management` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/openapihubmgmt/OpenApiHubController.kt#L158) | `oapiId: Int` · `OpenApiHubSaveRequest` `hubMngId`, `transferMode`, `adoptionModel`, `authenticationMethod`, `signatureMethod`, `developmentLanguage`, `openedAt`, `billingGroupCode`, `memberLinkCallbackUrl`, `memberLinkRefererUrl`, `specialRatePlanCode`, `chargeType`, `vendorContactInfo`, `remarks` → `success`, `data`, `error`, `hubId`, `message` | `office.dbo.upGW_CompanyOpenApi_Hub`, `office.dbo.UPGW_COMPANYOPENAPI_HUB_EXTENSION`, `office.dbo.MNG_HUB`, `office.dbo.BUSINESS`, `office.dbo.upGW_CompanyOpenApi` 외 10개 · 정의에서 확인한 쓰기 `SB_DTI.dbo.OPENAPI_HUB`, `SB_DTI.dbo.OPENAPI_HUB_ATTRIBUTE`, `SB_DTI.dbo.OPENAPI_HUB_FEE`, `SB_COMMON.dbo.VENDOR_MIGRATION_FEE` 외 3개 · 코드 연계 트랜잭션 |
| OpenAPI 허브 삭제 (soft delete + action_reason) | `DELETE /api/v1/hub-vendor/openapi-hubs/{oapiId}` · `/hub-vendor/openapi-hub-management` `DELETE` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/openapihubmgmt/OpenApiHubController.kt#L179) | `oapiId: Int` · `DeleteOpenApiHubRequest` `deleteReason` · 서버 필수 `deleteReason` → `success`, `data`, `error`, `hubId`, `message` | `office.dbo.upGW_CompanyOpenApi_Hub`, `office.dbo.UPGW_COMPANYOPENAPI_HUB_EXTENSION`, `office.dbo.MNG_HUB`, `office.dbo.BUSINESS`, `office.dbo.upGW_CompanyOpenApi` 외 7개 · 정의에서 확인한 쓰기 `SB_DTI.dbo.OPENAPI_HUB`, `smartwork.dbo.action_reason` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `office.dbo.upGW_CompanyOpenApi_Hub` | @oapi_id int | 정의 참조 `SB_DTI.dbo.OPENAPI_HUB`, `office.dbo.SAWON` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/openapihubmgmt/repository/OpenApiHubMapper.kt#L82) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-470cc28f1ba26a9f) |
| `office.dbo.UPGW_COMPANYOPENAPI_HUB_EXTENSION` | @OAPI_ID int | 정의 참조 `SB_BILL.dbo.CHARGEPOLICY_SPECIAL`, `SB_DTI.dbo.OPENAPI_HUB_FEE` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/openapihubmgmt/repository/OpenApiHubMapper.kt#L95) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-0cc351095b5e889e) |
| `office.dbo.MNG_HUB` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/openapihubmgmt/repository/OpenApiHubMapper.kt#L160) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-bb97dfe4e2b8c3b3) |
| `office.dbo.BUSINESS` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/openapihubmgmt/repository/OpenApiHubMapper.kt#L160) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-1c6a832844bf01aa) |
| `office.dbo.upGW_CompanyOpenApi` | @bns_id varchar(10) | 정의 참조 `SmartBill3.dbo.COMPANY`, `SB_DTI.dbo.COMPANY_MNG_INFO`, `office.dbo.MNG_HUB_DETAIL`, `SB_DTI.dbo.OPENAPI_HUB` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/openapihubmgmt/repository/OpenApiHubMapper.kt#L108) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-eed4a622661373f5) |
| `SB_DTI.dbo.upNeoBill_GetUseCompanyInfo` | @COM_NO int | 정의 참조 `SmartBill3.dbo.COMPANY`, `SmartBill3.dbo.MEMBER`, `SB_DTI.dbo.NEOBILL_AUTHCODE`, `SB_DTI.dbo.NEOBILL_CERTINFO` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/openapihubmgmt/repository/OpenApiHubMapper.kt#L139) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3c1cf7d4bb63980d) |
| `SmartBill3.dbo.upGW_CompanyException_Info` | @COM_NO varchar(10) | 정의 참조 `SmartBill3.dbo.COMPANY_EXCEPTION` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/openapihubmgmt/repository/OpenApiHubMapper.kt#L152) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-61fbcff048bfd48e) |
| `SB_DTI.dbo.COMPANY_MNG_INFO` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/openapihubmgmt/repository/OpenApiHubMapper.kt#L330) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-229b2f17422cb4f2) |
| `SB_DTI.dbo.OPENAPI_USE_FUNC` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/openapihubmgmt/repository/OpenApiHubMapper.kt#L172) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-f307b2ee4a7e08bb) |
| `smartwork.dbo.OPENAPI_HUB_CONTACT` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/openapihubmgmt/repository/OpenApiHubMapper.kt#L283) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-bf7efa340d10c6e1) |
| `office.dbo.MNG_SYSTEM` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/hubvendormgmt/repository/HubVendorMapper.kt#L223) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-41fa24c29bca86c9) |
| `SB_BILL.dbo.UspBill_SpecialFeePolicyList_SELECT_TOP` | @PAGE int, @TOP int, @SERVICE_TYPE varchar(20), @CHARGE_TYPE varchar(10), @FROM_MONTH varchar(10), @TO_MONTH varchar(10), @DIVISION varchar(10) | 정의 참조 `SB_BILL.dbo.UspBill_SpecialFeePolicyListCount_SELECT` · 하위 호출 `SB_BILL.dbo.UspBill_SpecialFeePolicyListCount_SELECT` · 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/openapihubmgmt/repository/OpenApiHubMapper.kt#L185) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-6874a9c9a7fc9ef7) |
| `office.dbo.upGW_OpenApiHubUpdate` | @oapi_id int, @hub_id int, @platform_type varchar(3), @auth_type varchar(3), @sign_type varchar(3), @lan_type varchar(20), @open_date varchar(10), @customer varchar(8000), @remark varchar(8000), @sw_no int, @hub_name varchar(100), @send_link_mng char(1) | 정의 참조 `SB_DTI.dbo.OPENAPI_HUB` · 정적 쓰기 `SB_DTI.dbo.OPENAPI_HUB` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/openapihubmgmt/repository/OpenApiHubMapper.kt#L207) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-7cb191fe2dd07da0) |
| `smartwork.dbo.upGW_OpenApiHubDetailSave` | @OAPIID int, @SYSTEMCODE varchar(40), @CALLBACKURL varchar(200), @REFERRERURL varchar(400), @SPECIALCHARGE varchar(10), @CHARGETYPE varchar(10), @SW_NO int, @RESULT int OUT | 정의 참조 `SB_DTI.dbo.OPENAPI_HUB_ATTRIBUTE`, `SB_DTI.dbo.OPENAPI_HUB_FEE`, `SB_COMMON.dbo.VENDOR_MIGRATION_FEE` · 정적 쓰기 `SB_DTI.dbo.OPENAPI_HUB_ATTRIBUTE`, `SB_DTI.dbo.OPENAPI_HUB_FEE`, `SB_COMMON.dbo.VENDOR_MIGRATION_FEE` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/openapihubmgmt/repository/OpenApiHubMapper.kt#L220) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-79f6f3f1f86b8209) |
| `office.dbo.upGW_OpenApiSignalDelete` | @oapi_id int, @signal varchar(30) | 정의 참조 `SB_DTI.dbo.OPENAPI_USE_FUNC` · 정적 쓰기 `SB_DTI.dbo.OPENAPI_USE_FUNC` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/openapihubmgmt/repository/OpenApiHubMapper.kt#L234) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-67b9d46210ceca2e) |
| `office.dbo.upGW_OpenApiSignalSave` | @oapi_id int, @signal varchar(30), @sw_no int | 정의 참조 `SB_DTI.dbo.OPENAPI_USE_FUNC` · 정적 쓰기 `SB_DTI.dbo.OPENAPI_USE_FUNC` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/openapihubmgmt/repository/OpenApiHubMapper.kt#L225) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-2921784236c7e385) |
| `office.dbo.SSP_BrkComPerManage_OpenApi` | @HUB_ID int, @COM_LIST varchar(max), @USER int, @BRKMYCOMLST varchar(max), @MULTI_COM_LIST_FAP varchar(max), @MULTI_COM_LIST_FAR varchar(max), @MULTI_COM_LIST_RAR varchar(max), @MULTI_COM_LIST_RAP varchar(max), @MYCOM_UPDATE_COM_LIST varchar(max) = NULL | 정의 참조 `SmartBill3.dbo.COMPANY`, `SmartBill3.dbo.COMPANY_EXCEPTION`, `SB_DTI.dbo.COMPANY_MNG_INFO`, `office.dbo.MNG_HUB_DETAIL` · 정적 쓰기 `SB_DTI.dbo.COMPANY_MNG_INFO`, `SmartBill3.dbo.COMPANY_EXCEPTION` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/openapihubmgmt/repository/OpenApiHubMapper.kt#L263) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-4e0ba8edb92ea9db) |
| `office.dbo.upGW_OpenApiHubDelete` | @oapi_id int, @sw_no int | 정의 참조 `SB_DTI.dbo.OPENAPI_HUB` · 정적 쓰기 `SB_DTI.dbo.OPENAPI_HUB` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/openapihubmgmt/repository/OpenApiHubMapper.kt#L242) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-ce9e2e6664be1b13) |
| `smartwork.dbo.action_reason` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL INSERT INTO | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/shared/actionreason/repository/ActionReasonMapper.kt#L16) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b0430106ffe0743f) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 허브업체명, 통합관리 전송, 스마트빌 회원 가입 데이터 (default), 공급받는자 ERP 데이터, 도입모델, 인증방식 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > OpenAPI 허브 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| OpenApi 허브 삭제를 취소하였습니다. | 허브업체명, 통합관리 전송, 스마트빌 회원 가입 데이터 (default), 공급받는자 ERP 데이터, 도입모델, 인증방식 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/IntegrationRoutes.tsx#L120) · [OpenApiHubManagementDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/OpenApiHubManagementDetailPage.tsx#L24) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/openApiHubManagement/api/openApiHubManagementApi.ts#L168) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/hubVendorManagementApi.ts#L128) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/hubVendorManagementApi.ts#L135) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/openApiHubManagement/api/openApiHubManagementApi.ts#L215) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/openApiHubManagement/api/openApiHubManagementApi.ts#L194) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/openApiHubManagement/api/openApiHubManagementApi.ts#L211) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 19개 중 개발 메타데이터 확인 19개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-f35826b20542f452) | 2026-11-11 기준으로 Demo 메타데이터 19/19개 확인 · Dev와 계약 차이 2개 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |
| 최신 변경 대조 | [11월 12일 전수 대조](../../references/all-pages-audit-2026-11-12.md) | 현재 코드 b923849c5 · 2026-11-12 |

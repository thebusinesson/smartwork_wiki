# [시스템 키·벌크계좌·업체 연결 설정] 연동플랫폼 통합관리 상세 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

시스템 기본 정보 + 허브업체 목록 + 서비스별 라우팅 정보 + ETC_SERVICE 메모.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 시스템 키·벌크계좌·업체 연결 설정 |
| 언제 사용하는가 | 연동 플랫폼 통합 관리 상세 조회, 참고사항(ETC_SERVICE) 저장 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 허브업체명, 사업자번호, 회사명, 청구SSS, 청구요금제, 청구부가서비스 |
| 업무 흐름 | 연동 플랫폼 통합 관리 상세 조회, 참고사항(ETC_SERVICE) 저장 |
| 이 페이지의 역할 | 상세 · 연동 플랫폼 통합 관리 상세 조회 |
| 판단 결과·다음 업무 | [연동플랫폼 통합관리](platform-management.md) · [연동플랫폼 통합관리 상세](platform-management__system-port__by-portId.md) |
| 다른 화면과의 구분 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > 연동플랫폼 통합관리에서 사용하는 상세 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 시스템 기본 정보 + 허브업체 목록 + 서비스별 라우팅 정보 + ETC_SERVICE 메모. |
| 메뉴·화면 경로 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > 연동플랫폼 통합관리 · `/hub-vendor/platform-management/:platformId` · 경로 변수 `platformId` |
| 화면 유형·담당 | 상세 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [연동플랫폼 통합관리](platform-management.md) · [연동플랫폼 통합관리 상세](platform-management__system-port__by-portId.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/hub-vendor/platform-management` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `platformId` |
| 연동 플랫폼 통합 관리 상세 조회 | `/hub-vendor/platform-management` `VIEW` | `id: Int` |
| 참고사항(ETC_SERVICE) 저장 | `/hub-vendor/platform-management` `PROCESS` | `id: Int` · `PlatformMgmtRemarksUpdateRequest` `remarks` |

코드에서 확인한 버튼·작업명은 **이전**, **저장**, **목록**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [연동플랫폼 통합관리](platform-management.md)에서 대상 또는 작업을 선택한다. `/hub-vendor/platform-management/:platformId`에서 이전 화면이 전달한 `platformId`와 현재 대상을 확인한다.
2. **사업자번호**, **회사명**, **청구SSS**, **청구요금제**, **청구부가서비스** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **저장** 중 해당 버튼을 선택한다.
3. **연동 플랫폼 통합 관리 상세 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [연동플랫폼 통합관리 상세](platform-management__system-port__by-portId.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `platformId` |
| 허브업체명 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/platformManagement/components/HubVendorInfoSection.tsx#L27) |
| 사업자번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `businessNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/platformManagement/components/ContractInfoSection.tsx#L21) |
| 회사명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `companyName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/platformManagement/components/ContractInfoSection.tsx#L23) |
| 청구SSS | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `billingGroup` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/platformManagement/components/ContractInfoSection.tsx#L24) |
| 청구요금제 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `billingPlan` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/platformManagement/components/ContractInfoSection.tsx#L25) |
| 청구부가서비스 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `additionalServices` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/platformManagement/components/ContractInfoSection.tsx#L36) |
| 무료사용여부 | 출력 | 조회 응답 기준 | 화면 필드 `isFreeService` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/platformManagement/components/ContractInfoSection.tsx#L37) |
| 미납여부 | 출력 | 조회 응답 기준 | 화면 필드 `hasArrears` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/platformManagement/components/ContractInfoSection.tsx#L43) |
| 참고사항을 입력하세요 | 출력 | 조회 응답 기준 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/platformManagement/components/RemarksSection.tsx#L27) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 연동 플랫폼 통합 관리 상세 조회 | `GET /api/v1/hub-vendor/platform-management/{id}` · `/hub-vendor/platform-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/platformmgmt/PlatformMgmtController.kt#L89) | `id: Int` → `success`, `data`, `error`, `systemId`, `systemKey`, `hubVendorName`, `remarks`, `hubVendors`, `relayInfos`, `contracts` | `smartwork.dbo.usp_platform_mgmt_detail_header_select`, `smartwork.dbo.usp_platform_mgmt_detail_vendors_select`, `smartwork.dbo.usp_platform_mgmt_detail_relays_select`, `smartwork.dbo.usp_platform_mgmt_detail_billing_select` · 코드 연계 트랜잭션 |
| 참고사항(ETC_SERVICE) 저장 | `PATCH /api/v1/hub-vendor/platform-management/{id}/remarks` · `/hub-vendor/platform-management` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/platformmgmt/PlatformMgmtController.kt#L101) | `id: Int` · `PlatformMgmtRemarksUpdateRequest` `remarks` → `success`, `data`, `error` | `office.dbo.upSW_SaveSystmeKey_EtcService` · 정의에서 확인한 쓰기 `office.dbo.MNG_SYSTEM` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.usp_platform_mgmt_detail_header_select` | @SYSTEM_ID int | 정의 참조 `office.dbo.MNG_SYSTEM` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/platformmgmt/repository/PlatformMgmtMapper.kt#L65) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-8c0b1e4fc6a17222) |
| `smartwork.dbo.usp_platform_mgmt_detail_vendors_select` | @SYSTEM_ID int | 정의 참조 `office.dbo.BUSINESS`, `office.dbo.HUBPRODUCT`, `office.dbo.MNG_HUB` · 하위 호출 `office.dbo.HUBPRODUCT` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/platformmgmt/repository/PlatformMgmtMapper.kt#L74) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-26e12cdcda9b09ec) |
| `smartwork.dbo.usp_platform_mgmt_detail_relays_select` | @SYSTEM_ID int | 정의 참조 `office.dbo.BUSINESS`, `SmartBill3.dbo.COMPANY`, `SB_DTI.dbo.COMPANY_LINK_OUT`, `DeliveryService.dbo.COMPANY_LINK_OUT`, `SmartBill3.dbo.DCT_COMPANY_LINK_OUT` 외 8개 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/platformmgmt/repository/PlatformMgmtMapper.kt#L84) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-c2e5fd5251bf5339) |
| `smartwork.dbo.usp_platform_mgmt_detail_billing_select` | @SYSTEM_ID int | 정의 참조 `SB_BILL.dbo.AGREEMENT_CHARGE`, `SB_BILL.dbo.AGREEMENT_CHARGE_BRANCH`, `office.dbo.BUSINESS`, `office.dbo.BUSINESS_CONTRACT_HIS`, `SB_BILL.dbo.CHARGE_AGENCY` 외 5개 · 쓰기 구문 존재 · 대상 별칭 또는 하위 정의 확인 · 하위 호출 `office.dbo.upBNS_ContractInfo_Detail2`, `office.dbo.upBNS_ContractInfo_Detail` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/platformmgmt/repository/PlatformMgmtMapper.kt#L100) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-a5a96ce1a8534034) |
| `office.dbo.upSW_SaveSystmeKey_EtcService` | @SYSTEM_ID int, @Etc_ServiceMsg varchar(8000), @SW_NO int | 정의 참조 `office.dbo.MNG_SYSTEM` · 정적 쓰기 `office.dbo.MNG_SYSTEM` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/platformmgmt/repository/PlatformMgmtMapper.kt#L114) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-9a34bbf008f2abcd) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 허브업체명, 사업자번호, 회사명, 청구SSS, 청구요금제, 청구부가서비스 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > 연동플랫폼 통합관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/IntegrationRoutes.tsx#L113) · [IntegrationPlatformDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/IntegrationPlatformDetailPage.tsx#L20) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/api/integrationPlatformApi.ts#L298) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/api/integrationPlatformApi.ts#L357) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 5개 중 개발 메타데이터 확인 5개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-4faf2c88f1fa46fa) | Demo 메타데이터 5/5개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

# [시스템 키·벌크계좌·업체 연결 설정] 허브업체 체크리스트 다운로드 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

동일 검색조건의 전체 결과를 Excel/CSV 로 다운로드. format=EXCEL(기본) 또는 CSV.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 시스템 키·벌크계좌·업체 연결 설정 |
| 언제 사용하는가 | 허브업체 오픈체크리스트, 허브업체 상세 조회, 허브업체 선택 팝업, SYSTEM_KEY 선택 팝업, 허브업체 오픈체크리스트 다운로드 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 허브업체명, 사업자번호, 업체명, 가입일, 자동승인, SMS 자동발송 |
| 업무 흐름 | 허브업체 오픈체크리스트, 허브업체 상세 조회, 허브업체 선택 팝업, SYSTEM_KEY 선택 팝업, 허브업체 오픈체크리스트 다운로드 |
| 이 페이지의 역할 | 체크리스트 · 허브업체 오픈체크리스트 다운로드 |
| 판단 결과·다음 업무 | [허브업체 관리](hub-vendor-management.md) |
| 다른 화면과의 구분 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > 허브업체 관리에서 사용하는 체크리스트 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 선택 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/hubVendor/components/SelectionLayerPopup.tsx#L102) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 동일 검색조건의 전체 결과를 Excel/CSV 로 다운로드. format=EXCEL(기본) 또는 CSV. |
| 메뉴·화면 경로 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > 허브업체 관리 · `/hub-vendor/hub-vendor-management/:id/checklist` · 경로 변수 `id` |
| 화면 유형·담당 | 체크리스트 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [허브업체 관리](hub-vendor-management.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/hub-vendor/hub-vendor-management` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `id` |
| 허브업체 오픈체크리스트 | `/hub-vendor/hub-vendor-management` `VIEW` | `id: Int` · `OpenCheckQuery` `page`, `size`, `searchType`, `searchText` |
| 허브업체 상세 조회 | `/hub-vendor/hub-vendor-management` `VIEW` | `id: Int` |
| 허브업체 선택 팝업 | `/hub-vendor/hub-vendor-management` `VIEW` | `keyword: String?` · `registeredOnly: Boolean` · `productCode: String?` |
| SYSTEM_KEY 선택 팝업 | `/hub-vendor/hub-vendor-management` `VIEW` | `keyword: String?` |
| 허브업체 오픈체크리스트 다운로드 | `/hub-vendor/hub-vendor-management` `EXCEL_DOWNLOAD` | `id: Int` · `searchType: String` · `searchText: String?` · `format: DownloadFormat` |

코드에서 확인한 버튼·작업명은 **선택**, **검색**, **다운로드**, **목록**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [허브업체 관리](hub-vendor-management.md)에서 대상 또는 작업을 선택한다. `/hub-vendor/hub-vendor-management/:id/checklist`에서 이전 화면이 전달한 `id`와 현재 대상을 확인한다.
2. **허브업체명** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색**, **다운로드** 중 해당 버튼을 선택한다.
3. **허브업체 오픈체크리스트 다운로드** 처리 결과를 확인하고 받은 파일의 대상과 적용 조건을 대조한다.
4. 후속 조회나 목록 복귀가 필요하면 [허브업체 관리](hub-vendor-management.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `id` |
| 허브업체명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/hubVendor/pages/HubVendorChecklistPage.tsx#L296) |
| 허브업체를 선택해 주세요 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/hubVendor/pages/HubVendorChecklistPage.tsx#L301) |
| 사업자번호 | 출력 | 조회 응답 기준 | 화면 필드 `businessNumber-h` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/hubVendor/components/ChecklistTable.tsx#L44) |
| 업체명 | 출력 | 조회 응답 기준 | 화면 필드 `companyName-h` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/hubVendor/components/ChecklistTable.tsx#L45) |
| 가입일 | 출력 | 조회 응답 기준 | 화면 필드 `joinDate-h` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/hubVendor/components/ChecklistTable.tsx#L46) |
| 자동승인 | 출력 | 조회 응답 기준 | 화면 필드 `autoApproval-group` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/hubVendor/components/ChecklistTable.tsx#L60) |
| SMS 자동발송 | 출력 | 조회 응답 기준 | 화면 필드 `smsAuto-group` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/hubVendor/components/ChecklistTable.tsx#L74) |
| 정매입 | 출력 | 조회 응답 기준 | 화면 필드 `issueCmtYn-h` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/hubVendor/components/ChecklistTable.tsx#L77) |
| 역매입 | 출력 | 조회 응답 기준 | 화면 필드 `rissueCmtYn-h` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/hubVendor/components/ChecklistTable.tsx#L78) |
| 개인매출 | 출력 | 조회 응답 기준 | 화면 필드 `pissueCmtYn-h` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/hubVendor/components/ChecklistTable.tsx#L79) |
| 정매출 | 출력 | 조회 응답 기준 | 화면 필드 `dtiSms-h` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/hubVendor/components/ChecklistTable.tsx#L80) |
| 위수탁 | 출력 | 조회 응답 기준 | 화면 필드 `bdtiSms-h` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/hubVendor/components/ChecklistTable.tsx#L82) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 허브업체 오픈체크리스트 | `GET /api/v1/hub-vendor/hub-vendors/{id}/open-check` · `/hub-vendor/hub-vendor-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/hubvendormgmt/HubVendorController.kt#L385) | `id: Int` · `OpenCheckQuery` `page`, `size`, `searchType`, `searchText` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `currentPage`, `size` | `office.dbo.upMg_Search_HubCompany` |
| 허브업체 상세 조회 | `GET /api/v1/hub-vendor/hub-vendors/{id}` · `/hub-vendor/hub-vendor-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/hubvendormgmt/HubVendorController.kt#L141) | `id: Int` → `success`, `data`, `error`, `id`, `vendorName`, `systemKey`, `salesProduct`, `integrationStatus`, `salesRep`, `productCode`, `saleId`, `systemId` | `office.dbo.upHub_MngHubMainInfo`, `office.dbo.upHub_HubBranchComList_Common` |
| 허브업체 선택 팝업 | `GET /api/v1/hub-vendor/hub-vendors/selection` · `/hub-vendor/hub-vendor-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/hubvendormgmt/HubVendorController.kt#L220) | `keyword: String?` · `registeredOnly: Boolean` · `productCode: String?` → `success`, `data`, `error`, `id`, `label`, `value`, `salesProduct`, `productCode`, `hubId` | `office.dbo.MNG_HUB`, `office.dbo.BUSINESS` |
| SYSTEM_KEY 선택 팝업 | `GET /api/v1/hub-vendor/hub-vendors/system-keys` · `/hub-vendor/hub-vendor-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/hubvendormgmt/HubVendorController.kt#L236) | `keyword: String?` → `success`, `data`, `error`, `id`, `label`, `value`, `salesProduct`, `productCode`, `hubId` | `office.dbo.MNG_SYSTEM` |
| 허브업체 오픈체크리스트 다운로드 | `GET /api/v1/hub-vendor/hub-vendors/{id}/open-check/download` · `/hub-vendor/hub-vendor-management` `EXCEL_DOWNLOAD` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/hubvendormgmt/HubVendorController.kt#L347) | `id: Int` · `searchType: String` · `searchText: String?` · `format: DownloadFormat` → 파일 또는 오류 응답 | `office.dbo.upMg_Search_HubCompany` |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `office.dbo.upMg_Search_HubCompany` | @HUBID varchar(10), @SEARCH_TYPE varchar(10), @SEARCH_TEXT varchar(100) | 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/hubvendormgmt/repository/HubVendorMapper.kt#L332) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-eef03e3fe46e840b) |
| `office.dbo.upHub_MngHubMainInfo` | @hub_id int | 정의 참조 `office.dbo.BUSINESS`, `office.dbo.HUBPRODUCT`, `office.dbo.MNG_HUB`, `office.dbo.MNG_SYSTEM`, `office.dbo.SAWON` · 하위 호출 `office.dbo.HUBPRODUCT` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/hubvendormgmt/repository/HubVendorMapper.kt#L194) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-310f1ea2b6ed49e4) |
| `office.dbo.upHub_HubBranchComList_Common` | @hub_id int, @bns_product varchar(50) | 정의 참조 `SmartBill3.dbo.COMPANY`, `office.dbo.MNG_HUB_DCT_DETAIL`, `office.dbo.MNG_HUB_DETAIL`, `office.dbo.MNG_HUB_ETC_DETAIL` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/hubvendormgmt/repository/HubVendorMapper.kt#L207) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-f4368e431084f539) |
| `office.dbo.MNG_HUB` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/hubvendormgmt/repository/HubVendorMapper.kt#L264) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-bb97dfe4e2b8c3b3) |
| `office.dbo.BUSINESS` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/hubvendormgmt/repository/HubVendorMapper.kt#L264) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-1c6a832844bf01aa) |
| `office.dbo.MNG_SYSTEM` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/hubvendormgmt/repository/HubVendorMapper.kt#L223) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-41fa24c29bca86c9) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 허브업체명, 사업자번호, 업체명, 가입일, 자동승인, SMS 자동발송 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > 허브업체 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 오픈체크 리스트를 불러오는데 실패했습니다. | 허브업체명, 사업자번호, 업체명, 가입일, 자동승인, SMS 자동발송 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 허브업체를 먼저 선택해 주세요. | 허브업체명, 사업자번호, 업체명, 가입일, 자동승인, SMS 자동발송 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 다운로드 중 오류가 발생했습니다. | 허브업체명, 사업자번호, 업체명, 가입일, 자동승인, SMS 자동발송 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/IntegrationRoutes.tsx#L100) · [HubVendorChecklistPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/hubVendor/pages/HubVendorChecklistPage.tsx#L85) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/hubVendorManagementApi.ts#L205) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/hubVendorManagementApi.ts#L59) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/hubVendorManagementApi.ts#L128) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/hubVendorManagementApi.ts#L135) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/hubVendorManagementApi.ts#L193) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 6개 중 개발 메타데이터 확인 6개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-7e652ae09e8a97a0) | Demo 메타데이터 6/6개 확인 · Dev와 계약 차이 2개 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

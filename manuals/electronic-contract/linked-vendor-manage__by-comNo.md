# [계약 연동 업체·인증서와 장애] 연동업체 관리 상세 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

회사번호로 전자계약 연동업체 상세 정보를 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 계약 연동 업체·인증서와 장애 |
| 언제 사용하는가 | 전자계약 연동업체 상세 조회, 전자계약 허브업체 목록 조회, 전자계약 연동업체 부분 수정 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 연동 등록 업체, 회사명, 사업자 번호, 시스템 정보, 관련 허브업체 / 업체코드, 허브업체명 |
| 업무 흐름 | 전자계약 연동업체 상세 조회, 전자계약 허브업체 목록 조회, 전자계약 연동업체 부분 수정 |
| 이 페이지의 역할 | 상세 · 전자계약 연동업체 상세 조회 |
| 판단 결과·다음 업무 | [연동업체 관리](linked-vendor-manage.md) |
| 다른 화면과의 구분 | SB 서비스관리 > 전자계약 > 연동업체 관리에서 사용하는 상세 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 구분 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/components/LinkedVendorInputSections.tsx#L77) |
| 연동 시작일 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/components/LinkedVendorInputSections.tsx#L79) |
| 가능 상태 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/components/LinkedVendorInputSections.tsx#L80) |
| 사용여부 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/components/LinkedVendorInputSections.tsx#L81) |
| 수정일자 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/components/LinkedVendorInputSections.tsx#L82) |
| 수정자 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/components/LinkedVendorInputSections.tsx#L83) |
| 양자간(B) | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/components/LinkedVendorInputSections.tsx#L96) |
| 선택 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/components/LinkedVendorInputSections.tsx#L333) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 회사번호로 전자계약 연동업체 상세 정보를 조회한다. |
| 메뉴·화면 경로 | SB 서비스관리 > 전자계약 > 연동업체 관리 · `/electronic-contract/linked-vendor-manage/:comNo` · 경로 변수 `comNo` |
| 화면 유형·담당 | 상세 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [연동업체 관리](linked-vendor-manage.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/electronic-contract/linked-vendor-manage` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `comNo` |
| 전자계약 연동업체 상세 조회 | `/electronic-contract/linked-vendor-manage` `VIEW` | `comNo: Int` |
| 전자계약 허브업체 목록 조회 | `/electronic-contract/linked-vendor-manage` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 전자계약 연동업체 부분 수정 | `/electronic-contract/linked-vendor-manage` `PROCESS` | `comNo: Int` · `LinkedVendorPatchRequest` `systemInfo`, `hub`, `settings` |

코드에서 확인한 버튼·작업명은 **선택**, **저장**, **목록**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [연동업체 관리](linked-vendor-manage.md)에서 대상 또는 작업을 선택한다. `/electronic-contract/linked-vendor-manage/:comNo`에서 이전 화면이 전달한 `comNo`와 현재 대상을 확인한다.
2. **연동 등록 업체**, **회사명**, **사업자 번호**, **시스템 정보**, **관련 허브업체 / 업체코드**, **허브업체명**, **전자계약 기본 설정** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **저장** 중 해당 버튼을 선택한다.
3. **전자계약 연동업체 상세 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [연동업체 관리](linked-vendor-manage.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `comNo` |
| 연동 등록 업체 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/LinkedVendorManagePageDetail.tsx#L204) |
| 회사명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/LinkedVendorManagePageDetail.tsx#L209) |
| 사업자 번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/LinkedVendorManagePageDetail.tsx#L213) |
| 시스템 정보 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/components/LinkedVendorInputSections.tsx#L218) |
| 관련 허브업체 / 업체코드 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/components/LinkedVendorInputSections.tsx#L289) |
| 허브업체명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/components/LinkedVendorInputSections.tsx#L293) |
| 허브업체를 선택하세요 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/components/LinkedVendorInputSections.tsx#L297) |
| 허브업체명 또는 영업상품명을 입력하세요 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/components/LinkedVendorInputSections.tsx#L315) |
| 영업상품명 | 출력 | 조회 응답 기준 | API 응답 `salesProductTitle` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/components/LinkedVendorInputSections.tsx#L327) |
| 전자계약 기본 설정 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/components/LinkedVendorInputSections.tsx#L352) |
| 기본용량 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/components/LinkedVendorInputSections.tsx#L356) |
| 첨부파일 용량 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/components/LinkedVendorInputSections.tsx#L365) |
| 파일 자동삭제 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/components/LinkedVendorInputSections.tsx#L374) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 전자계약 연동업체 상세 조회 | `GET /api/v1/electronic-contract/linked-vendors/{comNo}` · `/electronic-contract/linked-vendor-manage` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/electroniccontract/linkedvendor/LinkedVendorController.kt#L73) | `comNo: Int` → `success`, `data`, `error`, `comNo`, `companyName`, `bizNo`, `systemInfo`, `hub`, `settings` | `office.dbo.upGW_CompanyINFO`, `SmartBill3.dbo.COMPANY`, `office.dbo.upStm_LstDCTCompanyLinkInfo`, `office.dbo.upStm_LoadHubDCTView`, `SmartBill3.dbo.upDCT_Sch_CompanyConfig` |
| 전자계약 허브업체 목록 조회 | `GET /api/v1/electronic-contract/linked-vendors/hub-vendors` · `/electronic-contract/linked-vendor-manage` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/electroniccontract/linkedvendor/LinkedVendorController.kt#L102) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `saleId`, `hubId`, `siteName`, `salesProductTitle`, `contactPoint`, `contactPhone` | `office.dbo.upPJT_BNSHubList_mnghub` |
| 전자계약 연동업체 부분 수정 | `PATCH /api/v1/electronic-contract/linked-vendors/{comNo}` · `/electronic-contract/linked-vendor-manage` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/electroniccontract/linkedvendor/LinkedVendorController.kt#L127) | `comNo: Int` · `LinkedVendorPatchRequest` `systemInfo`, `hub`, `settings` → `success`, `data`, `error` | `office.dbo.upGW_CompanyINFO`, `SmartBill3.dbo.COMPANY`, `office.dbo.upStm_ModHubDCTCompany`, `office.dbo.upStm_SavDCTCompanyLinkIn`, `office.dbo.upStm_SavDCTCompanyLinkOut` 외 1개 · 정의에서 확인한 쓰기 `office.dbo.MNG_HUB_DCT_DETAIL`, `SmartBill3.dbo.DCT_COMPANY_LINK_IN`, `office.dbo.MNG_COMPANY_EXCEPT`, `SmartBill3.dbo.DCT_COMPANY_LINK_OUT` 외 1개 · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `office.dbo.upGW_CompanyINFO` | @COM_NO varchar(10) | 정의 참조 `SmartBill3.dbo.COMPANY`, `SmartBill3.dbo.MEMBER`, `MIGRATION_ETCASP.dbo.MIGRATION_MAPPING_COMPANY` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/linkedvendor/repository/LinkedVendorMapper.kt#L74) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-363652a440a227d1) |
| `SmartBill3.dbo.COMPANY` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/linkedvendor/repository/LinkedVendorMapper.kt#L93) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-0e6fcaa6b5086c07) |
| `office.dbo.upStm_LstDCTCompanyLinkInfo` | @COM_NO varchar(10) | 정의 참조 `SmartBill3.dbo.DCT_COMPANY_LINK_IN`, `SmartBill3.dbo.DCT_COMPANY_LINK_OUT` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/linkedvendor/repository/LinkedVendorMapper.kt#L63) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-0b187d74447cf64f) |
| `office.dbo.upStm_LoadHubDCTView` | @COM_NO int | 정의 참조 `office.dbo.BUSINESS`, `SmartBill3.dbo.COMPANY`, `office.dbo.MNG_HUB`, `office.dbo.MNG_HUB_DCT_DETAIL` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/linkedvendor/repository/LinkedVendorMapper.kt#L113) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-fece7cac2f6fb6cb) |
| `SmartBill3.dbo.upDCT_Sch_CompanyConfig` | @COM_NO int | 정의 참조 `SmartBill3.dbo.DCT_COMPANY_CONFIG` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/linkedvendor/repository/LinkedVendorMapper.kt#L104) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-92d73b73c544ca5f) |
| `office.dbo.upPJT_BNSHubList_mnghub` | @BNS_PRODUCT varchar(20) | 정의 참조 `office.dbo.BUSINESS`, `office.dbo.HUBPRODUCT`, `office.dbo.MNG_HUB` · 하위 호출 `office.dbo.HUBPRODUCT` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/linkedvendor/repository/LinkedVendorMapper.kt#L127) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-858f4da9c5c5a939) |
| `office.dbo.upStm_ModHubDCTCompany` | @bns_id int, @com_regno varchar(13), @sw_no int | 정의 참조 `office.dbo.MNG_HUB`, `office.dbo.MNG_HUB_DCT_DETAIL` · 정적 쓰기 `office.dbo.MNG_HUB_DCT_DETAIL` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/linkedvendor/repository/LinkedVendorMapper.kt#L169) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-c59c3a5d32cf2a28) |
| `office.dbo.upStm_SavDCTCompanyLinkIn` | @COM_NO int, @IN_BA_SYSTEMID varchar(10), @IN_TXTFMDATE1 varchar(10), @IN_BA_STARTSTATUS char(1), @IN_BA_ACTIVE_YN char(1), @IN_BB_SYSTEMID varchar(10), @IN_TXTFMDATE2 varchar(10), @IN_BB_STARTSTATUS char(1), @IN_BB_ACTIVE_YN char(1), @ADMIN_NO varchar(10) | 정의 참조 `SmartBill3.dbo.COMPANY`, `SmartBill3.dbo.DCT_COMPANY_LINK_IN`, `office.dbo.MNG_COMPANY_EXCEPT` · 정적 쓰기 `SmartBill3.dbo.DCT_COMPANY_LINK_IN`, `office.dbo.MNG_COMPANY_EXCEPT` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/linkedvendor/repository/LinkedVendorMapper.kt#L177) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-0856f36ceb00d56e) |
| `office.dbo.upStm_SavDCTCompanyLinkOut` | @COM_NO int, @OUT_BA_SYSTEMID varchar(10), @OUT_TXTFMDATE1 varchar(10), @OUT_BA_STARTSTATUS char(1), @OUT_BA_ACTIVE_YN char(1), @OUT_BA_SAPCLIENTCODE varchar(3), @OUT_BA_SAPCOMPANYCODE varchar(4), @OUT_BA_ROUTINGURL varchar(100), @OUT_BA_PORT varchar(5), @OUT_BB_SYSTEMID varchar(10), @OUT_TXTFMDATE2 varchar(10), @OUT_BB_STARTSTATUS char(1), @OUT_BB_ACTIVE_YN char(1), @OUT_BB_SAPCLIENTCODE varchar(3), @OUT_BB_SAPCOMPANYCODE varchar(4), @OUT_BB_ROUTINGURL varchar(100), @OUT_BB_PORT varchar(5), @ADMIN_NO varchar(10) | 정의 참조 `SmartBill3.dbo.DCT_COMPANY_LINK_OUT` · 정적 쓰기 `SmartBill3.dbo.DCT_COMPANY_LINK_OUT` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/linkedvendor/repository/LinkedVendorMapper.kt#L187) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-c82cb68c2da03a93) |
| `SmartBill3.dbo.upDCT_SavDctDefaultDisk` | @COM_NO int, @DEFAULT_DISK int, @ATTACHFILE_DEL_YN char(1), @ATTACHFILE_LIMIT_SIZE int | 정의 참조 `SmartBill3.dbo.DCT_COMPANY_CONFIG` · 정적 쓰기 `SmartBill3.dbo.DCT_COMPANY_CONFIG` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/linkedvendor/repository/LinkedVendorMapper.kt#L194) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-313f509b14a6a506) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 연동 등록 업체, 회사명, 사업자 번호, 시스템 정보, 관련 허브업체 / 업체코드, 허브업체명 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 서비스관리 > 전자계약 > 연동업체 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 회사번호가 올바르지 않습니다. | 연동 등록 업체, 회사명, 사업자 번호, 시스템 정보, 관련 허브업체 / 업체코드, 허브업체명 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 상세 정보를 불러오지 못했습니다. | 연동 등록 업체, 회사명, 사업자 번호, 시스템 정보, 관련 허브업체 / 업체코드, 허브업체명 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 저장에 실패했습니다. | 연동 등록 업체, 회사명, 사업자 번호, 시스템 정보, 관련 허브업체 / 업체코드, 허브업체명 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 선택 가능한 허브업체가 없습니다. | 연동 등록 업체, 회사명, 사업자 번호, 시스템 정보, 관련 허브업체 / 업체코드, 허브업체명 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/ElectronicContractRoutes.tsx#L46) · [LinkedVendorManagePageDetail.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/LinkedVendorManagePageDetail.tsx#L52) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/api/linkedVendorManageApi.ts#L37) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/api/linkedVendorManageApi.ts#L48) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/api/linkedVendorManageApi.ts#L56) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 10개 중 개발 메타데이터 확인 10개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-7a729f021a7281a4) | Demo 메타데이터 10/10개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

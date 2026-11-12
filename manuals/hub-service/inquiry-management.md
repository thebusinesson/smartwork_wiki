# [연동 문의·점검·라우팅·복구] 연동업체 문의 처리 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

연동업체 문의 처리에서 **허브업체 목록** 결과를 확인한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 연동 문의·점검·라우팅·복구 |
| 언제 사용하는가 | 상세구분 트리, 허브업체 목록, 연동업체 문의 목록, 연동업체 문의 목록 다운로드 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 접수번호, 구분, 서비스, 문의업체, 연동방식, 제목 |
| 업무 흐름 | 상세구분 트리, 허브업체 목록, 연동업체 문의 목록, 연동업체 문의 목록 다운로드 |
| 이 페이지의 역할 | 조회 · 허브업체 목록 |
| 판단 결과·다음 업무 | [연동업체 문의 처리 상세](inquiry-management__by-id.md) · [연동업체 문의 처리 등록](inquiry-management__new.md) · [연동업체 문의 처리 등록](inquiry-management__by-id__edit.md) |
| 다른 화면과의 구분 | 이 경로에서 볼 수 있는 조건·결과를 기준으로 사용한다. 독립 경로의 상세·등록은 관련 화면에 연결한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 연동업체 문의 처리에서 **허브업체 목록** 결과를 확인한다. |
| 메뉴·화면 경로 | 연동 서비스 관리 > 연동 서비스 관리 > 연동업체 문의 처리 · `/hub-service/inquiry-management` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [연동업체 문의 처리 상세](inquiry-management__by-id.md) · [연동업체 문의 처리 등록](inquiry-management__new.md) · [연동업체 문의 처리 등록](inquiry-management__by-id__edit.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/hub-service/inquiry-management` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 상세구분 트리 | `/hub-service/inquiry-management` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 허브업체 목록 | `/hub-service/inquiry-management` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 연동업체 문의 목록 | `/hub-service/inquiry-management` `VIEW` | `PartnerInquirySearchRequest` `startDate`, `endDate`, `processor`, `services`, `hubCompanyKeyword`, `inquiryCompany`, `inquiryCompanyType`, `integrationMethods`, `mainCategory`, `subCategory`, `processingStatus`, `sssReport`, `keywordType`, `keyword` |
| 연동업체 문의 목록 다운로드 | `/hub-service/inquiry-management` `EXCEL_DOWNLOAD` | `PartnerInquirySearchRequest` `startDate`, `endDate`, `processor`, `services`, `hubCompanyKeyword`, `inquiryCompany`, `inquiryCompanyType`, `integrationMethods`, `mainCategory`, `subCategory`, `processingStatus`, `sssReport`, `keywordType`, `keyword` · `format: DownloadFormat` |
| 연동업체 문의 목록 등록자 원문 조회 | `/hub-service/inquiry-management` / `UNMASK` | `id`, `field` |

코드에서 확인한 버튼·작업명은 **검색**, **연동업체 문의 등록**, **다운로드**, **통합 문의 다운로드**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **연동 서비스 관리 > 연동 서비스 관리 > 연동업체 문의 처리**를 연다. `/hub-service/inquiry-management`를 연다.
2. **전체**, **처리일자**, **처리자**, **세금계산서**, **매입통합**, **전자계약**, **구매확인서** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색**, **연동업체 문의 등록**, **다운로드**, **통합 문의 다운로드** 중 해당 버튼을 선택한다.
3. **허브업체 목록** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [연동업체 문의 처리 상세](inquiry-management__by-id.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 접수번호 | 출력 | 조회 응답 기준 | 화면 필드 `receiptNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/IntegrationInquiryListPage.tsx#L95) |
| 구분 | 입력 또는 선택 | API 기본값 null | API 요청 `mainCategory` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/IntegrationInquiryListPage.tsx#L102) |
| 서비스 | 출력 | 조회 응답 기준 | 화면 필드 `serviceName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/IntegrationInquiryListPage.tsx#L109) |
| 문의업체 | 입력 또는 선택 | API 기본값 null | API 요청 `inquiryCompany` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/IntegrationInquiryListPage.tsx#L115) |
| 연동방식 | 출력 | 조회 응답 기준 | 화면 필드 `integrationMethodName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/IntegrationInquiryListPage.tsx#L129) |
| 제목 | 출력 | 조회 응답 기준 | 화면 필드 `inquiryTitle` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/IntegrationInquiryListPage.tsx#L135) |
| 등록자 | 출력 | 조회 응답 기준 | 화면 필드 `registrant` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/IntegrationInquiryListPage.tsx#L141) |
| 처리여부 | 입력 또는 선택 | API 기본값 null | API 요청 `processingStatus` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/IntegrationInquiryListPage.tsx#L163) |
| 전체 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `전체` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/IntegrationInquiryListPage.tsx#L335) |
| 처리일자 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/IntegrationInquiryListPage.tsx#L342) |
| 처리자 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/IntegrationInquiryListPage.tsx#L351) |
| 세금계산서 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `tax-invoice` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/IntegrationInquiryListPage.tsx#L33) |
| 매입통합 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `purchase-integration` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/IntegrationInquiryListPage.tsx#L34) |
| 전자계약 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `e-contract` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/IntegrationInquiryListPage.tsx#L35) |
| 구매확인서 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `purchase-confirmation` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/IntegrationInquiryListPage.tsx#L36) |
| 채권잔액 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `bond-balance` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/IntegrationInquiryListPage.tsx#L37) |
| 기타 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `etc` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/IntegrationInquiryListPage.tsx#L49) |
| 허브업체명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/IntegrationInquiryListPage.tsx#L375) |
| 문의 업체 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/IntegrationInquiryListPage.tsx#L388) |
| 사업자번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `businessNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/IntegrationInquiryListPage.tsx#L62) |
| 회사명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `companyName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/IntegrationInquiryListPage.tsx#L63) |
| 차세대(SAP) | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `next-gen-sap` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/IntegrationInquiryListPage.tsx#L47) |
| 차세대(SBMS) | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `next-gen-sbms` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/IntegrationInquiryListPage.tsx#L48) |
| 상세 구분 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/IntegrationInquiryListPage.tsx#L416) |
| 처리완료 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `completed` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/IntegrationInquiryListPage.tsx#L67) |
| 처리중 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `in-progress` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/IntegrationInquiryListPage.tsx#L68) |
| 키워드 검색 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/IntegrationInquiryListPage.tsx#L454) |
| 내용 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `inquiry-content` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/IntegrationInquiryListPage.tsx#L54) |
| 거래처담당자 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `partner-manager` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/IntegrationInquiryListPage.tsx#L55) |
| 오류코드 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `error-code` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/IntegrationInquiryListPage.tsx#L56) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 상세구분 트리 | `GET /api/v1/partner-inquiries/categories` · `/hub-service/inquiry-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/partnerinquiry/PartnerInquiryCodeController.kt#L31) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error` | 코드 연계 트랜잭션 |
| 허브업체 목록 | `GET /api/v1/partner-inquiries/hub-companies` · `/hub-service/inquiry-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/partnerinquiry/PartnerInquiryCodeController.kt#L37) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error` | `smartwork.dbo.UspSelectHubCompanyList` |
| 연동업체 문의 목록 | `GET /api/v1/partner-inquiries` · `/hub-service/inquiry-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/partnerinquiry/PartnerInquiryController.kt#L67) | `PartnerInquirySearchRequest` `startDate`, `endDate`, `processor`, `services`, `hubCompanyKeyword`, `inquiryCompany`, `inquiryCompanyType`, `integrationMethods`, `mainCategory`, `subCategory`, `processingStatus`, `sssReport`, `keywordType`, `keyword` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `size`, `currentPage` | `smartwork.dbo.UspSelectPartnerInquiryList` · 코드 연계 트랜잭션 |
| 연동업체 문의 목록 다운로드 | `GET /api/v1/partner-inquiries/download` · `/hub-service/inquiry-management` `EXCEL_DOWNLOAD` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/partnerinquiry/PartnerInquiryDownloadController.kt#L46) | `PartnerInquirySearchRequest` `startDate`, `endDate`, `processor`, `services`, `hubCompanyKeyword`, `inquiryCompany`, `inquiryCompanyType`, `integrationMethods`, `mainCategory`, `subCategory`, `processingStatus`, `sssReport`, `keywordType`, `keyword` · `format: DownloadFormat` → 파일 또는 오류 응답 | `smartwork.dbo.UspSelectPartnerInquiryList` |
| 연동업체 문의 목록 등록자 원문 조회 | `POST /api/v1/partner-inquiries/{id}/sensitive-values/reveal` · `/hub-service/inquiry-management` / `UNMASK` · [화면 컴포넌트](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/IntegrationInquiryListPage.tsx#L149) · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/partnerinquiry/PartnerInquiryController.kt#L77) | `id`, `field` → 요청한 항목의 원문 응답 | 권한 검사 후 대상 값을 조회하고 감사 기록을 남긴다. |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.UspSelectHubCompanyList` | 컬럼·결과 계약은 매퍼 참조 | 정의 참조 `office.dbo.BUSINESS`, `office.dbo.HUBPRODUCT`, `office.dbo.MNG_HUB`, `office.dbo.MNG_SYSTEM` · 하위 호출 `office.dbo.HUBPRODUCT` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/partnerinquiry/repository/PartnerInquiryCodeMapper.kt#L50) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-4a38f6f1932be431) |
| `smartwork.dbo.UspSelectPartnerInquiryList` | @FROM_DATE varchar(10), @TO_DATE varchar(10), @HANDLE_USER_SCH_TYPE varchar(1), @HANDLE_USER varchar(20), @BNS_NAME_SCH_TYPE varchar(1), @BNS_NAME varchar(70), @COM_SCH_TYPE varchar(1), @COM_SCH_VALUE varchar(70), @ROUTING_SCH_TYPE varchar(1), @ROUTING_TYPE varchar(40), @SUB_DIVISION varchar(5), @DETAIL_DIVISION varchar(5), @SSS_YN varchar(1), @KEYWORDTYPE varchar(5), @KEYWORD varchar(70), @SERVICE_SCH_TYPE varchar(1), @SERVICE_TYPE varchar(40), @ERROR_HANDLE_YN varchar(1), @DIV varchar(1), @DATEDIV varchar(1) | 정의 참조 `office.dbo.ERROR_MANAGEMENT_DETAIL`, `office.dbo.ERROR_MANAGEMENT_NEW`, `office.dbo.SAWON` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/partnerinquiry/repository/PartnerInquiryMapper.kt#L60) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-fbbd863012e7baf0) |
| `office.dbo.ERROR_MANAGEMENT_NEW` | 개발 컬럼 메타데이터 확인 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/partnerinquiry/repository/PartnerInquiryMapper.kt#L148) |
| `office.dbo.SAWON` | 개발 컬럼 메타데이터 확인 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/partnerinquiry/repository/PartnerInquiryMapper.kt#L148) |
| `smartwork.dbo.usp_sw_log_access_event_insert` | @EVENT_TYPE varchar(30) IN, @STATUS varchar(20) IN, @USER_ID bigint IN, @MEMBER_ID nvarchar(50) IN, @USER_NAME nvarchar(100) IN, @DEPARTMENT_NAME nvarchar(100) IN, @PAGE_TITLE nvarchar(200) IN, @PATH nvarchar(500) IN, @MENU_PATH nvarchar(500) IN, @MENU_LABEL nvarchar(200) IN, @CATEGORY_NAME nvarchar(200) IN, @SUB_CATEGORY_NAME nvarchar(200) IN, @MENU_ORDER int IN, @IP_ADDRESS varchar(45) IN, @USER_AGENT nvarchar(1000) IN, @BROWSER varchar(100) IN, @OS varchar(100) IN, @REFERRER nvarchar(500) IN, @DETAIL nvarchar(1000) IN, @RESULT int OUT, @COUNTS_AS_VISIT bit IN | 원문 조회 또는 감사 흐름에서 호출 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/logmanagement/repository/LogManagementMapper.kt#L92) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 접수번호, 구분, 서비스, 문의업체, 연동방식, 제목 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 연동 서비스 관리 > 연동 서비스 관리 > 연동업체 문의 처리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 다운로드에 실패했습니다. | 접수번호, 구분, 서비스, 문의업체, 연동방식, 제목 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 다운로드 중 오류가 발생했습니다. | 접수번호, 구분, 서비스, 문의업체, 연동방식, 제목 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 검색 결과가 없습니다. | 접수번호, 구분, 서비스, 문의업체, 연동방식, 제목 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/IntegrationRoutes.tsx#L123) · [IntegrationInquiryListPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/IntegrationInquiryListPage.tsx#L204) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/api/integrationInquiryApi.ts#L186) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/api/integrationInquiryApi.ts#L193) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/api/integrationInquiryApi.ts#L82) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/api/integrationInquiryApi.ts#L228) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 2개 중 개발 메타데이터 확인 2개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-59127a4e484f340c) | Demo 메타데이터 5/5개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

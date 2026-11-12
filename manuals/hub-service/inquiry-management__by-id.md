# [연동 문의·점검·라우팅·복구] 연동업체 문의 처리 상세 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

상세구분(A~G) × 세부구분(function_code_list_NEW) 트리.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 연동 문의·점검·라우팅·복구 |
| 언제 사용하는가 | 상세구분 트리, 허브업체 목록, 연동업체 문의 상세, 업체/허브 검색, 첨부파일 다운로드 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 오류 번호, 등록자, 오류 접수 일시, 허브업체명, 영업상품, 회사명 |
| 업무 흐름 | 상세구분 트리, 허브업체 목록, 연동업체 문의 상세, 업체/허브 검색, 첨부파일 다운로드 |
| 이 페이지의 역할 | 상세 · 상세구분 트리 |
| 판단 결과·다음 업무 | [연동업체 문의 처리](inquiry-management.md) · [연동업체 문의 처리 등록](inquiry-management__by-id__edit.md) |
| 다른 화면과의 구분 | 연동 서비스 관리 > 연동 서비스 관리 > 연동업체 문의 처리에서 사용하는 상세 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 선택 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/components/detail/HubCompanySearchDialog.tsx#L74) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 상세구분(A~G) × 세부구분(function_code_list_NEW) 트리. |
| 메뉴·화면 경로 | 연동 서비스 관리 > 연동 서비스 관리 > 연동업체 문의 처리 · `/hub-service/inquiry-management/:id` · 경로 변수 `id` |
| 화면 유형·담당 | 상세 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [연동업체 문의 처리](inquiry-management.md) · [연동업체 문의 처리 등록](inquiry-management__by-id__edit.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/hub-service/inquiry-management` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `id` |
| 상세구분 트리 | `/hub-service/inquiry-management` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 허브업체 목록 | `/hub-service/inquiry-management` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 연동업체 문의 상세 | `/hub-service/inquiry-management` `VIEW` | `id: Int` |
| 업체/허브 검색 | `/hub-service/inquiry-management` `VIEW` | `condition: String` · `keyword: String` |
| 첨부파일 다운로드 | `/hub-service/inquiry-management` `VIEW` | `path: String` |
| 연동업체 문의 등록 | `/hub-service/inquiry-management` `PROCESS` | `PartnerInquiryCreateRequest` `inquiryCompanyName`, `inquiryBusinessNumber`, `applicant`, `department`, `contact`, `service`, `integrationMethod`, `hubCompanyCode`, `mainCategory`, `subCategory`, `errorCode`, `inquiryTitle`, `inquiryContent`, `processingStatus` · `attachments: List<MultipartFile>?` |
| 연동업체 문의 수정 | `/hub-service/inquiry-management` `PROCESS` | `id: Int` · `PartnerInquiryUpdateRequest` `inquiryCompanyName`, `inquiryBusinessNumber`, `applicant`, `department`, `contact`, `service`, `integrationMethod`, `hubCompanyCode`, `mainCategory`, `subCategory`, `errorCode`, `inquiryTitle`, `inquiryContent`, `processingStatus` |
| 처리이력 추가 | `/hub-service/inquiry-management` `PROCESS` | `id: Int` · `ProcessingHistoryRequest` `processingContent`, `sssReport`, `processingDate`, `durationHours` · `attachments: List<MultipartFile>?` |
| 처리이력 삭제 | `/hub-service/inquiry-management` `DELETE` | `id: Int` · `detailId: Int` |
| 처리이력 수정 | `/hub-service/inquiry-management` `PROCESS` | `id: Int` · `detailId: Int` · `ProcessingHistoryRequest` `processingContent`, `sssReport`, `processingDate`, `durationHours` · `attachments: List<MultipartFile>?` |
| 연동업체 문의 삭제 | `/hub-service/inquiry-management` `DELETE` | `id: Int` |

코드에서 확인한 버튼·작업명은 **목록으로 돌아가기**, **검색**, **선택**, **처리 내역 추가**, **파일 선택**, **파일 삭제**, **취소**, **추가**, **수정**, **통합 문의 수정**, **목록**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [연동업체 문의 처리](inquiry-management.md)에서 대상 또는 작업을 선택한다. `/hub-service/inquiry-management/:id`에서 이전 화면이 전달한 `id`와 현재 대상을 확인한다.
2. **허브업체명 검색**, **업체정보 직접 입력**, **차세대(SAP)**, **차세대(SBMS)**, **기타**, **처리 내용** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색** 중 해당 버튼을 선택한다.
3. **상세구분 트리** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [연동업체 문의 처리 등록](inquiry-management__by-id__edit.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `id` |
| 오류 번호 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/components/detail/ErrorReceptionInfoSection.tsx#L25) |
| 등록자 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/components/detail/ErrorReceptionInfoSection.tsx#L31) |
| 오류 접수 일시 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/components/detail/ErrorReceptionInfoSection.tsx#L33) |
| 허브업체명 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/components/detail/InquiryCompanyInfoSection.tsx#L238) |
| 영업상품 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/components/detail/InquiryCompanyInfoSection.tsx#L240) |
| 회사명 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/components/detail/InquiryCompanyInfoSection.tsx#L244) |
| 사업자번호 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/components/detail/InquiryCompanyInfoSection.tsx#L257) |
| 문의고객 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/components/detail/InquiryCompanyInfoSection.tsx#L279) |
| 연락처 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/components/detail/InquiryCompanyInfoSection.tsx#L292) |
| 검색어를 입력하세요 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/components/detail/InquiryCompanyInfoSection.tsx#L167) |
| 허브업체명 검색 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/components/detail/InquiryCompanyInfoSection.tsx#L198) |
| 업체정보 직접 입력 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/components/detail/InquiryCompanyInfoSection.tsx#L208) |
| 업체명을 입력하세요 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/components/detail/InquiryCompanyInfoSection.tsx#L251) |
| 숫자 10자리 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/components/detail/InquiryCompanyInfoSection.tsx#L269) |
| 신청자명을 입력하세요 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/components/detail/InquiryCompanyInfoSection.tsx#L286) |
| 차세대(SAP) | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `next-gen-sap` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/components/detail/IntegrationDivisionSection.tsx#L63) |
| 차세대(SBMS) | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `next-gen-sbms` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/components/detail/IntegrationDivisionSection.tsx#L64) |
| 기타 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `etc` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/components/detail/IntegrationDivisionSection.tsx#L65) |
| 연동 방식 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/components/detail/IntegrationDivisionSection.tsx#L109) |
| 서비스 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/components/detail/IntegrationDivisionSection.tsx#L134) |
| 상세구분 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/components/detail/IntegrationDivisionSection.tsx#L161) |
| 오류코드 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/components/detail/IntegrationDivisionSection.tsx#L203) |
| 선택 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/components/detail/IntegrationDivisionSection.tsx#L190) |
| 오류코드를 입력하세요 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/components/detail/IntegrationDivisionSection.tsx#L210) |
| 제목 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/components/detail/InquiryMattersSection.tsx#L102) |
| 문의 내용 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/components/detail/InquiryMattersSection.tsx#L118) |
| 첨부파일 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/components/detail/InquiryMattersSection.tsx#L133) |
| 문의제목을 입력하세요 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/components/detail/InquiryMattersSection.tsx#L110) |
| 문의내용을 입력하세요 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/components/detail/InquiryMattersSection.tsx#L126) |
| 처리 회차 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/components/detail/ProcessingHistorySection.tsx#L151) |
| 처리 일자 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/components/detail/ProcessingHistorySection.tsx#L153) |
| 처리자 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/components/detail/ProcessingHistorySection.tsx#L155) |
| 소요시간 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/components/detail/ProcessingHistorySection.tsx#L157) |
| 처리내역 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/components/detail/ProcessingHistorySection.tsx#L161) |
| SSS Report 전송 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/components/detail/ProcessingHistorySection.tsx#L211) |
| 처리 내용 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/components/detail/ProcessingHistorySection.tsx#L399) |
| 처리 내용을 입력하세요 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/components/detail/ProcessingHistorySection.tsx#L405) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 상세구분 트리 | `GET /api/v1/partner-inquiries/categories` · `/hub-service/inquiry-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/partnerinquiry/PartnerInquiryCodeController.kt#L31) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error` | 코드 연계 트랜잭션 |
| 허브업체 목록 | `GET /api/v1/partner-inquiries/hub-companies` · `/hub-service/inquiry-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/partnerinquiry/PartnerInquiryCodeController.kt#L37) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error` | `smartwork.dbo.UspSelectHubCompanyList` |
| 연동업체 문의 상세 | `GET /api/v1/partner-inquiries/{id}` · `/hub-service/inquiry-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/partnerinquiry/PartnerInquiryController.kt#L99) | `id: Int` → `success`, `data`, `error`, `id`, `receiptNumber`, `inquiryCompany`, `integrationDivision`, `inquiryMatters`, `processingHistory`, `processingStatus`, `sssReport`, `createdAt` | `office.dbo.upGW_ViewError_NEW`, `office.dbo.UPGW_VIEW_ERROR_DETAIL`, `smartwork.dbo.partner_inquiry_attachment_meta` |
| 업체/허브 검색 | `GET /api/v1/partner-inquiries/companies/search` · `/hub-service/inquiry-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/partnerinquiry/PartnerInquiryCodeController.kt#L43) | `condition: String` · `keyword: String` → `success`, `data`, `error` | `office.dbo.upGW_LstCompany_NEW` |
| 첨부파일 다운로드 | `GET /api/v1/partner-inquiries/attachments/download` · `/hub-service/inquiry-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/partnerinquiry/PartnerInquiryFileController.kt#L37) | `path: String` → 파일 또는 오류 응답 | `smartwork.dbo.partner_inquiry_attachment_meta` |
| 연동업체 문의 등록 | `POST /api/v1/partner-inquiries` · `/hub-service/inquiry-management` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/partnerinquiry/PartnerInquiryController.kt#L112) | `PartnerInquiryCreateRequest` `inquiryCompanyName`, `inquiryBusinessNumber`, `applicant`, `department`, `contact`, `service`, `integrationMethod`, `hubCompanyCode`, `mainCategory`, `subCategory`, `errorCode`, `inquiryTitle`, `inquiryContent`, `processingStatus` · `attachments: List<MultipartFile>?` → `success`, `data`, `error`, `id` | `smartwork.dbo.UspInsertPartnerInquiryHeader`, `smartwork.dbo.partner_inquiry_attachment_meta`, `smartwork.dbo.UspSelectHubCompanyList` · 정의에서 확인한 쓰기 `office.dbo.ERROR_MANAGEMENT_NEW`, `office.dbo.ERROR_MANAGEMENT_DETAIL`, `smartwork.dbo.partner_inquiry_attachment_meta` · 코드 연계 트랜잭션 |
| 연동업체 문의 수정 | `PUT /api/v1/partner-inquiries/{id}` · `/hub-service/inquiry-management` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/partnerinquiry/PartnerInquiryController.kt#L124) | `id: Int` · `PartnerInquiryUpdateRequest` `inquiryCompanyName`, `inquiryBusinessNumber`, `applicant`, `department`, `contact`, `service`, `integrationMethod`, `hubCompanyCode`, `mainCategory`, `subCategory`, `errorCode`, `inquiryTitle`, `inquiryContent`, `processingStatus` → `success`, `data`, `error` | `office.dbo.upGW_ViewError_NEW`, `smartwork.dbo.UspUpdatePartnerInquiryHeader`, `smartwork.dbo.UspSelectHubCompanyList` · 정의에서 확인한 쓰기 `office.dbo.ERROR_MANAGEMENT_NEW` · 코드 연계 트랜잭션 |
| 처리이력 추가 | `POST /api/v1/partner-inquiries/{id}/history` · `/hub-service/inquiry-management` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/partnerinquiry/PartnerInquiryController.kt#L135) | `id: Int` · `ProcessingHistoryRequest` `processingContent`, `sssReport`, `processingDate`, `durationHours` · `attachments: List<MultipartFile>?` → `success`, `data`, `error` | `office.dbo.upGW_ViewError_NEW`, `office.dbo.upGW_SaveError_NEW`, `smartwork.dbo.partner_inquiry_attachment_meta` · 정의에서 확인한 쓰기 `office.dbo.ERROR_MANAGEMENT_NEW`, `office.dbo.ERROR_MANAGEMENT_DETAIL`, `smartwork.dbo.partner_inquiry_attachment_meta` · 코드 연계 트랜잭션 |
| 처리이력 삭제 | `DELETE /api/v1/partner-inquiries/{id}/history/{detailId}` · `/hub-service/inquiry-management` `DELETE` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/partnerinquiry/PartnerInquiryController.kt#L162) | `id: Int` · `detailId: Int` → `success`, `data`, `error` | `office.dbo.upGW_ViewError_NEW`, `smartwork.dbo.UspDeletePartnerInquiryDetail` · 정의에서 확인한 쓰기 `office.dbo.ERROR_MANAGEMENT_DETAIL` · 코드 연계 트랜잭션 |
| 처리이력 수정 | `PUT /api/v1/partner-inquiries/{id}/history/{detailId}` · `/hub-service/inquiry-management` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/partnerinquiry/PartnerInquiryController.kt#L148) | `id: Int` · `detailId: Int` · `ProcessingHistoryRequest` `processingContent`, `sssReport`, `processingDate`, `durationHours` · `attachments: List<MultipartFile>?` → `success`, `data`, `error` | `office.dbo.upGW_ViewError_NEW`, `office.dbo.upGW_SaveError_NEW`, `smartwork.dbo.partner_inquiry_attachment_meta` · 정의에서 확인한 쓰기 `office.dbo.ERROR_MANAGEMENT_NEW`, `office.dbo.ERROR_MANAGEMENT_DETAIL`, `smartwork.dbo.partner_inquiry_attachment_meta` · 코드 연계 트랜잭션 |
| 연동업체 문의 삭제 | `DELETE /api/v1/partner-inquiries/{id}` · `/hub-service/inquiry-management` `DELETE` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/partnerinquiry/PartnerInquiryController.kt#L174) | `id: Int` → `success`, `data`, `error` | `office.dbo.upGW_ViewError_NEW`, `smartwork.dbo.UspDeletePartnerInquiry` · 정의에서 확인한 쓰기 `office.dbo.ERROR_MANAGEMENT_NEW` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.UspSelectHubCompanyList` | 컬럼·결과 계약은 매퍼 참조 | 정의 참조 `office.dbo.BUSINESS`, `office.dbo.HUBPRODUCT`, `office.dbo.MNG_HUB`, `office.dbo.MNG_SYSTEM` · 하위 호출 `office.dbo.HUBPRODUCT` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/partnerinquiry/repository/PartnerInquiryCodeMapper.kt#L50) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-4a38f6f1932be431) |
| `office.dbo.upGW_ViewError_NEW` | @ERR_IDX int | 정의 참조 `office.dbo.BUSINESS`, `office.dbo.ERROR_MANAGEMENT_NEW`, `office.dbo.FUNCTION_CODE`, `office.dbo.HUBPRODUCT`, `office.dbo.SAWON` · 하위 호출 `office.dbo.HUBPRODUCT` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/partnerinquiry/repository/PartnerInquiryMapper.kt#L124) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-6fe6310f981bb64b) |
| `office.dbo.UPGW_VIEW_ERROR_DETAIL` | @ERR_IDX int | 정의 참조 `office.dbo.ERROR_MANAGEMENT_DETAIL`, `office.dbo.SAWON` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/partnerinquiry/repository/PartnerInquiryMapper.kt#L140) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-a221c00e4438d910) |
| `smartwork.dbo.partner_inquiry_attachment_meta` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/partnerinquiry/repository/PartnerInquiryAttachmentMetaMapper.kt#L56) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-4d5a74d0280f819b) |
| `office.dbo.upGW_LstCompany_NEW` | @schItem varchar(1), @schText varchar(70) | 정의 참조 `office.dbo.BUSINESS`, `office.dbo.HUBPRODUCT`, `office.dbo.MNG_HUB`, `office.dbo.MNG_SYSTEM` · 하위 호출 `office.dbo.HUBPRODUCT` · 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/partnerinquiry/repository/PartnerInquiryCodeMapper.kt#L36) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-f9604d0ef08a3e17) |
| `smartwork.dbo.UspInsertPartnerInquiryHeader` | @BNS_ID varchar(10), @BNS_NAME varchar(70), @COM_REGNO varchar(10), @COM_NAME varchar(400), @MEM_NAME varchar(200), @MEM_TEL varchar(20), @ROUTING_TYPE varchar(10), @SERVICE_TYPE varchar(10), @SUB_DIVISION varchar(5), @DETAIL_DIVISION varchar(5), @ERROR_TITLE varchar(100), @ERROR_CODE varchar(5), @ERR_CONTENT varchar(max), @ATTACH_FILE_NAME varchar(100), @CUSER int, @SSS_YN char(1), @ERR_HANDLE_YN char(1) | 정의 참조 `office.dbo.ERROR_MANAGEMENT_DETAIL`, `office.dbo.ERROR_MANAGEMENT_NEW` · 정적 쓰기 `office.dbo.ERROR_MANAGEMENT_NEW`, `office.dbo.ERROR_MANAGEMENT_DETAIL` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/partnerinquiry/repository/PartnerInquiryWriteMapper.kt#L52) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-dcb02c27279a8da9) |
| `smartwork.dbo.UspUpdatePartnerInquiryHeader` | @ERR_IDX int, @BNS_ID varchar(10), @BNS_NAME varchar(70), @COM_REGNO varchar(10), @COM_NAME varchar(400), @MEM_NAME varchar(200), @MEM_TEL varchar(20), @ROUTING_TYPE varchar(10), @SERVICE_TYPE varchar(10), @SUB_DIVISION varchar(5), @DETAIL_DIVISION varchar(5), @ERROR_TITLE varchar(100), @ERROR_CODE varchar(5), @ERR_CONTENT varchar(max), @SSS_YN char(1), @ERR_HANDLE_YN char(1), @RESULT int OUT | 정의 참조 `office.dbo.ERROR_MANAGEMENT_NEW` · 정적 쓰기 `office.dbo.ERROR_MANAGEMENT_NEW` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/partnerinquiry/repository/PartnerInquiryWriteMapper.kt#L34) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-177c0e71109ecee5) |
| `office.dbo.upGW_SaveError_NEW` | @BNS_ID varchar(10), @BNS_NAME varchar(70), @COM_REGNO varchar(10), @COM_NAME varchar(70), @MEM_NAME varchar(40), @MEM_TEL varchar(20), @ROUTING_TYPE varchar(10), @SERVICE_TYPE varchar(10), @SUB_DIVISION varchar(5), @DETAIL_DIVISION varchar(5), @ERROR_TITLE varchar(100), @ATTACH_FILE_NAME varchar(100), @ERROR_CODE varchar(5), @CUSER int, @MODE varchar(3), @ERROR_IDX int, @SSS_YN char(1), @STR_CONTENT varchar(3000), @STR_DATE varchar(10), @STR_TIME numeric(10,2), @DETAIL_IDX int, @ERR_HANDLE_YN char(1) | 정의 참조 `office.dbo.ERROR_MANAGEMENT_DETAIL`, `office.dbo.ERROR_MANAGEMENT_NEW` · 정적 쓰기 `office.dbo.ERROR_MANAGEMENT_NEW`, `office.dbo.ERROR_MANAGEMENT_DETAIL` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/partnerinquiry/repository/PartnerInquiryMapper.kt#L163) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-517c90c18e3f06a9) |
| `smartwork.dbo.UspDeletePartnerInquiryDetail` | @DETAIL_IDX int, @DUSER int, @RESULT int OUT | 정의 참조 `office.dbo.ERROR_MANAGEMENT_DETAIL` · 정적 쓰기 `office.dbo.ERROR_MANAGEMENT_DETAIL` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/partnerinquiry/repository/PartnerInquiryWriteMapper.kt#L42) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-dff8393e7b1147ec) |
| `smartwork.dbo.UspDeletePartnerInquiry` | @ERR_IDX int, @DUSER int, @RESULT int OUT | 정의 참조 `office.dbo.ERROR_MANAGEMENT_NEW` · 정적 쓰기 `office.dbo.ERROR_MANAGEMENT_NEW` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/partnerinquiry/repository/PartnerInquiryWriteMapper.kt#L38) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-e0ac61222e63c2b0) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 오류 번호, 등록자, 오류 접수 일시, 허브업체명, 영업상품, 회사명 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 연동 서비스 관리 > 연동 서비스 관리 > 연동업체 문의 처리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 문의 정보를 불러오는데 실패했습니다. | 오류 번호, 등록자, 오류 접수 일시, 허브업체명, 영업상품, 회사명 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 문의 등록에 실패했습니다. | 오류 번호, 등록자, 오류 접수 일시, 허브업체명, 영업상품, 회사명 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 문의 수정에 실패했습니다. | 오류 번호, 등록자, 오류 접수 일시, 허브업체명, 영업상품, 회사명 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 처리 이력 추가에 실패했습니다. | 오류 번호, 등록자, 오류 접수 일시, 허브업체명, 영업상품, 회사명 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/IntegrationRoutes.tsx#L124) · [IntegrationInquiryDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/integrationInquiry/IntegrationInquiryDetailPage.tsx#L13) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/api/integrationInquiryApi.ts#L186) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/api/integrationInquiryApi.ts#L193) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/api/integrationInquiryApi.ts#L89) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/api/integrationInquiryApi.ts#L209) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/api/integrationInquiryApi.ts#L217) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/api/integrationInquiryApi.ts#L125) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/api/integrationInquiryApi.ts#L135) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/api/integrationInquiryApi.ts#L145) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 10개 중 개발 메타데이터 확인 10개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-d25d460e8a1792f3) | Demo 메타데이터 10/10개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

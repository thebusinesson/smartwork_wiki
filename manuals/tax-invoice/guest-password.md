# [문서 당사자와 발행·수신 조건] 비회원 수신 비밀번호 조회 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

비회원 수신 비밀번호 목록을 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 문서 당사자와 발행·수신 조건 |
| 언제 사용하는가 | 비회원 수신 비밀번호 조회, 메일 발송 (통합) 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 작성일자, 발행일자, 매출 사업자, 매출 회사명, 매출 담당자, 매입 사업자 |
| 업무 흐름 | 비회원 수신 비밀번호 조회, 메일 발송 (통합) |
| 이 페이지의 역할 | 조회 · 비회원 수신 비밀번호 조회 |
| 판단 결과·다음 업무 | 현재 화면에서 결과를 확인한다. |
| 다른 화면과의 구분 | 같은 경로에서 열리는 조회·팝업은 이 문서에서 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 메일 발송 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/GuestPasswordList.tsx#L526) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 비회원 수신 비밀번호 목록을 조회한다. |
| 메뉴·화면 경로 | SB 서비스관리 > 전자세금계산서 > 비회원 수신 비밀번호 조회 · `/tax-invoice/guest-password` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | 현재 화면에서 결과를 확인한다. |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/tax-invoice/guest-password` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 비회원 수신 비밀번호 조회 | `/tax-invoice/guest-password` `VIEW` | `GuestPasswordSearchRequest` `fromDate`, `toDate`, `supplierSearchType`, `supplierKeyword`, `buyerSearchType`, `buyerKeyword`, `page`, `size` · 서버 필수 `buyerSearchType`, `buyerKeyword` |
| 메일 발송 (통합) | 정적 메뉴 액션 미확인 · Controller·공통 보안 검사 확인 | `MailSendRequest` `mailType`, `ids`, `items`, `emailAddress`, `title`, `emailContent`, `targetId` · 서버 필수 `mailType` |

코드에서 확인한 버튼·작업명은 **검색**, **일괄 메일 발송**, **메일 발송**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **SB 서비스관리 > 전자세금계산서 > 비회원 수신 비밀번호 조회**를 연다. `/tax-invoice/guest-password`를 연다.
2. **매입 업체 등록번호**, **공급자 조건**, **전체**, **사업자번호**, **공급받는자 조건**, **수신 이메일** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색** 중 해당 버튼을 선택한다.
3. **비회원 수신 비밀번호 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 작성일자 | 출력 | 조회 응답 기준 | 화면 필드 `createdDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/GuestPasswordList.tsx#L355) |
| 발행일자 | 출력 | 조회 응답 기준 | 화면 필드 `issueDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/GuestPasswordList.tsx#L356) |
| 매출 사업자 | 출력 | 조회 응답 기준 | 화면 필드 `salesBusinessNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/GuestPasswordList.tsx#L357) |
| 매출 회사명 | 출력 | 조회 응답 기준 | 화면 필드 `salesCompanyName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/GuestPasswordList.tsx#L358) |
| 매출 담당자 | 출력 | 조회 응답 기준 | 화면 필드 `salesManagerName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/GuestPasswordList.tsx#L359) |
| 매입 사업자 | 출력 | 조회 응답 기준 | 화면 필드 `purchaseBusinessNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/GuestPasswordList.tsx#L371) |
| 매입 업체 등록번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `BUYER_BUSINESS_NUMBER` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/GuestPasswordList.tsx#L379) |
| 매입 회사명 | 출력 | 조회 응답 기준 | 화면 필드 `purchaseCompanyName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/GuestPasswordList.tsx#L386) |
| 매입 담당자 | 출력 | 조회 응답 기준 | 화면 필드 `purchaseManagerName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/GuestPasswordList.tsx#L387) |
| 공급가액 | 출력 | 조회 응답 기준 | 화면 필드 `supplyAmount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/GuestPasswordList.tsx#L397) |
| 세액 | 출력 | 조회 응답 기준 | 화면 필드 `taxAmount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/GuestPasswordList.tsx#L398) |
| 상태 | 출력 | 조회 응답 기준 | 화면 필드 `status` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/GuestPasswordList.tsx#L399) |
| 승인일자 | 출력 | 조회 응답 기준 | 화면 필드 `approvalDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/GuestPasswordList.tsx#L400) |
| 비밀번호 | 출력 | 조회 응답 기준 | 화면 필드 `password` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/GuestPasswordList.tsx#L401) |
| 이메일 | 출력 | 조회 응답 기준 | 화면 필드 `email` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/GuestPasswordList.tsx#L404) |
| 매출업체 | 출력 | 조회 응답 기준 | 화면 필드 `salesGroup` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/GuestPasswordList.tsx#L440) |
| 매입업체 | 출력 | 조회 응답 기준 | 화면 필드 `purchaseGroup` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/GuestPasswordList.tsx#L441) |
| 사업자 | 출력 | 조회 응답 기준 | 화면 필드 `salesBusinessNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/GuestPasswordList.tsx#L450) |
| 회사명 | 출력 | 조회 응답 기준 | 화면 필드 `salesCompanyName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/GuestPasswordList.tsx#L451) |
| 담당자 | 출력 | 조회 응답 기준 | 화면 필드 `salesManagerName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/GuestPasswordList.tsx#L452) |
| 공급자 조건 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/GuestPasswordList.tsx#L91) |
| 전체 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `ALL` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/GuestPasswordList.tsx#L99) |
| 사업자번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `BIZ_NO` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/GuestPasswordList.tsx#L121) |
| 공급받는자 조건 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/GuestPasswordList.tsx#L114) |
| 수신 이메일 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/GuestPasswordList.tsx#L532) |
| 이메일을 입력하세요 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/GuestPasswordList.tsx#L539) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 비회원 수신 비밀번호 조회 | `GET /api/v1/tax-invoice/guest-passwords` · `/tax-invoice/guest-password` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/taxinvoice/guestpassword/GuestPasswordController.kt#L62) | `GuestPasswordSearchRequest` `fromDate`, `toDate`, `supplierSearchType`, `supplierKeyword`, `buyerSearchType`, `buyerKeyword`, `page`, `size` · 서버 필수 `buyerSearchType`, `buyerKeyword` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `currentPage`, `size` | `smartwork.dbo.upSBAdm_CustomerPwdList` · 코드 연계 트랜잭션 |
| 메일 발송 (통합) | `POST /api/v1/mail/send` · 정적 메뉴 액션 미확인 · Controller·공통 보안 검사 확인 · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/shared/mail/MailController.kt#L48) · [기존 상세 계약](../../references/api-contracts.md#api220) | `MailSendRequest` `mailType`, `ids`, `items`, `emailAddress`, `title`, `emailContent`, `targetId` · 서버 필수 `mailType` → `success`, `data`, `error`, `isAllSuccess`, `successCount`, `failedCount`, `message` | `SB_DTI.dbo.DTI_HEADER_CUB`, `SB_COMMON.dbo.upSBAdm_LstDTI04`, `SB_DTI_DW.dbo.DTI_HEADER_CUB`, `SB_COMMON.dbo.upSBAdm_LstDTI04_DW`, `office.dbo.upSM_mailSendList` 외 9개 · 정의에서 확인한 쓰기 `SB_DTI_LOG.dbo.DTI_CUSTOMER_PWD`, `office.dbo.ServiceMail_Send` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.upSBAdm_CustomerPwdList` | @strChkAll varchar(5), @fromDate varchar(10), @toDate varchar(10), @supItem varchar(15), @supText varchar(20), @byrItem varchar(15), @byrText varchar(20), @page int = 1, @pageSize int = 10 | 정의 참조 `master.dbo.dec_char_sel_tc`, `SB_DTI_LOG.dbo.DTI_CUSTOMER_PWD`, `SB_DTI.dbo.DTI_HEADER_CUB`, `SB_DTI.dbo.DTI_HEADER_DETAIL`, `master.dbo.enc_index_char_sel_tc` · 하위 호출 `master.dbo.dec_char_sel_tc`, `master.dbo.enc_index_char_sel_tc` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/guestpassword/repository/GuestPasswordMapper.kt#L46) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-f736d409b0b73a05) |
| `SB_DTI.dbo.DTI_HEADER_CUB` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM · 정의 참조 `sb_dti.dbo.dti_header_cub_2023_07`, `sb_dti.dbo.dti_header_cub_part`, `sb_dti.dbo.dti_header_cub_prev_buffer` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/repository/TaxInvoiceMapper.kt#L453) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-9b704ca2245fb3f1) |
| `SB_COMMON.dbo.upSBAdm_LstDTI04` | @DTI_WDAY varchar(10), @DTI_IDX int | 정의 참조 `SB_DTI_LOG.dbo.DTI_CUSTOMER_PWD`, `SB_DTI.dbo.DTI_HEADER_CUB`, `SmartBill3.dbo.fnRanByEmail`, `SB_DTI_LOG.dbo.V_DTI_CUSTOMER_PWD` · 정적 쓰기 `SB_DTI_LOG.dbo.DTI_CUSTOMER_PWD` · 하위 호출 `SmartBill3.dbo.fnRanByEmail` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/taxinvoice/repository/BonabankTaxInvoiceMapper.kt#L231) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b70e5915dd1d37bd) |
| `SB_DTI_DW.dbo.DTI_HEADER_CUB` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM · 정의 참조 `sb_dti.dbo.dti_header_cub_2020_01`, `sb_dti.dbo.dti_header_cub_2020_02`, `sb_dti.dbo.dti_header_cub_2020_03`, `sb_dti.dbo.dti_header_cub_2020_04`, `sb_dti.dbo.dti_header_cub_2020_05` 외 37개 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/legacytaxinvoice/repository/LegacyTaxInvoiceMapper.kt#L332) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-ad6e47ef0f0ed643) |
| `SB_COMMON.dbo.upSBAdm_LstDTI04_DW` | @DTI_WDAY varchar(10), @DTI_IDX int | 정의 참조 `SB_DTI_LOG.dbo.DTI_CUSTOMER_PWD`, `SB_DTI_DW.dbo.DTI_HEADER_CUB`, `SmartBill3.dbo.fnRanByEmail`, `SB_DTI_LOG.dbo.V_DTI_CUSTOMER_PWD` · 정적 쓰기 `SB_DTI_LOG.dbo.DTI_CUSTOMER_PWD` · 하위 호출 `SmartBill3.dbo.fnRanByEmail` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/legacytaxinvoice/repository/LegacyTaxInvoiceMapper.kt#L356) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-4999b219d6165194) |
| `office.dbo.upSM_mailSendList` | @DIV varchar(10) | 정의 참조 `office.dbo.ServiceMail` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/servicenoticemail/repository/EmailVendorMapper.kt#L114) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-80ee241109d15682) |
| `office.dbo.upSM_mailSend_Insert` | @TITLE varchar(100), @CONTENT text, @CUSER varchar(20), @RESULT int OUT | 정의 참조 `office.dbo.ServiceMail_Send` · 정적 쓰기 `office.dbo.ServiceMail_Send` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/servicenoticemail/repository/EmailVendorMapper.kt#L125) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-51da5c7d65aa6b46) |
| `SmartBill3.dbo.CMS_EA14` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb14AccountMapper.kt#L55) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3229f827e97f2667) |
| `SmartBill3.dbo.CMS_EA14_DETAIL_CUB` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb14AccountMapper.kt#L166) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-9a14be878da3eade) |
| `SmartBill3.dbo.COMPANY` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb14AccountMapper.kt#L166) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-0e6fcaa6b5086c07) |
| `SmartBill3.dbo.MEMBER` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb14AccountMapper.kt#L166) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-9042ff61b257b012) |
| `SmartBill3.dbo.COMMON_CODE` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb14AccountMapper.kt#L166) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-49b15682b4d4770c) |
| `SB_BILL.dbo.BILL_COMMON_CODE` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb14AccountMapper.kt#L166) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b05907f373842dd1) |
| `SmartBill3.dbo.CMS_EA22_DETAIL_CUB` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmseb22/repository/Eb22Mapper.kt#L281) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-2d8296b635adbf7b) |
| `SmartBill3.dbo.CMS_EA22` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmseb22/repository/Eb22Mapper.kt#L281) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-8cc8fe0c5cb8684a) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 작성일자, 발행일자, 매출 사업자, 매출 회사명, 매출 담당자, 매입 사업자 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 서비스관리 > 전자세금계산서 > 비회원 수신 비밀번호 조회의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 전체 선택에 실패했습니다. | 작성일자, 발행일자, 매출 사업자, 매출 회사명, 매출 담당자, 매입 사업자 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 메일 발송할 항목을 선택해주세요. | 작성일자, 발행일자, 매출 사업자, 매출 회사명, 매출 담당자, 매입 사업자 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 메일 발송 중 오류가 발생했습니다. | 작성일자, 발행일자, 매출 사업자, 매출 회사명, 매출 담당자, 매입 사업자 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 데이터가 없습니다. | 작성일자, 발행일자, 매출 사업자, 매출 회사명, 매출 담당자, 매입 사업자 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/TaxInvoiceRoutes.tsx#L42) · [GuestPasswordList.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/GuestPasswordList.tsx#L148) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/api/guestManagementApi.ts#L83) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/api/mailApi.ts#L45) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 15개 중 개발 메타데이터 확인 15개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-eb7ca70b7cc079cd) | Demo 메타데이터 15/15개 확인 · Dev와 계약 차이 3개 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

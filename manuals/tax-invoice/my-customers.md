# [문서 당사자와 발행·수신 조건] 내 거래처 조회 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

사업자번호 기준 내거래처 목록을 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 문서 당사자와 발행·수신 조건 |
| 언제 사용하는가 | 내거래처 목록 조회, 내거래처 엑셀 다운로드 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 번호, 종류, 주민/사업자번호, 주민등록번호, 성명/회사명, 담당자 |
| 업무 흐름 | 내거래처 목록 조회, 내거래처 엑셀 다운로드 |
| 이 페이지의 역할 | 조회 · 내거래처 목록 조회 |
| 판단 결과·다음 업무 | 현재 화면에서 결과를 확인한다. |
| 다른 화면과의 구분 | 같은 경로에서 열리는 조회·팝업은 이 문서에서 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 사업자번호 기준 내거래처 목록을 조회한다. |
| 메뉴·화면 경로 | SB 서비스관리 > 전자세금계산서 > 내 거래처 조회 · `/tax-invoice/my-customers` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | 현재 화면에서 결과를 확인한다. |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/tax-invoice/my-customers` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 내거래처 목록 조회 | `/tax-invoice/my-customers` `VIEW` | `MyClientSearchRequest` `comRegNo`, `searchType`, `keyword`, `email`, `clientType`, `page`, `size` · 서버 필수 `comRegNo` |
| 내거래처 엑셀 다운로드 | `/tax-invoice/my-customers` `EXCEL_DOWNLOAD` | `MyClientDownloadRequest` `comRegNo`, `searchType`, `keyword`, `email`, `clientType`, `reason` · 서버 필수 `comRegNo`, `reason` |

코드에서 확인한 버튼·작업명은 **검색**, **다운로드**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **SB 서비스관리 > 전자세금계산서 > 내 거래처 조회**를 연다. `/tax-invoice/my-customers`를 연다.
2. **주민등록번호**, **사업자 번호**, **거래처 종류**, **전체**, **회원사**, **사업자(비회원)**, **개인** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색**, **다운로드** 중 해당 버튼을 선택한다.
3. **내거래처 목록 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 번호 | 출력 | 조회 응답 기준 | 화면 필드 `rowNum` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/CustomerSearchPage.tsx#L237) |
| 종류 | 출력 | 조회 응답 기준 | 화면 필드 `typeName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/CustomerSearchPage.tsx#L241) |
| 주민/사업자번호 | 출력 | 조회 응답 기준 | 화면 필드 `registrationNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/CustomerSearchPage.tsx#L244) |
| 주민등록번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `REGISTRATION_NUMBER` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/CustomerSearchPage.tsx#L253) |
| 성명/회사명 | 출력 | 조회 응답 기준 | 화면 필드 `companyName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/CustomerSearchPage.tsx#L263) |
| 담당자 | 출력 | 조회 응답 기준 | 화면 필드 `managerName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/CustomerSearchPage.tsx#L273) |
| 이메일 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | API 요청 `email` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/CustomerSearchPage.tsx#L292) |
| 사용여부 | 출력 | 조회 응답 기준 | 화면 필드 `active` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/CustomerSearchPage.tsx#L309) |
| 등록자 | 출력 | 조회 응답 기준 | 화면 필드 `registrantName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/CustomerSearchPage.tsx#L312) |
| 사업자 번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/CustomerSearchPage.tsx#L40) |
| 거래처 종류 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/CustomerSearchPage.tsx#L55) |
| 전체 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/CustomerSearchPage.tsx#L78) |
| 회원사 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `M` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/CustomerSearchPage.tsx#L62) |
| 사업자(비회원) | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `C` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/CustomerSearchPage.tsx#L63) |
| 개인 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `P` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/CustomerSearchPage.tsx#L64) |
| 업체 조건 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/CustomerSearchPage.tsx#L70) |
| 사업자번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `R` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/CustomerSearchPage.tsx#L79) |
| 회사명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `C` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/CustomerSearchPage.tsx#L80) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 내거래처 목록 조회 | `GET /api/v1/tax-invoice/my-clients` · `/tax-invoice/my-customers` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/taxinvoice/myclient/MyClientController.kt#L67) | `MyClientSearchRequest` `comRegNo`, `searchType`, `keyword`, `email`, `clientType`, `page`, `size` · 서버 필수 `comRegNo` → `success`, `data`, `error`, `comRegNo`, `clientShareYn`, `content`, `totalElements`, `totalPages`, `currentPage`, `size` | `smartwork.dbo.SSP_ADMIN_MYCLIENT`, `SmartBill3.dbo.COMPANY`, `SmartBill3.dbo.MEMBER`, `SB_DTI.dbo.DTI_MYCLIENT_CUB`, `SB_DTI.dbo.DTI_MYCLIENT_MEMBER` 외 1개 · 코드 연계 트랜잭션 |
| 내거래처 엑셀 다운로드 | `POST /api/v1/tax-invoice/my-clients/download` · `/tax-invoice/my-customers` `EXCEL_DOWNLOAD` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/taxinvoice/myclient/MyClientController.kt#L111) | `MyClientDownloadRequest` `comRegNo`, `searchType`, `keyword`, `email`, `clientType`, `reason` · 서버 필수 `comRegNo`, `reason` → 파일 또는 오류 응답 | `smartwork.dbo.SSP_ADMIN_MYCLIENT`, `smartwork.dbo.action_reason` · 정의에서 확인한 쓰기 `smartwork.dbo.action_reason` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.SSP_ADMIN_MYCLIENT` | @COM_REGNO1 varchar(32), @SCHTYPE varchar(1), @COM_KEYWORD varchar(70), @MEM_EMAIL varchar(30), @COM_TYPE varchar(1), @PAGE_NUMBER int = 1, @PAGE_SIZE int = 10 | 정의 참조 `master.dbo.enc_index_char_sel_tc` · 하위 호출 `master.dbo.enc_index_char_sel_tc` · 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/myclient/repository/MyClientMapper.kt#L38) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-ccbf1373942c5872) |
| `SmartBill3.dbo.COMPANY` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/myclient/repository/MyClientMapper.kt#L88) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-0e6fcaa6b5086c07) |
| `SmartBill3.dbo.MEMBER` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/myclient/repository/MyClientMapper.kt#L88) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-9042ff61b257b012) |
| `SB_DTI.dbo.DTI_MYCLIENT_CUB` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/myclient/repository/MyClientMapper.kt#L88) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-e0675d2932298196) |
| `SB_DTI.dbo.DTI_MYCLIENT_MEMBER` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/myclient/repository/MyClientMapper.kt#L88) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-1bc42eac86f068af) |
| `SB_DTI.dbo.COMPANY_DTICONFIG` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/myclient/repository/MyClientMapper.kt#L131) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-2fa3ac3de7960ed7) |
| `smartwork.dbo.action_reason` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL INSERT INTO | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/shared/actionreason/repository/ActionReasonMapper.kt#L16) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b0430106ffe0743f) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 번호, 종류, 주민/사업자번호, 주민등록번호, 성명/회사명, 담당자 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 서비스관리 > 전자세금계산서 > 내 거래처 조회의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 다운로드할 검색 결과가 없습니다. | 번호, 종류, 주민/사업자번호, 주민등록번호, 성명/회사명, 담당자 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/TaxInvoiceRoutes.tsx#L33) · [CustomerSearchPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/CustomerSearchPage.tsx#L111) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/api/customerSearchApi.ts#L87) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/api/customerSearchApi.ts#L94) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 7개 중 개발 메타데이터 확인 7개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-3fdf438496913d6e) | Demo 메타데이터 7/7개 확인 · Dev와 계약 차이 2개 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

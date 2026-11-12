# [오픈스크랩 대상·수집과 결과] 업체 관리 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

검색조건(전체/사업자번호/회사명)으로 오픈스크랩 허브업체 목록을 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 오픈스크랩 대상·수집과 결과 |
| 언제 사용하는가 | 업체 목록 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 업체 조건, 전체, 사업자번호, 회사명, 인증코드, 사업자목록 |
| 업무 흐름 | 업체 목록 |
| 이 페이지의 역할 | 조회 · 업체 목록 |
| 판단 결과·다음 업무 | [업체 관리 상세](vendors__by-id.md) |
| 다른 화면과의 구분 | 이 경로에서 볼 수 있는 조건·결과를 기준으로 사용한다. 독립 경로의 상세·등록은 관련 화면에 연결한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 검색조건(전체/사업자번호/회사명)으로 오픈스크랩 허브업체 목록을 조회한다. |
| 메뉴·화면 경로 | SB 서비스관리 > 오픈스크랩 > 업체 관리 · `/openscrap/vendors` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [업체 관리 상세](vendors__by-id.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/openscrap/vendors` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 업체 목록 | `/openscrap/vendors` `VIEW` | `OpenscrapVendorSearchRequest` `searchType`, `searchTerm`, `page`, `size` |

코드에서 확인한 버튼·작업명은 **검색**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **SB 서비스관리 > 오픈스크랩 > 업체 관리**를 연다. `/openscrap/vendors`를 연다.
2. **업체 조건**, **전체**, **사업자번호**, **회사명** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색** 중 해당 버튼을 선택한다.
3. **업체 목록** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [업체 관리 상세](vendors__by-id.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 업체 조건 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/VendorListPage.tsx#L78) |
| 전체 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `all` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/VendorListPage.tsx#L84) |
| 사업자번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `사업자번호` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/VendorListPage.tsx#L85) |
| 회사명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `회사명` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/VendorListPage.tsx#L86) |
| 인증코드 | 출력 | 조회 응답 기준 | 화면 필드 `authCode` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/VendorListPage.tsx#L39) |
| 사업자목록 | 출력 | 조회 응답 기준 | 화면 필드 `businessList` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/VendorListPage.tsx#L42) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 업체 목록 | `GET /api/v1/openscrap/vendors` · `/openscrap/vendors` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/openscrap/vendor/OpenscrapVendorController.kt#L48) | `OpenscrapVendorSearchRequest` `searchType`, `searchTerm`, `page`, `size` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `currentPage`, `size` | `smartwork.dbo.usp_os_vendor_list_select` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.usp_os_vendor_list_select` | @PAGE int = 1, @PAGE_SIZE int = 10, @SEARCH_TYPE char(1), @SEARCH_TEXT varchar(100) | 정의 참조 `SmartBill3.dbo.COMPANY`, `SB_OPENSCRAP.dbo.fnOS_CompanyInfoNameList`, `SB_DTI.dbo.NEOBILL_AUTHCODE`, `SB_OPENSCRAP.dbo.OS_COMPANY_INFO` · 하위 호출 `SB_OPENSCRAP.dbo.fnOS_CompanyInfoNameList` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/openscrap/vendor/repository/OpenscrapVendorMapper.kt#L44) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-6ad2fcffcd9129fa) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 업체 조건, 전체, 사업자번호, 회사명, 인증코드, 사업자목록 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 서비스관리 > 오픈스크랩 > 업체 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/OpenscrapRoutes.tsx#L14) · [VendorListPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/VendorListPage.tsx#L100) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/openscrap/api/vendorApi.ts#L105) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 1개 중 개발 메타데이터 확인 1개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-66ed7b01e4e1b017) | Demo 메타데이터 1/1개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

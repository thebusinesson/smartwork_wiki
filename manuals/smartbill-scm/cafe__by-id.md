# [카페·SCM·사업장 운영] 카페 조회 상세 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

목록에서 선택한 카페의 기본정보와 회원을 조회한다. 유료게시판 메뉴 타이틀은 해당 메뉴에서 상세 확인한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 카페·SCM·사업장 운영 |
| 언제 사용하는가 | 카페 회원 목록 조회 (페이징), 카페 상세 조회, 유료게시판 메뉴 타이틀 상세 조회 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 카페 ID, 기본정보, 회원, 유료게시판 메뉴 |
| 업무 흐름 | 카페 회원 목록 조회 (페이징), 카페 상세 조회, 유료게시판 메뉴 타이틀 상세 조회 |
| 이 페이지의 역할 | 상세 · 카페 상세 조회 |
| 판단 결과·다음 업무 | [카페 조회](cafe.md) |
| 다른 화면과의 구분 | SB 서비스관리 > SCM > 카페 조회에서 사용하는 상세 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 목록에서 선택한 카페의 기본정보와 회원을 조회한다. 유료게시판 메뉴 타이틀은 해당 메뉴에서 상세 확인한다. |
| 메뉴·화면 경로 | SB 서비스관리 > SCM > 카페 조회 · `/smartbill-scm/cafe/:id` · 경로 변수 `id` |
| 화면 유형·담당 | 상세 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [카페 조회](cafe.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/smartbill-scm/cafe` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `id` |
| 카페 회원 목록 조회 (페이징) | `/smartbill-scm/cafe` `VIEW` | `cafeId: String` · `CafeMemberSearchRequest` `page`, `size`, `startDate`, `endDate`, `searchType`, `searchValue`, `status` |
| 카페 상세 조회 | `/smartbill-scm/cafe` `VIEW` | `cafeId: String` |
| 유료게시판 메뉴 타이틀 상세 조회 | `/smartbill-scm/cafe` `VIEW` | `menuNo: Int` |
| 카페 운영자 아이디·이름 원문 조회 | `/smartbill-scm/cafe` / `UNMASK` | `cafeId`, `memNo`, `field` |

코드에서 확인한 버튼·작업명은 **검색**, **목록**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [카페 조회](cafe.md)에서 대상 또는 작업을 선택한다. `/smartbill-scm/cafe/:id`에서 이전 화면이 전달한 `id`와 현재 대상을 확인한다.
2. **카페 가입일**, **가입 업체**, **전체**, **회원 상태**, **가입**, **탈퇴** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색** 중 해당 버튼을 선택한다.
3. **카페 상세 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [카페 조회](cafe.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `id` |
| 운영자 ID | 출력 | 조회 응답 기준 | 화면 필드 `operatorId` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/CafeDetailPage.tsx#L244) |
| 운영자명 | 출력 | 조회 응답 기준 | 화면 필드 `operatorName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/CafeDetailPage.tsx#L245) |
| 사업자번호 | 출력 | 조회 응답 기준 | 화면 필드 `businessNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/CafeDetailPage.tsx#L253) |
| 회사명 | 출력 | 조회 응답 기준 | 화면 필드 `companyName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/CafeDetailPage.tsx#L254) |
| 운영자 등록일 | 출력 | 조회 응답 기준 | 화면 필드 `registrationDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/CafeDetailPage.tsx#L248) |
| 카페가입일 | 출력 | 조회 응답 기준 | 화면 필드 `joinDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/CafeDetailPage.tsx#L252) |
| 담당자(닉네임) | 출력 | 조회 응답 기준 | 화면 필드 `managerNickname` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/CafeDetailPage.tsx#L255) |
| 상태 | 입력 또는 선택 | 서버 형식 검사 · API 기본값 "all" | API 요청 `status` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/CafeDetailPage.tsx#L256) |
| 메뉴생성일 | 출력 | 조회 응답 기준 | 화면 필드 `menuCreationDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/CafeDetailPage.tsx#L260) |
| 메뉴명 | 출력 | 조회 응답 기준 | API 응답 `menuName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/CafeDetailPage.tsx#L263) |
| 프로세스ID | 출력 | 조회 응답 기준 | 화면 필드 `processId` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/CafeDetailPage.tsx#L277) |
| 프로세스명 | 출력 | 조회 응답 기준 | 화면 필드 `processName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/CafeDetailPage.tsx#L278) |
| 메뉴등록자 | 출력 | 조회 응답 기준 | 화면 필드 `menuRegistrant` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/CafeDetailPage.tsx#L279) |
| 인쇄양식 | 출력 | 조회 응답 기준 | 화면 필드 `printFormat` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/CafeDetailPage.tsx#L280) |
| 타이틀 | 출력 | 조회 응답 기준 | 화면 필드 `title` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/CafeDetailPage.tsx#L281) |
| 메뉴상태 | 출력 | 조회 응답 기준 | 화면 필드 `menuStatus` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/CafeDetailPage.tsx#L282) |
| 카페 가입일 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/CafeDetailPage.tsx#L42) |
| 가입 업체 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/CafeDetailPage.tsx#L52) |
| 전체 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `all` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/CafeDetailPage.tsx#L80) |
| 회원 상태 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/CafeDetailPage.tsx#L74) |
| 가입 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `joined` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/CafeDetailPage.tsx#L81) |
| 탈퇴 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `withdrawn` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/CafeDetailPage.tsx#L82) |
| 번호 | 출력 | 조회 응답 기준 | 화면 필드 `id` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/components/PaidBoardMenuDialog.tsx#L61) |
| 타이틀명 | 출력 | 조회 응답 기준 | 화면 필드 `title` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/components/PaidBoardMenuDialog.tsx#L62) |
| 사이즈 | 입력 또는 선택 | 최소 1 · 최대 100 · API 기본값 10 | API 요청 `size` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/components/PaidBoardMenuDialog.tsx#L63) |
| 순서 | 출력 | 조회 응답 기준 | 화면 필드 `order` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/components/PaidBoardMenuDialog.tsx#L64) |
| 정렬 | 출력 | 조회 응답 기준 | 화면 필드 `alignment` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/components/PaidBoardMenuDialog.tsx#L65) |
| 숫자 | 출력 | 조회 응답 기준 | 화면 필드 `displayOnScreen` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/components/PaidBoardMenuDialog.tsx#L68) |
| 화면표시여부 | 출력 | 조회 응답 기준 | 화면 필드 `hidden` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/components/PaidBoardMenuDialog.tsx#L69) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 카페 회원 목록 조회 (페이징) | `GET /api/v1/smartbill-scm/cafes/{cafeId}/members` · `/smartbill-scm/cafe` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/smartbillscm/cafelookup/CafeLookupController.kt#L139) | `cafeId: String` · `CafeMemberSearchRequest` `page`, `size`, `startDate`, `endDate`, `searchType`, `searchValue`, `status` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `currentPage`, `size` | `smartwork.dbo.usp_taxcafe_member_list_select` |
| 카페 상세 조회 | `GET /api/v1/smartbill-scm/cafes/{cafeId}` · `/smartbill-scm/cafe` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/smartbillscm/cafelookup/CafeLookupController.kt#L124) | `cafeId: String` → `success`, `data`, `error`, `detail`, `operators`, `paidBoards` | `SmartBill3.dbo.TAX_MAIN`, `SmartBill3.dbo.COMPANY`, `SmartBill3.dbo.upAdmSB_SchTaxAdmin`, `SmartBill3.dbo.upAdmSB_SchTaxProcessID` |
| 유료게시판 메뉴 타이틀 상세 조회 | `GET /api/v1/smartbill-scm/cafes/menus/{menuNo}` · `/smartbill-scm/cafe` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/smartbillscm/cafelookup/CafeLookupController.kt#L156) | `menuNo: Int` → `success`, `data`, `error`, `menuId`, `menuName`, `details`, `totalCount` | `SmartBill3.dbo.upAdmSB_SchTaxTitle` |
| 카페 운영자 아이디·이름 원문 조회 | `POST /api/v1/smartbill-scm/cafes/{cafeId}/operators/{memNo}/sensitive-values/reveal` · `/smartbill-scm/cafe` / `UNMASK` · [화면 컴포넌트](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/CafeDetailPage.tsx#L233) · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/smartbillscm/cafelookup/CafeLookupController.kt#L95) | `cafeId`, `memNo`, `field` → 요청한 항목의 원문 응답 | 권한 검사 후 대상 값을 조회하고 감사 기록을 남긴다. |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.usp_taxcafe_member_list_select` | @cafeId varchar(15), @PAGE int = 1, @PAGE_SIZE int = 10, @fromDate varchar(10), @toDate varchar(10), @strItem varchar(100), @strContents varchar(100), @memStatus varchar(2) | 정의 참조 `SmartBill3.dbo.COMPANY`, `SmartBill3.dbo.MEMBER`, `SmartBill3.dbo.TAX_MEMBER` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/smartbillscm/cafelookup/repository/CafeLookupMapper.kt#L138) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-178a4f7cbcce845a) |
| `SmartBill3.dbo.TAX_MAIN` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/smartbillscm/cafelookup/repository/CafeLookupMapper.kt#L75) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-d1d0036962b6ad5c) |
| `SmartBill3.dbo.COMPANY` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/smartbillscm/cafelookup/repository/CafeLookupMapper.kt#L75) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-0e6fcaa6b5086c07) |
| `SmartBill3.dbo.upAdmSB_SchTaxAdmin` | @cafe_id varchar(15) | 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/smartbillscm/cafelookup/repository/CafeLookupMapper.kt#L93) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-a8599ff743a2902e) |
| `SmartBill3.dbo.upAdmSB_SchTaxProcessID` | @cafe_id varchar(15) | 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/smartbillscm/cafelookup/repository/CafeLookupMapper.kt#L158) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-ef05408047e77e0f) |
| `SmartBill3.dbo.upAdmSB_SchTaxTitle` | @menu_no no | 정의 참조 `smartbill3.dbo.no` · 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/smartbillscm/cafelookup/repository/CafeLookupMapper.kt#L174) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-a35469996aa60a2e) |
| `SmartBill3.dbo.TAX_ADMIN` | 개발 컬럼 메타데이터 확인 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/smartbillscm/cafelookup/repository/CafeLookupMapper.kt#L113) |
| `SmartBill3.dbo.MEMBER` | 개발 컬럼 메타데이터 확인 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/smartbillscm/cafelookup/repository/CafeLookupMapper.kt#L113) |
| `smartwork.dbo.usp_sw_log_access_event_insert` | @EVENT_TYPE varchar(30) IN, @STATUS varchar(20) IN, @USER_ID bigint IN, @MEMBER_ID nvarchar(50) IN, @USER_NAME nvarchar(100) IN, @DEPARTMENT_NAME nvarchar(100) IN, @PAGE_TITLE nvarchar(200) IN, @PATH nvarchar(500) IN, @MENU_PATH nvarchar(500) IN, @MENU_LABEL nvarchar(200) IN, @CATEGORY_NAME nvarchar(200) IN, @SUB_CATEGORY_NAME nvarchar(200) IN, @MENU_ORDER int IN, @IP_ADDRESS varchar(45) IN, @USER_AGENT nvarchar(1000) IN, @BROWSER varchar(100) IN, @OS varchar(100) IN, @REFERRER nvarchar(500) IN, @DETAIL nvarchar(1000) IN, @RESULT int OUT, @COUNTS_AS_VISIT bit IN | 원문 조회 또는 감사 흐름에서 호출 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/logmanagement/repository/LogManagementMapper.kt#L92) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 카페 ID, 기본정보, 회원, 유료게시판 메뉴 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 서비스관리 > SCM > 카페 조회의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 등록된 운영자가 없습니다. | 카페 ID, 기본정보, 회원, 유료게시판 메뉴 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 검색 결과가 존재하지 않습니다. | 카페 ID, 기본정보, 회원, 유료게시판 메뉴 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 등록된 유료 게시판이 없습니다. | 카페 ID, 기본정보, 회원, 유료게시판 메뉴 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 데이터가 없습니다. | 카페 ID, 기본정보, 회원, 유료게시판 메뉴 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/SmartbillScmRoutes.tsx#L12) · [CafeDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/CafeDetailPage.tsx#L123) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/api/cafeApi.ts#L114) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/api/cafeApi.ts#L86) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/api/cafeApi.ts#L124) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 6개 중 개발 메타데이터 확인 6개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-21b05b799650d660) | Demo 메타데이터 9/9개 확인 · Dev와 계약 차이 1개 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

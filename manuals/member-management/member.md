# [회사·회원·서비스 권한] 회원 정보 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

회원 정보 목록을 검색한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 회사·회원·서비스 권한 |
| 언제 사용하는가 | 회원 목록 조회, 회원 민감정보 원문 조회 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 실명, 닉네임, 아이디, 연락처, 이메일, 가입일 |
| 업무 흐름 | 회원 목록 조회, 회원 민감정보 원문 조회 |
| 이 페이지의 역할 | 조회 · 회원 목록 조회 |
| 판단 결과·다음 업무 | [회원 정보 상세](member__by-id.md) · [회원 정보 변경 이력](member__by-id__change-history.md) |
| 다른 화면과의 구분 | 이 경로에서 볼 수 있는 조건·결과를 기준으로 사용한다. 독립 경로의 상세·등록은 관련 화면에 연결한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 회원 정보 목록을 검색한다. |
| 메뉴·화면 경로 | SB 고객관리 > 스마트빌 회원·회사정보 관리 > 회원 정보 · `/member-management/member` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [회원 정보 상세](member__by-id.md) · [회원 정보 변경 이력](member__by-id__change-history.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/member-management/member` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 회원 목록 조회 | `/member-management/member` `VIEW` | `MemberInfoSearchRequest` `dateStart`, `dateEnd`, `companyCondition`, `companyValue`, `personalCondition`, `personalValue`, `memberType`, `memberCategory`, `memberStatus`, `page`, `size`, `sortDirection` |
| 회원 민감정보 원문 조회 | `/member-management/member` `UNMASK` | `memNo: Long` · `MemberSensitiveValueRevealRequest` `field` |

코드에서 확인한 버튼·작업명은 **검색**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **SB 고객관리 > 스마트빌 회원·회사정보 관리 > 회원 정보**를 연다. `/member-management/member`를 연다.
2. **날짜 조건**, **업체 조건**, **개인 조건**, **회원 구분**, **회원 종류**, **회원 상태** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색** 중 해당 버튼을 선택한다.
3. **회원 목록 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [회원 정보 상세](member__by-id.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 실명 | 출력 | 조회 응답 기준 | 화면 필드 `realName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/MemberManagementPage.tsx#L272) |
| 닉네임 | 출력 | 조회 응답 기준 | 화면 필드 `nickname` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/MemberManagementPage.tsx#L273) |
| 아이디 | 출력 | 조회 응답 기준 | 화면 필드 `userId` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/MemberManagementPage.tsx#L274) |
| 연락처 | 출력 | 조회 응답 기준 | 화면 필드 `contact` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/MemberManagementPage.tsx#L275) |
| 이메일 | 출력 | 조회 응답 기준 | 화면 필드 `email` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/MemberManagementPage.tsx#L276) |
| 가입일 | 출력 | 조회 응답 기준 | 화면 필드 `joinDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/MemberManagementPage.tsx#L277) |
| 종류 | 출력 | 조회 응답 기준 | 화면 필드 `category` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/MemberManagementPage.tsx#L278) |
| 상태 | 출력 | 조회 응답 기준 | 화면 필드 `status` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/MemberManagementPage.tsx#L279) |
| 사업자/주민 번호 | 출력 | 조회 응답 기준 | 화면 필드 `businessNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/MemberManagementPage.tsx#L282) |
| 회사명 | 출력 | 조회 응답 기준 | 화면 필드 `companyName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/MemberManagementPage.tsx#L300) |
| 날짜 조건 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/MemberManagementPage.tsx#L80) |
| 업체 조건 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/MemberManagementPage.tsx#L94) |
| 개인 조건 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/MemberManagementPage.tsx#L115) |
| 회원 구분 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/MemberManagementPage.tsx#L138) |
| 회원 종류 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/MemberManagementPage.tsx#L151) |
| 회원 상태 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/MemberManagementPage.tsx#L164) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 회원 목록 조회 | `GET /api/v1/members` · `/member-management/member` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/customer/member/MemberInfoController.kt#L89) | `MemberInfoSearchRequest` `dateStart`, `dateEnd`, `companyCondition`, `companyValue`, `personalCondition`, `personalValue`, `memberType`, `memberCategory`, `memberStatus`, `page`, `size`, `sortDirection` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `currentPage`, `size` | `smartwork.dbo.usp_member_info_count_select`, `smartwork.dbo.usp_member_info_list_select` · 코드 연계 트랜잭션 |
| 회원 민감정보 원문 조회 | `POST /api/v1/members/{memNo}/sensitive-values/reveal` · `/member-management/member` `UNMASK` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/customer/member/MemberInfoController.kt#L106) · [기존 상세 계약](../../references/api-contracts.md#api221) | `memNo: Long` · `MemberSensitiveValueRevealRequest` `field` → `success`, `data`, `error`, `field`, `value` | `smartwork.dbo.usp_sw_log_access_event_insert` · 정의에서 확인한 쓰기 `smartwork.dbo.sw_log_access_event` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.usp_member_info_count_select` | @FROM_DATE varchar(10), @TO_DATE varchar(10), @COMP_ITEM varchar(20), @COMP_TEXT varchar(100), @PERS_ITEM varchar(20), @PERS_TEXT varchar(100), @MEM_TYPE varchar(10), @MEM_STATUS varchar(10) | 정의 참조 `SmartBill3.dbo.COMPANY`, `SB_DTI_LOG.dbo.DORMANT_MEMBER`, `SmartBill3.dbo.MEMBER` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/member/repository/MemberInfoMapper.kt#L52) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-1478b4335cca5dfd) |
| `smartwork.dbo.usp_member_info_list_select` | @PAGE int, @PAGESIZE int, @FROM_DATE varchar(10), @TO_DATE varchar(10), @COMP_ITEM varchar(20), @COMP_TEXT varchar(100), @PERS_ITEM varchar(20), @PERS_TEXT varchar(100), @MEM_TYPE varchar(10), @MEM_STATUS varchar(10), @SORT_DIR varchar(4) | 정의 참조 `SmartBill3.dbo.COMPANY`, `SB_DTI_LOG.dbo.DORMANT_MEMBER`, `SmartBill3.dbo.MEMBER` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/member/repository/MemberInfoMapper.kt#L76) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-acf8046281eb62a4) |
| `smartwork.dbo.usp_sw_log_access_event_insert` | @EVENT_TYPE varchar(30), @STATUS varchar(20), @USER_ID bigint = NULL, @MEMBER_ID nvarchar(50) = NULL, @USER_NAME nvarchar(100) = NULL, @DEPARTMENT_NAME nvarchar(100) = NULL, @PAGE_TITLE nvarchar(200) = NULL, @PATH nvarchar(500) = NULL, @MENU_PATH nvarchar(500) = NULL, @MENU_LABEL nvarchar(200) = NULL, @CATEGORY_NAME nvarchar(200) = NULL, @SUB_CATEGORY_NAME nvarchar(200) = NULL, @MENU_ORDER int = NULL, @IP_ADDRESS varchar(45) = NULL, @USER_AGENT nvarchar(1000) = NULL, @BROWSER varchar(100) = NULL, @OS varchar(100) = NULL, @REFERRER nvarchar(500) = NULL, @DETAIL nvarchar(1000) = NULL, @RESULT int OUT, @COUNTS_AS_VISIT bit = 1 | 정의 참조 `smartwork.dbo.sw_log_access_event` · 정적 쓰기 `smartwork.dbo.sw_log_access_event` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/logmanagement/repository/LogManagementMapper.kt#L92) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b7ba94e0cc2f35c0) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 실명, 닉네임, 아이디, 연락처, 이메일, 가입일 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 고객관리 > 스마트빌 회원·회사정보 관리 > 회원 정보의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 데이터를 불러오는 중 오류가 발생했습니다. | 실명, 닉네임, 아이디, 연락처, 이메일, 가입일 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/CustomerRoutes.tsx#L41) · [MemberManagementPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/MemberManagementPage.tsx#L183) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/api/memberManagementApi.ts#L67) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/api/memberManagementApi.ts#L75) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 3개 중 개발 메타데이터 확인 3개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-eb98e597f5d55054) | Demo 메타데이터 3/3개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

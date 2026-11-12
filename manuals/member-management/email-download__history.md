# [회사·회원·서비스 권한] 회원 이메일 다운로드 내역 조회 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

회원 이메일 다운로드 내역을 페이징 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 회사·회원·서비스 권한 |
| 언제 사용하는가 | 다운로드 내역 조회 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 다운로드 일시, 다운로드 갯수, 다운로드 항목, 처리자, 다운로드 사유, 사유 |
| 업무 흐름 | 다운로드 내역 조회 |
| 이 페이지의 역할 | 이력 · 다운로드 내역 조회 |
| 판단 결과·다음 업무 | [회원 이메일 다운로드](email-download.md) |
| 다른 화면과의 구분 | SB 고객관리 > 스마트빌 회원·회사정보 관리 > 회원 이메일 다운로드에서 사용하는 이력 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 회원 이메일 다운로드 내역을 페이징 조회한다. |
| 메뉴·화면 경로 | SB 고객관리 > 스마트빌 회원·회사정보 관리 > 회원 이메일 다운로드 · `/member-management/email-download/history` |
| 화면 유형·담당 | 이력 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [회원 이메일 다운로드](email-download.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/member-management/email-download` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 다운로드 내역 조회 | `/member-management/email-download` `VIEW` | `page: Int` · `size: Int` |
| 다운로드 내역 처리자명 원문 조회 | `/member-management/email-download` / `UNMASK` | `id`, `field` |

코드에서 확인한 버튼·작업명은 **보기**, **이전**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [회원 이메일 다운로드](email-download.md)에서 대상 또는 작업을 선택한다. `/member-management/email-download/history`를 연다.
2. **사유**에서 조회 조건과 결과의 대상이 맞는지 확인한다.
3. **다운로드 내역 조회** 처리 결과를 확인하고 받은 파일의 대상과 적용 조건을 대조한다.
4. 후속 조회나 목록 복귀가 필요하면 [회원 이메일 다운로드](email-download.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 다운로드 일시 | 출력 | 조회 응답 기준 | 화면 필드 `downloadDateTime` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/emailDownload/components/MemberEmailDownloadHistoryTable.tsx#L31) |
| 다운로드 갯수 | 출력 | 조회 응답 기준 | 화면 필드 `downloadCount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/emailDownload/components/MemberEmailDownloadHistoryTable.tsx#L37) |
| 다운로드 항목 | 출력 | 조회 응답 기준 | 화면 필드 `downloadItems` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/emailDownload/components/MemberEmailDownloadHistoryTable.tsx#L44) |
| 처리자 | 출력 | 조회 응답 기준 | 화면 필드 `processor` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/emailDownload/components/MemberEmailDownloadHistoryTable.tsx#L49) |
| 다운로드 사유 | 출력 | 조회 응답 기준 | 화면 필드 `reason` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/emailDownload/components/MemberEmailDownloadHistoryTable.tsx#L64) |
| 사유 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/emailDownload/components/MemberEmailDownloadReasonDetailDialog.tsx#L38) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 다운로드 내역 조회 | `GET /api/v1/members/email-download/history` · `/member-management/email-download` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/customer/member/MemberEmailDownloadController.kt#L145) | `page: Int` · `size: Int` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `currentPage`, `size` | `smartwork.dbo.usp_member_email_download_history_select` |
| 다운로드 내역 처리자명 원문 조회 | `POST /api/v1/members/email-download/history/{id}/sensitive-values/reveal` · `/member-management/email-download` / `UNMASK` · [화면 컴포넌트](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/emailDownload/components/MemberEmailDownloadHistoryTable.tsx#L54) · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/customer/member/MemberEmailDownloadController.kt#L156) | `id`, `field` → 요청한 항목의 원문 응답 | 권한 검사 후 대상 값을 조회하고 감사 기록을 남긴다. |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.usp_member_email_download_history_select` | @PAGE int, @PAGESIZE int | 정의 참조 `smartwork.dbo.action_reason`, `office.dbo.SAWON` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/member/repository/MemberInfoMapper.kt#L135) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-a92d735fefac5d82) |
| `smartwork.dbo.action_reason` | 개발 컬럼 메타데이터 확인 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/member/repository/MemberInfoMapper.kt#L151) |
| `office.dbo.SAWON` | 개발 컬럼 메타데이터 확인 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/member/repository/MemberInfoMapper.kt#L151) |
| `smartwork.dbo.usp_sw_log_access_event_insert` | @EVENT_TYPE varchar(30) IN, @STATUS varchar(20) IN, @USER_ID bigint IN, @MEMBER_ID nvarchar(50) IN, @USER_NAME nvarchar(100) IN, @DEPARTMENT_NAME nvarchar(100) IN, @PAGE_TITLE nvarchar(200) IN, @PATH nvarchar(500) IN, @MENU_PATH nvarchar(500) IN, @MENU_LABEL nvarchar(200) IN, @CATEGORY_NAME nvarchar(200) IN, @SUB_CATEGORY_NAME nvarchar(200) IN, @MENU_ORDER int IN, @IP_ADDRESS varchar(45) IN, @USER_AGENT nvarchar(1000) IN, @BROWSER varchar(100) IN, @OS varchar(100) IN, @REFERRER nvarchar(500) IN, @DETAIL nvarchar(1000) IN, @RESULT int OUT, @COUNTS_AS_VISIT bit IN | 원문 조회 또는 감사 흐름에서 호출 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/logmanagement/repository/LogManagementMapper.kt#L92) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 다운로드 일시, 다운로드 갯수, 다운로드 항목, 처리자, 다운로드 사유, 사유 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 고객관리 > 스마트빌 회원·회사정보 관리 > 회원 이메일 다운로드의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 데이터가 없습니다. | 다운로드 일시, 다운로드 갯수, 다운로드 항목, 처리자, 다운로드 사유, 사유 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/CustomerRoutes.tsx#L48) · [MemberEmailDownloadHistoryPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/emailDownload/MemberEmailDownloadHistoryPage.tsx#L12) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/api/memberEmailDownloadApi.ts#L139) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 1개 중 개발 메타데이터 확인 1개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-c3951371d1ed8a24) | Demo 메타데이터 4/4개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

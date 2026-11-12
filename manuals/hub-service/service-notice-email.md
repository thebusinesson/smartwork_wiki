# [서비스 공지 메일과 발송 이력] 메일 발송 업체 관리 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

메일 발송 업체 관리에서 **메일링 업체 목록 (검색 + 페이징)** 결과를 확인한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 서비스 공지 메일과 발송 이력 |
| 언제 사용하는가 | 메일링 업체 목록 (검색 + 페이징) 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 사업자번호, 회사명(업체명), 이메일, 담당자명, 업체 조건, 전체 |
| 업무 흐름 | 메일링 업체 목록 (검색 + 페이징) |
| 이 페이지의 역할 | 조회 · 메일링 업체 목록 (검색 + 페이징) |
| 판단 결과·다음 업무 | [메일 발송 업체 관리 등록](service-notice-email__new.md) · [메일 발송 업체 관리 상세](service-notice-email__by-id.md) |
| 다른 화면과의 구분 | 이 경로에서 볼 수 있는 조건·결과를 기준으로 사용한다. 독립 경로의 상세·등록은 관련 화면에 연결한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 메일 발송 업체 관리에서 **메일링 업체 목록 (검색 + 페이징)** 결과를 확인한다. |
| 메뉴·화면 경로 | 연동 서비스 관리 > 서비스 공지 메일관리 > 메일 발송 업체 관리 · `/hub-service/service-notice-email` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [메일 발송 업체 관리 등록](service-notice-email__new.md) · [메일 발송 업체 관리 상세](service-notice-email__by-id.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/hub-service/service-notice-email` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 메일링 업체 목록 (검색 + 페이징) | `/hub-service/service-notice-email` `VIEW` | `page: Int` · `pageSize: Int` · `vendorSearchType: String` · `searchValue: String?` |
| 메일링 업체 민감정보 원문 조회 | `/hub-service/service-notice-email` / `UNMASK` | `id`, `field` |

코드에서 확인한 버튼·작업명은 **검색**, **발송 업체 등록**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **연동 서비스 관리 > 서비스 공지 메일관리 > 메일 발송 업체 관리**를 연다. `/hub-service/service-notice-email`를 연다.
2. **업체 조건**, **전체**, **회사명** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색**, **발송 업체 등록** 중 해당 버튼을 선택한다.
3. **메일링 업체 목록 (검색 + 페이징)** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [메일 발송 업체 관리 등록](service-notice-email__new.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 사업자번호 | 출력 | 조회 응답 기준 | 화면 필드 `businessNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/serviceNoticeEmail/ServiceNoticeEmailPage.tsx#L128) |
| 회사명(업체명) | 출력 | 조회 응답 기준 | 화면 필드 `companyName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/serviceNoticeEmail/ServiceNoticeEmailPage.tsx#L135) |
| 이메일 | 출력 | 조회 응답 기준 | 화면 필드 `email` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/serviceNoticeEmail/ServiceNoticeEmailPage.tsx#L141) |
| 담당자명 | 출력 | 조회 응답 기준 | 화면 필드 `contactName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/serviceNoticeEmail/ServiceNoticeEmailPage.tsx#L156) |
| 업체 조건 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/serviceNoticeEmail/ServiceNoticeEmailPage.tsx#L24) |
| 전체 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `all` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/serviceNoticeEmail/ServiceNoticeEmailPage.tsx#L30) |
| 회사명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `companyName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/serviceNoticeEmail/ServiceNoticeEmailPage.tsx#L32) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 메일링 업체 목록 (검색 + 페이징) | `GET /api/v1/service-notice-email` · `/hub-service/service-notice-email` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/servicenoticemail/ServiceNoticeEmailVendorController.kt#L73) | `page: Int` · `pageSize: Int` · `vendorSearchType: String` · `searchValue: String?` → `success`, `data`, `error`, `items`, `total`, `page`, `pageSize` | `office.dbo.upSM_mailComList` · 코드 연계 트랜잭션 |
| 메일링 업체 민감정보 원문 조회 | `POST /api/v1/service-notice-email/{id}/sensitive-values/reveal` · `/hub-service/service-notice-email` / `UNMASK` · [화면 컴포넌트](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/serviceNoticeEmail/ServiceNoticeEmailPage.tsx#L161) · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/servicenoticemail/ServiceNoticeEmailVendorController.kt#L109) | `id`, `field` → 요청한 항목의 원문 응답 | 권한 검사 후 대상 값을 조회하고 감사 기록을 남긴다. |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `office.dbo.upSM_mailComList` | @PAGENUM int, @PAGESIZE int | 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/servicenoticemail/repository/EmailVendorMapper.kt#L53) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-dcf5c0aba79a23a8) |
| `office.dbo.ServiceMail` | 개발 컬럼 메타데이터 확인 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/servicenoticemail/repository/EmailVendorMapper.kt#L75) |
| `smartwork.dbo.usp_sw_log_access_event_insert` | @EVENT_TYPE varchar(30) IN, @STATUS varchar(20) IN, @USER_ID bigint IN, @MEMBER_ID nvarchar(50) IN, @USER_NAME nvarchar(100) IN, @DEPARTMENT_NAME nvarchar(100) IN, @PAGE_TITLE nvarchar(200) IN, @PATH nvarchar(500) IN, @MENU_PATH nvarchar(500) IN, @MENU_LABEL nvarchar(200) IN, @CATEGORY_NAME nvarchar(200) IN, @SUB_CATEGORY_NAME nvarchar(200) IN, @MENU_ORDER int IN, @IP_ADDRESS varchar(45) IN, @USER_AGENT nvarchar(1000) IN, @BROWSER varchar(100) IN, @OS varchar(100) IN, @REFERRER nvarchar(500) IN, @DETAIL nvarchar(1000) IN, @RESULT int OUT, @COUNTS_AS_VISIT bit IN | 원문 조회 또는 감사 흐름에서 호출 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/logmanagement/repository/LogManagementMapper.kt#L92) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 사업자번호, 회사명(업체명), 이메일, 담당자명, 업체 조건, 전체 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 연동 서비스 관리 > 서비스 공지 메일관리 > 메일 발송 업체 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 검색 결과가 없습니다. | 사업자번호, 회사명(업체명), 이메일, 담당자명, 업체 조건, 전체 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/IntegrationRoutes.tsx#L127) · [ServiceNoticeEmailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/serviceNoticeEmail/ServiceNoticeEmailPage.tsx#L54) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/api/serviceNoticeEmailApi.ts#L33) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 1개 중 개발 메타데이터 확인 1개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-b5a721da8e7f8af0) | Demo 메타데이터 3/3개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

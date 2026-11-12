# [서비스 도입·제휴 문의와 제한] 블랙리스트 관리 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

블랙리스트 관리에서 **블랙리스트 목록** 결과를 확인한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 서비스 도입·제휴 문의와 제한 |
| 언제 사용하는가 | 블랙리스트 목록, 블랙리스트 등록, 블랙리스트 삭제 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 검색 조건, 전체, 개별 E-mail 검색, 등록일 |
| 업무 흐름 | 블랙리스트 목록, 블랙리스트 등록, 블랙리스트 삭제 |
| 이 페이지의 역할 | 조회·관리 · 블랙리스트 목록 |
| 판단 결과·다음 업무 | 현재 화면에서 결과를 확인한다. |
| 다른 화면과의 구분 | 같은 경로에서 열리는 조회·팝업은 이 문서에서 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 삭제 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/customersupport/BlacklistManagePage.tsx#L347) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 블랙리스트 관리에서 **블랙리스트 목록** 결과를 확인한다. |
| 메뉴·화면 경로 | 고객지원 > 고객 문의 관리 > 블랙리스트 관리 · `/customer-support/blacklist` |
| 화면 유형·담당 | 조회·관리 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | 현재 화면에서 결과를 확인한다. |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/customer-support/blacklist` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 블랙리스트 목록 | `/customer-support/blacklist` `VIEW` | `BlacklistSearchRequest` `type`, `email`, `page`, `size` |
| 블랙리스트 등록 | `/customer-support/blacklist` `PROCESS` | `BlacklistAddRequest` `email` · 서버 필수 `email` |
| 블랙리스트 삭제 | `/customer-support/blacklist` `DELETE` | `id: Long` |
| 블랙리스트 이메일 원문 조회 | `/customer-support/blacklist` / `UNMASK` | `id`, `field` |

코드에서 확인한 버튼·작업명은 **검색**, **삭제**, **등록**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **고객지원 > 고객 문의 관리 > 블랙리스트 관리**를 연다. `/customer-support/blacklist`를 연다.
2. **검색 조건**, **전체**, **개별 E-mail 검색** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색**, **등록** 중 해당 버튼을 선택한다.
3. **블랙리스트 목록** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 검색 조건 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/customersupport/BlacklistManagePage.tsx#L171) |
| 전체 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `all` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/customersupport/BlacklistManagePage.tsx#L184) |
| 개별 E-mail 검색 | 입력 또는 선택 | 길이·개수 최대 80 · API 기본값 null | API 요청 `email` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/customersupport/BlacklistManagePage.tsx#L185) |
| 등록일 | 출력 | 조회 응답 기준 | 화면 필드 `createdAt` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/customersupport/BlacklistManagePage.tsx#L243) |
| E-mail을 입력하세요 | 입력 또는 선택 | 길이·개수 최대 80 · API 기본값 null | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/customersupport/BlacklistManagePage.tsx#L302) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 블랙리스트 목록 | `GET /api/v1/customer-support/blacklists` · `/customer-support/blacklist` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/support/customersupport/blacklist/BlacklistController.kt#L69) | `BlacklistSearchRequest` `type`, `email`, `page`, `size` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `currentPage`, `size` | `office.dbo.upSW_SERVICE_BLACKLIST` · 코드 연계 트랜잭션 |
| 블랙리스트 등록 | `POST /api/v1/customer-support/blacklists` · `/customer-support/blacklist` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/support/customersupport/blacklist/BlacklistController.kt#L88) | `BlacklistAddRequest` `email` · 서버 필수 `email` → `success`, `data`, `error` | `office.dbo.upSW_ADD_SB_BLACKLIST` · 정의에서 확인한 쓰기 `office.dbo.SB_BLACKLIST` · 코드 연계 트랜잭션 |
| 블랙리스트 삭제 | `DELETE /api/v1/customer-support/blacklists/{id}` · `/customer-support/blacklist` `DELETE` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/support/customersupport/blacklist/BlacklistController.kt#L102) | `id: Long` → `success`, `data`, `error` | `office.dbo.upSW_DEL_SB_BLACKLIST` · 정의에서 확인한 쓰기 `office.dbo.SB_BLACKLIST` · 코드 연계 트랜잭션 |
| 블랙리스트 이메일 원문 조회 | `POST /api/v1/customer-support/blacklists/{id}/sensitive-values/reveal` · `/customer-support/blacklist` / `UNMASK` · [화면 컴포넌트](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/customersupport/BlacklistManagePage.tsx#L250) · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/support/customersupport/blacklist/BlacklistController.kt#L112) | `id`, `field` → 요청한 항목의 원문 응답 | 권한 검사 후 대상 값을 조회하고 감사 기록을 남긴다. |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `office.dbo.upSW_SERVICE_BLACKLIST` | @SEARCHGUBUN varchar(10), @SEARCHTEXT varchar(80) | 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/customersupport/blacklist/repository/BlacklistMapper.kt#L43) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-189e1743b0f4fd80) |
| `office.dbo.upSW_ADD_SB_BLACKLIST` | @EMAIL varchar(300), @SW_NO int, @GUBUN nvarchar(50) | 정의 참조 `office.dbo.SB_BLACKLIST` · 정적 쓰기 `office.dbo.SB_BLACKLIST` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/customersupport/blacklist/repository/BlacklistMapper.kt#L57) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-fe0292a624671432) |
| `office.dbo.upSW_DEL_SB_BLACKLIST` | @IDX int, @GUBUN nvarchar(50) | 정의 참조 `office.dbo.SB_BLACKLIST` · 정적 쓰기 `office.dbo.SB_BLACKLIST` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/customersupport/blacklist/repository/BlacklistMapper.kt#L70) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-e4c6177e61cdbd92) |
| `smartwork.dbo.usp_sw_log_access_event_insert` | @EVENT_TYPE varchar(30) IN, @STATUS varchar(20) IN, @USER_ID bigint IN, @MEMBER_ID nvarchar(50) IN, @USER_NAME nvarchar(100) IN, @DEPARTMENT_NAME nvarchar(100) IN, @PAGE_TITLE nvarchar(200) IN, @PATH nvarchar(500) IN, @MENU_PATH nvarchar(500) IN, @MENU_LABEL nvarchar(200) IN, @CATEGORY_NAME nvarchar(200) IN, @SUB_CATEGORY_NAME nvarchar(200) IN, @MENU_ORDER int IN, @IP_ADDRESS varchar(45) IN, @USER_AGENT nvarchar(1000) IN, @BROWSER varchar(100) IN, @OS varchar(100) IN, @REFERRER nvarchar(500) IN, @DETAIL nvarchar(1000) IN, @RESULT int OUT, @COUNTS_AS_VISIT bit IN | 원문 조회 또는 감사 흐름에서 호출 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/logmanagement/repository/LogManagementMapper.kt#L92) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 검색 조건, 전체, 개별 E-mail 검색, 등록일 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 고객지원 > 고객 문의 관리 > 블랙리스트 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/CustomerSupportRoutes.tsx#L119) · [BlacklistManagePage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/customersupport/BlacklistManagePage.tsx#L45) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/customersupport/api/blacklistApi.ts#L27) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/customersupport/api/blacklistApi.ts#L32) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/customersupport/api/blacklistApi.ts#L37) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 3개 중 개발 메타데이터 확인 3개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-68c2f1826f36fc05) | Demo 메타데이터 4/4개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

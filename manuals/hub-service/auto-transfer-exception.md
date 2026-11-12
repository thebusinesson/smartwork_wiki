# [연동 문의·점검·라우팅·복구] 자동이체 예외 설정 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

자동이체 예외 설정에서 **자동이체 예외업체 목록 조회** 결과를 확인한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 연동 문의·점검·라우팅·복구 |
| 언제 사용하는가 | 자동이체 예외업체 목록 조회, 자동이체 예외업체 일괄 등록 샘플 다운로드, 자동이체 예외업체 일괄 등록 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 사업자번호, 회사명, 연동여부, 업체 조건 |
| 업무 흐름 | 자동이체 예외업체 목록 조회, 자동이체 예외업체 일괄 등록 샘플 다운로드, 자동이체 예외업체 일괄 등록 |
| 이 페이지의 역할 | 조회 · 자동이체 예외업체 목록 조회 |
| 판단 결과·다음 업무 | [자동이체 예외 설정 상세](auto-transfer-exception__by-id.md) · [자동이체 예외업체 등록](auto-transfer-exception__new.md) |
| 다른 화면과의 구분 | 이 경로에서 볼 수 있는 조건·결과를 기준으로 사용한다. 독립 경로의 상세·등록은 관련 화면에 연결한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 업로드 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/autoTransferException/components/bulk/BulkUploadDialog.tsx#L132) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 자동이체 예외 설정에서 **자동이체 예외업체 목록 조회** 결과를 확인한다. |
| 메뉴·화면 경로 | 연동 서비스 관리 > 연동 서비스 관리 > 자동이체 예외 설정 · `/hub-service/auto-transfer-exception` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [자동이체 예외 설정 상세](auto-transfer-exception__by-id.md) · [자동이체 예외업체 등록](auto-transfer-exception__new.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/hub-service/auto-transfer-exception` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 자동이체 예외업체 목록 조회 | `/hub-service/auto-transfer-exception` `VIEW` | `AutoTransferExceptionSearchRequest` `searchType`, `searchKeyword`, `page`, `size`, `pageSize` |
| 자동이체 예외업체 일괄 등록 샘플 다운로드 | `/hub-service/auto-transfer-exception` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 자동이체 예외업체 일괄 등록 | `/hub-service/auto-transfer-exception` `EXCEL_UPLOAD` | `file: MultipartFile` |
| 자동이체 예외업체 등록번호 원문 조회 | `/hub-service/auto-transfer-exception` / `UNMASK` | `revealId`, `field` |

코드에서 확인한 버튼·작업명은 **검색**, **일괄 등록**, **자동이체 예외 등록**, **업로드**, **양식 다운로드**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **연동 서비스 관리 > 연동 서비스 관리 > 자동이체 예외 설정**를 연다. `/hub-service/auto-transfer-exception`를 연다.
2. **업체 조건** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색**, **일괄 등록**, **자동이체 예외 등록**, **양식 다운로드** 중 해당 버튼을 선택한다.
3. **자동이체 예외업체 목록 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [자동이체 예외 설정 상세](auto-transfer-exception__by-id.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 사업자번호 | 출력 | 조회 응답 기준 | 화면 필드 `businessNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/autoTransferException/AutoTransferExceptionListPage.tsx#L39) |
| 회사명 | 출력 | 조회 응답 기준 | 화면 필드 `companyName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/autoTransferException/AutoTransferExceptionListPage.tsx#L58) |
| 연동여부 | 출력 | 조회 응답 기준 | 화면 필드 `isIntegrated` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/autoTransferException/AutoTransferExceptionListPage.tsx#L64) |
| 업체 조건 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/autoTransferException/AutoTransferExceptionListPage.tsx#L132) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 자동이체 예외업체 목록 조회 | `GET /api/v1/hub-service/auto-transfer-exception` · `/hub-service/auto-transfer-exception` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/autotransferexception/AutoTransferExceptionController.kt#L63) | `AutoTransferExceptionSearchRequest` `searchType`, `searchKeyword`, `page`, `size`, `pageSize` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `currentPage`, `size` | `office.dbo.SSP_AUTO_EXCEPT` · 코드 연계 트랜잭션 |
| 자동이체 예외업체 일괄 등록 샘플 다운로드 | `GET /api/v1/hub-service/auto-transfer-exception/template` · `/hub-service/auto-transfer-exception` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/autotransferexception/AutoTransferExceptionController.kt#L153) | 추가 입력은 Controller 서명 참조 → 파일 또는 오류 응답 | 직접 DB 호출이 연결된 경로는 현재 소스에서 미확인. 세부 저장소는 Controller와 Service 참조. |
| 자동이체 예외업체 일괄 등록 | `POST /api/v1/hub-service/auto-transfer-exception/bulk-upload` · `/hub-service/auto-transfer-exception` `EXCEL_UPLOAD` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/autotransferexception/AutoTransferExceptionController.kt#L139) | `file: MultipartFile` → `success`, `data`, `error`, `successCount`, `failureCount`, `errors` | `office.dbo.SSP_EXCEPT_INSERT` · 정의에서 확인한 쓰기 `office.dbo.MNG_COMPANY_EXCEPT`, `office.dbo.MNG_COMPANY_EXCEPT_HIS` · 코드 연계 트랜잭션 |
| 자동이체 예외업체 등록번호 원문 조회 | `POST /api/v1/hub-service/auto-transfer-exception/records/{revealId}/sensitive-values/reveal` · `/hub-service/auto-transfer-exception` / `UNMASK` · [화면 컴포넌트](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/autoTransferException/AutoTransferExceptionListPage.tsx#L45) · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/autotransferexception/AutoTransferExceptionController.kt#L167) | `revealId`, `field` → 요청한 항목의 원문 응답 | 권한 검사 후 대상 값을 조회하고 감사 기록을 남긴다. |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `office.dbo.SSP_AUTO_EXCEPT` | @DIV varchar(7), @TXTSEARCH varchar(70), @PAGENUM int, @PAGESIZE int | 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/autotransferexception/repository/AutoTransferExceptionMapper.kt#L40) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-ed592f13a1367218) |
| `office.dbo.SSP_EXCEPT_INSERT` | @COM_REGNO varchar(13), @EXCEPT_CODE1 varchar(20), @EXCEPT_CODE2 varchar(20), @EXCEPT_CODE3 varchar(20), @EXCEPT_CODE4 varchar(20), @CUSER varchar(20), @DIVISION varchar(7), @RESULT varchar(1) OUT | 정의 참조 `office.dbo.MNG_COMPANY_EXCEPT`, `office.dbo.MNG_COMPANY_EXCEPT_HIS` · 정적 쓰기 `office.dbo.MNG_COMPANY_EXCEPT`, `office.dbo.MNG_COMPANY_EXCEPT_HIS` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/autotransferexception/repository/AutoTransferExceptionMapper.kt#L57) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-288b8718040da13a) |
| `office.dbo.MNG_COMPANY_EXCEPT` | 개발 컬럼 메타데이터 확인 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/autotransferexception/repository/AutoTransferExceptionMapper.kt#L82) |
| `smartwork.dbo.usp_sw_log_access_event_insert` | @EVENT_TYPE varchar(30) IN, @STATUS varchar(20) IN, @USER_ID bigint IN, @MEMBER_ID nvarchar(50) IN, @USER_NAME nvarchar(100) IN, @DEPARTMENT_NAME nvarchar(100) IN, @PAGE_TITLE nvarchar(200) IN, @PATH nvarchar(500) IN, @MENU_PATH nvarchar(500) IN, @MENU_LABEL nvarchar(200) IN, @CATEGORY_NAME nvarchar(200) IN, @SUB_CATEGORY_NAME nvarchar(200) IN, @MENU_ORDER int IN, @IP_ADDRESS varchar(45) IN, @USER_AGENT nvarchar(1000) IN, @BROWSER varchar(100) IN, @OS varchar(100) IN, @REFERRER nvarchar(500) IN, @DETAIL nvarchar(1000) IN, @RESULT int OUT, @COUNTS_AS_VISIT bit IN | 원문 조회 또는 감사 흐름에서 호출 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/logmanagement/repository/LogManagementMapper.kt#L92) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 사업자번호, 회사명, 연동여부, 업체 조건 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 연동 서비스 관리 > 연동 서비스 관리 > 자동이체 예외 설정의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 검색 결과가 없습니다. | 사업자번호, 회사명, 연동여부, 업체 조건 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 양식 다운로드에 실패했습니다. | 사업자번호, 회사명, 연동여부, 업체 조건 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/IntegrationRoutes.tsx#L145) · [AutoTransferExceptionListPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/autoTransferException/AutoTransferExceptionListPage.tsx#L78) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/api/autoTransferExceptionApi.ts#L35) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/api/autoTransferExceptionApi.ts#L92) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/api/autoTransferExceptionApi.ts#L82) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 2개 중 개발 메타데이터 확인 2개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-b103c49273440f01) | Demo 메타데이터 4/4개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

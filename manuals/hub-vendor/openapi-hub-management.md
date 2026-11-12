# [시스템 키·벌크계좌·업체 연결 설정] OpenAPI 허브 관리 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

OpenAPI 허브 관리에서 **OpenAPI 허브 관리 목록 조회** 결과를 확인한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 시스템 키·벌크계좌·업체 연결 설정 |
| 언제 사용하는가 | OpenAPI 허브 관리 목록 조회, OpenAPI 허브 관리 목록 엑셀 다운로드 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 업체 조건, 허브업체명, 사업자번호/회사명, 업체코드, 도입모델, 인증방식 |
| 업무 흐름 | OpenAPI 허브 관리 목록 조회, OpenAPI 허브 관리 목록 엑셀 다운로드 |
| 이 페이지의 역할 | 조회 · OpenAPI 허브 관리 목록 조회 |
| 판단 결과·다음 업무 | [OAPI 허브 등록](openapi-hub-management__new.md) · [OpenAPI 허브 관리 상세](openapi-hub-management__by-hubId.md) |
| 다른 화면과의 구분 | 이 경로에서 볼 수 있는 조건·결과를 기준으로 사용한다. 독립 경로의 상세·등록은 관련 화면에 연결한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | OpenAPI 허브 관리에서 **OpenAPI 허브 관리 목록 조회** 결과를 확인한다. |
| 메뉴·화면 경로 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > OpenAPI 허브 관리 · `/hub-vendor/openapi-hub-management` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [OAPI 허브 등록](openapi-hub-management__new.md) · [OpenAPI 허브 관리 상세](openapi-hub-management__by-hubId.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/hub-vendor/openapi-hub-management` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| OpenAPI 허브 관리 목록 조회 | `/hub-vendor/openapi-hub-management` `VIEW` | `OpenApiHubSearchRequest` `page`, `size`, `companyCondition`, `companyConditionValue`, `hubNameCondition`, `hubNames` |
| OpenAPI 허브 관리 목록 엑셀 다운로드 | `/hub-vendor/openapi-hub-management` `EXCEL_DOWNLOAD` | `OpenApiHubSearchRequest` `page`, `size`, `companyCondition`, `companyConditionValue`, `hubNameCondition`, `hubNames` |

코드에서 확인한 버튼·작업명은 **검색**, **OAPI 허브 등록**, **다운로드**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **연동/허브 업체 관리 > 연동/허브 업체 관리 > OpenAPI 허브 관리**를 연다. `/hub-vendor/openapi-hub-management`를 연다.
2. **업체 조건**, **허브업체명** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색**, **OAPI 허브 등록**, **다운로드** 중 해당 버튼을 선택한다.
3. **OpenAPI 허브 관리 목록 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [OAPI 허브 등록](openapi-hub-management__new.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 업체 조건 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/OpenApiHubManagementPage.tsx#L218) |
| 허브업체명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/OpenApiHubManagementPage.tsx#L235) |
| 사업자번호/회사명 | 출력 | 조회 응답 기준 | 화면 필드 `companies` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/OpenApiHubManagementPage.tsx#L56) |
| 업체코드 | 출력 | 조회 응답 기준 | 화면 필드 `hubCode` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/OpenApiHubManagementPage.tsx#L77) |
| 도입모델 | 출력 | 조회 응답 기준 | 화면 필드 `adoptionModel` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/OpenApiHubManagementPage.tsx#L83) |
| 인증방식 | 출력 | 조회 응답 기준 | 화면 필드 `authenticationMethod` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/OpenApiHubManagementPage.tsx#L90) |
| 서명방식 | 출력 | 조회 응답 기준 | 화면 필드 `signatureMethod` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/OpenApiHubManagementPage.tsx#L97) |
| 개발언어 | 출력 | 조회 응답 기준 | 화면 필드 `developmentLanguage` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/OpenApiHubManagementPage.tsx#L104) |
| 사용 API | 출력 | 조회 응답 기준 | 화면 필드 `apiUsageCount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/OpenApiHubManagementPage.tsx#L111) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| OpenAPI 허브 관리 목록 조회 | `GET /api/v1/hub-vendor/openapi-hubs` · `/hub-vendor/openapi-hub-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/openapihubmgmt/OpenApiHubController.kt#L59) | `OpenApiHubSearchRequest` `page`, `size`, `companyCondition`, `companyConditionValue`, `hubNameCondition`, `hubNames` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `currentPage`, `size` | `smartwork.dbo.usp_openapi_hub_list_select` |
| OpenAPI 허브 관리 목록 엑셀 다운로드 | `GET /api/v1/hub-vendor/openapi-hubs/download` · `/hub-vendor/openapi-hub-management` `EXCEL_DOWNLOAD` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/openapihubmgmt/OpenApiHubController.kt#L76) | `OpenApiHubSearchRequest` `page`, `size`, `companyCondition`, `companyConditionValue`, `hubNameCondition`, `hubNames` → 파일 또는 오류 응답 | `smartwork.dbo.usp_sw_log_system_event_insert`, `smartwork.dbo.usp_openapi_hub_list_select` · 정의에서 확인한 쓰기 `smartwork.dbo.sw_log_system_event` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.usp_openapi_hub_list_select` | @PAGE int = 1, @PAGE_SIZE int = 10, @ComSchCode char(1), @ComSchContent varchar(50), @HubNameYn char(1), @HubNames varchar(max) | 정의 참조 `office.dbo.BUSINESS`, `SmartBill3.dbo.COMPANY`, `office.dbo.MNG_HUB`, `office.dbo.MNG_HUB_DETAIL`, `SB_DTI.dbo.OPENAPI_HUB` 외 2개 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/openapihubmgmt/repository/OpenApiHubMapper.kt#L56) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-8c8fba7d7093c485) |
| `smartwork.dbo.usp_sw_log_system_event_insert` | @LEVEL varchar(10), @CATEGORY varchar(30), @SOURCE nvarchar(200) = NULL, @MESSAGE nvarchar(1000), @REQUEST_PATH nvarchar(500) = NULL, @HTTP_METHOD varchar(10) = NULL, @USER_ID bigint = NULL, @MEMBER_ID nvarchar(50) = NULL, @STATUS_CODE int = NULL, @DURATION_MS bigint = NULL, @IP_ADDRESS varchar(45) = NULL, @USER_AGENT nvarchar(1000) = NULL, @DETAIL nvarchar(max) = NULL, @RESULT int OUT | 정의 참조 `smartwork.dbo.sw_log_system_event` · 정적 쓰기 `smartwork.dbo.sw_log_system_event` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/logmanagement/repository/LogManagementMapper.kt#L115) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-30344bbc069b2be3) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 업체 조건, 허브업체명, 사업자번호/회사명, 업체코드, 도입모델, 인증방식 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > OpenAPI 허브 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 검색 결과가 없습니다. | 업체 조건, 허브업체명, 사업자번호/회사명, 업체코드, 도입모델, 인증방식 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/IntegrationRoutes.tsx#L118) · [OpenApiHubManagementPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/OpenApiHubManagementPage.tsx#L151) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/openApiHubManagement/api/openApiHubManagementApi.ts#L142) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/openApiHubManagement/api/openApiHubManagementApi.ts#L232) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 2개 중 개발 메타데이터 확인 2개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-002f723df52d0931) | Demo 메타데이터 2/2개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

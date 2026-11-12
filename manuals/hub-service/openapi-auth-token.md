# [OpenAPI 인증·로그·인증서 구분] OpenAPI 인증토큰 관리 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

현행·과거 인증토큰 발급 이력을 통합 검색한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | OpenAPI 인증·로그·인증서 구분 |
| 언제 사용하는가 | OpenAPI 인증토큰 발급 이력 조회, OpenAPI 인증토큰 복호화 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 발급일자, 사업자번호, 스마트빌 아이디, 만료일자, 인증토큰, 검색 조건 |
| 업무 흐름 | OpenAPI 인증토큰 발급 이력 조회, OpenAPI 인증토큰 복호화 |
| 이 페이지의 역할 | 조회 · OpenAPI 인증토큰 발급 이력 조회 |
| 판단 결과·다음 업무 | 현재 화면에서 결과를 확인한다. |
| 다른 화면과의 구분 | 같은 경로에서 열리는 조회·팝업은 이 문서에서 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 현행·과거 인증토큰 발급 이력을 통합 검색한다. |
| 메뉴·화면 경로 | 연동 서비스 관리 > 연동 서비스 관리 > OpenAPI 인증토큰 관리 · `/hub-service/openapi-auth-token` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | 현재 화면에서 결과를 확인한다. |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/hub-service/openapi-auth-token` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| OpenAPI 인증토큰 발급 이력 조회 | `/hub-service/openapi-auth-token` `VIEW` | `OpenApiAuthTokenSearchRequest` `searchType`, `searchValue`, `page`, `pageSize` |
| OpenAPI 인증토큰 복호화 | `/hub-service/openapi-auth-token` `VIEW` | `OpenApiAuthTokenDecryptRequest` `encryptedToken` · 서버 필수 `encryptedToken` |

코드에서 확인한 버튼·작업명은 **검색**, **복호화**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **연동 서비스 관리 > 연동 서비스 관리 > OpenAPI 인증토큰 관리**를 연다. `/hub-service/openapi-auth-token`를 연다.
2. **검색 조건** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색** 중 해당 버튼을 선택한다.
3. **OpenAPI 인증토큰 발급 이력 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 발급일자 | 출력 | 조회 응답 기준 | 화면 필드 `issuedAt` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/OpenApiAuthTokenPage.tsx#L34) |
| 사업자번호 | 출력 | 조회 응답 기준 | API 응답 `businessNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/OpenApiAuthTokenPage.tsx#L41) |
| 스마트빌 아이디 | 출력 | 조회 응답 기준 | API 응답 `smartBillId` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/OpenApiAuthTokenPage.tsx#L48) |
| 만료일자 | 출력 | 조회 응답 기준 | API 응답 `expirationDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/OpenApiAuthTokenPage.tsx#L63) |
| 인증토큰 | 출력 | 조회 응답 기준 | 화면 필드 `authToken` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/OpenApiAuthTokenPage.tsx#L69) |
| 검색 조건 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/OpenApiAuthTokenPage.tsx#L82) |
| 암호화된 인증토큰을 입력하세요 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/openApiAuthToken/components/decrypt/TokenDecryptionSection.tsx#L48) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| OpenAPI 인증토큰 발급 이력 조회 | `GET /api/v1/hub/auth-tokens/search` · `/hub-service/openapi-auth-token` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/openapiauthtoken/OpenApiAuthTokenController.kt#L53) | `OpenApiAuthTokenSearchRequest` `searchType`, `searchValue`, `page`, `pageSize` → `success`, `data`, `error`, `content`, `totalElements`, `page`, `pageSize`, `totalPages` | `SB_DTI_LOG.dbo.OAPI_GET_TOKEN_HISTORY`, `sb_dti_log.dbo.oapi_get_token_history_old` · 코드 연계 트랜잭션 |
| OpenAPI 인증토큰 복호화 | `POST /api/v1/hub/auth-tokens/decrypt` · `/hub-service/openapi-auth-token` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/openapiauthtoken/OpenApiAuthTokenController.kt#L66) | `OpenApiAuthTokenDecryptRequest` `encryptedToken` · 서버 필수 `encryptedToken` → `success`, `data`, `error`, `businessNumber`, `smartBillId`, `expirationDate` | 직접 DB 호출이 연결된 경로는 현재 소스에서 미확인. 세부 저장소는 Controller와 Service 참조. |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `SB_DTI_LOG.dbo.OAPI_GET_TOKEN_HISTORY` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/openapiauthtoken/repository/OpenApiAuthTokenMapper.kt#L74) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-33ae15293c464778) |
| `sb_dti_log.dbo.oapi_get_token_history_old` | 메타데이터 확인 필요 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/openapiauthtoken/repository/OpenApiAuthTokenMapper.kt#L74) · 개발 정의 미확인 |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 발급일자, 사업자번호, 스마트빌 아이디, 만료일자, 인증토큰, 검색 조건 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 연동 서비스 관리 > 연동 서비스 관리 > OpenAPI 인증토큰 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 검색 결과가 없습니다. | 발급일자, 사업자번호, 스마트빌 아이디, 만료일자, 인증토큰, 검색 조건 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/IntegrationRoutes.tsx#L136) · [OpenApiAuthTokenPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/OpenApiAuthTokenPage.tsx#L115) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/api/openApiAuthTokenApi.ts#L26) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/api/openApiAuthTokenApi.ts#L35) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 2개 중 개발 메타데이터 확인 1개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-88eb7ebcca689ce7) | Demo 메타데이터 2/2개 확인 · Dev와 계약 차이 1개 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

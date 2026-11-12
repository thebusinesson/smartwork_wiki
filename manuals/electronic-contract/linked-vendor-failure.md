# [계약 연동 업체·인증서와 장애] 연동업체 장애관리 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

허브업체 ID 또는 허브업체명으로 전자계약 연동업체 장애 현황 목록을 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 계약 연동 업체·인증서와 장애 |
| 언제 사용하는가 | 전자계약 연동업체 장애 목록 조회, 전자계약 허브업체 드롭다운 조회 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 전체, 허브업체명, 시스템 분류, 서버정보, 포트, 소속 사업자수 |
| 업무 흐름 | 전자계약 연동업체 장애 목록 조회, 전자계약 허브업체 드롭다운 조회 |
| 이 페이지의 역할 | 조회 · 전자계약 연동업체 장애 목록 조회 |
| 판단 결과·다음 업무 | [연동업체 장애관리 상세](linked-vendor-failure__detail.md) |
| 다른 화면과의 구분 | 이 경로에서 볼 수 있는 조건·결과를 기준으로 사용한다. 독립 경로의 상세·등록은 관련 화면에 연결한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 허브업체 ID 또는 허브업체명으로 전자계약 연동업체 장애 현황 목록을 조회한다. |
| 메뉴·화면 경로 | SB 서비스관리 > 전자계약 > 연동업체 장애관리 · `/electronic-contract/linked-vendor-failure` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [연동업체 장애관리 상세](linked-vendor-failure__detail.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/electronic-contract/linked-vendor-failure` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 전자계약 연동업체 장애 목록 조회 | `/electronic-contract/linked-vendor-failure` `VIEW` | `LinkedVendorFailureSearchRequest` `hubId`, `hubCompanyName` |
| 전자계약 허브업체 드롭다운 조회 | `/electronic-contract/linked-vendor-failure` `VIEW` | 추가 입력은 Controller 서명 참조 |

코드에서 확인한 버튼·작업명은 **검색**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **SB 서비스관리 > 전자계약 > 연동업체 장애관리**를 연다. `/electronic-contract/linked-vendor-failure`를 연다.
2. **전체** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색** 중 해당 버튼을 선택한다.
3. **전자계약 연동업체 장애 목록 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [연동업체 장애관리 상세](linked-vendor-failure__detail.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 전체 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/LinkedVendorFailureManagement.tsx#L74) |
| 허브업체명 | 입력 또는 선택 | 길이·개수 최대 100 · API 기본값 null | API 요청 `hubCompanyName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/LinkedVendorFailureManagement.tsx#L86) |
| 시스템 분류 | 출력 | 조회 응답 기준 | 화면 필드 `systemType` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/LinkedVendorFailureManagement.tsx#L87) |
| 서버정보 | 출력 | 조회 응답 기준 | 화면 필드 `routingUrl` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/LinkedVendorFailureManagement.tsx#L88) |
| 포트 | 출력 | 조회 응답 기준 | 화면 필드 `port` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/LinkedVendorFailureManagement.tsx#L91) |
| 소속 사업자수 | 출력 | 조회 응답 기준 | 화면 필드 `partnerCount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/LinkedVendorFailureManagement.tsx#L98) |
| 장애여부 | 출력 | 조회 응답 기준 | 화면 필드 `hasError` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/LinkedVendorFailureManagement.tsx#L105) |
| 설정일시 | 출력 | 조회 응답 기준 | 화면 필드 `createdAt` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/LinkedVendorFailureManagement.tsx#L112) |
| 작업자 | 출력 | 조회 응답 기준 | 화면 필드 `operatorName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/LinkedVendorFailureManagement.tsx#L119) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 전자계약 연동업체 장애 목록 조회 | `GET /api/v1/electronic-contract/linked-vendor-failures` · `/electronic-contract/linked-vendor-failure` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/electroniccontract/linkedvendorfailure/LinkedVendorFailureController.kt#L64) | `LinkedVendorFailureSearchRequest` `hubId`, `hubCompanyName` → `success`, `data`, `error`, `content`, `totalElements` | `office.dbo.upGw_Dct_HubError_Reg_NEW` · 코드 연계 트랜잭션 |
| 전자계약 허브업체 드롭다운 조회 | `GET /api/v1/electronic-contract/linked-vendor-failures/hub-companies` · `/electronic-contract/linked-vendor-failure` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/electroniccontract/linkedvendorfailure/LinkedVendorFailureController.kt#L80) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `hubId`, `siteName` | 직접 DB 호출이 연결된 경로는 현재 소스에서 미확인. 세부 저장소는 Controller와 Service 참조. |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `office.dbo.upGw_Dct_HubError_Reg_NEW` | @HUB_ID int | 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/linkedvendorfailure/repository/LinkedVendorFailureMapper.kt#L49) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-78c304d2086f88bf) |

### 매퍼 호출 추가 확인

| DB 객체 | 호출 근거 | 개발 DB 확인 범위 |
| --- | --- | --- |
| [office.dbo.upHub_HubList03](../../references/all-pages-demo.md#object-aa139319d7785fa2) | [findHubCompanies](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/linkedvendorfailure/repository/LinkedVendorFailureMapper.kt#L59) | 개발 카탈로그 확인 |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 전체, 허브업체명, 시스템 분류, 서버정보, 포트, 소속 사업자수 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 서비스관리 > 전자계약 > 연동업체 장애관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 검색 결과가 없습니다. | 전체, 허브업체명, 시스템 분류, 서버정보, 포트, 소속 사업자수 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/ElectronicContractRoutes.tsx#L40) · [LinkedVendorFailureManagement.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/LinkedVendorFailureManagement.tsx#L31) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/api/linkedVendorFailureManagementApi.ts#L30) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/api/linkedVendorFailureManagementApi.ts#L40) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 1개 중 개발 메타데이터 확인 1개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-a3792d57f4872d9c) | Demo 메타데이터 2/2개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

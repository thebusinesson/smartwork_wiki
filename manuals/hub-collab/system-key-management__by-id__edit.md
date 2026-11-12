# [시스템 키·벌크계좌·업체 연결 설정] System Key 관리 수정 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

System Key 관리 수정에서 대상과 입력값을 확인해 **System Key 수정** 업무를 처리한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 시스템 키·벌크계좌·업체 연결 설정 |
| 언제 사용하는가 | System Key 상세 조회, System Key 중복 확인, 허브업체 검색 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | System Key 명, 허브업체명 |
| 업무 흐름 | System Key 상세 조회, System Key 중복 확인, 허브업체 검색, System Key 수정 |
| 이 페이지의 역할 | 수정 · System Key 수정 |
| 판단 결과·다음 업무 | [System Key 관리](system-key-management.md) · [System Key 관리 상세](system-key-management__by-id.md) |
| 다른 화면과의 구분 | 연동 협업 관리 > 연동 협업 관리 > System Key 관리에서 사용하는 수정 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 확인 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/systemKey/pages/SystemKeyEditPage.tsx#L180) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | System Key 관리 수정에서 대상과 입력값을 확인해 **System Key 수정** 업무를 처리한다. |
| 메뉴·화면 경로 | 연동 협업 관리 > 연동 협업 관리 > System Key 관리 · `/hub-collab/system-key-management/:id/edit` · 경로 변수 `id` |
| 화면 유형·담당 | 수정 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [System Key 관리](system-key-management.md) · [System Key 관리 상세](system-key-management__by-id.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/hub-collab/system-key-management` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `id` |
| System Key 상세 조회 | `/hub-collab/system-key-management` `VIEW` | `id: Int` |
| System Key 중복 확인 | `/hub-collab/system-key-management` `VIEW` | `systemKey: String` · `excludeId: Int?` |
| 허브업체 검색 | `/hub-collab/system-key-management` `VIEW` | `keyword: String?` |
| System Key 수정 | `/hub-collab/system-key-management` `PROCESS` | `id: Int` · `UpdateSystemKeyRequest` `systemKey`, `vendorIds` · 서버 필수 `systemKey` |

코드에서 확인한 버튼·작업명은 **중복확인**, **검색**, **등록업체 추가**, **등록업체 삭제**, **저장**, **System Key 저장**, **취소**, **System Key 등록/수정 취소**, **확인**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [System Key 관리](system-key-management.md)에서 대상 또는 작업을 선택한다. `/hub-collab/system-key-management/:id/edit`에서 이전 화면이 전달한 `id`와 현재 대상을 확인한다.
2. **System Key 명**, **허브업체명** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **중복확인**, **검색**, **등록업체 추가**, **등록업체 삭제**, **저장** 중 해당 버튼을 선택한다.
3. **System Key 수정**을 실행하기 전에 변경 대상과 입력값을 확인한다. 처리 응답을 확인하고 관련 조회에서 대상의 상태를 확인한다.
4. 후속 조회나 목록 복귀가 필요하면 [System Key 관리 상세](system-key-management__by-id.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `id` |
| System Key 명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/systemKey/pages/SystemKeyEditPage.tsx#L115) |
| 허브업체명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/systemKey/components/VendorSearchPanel.tsx#L122) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| System Key 상세 조회 | `GET /api/v1/system-keys/{id}` · `/hub-collab/system-key-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/systemkey/SystemKeyController.kt#L77) | `id: Int` → `success`, `data`, `error`, `id`, `systemKey`, `vendorCount`, `status`, `createdAt`, `updatedAt`, `registeredVendors` | `office.dbo.MNG_SYSTEM`, `office.dbo.MNG_HUB`, `office.dbo.BUSINESS` |
| System Key 중복 확인 | `GET /api/v1/system-keys/check-duplicate` · `/hub-collab/system-key-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/systemkey/SystemKeyController.kt#L101) | `systemKey: String` · `excludeId: Int?` → `success`, `data`, `error`, `isDuplicate` | `office.dbo.MNG_SYSTEM` |
| 허브업체 검색 | `GET /api/v1/system-keys/vendors/search` · `/hub-collab/system-key-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/systemkey/SystemKeyController.kt#L176) | `keyword: String?` → `success`, `data`, `error`, `content`, `totalElements` | `office.dbo.BUSINESS`, `office.dbo.MNG_HUB` |
| System Key 수정 | `PUT /api/v1/system-keys/{id}` · `/hub-collab/system-key-management` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/systemkey/SystemKeyController.kt#L134) | `id: Int` · `UpdateSystemKeyRequest` `systemKey`, `vendorIds` · 서버 필수 `systemKey` → `success`, `data`, `error`, `message`, `id` | `office.dbo.MNG_SYSTEM`, `office.dbo.MNG_HUB`, `office.dbo.BUSINESS` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `office.dbo.MNG_SYSTEM` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/systemkey/repository/SystemKeyMapper.kt#L67) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-41fa24c29bca86c9) |
| `office.dbo.MNG_HUB` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/systemkey/repository/SystemKeyMapper.kt#L86) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-bb97dfe4e2b8c3b3) |
| `office.dbo.BUSINESS` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/systemkey/repository/SystemKeyMapper.kt#L86) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-1c6a832844bf01aa) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | System Key 명, 허브업체명 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 연동 협업 관리 > 연동 협업 관리 > System Key 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 수정이 취소되었습니다. | System Key 명, 허브업체명 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/IntegrationRoutes.tsx#L90) · [SystemKeyEditPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/systemKey/pages/SystemKeyEditPage.tsx#L35) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/systemKeyManagementApi.ts#L35) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/systemKeyManagementApi.ts#L46) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/systemKeyManagementApi.ts#L79) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/systemKeyManagementApi.ts#L53) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/systemKeyManagementApi.ts#L60) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/systemKeyManagementApi.ts#L67) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 4개 중 개발 메타데이터 확인 4개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-34ae3ab0ed889f02) | Demo 메타데이터 3/3개 확인 · Dev와 계약 차이 2개 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

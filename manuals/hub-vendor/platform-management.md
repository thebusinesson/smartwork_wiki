# [시스템 키·벌크계좌·업체 연결 설정] 연동플랫폼 통합관리 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

페이징 + 검색 (System Key / IP / 사업자번호) + 영업상품 분기 키 (etax/contract/bond-balance).

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 시스템 키·벌크계좌·업체 연결 설정 |
| 언제 사용하는가 | 연동 플랫폼 통합 관리 목록 조회 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 검색조건, 사업자번호 |
| 업무 흐름 | 연동 플랫폼 통합 관리 목록 조회 |
| 이 페이지의 역할 | 조회 · 연동 플랫폼 통합 관리 목록 조회 |
| 판단 결과·다음 업무 | [연동플랫폼 통합관리 상세](platform-management__by-platformId.md) · [연동플랫폼 통합관리 상세](platform-management__system-port__by-portId.md) |
| 다른 화면과의 구분 | 이 경로에서 볼 수 있는 조건·결과를 기준으로 사용한다. 독립 경로의 상세·등록은 관련 화면에 연결한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 페이징 + 검색 (System Key / IP / 사업자번호) + 영업상품 분기 키 (etax/contract/bond-balance). |
| 메뉴·화면 경로 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > 연동플랫폼 통합관리 · `/hub-vendor/platform-management` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [연동플랫폼 통합관리 상세](platform-management__by-platformId.md) · [연동플랫폼 통합관리 상세](platform-management__system-port__by-portId.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/hub-vendor/platform-management` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 연동 플랫폼 통합 관리 목록 조회 | `/hub-vendor/platform-management` `VIEW` | `PlatformMgmtSearchRequest` `page`, `size`, `searchMode`, `searchValue`, `productCode` |

코드에서 확인한 버튼·작업명은 **검색**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **연동/허브 업체 관리 > 연동/허브 업체 관리 > 연동플랫폼 통합관리**를 연다. `/hub-vendor/platform-management`를 연다.
2. **검색조건**, **사업자번호** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색** 중 해당 버튼을 선택한다.
3. **연동 플랫폼 통합 관리 목록 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [연동플랫폼 통합관리 상세](platform-management__by-platformId.md)에서 후속 절차를 확인한다.

라우팅을 IP 또는 사업자번호로 검색할 때 **영업상품**을 **전체**로 두면 상품별 제한 없이 조회한다. IP와 사업자번호 모드를 바꾸면 기존 검색어와 상품 조건이 초기화된다. [검색 옵션](https://github.com/thebusinesson/smartwork/blob/b923849c5d878772e0de2b67becff0ae511f03b3/frontend/src/feature/integration/hubvendor/IntegrationPlatformPage.tsx)

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 검색조건 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/IntegrationPlatformPage.tsx#L154) |
| System Key 입력 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/IntegrationPlatformPage.tsx#L167) |
| 사업자번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `businessNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/IntegrationPlatformPage.tsx#L182) |
| 영업상품 선택 | 입력 또는 선택 | 서버 형식 검사 · API 기본값 null | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/IntegrationPlatformPage.tsx#L194) |
| IP 입력 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/IntegrationPlatformPage.tsx#L203) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 연동 플랫폼 통합 관리 목록 조회 | `GET /api/v1/hub-vendor/platform-management` · `/hub-vendor/platform-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/platformmgmt/PlatformMgmtController.kt#L76) | `PlatformMgmtSearchRequest` `page`, `size`, `searchMode`, `searchValue`, `productCode` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `currentPage`, `size` | `smartwork.dbo.usp_platform_mgmt_list_select` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.usp_platform_mgmt_list_select` | @PAGE int, @PAGE_SIZE int, @SEARCH_MODE char(1) = NULL, @SEARCH_VALUE varchar(100) = NULL, @SERVICE_KIND varchar(10) = NULL | 정의 참조 `office.dbo.BUSINESS`, `SmartBill3.dbo.COMPANY`, `SB_DTI.dbo.COMPANY_LINK_OUT`, `SmartBill3.dbo.DCT_COMPANY_LINK_OUT`, `SB_DRC.dbo.DRC_COMPANY_LINK` 외 6개 · 쓰기 구문 존재 · 대상 별칭 또는 하위 정의 확인 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/platformmgmt/repository/PlatformMgmtMapper.kt#L52) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-d26be6b0fa46b7a5) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 검색조건, 사업자번호 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > 연동플랫폼 통합관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/IntegrationRoutes.tsx#L112) · [IntegrationPlatformPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/IntegrationPlatformPage.tsx#L34) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/api/integrationPlatformApi.ts#L278) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 1개 중 개발 메타데이터 확인 1개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-775979b3b448ef40) | 2026-11-11 기준으로 Demo 메타데이터 1/1개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |
| 최신 변경 대조 | [11월 12일 전수 대조](../../references/all-pages-audit-2026-11-12.md) | 현재 코드 b923849c5 · 2026-11-12 |

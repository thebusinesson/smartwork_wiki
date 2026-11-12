# [이용료 청구·일일 정산·영수 발행] 클로버 관리 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

클로버 충전/사용 현황을 업체별로 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 이용료 청구·일일 정산·영수 발행 |
| 언제 사용하는가 | 클로버 업체 목록 조회 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 업체 조건, 회사명, 사업자번호, 충전, 사용, 기간만료 |
| 업무 흐름 | 클로버 업체 목록 조회 |
| 이 페이지의 역할 | 조회 · 클로버 업체 목록 조회 |
| 판단 결과·다음 업무 | [클로버 관리 조회](clover-charge__input.md) · [클로버 관리 상세](clover-charge__by-businessNumber.md) |
| 다른 화면과의 구분 | 이 경로에서 볼 수 있는 조건·결과를 기준으로 사용한다. 독립 경로의 상세·등록은 관련 화면에 연결한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 클로버 충전/사용 현황을 업체별로 조회한다. |
| 메뉴·화면 경로 | 서비스 현황 > 요금관리 > 클로버 관리 · `/billing-management/clover-charge` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [클로버 관리 조회](clover-charge__input.md) · [클로버 관리 상세](clover-charge__by-businessNumber.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/billing-management/clover-charge` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 클로버 업체 목록 조회 | `/billing-management/clover-charge` `VIEW` | `searchTarget: String?` · `searchValue: String?` |

코드에서 확인한 버튼·작업명은 **검색**, **클로버 충전**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **서비스 현황 > 요금관리 > 클로버 관리**를 연다. `/billing-management/clover-charge`를 연다.
2. **업체 조건**, **회사명**, **사업자번호** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색** 중 해당 버튼을 선택한다.
3. **클로버 업체 목록 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [클로버 관리 조회](clover-charge__input.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 업체 조건 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/CloverChargePage.tsx#L37) |
| 회사명 | 출력 | 조회 응답 기준 | API 응답 `companyName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/CloverChargePage.tsx#L21) |
| 사업자번호 | 출력 | 조회 응답 기준 | API 응답 `businessNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/CloverChargePage.tsx#L22) |
| 충전 | 출력 | 조회 응답 기준 | API 응답 `charged` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/CloverChargePage.tsx#L23) |
| 사용 | 출력 | 조회 응답 기준 | API 응답 `used` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/CloverChargePage.tsx#L24) |
| 기간만료 | 출력 | 조회 응답 기준 | API 응답 `expired` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/CloverChargePage.tsx#L25) |
| 잔여 | 출력 | 조회 응답 기준 | API 응답 `remain` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/CloverChargePage.tsx#L26) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 클로버 업체 목록 조회 | `GET /api/v1/service-status/clover/companies` · `/billing-management/clover-charge` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/billing/clover/CloverController.kt#L43) | `searchTarget: String?` · `searchValue: String?` → `success`, `data`, `error`, `companyName`, `businessNumber`, `charged`, `used`, `expired`, `remain` | `SB_BILL.dbo.UspBill_FreeServiceList_SELECT_TOP` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `SB_BILL.dbo.UspBill_FreeServiceList_SELECT_TOP` | @PAGE int, @TOP int, @SEARCH_CODE varchar(2), @SEARCH_TEXT varchar(50), @DIV varchar(1) | 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/billing/clover/repository/CloverMapper.kt#L38) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-1ea6c1ec040b8983) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 업체 조건, 회사명, 사업자번호, 충전, 사용, 기간만료 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 서비스 현황 > 요금관리 > 클로버 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/BillingManagementRoutes.tsx#L19) · [CloverChargePage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/CloverChargePage.tsx#L56) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/api/cloverManagementApi.ts#L28) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 1개 중 개발 메타데이터 확인 1개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-7690fdbdb49e4b3f) | Demo 메타데이터 1/1개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

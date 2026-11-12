# [이용료 청구·일일 정산·영수 발행] 클로버 관리 조회 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

업체의 클로버 요약 정보와 충전 이력을 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 이용료 청구·일일 정산·영수 발행 |
| 언제 사용하는가 | 클로버 업체 상세 조회, 클로버 충전 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 사업자 번호, 업체 정보, 클로버 충전 |
| 업무 흐름 | 클로버 업체 상세 조회, 클로버 충전 |
| 이 페이지의 역할 | 조회 · 클로버 업체 상세 조회 |
| 판단 결과·다음 업무 | [클로버 관리](clover-charge.md) · [클로버 관리 상세](clover-charge__by-businessNumber.md) |
| 다른 화면과의 구분 | 서비스 현황 > 요금관리 > 클로버 관리에서 사용하는 조회 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 회사명 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/CloverListPage.tsx#L259) |
| 사업자번호 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/CloverListPage.tsx#L260) |
| 충전 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/CloverListPage.tsx#L261) |
| 사용 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/CloverListPage.tsx#L262) |
| 기간만료 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/CloverListPage.tsx#L263) |
| 잔여 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/CloverListPage.tsx#L264) |
| 확인 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/CloverListPage.tsx#L398) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 업체의 클로버 요약 정보와 충전 이력을 조회한다. |
| 메뉴·화면 경로 | 서비스 현황 > 요금관리 > 클로버 관리 · `/billing-management/clover-charge/input` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [클로버 관리](clover-charge.md) · [클로버 관리 상세](clover-charge__by-businessNumber.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/billing-management/clover-charge` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 클로버 업체 상세 조회 | `/billing-management/clover-charge` `VIEW` | `businessNumber: String` |
| 클로버 충전 | `/billing-management/clover-charge` `PROCESS` | `CloverChargeRequest` `businessNumber`, `cloverAmount`, `startDate`, `endDate`, `note` |

코드에서 확인한 버튼·작업명은 **검색**, **취소**, **충전**, **확인**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [클로버 관리](clover-charge.md)에서 대상 또는 작업을 선택한다. `/billing-management/clover-charge/input`를 연다.
2. **사업자 번호**, **업체 정보**, **클로버 충전** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색**, **확인** 중 해당 버튼을 선택한다.
3. **클로버 업체 상세 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [클로버 관리 상세](clover-charge__by-businessNumber.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 사업자 번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/CloverListPage.tsx#L38) |
| 업체 정보 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/CloverListPage.tsx#L254) |
| 클로버 충전 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/CloverListPage.tsx#L289) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 클로버 업체 상세 조회 | `GET /api/v1/service-status/clover/{businessNumber}` · `/billing-management/clover-charge` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/billing/clover/CloverController.kt#L59) | `businessNumber: String` → `success`, `data`, `error`, `cloverStatus`, `transactions` | `smartwork.dbo.UspBill_FreeServiceSummary_SELECT`, `smartwork.dbo.UspBill_FreeServiceChargeHistory_SELECT` |
| 클로버 충전 | `POST /api/v1/service-status/clover/charge` · `/billing-management/clover-charge` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/billing/clover/CloverController.kt#L70) | `CloverChargeRequest` `businessNumber`, `cloverAmount`, `startDate`, `endDate`, `note` → `success`, `data`, `error` | `smartwork.dbo.UspBill_FreeServiceSummary_SELECT`, `SB_BILL.dbo.UspBill_EventSingleInfo_INSERT` · 정의에서 확인한 쓰기 `SB_COMMON.dbo.FREE_SERVICE`, `SB_COMMON.dbo.FREE_SERVICE_HIS` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.UspBill_FreeServiceSummary_SELECT` | @COM_REGNO varchar(20) | 정의 참조 `SmartBill3.dbo.COMPANY`, `SB_COMMON.dbo.FREE_SERVICE` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/billing/clover/repository/CloverMapper.kt#L51) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-1c51e563555990f5) |
| `smartwork.dbo.UspBill_FreeServiceChargeHistory_SELECT` | @COM_REGNO varchar(20) | 정의 참조 `SmartBill3.dbo.COMPANY`, `SB_COMMON.dbo.FREE_SERVICE`, `office.dbo.SAWON` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/billing/clover/repository/CloverMapper.kt#L66) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-6d9242479c3b98f6) |
| `SB_BILL.dbo.UspBill_EventSingleInfo_INSERT` | @COM_NO int, @CHARGE_CNT int, @FROM_DATE varchar(10), @TO_DATE varchar(10), @REMARK varchar(300), @SW_NO int, @RESULT varchar(1) OUT | 정의 참조 `SB_COMMON.dbo.FREE_SERVICE`, `SB_COMMON.dbo.FREE_SERVICE_HIS` · 정적 쓰기 `SB_COMMON.dbo.FREE_SERVICE`, `SB_COMMON.dbo.FREE_SERVICE_HIS` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/billing/clover/repository/CloverMapper.kt#L75) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-539441051ea11dae) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 사업자 번호, 업체 정보, 클로버 충전 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 서비스 현황 > 요금관리 > 클로버 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 업체 정보를 조회하는 중 오류가 발생했습니다. | 사업자 번호, 업체 정보, 클로버 충전 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 클로버 충전이 취소되었습니다. | 사업자 번호, 업체 정보, 클로버 충전 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 먼저 업체를 조회해 주세요. | 사업자 번호, 업체 정보, 클로버 충전 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 클로버 충전 중 오류가 발생했습니다. | 사업자 번호, 업체 정보, 클로버 충전 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/BillingManagementRoutes.tsx#L20) · [CloverListPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/CloverListPage.tsx#L54) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/api/cloverManagementApi.ts#L32) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/billing/api/cloverManagementApi.ts#L38) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 3개 중 개발 메타데이터 확인 3개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-65b0e6d0ed9bd0cb) | Demo 메타데이터 3/3개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

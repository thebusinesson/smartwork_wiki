# [고객·매출·연동과 외부 호출 지표] 월별 고객·매출 통합 현황 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

서버 보관 마스터 엑셀의 요청 월 시트(`(YY.M월)`)에 DTI/DCT 연동·웹 고객수/발행량 및 스마트빌 홈페이지·스마트워크 지표를 누적·갱신한 뒤 xlsx 로 다운로드한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 고객·매출·연동과 외부 호출 지표 |
| 언제 사용하는가 | 월별 고객·매출 통합 현황 다운로드, 다운로드 사유 등록 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 대상 월 |
| 업무 흐름 | 월별 고객·매출 통합 현황 다운로드, 다운로드 사유 등록 |
| 이 페이지의 역할 | 조회 · 월별 고객·매출 통합 현황 다운로드 |
| 판단 결과·다음 업무 | 현재 화면에서 결과를 확인한다. |
| 다른 화면과의 구분 | 같은 경로에서 열리는 조회·팝업은 이 문서에서 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 서버 보관 마스터 엑셀의 요청 월 시트(`(YY.M월)`)에 DTI/DCT 연동·웹 고객수/발행량 및 스마트빌 홈페이지·스마트워크 지표를 누적·갱신한 뒤 xlsx 로 다운로드한다. |
| 메뉴·화면 경로 | 서비스 현황 > 통계 정보 > 월별 고객·매출 통합 현황 · `/statistics/monthly-customer-sales` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | 현재 화면에서 결과를 확인한다. |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/statistics/monthly-customer-sales` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 월별 고객·매출 통합 현황 다운로드 | `/statistics/monthly-customer-sales` `EXCEL_DOWNLOAD` | `MonthlyCustomerSalesDownloadRequest` `yearMonth` · 서버 필수 `yearMonth` |
| 다운로드 사유 등록 | 정적 메뉴 액션 미확인 · Controller·공통 보안 검사 확인 | `request: DownloadReasonRequest` |

코드에서 확인한 버튼·작업명은 **대상 월**, **다운로드**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **서비스 현황 > 통계 정보 > 월별 고객·매출 통합 현황**를 연다. `/statistics/monthly-customer-sales`를 연다.
2. **대상 월** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **다운로드** 중 해당 버튼을 선택한다.
3. **월별 고객·매출 통합 현황 다운로드** 처리 결과를 확인하고 받은 파일의 대상과 적용 조건을 대조한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 대상 월 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/MonthlyCustomerSalesDownloadPage.tsx#L76) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 월별 고객·매출 통합 현황 다운로드 | `GET /api/v1/service-status/statistics/monthly-customer-sales/download` · `/statistics/monthly-customer-sales` `EXCEL_DOWNLOAD` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/statistics/monthlycustomersales/MonthlyCustomerSalesController.kt#L49) | `MonthlyCustomerSalesDownloadRequest` `yearMonth` · 서버 필수 `yearMonth` → 파일 또는 오류 응답 | `smartwork.dbo.sp_GetMonthlyCustomerSales` · 코드 연계 트랜잭션 |
| 다운로드 사유 등록 | `POST /api/v1/download-reason` · 정적 메뉴 액션 미확인 · Controller·공통 보안 검사 확인 · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/shared/downloadreason/DownloadReasonController.kt#L32) · [기존 상세 계약](../../references/api-contracts.md#api210) | `request: DownloadReasonRequest` → `success`, `data`, `error` | `smartwork.dbo.action_reason` · 정의에서 확인한 쓰기 `smartwork.dbo.action_reason` |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.sp_GetMonthlyCustomerSales` | @YearMonth char(6) | 정의 참조 `SmartBill3_DW_260715.dbo.COMPANY`, `SmartBill3_DW_260715.dbo.MEMBER`, `SmartBill3_DW_260715.dbo.MNG_MONTHLY_SUM`, `SmartBill3_DW_260715.dbo.SERVICE_PREPAY_HIS` · 쓰기 구문 존재 · 대상 별칭 또는 하위 정의 확인 · 동적 SQL 포함 · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/statistics/monthlycustomersales/repository/MonthlyCustomerSalesMapper.kt#L51) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b91ca9316c0f1ec3) |
| `smartwork.dbo.action_reason` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL INSERT INTO | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/shared/actionreason/repository/ActionReasonMapper.kt#L16) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b0430106ffe0743f) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 대상 월 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 서비스 현황 > 통계 정보 > 월별 고객·매출 통합 현황의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/StatisticsRoutes.tsx#L41) · [MonthlyCustomerSalesDownloadPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/MonthlyCustomerSalesDownloadPage.tsx#L24) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/api/monthlyCustomerSalesApi.ts#L21) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/api/downloadReasonApi.ts#L15) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 2개 중 개발 메타데이터 확인 2개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-8db00fc341344932) | Demo 메타데이터 2/2개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

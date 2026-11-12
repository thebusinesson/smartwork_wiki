# [고객·매출·연동과 외부 호출 지표] 서비스별 매출액 조회 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

월별 또는 연별 서비스별 매출액을 조회한다. 레거시 OFFICE SP를 재사용한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 고객·매출·연동과 외부 호출 지표 |
| 언제 사용하는가 | 서비스별 매출액 조회 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 통계 구분, 월별, 연별, 통계 기간, 표준형, 건별형 |
| 업무 흐름 | 서비스별 매출액 조회 |
| 이 페이지의 역할 | 조회 · 서비스별 매출액 조회 |
| 판단 결과·다음 업무 | 현재 화면에서 결과를 확인한다. |
| 다른 화면과의 구분 | 같은 경로에서 열리는 조회·팝업은 이 문서에서 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 월별 또는 연별 서비스별 매출액을 조회한다. 레거시 OFFICE SP를 재사용한다. |
| 메뉴·화면 경로 | 서비스 현황 > 통계 정보 > 서비스별 매출액 조회 · `/statistics/service-sales` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | 현재 화면에서 결과를 확인한다. |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/statistics/service-sales` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 서비스별 매출액 조회 | `/statistics/service-sales` `VIEW` | `ServiceSalesSearchRequest` `statisticsType`, `periodStart`, `periodEnd` · 서버 필수 `statisticsType`, `periodStart`, `periodEnd` |

코드에서 확인한 버튼·작업명은 **검색**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **서비스 현황 > 통계 정보 > 서비스별 매출액 조회**를 연다. `/statistics/service-sales`를 연다.
2. **통계 구분**, **월별**, **연별**, **통계 기간** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색** 중 해당 버튼을 선택한다.
3. **서비스별 매출액 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 통계 구분 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/ServiceSalesPage.tsx#L66) |
| 월별 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `monthly` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/ServiceSalesPage.tsx#L72) |
| 연별 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `yearly` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/ServiceSalesPage.tsx#L73) |
| 통계 기간 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/ServiceSalesPage.tsx#L79) |
| 표준형 | 출력 | 조회 응답 기준 | 화면 필드 `taxInvoice.standardType` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/ServiceSalesTable.tsx#L187) |
| 건별형 | 출력 | 조회 응답 기준 | 화면 필드 `taxInvoice.caseByCaseType` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/ServiceSalesTable.tsx#L193) |
| 합계 | 출력 | 조회 응답 기준 | 화면 필드 `taxInvoice.total` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/ServiceSalesTable.tsx#L199) |
| 전자계약 | 출력 | 조회 응답 기준 | 화면 필드 `electronicContract` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/ServiceSalesTable.tsx#L70) |
| 기타 | 출력 | 조회 응답 기준 | 화면 필드 `other` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/ServiceSalesTable.tsx#L108) |
| 총매출액 | 출력 | 조회 응답 기준 | 화면 필드 `totalSalesAmount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/ServiceSalesTable.tsx#L117) |
| 세금계산서 | 출력 | 조회 응답 기준 | 화면 필드 `taxInvoice-group` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/ServiceSalesTable.tsx#L142) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 서비스별 매출액 조회 | `GET /api/v1/service-status/statistics/service-sales` · `/statistics/service-sales` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/statistics/servicesales/ServiceSalesController.kt#L39) | `ServiceSalesSearchRequest` `statisticsType`, `periodStart`, `periodEnd` · 서버 필수 `statisticsType`, `periodStart`, `periodEnd` → `success`, `data`, `error`, `content`, `totalElements`, `statisticsType` | `office.dbo.upAdmSB_TotalSalesSumInvAmt`, `office.dbo.upAdmSB_prepaySumInvAmt` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `office.dbo.upAdmSB_TotalSalesSumInvAmt` | @str_Div char(2), @s_yymm char(6), @e_yymm char(6) | 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/statistics/servicesales/repository/ServiceSalesMapper.kt#L34) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-bb4b7901d9f97943) |
| `office.dbo.upAdmSB_prepaySumInvAmt` | @start_date varchar(10), @end_date varchar(10) | 정의 참조 `SmartBill3.dbo.SERVICE_PREPAY` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/statistics/servicesales/repository/ServiceSalesMapper.kt#L42) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-8af22ebc5b84fcab) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 통계 구분, 월별, 연별, 통계 기간, 표준형, 건별형 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 서비스 현황 > 통계 정보 > 서비스별 매출액 조회의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 데이터를 불러오는 중 오류가 발생했습니다. | 통계 구분, 월별, 연별, 통계 기간, 표준형, 건별형 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/StatisticsRoutes.tsx#L47) · [ServiceSalesPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/ServiceSalesPage.tsx#L34) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/api/serviceSalesApi.ts#L28) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 2개 중 개발 메타데이터 확인 2개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-a692a5f1d70a3dfe) | Demo 메타데이터 2/2개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

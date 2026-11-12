# [고객·매출·연동과 외부 호출 지표] 허브업체 이용 현황 상세 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

허브 ID 기준으로 사업자별 세금계산서 또는 전자계약 이용 현황을 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 고객·매출·연동과 외부 호출 지표 |
| 언제 사용하는가 | 허브업체 이용 현황 상세 조회 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 허브업체명, 사업자수, 발행 월, 영업대표, 사업자번호, 회사명 |
| 업무 흐름 | 허브업체 이용 현황 상세 조회 |
| 이 페이지의 역할 | 상세 · 허브업체 이용 현황 상세 조회 |
| 판단 결과·다음 업무 | [허브업체 이용 현황](hub-company-usage.md) |
| 다른 화면과의 구분 | 서비스 현황 > 통계 정보 > 허브업체 이용 현황에서 사용하는 상세 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 허브 ID 기준으로 사업자별 세금계산서 또는 전자계약 이용 현황을 조회한다. |
| 메뉴·화면 경로 | 서비스 현황 > 통계 정보 > 허브업체 이용 현황 · `/statistics/hub-company-usage/:id` · 경로 변수 `id` |
| 화면 유형·담당 | 상세 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [허브업체 이용 현황](hub-company-usage.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/statistics/hub-company-usage` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `id` |
| 허브업체 이용 현황 상세 조회 | `/statistics/hub-company-usage` `VIEW` | `HubCompanyUsageDetailRequest` `hubId`, `serviceType`, `usageMonthAll`, `usageMonthStart`, `usageMonthEnd` |

코드에서 확인한 버튼·작업명은 **목록**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [허브업체 이용 현황](hub-company-usage.md)에서 대상 또는 작업을 선택한다. `/statistics/hub-company-usage/:id`에서 이전 화면이 전달한 `id`와 현재 대상을 확인한다.
2. **허브업체 이용 현황 상세 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
3. 후속 조회나 목록 복귀가 필요하면 [허브업체 이용 현황](hub-company-usage.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `id` |
| 허브업체명 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/HubCompanyUsageDetailHeader.tsx#L14) |
| 사업자수 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/HubCompanyUsageDetailHeader.tsx#L16) |
| 발행 월 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/HubCompanyUsageDetailHeader.tsx#L20) |
| 영업대표 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/HubCompanyUsageDetailHeader.tsx#L22) |
| 사업자번호 | 출력 | 조회 응답 기준 | 화면 필드 `businessNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/HubCompanyUsageDetailTable.tsx#L116) |
| 회사명 | 출력 | 조회 응답 기준 | 화면 필드 `companyName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/HubCompanyUsageDetailTable.tsx#L124) |
| 기간 | 출력 | 조회 응답 기준 | 화면 필드 `periodMonth` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/HubCompanyUsageDetailTable.tsx#L137) |
| 업체수 | 출력 | 조회 응답 기준 | 화면 필드 `salesCompanyCount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/HubCompanyUsageDetailTable.tsx#L57) |
| 건수 | 출력 | 조회 응답 기준 | 화면 필드 `salesCount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/HubCompanyUsageDetailTable.tsx#L66) |
| 매출 | 출력 | 조회 응답 기준 | 화면 필드 `sales-group` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/HubCompanyUsageDetailTable.tsx#L101) |
| 매입 | 출력 | 조회 응답 기준 | 화면 필드 `purchase-group` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/HubCompanyUsageDetailTable.tsx#L102) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 허브업체 이용 현황 상세 조회 | `GET /api/v1/service-status/usage/hub-companies/detail` · `/statistics/hub-company-usage` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/statistics/hubcompanyusage/HubCompanyUsageController.kt#L89) | `HubCompanyUsageDetailRequest` `hubId`, `serviceType`, `usageMonthAll`, `usageMonthStart`, `usageMonthEnd` → `success`, `data`, `error`, `header`, `content`, `totalElements` | `office.dbo.upHub_ViewHubMainInfo` |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `office.dbo.upHub_ViewHubMainInfo` | @hub_id int | 정의 참조 `office.dbo.BUSINESS`, `office.dbo.MNG_HUB`, `office.dbo.SAWON` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/statistics/hubcompanyusage/repository/HubCompanyUsageMapper.kt#L161) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-883872dfd4472a10) |

### 매퍼 호출 추가 확인

| DB 객체 | 호출 근거 | 개발 DB 확인 범위 |
| --- | --- | --- |
| [office.dbo.upHub_DetailResultsList](../../references/all-pages-demo.md#object-4bd1ea5a99b17c01) | [selectDtiDetail](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/statistics/hubcompanyusage/repository/HubCompanyUsageMapper.kt#L201) | @hub_id int IN · @fromMonth varchar(10) IN · @toMonth varchar(10) IN |
| [office.dbo.upHub_DCTDetailResultsList](../../references/all-pages-demo.md#object-f359a6a91853f896) | [selectDctDetail](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/statistics/hubcompanyusage/repository/HubCompanyUsageMapper.kt#L238) | @hub_id int IN · @fromMonth varchar(10) IN · @toMonth varchar(10) IN |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 허브업체명, 사업자수, 발행 월, 영업대표, 사업자번호, 회사명 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 서비스 현황 > 통계 정보 > 허브업체 이용 현황의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 검색 결과가 없습니다. | 허브업체명, 사업자수, 발행 월, 영업대표, 사업자번호, 회사명 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/StatisticsRoutes.tsx#L34) · [HubCompanyUsageDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/HubCompanyUsageDetailPage.tsx#L16) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/api/hubCompanyUsageDetailApi.ts#L17) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 1개 중 개발 메타데이터 확인 1개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-211aed95874d8465) | Demo 메타데이터 3/3개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

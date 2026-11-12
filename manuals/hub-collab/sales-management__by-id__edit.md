# [연동 영업과 프로젝트 완료] 영업 관리 업체 등록 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

영업 관리 업체 등록에서 대상과 입력값을 확인해 **영업 수정** 업무를 처리한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 연동 영업과 프로젝트 완료 |
| 언제 사용하는가 | 전체 사원 목록 조회 (진행내역 담당자 콤보용), 영업 상세 조회, 영업구분 코드 조회 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 계약기간, 요금제, SSS 비용, 부가서비스비용, 비고, 작성일시 |
| 업무 흐름 | 전체 사원 목록 조회 (진행내역 담당자 콤보용), 영업 상세 조회, 영업구분 코드 조회, 영업경로 코드 조회, 영업상품 코드 조회 |
| 이 페이지의 역할 | 수정 · 영업 수정 |
| 판단 결과·다음 업무 | [영업 관리](sales-management.md) |
| 다른 화면과의 구분 | 연동 협업 관리 > 연동 협업 관리 > 영업 관리에서 사용하는 수정 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 삭제 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/ProgressHistorySection.tsx#L234) |
| 확인 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/SalesRegistrationPage.tsx#L373) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 영업 관리 업체 등록에서 대상과 입력값을 확인해 **영업 수정** 업무를 처리한다. |
| 메뉴·화면 경로 | 연동 협업 관리 > 연동 협업 관리 > 영업 관리 · `/hub-collab/sales-management/:id/edit` · 경로 변수 `id` |
| 화면 유형·담당 | 수정 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [영업 관리](sales-management.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/hub-collab/sales-management` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `id` |
| 전체 사원 목록 조회 (진행내역 담당자 콤보용) | `/hub-collab/sales-management` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 영업 상세 조회 | `/hub-collab/sales-management` `VIEW` | `id: Int` |
| 영업구분 코드 조회 | `/hub-collab/sales-management` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 영업경로 코드 조회 | `/hub-collab/sales-management` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 영업상품 코드 조회 | `/hub-collab/sales-management` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 업종 코드 조회 | `/hub-collab/sales-management` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 영업대표 목록 조회 | `/hub-collab/sales-management` `VIEW` | `includeRetired: Boolean` |
| 영업그룹 코드 조회 | `/hub-collab/sales-management` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 진행내역 비고 조회 | `/hub-collab/sales-management` `VIEW` | `historyId: Int` |
| 영업 수정 | `/hub-collab/sales-management` `PROCESS` | `id: Int` · `UpdateSalesRequest` `id`, `companyName`, `salesRep`, `groupName`, `businessNumber`, `companyContact`, `contactPhone`, `contactEmail`, `expectedOrderMonth`, `salesStartMonth`, `salesEndDate`, `usageTimeSales`, `usageTimePurchase`, `industry` · 서버 필수 `id`, `companyName`, `salesRep`, `companyContact`, `contactPhone`, `salesStartMonth`, `industry`, `salesChannel`, `salesProduct`, `integrationMethod` |
| 진행내역 비고 등록 | `/hub-collab/sales-management` `PROCESS` | `historyId: Int` · `ProgressReplyInputDto` `content` · 서버 필수 `content` |
| 진행내역 비고 삭제 | `/hub-collab/sales-management` `DELETE` | `replyId: Int` |

코드에서 확인한 버튼·작업명은 **수주 예상월**, **영업 시작월**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [영업 관리](sales-management.md)에서 대상 또는 작업을 선택한다. `/hub-collab/sales-management/:id/edit`에서 이전 화면이 전달한 `id`와 현재 대상을 확인한다.
2. **방문**, **연락** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **등록**, **저장 중...**, **확인** 중 해당 버튼을 선택한다.
3. **영업 수정**을 실행하기 전에 변경 대상과 입력값을 확인한다. 처리 응답을 확인하고 관련 조회에서 대상의 상태를 확인한다.
4. 후속 조회나 목록 복귀가 필요하면 [영업 관리](sales-management.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `id` |
| 업체명을 입력하세요 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/SalesForm.tsx#L180) |
| 담당자명을 입력하세요 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/SalesForm.tsx#L268) |
| 추진배경 : &#10;요구사항 :&#10;Needs :&#10;의사결정 포인트 :&#10;영업전략 : | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/SalesForm.tsx#L539) |
| 계약기간 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/QuoteProposalFormSection.tsx#L102) |
| 요금제 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/QuoteProposalFormSection.tsx#L134) |
| SSS 비용 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/QuoteProposalFormSection.tsx#L161) |
| 부가서비스비용 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/QuoteProposalFormSection.tsx#L178) |
| 부가서비스 비용 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/QuoteProposalFormSection.tsx#L191) |
| 비고 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/QuoteProposalFormSection.tsx#L205) |
| 작성일시 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/ProgressHistorySection.tsx#L327) |
| 담당자 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/ProgressHistorySection.tsx#L336) |
| 진행 현황 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/ProgressHistorySection.tsx#L348) |
| 진행형태 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/ProgressHistorySection.tsx#L390) |
| 진행일자 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/ProgressHistorySection.tsx#L361) |
| 투입시간 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/ProgressHistorySection.tsx#L402) |
| 방문목적 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/ProgressHistorySection.tsx#L410) |
| 향후계획 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/ProgressHistorySection.tsx#L383) |
| 예정일자 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/ProgressHistorySection.tsx#L396) |
| 방문 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/ProgressHistoryFormSection.tsx#L62) |
| 연락 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/ProgressHistoryFormSection.tsx#L68) |
| 진행 메모 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/ProgressHistoryFormSection.tsx#L196) |
| 진행 메모를 입력하세요 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/ProgressHistoryFormSection.tsx#L202) |
| 진행예정 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/ProgressHistoryFormSection.tsx#L167) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 전체 사원 목록 조회 (진행내역 담당자 콤보용) | `GET /api/v1/sales/codes/employees` · `/hub-collab/sales-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/sales/SalesCodeController.kt#L133) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `swNo`, `name` | 직접 DB 호출이 연결된 경로는 현재 소스에서 미확인. 세부 저장소는 Controller와 Service 참조. |
| 영업 상세 조회 | `GET /api/v1/sales/{id}` · `/hub-collab/sales-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/sales/SalesController.kt#L172) | `id: Int` → `success`, `data`, `error`, `id`, `companyName`, `salesRep`, `salesRepSwNo`, `groupName`, `groupTitle`, `businessNumber`, `companyContact`, `contactPhone` | `office.dbo.BUSINESS_STRATEGY`, `office.dbo.BUSINESS`, `office.dbo.SAWON`, `office.dbo.FUNCTION_CODE`, `office.dbo.BUSINESS_CONTRACT_HIS` 외 2개 |
| 영업구분 코드 조회 | `GET /api/v1/sales/codes/categories` · `/hub-collab/sales-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/sales/SalesCodeController.kt#L112) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `code`, `title` | 직접 DB 호출이 연결된 경로는 현재 소스에서 미확인. 세부 저장소는 Controller와 Service 참조. |
| 영업경로 코드 조회 | `GET /api/v1/sales/codes/channels` · `/hub-collab/sales-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/sales/SalesCodeController.kt#L94) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `code`, `title` | `office.dbo.upBNS_BusinessRoute` |
| 영업상품 코드 조회 | `GET /api/v1/sales/codes/products` · `/hub-collab/sales-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/sales/SalesCodeController.kt#L75) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `code`, `title` | `office.dbo.upBNS_BusinessRoute` |
| 업종 코드 조회 | `GET /api/v1/sales/codes/industries` · `/hub-collab/sales-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/sales/SalesCodeController.kt#L103) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `code`, `title` | `office.dbo.upBNS_BusinessRoute` |
| 영업대표 목록 조회 | `GET /api/v1/sales/codes/representatives` · `/hub-collab/sales-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/sales/SalesCodeController.kt#L121) | `includeRetired: Boolean` → `success`, `data`, `error`, `swNo`, `name`, `leaveYn` | `office.dbo.DEPT_MANAGER`, `office.dbo.SAWON`, `office.dbo.DEPT_DETAIL` |
| 영업그룹 코드 조회 | `GET /api/v1/sales/codes/groups` · `/hub-collab/sales-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/sales/SalesCodeController.kt#L85) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `code`, `title` | `office.dbo.FUNCTION_CODE` |
| 진행내역 비고 조회 | `GET /api/v1/sales/progress-history/{historyId}/replies` · `/hub-collab/sales-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/sales/SalesController.kt#L331) | `historyId: Int` → `success`, `data`, `error`, `id`, `historyId`, `content`, `createdAt`, `createdBy`, `createdByName` | `office.dbo.upBNS_LstBnsReply` |
| 영업 수정 | `PUT /api/v1/sales/{id}` · `/hub-collab/sales-management` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/sales/SalesController.kt#L217) | `id: Int` · `UpdateSalesRequest` `id`, `companyName`, `salesRep`, `groupName`, `businessNumber`, `companyContact`, `contactPhone`, `contactEmail`, `expectedOrderMonth`, `salesStartMonth`, `salesEndDate`, `usageTimeSales`, `usageTimePurchase`, `industry` · 서버 필수 `id`, `companyName`, `salesRep`, `companyContact`, `contactPhone`, `salesStartMonth`, `industry`, `salesChannel`, `salesProduct`, `integrationMethod` → `success`, `data`, `error`, `message` | `office.dbo.BUSINESS_STRATEGY`, `office.dbo.BUSINESS`, `office.dbo.SAWON`, `office.dbo.FUNCTION_CODE`, `smartwork.dbo.usp_sales_update` 외 3개 · 정의에서 확인한 쓰기 `office.dbo.BUSINESS`, `office.dbo.BUSINESS_STEP`, `office.dbo.BUSINESS_STRATEGY`, `office.dbo.BUSINESS_CONTRACT_HIS` 외 2개 · 코드 연계 트랜잭션 |
| 진행내역 비고 등록 | `POST /api/v1/sales/progress-history/{historyId}/replies` · `/hub-collab/sales-management` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/sales/SalesController.kt#L344) | `historyId: Int` · `ProgressReplyInputDto` `content` · 서버 필수 `content` → `success`, `data`, `error`, `message` | `office.dbo.upBNS_SavBnsReply` · 정의에서 확인한 쓰기 `office.dbo.BUSINESS_HISTORY_REPLY` · 코드 연계 트랜잭션 |
| 진행내역 비고 삭제 | `DELETE /api/v1/sales/progress-history/replies/{replyId}` · `/hub-collab/sales-management` `DELETE` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/sales/SalesController.kt#L363) | `replyId: Int` → `success`, `data`, `error`, `message` | `office.dbo.BUSINESS_HISTORY_REPLY`, `office.dbo.upBNS_DelBnsReply` · 정의에서 확인한 쓰기 `office.dbo.BUSINESS_HISTORY_REPLY` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `office.dbo.BUSINESS_STRATEGY` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesMapper.kt#L244) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-a7f3c4749af8a4fe) |
| `office.dbo.BUSINESS` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesMapper.kt#L244) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-1c6a832844bf01aa) |
| `office.dbo.SAWON` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesMapper.kt#L244) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3a9ea6e368df5cb3) |
| `office.dbo.FUNCTION_CODE` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesMapper.kt#L244) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-c6c02d5b7b192e0e) |
| `office.dbo.BUSINESS_CONTRACT_HIS` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesMapper.kt#L378) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-c5d58e6e24c587a8) |
| `office.dbo.upBNS_BnsHistoryInfo02` | @bns_id int, @rdoSlt varchar(10), @teamno int, @swno int | 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesMapper.kt#L423) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-d6d7918256fc47b6) |
| `office.dbo.upBNS_LstBnsReply` | @his_id int | 정의 참조 `office.dbo.BUSINESS_HISTORY_REPLY`, `office.dbo.SAWON` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesMapper.kt#L466) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-7f0f3d95d761e8d6) |
| `office.dbo.upBNS_BusinessRoute` | @cate01 varchar(15), @cate02 varchar(7), @flag varchar(5), @orderby varchar(10) = NULL | 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesCodeMapper.kt#L59) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-9f917ea22b3cc4fc) |
| `office.dbo.DEPT_MANAGER` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesCodeMapper.kt#L116) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-6bd350bbf4a76a9a) |
| `office.dbo.DEPT_DETAIL` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesCodeMapper.kt#L116) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-f1473984f53ebe9a) |
| `smartwork.dbo.usp_sales_update` | @BNS_ID int, @BNS_SITE varchar(100), @BNS_LEADER int, @BNS_CATEGORY char(2), @BNS_GRADE char(1), @SALE_RANK int, @CONTACT_POINT varchar(20), @CONTACT_HP varchar(20), @CONTACT_EMAIL varchar(50), @AR_CUSTOMER int, @AP_CUSTOMER int, @AR_USE_DATE varchar(10), @AP_USE_DATE varchar(10), @ENTRY_DATE varchar(10), @INF_TYPE varchar(10), @CONEXPDATE varchar(10), @STRATEGY varchar(10), @STRATEGY_DTL varchar(10), @RECEIVE_DATE varchar(10), @GROUP_NAME varchar(20), @PM int, @COM_REGNO varchar(10), @BNS_PRODUCT varchar(2), @BNS_DIVISION char(1), @CONTENT nvarchar(max), @BNS_SALES_GRADE char(1) = NULL, @BNS_SALES_STATUS char(1) = NULL, @BNS_INTEGRATION_STATUS char(1) = NULL | 정의 참조 `office.dbo.BUSINESS`, `office.dbo.BUSINESS_STEP`, `office.dbo.BUSINESS_STRATEGY` · 정적 쓰기 `office.dbo.BUSINESS`, `office.dbo.BUSINESS_STEP`, `office.dbo.BUSINESS_STRATEGY` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesMapper.kt#L323) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-6d3ca83ef4517d46) |
| `office.dbo.upBNS_SavContractHistory` | @BNS_ID int, @FROM_DATE varchar(7), @TO_DATE varchar(7), @CHARGE_NAME varchar(50), @SSS_FEE money, @ADDSERVICE_FEE money, @REMARK varchar(500) | 정의 참조 `office.dbo.BUSINESS_CONTRACT_HIS` · 정적 쓰기 `office.dbo.BUSINESS_CONTRACT_HIS` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesMapper.kt#L402) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-abebe98d8e7496d3) |
| `office.dbo.upBNS_SavBNSHIstory` | @bns_id int, @sw_no int, @visit_com char(1), @visit_date varchar(10), @visit_time numeric(18,0), @visit_content text, @plan_visit_com char(1), @plan_visit_from_date varchar(10), @plan_visit_to_date varchar(10), @plan_visit_content text, @pWriter int, @pRegDate varchar(30), @his_id int, @plan_visit_time numeric(18,0) | 정의 참조 `office.dbo.BUSINESS_HISTORY`, `office.dbo.BUSINESS_HISTORY_REPLY` · 정적 쓰기 `office.dbo.BUSINESS_HISTORY`, `office.dbo.BUSINESS_HISTORY_REPLY` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesMapper.kt#L451) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-0f79dd521be4267d) |
| `smartwork.dbo.usp_sales_save` | @BNS_SITE varchar(100), @BNS_LEADER int, @BNS_CATEGORY char(2), @BNS_GRADE char(1), @SALE_RANK int, @CONTACT_POINT varchar(20), @CONTACT_HP varchar(20), @CONTACT_EMAIL varchar(50), @AR_CUSTOMER int, @AP_CUSTOMER int, @SW_NO int, @AR_USE_DATE varchar(10), @AP_USE_DATE varchar(10), @ENTRY_DATE varchar(10), @INF_TYPE varchar(10), @CONEXPDATE varchar(10), @STRATEGY varchar(10), @STRATEGY_DTL varchar(10), @RECEIVE_DATE varchar(10), @GROUP_NAME varchar(20), @PM int, @COM_REGNO varchar(10), @BNS_PRODUCT varchar(2), @BNS_DIVISION char(1), @CONTENT nvarchar(max), @BNS_SALES_GRADE char(1) = NULL, @BNS_SALES_STATUS char(1) = NULL, @BNS_INTEGRATION_STATUS char(1) = NULL, @BNS_ID int OUT | 정의 참조 `office.dbo.BUSINESS`, `office.dbo.BUSINESS_STEP`, `office.dbo.BUSINESS_STRATEGY` · 정적 쓰기 `office.dbo.BUSINESS`, `office.dbo.BUSINESS_STEP`, `office.dbo.BUSINESS_STRATEGY` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesMapper.kt#L285) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-2ab3521cb66b82f0) |
| `office.dbo.upBNS_SavBnsReply` | @his_id int, @content varchar(2000), @sw_no int | 정의 참조 `office.dbo.BUSINESS_HISTORY_REPLY` · 정적 쓰기 `office.dbo.BUSINESS_HISTORY_REPLY` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesMapper.kt#L480) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-a0320afaa6733738) |
| `office.dbo.BUSINESS_HISTORY_REPLY` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesMapper.kt#L484) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-9abe07fbca2cb4a6) |
| `office.dbo.upBNS_DelBnsReply` | @reply_id int | 정의 참조 `office.dbo.BUSINESS_HISTORY_REPLY` · 정적 쓰기 `office.dbo.BUSINESS_HISTORY_REPLY` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesMapper.kt#L489) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-745607a1fb20e1b3) |

### 매퍼 호출 추가 확인

| DB 객체 | 호출 근거 | 개발 DB 확인 범위 |
| --- | --- | --- |
| [office.dbo.upApp_SawonList](../../references/all-pages-demo.md#object-a7f6826ec54e8008) | [findEmployees](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesCodeMapper.kt#L125) | 개발 카탈로그 확인 |
| [office.dbo.SSP_BNS_DIVISION_LIST](../../references/all-pages-demo.md#object-59b44da4cea2d1dc) | [findCategories](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesCodeMapper.kt#L77) | 개발 카탈로그 확인 |
| [office.dbo.upApp_BusinessSawonList](../../references/all-pages-demo.md#object-ac2a9723e4fad5c2) | [findRepresentatives](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesCodeMapper.kt#L87) | 개발 카탈로그 확인 |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 계약기간, 요금제, SSS 비용, 부가서비스비용, 비고, 작성일시 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 연동 협업 관리 > 연동 협업 관리 > 영업 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 데이터 로딩에 실패했습니다. | 계약기간, 요금제, SSS 비용, 부가서비스비용, 비고, 작성일시 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 기존 데이터에서 복사되었습니다. | 계약기간, 요금제, SSS 비용, 부가서비스비용, 비고, 작성일시 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 비고 등록에 실패했습니다. | 계약기간, 요금제, SSS 비용, 부가서비스비용, 비고, 작성일시 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 비고 삭제에 실패했습니다. | 계약기간, 요금제, SSS 비용, 부가서비스비용, 비고, 작성일시 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/IntegrationRoutes.tsx#L84) · [SalesRegistrationPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/SalesRegistrationPage.tsx#L29) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/salesManagementApi.ts#L238) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/salesManagementApi.ts#L108) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/salesManagementApi.ts#L286) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/salesManagementApi.ts#L274) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/salesManagementApi.ts#L220) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/salesManagementApi.ts#L280) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/salesManagementApi.ts#L229) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/salesManagementApi.ts#L268) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 17개 중 개발 메타데이터 확인 17개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-a0be5bcb13aec798) | Demo 메타데이터 20/20개 확인 · Dev와 계약 차이 1개 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

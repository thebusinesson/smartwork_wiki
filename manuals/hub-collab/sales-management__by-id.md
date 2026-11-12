# [연동 영업과 프로젝트 완료] 영업 관리 상세 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

영업 단건 + 견적 제안 목록 + 진행 내역 목록 통합 응답. 존재하지 않으면 data=null.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 연동 영업과 프로젝트 완료 |
| 언제 사용하는가 | 영업 상세 조회, 견적 제안 목록 조회, 진행 내역 조회 (다건), 변경 이력 조회, 진행내역 비고 조회 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 업체명, 영업대표, 그룹명, 대표사업자번호, 업체 담당자, 담당자 연락처 |
| 업무 흐름 | 영업 상세 조회, 견적 제안 목록 조회, 진행 내역 조회 (다건), 변경 이력 조회, 진행내역 비고 조회 |
| 이 페이지의 역할 | 상세 · 영업 상세 조회 |
| 판단 결과·다음 업무 | [영업 관리](sales-management.md) · [영업 관리 업체 등록](sales-management__by-id__edit.md) · [영업 관리 업체 등록](sales-management__new.md) |
| 다른 화면과의 구분 | 연동 협업 관리 > 연동 협업 관리 > 영업 관리에서 사용하는 상세 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 삭제 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/ProgressHistorySection.tsx#L234) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 영업 단건 + 견적 제안 목록 + 진행 내역 목록 통합 응답. 존재하지 않으면 data=null. |
| 메뉴·화면 경로 | 연동 협업 관리 > 연동 협업 관리 > 영업 관리 · `/hub-collab/sales-management/:id` · 경로 변수 `id` |
| 화면 유형·담당 | 상세 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [영업 관리](sales-management.md) · [영업 관리 업체 등록](sales-management__by-id__edit.md) · [영업 관리 업체 등록](sales-management__new.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/hub-collab/sales-management` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `id` |
| 영업 상세 조회 | `/hub-collab/sales-management` `VIEW` | `id: Int` |
| 견적 제안 목록 조회 | `/hub-collab/sales-management` `VIEW` | `salesId: Int` · `month: String?` |
| 진행 내역 조회 (다건) | `/hub-collab/sales-management` `VIEW` | `salesId: Int` |
| 변경 이력 조회 | `/hub-collab/sales-management` `VIEW` | `salesId: Int` · `page: Int` · `size: Int` · `fieldFilter: String?` |
| 진행내역 비고 조회 | `/hub-collab/sales-management` `VIEW` | `historyId: Int` |
| 영업 삭제 | `/hub-collab/sales-management` `DELETE` | `id: Int` |
| 진행 내역 등록 (단건) | `/hub-collab/sales-management` `PROCESS` | `salesId: Int` · `ProgressHistoryInputDto` `content`, `scheduledDate`, `contactPerson`, `progressType`, `workHours`, `nextProgressType`, `nextScheduledDate`, `nextExpectedHours`, `nextPurpose` |
| 진행내역 비고 등록 | `/hub-collab/sales-management` `PROCESS` | `historyId: Int` · `ProgressReplyInputDto` `content` · 서버 필수 `content` |
| 진행내역 비고 삭제 | `/hub-collab/sales-management` `DELETE` | `replyId: Int` |

코드에서 확인한 버튼·작업명은 **변경내역**, **삭제**, **등록**, **수정**, **복사하여 작성**, **목록**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [영업 관리](sales-management.md)에서 대상 또는 작업을 선택한다. `/hub-collab/sales-management/:id`에서 이전 화면이 전달한 `id`와 현재 대상을 확인한다.
2. **변경내역 항목 선택** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **등록** 중 해당 버튼을 선택한다.
3. **영업 상세 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [영업 관리 업체 등록](sales-management__by-id__edit.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `id` |
| 업체명 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/SalesDetailInfo.tsx#L65) |
| 영업대표 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/SalesDetailInfo.tsx#L71) |
| 그룹명 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/SalesDetailInfo.tsx#L81) |
| 대표사업자번호 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/SalesDetailInfo.tsx#L99) |
| 업체 담당자 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/SalesDetailInfo.tsx#L117) |
| 담당자 연락처 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/SalesDetailInfo.tsx#L135) |
| 수주 예상월 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/SalesDetailInfo.tsx#L141) |
| 담당자 이메일 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/SalesDetailInfo.tsx#L151) |
| 영업 시작월 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/SalesDetailInfo.tsx#L157) |
| 업종 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/SalesDetailInfo.tsx#L167) |
| 영업 종료일 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/SalesDetailInfo.tsx#L173) |
| 영업 구분 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/SalesDetailInfo.tsx#L183) |
| 우선순위 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/SalesDetailInfo.tsx#L189) |
| 영업 경로 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/SalesDetailInfo.tsx#L199) |
| 예상 매출 업체수 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/SalesDetailInfo.tsx#L205) |
| 영업 상품 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/SalesDetailInfo.tsx#L217) |
| 예상 매입 업체수 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/SalesDetailInfo.tsx#L223) |
| 연동방식 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/SalesDetailInfo.tsx#L235) |
| 사용시기 - 매출 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/SalesDetailInfo.tsx#L241) |
| 담당 PM | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/SalesDetailInfo.tsx#L251) |
| 사용시기 - 매입 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/SalesDetailInfo.tsx#L257) |
| 계약기간 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/QuoteProposalSection.tsx#L61) |
| 요금제 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/QuoteProposalSection.tsx#L67) |
| SSS비용 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/QuoteProposalSection.tsx#L73) |
| 부가서비스비용 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/QuoteProposalSection.tsx#L81) |
| 비고 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/QuoteProposalSection.tsx#L93) |
| 작성일시 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/ProgressHistorySection.tsx#L327) |
| 담당자 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/ProgressHistorySection.tsx#L336) |
| 진행 현황 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/ProgressHistorySection.tsx#L348) |
| 진행형태 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/ProgressHistorySection.tsx#L390) |
| 진행일자 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/ProgressHistorySection.tsx#L361) |
| 투입시간 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/ProgressHistorySection.tsx#L402) |
| 방문목적 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/ProgressHistorySection.tsx#L410) |
| 향후계획 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/ProgressHistorySection.tsx#L383) |
| 예정일자 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/ProgressHistorySection.tsx#L396) |
| 변경내역 항목 선택 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/ChangeHistoryDialog.tsx#L60) |
| 변경일시 | 출력 | 조회 응답 기준 | 화면 필드 `changedAt` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/ChangeHistoryDialog.tsx#L87) |
| 변경내역 (항목) | 출력 | 조회 응답 기준 | 화면 필드 `changedField` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/ChangeHistoryDialog.tsx#L94) |
| 변경전 내역 | 출력 | 조회 응답 기준 | 화면 필드 `beforeValue` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/ChangeHistoryDialog.tsx#L99) |
| 변경후 내역 | 출력 | 조회 응답 기준 | 화면 필드 `afterValue` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/components/ChangeHistoryDialog.tsx#L105) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 영업 상세 조회 | `GET /api/v1/sales/{id}` · `/hub-collab/sales-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/sales/SalesController.kt#L172) | `id: Int` → `success`, `data`, `error`, `id`, `companyName`, `salesRep`, `salesRepSwNo`, `groupName`, `groupTitle`, `businessNumber`, `companyContact`, `contactPhone` | `office.dbo.BUSINESS_STRATEGY`, `office.dbo.BUSINESS`, `office.dbo.SAWON`, `office.dbo.FUNCTION_CODE`, `office.dbo.BUSINESS_CONTRACT_HIS` 외 2개 |
| 견적 제안 목록 조회 | `GET /api/v1/sales/{salesId}/quote-proposals` · `/hub-collab/sales-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/sales/SalesController.kt#L265) | `salesId: Int` · `month: String?` → `success`, `data`, `error`, `content`, `totalElements` | `office.dbo.BUSINESS_CONTRACT_HIS` |
| 진행 내역 조회 (다건) | `GET /api/v1/sales/{salesId}/progress-history` · `/hub-collab/sales-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/sales/SalesController.kt#L299) | `salesId: Int` → `success`, `data`, `error`, `id`, `salesId`, `content`, `scheduledDate`, `contactPerson`, `createdAt`, `createdBy`, `progressType`, `workHours` | `office.dbo.upBNS_BnsHistoryInfo02`, `office.dbo.upBNS_LstBnsReply` |
| 변경 이력 조회 | `GET /api/v1/sales/{salesId}/change-history` · `/hub-collab/sales-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/sales/SalesController.kt#L382) | `salesId: Int` · `page: Int` · `size: Int` · `fieldFilter: String?` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `currentPage`, `size` | `office.dbo.BUSINESS_HISTORY_MNG`, `office.dbo.SAWON` |
| 진행내역 비고 조회 | `GET /api/v1/sales/progress-history/{historyId}/replies` · `/hub-collab/sales-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/sales/SalesController.kt#L331) | `historyId: Int` → `success`, `data`, `error`, `id`, `historyId`, `content`, `createdAt`, `createdBy`, `createdByName` | `office.dbo.upBNS_LstBnsReply` |
| 영업 삭제 | `DELETE /api/v1/sales/{id}` · `/hub-collab/sales-management` `DELETE` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/sales/SalesController.kt#L246) | `id: Int` → `success`, `data`, `error`, `message` | `office.dbo.upBNS_DelBns` · 정의에서 확인한 쓰기 `office.dbo.BUSINESS_HISTORY_MNG`, `office.dbo.BUSINESS_HISTORY_REPLY`, `office.dbo.BUSINESS_HISTORY`, `office.dbo.BUSINESS` 외 1개 · 코드 연계 트랜잭션 |
| 진행 내역 등록 (단건) | `POST /api/v1/sales/{salesId}/progress-history` · `/hub-collab/sales-management` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubcollab/sales/SalesController.kt#L312) | `salesId: Int` · `ProgressHistoryInputDto` `content`, `scheduledDate`, `contactPerson`, `progressType`, `workHours`, `nextProgressType`, `nextScheduledDate`, `nextExpectedHours`, `nextPurpose` → `success`, `data`, `error`, `message` | `office.dbo.upBNS_SavBNSHIstory` · 정의에서 확인한 쓰기 `office.dbo.BUSINESS_HISTORY`, `office.dbo.BUSINESS_HISTORY_REPLY` · 코드 연계 트랜잭션 |
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
| `office.dbo.BUSINESS_HISTORY_MNG` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesMapper.kt#L533) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-dcd6a4a1673f2f3b) |
| `office.dbo.upBNS_DelBns` | @bns_id int, @sw_no int | 정의 참조 `office.dbo.BUSINESS`, `office.dbo.BUSINESS_HISTORY`, `office.dbo.BUSINESS_HISTORY_MNG`, `office.dbo.BUSINESS_HISTORY_REPLY`, `office.dbo.BUSINESS_STEP` · 정적 쓰기 `office.dbo.BUSINESS_HISTORY_MNG`, `office.dbo.BUSINESS_HISTORY_REPLY`, `office.dbo.BUSINESS_HISTORY`, `office.dbo.BUSINESS` 외 1개 · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesMapper.kt#L344) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3cc1fcc7eafc8ce1) |
| `office.dbo.upBNS_SavBNSHIstory` | @bns_id int, @sw_no int, @visit_com char(1), @visit_date varchar(10), @visit_time numeric(18,0), @visit_content text, @plan_visit_com char(1), @plan_visit_from_date varchar(10), @plan_visit_to_date varchar(10), @plan_visit_content text, @pWriter int, @pRegDate varchar(30), @his_id int, @plan_visit_time numeric(18,0) | 정의 참조 `office.dbo.BUSINESS_HISTORY`, `office.dbo.BUSINESS_HISTORY_REPLY` · 정적 쓰기 `office.dbo.BUSINESS_HISTORY`, `office.dbo.BUSINESS_HISTORY_REPLY` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesMapper.kt#L451) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-0f79dd521be4267d) |
| `office.dbo.upBNS_SavBnsReply` | @his_id int, @content varchar(2000), @sw_no int | 정의 참조 `office.dbo.BUSINESS_HISTORY_REPLY` · 정적 쓰기 `office.dbo.BUSINESS_HISTORY_REPLY` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesMapper.kt#L480) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-a0320afaa6733738) |
| `office.dbo.BUSINESS_HISTORY_REPLY` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesMapper.kt#L484) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-9abe07fbca2cb4a6) |
| `office.dbo.upBNS_DelBnsReply` | @reply_id int | 정의 참조 `office.dbo.BUSINESS_HISTORY_REPLY` · 정적 쓰기 `office.dbo.BUSINESS_HISTORY_REPLY` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubcollab/sales/repository/SalesMapper.kt#L489) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-745607a1fb20e1b3) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 업체명, 영업대표, 그룹명, 대표사업자번호, 업체 담당자, 담당자 연락처 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 연동 협업 관리 > 연동 협업 관리 > 영업 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 비고 등록에 실패했습니다. | 업체명, 영업대표, 그룹명, 대표사업자번호, 업체 담당자, 담당자 연락처 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 비고 삭제에 실패했습니다. | 업체명, 영업대표, 그룹명, 대표사업자번호, 업체 담당자, 담당자 연락처 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 변경 이력이 없습니다. | 업체명, 영업대표, 그룹명, 대표사업자번호, 업체 담당자, 담당자 연락처 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/IntegrationRoutes.tsx#L85) · [SalesManagementDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/SalesManagementDetailPage.tsx#L15) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/salesManagementApi.ts#L108) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/salesManagementApi.ts#L137) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/salesManagementApi.ts#L152) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/salesManagementApi.ts#L195) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/salesManagementApi.ts#L167) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/salesManagementApi.ts#L129) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/salesManagementApi.ts#L160) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/api/salesManagementApi.ts#L174) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 13개 중 개발 메타데이터 확인 13개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-04e968161080121c) | Demo 메타데이터 13/13개 확인 · Dev와 계약 차이 1개 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

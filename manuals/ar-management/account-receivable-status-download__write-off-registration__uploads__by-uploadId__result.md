# [매출채권과 회수·대손 기록] 매출 채권 현황 다운로드 처리 결과 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

업로드에서 저장 완료된 회사의 매출채권 현황 스냅샷을 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 매출채권과 회수·대손 기록 |
| 언제 사용하는가 | 업로드 반영 결과 조회 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 청구서 날짜, 사업자 코드, 사업자번호, 거래처명, 기초 잔액, 청구합계 |
| 업무 흐름 | 업로드 반영 결과 조회 |
| 이 페이지의 역할 | 처리 결과 · 업로드 반영 결과 조회 |
| 판단 결과·다음 업무 | [매출 채권 현황 다운로드](account-receivable-status-download.md) |
| 다른 화면과의 구분 | 서비스 현황 > 채권 관리 > 매출 채권 현황 다운로드에서 사용하는 처리 결과 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 제각내역 개별등록 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/arManagement/components/WriteOffRegistrationTabs.tsx#L42) |
| 제각내역 파일 업로드 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/arManagement/components/WriteOffRegistrationTabs.tsx#L48) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 업로드에서 저장 완료된 회사의 매출채권 현황 스냅샷을 조회한다. |
| 메뉴·화면 경로 | 서비스 현황 > 채권 관리 > 매출 채권 현황 다운로드 · `/ar-management/account-receivable-status-download/write-off-registration/uploads/:uploadId/result` · 경로 변수 `uploadId` |
| 화면 유형·담당 | 처리 결과 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [매출 채권 현황 다운로드](account-receivable-status-download.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/ar-management/account-receivable-status-download` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `uploadId` |
| 업로드 반영 결과 조회 | `/ar-management/account-receivable-status-download` `VIEW` | `uploadId: Long` · `page: Int` · `size: Int` |

코드에서 확인한 버튼·작업명은 **매출채권 현황 다운로드**, **목록**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [매출 채권 현황 다운로드](account-receivable-status-download.md)에서 대상 또는 작업을 선택한다. `/ar-management/account-receivable-status-download/write-off-registration/uploads/:uploadId/result`에서 이전 화면이 전달한 `uploadId`와 현재 대상을 확인한다.
2. **업로드 반영 결과 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
3. 후속 조회나 목록 복귀가 필요하면 [매출 채권 현황 다운로드](account-receivable-status-download.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `uploadId` |
| 청구서 날짜 | 출력 | 조회 응답 기준 | 화면 필드 `billingDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/arManagement/AccountReceivableWriteOffRegistrationResultPage.tsx#L28) |
| 사업자 코드 | 출력 | 조회 응답 기준 | 화면 필드 `businessCode` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/arManagement/AccountReceivableWriteOffRegistrationResultPage.tsx#L29) |
| 사업자번호 | 출력 | 조회 응답 기준 | 화면 필드 `businessNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/arManagement/AccountReceivableWriteOffRegistrationResultPage.tsx#L32) |
| 거래처명 | 출력 | 조회 응답 기준 | 화면 필드 `companyName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/arManagement/AccountReceivableWriteOffRegistrationResultPage.tsx#L39) |
| 기초 잔액 | 출력 | 조회 응답 기준 | 화면 필드 `initialAmount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/arManagement/AccountReceivableWriteOffRegistrationResultPage.tsx#L48) |
| 청구합계 | 출력 | 조회 응답 기준 | 화면 필드 `invoiceAmount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/arManagement/AccountReceivableWriteOffRegistrationResultPage.tsx#L49) |
| 입금합계 | 출력 | 조회 응답 기준 | 화면 필드 `paymentAmount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/arManagement/AccountReceivableWriteOffRegistrationResultPage.tsx#L50) |
| 제각금액 | 출력 | 조회 응답 기준 | 화면 필드 `removeBondAmount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/arManagement/AccountReceivableWriteOffRegistrationResultPage.tsx#L51) |
| 제각환입 | 출력 | 조회 응답 기준 | 화면 필드 `repayBondAmount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/arManagement/AccountReceivableWriteOffRegistrationResultPage.tsx#L52) |
| 잔여 채권 | 출력 | 조회 응답 기준 | 화면 필드 `remainAmount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/arManagement/AccountReceivableWriteOffRegistrationResultPage.tsx#L53) |
| 청구세금계산서 | 출력 | 조회 응답 기준 | 화면 필드 `taxInvoiceLabel` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/arManagement/AccountReceivableWriteOffRegistrationResultPage.tsx#L54) |
| 매출유형 | 출력 | 조회 응답 기준 | 화면 필드 `salesType` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/arManagement/AccountReceivableWriteOffRegistrationResultPage.tsx#L55) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 업로드 반영 결과 조회 | `GET /api/v1/ar-management/account-receivable-status/write-off-registrations/uploads/{uploadId}/result` · `/ar-management/account-receivable-status-download` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/armanagement/writeoffregistration/AccountReceivableWriteOffRegistrationController.kt#L171) | `uploadId: Long` · `page: Int` · `size: Int` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `currentPage`, `pageSize` | `smartwork.dbo.usp_account_receivable_write_off_result_by_upload_select` |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.usp_account_receivable_write_off_result_by_upload_select` | @UPLOAD_ID bigint, @PAGE int, @PAGE_SIZE int | 정의 참조 `smartwork.dbo.account_receivable_write_off_upload`, `smartwork.dbo.account_receivable_write_off_upload_item`, `smartwork.dbo.usp_account_receivable_write_off_result_core_select` · 쓰기 구문 존재 · 대상 별칭 또는 하위 정의 확인 · 하위 호출 `smartwork.dbo.usp_account_receivable_write_off_result_core_select` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/armanagement/writeoffregistration/repository/AccountReceivableWriteOffRegistrationMapper.kt#L107) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-1f5c3cc4e6e2b116) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 청구서 날짜, 사업자 코드, 사업자번호, 거래처명, 기초 잔액, 청구합계 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 서비스 현황 > 채권 관리 > 매출 채권 현황 다운로드의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 조회 조건이 없어 다운로드 화면으로 이동합니다. | 청구서 날짜, 사업자 코드, 사업자번호, 거래처명, 기초 잔액, 청구합계 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 유효하지 않은 업로드 ID 입니다. | 청구서 날짜, 사업자 코드, 사업자번호, 거래처명, 기초 잔액, 청구합계 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 이번 세션에 저장한 회사가 없어 개별 등록 화면으로 이동합니다. | 청구서 날짜, 사업자 코드, 사업자번호, 거래처명, 기초 잔액, 청구합계 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 반영 결과 조회 중 오류가 발생했습니다. | 청구서 날짜, 사업자 코드, 사업자번호, 거래처명, 기초 잔액, 청구합계 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/ArManagementRoutes.tsx#L14) · [AccountReceivableWriteOffRegistrationResultPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/arManagement/AccountReceivableWriteOffRegistrationResultPage.tsx#L58) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/arManagement/api/accountReceivableWriteOffRegistrationApi.ts#L100) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 1개 중 개발 메타데이터 확인 1개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-83e09b665d8cc536) | Demo 메타데이터 1/1개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

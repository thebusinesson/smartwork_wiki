# [매출채권과 회수·대손 기록] 매출 채권 현황 다운로드 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

청구·입금기간과 제각 대상 여부로 매출채권 현황을 추려 엑셀로 받는다. 제각내역 등록은 별도 화면에서 처리한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 매출채권과 회수·대손 기록 |
| 언제 사용하는가 | 매출 채권 현황 엑셀 다운로드 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 청구기간, 입금기간, 제각 대상 여부 |
| 업무 흐름 | 매출 채권 현황 엑셀 다운로드 |
| 이 페이지의 역할 | 조회 · 매출 채권 현황 엑셀 다운로드 |
| 판단 결과·다음 업무 | [매출 채권 현황 다운로드 개별 등록](account-receivable-status-download__write-off-registration__individual.md) · [매출 채권 현황 다운로드 업로드 이력](account-receivable-status-download__write-off-registration__uploads.md) |
| 다른 화면과의 구분 | 이 경로에서 볼 수 있는 조건·결과를 기준으로 사용한다. 독립 경로의 상세·등록은 관련 화면에 연결한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 청구·입금기간과 제각 대상 여부로 매출채권 현황을 추려 엑셀로 받는다. 제각내역 등록은 별도 화면에서 처리한다. |
| 메뉴·화면 경로 | 서비스 현황 > 채권 관리 > 매출 채권 현황 다운로드 · `/ar-management/account-receivable-status-download` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [매출 채권 현황 다운로드 개별 등록](account-receivable-status-download__write-off-registration__individual.md) · [매출 채권 현황 다운로드 업로드 이력](account-receivable-status-download__write-off-registration__uploads.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/ar-management/account-receivable-status-download` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 매출 채권 현황 엑셀 다운로드 | `/ar-management/account-receivable-status-download` `EXCEL_DOWNLOAD` | `AccountReceivableStatusDownloadRequest` `billingStartMonth`, `billingEndMonth`, `depositPeriodType`, `depositStart`, `depositEnd`, `includeTarget`, `includeNonTarget` |

코드에서 확인한 버튼·작업명은 **제각내역 등록**, **다운로드**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **청구기간**, **입금기간**, **제각 대상 여부**를 설정한다. 대상·비대상 중 필요한 범위를 선택한다.
2. 다운로드 작업을 실행하고 확인창의 조건을 확인한다. 다운로드 완료 후 파일이 해당 조건의 결과인지 대조한다.
3. 제각 기록을 추가하려면 **제각내역 등록**을 선택해 별도 등록 화면에서 진행한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 청구기간 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/arManagement/AccountReceivableStatusDownloadPage.tsx#L144) |
| 입금기간 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/arManagement/AccountReceivableStatusDownloadPage.tsx#L162) |
| 제각 대상 여부 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/arManagement/AccountReceivableStatusDownloadPage.tsx#L206) |
| 대상 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `target` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/arManagement/AccountReceivableStatusDownloadPage.tsx#L212) |
| 비대상 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `non-target` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/arManagement/AccountReceivableStatusDownloadPage.tsx#L213) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 매출 채권 현황 엑셀 다운로드 | `GET /api/v1/ar-management/account-receivable-status/download` · `/ar-management/account-receivable-status-download` `EXCEL_DOWNLOAD` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/armanagement/accountreceivablestatusdownload/AccountReceivableStatusDownloadController.kt#L49) | `AccountReceivableStatusDownloadRequest` `billingStartMonth`, `billingEndMonth`, `depositPeriodType`, `depositStart`, `depositEnd`, `includeTarget`, `includeNonTarget` → 파일 또는 오류 응답 | `smartwork.dbo.usp_account_receivable_status_download_select` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.usp_account_receivable_status_download_select` | @BILLING_START_MONTH varchar(6), @BILLING_END_MONTH varchar(6), @DEPOSIT_PERIOD_TYPE varchar(5), @DEPOSIT_START varchar(10), @DEPOSIT_END varchar(10), @INCLUDE_TARGET bit, @INCLUDE_NON_TARGET bit | 정의 참조 `SmartBill3.dbo.COMPANY`, `SB_DTI.dbo.DTI_HEADER_CUB`, `SB_BILL.dbo.INVOICE`, `SB_BILL.dbo.INVOICE_SALES`, `SB_BILL.dbo.MANUALLY_SALES` 외 2개 · 쓰기 구문 존재 · 대상 별칭 또는 하위 정의 확인 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/armanagement/accountreceivablestatusdownload/repository/AccountReceivableStatusDownloadMapper.kt#L26) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-8b45b484f74f3cac) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 청구기간, 입금기간, 제각 대상 여부 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 서비스 현황 > 채권 관리 > 매출 채권 현황 다운로드의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 다운로드 중 오류가 발생했습니다. | 청구기간, 입금기간, 제각 대상 여부 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/ArManagementRoutes.tsx#L10) · [AccountReceivableStatusDownloadPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/arManagement/AccountReceivableStatusDownloadPage.tsx#L171) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/arManagement/api/accountReceivableStatusDownloadApi.ts#L21) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 1개 중 개발 메타데이터 확인 1개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-889aff4f314aae27) | Demo 메타데이터 1/1개 확인 · 2026-11-11 |
| 화면 재현 | [로컬 Playwright 표본](../../evidence/browser/all-pages-sample-2026-11-11.json) | 진입 및 표시 확인 · 표시 청구기간, 입금기간, 제각내역 등록 · 2026-11-11 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

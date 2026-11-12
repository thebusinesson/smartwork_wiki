# [문서 당사자와 발행·수신 조건] 매입 자동 승인 설정 조회 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

업체별 정발행·역발행·개인매출 자동승인 설정을 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 문서 당사자와 발행·수신 조건 |
| 언제 사용하는가 | 매입 자동 승인 설정 조회 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 사업자번호, 회사명, 정발행 자동승인, 역발행 자동승인, 개인매출 자동승인, 업체 조건 |
| 업무 흐름 | 매입 자동 승인 설정 조회 |
| 이 페이지의 역할 | 조회 · 매입 자동 승인 설정 조회 |
| 판단 결과·다음 업무 | 현재 화면에서 결과를 확인한다. |
| 다른 화면과의 구분 | 같은 경로에서 열리는 조회·팝업은 이 문서에서 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 업체별 정발행·역발행·개인매출 자동승인 설정을 조회한다. |
| 메뉴·화면 경로 | SB 서비스관리 > 전자세금계산서 > 매입 자동 승인 설정 조회 · `/tax-invoice/purchase-auto-approval-settings` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | 현재 화면에서 결과를 확인한다. |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/tax-invoice/purchase-auto-approval-settings` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 매입 자동 승인 설정 조회 | `/tax-invoice/purchase-auto-approval-settings` `VIEW` | `PurchaseAutoApprovalSearchRequest` `searchType`, `keyword`, `issue`, `rissue`, `pissue`, `page`, `size` |

코드에서 확인한 버튼·작업명은 **검색**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **SB 서비스관리 > 전자세금계산서 > 매입 자동 승인 설정 조회**를 연다. `/tax-invoice/purchase-auto-approval-settings`를 연다.
2. **업체 조건**, **전체**, **정발행 자동 승인**, **자동 승인**, **수동 승인**, **역발행 자동 승인**, **개인 매출** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색** 중 해당 버튼을 선택한다.
3. **매입 자동 승인 설정 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 사업자번호 | 출력 | 조회 응답 기준 | 화면 필드 `businessNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/PurchaseAutoApprovalSettings.tsx#L163) |
| 회사명 | 출력 | 조회 응답 기준 | 화면 필드 `companyName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/PurchaseAutoApprovalSettings.tsx#L164) |
| 정발행 자동승인 | 출력 | 조회 응답 기준 | 화면 필드 `issueAutoApproval` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/PurchaseAutoApprovalSettings.tsx#L165) |
| 역발행 자동승인 | 출력 | 조회 응답 기준 | 화면 필드 `rissueAutoApproval` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/PurchaseAutoApprovalSettings.tsx#L166) |
| 개인매출 자동승인 | 출력 | 조회 응답 기준 | 화면 필드 `pissueAutoApproval` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/PurchaseAutoApprovalSettings.tsx#L167) |
| 업체 조건 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/PurchaseAutoApprovalSettings.tsx#L40) |
| 전체 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `all` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/PurchaseAutoApprovalSettings.tsx#L48) |
| 정발행 자동 승인 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/PurchaseAutoApprovalSettings.tsx#L61) |
| 자동 승인 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `AUTO` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/PurchaseAutoApprovalSettings.tsx#L93) |
| 수동 승인 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `MANUAL` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/PurchaseAutoApprovalSettings.tsx#L94) |
| 역발행 자동 승인 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/PurchaseAutoApprovalSettings.tsx#L74) |
| 개인 매출 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/PurchaseAutoApprovalSettings.tsx#L87) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 매입 자동 승인 설정 조회 | `GET /api/v1/tax-invoice/purchase-auto-approval-settings` · `/tax-invoice/purchase-auto-approval-settings` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/taxinvoice/purchaseautoapproval/PurchaseAutoApprovalController.kt#L47) | `PurchaseAutoApprovalSearchRequest` `searchType`, `keyword`, `issue`, `rissue`, `pissue`, `page`, `size` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `currentPage`, `size` | `smartwork.dbo.usp_purchase_auto_approval_settings_select` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.usp_purchase_auto_approval_settings_select` | @PAGE int, @PAGESIZE int, @SCH_TYPE varchar(1), @SCH_KEYWORD varchar(100), @ISSUE varchar(1), @RISSUE varchar(1), @PISSUE varchar(1) | 정의 참조 `SmartBill3.dbo.COMPANY`, `SB_DTI.dbo.COMPANY_DTICONFIG` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/purchaseautoapproval/repository/PurchaseAutoApprovalMapper.kt#L27) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-add3e2b30f9fc616) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 사업자번호, 회사명, 정발행 자동승인, 역발행 자동승인, 개인매출 자동승인, 업체 조건 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 서비스관리 > 전자세금계산서 > 매입 자동 승인 설정 조회의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 검색 결과가 존재하지 않습니다. | 사업자번호, 회사명, 정발행 자동승인, 역발행 자동승인, 개인매출 자동승인, 업체 조건 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/TaxInvoiceRoutes.tsx#L38) · [PurchaseAutoApprovalSettings.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/PurchaseAutoApprovalSettings.tsx#L110) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/api/purchaseAutoApprovalApi.ts#L22) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 1개 중 개발 메타데이터 확인 1개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-91193eefed9dde64) | Demo 메타데이터 1/1개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

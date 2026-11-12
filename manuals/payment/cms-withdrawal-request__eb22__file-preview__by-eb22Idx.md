# [CMS·카드 자동결제와 예외] (EB21/EB22) CMS 자동이체 관리 상세 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

업로드한 EB22 결과를 미리 보고 출금 결과를 반영한다. 반영요청·진행 상태·재요청·완료를 각각 확인한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | CMS·카드 자동결제와 예외 |
| 언제 사용하는가 | EB22 파일 미리보기, EB22 진행 상태 조회, EB22 반영요청, EB22 재요청, EB22 반영완료 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | EB22 파일 번호, 미리보기, 반영 상태 |
| 업무 흐름 | EB22 파일 미리보기, EB22 진행 상태 조회, EB22 반영요청, EB22 재요청, EB22 반영완료 |
| 이 페이지의 역할 | 상세 · EB22 진행 상태 조회 |
| 판단 결과·다음 업무 | [(EB21/EB22) CMS 자동이체 관리](cms-withdrawal-request.md) |
| 다른 화면과의 구분 | 서비스 현황 > 입금관리 > (EB21/EB22) CMS 자동이체 관리에서 사용하는 상세 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 확인 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/CmsWithdrawalPendingResultDetailPage.tsx#L394) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 업로드한 EB22 결과를 미리 보고 출금 결과를 반영한다. 반영요청·진행 상태·재요청·완료를 각각 확인한다. |
| 메뉴·화면 경로 | 서비스 현황 > 입금관리 > (EB21/EB22) CMS 자동이체 관리 · `/payment/cms-withdrawal-request/eb22/file-preview/:eb22Idx` · 경로 변수 `eb22Idx` |
| 화면 유형·담당 | 상세 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [(EB21/EB22) CMS 자동이체 관리](cms-withdrawal-request.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/payment/cms-withdrawal-request` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `eb22Idx` |
| EB22 파일 미리보기 | `/payment/cms-withdrawal-request` `VIEW` | `id: Long` |
| EB22 진행 상태 조회 | `/payment/cms-withdrawal-request` `VIEW` | `id: Long` |
| EB22 반영요청 | `/payment/cms-withdrawal-request` `PROCESS` | `id: Long` |
| EB22 재요청 | `/payment/cms-withdrawal-request` `PROCESS` | `id: Long` |
| EB22 반영완료 | `/payment/cms-withdrawal-request` `PROCESS` | `id: Long` · `force: Boolean` |

코드에서 확인한 버튼·작업명은 **목록**, **출금신청(EB21)**, **출금결과 반영(EB22)**, **지금 상태 확인**, **자동 확인 중**, **자동 확인 중지**, **반영요청**, **재요청**, **반영완료**, **확인**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [(EB21/EB22) CMS 자동이체 관리](cms-withdrawal-request.md)에서 대상 또는 작업을 선택한다. `/payment/cms-withdrawal-request/eb22/file-preview/:eb22Idx`에서 이전 화면이 전달한 `eb22Idx`와 현재 대상을 확인한다.
2. **EB22 진행 상태 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
3. 후속 조회나 목록 복귀가 필요하면 [(EB21/EB22) CMS 자동이체 관리](cms-withdrawal-request.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `eb22Idx` |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| EB22 파일 미리보기 | `GET /api/v1/cms/withdrawal-results/file-preview/{id}` · `/payment/cms-withdrawal-request` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/cmseb22/CmsEb22Controller.kt#L166) | `id: Long` → `success`, `data`, `error`, `id`, `eb22FileName`, `transferRequestDate`, `errorCount`, `errorAmount`, `summary` | `SmartBill3.dbo.CMS_EA22`, `SmartBill3.dbo.CMS_EA22_DETAIL`, `SB_BILL.dbo.PAYMENT`, `SmartBill3.dbo.upCMS_SchRsltEA22` |
| EB22 진행 상태 조회 | `GET /api/v1/cms/withdrawal-results/file-preview/{id}/status` · `/payment/cms-withdrawal-request` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/cmseb22/CmsEb22Controller.kt#L186) | `id: Long` → `success`, `data`, `error`, `totalCount`, `totalAmount`, `generateDtiCount`, `cmsSuccessCount`, `cmsSuccessAmount`, `dtiSuccessCount`, `dtiSuccessAmount`, `retryTargetCount`, `requestStarted` | `SmartBill3.dbo.CMS_EA22_DETAIL`, `SB_BILL.dbo.PAYMENT`, `SmartBill3.dbo.upCMS_SchRsltEA22`, `SmartBill3.dbo.CMS_EA22` |
| EB22 반영요청 | `POST /api/v1/cms/withdrawal-results/file-preview/{id}/request` · `/payment/cms-withdrawal-request` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/cmseb22/CmsEb22Controller.kt#L176) | `id: Long` → `success`, `data`, `error` | `SmartBill3.dbo.upCMS_UptEA22Dtl01`, `SmartBill3.dbo.upCMS_UptEA22Dtl02`, `SmartBill3.dbo.upCMS_UptEA22`, `SmartBill3.dbo.CMS_EA22`, `SmartBill3.dbo.CMS_EA22_DETAIL` 외 3개 · 정의에서 확인한 쓰기 `SmartBill3.dbo.CMS_EA22_DETAIL_CUB`, `SmartBill3.dbo.CMS_EA22` · 코드 연계 트랜잭션 |
| EB22 재요청 | `POST /api/v1/cms/withdrawal-results/file-preview/{id}/retry` · `/payment/cms-withdrawal-request` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/cmseb22/CmsEb22Controller.kt#L195) | `id: Long` → `success`, `data`, `error` | `SmartBill3.dbo.CMS_EA22_DETAIL`, `SmartBill3.dbo.upCMS_SchRsltEA22`, `SmartBill3.dbo.CMS_EA22`, `SB_COMMON.dbo.upSBAdm_GetDtiSupByrInfo`, `SB_DTI.dbo.upLink_GetDtiConfig` · 코드 연계 트랜잭션 |
| EB22 반영완료 | `POST /api/v1/cms/withdrawal-results/file-preview/{id}/commit` · `/payment/cms-withdrawal-request` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/cmseb22/CmsEb22Controller.kt#L205) | `id: Long` · `force: Boolean` → `success`, `data`, `error` | `SmartBill3.dbo.UPCMS_COMMITEB22`, `SmartBill3.dbo.CMS_EA22`, `SmartBill3.dbo.CMS_EA22_DETAIL`, `SB_BILL.dbo.PAYMENT`, `SmartBill3.dbo.upCMS_SchRsltEA22` · 정의에서 확인한 쓰기 `SmartBill3.dbo.CMS_EA22` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `SmartBill3.dbo.CMS_EA22` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmseb22/repository/Eb22Mapper.kt#L149) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-8cc8fe0c5cb8684a) |
| `SmartBill3.dbo.CMS_EA22_DETAIL` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM · 정의 참조 `SmartBill3.dbo.CMS_EA22_DETAIL_CUB`, `master.dbo.dec_char_sel_tc` · 하위 호출 `master.dbo.dec_char_sel_tc` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmseb22/repository/Eb22Mapper.kt#L219) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3d93e003ec253442) |
| `SB_BILL.dbo.PAYMENT` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmseb22/repository/Eb22Mapper.kt#L219) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-abdfd3b9c475faa0) |
| `SmartBill3.dbo.upCMS_SchRsltEA22` | @idx varchar(20), @ea22_idx varchar(20), @rslt_code char(1) | 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmseb22/repository/Eb22Mapper.kt#L292) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-fc64eb80739b5034) |
| `SmartBill3.dbo.upCMS_UptEA22Dtl01` | @EA22_IDX int, @PAYER_NO char(20), @RSLT_CODE char(1), @ERR_CODE varchar(4) | 정의 참조 `SmartBill3.dbo.CMS_EA22_DETAIL_CUB` · 정적 쓰기 `SmartBill3.dbo.CMS_EA22_DETAIL_CUB` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmseb22/repository/Eb22Mapper.kt#L374) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-c8edee1bbd3cd9b9) |
| `SmartBill3.dbo.upCMS_UptEA22Dtl02` | @EA22_IDX int | 정의 참조 `SmartBill3.dbo.CMS_EA22_DETAIL_CUB` · 정적 쓰기 `SmartBill3.dbo.CMS_EA22_DETAIL_CUB` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmseb22/repository/Eb22Mapper.kt#L383) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-1ed4fcf24a18ea45) |
| `SmartBill3.dbo.upCMS_UptEA22` | @IDX int, @PAY_CNT int, @PAY_AMT money | 정의 참조 `SmartBill3.dbo.CMS_EA21`, `SmartBill3.dbo.CMS_EA22`, `SmartBill3.dbo.CMS_EA22_DETAIL` · 정적 쓰기 `SmartBill3.dbo.CMS_EA22` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmseb22/repository/Eb22Mapper.kt#L387) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-5ae566acd9e21636) |
| `SB_COMMON.dbo.upSBAdm_GetDtiSupByrInfo` | @MEM_NO varchar(10), @COM_NO varchar(10) | 정의 참조 `SB_DTI.dbo.BIZPLACE`, `SB_DTI.dbo.BIZPLACE_MEMBER`, `SmartBill3.dbo.COMPANY`, `SB_DTI.dbo.DEPT_ADMIN`, `SB_DTI.dbo.DEPT_MEMBER` 외 2개 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmseb22/repository/Eb22Mapper.kt#L352) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-00da21345ef3178b) |
| `SB_DTI.dbo.upLink_GetDtiConfig` | @COM_NO int, @BP_CODE varchar(35) | 정의 참조 `SB_DTI.dbo.COMPANY_DTICONFIG` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmseb22/repository/Eb22Mapper.kt#L359) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-60b2773a1a961b4d) |
| `SmartBill3.dbo.UPCMS_COMMITEB22` | @EB22IDX int, @RESULT varchar(5) OUT | 정의 참조 `SmartBill3.dbo.CMS_EA22` · 정적 쓰기 `SmartBill3.dbo.CMS_EA22` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmseb22/repository/Eb22Mapper.kt#L395) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-76e7f5d222b86ef4) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | EB22 파일 번호, 미리보기, 반영 상태 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 서비스 현황 > 입금관리 > (EB21/EB22) CMS 자동이체 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/PaymentRoutes.tsx#L93) · [CmsWithdrawalPendingResultDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/CmsWithdrawalPendingResultDetailPage.tsx#L33) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/cmsWithdrawalResultApi.ts#L185) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/cmsWithdrawalResultApi.ts#L253) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/cmsWithdrawalResultApi.ts#L242) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/cmsWithdrawalResultApi.ts#L260) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/cmsWithdrawalResultApi.ts#L272) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 10개 중 개발 메타데이터 확인 10개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-0064a0d1ad68f7bc) | Demo 메타데이터 10/10개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

# [카페·SCM·사업장 운영] SCM 조회 메인 수정 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

선택한 SCM의 ID, 폐쇄 여부, 본·지사 통합 설정과 메인 주소를 변경한다. 통합을 사용하는 경우 관리지사를 지정한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 카페·SCM·사업장 운영 |
| 언제 사용하는가 | 통합 가능한 후보 지사 조회, 통합관리지사 조회, SCM 상세 조회, SCM ID 중복 확인, SCM 메인 정보 저장 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | SCM ID, 폐쇄 여부, 본/지사 통합 여부, 메인 주소, 통합관리지사 |
| 업무 흐름 | 통합 가능한 후보 지사 조회, 통합관리지사 조회, SCM 상세 조회, SCM ID 중복 확인, SCM 메인 정보 저장 |
| 이 페이지의 역할 | 메인 수정 · SCM 메인 정보 저장 |
| 판단 결과·다음 업무 | [SCM 조회](scm.md) |
| 다른 화면과의 구분 | SB 서비스관리 > SCM > SCM 조회에서 사용하는 메인 수정 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 선택한 SCM의 ID, 폐쇄 여부, 본·지사 통합 설정과 메인 주소를 변경한다. 통합을 사용하는 경우 관리지사를 지정한다. |
| 메뉴·화면 경로 | SB 서비스관리 > SCM > SCM 조회 · `/smartbill-scm/scm/main-edit/:id` · 경로 변수 `id` |
| 화면 유형·담당 | 메인 수정 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [SCM 조회](scm.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/smartbill-scm/scm` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `id` |
| 통합 가능한 후보 지사 조회 | `/smartbill-scm/scm` `VIEW` | `scmId: String` |
| 통합관리지사 조회 | `/smartbill-scm/scm` `VIEW` | `scmId: String` |
| SCM 상세 조회 | `/smartbill-scm/scm` `VIEW` | `scmId: String` |
| SCM ID 중복 확인 | `/smartbill-scm/scm` `VIEW` | `scmId: String` |
| SCM 메인 정보 저장 | `/smartbill-scm/scm` `PROCESS` | `scmId: String` · `ScmMainUpdateRequest` `scmId`, `isIntegrated`, `isClosed`, `mainUrl`, `integratedBranchComNos` · 서버 필수 `scmId` |

코드에서 확인한 버튼·작업명은 **중복확인**, **▸ 추가하기**, **◂ 삭제하기**, **저장**, **목록**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. SCM 조회에서 대상을 선택해 **메인 수정**을 연다. 회사명, 사업자번호와 현재 SCM ID를 확인한다.
2. SCM ID를 바꾸는 경우 **중복확인**으로 확인한다. **폐쇄 여부**와 **본/지사 통합 여부**를 검토한다.
3. 통합으로 설정한 경우 추가 가능한 지사에서 **추가하기**를 사용해 **통합관리지사**를 한 곳 이상 지정한다. 목록에서 제외할 때는 **삭제하기**를 사용한다.
4. 메인 주소와 통합관리지사를 확인한 뒤 **저장**한다. **저장되었습니다** 메시지 뒤 SCM 조회 목록으로 돌아간다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `id` |
| 회사명 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/ScmMainEditPage.tsx#L266) |
| 사업자번호 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/ScmMainEditPage.tsx#L267) |
| 관리지명 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/ScmMainEditPage.tsx#L268) |
| 폐쇄 여부 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/ScmMainEditPage.tsx#L301) |
| 본/지사 통합 여부 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/ScmMainEditPage.tsx#L318) |
| 개별 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/ScmMainEditPage.tsx#L339) |
| 통합 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/ScmMainEditPage.tsx#L343) |
| * 지사 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/ScmMainEditPage.tsx#L355) |
| * 통합관리지사 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/ScmMainEditPage.tsx#L381) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 통합 가능한 후보 지사 조회 | `GET /api/v1/smartbill-scm/scms/{scmId}/branches/available` · `/smartbill-scm/scm` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/smartbillscm/scmlookup/ScmLookupController.kt#L103) | `scmId: String` → `success`, `data`, `error`, `id`, `companyName`, `businessNumber` | `smartwork.dbo.usp_scm_available_branch_select`, `SmartBill3.dbo.upAdm_ScmMain_View` |
| 통합관리지사 조회 | `GET /api/v1/smartbill-scm/scms/{scmId}/branches/integrated-managers` · `/smartbill-scm/scm` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/smartbillscm/scmlookup/ScmLookupController.kt#L115) | `scmId: String` → `success`, `data`, `error`, `id`, `companyName`, `businessNumber` | `smartwork.dbo.usp_scm_integrated_branch_select` |
| SCM 상세 조회 | `GET /api/v1/smartbill-scm/scms/{scmId}` · `/smartbill-scm/scm` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/smartbillscm/scmlookup/ScmLookupController.kt#L88) | `scmId: String` → `success`, `data`, `error`, `scmId`, `companyName`, `businessNumber`, `representativeName`, `isIntegrated`, `isClosed`, `mainUrl` | `SmartBill3.dbo.upAdm_ScmMain_View` |
| SCM ID 중복 확인 | `GET /api/v1/smartbill-scm/scms/check-duplicate` · `/smartbill-scm/scm` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/smartbillscm/scmlookup/ScmLookupController.kt#L73) | `scmId: String` → `success`, `data`, `error`, `scmId`, `available` | `SmartBill3.dbo.upCafe_DupCafeID01` |
| SCM 메인 정보 저장 | `PUT /api/v1/smartbill-scm/scms/{scmId}` · `/smartbill-scm/scm` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/smartbillscm/scmlookup/ScmLookupController.kt#L130) | `scmId: String` · `ScmMainUpdateRequest` `scmId`, `isIntegrated`, `isClosed`, `mainUrl`, `integratedBranchComNos` · 서버 필수 `scmId` → `success`, `data`, `error` | `SmartBill3.dbo.upCafe_DelTaxBranch`, `SmartBill3.dbo.upADM_ScmMain_Save`, `SmartBill3.dbo.upAdm_ScmBranch_Save`, `SmartBill3.dbo.upAdm_ScmMain_View` · 정의에서 확인한 쓰기 `SmartBill3.dbo.TAX_BRANCH`, `SmartBill3.dbo.TAX_MAIN`, `SmartBill3.dbo.TAX_ADMIN`, `SmartBill3.dbo.TAX_MENU` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.usp_scm_available_branch_select` | @com_no int, @cafe_id varchar(15) | 정의 참조 `SmartBill3.dbo.COMPANY`, `SmartBill3.dbo.COMPANY_BRANCH`, `SmartBill3.dbo.TAX_BRANCH` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/smartbillscm/scmlookup/repository/ScmLookupMapper.kt#L94) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-6c114a06b20bb938) |
| `SmartBill3.dbo.upAdm_ScmMain_View` | @scm_id varchar(15) | 정의 참조 `SmartBill3.dbo.COMPANY`, `SmartBill3.dbo.MEMBER`, `SmartBill3.dbo.SCM_SUB_IMAGE`, `SmartBill3.dbo.TAX_ADMIN`, `SmartBill3.dbo.TAX_MAIN` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/smartbillscm/scmlookup/repository/ScmLookupMapper.kt#L70) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-57bf8898c999bd23) |
| `smartwork.dbo.usp_scm_integrated_branch_select` | @cafe_id varchar(15) | 정의 참조 `SmartBill3.dbo.COMPANY`, `SmartBill3.dbo.TAX_BRANCH` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/smartbillscm/scmlookup/repository/ScmLookupMapper.kt#L82) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-0230396428862ddd) |
| `SmartBill3.dbo.upCafe_DupCafeID01` | @cafe_id varchar(15) | 정의 참조 `SmartBill3.dbo.TAX_MAIN`, `SmartBill3.dbo.TAX_MAIN_TEMP` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/smartbillscm/scmlookup/repository/ScmLookupMapper.kt#L107) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-34e043b29f849277) |
| `SmartBill3.dbo.upCafe_DelTaxBranch` | @cafe_id varchar(15) | 정의 참조 `SmartBill3.dbo.TAX_BRANCH` · 정적 쓰기 `SmartBill3.dbo.TAX_BRANCH` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/smartbillscm/scmlookup/repository/ScmLookupMapper.kt#L112) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-7cb12e1eeded6911) |
| `SmartBill3.dbo.upADM_ScmMain_Save` | @mod varchar(3), @scm_no int, @scm_id varchar(15), @total_yn varchar(1), @com_no int, @shut_yn varchar(1), @mem_no int, @main_url varchar(100) | 정의 참조 `SmartBill3.dbo.TAX_ADMIN`, `SmartBill3.dbo.TAX_MAIN`, `SmartBill3.dbo.TAX_MENU` · 정적 쓰기 `SmartBill3.dbo.TAX_MAIN`, `SmartBill3.dbo.TAX_ADMIN`, `SmartBill3.dbo.TAX_MENU` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/smartbillscm/scmlookup/repository/ScmLookupMapper.kt#L123) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-00164905f80662da) |
| `SmartBill3.dbo.upAdm_ScmBranch_Save` | @cafe_id varchar(15), @mem_no int, @com_no int | 정의 참조 `SmartBill3.dbo.TAX_BRANCH` · 정적 쓰기 `SmartBill3.dbo.TAX_BRANCH` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/smartbillscm/scmlookup/repository/ScmLookupMapper.kt#L128) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-69b06f41798311dd) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | SCM ID, 폐쇄 여부, 본/지사 통합 여부, 메인 주소, 통합관리지사 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 서비스관리 > SCM > SCM 조회의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 업체 ID가 없습니다 | SCM ID, 폐쇄 여부, 본/지사 통합 여부, 메인 주소, 통합관리지사 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 데이터를 불러올 수 없습니다 | SCM ID, 폐쇄 여부, 본/지사 통합 여부, 메인 주소, 통합관리지사 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 현재 사용 중인 SCM ID입니다 | SCM ID, 폐쇄 여부, 본/지사 통합 여부, 메인 주소, 통합관리지사 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 이미 사용 중인 SCM ID입니다 | SCM ID, 폐쇄 여부, 본/지사 통합 여부, 메인 주소, 통합관리지사 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/SmartbillScmRoutes.tsx#L14) · [ScmMainEditPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/ScmMainEditPage.tsx#L41) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/api/sbScmApi.ts#L206) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/api/sbScmApi.ts#L218) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/api/sbScmApi.ts#L98) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/api/sbScmApi.ts#L108) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/api/sbScmApi.ts#L121) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 7개 중 개발 메타데이터 확인 7개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-f2f49d6d0c5c721b) | Demo 메타데이터 7/7개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

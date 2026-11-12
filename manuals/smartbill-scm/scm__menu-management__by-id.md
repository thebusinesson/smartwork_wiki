# [카페·SCM·사업장 운영] SCM 조회 메뉴 관리 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

선택한 SCM이 제공하는 메뉴와 메뉴별 설정을 관리한다. SCM 기본정보와 메뉴의 저장 범위를 구분한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 카페·SCM·사업장 운영 |
| 언제 사용하는가 | SCM 상세 조회, SCM 메뉴 목록 조회, SCM 메뉴 삭제, SCM 메뉴 일괄 저장 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | SCM 식별자, 메뉴 목록과 설정 |
| 업무 흐름 | SCM 상세 조회, SCM 메뉴 목록 조회, SCM 메뉴 삭제, SCM 메뉴 일괄 저장 |
| 이 페이지의 역할 | 메뉴 관리 · SCM 메뉴 일괄 저장 |
| 판단 결과·다음 업무 | [SCM 조회](scm.md) |
| 다른 화면과의 구분 | SB 서비스관리 > SCM > SCM 조회에서 사용하는 메뉴 관리 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 삭제 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/ScmMenuManagementPage.tsx#L349) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 선택한 SCM이 제공하는 메뉴와 메뉴별 설정을 관리한다. SCM 기본정보와 메뉴의 저장 범위를 구분한다. |
| 메뉴·화면 경로 | SB 서비스관리 > SCM > SCM 조회 · `/smartbill-scm/scm/menu-management/:id` · 경로 변수 `id` |
| 화면 유형·담당 | 메뉴 관리 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [SCM 조회](scm.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/smartbill-scm/scm` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `id` |
| SCM 상세 조회 | `/smartbill-scm/scm` `VIEW` | `scmId: String` |
| SCM 메뉴 목록 조회 | `/smartbill-scm/scm` `VIEW` | `scmId: String` |
| SCM 메뉴 삭제 | `/smartbill-scm/scm` `DELETE` | `scmId: String` · `menuId: Long` |
| SCM 메뉴 일괄 저장 | `/smartbill-scm/scm` `PROCESS` | `scmId: String` · `ScmMenuSaveRequest` `menus` |

코드에서 확인한 버튼·작업명은 **삭제**, **메뉴 추가**, **저장**, **목록**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [SCM 조회](scm.md)에서 대상 또는 작업을 선택한다. `/smartbill-scm/scm/menu-management/:id`에서 이전 화면이 전달한 `id`와 현재 대상을 확인한다.
2. **SCM 메뉴 일괄 저장**을 실행하기 전에 변경 대상과 입력값을 확인한다. 처리 응답을 확인하고 관련 조회에서 대상의 상태를 확인한다.
3. 후속 조회나 목록 복귀가 필요하면 [SCM 조회](scm.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `id` |
| 회사명 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/ScmMenuManagementPage.tsx#L198) |
| 사업자번호 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/ScmMenuManagementPage.tsx#L199) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| SCM 상세 조회 | `GET /api/v1/smartbill-scm/scms/{scmId}` · `/smartbill-scm/scm` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/smartbillscm/scmlookup/ScmLookupController.kt#L88) | `scmId: String` → `success`, `data`, `error`, `scmId`, `companyName`, `businessNumber`, `representativeName`, `isIntegrated`, `isClosed`, `mainUrl` | `SmartBill3.dbo.upAdm_ScmMain_View` |
| SCM 메뉴 목록 조회 | `GET /api/v1/smartbill-scm/scms/{scmId}/menus` · `/smartbill-scm/scm` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/smartbillscm/scmlookup/ScmLookupController.kt#L144) | `scmId: String` → `success`, `data`, `error`, `id`, `rank`, `menuName`, `menuKind`, `procId`, `titleImg`, `tableBorderColor`, `fontColor`, `tableBgColor` | `SmartBill3.dbo.upAdm_ScmMenu_View` |
| SCM 메뉴 삭제 | `DELETE /api/v1/smartbill-scm/scms/{scmId}/menus/{menuId}` · `/smartbill-scm/scm` `DELETE` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/smartbillscm/scmlookup/ScmLookupController.kt#L178) | `scmId: String` · `menuId: Long` → `success`, `data`, `error` | `SmartBill3.dbo.upAdm_ScmMenu_Delete` · 정의에서 확인한 쓰기 `SmartBill3.dbo.TAX_MENU`, `SmartBill3.dbo.TAX_USE` · 코드 연계 트랜잭션 |
| SCM 메뉴 일괄 저장 | `PUT /api/v1/smartbill-scm/scms/{scmId}/menus` · `/smartbill-scm/scm` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/smartbillscm/scmlookup/ScmLookupController.kt#L161) | `scmId: String` · `ScmMenuSaveRequest` `menus` → `success`, `data`, `error` | `SmartBill3.dbo.upADM_ScmMenu_Save` · 정의에서 확인한 쓰기 `SmartBill3.dbo.TAX_MENU`, `SmartBill3.dbo.SCM_MENU_IMAGE` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `SmartBill3.dbo.upAdm_ScmMain_View` | @scm_id varchar(15) | 정의 참조 `SmartBill3.dbo.COMPANY`, `SmartBill3.dbo.MEMBER`, `SmartBill3.dbo.SCM_SUB_IMAGE`, `SmartBill3.dbo.TAX_ADMIN`, `SmartBill3.dbo.TAX_MAIN` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/smartbillscm/scmlookup/repository/ScmLookupMapper.kt#L70) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-57bf8898c999bd23) |
| `SmartBill3.dbo.upAdm_ScmMenu_View` | @scm_id varchar(15) | 정의 참조 `SmartBill3.dbo.SCM_MENU_IMAGE`, `SmartBill3.dbo.TAX_MENU` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/smartbillscm/scmlookup/repository/ScmLookupMapper.kt#L146) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-aa1b78a93d5f1470) |
| `SmartBill3.dbo.upAdm_ScmMenu_Delete` | @menu_no int | 정의 참조 `SmartBill3.dbo.TAX_MENU`, `SmartBill3.dbo.TAX_USE` · 정적 쓰기 `SmartBill3.dbo.TAX_MENU`, `SmartBill3.dbo.TAX_USE` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/smartbillscm/scmlookup/repository/ScmLookupMapper.kt#L163) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-e221845510d4f4eb) |
| `SmartBill3.dbo.upADM_ScmMenu_Save` | @scm_id varchar(15), @menu_no int, @menu_name varchar(30), @menu_kind varchar(1), @menu_rank int, @proc_id varchar(10), @title_img varchar(100), @border varchar(50), @font varchar(50), @bg varchar(50) | 정의 참조 `SmartBill3.dbo.SCM_MENU_IMAGE`, `SmartBill3.dbo.TAX_MENU` · 정적 쓰기 `SmartBill3.dbo.TAX_MENU`, `SmartBill3.dbo.SCM_MENU_IMAGE` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/smartbillscm/scmlookup/repository/ScmLookupMapper.kt#L158) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-617c1b1d77805a78) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | SCM 식별자, 메뉴 목록과 설정 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 서비스관리 > SCM > SCM 조회의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 업체 ID가 없습니다 | SCM 식별자, 메뉴 목록과 설정 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/SmartbillScmRoutes.tsx#L15) · [ScmMenuManagementPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/ScmMenuManagementPage.tsx#L31) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/api/sbScmApi.ts#L98) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/api/sbScmApi.ts#L133) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/api/sbScmApi.ts#L169) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/api/sbScmApi.ts#L158) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 4개 중 개발 메타데이터 확인 4개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-381feee9678ec824) | Demo 메타데이터 4/4개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

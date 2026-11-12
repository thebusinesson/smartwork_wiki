# [카페·SCM·사업장 운영] SCM 조회 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

업체조건(SCM ID/사업자번호/회사명)/본·지사 통합여부/폐쇄여부 조건으로 SCM 목록을 페이징 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 카페·SCM·사업장 운영 |
| 언제 사용하는가 | SCM 목록 조회 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 회사명, 사업자번호, 본/지사 통합, 폐쇄여부, 업체 조건, 전체 |
| 업무 흐름 | SCM 목록 조회 |
| 이 페이지의 역할 | 조회 · SCM 목록 조회 |
| 판단 결과·다음 업무 | [SCM 조회 메인 수정](scm__main-edit__by-id.md) · [SCM 조회 메뉴 관리](scm__menu-management__by-id.md) · [SCM 조회 디자인 관리](scm__design-management__by-id.md) |
| 다른 화면과의 구분 | 이 경로에서 볼 수 있는 조건·결과를 기준으로 사용한다. 독립 경로의 상세·등록은 관련 화면에 연결한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 업체조건(SCM ID/사업자번호/회사명)/본·지사 통합여부/폐쇄여부 조건으로 SCM 목록을 페이징 조회한다. |
| 메뉴·화면 경로 | SB 서비스관리 > SCM > SCM 조회 · `/smartbill-scm/scm` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [SCM 조회 메인 수정](scm__main-edit__by-id.md) · [SCM 조회 메뉴 관리](scm__menu-management__by-id.md) · [SCM 조회 디자인 관리](scm__design-management__by-id.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/smartbill-scm/scm` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| SCM 목록 조회 | `/smartbill-scm/scm` `VIEW` | `ScmSearchRequest` `page`, `size`, `vendorSearchType`, `vendorValue`, `integrationStatus`, `closureStatus` |

코드에서 확인한 버튼·작업명은 **검색**, **메인 수정**, **메뉴 관리**, **메인 디자인 관리**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **SB 서비스관리 > SCM > SCM 조회**를 연다. `/smartbill-scm/scm`를 연다.
2. **업체 조건**, **전체**, **본/지사 통합여부** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색** 중 해당 버튼을 선택한다.
3. **SCM 목록 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [SCM 조회 메인 수정](scm__main-edit__by-id.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 회사명 | 출력 | 조회 응답 기준 | 화면 필드 `companyName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/ScmLookupPage.tsx#L186) |
| 사업자번호 | 출력 | 조회 응답 기준 | 화면 필드 `businessNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/ScmLookupPage.tsx#L189) |
| 본/지사 통합 | 출력 | 조회 응답 기준 | 화면 필드 `isIntegrated` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/ScmLookupPage.tsx#L196) |
| 폐쇄여부 | 출력 | 조회 응답 기준 | 화면 필드 `isClosed` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/ScmLookupPage.tsx#L203) |
| 업체 조건 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/ScmLookupPage.tsx#L35) |
| 전체 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `all` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/ScmLookupPage.tsx#L78) |
| 본/지사 통합여부 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/ScmLookupPage.tsx#L58) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| SCM 목록 조회 | `GET /api/v1/smartbill-scm/scms` · `/smartbill-scm/scm` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/smartbillscm/scmlookup/ScmLookupController.kt#L60) | `ScmSearchRequest` `page`, `size`, `vendorSearchType`, `vendorValue`, `integrationStatus`, `closureStatus` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `currentPage`, `size` | `smartwork.dbo.usp_scm_list_select` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.usp_scm_list_select` | @PAGE int = 1, @PAGE_SIZE int = 10, @schType char(1), @schText varchar(200), @totalYn char(1), @shutYn char(1) | 정의 참조 `SmartBill3.dbo.COMPANY`, `SmartBill3.dbo.TAX_MAIN` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/smartbillscm/scmlookup/repository/ScmLookupMapper.kt#L47) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-938f48ab2ea777f9) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 회사명, 사업자번호, 본/지사 통합, 폐쇄여부, 업체 조건, 전체 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 서비스관리 > SCM > SCM 조회의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 업체를 선택하세요 | 회사명, 사업자번호, 본/지사 통합, 폐쇄여부, 업체 조건, 전체 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 검색 결과가 없습니다. | 회사명, 사업자번호, 본/지사 통합, 폐쇄여부, 업체 조건, 전체 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/SmartbillScmRoutes.tsx#L13) · [ScmLookupPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/ScmLookupPage.tsx#L94) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/smartbillscm/api/sbScmApi.ts#L90) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 1개 중 개발 메타데이터 확인 1개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-a5283fb187b722d7) | Demo 메타데이터 1/1개 확인 · 2026-11-11 |
| 화면 재현 | [로컬 Playwright 표본](../../evidence/browser/all-pages-sample-2026-11-11.json) | 진입 및 표시 확인 · 표시 SCM 조회 · 2026-11-11 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

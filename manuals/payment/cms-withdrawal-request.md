# [CMS·카드 자동결제와 예외] (EB21/EB22) CMS 자동이체 관리 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

CMS 출금 요청 파일(EB21)과 금융기관의 처리 결과 파일(EB22)을 관리한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | CMS·카드 자동결제와 예외 |
| 언제 사용하는가 | EB21 목록 조회, EB22 목록 조회, EB21 파일 다운로드, EB21 전송 확인, EB21 삭제 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | EB21 요청 파일, EB22 결과 파일 |
| 업무 흐름 | EB21 목록 조회, EB22 목록 조회, EB21 파일 다운로드, EB21 전송 확인, EB21 삭제 |
| 이 페이지의 역할 | 조회·관리 · EB21 목록 조회 |
| 판단 결과·다음 업무 | [(EB21/EB22) CMS 자동이체 관리 조회](cms-withdrawal-request__eb21__apply.md) · [(EB21/EB22) CMS 자동이체 관리 상세](cms-withdrawal-request__eb21__by-id.md) · [(EB21/EB22) CMS 자동이체 관리 신청 정보](cms-withdrawal-request__eb22__by-id__application.md) · [(EB21/EB22) CMS 자동이체 관리 등록](cms-withdrawal-request__eb22__upload__by-ea21Idx__new.md) · [(EB21/EB22) CMS 자동이체 관리 처리 결과](cms-withdrawal-request__eb22__by-id__result.md) · [(EB21/EB22) CMS 자동이체 관리 상세](cms-withdrawal-request__eb22__file__by-eb22Idx.md) · [(EB21/EB22) CMS 자동이체 관리 상세](cms-withdrawal-request__eb22__file-preview__by-eb22Idx.md) |
| 다른 화면과의 구분 | 이 경로에서 볼 수 있는 조건·결과를 기준으로 사용한다. 독립 경로의 상세·등록은 관련 화면에 연결한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 확인 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CmsWithdrawalRequestTable.tsx#L262) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | CMS 출금 요청 파일(EB21)과 금융기관의 처리 결과 파일(EB22)을 관리한다. |
| 메뉴·화면 경로 | 서비스 현황 > 입금관리 > (EB21/EB22) CMS 자동이체 관리 · `/payment/cms-withdrawal-request` |
| 화면 유형·담당 | 조회·관리 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [(EB21/EB22) CMS 자동이체 관리 조회](cms-withdrawal-request__eb21__apply.md) · [(EB21/EB22) CMS 자동이체 관리 상세](cms-withdrawal-request__eb21__by-id.md) · [(EB21/EB22) CMS 자동이체 관리 신청 정보](cms-withdrawal-request__eb22__by-id__application.md) · [(EB21/EB22) CMS 자동이체 관리 등록](cms-withdrawal-request__eb22__upload__by-ea21Idx__new.md) · [(EB21/EB22) CMS 자동이체 관리 처리 결과](cms-withdrawal-request__eb22__by-id__result.md) · [(EB21/EB22) CMS 자동이체 관리 상세](cms-withdrawal-request__eb22__file__by-eb22Idx.md) · [(EB21/EB22) CMS 자동이체 관리 상세](cms-withdrawal-request__eb22__file-preview__by-eb22Idx.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/payment/cms-withdrawal-request` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| EB21 목록 조회 | `/payment/cms-withdrawal-request` `VIEW` | `Eb21SearchRequest` `invoiceMonth` |
| EB22 목록 조회 | `/payment/cms-withdrawal-request` `VIEW` | `Eb22SearchRequest` `billingYearMonth`, `transferRequestDate`, `page`, `size` |
| EB21 파일 다운로드 | `/payment/cms-withdrawal-request` `VIEW` | `idx: Long` · `fileName: String` · `createdDate: String` |
| EB21 전송 확인 | `/payment/cms-withdrawal-request` `PROCESS` | `Eb21SendConfirmRequest` `idx` |
| EB21 삭제 | `/payment/cms-withdrawal-request` `DELETE` | `idx: Long` |

코드에서 확인한 버튼·작업명은 **출금신청(EB21)**, **출금신청 결과(EB22)**, **검색**, **출금신청 생성**, **확인**, **다운로드**, **업로드**, **파일반영**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **서비스 현황 > 입금관리 > (EB21/EB22) CMS 자동이체 관리**를 연다. `/payment/cms-withdrawal-request`를 연다.
2. **청구년월** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색**, **확인**, **다운로드** 중 해당 버튼을 선택한다.
3. **EB21 목록 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [(EB21/EB22) CMS 자동이체 관리 조회](cms-withdrawal-request__eb21__apply.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 청구년월 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/CmsWithdrawalRequestListPage.tsx#L72) |
| 이체의뢰일 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | API 요청 `createdDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CmsWithdrawalRequestTable.tsx#L156) |
| 파일명 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | API 요청 `fileName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CmsWithdrawalRequestTable.tsx#L159) |
| 업체수 | 출력 | 조회 응답 기준 | 화면 필드 `payCountFormatted` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CmsWithdrawalRequestTable.tsx#L170) |
| 금액 | 출력 | 조회 응답 기준 | 화면 필드 `payAmountFormatted` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CmsWithdrawalRequestTable.tsx#L171) |
| 전송여부 | 출력 | 조회 응답 기준 | 화면 필드 `sendYn` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CmsWithdrawalRequestTable.tsx#L174) |
| 비고 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | API 요청 `idx` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CmsWithdrawalRequestTable.tsx#L193) |
| 이체요청일 | 출력 | 조회 응답 기준 | 화면 필드 `transferResultDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CmsWithdrawalResultTable.tsx#L22) |
| 결과반영여부 | 출력 | 조회 응답 기준 | 화면 필드 `writeYn` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CmsWithdrawalResultTable.tsx#L31) |
| 오류업체수 | 출력 | 조회 응답 기준 | 화면 필드 `errorCompanyCount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CmsWithdrawalResultTable.tsx#L32) |
| 오류금액 | 출력 | 조회 응답 기준 | 화면 필드 `errorAmount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CmsWithdrawalResultTable.tsx#L33) |
| 신청정보 | 출력 | 조회 응답 기준 | 화면 필드 `applicationInfo` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CmsWithdrawalResultTable.tsx#L23) |
| 결과정보 | 출력 | 조회 응답 기준 | 화면 필드 `resultInfo` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CmsWithdrawalResultTable.tsx#L24) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| EB21 목록 조회 | `GET /api/v1/payment/cms-auto-transfer/eb21` · `/payment/cms-withdrawal-request` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/cmseb21/CmsEb21Controller.kt#L59) | `Eb21SearchRequest` `invoiceMonth` → `success`, `data`, `error`, `content`, `totalElements` | `SmartBill3.dbo.upCMS_Lst_EA21` · 코드 연계 트랜잭션 |
| EB22 목록 조회 | `GET /api/v1/cms/withdrawal-results` · `/payment/cms-withdrawal-request` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/cmseb22/CmsEb22Controller.kt#L70) | `Eb22SearchRequest` `billingYearMonth`, `transferRequestDate`, `page`, `size` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `currentPage`, `size` | `SmartBill3.dbo.CMS_EA21`, `SmartBill3.dbo.CMS_EA22` · 코드 연계 트랜잭션 |
| EB21 파일 다운로드 | `GET /api/v1/payment/cms-auto-transfer/eb21/{idx}/download` · `/payment/cms-withdrawal-request` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/cmseb21/CmsEb21Controller.kt#L243) | `idx: Long` · `fileName: String` · `createdDate: String` → 파일 또는 오류 응답 | 직접 DB 호출이 연결된 경로는 현재 소스에서 미확인. 세부 저장소는 Controller와 Service 참조. |
| EB21 전송 확인 | `POST /api/v1/payment/cms-auto-transfer/eb21/send-confirm` · `/payment/cms-withdrawal-request` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/cmseb21/CmsEb21Controller.kt#L172) | `Eb21SendConfirmRequest` `idx` → `success`, `data`, `error`, `message` | `SmartBill3.dbo.upCMS_Sav_EA21Status` · 정의에서 확인한 쓰기 `SmartBill3.dbo.CMS_EA21` · 코드 연계 트랜잭션 |
| EB21 삭제 | `DELETE /api/v1/payment/cms-auto-transfer/eb21/{idx}` · `/payment/cms-withdrawal-request` `DELETE` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/cmseb21/CmsEb21Controller.kt#L189) | `idx: Long` → `success`, `data`, `error` | `SmartBill3.dbo.CMS_EA21`, `SmartBill3.dbo.upCMS_Del_EA21` · 정의에서 확인한 쓰기 `SmartBill3.dbo.CMS_EA21_DETAIL_CUB`, `SmartBill3.dbo.CMS_EA21` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `SmartBill3.dbo.upCMS_Lst_EA21` | @yymm varchar(6) | 정의 참조 `SmartBill3.dbo.CMS_EA21` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmseb21/repository/Eb21Mapper.kt#L40) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-e0af4947735fcb93) |
| `SmartBill3.dbo.CMS_EA21` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmseb22/repository/Eb22Mapper.kt#L83) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-6dbbeb540f7fb742) |
| `SmartBill3.dbo.CMS_EA22` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmseb22/repository/Eb22Mapper.kt#L83) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-8cc8fe0c5cb8684a) |
| `SmartBill3.dbo.upCMS_Sav_EA21Status` | @EA21_IDX int | 정의 참조 `SmartBill3.dbo.CMS_EA21` · 정적 쓰기 `SmartBill3.dbo.CMS_EA21` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmseb21/repository/Eb21Mapper.kt#L118) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-f8e70947dea59629) |
| `SmartBill3.dbo.upCMS_Del_EA21` | @IDX int | 정의 참조 `SmartBill3.dbo.CMS_EA21`, `SmartBill3.dbo.CMS_EA21_DETAIL_CUB` · 정적 쓰기 `SmartBill3.dbo.CMS_EA21_DETAIL_CUB`, `SmartBill3.dbo.CMS_EA21` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmseb21/repository/Eb21Mapper.kt#L122) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-7e807a5e271f85d2) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | EB21 요청 파일, EB22 결과 파일 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 서비스 현황 > 입금관리 > (EB21/EB22) CMS 자동이체 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 다운로드 중 오류가 발생했습니다. | EB21 요청 파일, EB22 결과 파일 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 생성된 파일을 목록에서 찾지 못했습니다. 조회 조건을 확인해 주세요. | EB21 요청 파일, EB22 결과 파일 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 삭제 처리에 실패했습니다. | EB21 요청 파일, EB22 결과 파일 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 파일 다운로드에 실패했습니다. | EB21 요청 파일, EB22 결과 파일 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/PaymentRoutes.tsx#L87) · [CmsWithdrawalRequestPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/CmsWithdrawalRequestPage.tsx#L10) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/cmsWithdrawalRequestApi.ts#L34) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/cmsWithdrawalResultApi.ts#L111) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/cmsWithdrawalRequestApi.ts#L69) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/cmsWithdrawalRequestApi.ts#L111) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/cmsWithdrawalRequestApi.ts#L120) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 5개 중 개발 메타데이터 확인 5개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-ac534961a73cbb15) | Demo 메타데이터 5/5개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

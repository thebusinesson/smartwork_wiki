# [CMS·카드 자동결제와 예외] (EB21/EB22) CMS 자동이체 관리 등록 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

EB22 신규 결과 파일을 업로드한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | CMS·카드 자동결제와 예외 |
| 언제 사용하는가 | EB22 업로드 정보 조회, EB22 파일 업로드 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 파일, 대상 파일명 |
| 업무 흐름 | EB22 업로드 정보 조회, EB22 파일 업로드 |
| 이 페이지의 역할 | 등록 · EB22 파일 업로드 |
| 판단 결과·다음 업무 | [(EB21/EB22) CMS 자동이체 관리](cms-withdrawal-request.md) |
| 다른 화면과의 구분 | 서비스 현황 > 입금관리 > (EB21/EB22) CMS 자동이체 관리에서 사용하는 등록 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | EB22 신규 결과 파일을 업로드한다. |
| 메뉴·화면 경로 | 서비스 현황 > 입금관리 > (EB21/EB22) CMS 자동이체 관리 · `/payment/cms-withdrawal-request/eb22/upload/:ea21Idx/new` · 경로 변수 `ea21Idx` |
| 화면 유형·담당 | 등록 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [(EB21/EB22) CMS 자동이체 관리](cms-withdrawal-request.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/payment/cms-withdrawal-request` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `ea21Idx` |
| EB22 업로드 정보 조회 | `/payment/cms-withdrawal-request` `VIEW` | `ea21Idx: Long` |
| EB22 파일 업로드 | `/payment/cms-withdrawal-request` `PROCESS` | `ea21Idx: Long` · `file: MultipartFile` |

코드에서 확인한 버튼·작업명은 **목록**, **출금신청(EB21)**, **출금결과 반영(EB22)**, **찾아보기**, **저장**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [(EB21/EB22) CMS 자동이체 관리](cms-withdrawal-request.md)에서 대상 또는 작업을 선택한다. `/payment/cms-withdrawal-request/eb22/upload/:ea21Idx/new`에서 이전 화면이 전달한 `ea21Idx`와 현재 대상을 확인한다.
2. **파일**, **대상 파일명** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **저장** 중 해당 버튼을 선택한다.
3. **EB22 파일 업로드**을 실행하기 전에 변경 대상과 입력값을 확인한다. 표시되는 **파일 업로드가 완료되었습니다.** 메시지와 대상 상태를 확인한다.
4. 후속 조회나 목록 복귀가 필요하면 [(EB21/EB22) CMS 자동이체 관리](cms-withdrawal-request.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `ea21Idx` |
| 파일 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CmsAccountEb14UploadForm.tsx#L55) |
| 대상 파일명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/CmsWithdrawalUploadRequiredPage.tsx#L106) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| EB22 업로드 정보 조회 | `GET /api/v1/cms/withdrawal-results/upload/{ea21Idx}` · `/payment/cms-withdrawal-request` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/cmseb22/CmsEb22Controller.kt#L124) | `ea21Idx: Long` → `success`, `data`, `error`, `ea21Idx`, `eb21FileName`, `transferRequestDate` | `SmartBill3.dbo.CMS_EA21`, `SmartBill3.dbo.CMS_EA22` |
| EB22 파일 업로드 | `POST /api/v1/cms/withdrawal-results/upload/{ea21Idx}` · `/payment/cms-withdrawal-request` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/cmseb22/CmsEb22Controller.kt#L134) | `ea21Idx: Long` · `file: MultipartFile` → `success`, `data`, `error` | `SmartBill3.dbo.upCMS_SavEA22`, `SmartBill3.dbo.CMS_EA21`, `SmartBill3.dbo.CMS_EA22` · 정의에서 확인한 쓰기 `SmartBill3.dbo.CMS_EA22`, `SmartBill3.dbo.CMS_EA22_DETAIL_CUB` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `SmartBill3.dbo.CMS_EA21` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmseb22/repository/Eb22Mapper.kt#L132) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-6dbbeb540f7fb742) |
| `SmartBill3.dbo.CMS_EA22` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmseb22/repository/Eb22Mapper.kt#L132) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-8cc8fe0c5cb8684a) |
| `SmartBill3.dbo.upCMS_SavEA22` | @FILENAME varchar(8) | 정의 참조 `SmartBill3.dbo.CMS_EA21`, `SmartBill3.dbo.CMS_EA21_DETAIL_CUB`, `SmartBill3.dbo.CMS_EA22`, `SmartBill3.dbo.CMS_EA22_DETAIL_CUB` · 정적 쓰기 `SmartBill3.dbo.CMS_EA22`, `SmartBill3.dbo.CMS_EA22_DETAIL_CUB` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmseb22/repository/Eb22Mapper.kt#L366) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-fe3b1b194aa2519d) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 파일, 대상 파일명 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 서비스 현황 > 입금관리 > (EB21/EB22) CMS 자동이체 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/PaymentRoutes.tsx#L94) · [CmsWithdrawalUploadRequiredPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/CmsWithdrawalUploadRequiredPage.tsx#L15) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/cmsWithdrawalResultApi.ts#L171) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/cmsWithdrawalResultApi.ts#L205) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 3개 중 개발 메타데이터 확인 3개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-64fa78bdbe3bbb54) | Demo 메타데이터 3/3개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

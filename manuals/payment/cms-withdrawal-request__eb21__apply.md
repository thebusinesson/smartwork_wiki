# [CMS·카드 자동결제와 예외] (EB21/EB22) CMS 자동이체 관리 조회 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

EB21 등록 화면을 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | CMS·카드 자동결제와 예외 |
| 언제 사용하는가 | EB21 등록 정보 조회, EB21 생성 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 청구년월, 이체 요청일, 파일생성일, 출금일자, 파일명, 사업자번호 |
| 업무 흐름 | EB21 등록 정보 조회, EB21 생성 |
| 이 페이지의 역할 | 조회 · EB21 등록 정보 조회 |
| 판단 결과·다음 업무 | [(EB21/EB22) CMS 자동이체 관리](cms-withdrawal-request.md) |
| 다른 화면과의 구분 | 서비스 현황 > 입금관리 > (EB21/EB22) CMS 자동이체 관리에서 사용하는 조회 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 생성 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/Eb21WithdrawApplyPage.tsx#L397) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | EB21 등록 화면을 조회한다. |
| 메뉴·화면 경로 | 서비스 현황 > 입금관리 > (EB21/EB22) CMS 자동이체 관리 · `/payment/cms-withdrawal-request/eb21/apply` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [(EB21/EB22) CMS 자동이체 관리](cms-withdrawal-request.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/payment/cms-withdrawal-request` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| EB21 등록 정보 조회 | `/payment/cms-withdrawal-request` `VIEW` | `Eb21RegistrationSearchRequest` `invoiceMonth` |
| EB21 생성 | `/payment/cms-withdrawal-request` `PROCESS` | `Eb21CreateRequest?` `invoiceMonth`, `payDate` |

코드에서 확인한 버튼·작업명은 **검색**, **출금이체신청 작성**, **생성**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [(EB21/EB22) CMS 자동이체 관리](cms-withdrawal-request.md)에서 대상 또는 작업을 선택한다. `/payment/cms-withdrawal-request/eb21/apply`를 연다.
2. **청구년월**, **이체 요청일** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색** 중 해당 버튼을 선택한다.
3. **EB21 등록 정보 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [(EB21/EB22) CMS 자동이체 관리](cms-withdrawal-request.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 청구년월 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/Eb21WithdrawApplyPage.tsx#L103) |
| 이체 요청일 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/Eb21WithdrawApplyPage.tsx#L113) |
| 파일생성일 | 출력 | 조회 응답 기준 | 화면 필드 `fileCreatedDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/Eb21WithdrawApplyPage.tsx#L34) |
| 출금일자 | 출력 | 조회 응답 기준 | 화면 필드 `withdrawDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/Eb21WithdrawApplyPage.tsx#L41) |
| 파일명 | 출력 | 조회 응답 기준 | API 응답 `fileName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/Eb21WithdrawApplyPage.tsx#L47) |
| 사업자번호 | 출력 | 조회 응답 기준 | 화면 필드 `bizNo` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/Eb21WithdrawApplyPage.tsx#L132) |
| 회사명 | 출력 | 조회 응답 기준 | 화면 필드 `companyName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/Eb21WithdrawApplyPage.tsx#L138) |
| 출금요청액 | 출력 | 조회 응답 기준 | 화면 필드 `withdrawRequestAmount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/Eb21WithdrawApplyPage.tsx#L144) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| EB21 등록 정보 조회 | `GET /api/v1/payment/cms-auto-transfer/eb21/registration` · `/payment/cms-withdrawal-request` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/cmseb21/CmsEb21Controller.kt#L134) | `Eb21RegistrationSearchRequest` `invoiceMonth` → `success`, `data`, `error`, `generatedFiles`, `targets`, `fileCount`, `totalTargetCount` | `SmartBill3.dbo.upCMS_Lst_EA21`, `SmartBill3.dbo.upCMS_Lst_AppEA21` |
| EB21 생성 | `POST /api/v1/payment/cms-auto-transfer/eb21/registration/create` · `/payment/cms-withdrawal-request` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/cmseb21/CmsEb21Controller.kt#L150) | `Eb21CreateRequest?` `invoiceMonth`, `payDate` → `success`, `data`, `error`, `message`, `fileName` | `SmartBill3.dbo.upCMS_Lst_AppEA21`, `SmartBill3.dbo.upCMS_Sav_EA21File01`, `SmartBill3.dbo.upCMS_Lst_EA21` · 정의에서 확인한 쓰기 `SmartBill3.dbo.CMS_EA21`, `SmartBill3.dbo.CMS_EA21_DETAIL_CUB` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `SmartBill3.dbo.upCMS_Lst_EA21` | @yymm varchar(6) | 정의 참조 `SmartBill3.dbo.CMS_EA21` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmseb21/repository/Eb21Mapper.kt#L40) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-e0af4947735fcb93) |
| `SmartBill3.dbo.upCMS_Lst_AppEA21` | @YYMM varchar(6) | 정의 참조 `SB_BILL.dbo.BILL_EXCEPTION_COM_LIST`, `SmartBill3.dbo.CMS_ACCOUNT_MAIN`, `SmartBill3.dbo.COMPANY`, `SB_BILL.dbo.INVOICE`, `SB_BILL.dbo.PAYMENT` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmseb21/repository/Eb21Mapper.kt#L55) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-d2e73dae785e69b2) |
| `SmartBill3.dbo.upCMS_Sav_EA21File01` | @YYMM varchar(6), @PAYDATE varchar(6), @EA21FILE_NAME varchar(8), @INVBANKCODE varchar(6), @INVBANKACCNO varchar(16) | 정의 참조 `SB_BILL.dbo.BILL_EXCEPTION_COM_LIST`, `SmartBill3.dbo.CMS_ACCOUNT_MAIN_CUB`, `SmartBill3.dbo.CMS_EA21`, `SmartBill3.dbo.CMS_EA21_DETAIL`, `SmartBill3.dbo.CMS_EA21_DETAIL_CUB` 외 4개 · 정적 쓰기 `SmartBill3.dbo.CMS_EA21`, `SmartBill3.dbo.CMS_EA21_DETAIL_CUB` · 하위 호출 `SmartBill3.dbo.fnFillDigit` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmseb21/repository/Eb21Mapper.kt#L114) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-6b19eef98d07e27f) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 청구년월, 이체 요청일, 파일생성일, 출금일자, 파일명, 사업자번호 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 서비스 현황 > 입금관리 > (EB21/EB22) CMS 자동이체 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 작성 대상이 없습니다. | 청구년월, 이체 요청일, 파일생성일, 출금일자, 파일명, 사업자번호 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 현재월은 EB21 파일생성 작업이 끝났습니다. | 청구년월, 이체 요청일, 파일생성일, 출금일자, 파일명, 사업자번호 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 출금이체신청 작성에 실패했습니다. | 청구년월, 이체 요청일, 파일생성일, 출금일자, 파일명, 사업자번호 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/PaymentRoutes.tsx#L88) · [Eb21WithdrawApplyPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/Eb21WithdrawApplyPage.tsx#L213) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/eb21WithdrawApplyApi.ts#L30) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/eb21WithdrawApplyApi.ts#L37) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 3개 중 개발 메타데이터 확인 3개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-631ea2a9252ba468) | Demo 메타데이터 3/3개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

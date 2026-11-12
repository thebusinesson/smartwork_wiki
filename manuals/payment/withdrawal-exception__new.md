# [CMS·카드 자동결제와 예외] 출금신청 예외처리 등록 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

출금신청 예외처리 업체를 신규 등록한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | CMS·카드 자동결제와 예외 |
| 언제 사용하는가 | 예외처리 서비스 코드 목록 조회, 회사 정보 목록 조회, 출금신청 예외처리 등록 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 예외 서비스, 예외처리 코드, 업체, 예외처리 시작일, 예외처리 종료일, 사용여부 |
| 업무 흐름 | 예외처리 서비스 코드 목록 조회, 회사 정보 목록 조회, 출금신청 예외처리 등록 |
| 이 페이지의 역할 | 등록 · 출금신청 예외처리 등록 |
| 판단 결과·다음 업무 | [출금신청 예외처리 관리](withdrawal-exception.md) |
| 다른 화면과의 구분 | 서비스 현황 > 입금관리 > 출금신청 예외처리 관리에서 사용하는 등록 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 출금신청 예외처리 업체를 신규 등록한다. |
| 메뉴·화면 경로 | 서비스 현황 > 입금관리 > 출금신청 예외처리 관리 · `/payment/withdrawal-exception/new` |
| 화면 유형·담당 | 등록 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [출금신청 예외처리 관리](withdrawal-exception.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/payment/withdrawal-exception` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 예외처리 서비스 코드 목록 조회 | `/payment/withdrawal-exception` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 회사 정보 목록 조회 | `/company-management/company-info` `VIEW` | `CompanyInfoSearchRequest` `dateConditionType`, `companyConditionType`, `searchKeyword`, `fromDate`, `toDate`, `unpaidStatus`, `membershipStatus`, `issuanceSchedule` |
| 출금신청 예외처리 등록 | `/payment/withdrawal-exception` `PROCESS` | `WithdrawalExceptionSaveRequest` `serviceCode`, `comNo`, `beginDate`, `endDate`, `useYn` |

코드에서 확인한 버튼·작업명은 **업체 검색**, **저장**, **목록**, **검색**, **취소**, **확인**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [출금신청 예외처리 관리](withdrawal-exception.md)에서 대상 또는 작업을 선택한다. `/payment/withdrawal-exception/new`를 연다.
2. **사용**, **미사용** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **업체 검색**, **저장**, **검색**, **확인** 중 해당 버튼을 선택한다.
3. **출금신청 예외처리 등록**을 실행하기 전에 변경 대상과 입력값을 확인한다. 처리 응답을 확인하고 관련 조회에서 대상의 상태를 확인한다.
4. 후속 조회나 목록 복귀가 필요하면 [출금신청 예외처리 관리](withdrawal-exception.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 예외 서비스 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/WithdrawalExceptionRegistrationPage.tsx#L151) |
| 예외처리 코드 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/WithdrawalExceptionRegistrationPage.tsx#L166) |
| 업체 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/WithdrawalExceptionRegistrationPage.tsx#L170) |
| 예외처리 시작일 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/WithdrawalExceptionRegistrationPage.tsx#L190) |
| 예외처리 종료일 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/WithdrawalExceptionRegistrationPage.tsx#L199) |
| 사용여부 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/WithdrawalExceptionRegistrationPage.tsx#L210) |
| 사용 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/WithdrawalExceptionRegistrationPage.tsx#L213) |
| 미사용 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/WithdrawalExceptionRegistrationPage.tsx#L223) |
| 회사명을 입력하세요 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/WithdrawalExceptionCompanySearchDialog.tsx#L179) |
| 사업자등록번호 | 출력 | 조회 응답 기준 | 화면 필드 `businessNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/WithdrawalExceptionCompanySearchDialog.tsx#L30) |
| 회사명 | 출력 | 조회 응답 기준 | 화면 필드 `companyName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/WithdrawalExceptionCompanySearchDialog.tsx#L34) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 예외처리 서비스 코드 목록 조회 | `GET /api/v1/payment/withdrawal-exception/service-codes` · `/payment/withdrawal-exception` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/withdrawalexception/WithdrawalExceptionController.kt#L61) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `code`, `description` | `SB_BILL.dbo.USPBILL_COMMON_CODE_LIST` · 코드 연계 트랜잭션 |
| 회사 정보 목록 조회 | `GET /api/v1/company-management/company-info` · `/company-management/company-info` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/customer/company/CompanyInfoController.kt#L108) · [기존 상세 계약](../../references/api-contracts.md#api044) | `CompanyInfoSearchRequest` `dateConditionType`, `companyConditionType`, `searchKeyword`, `fromDate`, `toDate`, `unpaidStatus`, `membershipStatus`, `issuanceSchedule` → `success`, `data`, `error`, `content`, `totalElements` | `smartwork.dbo.usp_company_info_list_select` · 코드 연계 트랜잭션 |
| 출금신청 예외처리 등록 | `POST /api/v1/payment/withdrawal-exception` · `/payment/withdrawal-exception` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/withdrawalexception/WithdrawalExceptionController.kt#L111) | `WithdrawalExceptionSaveRequest` `serviceCode`, `comNo`, `beginDate`, `endDate`, `useYn` → `success`, `data`, `error` | `SB_BILL.dbo.USPBILL_MANAGE_EXCEPTION_WRITE` · 정의에서 확인한 쓰기 `SB_BILL.dbo.BILL_EXCEPTION_COM_LIST` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `SB_BILL.dbo.USPBILL_COMMON_CODE_LIST` | @CODETYPE varchar(20), @SUBTYPE varchar(10) | 정의 참조 `SB_BILL.dbo.BILL_COMMON_CODE` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/withdrawalexception/repository/WithdrawalExceptionMapper.kt#L29) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b4eadc2296c818b6) |
| `smartwork.dbo.usp_company_info_list_select` | @STRITEM varchar(100), @STRCONTENTS varchar(100), @FROMDATE varchar(10), @TODATE varchar(10), @CSTATUS varchar(10), @CSTATUS2 varchar(10), @DTI_BILLTYPE varchar(10), @DCT_BILLTYPE varchar(10), @ISSUANCE_SCHEDULE varchar(10) | 정의 참조 `SmartBill3.dbo.CMS_ACCOUNT_CUB`, `SmartBill3.dbo.COMPANY`, `SB_DTI.dbo.COMPANY_DTICONFIG`, `SmartBill3.dbo.SETTLEMENT` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoMapper.kt#L51) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-d99504f061a3c537) |
| `SB_BILL.dbo.USPBILL_MANAGE_EXCEPTION_WRITE` | @SERVICE_CODE varchar(10), @COM_NO int, @BEGIN_DATE varchar(10), @END_DATE varchar(10), @USE_YN varchar(1), @SW_NO int, @RESULT_CODE varchar(5) OUT | 정의 참조 `SB_BILL.dbo.BILL_EXCEPTION_COM_LIST` · 정적 쓰기 `SB_BILL.dbo.BILL_EXCEPTION_COM_LIST` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/withdrawalexception/repository/WithdrawalExceptionMapper.kt#L74) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-afadcfe8e90ea130) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 예외 서비스, 예외처리 코드, 업체, 예외처리 시작일, 예외처리 종료일, 사용여부 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 서비스 현황 > 입금관리 > 출금신청 예외처리 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/PaymentRoutes.tsx#L103) · [WithdrawalExceptionRegistrationPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/WithdrawalExceptionRegistrationPage.tsx#L49) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/withdrawalExceptionApi.ts#L18) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/withdrawalExceptionApi.ts#L77) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/withdrawalExceptionApi.ts#L60) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 3개 중 개발 메타데이터 확인 3개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-fc10fb148bdee45c) | Demo 메타데이터 3/3개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

# [CMS·카드 자동결제와 예외] 신용카드 자동결제 승인요청 상세 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

특정 출금월/차수의 업체별 카드빌링 상세(승인결과, 금액 등) 목록을 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | CMS·카드 자동결제와 예외 |
| 언제 사용하는가 | 신용카드 자동결제 승인요청 상세 목록 조회 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 검색조건, 전체, 회사명, 사업자번호, 승인 여부, 성공 |
| 업무 흐름 | 신용카드 자동결제 승인요청 상세 목록 조회 |
| 이 페이지의 역할 | 상세 · 신용카드 자동결제 승인요청 상세 목록 조회 |
| 판단 결과·다음 업무 | [신용카드 자동결제 승인요청](credit-card-auto-payment.md) |
| 다른 화면과의 구분 | 서비스 현황 > 입금관리 > 신용카드 자동결제 승인요청에서 사용하는 상세 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 특정 출금월/차수의 업체별 카드빌링 상세(승인결과, 금액 등) 목록을 조회한다. |
| 메뉴·화면 경로 | 서비스 현황 > 입금관리 > 신용카드 자동결제 승인요청 · `/payment/credit-card-auto-payment/:withdrawalMonth/:division` · 경로 변수 `withdrawalMonth`, `division` |
| 화면 유형·담당 | 상세 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [신용카드 자동결제 승인요청](credit-card-auto-payment.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/payment/credit-card-auto-payment` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `withdrawalMonth`, `division` |
| 신용카드 자동결제 승인요청 상세 목록 조회 | `/payment/credit-card-auto-payment` `VIEW` | `CardBillingDetailSearchRequest` `withdrawalMonth`, `division`, `searchType`, `searchText`, `approvalStatusSuccess`, `approvalStatusFailure`, `page`, `size` |

코드에서 확인한 버튼·작업명은 **검색**, **목록**, **목록으로 돌아가기**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [신용카드 자동결제 승인요청](credit-card-auto-payment.md)에서 대상 또는 작업을 선택한다. `/payment/credit-card-auto-payment/:withdrawalMonth/:division`에서 이전 화면이 전달한 `withdrawalMonth`, `division`와 현재 대상을 확인한다.
2. **검색조건**, **전체**, **회사명**, **사업자번호**, **승인 여부**, **성공**, **실패** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색** 중 해당 버튼을 선택한다.
3. **신용카드 자동결제 승인요청 상세 목록 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [신용카드 자동결제 승인요청](credit-card-auto-payment.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `withdrawalMonth`, `division` |
| 검색조건 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/CreditCardAutoPaymentDetailPage.tsx#L28) |
| 전체 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `ALL` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/CreditCardAutoPaymentDetailPage.tsx#L35) |
| 회사명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `A` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/CreditCardAutoPaymentDetailPage.tsx#L36) |
| 사업자번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `B` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/CreditCardAutoPaymentDetailPage.tsx#L37) |
| 검색어를 입력하세요 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/CreditCardAutoPaymentDetailPage.tsx#L40) |
| 승인 여부 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/CreditCardAutoPaymentDetailPage.tsx#L50) |
| 성공 | 입력 또는 선택 | API 기본값 null | API 요청 `approvalStatusSuccess` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/CreditCardAutoPaymentDetailPage.tsx#L55) |
| 실패 | 입력 또는 선택 | API 기본값 null | API 요청 `approvalStatusFailure` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/CreditCardAutoPaymentDetailPage.tsx#L60) |
| 출금월 | 입력 또는 선택 | API 기본값 null | API 요청 `withdrawalMonth` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CreditCardAutoPaymentDetailTable.tsx#L40) |
| 차수 | 입력 또는 선택 | API 기본값 null | API 요청 `division` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CreditCardAutoPaymentDetailTable.tsx#L41) |
| 회사명(사업자번호) | 출력 | 조회 응답 기준 | 화면 필드 `companyName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CreditCardAutoPaymentDetailTable.tsx#L44) |
| 결제금액 | 출력 | 조회 응답 기준 | 화면 필드 `paymentAmountFormatted` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CreditCardAutoPaymentDetailTable.tsx#L56) |
| 결제카드 | 출력 | 조회 응답 기준 | 화면 필드 `financeName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CreditCardAutoPaymentDetailTable.tsx#L61) |
| 카드구분1 | 출력 | 조회 응답 기준 | 화면 필드 `cardType1` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CreditCardAutoPaymentDetailTable.tsx#L62) |
| 카드구분2 | 출력 | 조회 응답 기준 | 화면 필드 `cardType2` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CreditCardAutoPaymentDetailTable.tsx#L63) |
| 결제결과 | 출력 | 조회 응답 기준 | 화면 필드 `responseMessage` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CreditCardAutoPaymentDetailTable.tsx#L64) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 신용카드 자동결제 승인요청 상세 목록 조회 | `GET /api/v1/payment/card-billing/details` · `/payment/credit-card-auto-payment` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/cardbilling/CardBillingController.kt#L61) | `CardBillingDetailSearchRequest` `withdrawalMonth`, `division`, `searchType`, `searchText`, `approvalStatusSuccess`, `approvalStatusFailure`, `page`, `size` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `currentPage`, `size` | `SB_BILL.dbo.UspBill_CardBillingDetailList_SELECT_TOP` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `SB_BILL.dbo.UspBill_CardBillingDetailList_SELECT_TOP` | @PAGE int, @TOP int, @GUBUN varchar(3), @SCH_TEXT varchar(70), @WITHDRAWMONTH varchar(7), @DIVISION varchar(1), @SUCESSYN varchar(4) | 정의 참조 `SB_BILL.dbo.UspBill_CardBillingDetailCount_SELECT` · 하위 호출 `SB_BILL.dbo.UspBill_CardBillingDetailCount_SELECT` · 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cardbilling/repository/CardBillingDetailMapper.kt#L37) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-1109c3d16d439487) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 검색조건, 전체, 회사명, 사업자번호, 승인 여부, 성공 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 서비스 현황 > 입금관리 > 신용카드 자동결제 승인요청의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/PaymentRoutes.tsx#L107) · [CreditCardAutoPaymentDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/CreditCardAutoPaymentDetailPage.tsx#L67) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/creditCardAutoPaymentDetailApi.ts#L22) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 1개 중 개발 메타데이터 확인 1개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-1fa06918e8177854) | Demo 메타데이터 1/1개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

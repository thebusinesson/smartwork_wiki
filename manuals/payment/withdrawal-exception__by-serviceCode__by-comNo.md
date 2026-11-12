# [CMS·카드 자동결제와 예외] 출금신청 예외처리 관리 상세 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

서비스코드와 업체번호로 출금신청 예외처리 상세 정보를 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | CMS·카드 자동결제와 예외 |
| 언제 사용하는가 | 출금신청 예외처리 상세 조회, 출금신청 예외처리 수정 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 예외 서비스, 설명, 업체명, 사업자등록번호, 예외처리 시작일, 예외처리 종료일 |
| 업무 흐름 | 출금신청 예외처리 상세 조회, 출금신청 예외처리 수정 |
| 이 페이지의 역할 | 상세 · 출금신청 예외처리 상세 조회 |
| 판단 결과·다음 업무 | [출금신청 예외처리 관리](withdrawal-exception.md) |
| 다른 화면과의 구분 | 서비스 현황 > 입금관리 > 출금신청 예외처리 관리에서 사용하는 상세 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 서비스코드와 업체번호로 출금신청 예외처리 상세 정보를 조회한다. |
| 메뉴·화면 경로 | 서비스 현황 > 입금관리 > 출금신청 예외처리 관리 · `/payment/withdrawal-exception/:serviceCode/:comNo` · 경로 변수 `serviceCode`, `comNo` |
| 화면 유형·담당 | 상세 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [출금신청 예외처리 관리](withdrawal-exception.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/payment/withdrawal-exception` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `serviceCode`, `comNo` |
| 출금신청 예외처리 상세 조회 | `/payment/withdrawal-exception` `VIEW` | `serviceCode: String` · `comNo: Int` |
| 출금신청 예외처리 수정 | `/payment/withdrawal-exception` `PROCESS` | `serviceCode: String` · `comNo: Int` · `WithdrawalExceptionModifyRequest` `beginDate`, `endDate`, `useYn` |

코드에서 확인한 버튼·작업명은 **저장**, **수정**, **목록**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [출금신청 예외처리 관리](withdrawal-exception.md)에서 대상 또는 작업을 선택한다. `/payment/withdrawal-exception/:serviceCode/:comNo`에서 이전 화면이 전달한 `serviceCode`, `comNo`와 현재 대상을 확인한다.
2. **사용**, **미사용** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **저장** 중 해당 버튼을 선택한다.
3. **출금신청 예외처리 상세 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [출금신청 예외처리 관리](withdrawal-exception.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `serviceCode`, `comNo` |
| 예외 서비스 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/WithdrawalExceptionDetailPage.tsx#L141) |
| 설명 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/WithdrawalExceptionDetailPage.tsx#L143) |
| 업체명 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/WithdrawalExceptionDetailPage.tsx#L147) |
| 사업자등록번호 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/WithdrawalExceptionDetailPage.tsx#L149) |
| 예외처리 시작일 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/WithdrawalExceptionDetailPage.tsx#L153) |
| 예외처리 종료일 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/WithdrawalExceptionDetailPage.tsx#L166) |
| 등록일 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/WithdrawalExceptionDetailPage.tsx#L183) |
| 최종 수정일 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/WithdrawalExceptionDetailPage.tsx#L185) |
| 사용여부 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/WithdrawalExceptionDetailPage.tsx#L191) |
| 사용 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/WithdrawalExceptionDetailPage.tsx#L195) |
| 미사용 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/WithdrawalExceptionDetailPage.tsx#L205) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 출금신청 예외처리 상세 조회 | `GET /api/v1/payment/withdrawal-exception/{serviceCode}/{comNo}` · `/payment/withdrawal-exception` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/withdrawalexception/WithdrawalExceptionController.kt#L88) | `serviceCode: String` · `comNo: Int` → `success`, `data`, `error`, `serviceCode`, `serviceDescription`, `comNo`, `businessNumber`, `companyName`, `beginDate`, `endDate`, `useYn`, `createdDate` | `SB_BILL.dbo.USPBILL_MANAGE_EXCEPTION_ITEM` |
| 출금신청 예외처리 수정 | `PUT /api/v1/payment/withdrawal-exception/{serviceCode}/{comNo}` · `/payment/withdrawal-exception` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/withdrawalexception/WithdrawalExceptionController.kt#L99) | `serviceCode: String` · `comNo: Int` · `WithdrawalExceptionModifyRequest` `beginDate`, `endDate`, `useYn` → `success`, `data`, `error` | `SB_BILL.dbo.USPBILL_MANAGE_EXCEPTION_MODIFY` · 정의에서 확인한 쓰기 `SB_BILL.dbo.BILL_EXCEPTION_COM_LIST` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `SB_BILL.dbo.USPBILL_MANAGE_EXCEPTION_ITEM` | @SERVICECODE varchar(10), @COMNO int | 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/withdrawalexception/repository/WithdrawalExceptionMapper.kt#L63) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-0fa00aa5e9123192) |
| `SB_BILL.dbo.USPBILL_MANAGE_EXCEPTION_MODIFY` | @SERVICE_CODE varchar(10), @COM_NO int, @BEGIN_DATE varchar(10), @END_DATE varchar(10), @USE_YN varchar(1) | 정의 참조 `SB_BILL.dbo.BILL_EXCEPTION_COM_LIST` · 정적 쓰기 `SB_BILL.dbo.BILL_EXCEPTION_COM_LIST` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/withdrawalexception/repository/WithdrawalExceptionMapper.kt#L70) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-4d761719da3e87b0) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 예외 서비스, 설명, 업체명, 사업자등록번호, 예외처리 시작일, 예외처리 종료일 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 서비스 현황 > 입금관리 > 출금신청 예외처리 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/PaymentRoutes.tsx#L105) · [WithdrawalExceptionDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/WithdrawalExceptionDetailPage.tsx#L29) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/withdrawalExceptionApi.ts#L46) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/withdrawalExceptionApi.ts#L55) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 2개 중 개발 메타데이터 확인 2개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-c8baa184e82196d4) | Demo 메타데이터 2/2개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

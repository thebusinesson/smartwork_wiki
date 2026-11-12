# [CMS·카드 자동결제와 예외] 출금신청 예외처리 관리 등록 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

엑셀/CSV 파일을 업로드하여 출금신청 예외처리를 대량 등록한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | CMS·카드 자동결제와 예외 |
| 언제 사용하는가 | 대량 등록 샘플 양식 다운로드, 출금신청 예외처리 대량 등록 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 파일 첨부, 업로드 일시, 업로드 결과, 예외처리 서비스, 회사명, 사업자번호 |
| 업무 흐름 | 대량 등록 샘플 양식 다운로드, 출금신청 예외처리 대량 등록 |
| 이 페이지의 역할 | 등록 · 출금신청 예외처리 대량 등록 |
| 판단 결과·다음 업무 | [출금신청 예외처리 관리](withdrawal-exception.md) |
| 다른 화면과의 구분 | 서비스 현황 > 입금관리 > 출금신청 예외처리 관리에서 사용하는 등록 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 엑셀/CSV 파일을 업로드하여 출금신청 예외처리를 대량 등록한다. |
| 메뉴·화면 경로 | 서비스 현황 > 입금관리 > 출금신청 예외처리 관리 · `/payment/withdrawal-exception/bulk` |
| 화면 유형·담당 | 등록 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [출금신청 예외처리 관리](withdrawal-exception.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/payment/withdrawal-exception` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 대량 등록 샘플 양식 다운로드 | `/payment/withdrawal-exception` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 출금신청 예외처리 대량 등록 | `/payment/withdrawal-exception` `EXCEL_UPLOAD` | `file: MultipartFile` |

코드에서 확인한 버튼·작업명은 **파일 삭제**, **첨부파일**, **파일 선택**, **샘플 다운로드**, **업로드**, **파일 업로드**, **목록**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [출금신청 예외처리 관리](withdrawal-exception.md)에서 대상 또는 작업을 선택한다. `/payment/withdrawal-exception/bulk`를 연다.
2. **파일 첨부** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **샘플 다운로드** 중 해당 버튼을 선택한다.
3. **출금신청 예외처리 대량 등록**을 실행하기 전에 변경 대상과 입력값을 확인한다. 처리 응답을 확인하고 관련 조회에서 대상의 상태를 확인한다.
4. 후속 조회나 목록 복귀가 필요하면 [출금신청 예외처리 관리](withdrawal-exception.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 파일 첨부 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/WithdrawalExceptionBulkRegistrationPage.tsx#L166) |
| 업로드 일시 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/WithdrawalExceptionBulkRegistrationPage.tsx#L247) |
| 업로드 결과 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/WithdrawalExceptionBulkRegistrationPage.tsx#L249) |
| 예외처리 서비스 | 출력 | 조회 응답 기준 | 화면 필드 `service` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/WithdrawalExceptionBulkRegistrationPage.tsx#L35) |
| 회사명 | 출력 | 조회 응답 기준 | 화면 필드 `companyName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/WithdrawalExceptionBulkRegistrationPage.tsx#L36) |
| 사업자번호 | 출력 | 조회 응답 기준 | 화면 필드 `businessNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/WithdrawalExceptionBulkRegistrationPage.tsx#L37) |
| 예외처리 시작일 | 출력 | 조회 응답 기준 | 화면 필드 `beginDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/WithdrawalExceptionBulkRegistrationPage.tsx#L38) |
| 예외처리 종료일 | 출력 | 조회 응답 기준 | 화면 필드 `endDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/WithdrawalExceptionBulkRegistrationPage.tsx#L39) |
| 사용여부 | 출력 | 조회 응답 기준 | 화면 필드 `useYn` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/WithdrawalExceptionBulkRegistrationPage.tsx#L40) |
| 실패사유 | 출력 | 조회 응답 기준 | 화면 필드 `failureReason` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/WithdrawalExceptionBulkRegistrationPage.tsx#L41) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 대량 등록 샘플 양식 다운로드 | `GET /api/v1/payment/withdrawal-exception/template` · `/payment/withdrawal-exception` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/withdrawalexception/WithdrawalExceptionController.kt#L133) | 추가 입력은 Controller 서명 참조 → 파일 또는 오류 응답 | 직접 DB 호출이 연결된 경로는 현재 소스에서 미확인. 세부 저장소는 Controller와 Service 참조. |
| 출금신청 예외처리 대량 등록 | `POST /api/v1/payment/withdrawal-exception/bulk` · `/payment/withdrawal-exception` `EXCEL_UPLOAD` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/withdrawalexception/WithdrawalExceptionController.kt#L122) | `file: MultipartFile` → `success`, `data`, `error`, `uploadedAt`, `totalCount`, `successCount`, `failCount`, `serviceResults`, `errors` | `SB_BILL.dbo.USPBILL_COMMON_CODE_LIST`, `SmartBill3.dbo.COMPANY`, `SB_BILL.dbo.USPBILL_MANAGE_EXCEPTION_WRITE` · 정의에서 확인한 쓰기 `SB_BILL.dbo.BILL_EXCEPTION_COM_LIST` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `SB_BILL.dbo.USPBILL_COMMON_CODE_LIST` | @CODETYPE varchar(20), @SUBTYPE varchar(10) | 정의 참조 `SB_BILL.dbo.BILL_COMMON_CODE` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/withdrawalexception/repository/WithdrawalExceptionMapper.kt#L29) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b4eadc2296c818b6) |
| `SmartBill3.dbo.COMPANY` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoMapper.kt#L78) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-0e6fcaa6b5086c07) |
| `SB_BILL.dbo.USPBILL_MANAGE_EXCEPTION_WRITE` | @SERVICE_CODE varchar(10), @COM_NO int, @BEGIN_DATE varchar(10), @END_DATE varchar(10), @USE_YN varchar(1), @SW_NO int, @RESULT_CODE varchar(5) OUT | 정의 참조 `SB_BILL.dbo.BILL_EXCEPTION_COM_LIST` · 정적 쓰기 `SB_BILL.dbo.BILL_EXCEPTION_COM_LIST` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/withdrawalexception/repository/WithdrawalExceptionMapper.kt#L74) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-afadcfe8e90ea130) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 파일 첨부, 업로드 일시, 업로드 결과, 예외처리 서비스, 회사명, 사업자번호 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 서비스 현황 > 입금관리 > 출금신청 예외처리 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 샘플 다운로드에 실패했습니다. | 파일 첨부, 업로드 일시, 업로드 결과, 예외처리 서비스, 회사명, 사업자번호 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/PaymentRoutes.tsx#L104) · [WithdrawalExceptionBulkRegistrationPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/WithdrawalExceptionBulkRegistrationPage.tsx#L44) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/withdrawalExceptionApi.ts#L90) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/withdrawalExceptionApi.ts#L85) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 3개 중 개발 메타데이터 확인 3개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-aeefdd4342ce4e3e) | Demo 메타데이터 3/3개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

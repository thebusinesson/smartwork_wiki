# [서비스 현황] 입금 현황 조회 (상세) 관리자 매뉴얼

작성 기준: `dc216b313` · 확인일 2026-11-09 · 조사 상태 **검토 대기**. 코드·개발 DB 정의 확인. 브라우저: **진입 미재현**; 저장·발송 등 업무 실행 결과는 미검증이다.

## 1) 화면 기본 정보

### 도메인 이해

고객의 서비스 요금 입금과 미리 보유한 금액, 환불 신청을 관리하는 업무다. 입금 내역이 어느 업체·청구에 연결되는지, 예치금이 어떻게 늘거나 줄었는지, 환불 가능한 금액과 처리 상태가 무엇인지 확인한다.

| 구분 | 설명 |
|---|---|
| 업무 영역 | 입금·예치금·환불 관리 · 서비스 현황 > 입금관리 > 입금 현황 조회 |
| 주요 대상·용어 | 입금: 접수된 납부 내역 / 예치금: 서비스 이용을 위해 보유·차감되는 금액 / 청구월: 요금을 청구한 월 / 환불 신청: 환불 대상·금액·계좌·처리 상태 기록 |
| 업무 흐름 | 업체·기간·청구 찾기 → 입금·잔액·이력 확인 → 허용된 입금/예치금/환불 처리 → 상태·금액 재확인 |
| 이 페이지의 역할 | 요금 입금 내역에서 선택한 한 대상의 상세 내용·상태·관련 이력을 확인하는 화면이다. 청구월·입금일·방식·상태로 납부 내역과 처리 상태를 확인한다. |
| 관련 업무와 구분 | 예치금 잔액·환불 가능 금액·환불 신청 금액은 같은 값이 아니다. 화면의 처리 완료와 실제 은행 송금 완료의 확인 범위를 구분한다. |

도메인 설명 근거: 이 문서 7번의 현재 메뉴·라우트·화면 및 API·업무 규칙 소스. [전체 도메인 지도](../../references/domain-overview.md#payment). 설명 보강일 2026-11-09; 기존 실행 검증 범위와 미확인 상태는 변경하지 않았다.

### 화면 정보

| 항목 | 작성 내용 |
|---|---|
| 업무 도메인·목적 | 청구월·입금일·입금 방식·상태별 입금 내역과 처리 상태를 확인한다. |
| 메뉴·화면 경로 | 서비스 현황 > 입금관리 > 입금 현황 조회; `/payment/status/:id`; 목록에서 선택한 대상의 경로 변수를 유지하여 진입한다. |
| 화면 유형·담당 | 상세; WBS 작업자 유지윤. 업무·기술 담당 팀명은 원문에 없어 배포 전 해당 도메인 담당자가 확정한다. |
| 관련 화면 | [조회·관리](status.md) |

WBS 근거: No. 184 (사용자가 제공한 텍스트 행 230). API 개발/화면 개발의 중복 행은 같은 화면으로 통합했다.

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
|---|---|---|
| 화면 진입·조회 | `/payment/status` 메뉴 접근·하위 경로 작업 권한. 조회 API는 VIEW, 등록/수정 경로는 PROCESS 등 아래 서버 액션과 라우트 가드를 함께 적용한다. | 로그인된 관리자 계정; id 식별자는 이전 화면에서 선택한다. |
| 입금 취소 | `/payment/status`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 예치금 처리 | `/payment/status`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 목록 | `/payment/status`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 조회 중... | `/payment/status`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |

서버가 최종 권한을 검사한다. 버튼 모양(kind)으로 권한을 추정하지 않는다. 특히 등록·수정이 PROCESS를 사용하는 API와 EXECUTE·UNMASK·EXCEL_DOWNLOAD는 서로 구분한다.

## 3) 화면 사용 절차

1. 관련 화면에서 대상 또는 작업을 선택하여 `/payment/status/:id`로 이동한다. 경로 변수는 주소에서 임의로 바꾸지 않고 이전 화면이 전달한 식별자를 사용한다.
2. 대상의 기본 정보·상태·표시 항목을 확인한다. 목록의 식별자와 상세 대상이 일치하는지 확인한다.
3. **입금 취소, 예치금 처리, 조회 중...** 중 필요한 작업을 선택한다. 버튼의 표시·활성 조건과 아래 API별 권한을 확인한다. 저장·삭제·외부 호출 전에는 대상과 현재 상태를 재확인한다.
4. 작업 결과 또는 다운로드 파일을 확인하고 관련 목록으로 돌아가 변경된 상태를 다시 조회한다.

**이 화면에서 유의할 업무 규칙**: 업체 조건은 사업자번호가 기본이며 입금 방식·상태는 기본 전체 선택이다. 상세에서 입금 취소와 예치금 처리 가능 상태를 확인한다. 입금자 원문은 별도 UNMASK 권한과 감사 절차가 있는 경우에만 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
|---|---|---|---|
| 입금일 | 출력 | API 타입 String | `paymentDate`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/PaymentHistoriesTable.tsx#L11) |
| 입금자 | 출력 | API 타입 String | `payer`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/PaymentHistoriesTable.tsx#L17) |
| 입금방식 | 출력 | API 타입 String | `paymentMethod`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/PaymentHistoriesTable.tsx#L18) |
| 입금액 | 출력 | API 타입 Long | `paymentAmount`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/PaymentHistoriesTable.tsx#L19) |
| ORDER-ID | 출력 | API 타입 String | `orderId`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/PaymentHistoriesTable.tsx#L26) |
| 세금계산서 참조번호 | 출력 | API 타입 String? | `taxInvoiceReference`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/PaymentHistoriesTable.tsx#L27) |
| 사업자번호 | 출력 | API 타입 String | `businessNumber`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/ProcessingHistoriesTable.tsx#L12) |
| 회사명 | 출력 | API 타입 String | `companyName`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/ProcessingHistoriesTable.tsx#L18) |
| 처리구분 | 출력 | API 타입 String | `processingType`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/ProcessingHistoriesTable.tsx#L19) |
| 처리 금액 | 출력 | API 타입 Long | `processingAmount`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/ProcessingHistoriesTable.tsx#L20) |
| 처리일 | 출력 | API 타입 String | `processingDate`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/ProcessingHistoriesTable.tsx#L28) |
| 처리자 | 출력 | API 타입 String | `processor`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/ProcessingHistoriesTable.tsx#L34) |

입력 검증 근거: [createProcessAmountSchema.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/status/payment/components/createProcessAmountSchema.ts), [validationUtils.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/status/payment/utils/validationUtils.ts), [CommonPrepaidProcessingDialog.schema.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/status/payment/components/CommonPrepaidProcessingDialog.schema.ts). 프런트 검증과 서버 DTO 제약이 다르면 서버 검증이 최종 기준이다.

화면 필드 키와 API 필드명이 다른 경우 변환은 Hook/API의 검색·저장 매핑에서 수행된다. 요청·응답 필드와 DB 컬럼 매핑은 아래 API 계약 및 DB 객체 계약에 연결했다.

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
|---|---|---|---|
| 입금 현황 상세 조회 | [GET /api/v1/service-status/deposits/status/{id}](../../references/api-contracts.md#api111); `/payment/status` / `VIEW` | `경로·쿼리·본문 계약 참조` → `companyName, businessNumber, billingMonth, paymentStatus, billingAmount, paymentAmount, depositAvailableAmount, paymentHistories, processingHistories, waitingDeposit, canCancel, ca` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 입금 취소 | [POST /api/v1/service-status/deposits/status/{id}/cancel](../../references/api-contracts.md#api230); `/payment/status` / `PROCESS` | `경로·쿼리·본문 계약 참조` → `응답 DTO·파일/처리 결과 계약 참조` | 쓰기 대상 sb_bill.dbo.cardbilling_transfer_result, sb_bill.dbo.invoice, sb_bill.dbo.payment, sb_bill.dbo.payment_his, sb_bill.dbo.service_prepay_monthly_remain, sb_bill.dbo.service_prepay_monthly_remain_card_cancle_history, smartbill3.dbo.accinfo_cancel, smartbill3.dbo.accinfo_history, smartbill3.dbo.company, smartbill3.dbo.service_prepay, smartbill3.dbo.service_prepay_his |
| 선불 입금 처리 | [POST /api/v1/service-status/deposits/status/{id}/process-prepaid](../../references/api-contracts.md#api231); `/payment/status` / `PROCESS` | `processingAmount, note` → `success, message` | 쓰기 대상 sb_bill.dbo.invoice, sb_bill.dbo.payment, sb_bill.dbo.payment_his, smartbill3.dbo.service_prepay, smartbill3.dbo.service_prepay_his |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
|---|---|---|---|
| [smartwork.dbo.UspBill_PayMentDetailHistory_SELECT](../../references/database-contracts.md#db310) | `@IDX bigint IN` | 확정한 테이블 쓰기 없음. 참조: office.dbo.sawon, sb_bill.dbo.payment, sb_bill.dbo.payment_his, smartbill3.dbo.company, smartbill3.dbo.service_prepay | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.UspBill_PayMentWaitingDeposit_SELECT](../../references/database-contracts.md#db313) | `@IDX_LIST nvarchar(max) IN` | 확정한 테이블 쓰기 없음. 참조: sb_bill.dbo.headoffice_deposit, sb_bill.dbo.headoffice_deposit_his, sb_bill.dbo.payment, smartbill3.dbo.account_bulk, smartbill3.dbo.account_bulk_app, smartbill3.dbo.company | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_BILL.dbo.UspBill_PayMentDetail_SELECT](../../references/database-contracts.md#db078) | `@IDX int IN` | 확정한 테이블 쓰기 없음. 참조: sb_bill.dbo.invoice, sb_bill.dbo.payment, sb_dti.dbo.dti_header_cub, sb_dti.dbo.dti_header_cub_2023_07, sb_dti.dbo.dti_header_cub_part, sb_dti.dbo.dti_header_cub_prev_buffer, smartbill3.dbo.company, smartbill3.dbo.member | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_BILL.dbo.PAYMENT](../../references/database-contracts.md#db064) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 쓰기: sb_bill.dbo.payment. 참조: sb_bill.dbo.payment | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.UspBill_DepositCancelVerify_SELECT](../../references/database-contracts.md#db304) | `@ORDER_ID varchar(64) IN` | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.accinfo_cancel, smartbill3.dbo.accinfo_history | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_BILL.dbo.UPMEM_ACCETC_CANCEL](../../references/database-contracts.md#db065) | `@COM_NO int IN, @MEM_NO int IN, @ORDER_ID varchar(64) IN, @PREPAYNO int IN, @RESULT varchar(5) OUT` | 쓰기: sb_bill.dbo.invoice, sb_bill.dbo.payment, sb_bill.dbo.payment_his, sb_bill.dbo.service_prepay_monthly_remain, sb_bill.dbo.service_prepay_monthly_remain_card_cancle_history, smartbill3.dbo.accinfo_cancel, smartbill3.dbo.accinfo_history, smartbill3.dbo.company, smartbill3.dbo.service_prepay, smartbill3.dbo.service_prepay_his. 참조: sb_bill.dbo.close, sb_bill.dbo.invoice, sb_bill.dbo.payment, sb_bill.dbo.payment_his, sb_bill.dbo.service_prepay_monthly_remain, sb_bill.dbo.service_prepay_monthly_remain_card_cancle_history, smartbill3.dbo.accinfo_cancel, smartbill3.dbo.accinfo_history 외 4개 | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_BILL.dbo.UPMEM_ACCETC_TRANSFER_CANCEL](../../references/database-contracts.md#db066) | `@COM_NO int IN, @MEM_NO int IN, @PREPAYNO int IN, @ORDER_ID varchar(64) IN, @RESULT varchar(5) OUT` | 쓰기: sb_bill.dbo.cardbilling_transfer_result, sb_bill.dbo.payment, smartbill3.dbo.accinfo_cancel, smartbill3.dbo.company. 참조: sb_bill.dbo.cardbilling_transfer_result, sb_bill.dbo.payment, smartbill3.dbo.accinfo_cancel, smartbill3.dbo.company, smartbill3.dbo.company_history | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.UspBill_PayMentComNo_SELECT](../../references/database-contracts.md#db309) | `@IDX bigint IN` | 확정한 테이블 쓰기 없음. 참조: sb_bill.dbo.payment | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_BILL.dbo.UspBill_PaymentBalanceDepositProcessInfo_INSERT](../../references/database-contracts.md#db077) | `@IDX int IN, @COM_NO int IN, @AMOUNT int IN, @REMARK varchar(200) IN, @SW_NO int IN, @RESULT varchar(1) OUT` | 쓰기: sb_bill.dbo.invoice, sb_bill.dbo.payment, sb_bill.dbo.payment_his, smartbill3.dbo.service_prepay, smartbill3.dbo.service_prepay_his. 참조: sb_bill.dbo.invoice, sb_bill.dbo.payment, sb_bill.dbo.payment_his, smartbill3.dbo.member, smartbill3.dbo.service_prepay, smartbill3.dbo.service_prepay_his | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |

위 DB 계약 링크에는 실제 파라미터 타입·기본값·IN/OUT, Mapper 결과 컬럼, RETURN 바인딩, 참조 테이블·하위 프로시저·정의 필터/정렬을 기록했다. DTO·Service·Repository·Mapper의 상세 호출 경로는 각 API 계약에서 확인한다.

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
|---|---|---|
| 결과가 없거나 기대 건수와 다름 | 적용된 검색 기준·기간·탭·대상 상태·서버 필터·페이징·목록/다운로드 조건 | 조건을 다시 확인하고 조회한다. 지속되면 경로·작업 시각·마스킹한 식별자·필터를 업무/기술 담당에게 전달한다. |
| 메뉴·버튼 미표시 또는 접근 거부 | 사용자 그룹의 메뉴 접근·VIEW 및 API별 PROCESS/EXECUTE/DELETE/EXCEL_DOWNLOAD/UNMASK 등 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. 프런트 버튼 표시만으로 서버 권한을 판단하지 않는다. |
| 저장·삭제·외부 실행의 결과가 불명확 | 대상 현재 상태·중복 요청·감사 이력·API 오류·파일/외부 소비 로그 | 기존 반영 여부를 먼저 조회한다. 중복 발송·초기화·금액 처리를 피하기 위해 기술 담당 확인 후 재시도한다. |

## 7) 검증·출처

**브라우저 검증(2026-11-09)**: 진입 미재현. 목록·기간·회사명 조건에서 상세 진입 가능한 테스트 행을 확보하지 못함. 임의 ID 사용·데이터 생성은 하지 않음. [경로별 결과와 제한](../../references/browser-verification.md#page067). 역할별 권한 거부·저장 성공·파일 반출·외부 연계 완료는 이 결과로 보장하지 않는다.

| 검증 항목 | 근거·환경 | 상태·확인일 |
|---|---|---|
| 대상 선정 | 사용자가 WBS 탭 내용으로 제공한 텍스트의 No. 184; [선정 태스크](../../inventory/wbs-tasks.csv) | 제공 텍스트 확인 2026-11-09. 원본 Excel의 탭/병합 셀을 독립 재열람한 것은 아님. |
| 메뉴·라우트·화면 | [menuConfig.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts); [PaymentRoutes.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/PaymentRoutes.tsx); [PaymentStatusDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/PaymentStatusDetailPage.tsx) | 코드 확인 2026-11-09, 기준 dc216b313 |
| 기능·권한·API | 이 문서의 API 계약 링크 및 연결 Hook/API·Controller·DTO·Service·Repository·Mapper | 코드 확인 2026-11-09. 조회 요청·화면 대조 범위는 아래 브라우저 근거 참조. 권한 계정별 허용·거부 및 변경 요청 실행은 미확인. |
| DB 정의 | [개발 DB 계약](../../references/database-contracts.md), 이 문서의 연결 객체 | 개발 DB 정의 확인 2026-11-09. 동적 SQL·CLR 내부·정의 미공개 참조의 미확정 범위는 객체별 기록; 후속 확인 DB 담당. |
| 브라우저 화면·배포 환경 | 로컬 인증 계정·Playwright CLI; [화면별 검증표](../../references/browser-verification.md#page067) | 진입 미재현, 2026-11-09. 배포본·타 역할·업무 변경 결과는 미확인. |
| 업무 프로시저·쓰기·외부 결과 | 격리된 검증 환경·테스트 데이터의 실행 결과 | 미확인: 명시적인 저장·삭제·발송·초기화 요청은 실행하지 않음. 브라우저 GET의 업무 조회 프로시저·조회수·감사 기록은 별도 영향으로 구분. 격리 환경에서 기술 담당 확인. |

코드 확인과 DB 정의 확인은 실행 성공·업무 승인·다른 환경 적용을 보장하지 않는다. 업무·기술 담당 검토 후 조사 목록의 상태를 완료로 변경한다.

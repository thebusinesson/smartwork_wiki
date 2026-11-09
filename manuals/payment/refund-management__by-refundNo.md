# [서비스 현황] 환불 관리 (상세) 관리자 매뉴얼

작성 기준: `dc216b313` · 확인일 2026-11-09 · 조사 상태 **검토 대기**. 코드와 개발 DB 정의를 확인했으며 실제 화면·업무 실행은 미재현이다.

## 1) 화면 기본 정보

| 항목 | 작성 내용 |
|---|---|
| 업무 도메인·목적 | 환불 신청을 조회·등록하고 환불 가능 금액과 처리 상태를 관리한다. |
| 메뉴·화면 경로 | 서비스 현황 > 입금관리 > 환불 관리; `/payment/refund-management/:refundNo`; 목록에서 선택한 대상의 경로 변수를 유지하여 진입한다. |
| 화면 유형·담당 | 상세; WBS 작업자 유지윤. 업무·기술 담당 팀명은 원문에 없어 배포 전 해당 도메인 담당자가 확정한다. |
| 관련 화면 | [조회·관리](refund-management.md); [등록](refund-management__new.md); [환불 가능 금액 조회](refund-management__inquiry.md) |

WBS 근거: No. 213, 214, 215 (사용자가 제공한 텍스트 행 270, 271, 272). API 개발/화면 개발의 중복 행은 같은 화면으로 통합했다.

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
|---|---|---|
| 화면 진입·조회 | `/payment/refund-management` 메뉴 접근·하위 경로 작업 권한. 조회 API는 VIEW, 등록/수정 경로는 PROCESS 등 아래 서버 액션과 라우트 가드를 함께 적용한다. | 로그인된 관리자 계정; refundNo 식별자는 이전 화면에서 선택한다. |
| 취소 | `/payment/refund-management`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 저장 | `/payment/refund-management`; 화면 게이트 PROCESS. 실제 서버 액션은 API별 표 참조. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 처리내역 작성 | `/payment/refund-management`; 화면 게이트 PROCESS. 실제 서버 액션은 API별 표 참조. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 환불기본정보 수정 | `/payment/refund-management`; 화면 게이트 PROCESS. 실제 서버 액션은 API별 표 참조. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 목록 | `/payment/refund-management`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |

서버가 최종 권한을 검사한다. 버튼 모양(kind)으로 권한을 추정하지 않는다. 특히 등록·수정이 PROCESS를 사용하는 API와 EXECUTE·UNMASK·EXCEL_DOWNLOAD는 서로 구분한다.

## 3) 화면 사용 절차

1. 관련 화면에서 대상 또는 작업을 선택하여 `/payment/refund-management/:refundNo`로 이동한다. 경로 변수는 주소에서 임의로 바꾸지 않고 이전 화면이 전달한 식별자를 사용한다.
2. 대상의 기본 정보·상태·표시 항목을 확인한다. 목록의 식별자와 상세 대상이 일치하는지 확인한다.
3. **저장, 처리내역 작성, 환불기본정보 수정** 중 필요한 작업을 선택한다. 버튼의 표시·활성 조건과 아래 API별 권한을 확인한다. 저장·삭제·외부 호출 전에는 대상과 현재 상태를 재확인한다.
4. 작업 결과 또는 다운로드 파일을 확인하고 관련 목록으로 돌아가 변경된 상태를 다시 조회한다.

**이 화면에서 유의할 업무 규칙**: 목록의 기본 기간은 7일 전~오늘이다. 환불 가능 금액 조회와 신규 등록은 별도 화면이다. 환불 가능 금액은 잔액·사용량·기환불·수수료 등의 규칙이 적용되므로 표시 금액과 상세 이력을 확인한다. 기존 신청의 정보 수정과 상태 변경은 상세 화면에서 수행한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
|---|---|---|---|
| 충전일자 | 출력 | API 타입 String | `chargeDate`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/RefundManagementDetailPage.tsx#L35) |
| 충전금액 | 출력 | API 타입 Long | `chargeAmount`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/RefundManagementDetailPage.tsx#L36) |
| 잔액 | 출력 | API 타입 Long | `balance`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/RefundManagementDetailPage.tsx#L43) |
| 차감율 | 출력 | API 타입 String | `deductionRate`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/RefundManagementDetailPage.tsx#L50) |
| 수수료 | 출력 | API 타입 Long | `fee`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/RefundManagementDetailPage.tsx#L51) |
| 환불가능금액 | 출력 | API 타입 Long | `refundableAmount`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/RefundManagementDetailPage.tsx#L58) |
| 일자 | 출력 | API 타입 String | `date`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/RefundManagementDetailPage.tsx#L68) |
| 상태 | 출력 | API 타입 String | `state`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/RefundManagementDetailPage.tsx#L69) |
| 내용 | 출력 | API 타입 String | `content`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/RefundManagementDetailPage.tsx#L70) |
| 담당자 | 출력 | API 타입 String | `manager`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/RefundManagementDetailPage.tsx#L71) |
| 수수료제외 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/RefundManagementDetailPage.tsx#L299) |

입력 검증 근거: [RefundManagementDetailPage.rules.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/status/payment/RefundManagementDetailPage.rules.ts), [RefundProcessHistoryDialog.schema.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/status/payment/components/RefundProcessHistoryDialog.schema.ts). 프런트 검증과 서버 DTO 제약이 다르면 서버 검증이 최종 기준이다.

화면 필드 키와 API 필드명이 다른 경우 변환은 Hook/API의 검색·저장 매핑에서 수행된다. 요청·응답 필드와 DB 컬럼 매핑은 아래 API 계약 및 DB 객체 계약에 연결했다.

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
|---|---|---|---|
| 환불 상세 조회 | [GET /api/v1/service-status/deposits/refunds/{refundNo}](../../references/api-contracts.md#api108); `/payment/refund-management` / `VIEW` | `경로·쿼리·본문 계약 참조` → `basicInfo, refundInfo, chargeDetails, histories, refundDate, refundState, companyName, businessNumber, managerName, contactNumber, refundBank, refundAccount, totalBalance, totalRef` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 환불 정보 수정 | [PUT /api/v1/service-status/deposits/refunds/{refundNo}](../../references/api-contracts.md#api267); `/payment/refund-management` / `PROCESS` | `refundState, refundBank, refundAccount, refundAmount, totalRefundableAmount` → `success, message` | 쓰기 대상 smartbill3.dbo.service_refund, smartbill3.dbo.service_refund_his |
| 환불 상태 변경 | [POST /api/v1/service-status/deposits/refunds/{refundNo}/state-change](../../references/api-contracts.md#api229); `/payment/refund-management` / `PROCESS` | `refundState, content, charge, prepayArray` → `success, message` | 쓰기 대상 sb_dti.dbo.dti_header_cub, sb_dti.dbo.dti_header_detail, sb_dti.dbo.dti_item, sb_dti.dbo.dti_paymethod, sb_dti.dbo.dti_sequence01, sb_dti.dbo.dti_sequence02, sb_dti.dbo.dti_status_his, smartbill3.dbo.service_prepay, smartbill3.dbo.service_prepay_his, smartbill3.dbo.service_refund, smartbill3.dbo.service_refund_his |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
|---|---|---|---|
| [smartwork.dbo.UspBill_RefundHistoryInfo](../../references/database-contracts.md#db316) | `@REFUND_NO int IN` | 확정한 테이블 쓰기 없음. 참조: office.dbo.sawon, smartbill3.dbo.service_refund_his | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Sb_Bill.dbo.UspBill_RefundDetail_SELECT](../../references/database-contracts.md#db082) | `@COM_NO varchar(10) IN, @PREPAY_NO int IN, @REFUND_DATE varchar(10) IN` | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.service_prepay, smartbill3.dbo.service_prepay_his | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.UspBill_RefundChargeDetail_SELECT](../../references/database-contracts.md#db314) | `@COM_NO int IN, @REFUND_DATE varchar(10) IN, @GROUP_NO varchar(10) IN, @PREPAY_NO varchar(16) IN` | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.service_prepay, smartbill3.dbo.service_prepay_his | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Sb_Bill.dbo.UspBill_RefundInfo_SELECT](../../references/database-contracts.md#db084) | `@REFUND_NO int IN` | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.company, smartbill3.dbo.service_prepay, smartbill3.dbo.service_prepay_his, smartbill3.dbo.service_refund | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Sb_Bill.dbo.UspBill_RefundInfo_UPDATE](../../references/database-contracts.md#db085) | `@REFUND_NO int IN, @REQUEST_AMT varchar(30) IN, @ACC_NO varchar(30) IN, @ACC_NAME varchar(30) IN, @SW_ID varchar(30) IN, @RESULT varchar(1) OUT` | 쓰기: smartbill3.dbo.service_refund, smartbill3.dbo.service_refund_his. 참조: smartbill3.dbo.service_refund, smartbill3.dbo.service_refund_his | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [sb_bill.dbo.UspBill_Refund_Create_Dti](../../references/database-contracts.md#db079) | `@COM_NO int IN, @REFUND_AMOUNT int IN, @ERR_CODE int OUT` | 쓰기: sb_dti.dbo.dti_header_cub, sb_dti.dbo.dti_header_detail, sb_dti.dbo.dti_item, sb_dti.dbo.dti_paymethod, sb_dti.dbo.dti_sequence01, sb_dti.dbo.dti_sequence02, sb_dti.dbo.dti_status_his. 참조: sb_dti.dbo.bizplace, sb_dti.dbo.bizplace_member, sb_dti.dbo.dti_header_cub, sb_dti.dbo.dti_header_cub_2023_07, sb_dti.dbo.dti_header_cub_part, sb_dti.dbo.dti_header_cub_prev_buffer, sb_dti.dbo.dti_header_detail, sb_dti.dbo.dti_header_detail_2023_07 외 20개 | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Sb_Bill.dbo.UspBill_RefundStateInfo_UPDATE](../../references/database-contracts.md#db086) | `@REFUND_NO int IN, @REFUND_STATE varchar(2) IN, @CONTENT varchar(200) IN, @SW_ID varchar(30) IN, @CHARGE money IN, @PREPAY_ARRAY varchar(500) IN, @RESULT varchar(1) OUT` | 쓰기: smartbill3.dbo.service_prepay, smartbill3.dbo.service_prepay_his, smartbill3.dbo.service_refund, smartbill3.dbo.service_refund_his. 참조: smartbill3.dbo.service_prepay, smartbill3.dbo.service_prepay_his, smartbill3.dbo.service_refund, smartbill3.dbo.service_refund_his | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |

위 DB 계약 링크에는 실제 파라미터 타입·기본값·IN/OUT, Mapper 결과 컬럼, RETURN 바인딩, 참조 테이블·하위 프로시저·정의 필터/정렬을 기록했다. DTO·Service·Repository·Mapper의 상세 호출 경로는 각 API 계약에서 확인한다.

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
|---|---|---|
| 결과가 없거나 기대 건수와 다름 | 적용된 검색 기준·기간·탭·대상 상태·서버 필터·페이징·목록/다운로드 조건 | 조건을 다시 확인하고 조회한다. 지속되면 경로·작업 시각·마스킹한 식별자·필터를 업무/기술 담당에게 전달한다. |
| 메뉴·버튼 미표시 또는 접근 거부 | 사용자 그룹의 메뉴 접근·VIEW 및 API별 PROCESS/EXECUTE/DELETE/EXCEL_DOWNLOAD/UNMASK 등 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. 프런트 버튼 표시만으로 서버 권한을 판단하지 않는다. |
| 저장·삭제·외부 실행의 결과가 불명확 | 대상 현재 상태·중복 요청·감사 이력·API 오류·파일/외부 소비 로그 | 기존 반영 여부를 먼저 조회한다. 중복 발송·초기화·금액 처리를 피하기 위해 기술 담당 확인 후 재시도한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
|---|---|---|
| 대상 선정 | 사용자가 WBS 탭 내용으로 제공한 텍스트의 No. 213, 214, 215; [선정 태스크](../../inventory/wbs-tasks.csv) | 제공 텍스트 확인 2026-11-09. 원본 Excel의 탭/병합 셀을 독립 재열람한 것은 아님. |
| 메뉴·라우트·화면 | [menuConfig.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts); [PaymentRoutes.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/PaymentRoutes.tsx); [RefundManagementDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/RefundManagementDetailPage.tsx) | 코드 확인 2026-11-09, 기준 dc216b313 |
| 기능·권한·API | 이 문서의 API 계약 링크 및 연결 Hook/API·Controller·DTO·Service·Repository·Mapper | 코드 확인 2026-11-09. 요청 실행·권한 계정별 재현은 미확인. |
| DB 정의 | [개발 DB 계약](../../references/database-contracts.md), 이 문서의 연결 객체 | 개발 DB 정의 확인 2026-11-09. 동적 SQL·CLR 내부·정의 미공개 참조의 미확정 범위는 객체별 기록; 후속 확인 DB 담당. |
| 브라우저 화면·배포 환경 | 실제 검증 계정의 정상·빈 결과·권한 부족·입력 오류 및 현재 배포본 | 미확인: 브라우저 실행 검증을 수행하지 않음. 배포 전 업무 담당·QA·기술 담당 확인. |
| 업무 프로시저·쓰기·외부 결과 | 격리된 검증 환경·테스트 데이터의 실행 결과 | 미확인: 공유 개발 DB의 업무 프로시저·쓰기·발송을 실행하지 않음. 격리 환경에서 기술 담당 확인. |

코드 확인과 DB 정의 확인은 실행 성공·업무 승인·다른 환경 적용을 보장하지 않는다. 업무·기술 담당 검토 후 조사 목록의 상태를 완료로 변경한다.

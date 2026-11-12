# [SB 서비스관리] 세금계산서 조회 (조회·관리) 관리자 매뉴얼

작성 기준: `dc216b313` · 확인일 2026-11-09 · 조사 상태 **검토 대기**. 코드·개발 DB 정의 확인. 브라우저: **화면 대조**; 저장·발송 등 업무 실행 결과는 미검증이다.

## 1) 화면 기본 정보

### 도메인 이해

보나뱅크 세금계산서 목록에서 거래 문서를 찾고, 문서 상세 조사 또는 선택 문서의 일괄 메일 발송·목록 반출을 수행한다.

| 구분 | 설명 |
|---|---|
| 업무 영역 | 보나뱅크 서비스 운영 > 세금계산서 조회 조회·관리 |
| 언제 사용하는가 | 보나뱅크 세금계산서의 발행·수신 상태나 메일 관련 문의를 받았을 때 |
| 주요 대상·데이터 | 보나뱅크 문서의 작성일·거래처·상태·참조번호 등 검색/표시 정보와 메일 발송할 선택 문서·수신 이메일, 다운로드 조건·사유가 대상이다. |
| 업무 흐름 | 문서 조건 검색 → 행 선택으로 상세 조사 또는 발송 가능한 문서 선택 → 수신 이메일·권한·조건 확인 → 일괄 발송 결과 확인 |
| 이 페이지의 역할 | 보나뱅크 세금계산서 목록에서 거래 문서를 찾고, 문서 상세 조사 또는 선택 문서의 일괄 메일 발송·목록 반출을 수행한다. |
| 판단 결과·다음 업무 | 목록에서 일괄 메일 발송 팝업을 열고 입력한 주소로 선택 문서 발송을 요청할 수 있다. 성공/실패 건수와 상세 이력을 구분하며 발송 응답을 최종 수신 완료로 단정하지 않는다. 반출은 별도 권한·사유를 따른다. |
| 다른 화면과의 구분 | 상세는 한 문서의 본문·연계·이력을 조사하는 단계이고 일괄 메일 발송은 목록의 별도 작업이다. 현행·과거·보나뱅크 문서 원천과 상세 진입 경로를 유지한다. |

설명 근거: [BonabankTaxInvoiceListPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/BonabankTaxInvoiceListPage.tsx), 이 문서 4·5·7번의 항목·API·업무 규칙. [상위 업무 영역](../../references/domain-overview.md#bonabank)은 공통 배경이며 현재 화면의 데이터·동작은 위 설명을 따른다. 설명 수정일 **2026-11-10**; 새 업무 실행 검증을 수행한 것은 아니다.

### 화면 정보

| 항목 | 작성 내용 |
|---|---|
| 업무 도메인·목적 | 보나뱅크 세금계산서 목록에서 거래 문서를 찾고, 문서 상세 조사 또는 선택 문서의 일괄 메일 발송·목록 반출을 수행한다. |
| 메뉴·화면 경로 | SB 서비스관리 > 보나뱅크 > 세금계산서 조회; `/bonabank/tax-invoice`; 메뉴 또는 관련 화면에서 진입한다. |
| 화면 유형·담당 | 조회·관리; WBS 작업자 유지윤. 업무·기술 담당 팀명은 원문에 없어 배포 전 해당 도메인 담당자가 확정한다. |
| 관련 화면 | [상세](tax-invoice__by-dtiIdx.md) |

WBS 근거: No. 142, 143 (사용자가 제공한 텍스트 행 178, 179). API 개발/화면 개발의 중복 행은 같은 화면으로 통합했다.

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
|---|---|---|
| 화면 진입·조회 | `/bonabank/tax-invoice` 메뉴 접근·하위 경로 작업 권한. 조회 API는 VIEW, 등록/수정 경로는 PROCESS 등 아래 서버 액션과 라우트 가드를 함께 적용한다. | 로그인된 관리자 계정; 아래 검색·입력 항목을 준비한다. |
| 일괄 메일 발송 | `/bonabank/tax-invoice`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 다운로드 | `/bonabank/tax-invoice`; 엑셀 download 화면 게이트. 다운로드/업로드 API의 서버 권한과 사유 입력을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |

서버가 최종 권한을 검사한다. 버튼 모양(kind)으로 권한을 추정하지 않는다. 특히 등록·수정이 PROCESS를 사용하는 API와 EXECUTE·UNMASK·EXCEL_DOWNLOAD는 서로 구분한다.

## 3) 화면 사용 절차

**검증 시 화면 버튼**: 검색, 초기화, 다운로드. 화면 상태·대상에 따라 달라지며 아래 작업 절차와 권한 조건을 함께 확인한다.

**현재 상세 이동**: `BonabankTaxInvoiceListPage`의 행 선택은 `/tax-invoice/tax-invoice/:id?wday=...` 공통 상세로 이동한다. `/bonabank/tax-invoice/:dtiIdx`도 라우트에 등록되어 있지만 현재 목록의 기본 진입 경로는 아니다. 실제 행에서 받은 문서 ID와 `wday`를 유지한다. 보나뱅크 상세 경로를 공통 상세와 별개로 검사한 결과는 검증표에서 구분한다.

1. `SB 서비스관리 > 보나뱅크 > 세금계산서 조회` 메뉴를 연다. 경로 변수는 주소에서 임의로 바꾸지 않고 이전 화면이 전달한 식별자를 사용한다.
2. 현재 검색 조건과 아래 기본값을 확인한다. **날짜 조건, 공급자, 공급받는자, 공급받는자명, 참조번호, 문서 상태, 수신 이메일** 항목에 필요한 값을 입력하고 **검색**을 누른다.
3. 결과 행에서 업무 대상을 선택하여 관련 상세 화면으로 이동한다. 페이지 이동·검색 조건 변경 후에는 현재 조건과 조회 대상을 다시 확인한다.

**이 화면에서 유의할 업무 규칙**: 공급자 또는 공급받는자 조건 중 필요한 값을 입력하여 검색한다. 상세에서 문서·담당자·전송 정보를 확인하고 재발송 시 수신 이메일을 검증한다.

**반출**: 적용된 검색 조건과 반출 범위를 확인한 후 다운로드한다. 사유 입력창이 표시되면 업무 사유를 입력한다. 사유 등록 실패·파일 오류는 성공으로 간주하지 않고 다운로드 결과를 확인한다.

## 4) 입력·표시 데이터

**검증 시 표시된 날짜 필터**: 시작일 `2026-03-01`, 종료일 `2026-11-09`. 검증 날짜·조건 복원에 따른 표시값이며 모든 실행의 고정 기본값을 뜻하지 않는다.

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
|---|---|---|---|
| 날짜 조건 | 입력·선택(조건부 검증 별도) | 화면 타입 selectWithDateRange; 선택: 전체=ALL, 작성 일자=WRITE_DATE, 발행일자=ISSUE_DATE; 초기값 selectValue=WRITE_DATE; dateRange=startDate={formatDate(start)}; endDate={formatDate(end)} | `dateCondition`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/BonabankTaxInvoiceListPage.tsx#L232) |
| 공급자 | 입력·선택(조건부 검증 별도) | 화면 타입 selectWithInput; 선택: 전체=ALL, 사업자번호=BUSINESS_NUMBER, 회사명=COMPANY_NAME; 초기값 selectValue=BUSINESS_NUMBER; inputValue=빈값 | `supplierCondition`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/BonabankTaxInvoiceListPage.tsx#L247) |
| 공급받는자 | 입력·선택(조건부 검증 별도) | 화면 타입 selectWithInput; 선택: 전체=ALL, 사업자번호=BUSINESS_NUMBER, 회사명=COMPANY_NAME; 초기값 selectValue=BUSINESS_NUMBER; inputValue=빈값 | `buyerCondition`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/BonabankTaxInvoiceListPage.tsx#L279) |
| 공급받는자명 | 입력·선택(조건부 검증 별도) | 화면 타입 toggleableText; 최대 20자; API 타입 String?; 기본 null; 서버 검증 @field:Size(max = 20, message = "buyerNickname 은 20자 이하여야 합니다."); 초기값 isAll=켜짐; inputValue=빈값; 입력 안내 닉네임을 입력하세요. | `buyerNickname`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/BonabankTaxInvoiceListPage.tsx#L310) |
| 참조번호 | 입력·선택(조건부 검증 별도) | 화면 타입 toggleableText; 최대 35자; API 타입 String?; 기본 null; 서버 검증 @field:Size(max = 35, message = "referenceNumber 는 35자 이하여야 합니다."); 초기값 isAll=켜짐; inputValue=빈값; 입력 안내 참조번호를 입력하세요. | `referenceNumber`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/BonabankTaxInvoiceListPage.tsx#L325) |
| 문서 상태 | 입력·선택(조건부 검증 별도) | 화면 타입 radio; API 타입 String?; 기본 null; 서버 검증 @field:Pattern; 선택: 전체=ALL, 역발행 요청=REVERSE_REQUESTED, 역발행 거부=REVERSE_REJECTED, 관리자 발행 요청=ADMIN_REQUESTED, 관리자 발행 거부=ADMIN_REJECTED, 수신미승인=PENDING, 수신승인=APPROVED, 수신거부=REJECTED, 발행취소 요청=CANCEL_REQUESTED, 취소 완료=CANCELLED, 발행예정=SCHEDULED, 발행예정 취소=SCHEDULE_CANCELLED, 발행예정 승인=SCHEDULE_APPROVED, 발행예정 거부=SCHEDULE_REJECTED, 저장=DRAFT; 초기값 ALL | `documentStatus`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/BonabankTaxInvoiceListPage.tsx#L339) |
| 작성일자 | 출력 | API 타입 String? | `writeDate`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/BonabankTaxInvoiceListPage.tsx#L501) |
| 발행일자 | 출력 | API 타입 String? | `issueDate`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/BonabankTaxInvoiceListPage.tsx#L508) |
| 공급가액 | 출력 | API 타입 Long | `supplyAmount`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/BonabankTaxInvoiceListPage.tsx#L612) |
| 상태 | 출력 | API 타입 String? | `statusLabel`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/BonabankTaxInvoiceListPage.tsx#L632) |
| 수신 이메일 | 입력·선택(조건부 검증 별도) | 최대 100자 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/BonabankTaxInvoiceListPage.tsx#L801) |

입력 검증 근거: [BonabankTaxInvoiceListPage.checks.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/service/bonabank/BonabankTaxInvoiceListPage.checks.ts), [BonabankTaxInvoiceListPage.schema.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/service/bonabank/BonabankTaxInvoiceListPage.schema.ts). 프런트 검증과 서버 DTO 제약이 다르면 서버 검증이 최종 기준이다.

**복합 검색·폼의 초기 상태**

| 초기값 근거 | 기본 상태 |
|---|---|
| [buildDefaultFilters](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/BonabankTaxInvoiceListPage.tsx#L45) | dateCondition=selectValue=WRITE_DATE; dateRange=startDate={formatDate(start)}; endDate={formatDate(end)}; supplierCondition=selectValue=BUSINESS_NUMBER; inputValue=빈값; buyerCondition=selectValue=BUSINESS_NUMBER; inputValue=빈값; buyerNickname=isAll=켜짐; inputValue=빈값; referenceNumber=isAll=켜짐; inputValue=빈값; documentStatus=ALL |

화면 필드 키와 API 필드명이 다른 경우 변환은 Hook/API의 검색·저장 매핑에서 수행된다. 요청·응답 필드와 DB 컬럼 매핑은 아래 API 계약 및 DB 객체 계약에 연결했다.

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
|---|---|---|---|
| 보나뱅크 세금계산서 목록 (SP-side 페이징) | [GET /api/v1/bonabank/tax-invoices](../../references/api-contracts.md#api025); `/bonabank/tax-invoice` / `VIEW` | `dateConditionType, startDate, endDate, supplierConditionType, supplierConditionValue, buyerConditionType, buyerConditionValue, buyerNickname, referenceNumber, documentStatus, page,` → `content, totalElements, totalPages, page, size, rowNumber, dtiIdx, writeDate, issueDate, ntsSendDate, supplierBusinessNumber, supplierCompanyName, buyerBusinessNumber, buyerCompany` | Mapper 프로시저의 정적 테이블 쓰기 미검출; 동적 SQL의 런타임 대상은 미확정 |
| 보나뱅크 세금계산서 엑셀 다운로드 | [GET /api/v1/bonabank/tax-invoices/download](../../references/api-contracts.md#api026); `/bonabank/tax-invoice` / `EXCEL_DOWNLOAD` | `dateConditionType, startDate, endDate, supplierConditionType, supplierConditionValue, buyerConditionType, buyerConditionValue, buyerNickname, referenceNumber, documentStatus, page,` → `응답 DTO·파일/처리 결과 계약 참조` | Mapper 프로시저의 정적 테이블 쓰기 미검출; 동적 SQL의 런타임 대상은 미확정 |
| 메일 발송 (통합) | [POST /api/v1/mail/send](../../references/api-contracts.md#api220); `/bonabank/tax-invoice` / `PROCESS` | `mailType, ids, items, emailAddress, title, emailContent, targetId` → `isAllSuccess, successCount, failedCount, message` | 쓰기 대상 office.dbo.servicemail_send, sb_dti_log.dbo.dti_customer_pwd |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
|---|---|---|---|
| [smartwork.dbo.upSBAdm_LstDTI_Bona](../../references/database-contracts.md#db278) | `@PAGE int IN, @TOP int IN, @DATE_TYPE char(1) IN, @FMDATE varchar(10) IN, @TODATE varchar(10) IN, @SUP_INDEX varchar(20) IN, @SUP_TEXT varchar(70) IN, @BYR_INDEX varchar(20) IN, @BYR_TEXT varchar(70) IN, @REF_ID varchar(35) IN, @STATUS char(1) IN, @BYR_NAME varchar(20) IN` | 확정한 테이블 쓰기 없음. 참조: migration_etcasp.dbo.migration_mapping_company, sb_common.dbo.free_service, sb_dti.dbo.dti_header_cub, sb_dti.dbo.dti_header_cub_2023_07, sb_dti.dbo.dti_header_cub_part, sb_dti.dbo.dti_header_cub_prev_buffer, sb_dti.dbo.dti_header_detail, sb_dti.dbo.dti_header_detail_2023_07 외 6개 동적 SQL 포함, 런타임 조합 대상 미확정. | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.upSBAdm_LstDTI_Bona_excel](../../references/database-contracts.md#db279) | `@DATE_TYPE char(1) IN, @FMDATE varchar(10) IN, @TODATE varchar(10) IN, @SUP_INDEX varchar(20) IN, @SUP_TEXT varchar(70) IN, @BYR_INDEX varchar(20) IN, @BYR_TEXT varchar(70) IN, @REF_ID varchar(35) IN, @STATUS char(1) IN, @BYR_NAME varchar(20) IN` | 확정한 테이블 쓰기 없음. 참조: migration_etcasp.dbo.migration_mapping_company, sb_common.dbo.free_service, sb_dti.dbo.dti_header_cub, sb_dti.dbo.dti_header_cub_2023_07, sb_dti.dbo.dti_header_cub_part, sb_dti.dbo.dti_header_cub_prev_buffer, sb_dti.dbo.dti_header_detail, sb_dti.dbo.dti_header_detail_2023_07 외 6개 동적 SQL 포함, 런타임 조합 대상 미확정. | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SMARTBILL3.dbo.CMS_EA22](../../references/database-contracts.md#db194) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.cms_ea22 | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SMARTBILL3.dbo.CMS_EA22_DETAIL_CUB](../../references/database-contracts.md#db195) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.cms_ea22_detail_cub | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SMARTBILL3.dbo.COMPANY](../../references/database-contracts.md#db197) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.company | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SMARTBILL3.dbo.MEMBER](../../references/database-contracts.md#db203) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.member | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SMARTBILL3.dbo.COMMON_CODE](../../references/database-contracts.md#db196) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.common_code | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_BILL.dbo.BILL_COMMON_CODE](../../references/database-contracts.md#db063) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: sb_bill.dbo.bill_common_code | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SMARTBILL3.dbo.CMS_EA14_DETAIL_CUB](../../references/database-contracts.md#db193) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.cms_ea14_detail_cub | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SMARTBILL3.dbo.CMS_EA14](../../references/database-contracts.md#db192) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.cms_ea14 | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [OFFICE.dbo.upSM_mailSend_Insert](../../references/database-contracts.md#db061) | `@TITLE varchar(100) IN, @CONTENT text IN, @CUSER varchar(20) IN, @RESULT int OUT` | 쓰기: office.dbo.servicemail_send. 참조: office.dbo.servicemail_send | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [OFFICE.dbo.upSM_mailSendList](../../references/database-contracts.md#db062) | `@DIV varchar(10) IN` | 확정한 테이블 쓰기 없음. 참조: office.dbo.servicemail | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_COMMON.dbo.upSBAdm_LstDTI04](../../references/database-contracts.md#db102) | `@DTI_WDAY varchar(10) IN, @DTI_IDX int IN` | 쓰기: sb_dti_log.dbo.dti_customer_pwd. 참조: sb_dti.dbo.dti_header_cub, sb_dti.dbo.dti_header_cub_2023_07, sb_dti.dbo.dti_header_cub_part, sb_dti.dbo.dti_header_cub_prev_buffer, sb_dti_log.dbo.dti_customer_pwd, sb_dti_log.dbo.v_dti_customer_pwd | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DTI.dbo.DTI_HEADER_CUB](../../references/database-contracts.md#db139) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: sb_dti.dbo.dti_header_cub, sb_dti.dbo.dti_header_cub_2023_07, sb_dti.dbo.dti_header_cub_part, sb_dti.dbo.dti_header_cub_prev_buffer | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_COMMON.dbo.upSBAdm_LstDTI04_DW](../../references/database-contracts.md#db103) | `@DTI_WDAY varchar(10) IN, @DTI_IDX int IN` | 쓰기: sb_dti_log.dbo.dti_customer_pwd. 참조: sb_dti.dbo.dti_header_cub_2020_01, sb_dti.dbo.dti_header_cub_2020_02, sb_dti.dbo.dti_header_cub_2020_03, sb_dti.dbo.dti_header_cub_2020_04, sb_dti.dbo.dti_header_cub_2020_05, sb_dti.dbo.dti_header_cub_2020_06, sb_dti.dbo.dti_header_cub_2020_07, sb_dti.dbo.dti_header_cub_2020_08 외 37개 | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DTI_DW.dbo.DTI_HEADER_CUB](../../references/database-contracts.md#db157) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: sb_dti.dbo.dti_header_cub_2020_01, sb_dti.dbo.dti_header_cub_2020_02, sb_dti.dbo.dti_header_cub_2020_03, sb_dti.dbo.dti_header_cub_2020_04, sb_dti.dbo.dti_header_cub_2020_05, sb_dti.dbo.dti_header_cub_2020_06, sb_dti.dbo.dti_header_cub_2020_07, sb_dti.dbo.dti_header_cub_2020_08 외 35개 | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |

위 DB 계약 링크에는 실제 파라미터 타입·기본값·IN/OUT, Mapper 결과 컬럼, RETURN 바인딩, 참조 테이블·하위 프로시저·정의 필터/정렬을 기록했다. DTO·Service·Repository·Mapper의 상세 호출 경로는 각 API 계약에서 확인한다.

**메일 연계**: mailType과 문서/수신 대상을 확인한다. 서버는 유형별 권한을 검사하고 메시지 브로커에 발행할 수 있다. API 응답이 실제 수신 완료를 보장하지 않으므로 실패 시 발송·소비 로그를 확인한 뒤 재시도한다.

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
|---|---|---|
| 검색 결과가 존재하지 않습니다. | [문구·처리 코드](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/BonabankTaxInvoiceListPage.tsx#L697); 현재 조건·대상·권한 확인 | 검색·조회 오류면 조건을 확인 후 재조회. 변경·발송 결과가 불명확하면 처리 여부와 이력을 확인한 뒤 재시도 여부를 판단한다. |
| 결과가 없거나 기대 건수와 다름 | 적용된 검색 기준·기간·탭·대상 상태·서버 필터·페이징·목록/다운로드 조건 | 조건을 다시 확인하고 조회한다. 지속되면 경로·작업 시각·마스킹한 식별자·필터를 업무/기술 담당에게 전달한다. |
| 메뉴·버튼 미표시 또는 접근 거부 | 사용자 그룹의 메뉴 접근·VIEW 및 API별 PROCESS/EXECUTE/DELETE/EXCEL_DOWNLOAD/UNMASK 등 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. 프런트 버튼 표시만으로 서버 권한을 판단하지 않는다. |
| 저장·삭제·외부 실행의 결과가 불명확 | 대상 현재 상태·중복 요청·감사 이력·API 오류·파일/외부 소비 로그 | 기존 반영 여부를 먼저 조회한다. 중복 발송·초기화·금액 처리를 피하기 위해 기술 담당 확인 후 재시도한다. |

## 7) 검증·출처

**브라우저 검증(2026-11-09)**: 화면 대조. [경로별 결과와 제한](../../references/browser-verification.md#page047). 역할별 권한 거부·저장 성공·파일 반출·외부 연계 완료는 이 결과로 보장하지 않는다.

| 검증 항목 | 근거·환경 | 상태·확인일 |
|---|---|---|
| 대상 선정 | 사용자가 WBS 탭 내용으로 제공한 텍스트의 No. 142, 143; [선정 태스크](../../inventory/wbs-tasks.csv) | 제공 텍스트 확인 2026-11-09. 원본 Excel의 탭/병합 셀을 독립 재열람한 것은 아님. |
| 메뉴·라우트·화면 | [menuConfig.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts); [BonabankRoutes.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/BonabankRoutes.tsx); [BonabankTaxInvoiceListPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/BonabankTaxInvoiceListPage.tsx) | 코드 확인 2026-11-09, 기준 dc216b313 |
| 기능·권한·API | 이 문서의 API 계약 링크 및 연결 Hook/API·Controller·DTO·Service·Repository·Mapper | 코드 확인 2026-11-09. 조회 요청·화면 대조 범위는 아래 브라우저 근거 참조. 권한 계정별 허용·거부 및 변경 요청 실행은 미확인. |
| DB 정의 | [개발 DB 계약](../../references/database-contracts.md), 이 문서의 연결 객체 | 개발 DB 정의 확인 2026-11-09. 동적 SQL·CLR 내부·정의 미공개 참조의 미확정 범위는 객체별 기록; 후속 확인 DB 담당. |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-57eb528727f36c04) | Demo 메타데이터 16/16개 확인 · Dev와 계약 차이 3개 · 2026-11-11 |
| 브라우저 화면·배포 환경 | 로컬 인증 계정·Playwright CLI; [화면별 검증표](../../references/browser-verification.md#page047) | 화면 대조, 2026-11-09. 배포본·타 역할·업무 변경 결과는 미확인. |
| 업무 프로시저·쓰기·외부 결과 | 격리된 검증 환경·테스트 데이터의 실행 결과 | 미확인: 명시적인 저장·삭제·발송·초기화 요청은 실행하지 않음. 브라우저 GET의 업무 조회 프로시저·조회수·감사 기록은 별도 영향으로 구분. 격리 환경에서 기술 담당 확인. |

코드 확인과 DB 정의 확인은 실행 성공·업무 승인·다른 환경 적용을 보장하지 않는다. 업무·기술 담당 검토 후 조사 목록의 상태를 완료로 변경한다.

브라우저 직접 근거: [test-company-search](../../evidence/browser/targeted-stable.json). 경로·고정 버튼명·입력 속성·표 머리글·API 상태를 보관했고 실제 데이터 값·식별자·인증정보는 제외했다.

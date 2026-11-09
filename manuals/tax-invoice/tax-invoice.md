# [SB 서비스관리] 세금계산서 조회 (조회·관리) 관리자 매뉴얼

작성 기준: `dc216b313` · 확인일 2026-11-09 · 조사 상태 **검토 대기**. 코드·개발 DB 정의 확인. 브라우저: **화면 대조**; 저장·발송 등 업무 실행 결과는 미검증이다.

## 1) 화면 기본 정보

| 항목 | 작성 내용 |
|---|---|
| 업무 도메인·목적 | 현행 세금계산서와 연결·단독 거래명세서를 검색하고 문서 상세·메일·원본 파일을 확인한다. |
| 메뉴·화면 경로 | SB 서비스관리 > 전자세금계산서 > 세금계산서 조회; `/tax-invoice/tax-invoice`; 메뉴 또는 관련 화면에서 진입한다. |
| 화면 유형·담당 | 조회·관리; WBS 작업자 유지윤. 업무·기술 담당 팀명은 원문에 없어 배포 전 해당 도메인 담당자가 확정한다. |
| 관련 화면 | [상세](tax-invoice__by-id.md); [(단독) 거래명세서 상세](tax-invoice__statement__by-id.md) |

WBS 근거: No. 43, 44, 45, 46, 47 (사용자가 제공한 텍스트 행 69, 70, 71, 72, 73). API 개발/화면 개발의 중복 행은 같은 화면으로 통합했다.

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
|---|---|---|
| 화면 진입·조회 | `/tax-invoice/tax-invoice` 메뉴 접근·하위 경로 작업 권한. 조회 API는 VIEW, 등록/수정 경로는 PROCESS 등 아래 서버 액션과 라우트 가드를 함께 적용한다. | 로그인된 관리자 계정; 아래 검색·입력 항목을 준비한다. |
| 일괄 메일 발송 | `/tax-invoice/tax-invoice`; 화면 게이트 PROCESS. 실제 서버 액션은 API별 표 참조. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 다운로드 | `/tax-invoice/tax-invoice`; 엑셀 download 화면 게이트. 다운로드/업로드 API의 서버 권한과 사유 입력을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |

서버가 최종 권한을 검사한다. 버튼 모양(kind)으로 권한을 추정하지 않는다. 특히 등록·수정이 PROCESS를 사용하는 API와 EXECUTE·UNMASK·EXCEL_DOWNLOAD는 서로 구분한다.

## 3) 화면 사용 절차

**검증 시 화면 버튼**: 검색, 초기화, 다운로드. 화면 상태·대상에 따라 달라지며 아래 작업 절차와 권한 조건을 함께 확인한다.

1. `SB 서비스관리 > 전자세금계산서 > 세금계산서 조회` 메뉴를 연다. 경로 변수는 주소에서 임의로 바꾸지 않고 이전 화면이 전달한 식별자를 사용한다.
2. 최초 진입 시 자동조회하지 않는다. 아래 검색 항목을 입력한 후 **검색**을 누른다.
3. 결과 행에서 업무 대상을 선택하여 관련 상세 화면으로 이동한다. 페이지 이동·검색 조건 변경 후에는 현재 조건과 조회 대상을 다시 확인한다.

**이 화면에서 유의할 업무 규칙**: 날짜 조건과 공급자/공급받는자·참조번호·승인번호 등을 입력한다. 참조번호·승인번호 셀은 번호 복사 동작이므로 상세 이동과 구분한다. 선택 문서의 일괄 메일 발송은 전송 대상·주소를 확인하고 수행한다. document=transaction-statement 분기와 독립 statement 경로는 같은 문서 종류라도 진입 방식이 다르다.

**반출**: 적용된 검색 조건과 반출 범위를 확인한 후 다운로드한다. 사유 입력창이 표시되면 업무 사유를 입력한다. 사유 등록 실패·파일 오류는 성공으로 간주하지 않고 다운로드 결과를 확인한다.

## 4) 입력·표시 데이터

**검증 시 표시된 날짜 필터**: 시작일 `2026-10-10`, 종료일 `2026-11-09`, YYYY-MM-DD `2026-10-10`. 검증 날짜·조건 복원에 따른 표시값이며 모든 실행의 고정 기본값을 뜻하지 않는다.

**조회 기간 기본값(코드·브라우저 대조)**: 현행은 오늘 기준 한 달 전의 다음 날부터 오늘까지, 과거는 13개월 전 달의 1일부터 말일까지다. 2026-11-09 검증 시 현행은 2026-10-10~2026-11-09, 과거는 2025-10-01~2025-10-31이다. 검색 조건 복원 시 이전 값이 표시될 수 있다.

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
|---|---|---|---|
| 날짜 조건 | 입력·선택(조건부 검증 별도) | 화면 타입 selectWithDateRange; API 타입 String?; 선택: 작성 일자=created-date, 발행 일자=issue-date; 초기값 selectValue=created-date; dateRange={useMemo(() => getTaxInvoiceDefaultDateRange('current'), [])} | `issuanceCondition`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TaxInvoiceListPage.tsx#L199) |
| 공급자 | 입력·선택(조건부 검증 별도) | 화면 타입 selectWithInput; 선택: 전체=ALL, 사업자번호=business-number, 회사명=company-name; 초기값 selectValue=business-number; inputValue=빈값 | `supplier`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TaxInvoiceListPage.tsx#L213) |
| 공급받는자 | 입력·선택(조건부 검증 별도) | 화면 타입 selectWithInput; 선택: 전체=ALL, 사업자번호=business-number, 회사명=company-name; 초기값 selectValue=business-number; inputValue=빈값 | `buyer`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TaxInvoiceListPage.tsx#L232) |
| 공급받는자명 | 입력·선택(조건부 검증 별도) | 화면 타입 selectWithInput; 선택: 전체=ALL, 닉네임=nickname, 이메일=email; 초기값 selectValue=nickname; inputValue=빈값 | `buyerName`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TaxInvoiceListPage.tsx#L250) |
| 수탁자 (발행자) | 입력·선택(조건부 검증 별도) | 화면 타입 selectWithInput; 선택: 전체=ALL, 사업자번호=business-number, 회사명=company-name; 초기값 selectValue=business-number; inputValue=빈값 | `recipient`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TaxInvoiceListPage.tsx#L265) |
| 참조번호 | 입력·선택(조건부 검증 별도) | 화면 타입 selectWithInput; API 타입 String?; 선택: 전체=ALL, 참조번호=reference; 초기값 selectValue=reference; inputValue=빈값 | `referenceNumber`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TaxInvoiceListPage.tsx#L283) |
| 승인번호 | 입력·선택(조건부 검증 별도) | 화면 타입 selectWithInput; API 타입 String?; 선택: 전체=ALL, 승인번호=approval; 초기값 selectValue=approval; inputValue=빈값 | `approvalNumber`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TaxInvoiceListPage.tsx#L297) |
| 문서 상태 | 입력·선택(조건부 검증 별도) | 화면 타입 radio; API 타입 String?; 선택: 전체=ALL, 역발행 요청=V, 역발행 거부=T, 관리자 발행 요청=E, 관리자 발행 거부=U, 수신미승인=I, 수신승인=C, 수신거부=R, 발행취소 요청=N, 취소 완료=O, 발행예정=B, 발행예정 취소=H, 발행예정 승인=K, 발행예정 거부=L, 저장=S; 초기값 ALL | `documentStatus`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TaxInvoiceListPage.tsx#L311) |
| 세액 종류 | 입력·선택(조건부 검증 별도) | 화면 타입 checkbox; API 타입 List<String>?; 기본 null; 선택: 과세=T, 영세=P, 면세=F; 초기값 T, P, F | `taxTypes`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TaxInvoiceListPage.tsx#L327) |
| 문서 형태 | 입력·선택(조건부 검증 별도) | 화면 타입 checkbox; API 타입 List<String?>?; 기본 null; 선택: (세금)계산서=tax-invoice, (세금)계산서 + 거래명세서=tax-invoice-with-statement, 수정 세금계산서=amended-tax-invoice; 초기값 tax-invoice, tax-invoice-with-statement, amended-tax-invoice | `documentForms`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TaxInvoiceListPage.tsx#L337) |
| 발행 방향 | 입력·선택(조건부 검증 별도) | 화면 타입 checkbox; API 타입 List<String?>?; 기본 null; 선택: 정발행=F, 역발행=R; 초기값 F, R | `issuanceDirections`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TaxInvoiceListPage.tsx#L347) |
| 발행경로 | 입력·선택(조건부 검증 별도) | 화면 타입 selectWithSingleDate; API 타입 String?; 선택: 전체=ALL, 오픈API=OAPI, NxAPI=NxAPI, 신중계=NEOBILL, 보나뱅크=BONABANK, 모바일=MOBILE, EXCEL=EXCEL, CSV=CSV, NSAP=NSAP, SAP=SAP, SmartOnAI=SMARTONAI; 초기값 selectValue=ALL; date={defaultDateRange.startDate} | `issuancePath`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TaxInvoiceListPage.tsx#L357) |
| 이벤트 | 입력·선택(조건부 검증 별도) | 화면 타입 radio; API 타입 String?; 선택: 전체=ALL, 이벤트=event, 클로버=clover, 쿠폰=coupon; 초기값 ALL | `eventType`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TaxInvoiceListPage.tsx#L369) |
| 거래명세서 단독발행 | 입력·선택(조건부 검증 별도) | 화면 타입 radio; API 타입 String?; 선택: N (일반)=N, Y (단독발행)=Y; 초기값 N | `statementDownload`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TaxInvoiceListPage.tsx#L379) |
| 작성일자 | 출력 | API 타입 String | `createdAt`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TaxInvoiceListPage.tsx#L849) |
| 발행일자 | 출력 | API 타입 String | `issuanceDate`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TaxInvoiceListPage.tsx#L850) |
| 공급자 | 출력 | 초기값 selectValue=business-number; inputValue=빈값 | `supplier`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TaxInvoiceListPage.tsx#L851) |
| 공급받는자 | 출력 | 초기값 selectValue=business-number; inputValue=빈값 | `buyer`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TaxInvoiceListPage.tsx#L852) |
| 공급가액 | 출력 | API 타입 Long | `supplyAmount`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TaxInvoiceListPage.tsx#L853) |
| 세액종류 | 출력 | API 타입 String? | `taxType`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TaxInvoiceListPage.tsx#L854) |
| 상태 | 출력 | API 타입 String | `status`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TaxInvoiceListPage.tsx#L855) |
| 요금제 | 출력 | API 타입 String | `pricePlan`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TaxInvoiceListPage.tsx#L856) |
| 이벤트 | 출력 | API 타입 String | `event`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TaxInvoiceListPage.tsx#L857) |
| 위수탁 | 출력 | API 타입 String? | `trusteeType`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TaxInvoiceListPage.tsx#L859) |
| 사업자번호 | 출력 | API 타입 String | `supplierBusinessNumber`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TaxInvoiceListPage.tsx#L863) |
| 회사명 | 출력 | API 타입 String | `supplierCompanyName`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TaxInvoiceListPage.tsx#L864) |
| 사업자번호 | 출력 | API 타입 String | `buyerBusinessNumber`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TaxInvoiceListPage.tsx#L865) |
| 회사명 | 출력 | API 타입 String | `buyerCompanyName`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TaxInvoiceListPage.tsx#L866) |
| 공급받는자 이메일 | 입력·선택(조건부 검증 별도) | 길이·형식·조건부 필수는 검증 코드와 API DTO 참조 | `email`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TaxInvoiceListPage.tsx#L1007) |

입력 검증 근거: [TaxInvoiceListPage.rules.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/service/taxinvoice/TaxInvoiceListPage.rules.ts), [bulkEmailSchema.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/service/taxinvoice/bulkEmailSchema.ts). 프런트 검증과 서버 DTO 제약이 다르면 서버 검증이 최종 기준이다.

**복합 검색·폼의 초기 상태**

| 초기값 근거 | 기본 상태 |
|---|---|
| [defaultFilterValues](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TaxInvoiceListPage.tsx#L502) | issuanceCondition=selectValue=created-date; dateRange={useMemo(() => getTaxInvoiceDefaultDateRange('current'), [])}; supplier=selectValue=business-number; inputValue=빈값; buyer=selectValue=business-number; inputValue=빈값; buyerName=selectValue=nickname; inputValue=빈값; recipient=selectValue=business-number; inputValue=빈값; referenceNumber=selectValue=reference; inputValue=빈값; approvalNumber=selectValue=approval; inputValue=빈값; documentStatus=ALL; taxTypes=T, P, F; documentForms=tax-invoice, tax-invoice-with-statement, amended-tax-invoice; issuanceDirections=F, R; issuancePath=selectValue=ALL; date={defaultDateRange.startDate}; eventType=ALL; statementDownload=N |
| [defaultInitialParams](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TaxInvoiceListPage.tsx#L568) | issuanceCondition=created-date; startDate={defaultRange.startDate}; endDate={defaultRange.endDate}; documentStatus=ALL; includeAllReferenceNumbers=켜짐; includeAllApprovalNumbers=켜짐; eventType=ALL; statementDownload=N |

화면 필드 키와 API 필드명이 다른 경우 변환은 Hook/API의 검색·저장 매핑에서 수행된다. 요청·응답 필드와 DB 컬럼 매핑은 아래 API 계약 및 DB 객체 계약에 연결했다.

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
|---|---|---|---|
| 세금계산서 목록 조회 | [GET /api/v1/tax-invoices/search](../../references/api-contracts.md#api158); `/tax-invoice/tax-invoice` / `VIEW` | `issuanceCondition, startDate, endDate, supplierSearchType, supplierValue, buyerSearchType, buyerValue, buyerNameSearchType, buyerNameValue, verifiedOnly, recipientSearchType, recip` → `content, totalElements` | Mapper 프로시저의 정적 테이블 쓰기 미검출; 동적 SQL의 런타임 대상은 미확정 |
| downloadList | [GET /api/v1/tax-invoices/download](../../references/api-contracts.md#api155); `/tax-invoice/tax-invoice` / `EXCEL_DOWNLOAD` | `issuanceCondition, startDate, endDate, supplierSearchType, supplierValue, buyerSearchType, buyerValue, buyerNameSearchType, buyerNameValue, verifiedOnly, recipientSearchType, recip` → `응답 DTO·파일/처리 결과 계약 참조` | Mapper 프로시저의 정적 테이블 쓰기 미검출; 동적 SQL의 런타임 대상은 미확정 |
| 메일 발송 (통합) | [POST /api/v1/mail/send](../../references/api-contracts.md#api220); `/tax-invoice/tax-invoice` / `PROCESS` | `mailType, ids, items, emailAddress, title, emailContent, targetId` → `isAllSuccess, successCount, failedCount, message` | 쓰기 대상 office.dbo.servicemail_send, sb_dti_log.dbo.dti_customer_pwd |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
|---|---|---|---|
| [SB_DTI.dbo.DTT_HEADER_DETAIL](../../references/database-contracts.md#db142) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: sb_dti.dbo.dtt_header_detail, sb_dti.dbo.dtt_header_detail_2020_01, sb_dti.dbo.dtt_header_detail_2021_01, sb_dti.dbo.dtt_header_detail_2022_01, sb_dti.dbo.dtt_header_detail_2023_01, sb_dti.dbo.dtt_header_detail_bf, sb_dti.dbo.dtt_header_detail_part | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.UspSelectDttSingleList](../../references/database-contracts.md#db340) | `@PAGE int IN, @TOP int IN, @DATE_TYPE char(1) IN, @FMDATE varchar(10) IN, @TODATE varchar(10) IN, @SUP_INDEX varchar(20) IN, @SUP_TEXT varchar(70) IN, @BYR_INDEX varchar(20) IN, @BYR_TEXT varchar(70) IN, @BRK_INDEX varchar(20) IN, @BRK_TEXT varchar(70) IN, @REF_ID varchar(35) IN, @STATUS char(1) IN, @BYR_NAME varchar(20) IN, @EVENT_RESULT varchar(3) IN, @TAX_TYPES varchar(10) IN, @ISSUANCE_DIRECTIONS varchar(5) IN, @ISSUE_PATH varchar(10) IN, @CREATED_DATE varchar(10) IN, @ISSUE_ID varchar(24) IN, @ARCHIVE_SOURCE bit IN, @TOTAL_COUNT int OUT` | 확정한 테이블 쓰기 없음. 참조: sb_dti_dw.sys.objects, sb_dti_dw.sys.schemas, sb_dti_dw.sys.tables, smartbill3.dbo.member 동적 SQL 포함, 런타임 조합 대상 미확정. | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
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
| 다운로드할 데이터가 없습니다. | [문구·처리 코드](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TaxInvoiceListPage.tsx#L652); 현재 조건·대상·권한 확인 | 검색·조회 오류면 조건을 확인 후 재조회. 변경·발송 결과가 불명확하면 처리 여부와 이력을 확인한 뒤 재시도 여부를 판단한다. |
| 다운로드 중 오류가 발생했습니다. | [문구·처리 코드](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TaxInvoiceListPage.tsx#L691); 현재 조건·대상·권한 확인 | 검색·조회 오류면 조건을 확인 후 재조회. 변경·발송 결과가 불명확하면 처리 여부와 이력을 확인한 뒤 재시도 여부를 판단한다. |
| 일괄 메일 발송이 완료되었습니다. ({result.successCount}건) | [문구·처리 코드](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TaxInvoiceListPage.tsx#L776); 현재 조건·대상·권한 확인 | 검색·조회 오류면 조건을 확인 후 재조회. 변경·발송 결과가 불명확하면 처리 여부와 이력을 확인한 뒤 재시도 여부를 판단한다. |
| 일괄 메일 발송 완료: 성공 {result.successCount}건, 실패 {result.failedCount}건 | [문구·처리 코드](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TaxInvoiceListPage.tsx#L778); 현재 조건·대상·권한 확인 | 검색·조회 오류면 조건을 확인 후 재조회. 변경·발송 결과가 불명확하면 처리 여부와 이력을 확인한 뒤 재시도 여부를 판단한다. |
| 메일 발송 중 오류가 발생했습니다. | [문구·처리 코드](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TaxInvoiceListPage.tsx#L787); 현재 조건·대상·권한 확인 | 검색·조회 오류면 조건을 확인 후 재조회. 변경·발송 결과가 불명확하면 처리 여부와 이력을 확인한 뒤 재시도 여부를 판단한다. |
| 결과가 없거나 기대 건수와 다름 | 적용된 검색 기준·기간·탭·대상 상태·서버 필터·페이징·목록/다운로드 조건 | 조건을 다시 확인하고 조회한다. 지속되면 경로·작업 시각·마스킹한 식별자·필터를 업무/기술 담당에게 전달한다. |
| 메뉴·버튼 미표시 또는 접근 거부 | 사용자 그룹의 메뉴 접근·VIEW 및 API별 PROCESS/EXECUTE/DELETE/EXCEL_DOWNLOAD/UNMASK 등 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. 프런트 버튼 표시만으로 서버 권한을 판단하지 않는다. |
| 저장·삭제·외부 실행의 결과가 불명확 | 대상 현재 상태·중복 요청·감사 이력·API 오류·파일/외부 소비 로그 | 기존 반영 여부를 먼저 조회한다. 중복 발송·초기화·금액 처리를 피하기 위해 기술 담당 확인 후 재시도한다. |

## 7) 검증·출처

**브라우저 검증(2026-11-09)**: 화면 대조. [경로별 결과와 제한](../../references/browser-verification.md#page015). 역할별 권한 거부·저장 성공·파일 반출·외부 연계 완료는 이 결과로 보장하지 않는다.

| 검증 항목 | 근거·환경 | 상태·확인일 |
|---|---|---|
| 대상 선정 | 사용자가 WBS 탭 내용으로 제공한 텍스트의 No. 43, 44, 45, 46, 47; [선정 태스크](../../inventory/wbs-tasks.csv) | 제공 텍스트 확인 2026-11-09. 원본 Excel의 탭/병합 셀을 독립 재열람한 것은 아님. |
| 메뉴·라우트·화면 | [menuConfig.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts); [TaxInvoiceRoutes.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/TaxInvoiceRoutes.tsx); [TaxInvoiceListPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/TaxInvoiceListPage.tsx) | 코드 확인 2026-11-09, 기준 dc216b313 |
| 기능·권한·API | 이 문서의 API 계약 링크 및 연결 Hook/API·Controller·DTO·Service·Repository·Mapper | 코드 확인 2026-11-09. 조회 요청·화면 대조 범위는 아래 브라우저 근거 참조. 권한 계정별 허용·거부 및 변경 요청 실행은 미확인. |
| DB 정의 | [개발 DB 계약](../../references/database-contracts.md), 이 문서의 연결 객체 | 개발 DB 정의 확인 2026-11-09. 동적 SQL·CLR 내부·정의 미공개 참조의 미확정 범위는 객체별 기록; 후속 확인 DB 담당. |
| 브라우저 화면·배포 환경 | 로컬 인증 계정·Playwright CLI; [화면별 검증표](../../references/browser-verification.md#page015) | 화면 대조, 2026-11-09. 배포본·타 역할·업무 변경 결과는 미확인. |
| 업무 프로시저·쓰기·외부 결과 | 격리된 검증 환경·테스트 데이터의 실행 결과 | 미확인: 명시적인 저장·삭제·발송·초기화 요청은 실행하지 않음. 브라우저 GET의 업무 조회 프로시저·조회수·감사 기록은 별도 영향으로 구분. 격리 환경에서 기술 담당 확인. |

코드 확인과 DB 정의 확인은 실행 성공·업무 승인·다른 환경 적용을 보장하지 않는다. 업무·기술 담당 검토 후 조사 목록의 상태를 완료로 변경한다.

브라우저 직접 근거: [settled-static-recheck](../../evidence/browser/static-stable.json). 경로·고정 버튼명·입력 속성·표 머리글·API 상태를 보관했고 실제 데이터 값·식별자·인증정보는 제외했다.

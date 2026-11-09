# [SB 서비스관리] 세금계산서 통계 (조회·관리) 관리자 매뉴얼

작성 기준: `dc216b313` · 확인일 2026-11-09 · 조사 상태 **검토 대기**. 코드와 개발 DB 정의를 확인했으며 실제 화면·업무 실행은 미재현이다.

## 1) 화면 기본 정보

| 항목 | 작성 내용 |
|---|---|
| 업무 도메인·목적 | 보나뱅크 세금계산서의 월별 국세청 신고 통계와 업체별 증감을 비교한다. |
| 메뉴·화면 경로 | SB 서비스관리 > 보나뱅크 > 세금계산서 통계; `/bonabank/tax-invoice-statistics`; 메뉴 또는 관련 화면에서 진입한다. |
| 화면 유형·담당 | 조회·관리; WBS 작업자 유지윤. 업무·기술 담당 팀명은 원문에 없어 배포 전 해당 도메인 담당자가 확정한다. |
| 관련 화면 | 같은 메뉴에 별도 독립 경로 없음. 팝업·탭은 이 문서 참조. |

WBS 근거: No. 144, 145 (사용자가 제공한 텍스트 행 180, 181). API 개발/화면 개발의 중복 행은 같은 화면으로 통합했다.

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
|---|---|---|
| 화면 진입·조회 | `/bonabank/tax-invoice-statistics` 메뉴 접근·하위 경로 작업 권한. 조회 API는 VIEW, 등록/수정 경로는 PROCESS 등 아래 서버 액션과 라우트 가드를 함께 적용한다. | 로그인된 관리자 계정; 아래 검색·입력 항목을 준비한다. |
| 다운로드 | `/bonabank/tax-invoice-statistics`; 엑셀 download 화면 게이트. 다운로드/업로드 API의 서버 권한과 사유 입력을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |

서버가 최종 권한을 검사한다. 버튼 모양(kind)으로 권한을 추정하지 않는다. 특히 등록·수정이 PROCESS를 사용하는 API와 EXECUTE·UNMASK·EXCEL_DOWNLOAD는 서로 구분한다.

## 3) 화면 사용 절차

1. `SB 서비스관리 > 보나뱅크 > 세금계산서 통계` 메뉴를 연다. 경로 변수는 주소에서 임의로 바꾸지 않고 이전 화면이 전달한 식별자를 사용한다.
2. 현재 검색 조건과 아래 기본값을 확인한다. **대상 년월, 문서 구분, 사업자번호** 항목에 필요한 값을 입력하고 **검색**을 누른다.
3. 결과 표·탭·팝업에서 대상의 상태와 합계·이력을 확인한다. 다른 조회 조건으로 바꾼 경우 다시 검색하여 결과를 갱신한다.

**이 화면에서 유의할 업무 규칙**: 월별 국세청 신고 통계와 업체별 증감 현황 탭을 구분한다. 대상 년월·문서 구분·사업자번호 조건을 확인한다. 전체 구분이 아닌 통계 검색에는 사업자번호 필수 조건을 확인한다.

**반출**: 적용된 검색 조건과 반출 범위를 확인한 후 다운로드한다. 사유 입력창이 표시되면 업무 사유를 입력한다. 사유 등록 실패·파일 오류는 성공으로 간주하지 않고 다운로드 결과를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
|---|---|---|---|
| 대상 년월 | 입력·필수 | 화면 타입 month; API 타입 String; 서버 검증 @field:Pattern(regexp = YEAR_MONTH_REGEX, message = "yearMonth 는 yyyy-MM 형식이어야 합니다."); 초기값 {getCurrentYearMonth()} | `yearMonth`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/statistics/MonthlyNtsStatisticsTab.tsx#L84) |
| 문서 구분 | 입력·선택(조건부 검증 별도) | 화면 타입 select; API 타입 String?; 기본 null; 서버 검증 @field:Pattern; 선택: 전체=ALL, 세금계산서=TAX_INVOICE, 계산서=INVOICE; 초기값 ALL | `documentType`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/statistics/MonthlyNtsStatisticsTab.tsx#L88) |
| 사업자번호 | 입력·선택(조건부 검증 별도) | 화면 타입 toggleableText; 최대 10자; API 타입 String?; 기본 null; 서버 검증 @field:Size(max = 13, message = "businessNumber 는 13자 이하여야 합니다."); 초기값 isAll=꺼짐; inputValue=빈값; 입력 안내 사업자번호를 입력하세요. | `businessNumber`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/statistics/MonthlyNtsStatisticsTab.tsx#L102) |
| 문서구분 | 출력 | API 타입 String?; 기본 null; 서버 검증 @field:Pattern; 초기값 ALL | `documentType`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/statistics/NtsStatisticsSummaryTable.tsx#L34) |
| 접수 대기 | 출력 | API 타입 Long | `pendingReceipt`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/statistics/NtsStatisticsSummaryTable.tsx#L41) |
| 접수 완료 | 출력 | API 타입 Long | `completedReceipt`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/statistics/NtsStatisticsSummaryTable.tsx#L48) |
| 신고실패 | 출력 | API 타입 Long | `reportFailed`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/statistics/NtsStatisticsSummaryTable.tsx#L55) |
| 신고완료 | 출력 | API 타입 Long | `reportCompleted`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/statistics/NtsStatisticsSummaryTable.tsx#L62) |
| 총계 | 출력 | API 타입 Long | `total`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/statistics/NtsStatisticsSummaryTable.tsx#L69) |
| 공급가액 총계 | 출력 | API 타입 Long | `supplyAmountTotal`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/statistics/NtsStatisticsSummaryTable.tsx#L76) |
| 회사명 | 출력 | API 타입 String? | `companyName`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/statistics/CompanyStatusTable.tsx#L29) |
| 사업자 번호 | 출력 | API 타입 String?; 기본 null; 서버 검증 @field:Size(max = 13, message = "businessNumber 는 13자 이하여야 합니다."); 초기값 isAll=꺼짐; inputValue=빈값 | `businessNumber`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/statistics/CompanyStatusTable.tsx#L40) |
| 접수대기 | 출력 | API 타입 Long | `pendingReceipt`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/statistics/CompanyStatusTable.tsx#L47) |
| 회사명 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `companyName-header`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/statistics/CompanyChangeTable.tsx#L61) |
| 사업자 번호 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `businessNumber-header`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/statistics/CompanyChangeTable.tsx#L68) |
| 전월 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `prevMonth-group`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/statistics/CompanyChangeTable.tsx#L75) |
| 당월 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `currMonth-group`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/statistics/CompanyChangeTable.tsx#L81) |
| 증감현황 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `change-group`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/statistics/CompanyChangeTable.tsx#L87) |
| 비고 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `note-group`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/statistics/CompanyChangeTable.tsx#L93) |
| 신고완료 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `prevMonth.reportCompleted-header`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/statistics/CompanyChangeTable.tsx#L101) |
| 공급가액 총계 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `prevMonth.supplyAmountTotal-header`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/statistics/CompanyChangeTable.tsx#L107) |
| 신고완료 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `currMonth.reportCompleted-header`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/statistics/CompanyChangeTable.tsx#L113) |
| 공급가액 총계 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `currMonth.supplyAmountTotal-header`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/statistics/CompanyChangeTable.tsx#L119) |
| 신고완료 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `change.reportCompleted-header`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/statistics/CompanyChangeTable.tsx#L125) |
| 공급가액 총계 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `change.supplyAmountTotal-header`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/statistics/CompanyChangeTable.tsx#L131) |
| 담당자 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `manager-header`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/statistics/CompanyChangeTable.tsx#L137) |
| 연락처 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `phone-header`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/statistics/CompanyChangeTable.tsx#L143) |
| 전월 신고완료 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `prevMonth.reportCompleted`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/statistics/CompanyChangeTable.tsx#L174) |
| 전월 공급가액 총계 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `prevMonth.supplyAmountTotal`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/statistics/CompanyChangeTable.tsx#L181) |
| 당월 신고완료 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `currMonth.reportCompleted`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/statistics/CompanyChangeTable.tsx#L188) |
| 당월 공급가액 총계 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `currMonth.supplyAmountTotal`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/statistics/CompanyChangeTable.tsx#L195) |
| 증감 신고완료 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `change.reportCompleted`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/statistics/CompanyChangeTable.tsx#L202) |
| 증감 공급가액 총계 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `change.supplyAmountTotal`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/statistics/CompanyChangeTable.tsx#L209) |
| 담당자 | 출력 | API 타입 String? | `manager`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/statistics/CompanyChangeTable.tsx#L216) |
| 연락처 | 출력 | API 타입 String? | `phone`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/statistics/CompanyChangeTable.tsx#L231) |

**복합 검색·폼의 초기 상태**

| 초기값 근거 | 기본 상태 |
|---|---|
| [buildDefaultFilters](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/statistics/MonthlyNtsStatisticsTab.tsx#L38) | yearMonth={getCurrentYearMonth()}; documentType=ALL; businessNumber=isAll=꺼짐; inputValue=빈값 |
| [buildDefaultFilters](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/statistics/CompanyChangeTab.tsx#L39) | yearMonth={getCurrentYearMonth()}; documentType=ALL; businessNumber=isAll=꺼짐; inputValue=빈값 |

화면 필드 키와 API 필드명이 다른 경우 변환은 Hook/API의 검색·저장 매핑에서 수행된다. 요청·응답 필드와 DB 컬럼 매핑은 아래 API 계약 및 DB 객체 계약에 연결했다.

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
|---|---|---|---|
| 월별 국세청 신고 통계 (요약 + 회사별) | [GET /api/v1/bonabank/tax-invoice-statistics/monthly](../../references/api-contracts.md#api023); `/bonabank/tax-invoice-statistics` / `VIEW` | `yearMonth, documentType, businessNumber, page, size` → `summary, companies, documentType, pendingReceipt, completedReceipt, reportFailed, reportCompleted, total, supplyAmountTotal, content, totalElements, page, rowNumber, companyName, b` | Mapper 프로시저의 정적 테이블 쓰기 미검출; 동적 SQL의 런타임 대상은 미확정 |
| 월별 통계 엑셀 다운로드 (회사별) | [GET /api/v1/bonabank/tax-invoice-statistics/monthly/download](../../references/api-contracts.md#api024); `/bonabank/tax-invoice-statistics` / `EXCEL_DOWNLOAD` | `yearMonth, documentType, businessNumber` → `응답 DTO·파일/처리 결과 계약 참조` | Mapper 프로시저의 정적 테이블 쓰기 미검출; 동적 SQL의 런타임 대상은 미확정 |
| 업체별 증감 현황 (전월/당월/증감) | [GET /api/v1/bonabank/tax-invoice-statistics/company-change](../../references/api-contracts.md#api021); `/bonabank/tax-invoice-statistics` / `VIEW` | `yearMonth, documentType, businessNumber, page, size` → `content, totalElements, page, rowNumber, companyName, businessNumber, prevMonth, currMonth, change, manager, phone, reportCompleted, supplyAmountTotal` | Mapper 프로시저의 정적 테이블 쓰기 미검출; 동적 SQL의 런타임 대상은 미확정 |
| 업체별 증감 현황 엑셀 다운로드 | [GET /api/v1/bonabank/tax-invoice-statistics/company-change/download](../../references/api-contracts.md#api022); `/bonabank/tax-invoice-statistics` / `EXCEL_DOWNLOAD` | `yearMonth, documentType, businessNumber` → `응답 DTO·파일/처리 결과 계약 참조` | Mapper 프로시저의 정적 테이블 쓰기 미검출; 동적 SQL의 런타임 대상은 미확정 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
|---|---|---|---|
| [SB_COMMON.dbo.upSBAdm_StatsDTICompany_Bona](../../references/database-contracts.md#db116) | `@PAGE int IN, @TOP int IN, @FROMDATE varchar(10) IN, @TODATE varchar(10) IN, @DTI_TYPE varchar(1) IN, @COM_REGNO varchar(70) IN, @DATE_TYPE char(1) IN` | 확정한 테이블 쓰기 없음. 참조: migration_etcasp.dbo.migration_mapping_company, sb_dti.dbo.dti_header_cub, sb_dti.dbo.dti_header_cub_2023_07, sb_dti.dbo.dti_header_cub_part, sb_dti.dbo.dti_header_cub_prev_buffer, sb_dti.dbo.dti_sign_cub, sb_dti.dbo.dti_sign_cub_2023_07, sb_dti.dbo.dti_sign_cub_part 외 3개 동적 SQL 포함, 런타임 조합 대상 미확정. | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_COMMON.dbo.upSBAdm_StatsDTI_Bona](../../references/database-contracts.md#db115) | `@FROMDATE varchar(10) IN, @TODATE varchar(10) IN, @DTI_TYPE varchar(1) IN, @COM_REGNO varchar(70) IN, @DATE_TYPE char(1) IN` | 확정한 테이블 쓰기 없음. 참조: migration_etcasp.dbo.migration_mapping_company, sb_dti.dbo.dti_header_cub, sb_dti.dbo.dti_header_cub_2023_07, sb_dti.dbo.dti_header_cub_part, sb_dti.dbo.dti_header_cub_prev_buffer, sb_dti.dbo.dti_sign_cub, sb_dti.dbo.dti_sign_cub_2023_07, sb_dti.dbo.dti_sign_cub_part 외 3개 동적 SQL 포함, 런타임 조합 대상 미확정. | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_COMMON.dbo.upSBAdm_StatsDTICompany_Bona_excel](../../references/database-contracts.md#db117) | `@FROMDATE varchar(10) IN, @TODATE varchar(10) IN, @DTI_TYPE varchar(1) IN, @COM_REGNO varchar(70) IN, @DATE_TYPE char(1) IN` | 확정한 테이블 쓰기 없음. 참조: migration_etcasp.dbo.migration_mapping_company, sb_dti.dbo.dti_header_cub, sb_dti.dbo.dti_header_cub_2023_07, sb_dti.dbo.dti_header_cub_part, sb_dti.dbo.dti_header_cub_prev_buffer, sb_dti.dbo.dti_sign_cub, sb_dti.dbo.dti_sign_cub_2023_07, sb_dti.dbo.dti_sign_cub_part 외 3개 동적 SQL 포함, 런타임 조합 대상 미확정. | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_COMMON.dbo.upSBAdm_NtsSendCompany_Bona](../../references/database-contracts.md#db106) | `@PAGE_NO int IN, @ROWS int IN, @STAT_MONTH varchar(10) IN, @DTI_TYPE varchar(1) IN, @COM_REGNO varchar(10) IN, @DATE_TYPE char(1) IN` | 확정한 테이블 쓰기 없음. 참조: migration_etcasp.dbo.migration_mapping_company, sb_dti.dbo.dti_header_cub, sb_dti.dbo.dti_header_cub_2023_07, sb_dti.dbo.dti_header_cub_part, sb_dti.dbo.dti_header_cub_prev_buffer, sb_dti.dbo.dti_sign_cub, sb_dti.dbo.dti_sign_cub_2023_07, sb_dti.dbo.dti_sign_cub_part 외 4개 동적 SQL 포함, 런타임 조합 대상 미확정. | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_COMMON.dbo.upSBAdm_NtsSendCompany_Bona_excel](../../references/database-contracts.md#db107) | `@STAT_MONTH varchar(10) IN, @DTI_TYPE varchar(1) IN, @COM_REGNO varchar(10) IN, @DATE_TYPE char(1) IN` | 확정한 테이블 쓰기 없음. 참조: migration_etcasp.dbo.migration_mapping_company, sb_dti.dbo.dti_header_cub, sb_dti.dbo.dti_header_cub_2023_07, sb_dti.dbo.dti_header_cub_part, sb_dti.dbo.dti_header_cub_prev_buffer, sb_dti.dbo.dti_sign_cub, sb_dti.dbo.dti_sign_cub_2023_07, sb_dti.dbo.dti_sign_cub_part 외 4개 동적 SQL 포함, 런타임 조합 대상 미확정. | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |

위 DB 계약 링크에는 실제 파라미터 타입·기본값·IN/OUT, Mapper 결과 컬럼, RETURN 바인딩, 참조 테이블·하위 프로시저·정의 필터/정렬을 기록했다. DTO·Service·Repository·Mapper의 상세 호출 경로는 각 API 계약에서 확인한다.

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
|---|---|---|
| 검색 결과가 존재하지 않습니다. | [문구·처리 코드](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/components/statistics/CompanyStatusTable.tsx#L94); 현재 조건·대상·권한 확인 | 검색·조회 오류면 조건을 확인 후 재조회. 변경·발송 결과가 불명확하면 처리 여부와 이력을 확인한 뒤 재시도 여부를 판단한다. |
| 결과가 없거나 기대 건수와 다름 | 적용된 검색 기준·기간·탭·대상 상태·서버 필터·페이징·목록/다운로드 조건 | 조건을 다시 확인하고 조회한다. 지속되면 경로·작업 시각·마스킹한 식별자·필터를 업무/기술 담당에게 전달한다. |
| 메뉴·버튼 미표시 또는 접근 거부 | 사용자 그룹의 메뉴 접근·VIEW 및 API별 PROCESS/EXECUTE/DELETE/EXCEL_DOWNLOAD/UNMASK 등 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. 프런트 버튼 표시만으로 서버 권한을 판단하지 않는다. |
| 저장·삭제·외부 실행의 결과가 불명확 | 대상 현재 상태·중복 요청·감사 이력·API 오류·파일/외부 소비 로그 | 기존 반영 여부를 먼저 조회한다. 중복 발송·초기화·금액 처리를 피하기 위해 기술 담당 확인 후 재시도한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
|---|---|---|
| 대상 선정 | 사용자가 WBS 탭 내용으로 제공한 텍스트의 No. 144, 145; [선정 태스크](../../inventory/wbs-tasks.csv) | 제공 텍스트 확인 2026-11-09. 원본 Excel의 탭/병합 셀을 독립 재열람한 것은 아님. |
| 메뉴·라우트·화면 | [menuConfig.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts); [BonabankRoutes.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/BonabankRoutes.tsx); [BonabankTaxInvoiceStatisticsPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/BonabankTaxInvoiceStatisticsPage.tsx) | 코드 확인 2026-11-09, 기준 dc216b313 |
| 기능·권한·API | 이 문서의 API 계약 링크 및 연결 Hook/API·Controller·DTO·Service·Repository·Mapper | 코드 확인 2026-11-09. 요청 실행·권한 계정별 재현은 미확인. |
| DB 정의 | [개발 DB 계약](../../references/database-contracts.md), 이 문서의 연결 객체 | 개발 DB 정의 확인 2026-11-09. 동적 SQL·CLR 내부·정의 미공개 참조의 미확정 범위는 객체별 기록; 후속 확인 DB 담당. |
| 브라우저 화면·배포 환경 | 실제 검증 계정의 정상·빈 결과·권한 부족·입력 오류 및 현재 배포본 | 미확인: 브라우저 실행 검증을 수행하지 않음. 배포 전 업무 담당·QA·기술 담당 확인. |
| 업무 프로시저·쓰기·외부 결과 | 격리된 검증 환경·테스트 데이터의 실행 결과 | 미확인: 공유 개발 DB의 업무 프로시저·쓰기·발송을 실행하지 않음. 격리 환경에서 기술 담당 확인. |

코드 확인과 DB 정의 확인은 실행 성공·업무 승인·다른 환경 적용을 보장하지 않는다. 업무·기술 담당 검토 후 조사 목록의 상태를 완료로 변경한다.

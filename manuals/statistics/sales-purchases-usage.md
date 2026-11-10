# [서비스 현황] 매출/매입 이용 현황 (조회·관리) 관리자 매뉴얼

작성 기준: `dc216b313` · 확인일 2026-11-09 · 조사 상태 **검토 대기**. 코드·개발 DB 정의 확인. 브라우저: **화면 대조**; 저장·발송 등 업무 실행 결과는 미검증이다.

## 1) 화면 기본 정보

### 도메인 이해

업체의 매출 관점 발행 실적과 거래 상대인 매입 업체·문서 규모를 조사한다.

| 구분 | 설명 |
|---|---|
| 업무 영역 | 서비스 이용 통계 > 매출/매입 이용 현황 조회·관리 |
| 언제 사용하는가 | 특정 매출업체나 발행건수 조건으로 거래 이용 실적을 확인할 때 |
| 주요 대상·데이터 | 매출업체·사업자번호·월·매입업체수·세금계산서수는 업체·월별 거래 이용 지표다. |
| 업무 흐름 | 구분·기간·매출업체·건수 조건 선택 → 업체별 실적 확인 → 비교 대상 조건 일치 확인 |
| 이 페이지의 역할 | 업체별 매출·매입 이용량 중 **매출/매입 이용 현황 조회·관리** 단계. 업체의 매출 관점 발행 실적과 거래 상대인 매입 업체·문서 규모를 조사한다. |
| 판단 결과·다음 업무 | 거래 이용 규모를 파악하며 다른 집계와 비교할 때 업체·월·매출/매입 관점을 맞춘다. |
| 다른 화면과의 구분 | 회계 장부의 실제 매출액·미수금이나 개별 입금 금액을 조회하는 화면으로 해석하지 않는다. |

설명 근거: [SalesPurchasesUsagePage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/SalesPurchasesUsagePage.tsx), 이 문서 4·5·7번의 항목·API·업무 규칙. [상위 업무 영역](../../references/domain-overview.md#statistics)은 공통 배경이며 현재 화면의 데이터·동작은 위 설명을 따른다. 설명 수정일 **2026-11-10**; 새 업무 실행 검증을 수행한 것은 아니다.

### 화면 정보

| 항목 | 작성 내용 |
|---|---|
| 업무 도메인·목적 | 업체의 매출 관점 발행 실적과 거래 상대인 매입 업체·문서 규모를 조사한다. |
| 메뉴·화면 경로 | 서비스 현황 > 통계 정보 > 매출/매입 이용 현황; `/statistics/sales-purchases-usage`; 메뉴 또는 관련 화면에서 진입한다. |
| 화면 유형·담당 | 조회·관리; WBS 작업자 유지윤. 업무·기술 담당 팀명은 원문에 없어 배포 전 해당 도메인 담당자가 확정한다. |
| 관련 화면 | 같은 메뉴에 별도 독립 경로 없음. 팝업·탭은 이 문서 참조. |

WBS 근거: No. 225 (사용자가 제공한 텍스트 행 286). API 개발/화면 개발의 중복 행은 같은 화면으로 통합했다.

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
|---|---|---|
| 화면 진입·조회 | `/statistics/sales-purchases-usage` 메뉴 접근·하위 경로 작업 권한. 조회 API는 VIEW, 등록/수정 경로는 PROCESS 등 아래 서버 액션과 라우트 가드를 함께 적용한다. | 로그인된 관리자 계정; 아래 검색·입력 항목을 준비한다. |
| 다운로드 | `/statistics/sales-purchases-usage`; 엑셀 download 화면 게이트. 다운로드/업로드 API의 서버 권한과 사유 입력을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |

서버가 최종 권한을 검사한다. 버튼 모양(kind)으로 권한을 추정하지 않는다. 특히 등록·수정이 PROCESS를 사용하는 API와 EXECUTE·UNMASK·EXCEL_DOWNLOAD는 서로 구분한다.

## 3) 화면 사용 절차

**검증 시 화면 버튼**: 검색, 다운로드. 화면 상태·대상에 따라 달라지며 아래 작업 절차와 권한 조건을 함께 확인한다.

1. `서비스 현황 > 통계 정보 > 매출/매입 이용 현황` 메뉴를 연다. 경로 변수는 주소에서 임의로 바꾸지 않고 이전 화면이 전달한 식별자를 사용한다.
2. 현재 검색 조건과 아래 기본값을 확인한다. **구분, 발행기간, 매출업체, 매출 발행 건수** 항목에 필요한 값을 입력하고 **검색**을 누른다.
3. 결과 표·탭·팝업에서 대상의 상태와 합계·이력을 확인한다. 다른 조회 조건으로 바꾼 경우 다시 검색하여 결과를 갱신한다.

**이 화면에서 유의할 업무 규칙**: 구분 기본은 매출이며 발행기간은 현재 월이다. 매출업체 기본 검색은 사업자번호다. 매입으로 전환할 때 표시 업체와 집계 기준이 바뀌는 점을 확인한다.

**반출**: 적용된 검색 조건과 반출 범위를 확인한 후 다운로드한다. 사유 입력창이 표시되면 업무 사유를 입력한다. 사유 등록 실패·파일 오류는 성공으로 간주하지 않고 다운로드 결과를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
|---|---|---|---|
| 구분 | 입력·선택(조건부 검증 별도) | 화면 타입 radio; API 타입 String?; 기본 null; 선택: 매출=매출, 매입=매입; 초기값 매출 | `category`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/SalesPurchasesUsagePage.tsx#L30) |
| 발행기간 | 입력·선택(조건부 검증 별도) | 화면 타입 monthRange; 초기값 startMonth={getCurrentMonth()}; endMonth={getCurrentMonth()} | `usagePeriod`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/SalesPurchasesUsagePage.tsx#L43) |
| 매출업체 | 입력·선택(조건부 검증 별도) | 화면 타입 selectWithInput; 선택: 전체=all, 사업자번호=사업자번호, 회사명=회사명; 초기값 selectValue=사업자번호; inputValue=빈값 | `vendor`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/SalesPurchasesUsagePage.tsx#L52) |
| 매출 발행 건수 | 입력·선택(조건부 검증 별도) | 화면 타입 text; API 타입 Long?; 기본 null; 초기값 빈값 | `minIssueCount`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/SalesPurchasesUsagePage.tsx#L73) |
| 번호 | 출력 | API 타입 Int | `no`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/SalesPurchasesUsageTable.tsx#L27) |
| 매출업체 | 출력 | API 타입 String | `vendorName`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/SalesPurchasesUsageTable.tsx#L28) |
| 사업자번호 | 출력 | API 타입 String | `businessNumber`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/SalesPurchasesUsageTable.tsx#L29) |
| 월 | 출력 | API 타입 String | `month`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/SalesPurchasesUsageTable.tsx#L39) |
| 매입 업체수 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `purchaseCompanyCountFormatted`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/SalesPurchasesUsageTable.tsx#L40) |
| 세금계산서 수 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `taxInvoiceCountFormatted`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/SalesPurchasesUsageTable.tsx#L46) |

입력 검증 근거: [schemaErrors.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/schemaErrors.ts), [salesPurchasesUsage.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/status/statistics/salesPurchasesUsage.ts). 프런트 검증과 서버 DTO 제약이 다르면 서버 검증이 최종 기준이다.

**복합 검색·폼의 초기 상태**

| 초기값 근거 | 기본 상태 |
|---|---|
| [initialFilterValues](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/SalesPurchasesUsagePage.tsx#L89) | category=매출; usagePeriod=startMonth={getCurrentMonth()}; endMonth={getCurrentMonth()}; vendor=selectValue=사업자번호; inputValue=빈값; minIssueCount=빈값 |

화면 필드 키와 API 필드명이 다른 경우 변환은 Hook/API의 검색·저장 매핑에서 수행된다. 요청·응답 필드와 DB 컬럼 매핑은 아래 API 계약 및 DB 객체 계약에 연결했다.

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
|---|---|---|---|
| 다운로드 사유 등록 | [POST /api/v1/download-reason](../../references/api-contracts.md#api210); `메뉴별 추가 검사 없음` / `인증 사용자` | `downloadReason, downloadType, fileName, metadata` → `응답 DTO·파일/처리 결과 계약 참조` | 쓰기 대상 smartwork.dbo.action_reason |
| 매출/매입 이용 현황 리스트 조회 | [GET /api/v1/service-status/sales-purchase/usage](../../references/api-contracts.md#api119); `/statistics/sales-purchases-usage` / `VIEW` | `category, usageMonthStart, usageMonthEnd, vendorCondition, vendorKeyword, minIssueCount, page, size` → `content, totalElements, totalPages, currentPage, size, no, vendorName, businessNumber, month, purchaseCompanyCount, taxInvoiceCount, category` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 매출/매입 이용 현황 CSV 다운로드 | [GET /api/v1/service-status/sales-purchase/usage/download](../../references/api-contracts.md#api120); `/statistics/sales-purchases-usage` / `EXCEL_DOWNLOAD` | `category, usageMonthStart, usageMonthEnd, vendorCondition, vendorKeyword, minIssueCount` → `응답 DTO·파일/처리 결과 계약 참조` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
|---|---|---|---|
| [smartwork.dbo.action_reason](../../references/database-contracts.md#db266) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 쓰기: smartwork.dbo.action_reason. 참조: smartwork.dbo.action_reason | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.usp_sales_purchases_usage_select](../../references/database-contracts.md#db293) | `@div varchar(3) IN, @fmdate varchar(8) IN, @todate varchar(10) IN, @schItem varchar(50) IN, @schText varchar(50) IN, @count int IN` | 확정한 테이블 쓰기 없음. 참조: sb_dti.dbo.dti_header_cub_2020_01, sb_dti.dbo.dti_header_cub_2020_02, sb_dti.dbo.dti_header_cub_2020_03, sb_dti.dbo.dti_header_cub_2020_04, sb_dti.dbo.dti_header_cub_2020_05, sb_dti.dbo.dti_header_cub_2020_06, sb_dti.dbo.dti_header_cub_2020_07, sb_dti.dbo.dti_header_cub_2020_08 외 35개 | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |

위 DB 계약 링크에는 실제 파라미터 타입·기본값·IN/OUT, Mapper 결과 컬럼, RETURN 바인딩, 참조 테이블·하위 프로시저·정의 필터/정렬을 기록했다. DTO·Service·Repository·Mapper의 상세 호출 경로는 각 API 계약에서 확인한다.

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
|---|---|---|
| 검색 결과가 없습니다. | [문구·처리 코드](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/SalesPurchasesUsageTable.tsx#L62); 현재 조건·대상·권한 확인 | 검색·조회 오류면 조건을 확인 후 재조회. 변경·발송 결과가 불명확하면 처리 여부와 이력을 확인한 뒤 재시도 여부를 판단한다. |
| 결과가 없거나 기대 건수와 다름 | 적용된 검색 기준·기간·탭·대상 상태·서버 필터·페이징·목록/다운로드 조건 | 조건을 다시 확인하고 조회한다. 지속되면 경로·작업 시각·마스킹한 식별자·필터를 업무/기술 담당에게 전달한다. |
| 메뉴·버튼 미표시 또는 접근 거부 | 사용자 그룹의 메뉴 접근·VIEW 및 API별 PROCESS/EXECUTE/DELETE/EXCEL_DOWNLOAD/UNMASK 등 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. 프런트 버튼 표시만으로 서버 권한을 판단하지 않는다. |
| 저장·삭제·외부 실행의 결과가 불명확 | 대상 현재 상태·중복 요청·감사 이력·API 오류·파일/외부 소비 로그 | 기존 반영 여부를 먼저 조회한다. 중복 발송·초기화·금액 처리를 피하기 위해 기술 담당 확인 후 재시도한다. |

## 7) 검증·출처

**브라우저 검증(2026-11-09)**: 화면 대조. [경로별 결과와 제한](../../references/browser-verification.md#page085). 역할별 권한 거부·저장 성공·파일 반출·외부 연계 완료는 이 결과로 보장하지 않는다.

| 검증 항목 | 근거·환경 | 상태·확인일 |
|---|---|---|
| 대상 선정 | 사용자가 WBS 탭 내용으로 제공한 텍스트의 No. 225; [선정 태스크](../../inventory/wbs-tasks.csv) | 제공 텍스트 확인 2026-11-09. 원본 Excel의 탭/병합 셀을 독립 재열람한 것은 아님. |
| 메뉴·라우트·화면 | [menuConfig.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts); [StatisticsRoutes.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/StatisticsRoutes.tsx); [SalesPurchasesUsagePage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/SalesPurchasesUsagePage.tsx) | 코드 확인 2026-11-09, 기준 dc216b313 |
| 기능·권한·API | 이 문서의 API 계약 링크 및 연결 Hook/API·Controller·DTO·Service·Repository·Mapper | 코드 확인 2026-11-09. 조회 요청·화면 대조 범위는 아래 브라우저 근거 참조. 권한 계정별 허용·거부 및 변경 요청 실행은 미확인. |
| DB 정의 | [개발 DB 계약](../../references/database-contracts.md), 이 문서의 연결 객체 | 개발 DB 정의 확인 2026-11-09. 동적 SQL·CLR 내부·정의 미공개 참조의 미확정 범위는 객체별 기록; 후속 확인 DB 담당. |
| 브라우저 화면·배포 환경 | 로컬 인증 계정·Playwright CLI; [화면별 검증표](../../references/browser-verification.md#page085) | 화면 대조, 2026-11-09. 배포본·타 역할·업무 변경 결과는 미확인. |
| 업무 프로시저·쓰기·외부 결과 | 격리된 검증 환경·테스트 데이터의 실행 결과 | 미확인: 명시적인 저장·삭제·발송·초기화 요청은 실행하지 않음. 브라우저 GET의 업무 조회 프로시저·조회수·감사 기록은 별도 영향으로 구분. 격리 환경에서 기술 담당 확인. |

코드 확인과 DB 정의 확인은 실행 성공·업무 승인·다른 환경 적용을 보장하지 않는다. 업무·기술 담당 검토 후 조사 목록의 상태를 완료로 변경한다.

브라우저 직접 근거: [settled-static-recheck](../../evidence/browser/static-stable.json). 경로·고정 버튼명·입력 속성·표 머리글·API 상태를 보관했고 실제 데이터 값·식별자·인증정보는 제외했다.

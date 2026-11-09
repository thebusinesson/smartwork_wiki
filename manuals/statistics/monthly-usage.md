# [서비스 현황] 월별 이용 현황 (세금, 계약) (조회·관리) 관리자 매뉴얼

작성 기준: `dc216b313` · 확인일 2026-11-09 · 조사 상태 **검토 대기**. 코드와 개발 DB 정의를 확인했으며 실제 화면·업무 실행은 미재현이다.

## 1) 화면 기본 정보

| 항목 | 작성 내용 |
|---|---|
| 업무 도메인·목적 | 월별 전자세금계산서와 전자계약 이용 건수·업체 수를 비교한다. |
| 메뉴·화면 경로 | 서비스 현황 > 통계 정보 > 월별 이용 현황 (세금, 계약); `/statistics/monthly-usage`; 메뉴 또는 관련 화면에서 진입한다. |
| 화면 유형·담당 | 조회·관리; WBS 작업자 유지윤. 업무·기술 담당 팀명은 원문에 없어 배포 전 해당 도메인 담당자가 확정한다. |
| 관련 화면 | [세금계산서 일별 현황](monthly-usage__daily-tax-invoice.md); [전자계약 일별 현황](monthly-usage__daily-electronic-contract.md) |

WBS 근거: No. 223 (사용자가 제공한 텍스트 행 284). API 개발/화면 개발의 중복 행은 같은 화면으로 통합했다.

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
|---|---|---|
| 화면 진입·조회 | `/statistics/monthly-usage` 메뉴 접근·하위 경로 작업 권한. 조회 API는 VIEW, 등록/수정 경로는 PROCESS 등 아래 서버 액션과 라우트 가드를 함께 적용한다. | 로그인된 관리자 계정; 아래 검색·입력 항목을 준비한다. |

서버가 최종 권한을 검사한다. 버튼 모양(kind)으로 권한을 추정하지 않는다. 특히 등록·수정이 PROCESS를 사용하는 API와 EXECUTE·UNMASK·EXCEL_DOWNLOAD는 서로 구분한다.

## 3) 화면 사용 절차

1. `서비스 현황 > 통계 정보 > 월별 이용 현황 (세금, 계약)` 메뉴를 연다. 경로 변수는 주소에서 임의로 바꾸지 않고 이전 화면이 전달한 식별자를 사용한다.
2. 현재 검색 조건과 아래 기본값을 확인한다. **이용월** 항목에 필요한 값을 입력하고 **검색**을 누른다.
3. 결과 행에서 업무 대상을 선택하여 관련 상세 화면으로 이동한다. 페이지 이동·검색 조건 변경 후에는 현재 조건과 조회 대상을 다시 확인한다.

**이 화면에서 유의할 업무 규칙**: 이용월로 검색하고 세금계산서/전자계약의 일별 상세 화면으로 이동한다. 월별 합계와 일별 합계의 집계 대상·기간을 맞춰 비교한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
|---|---|---|---|
| 이용월 | 입력·선택(조건부 검증 별도) | 화면 타입 monthRange | `usageMonth`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/MonthlyUsagePage.tsx#L20) |
| 월 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `monthHeader`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/MonthlyUsageTable.tsx#L53) |
| 누적가입자수 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `cumulativeSubscribersHeader`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/MonthlyUsageTable.tsx#L60) |
| 세금계산서 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `taxInvoiceGroup`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/MonthlyUsageTable.tsx#L67) |
| 전자계약 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `electronicContractGroup`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/MonthlyUsageTable.tsx#L73) |
| 합계 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `totalGroup`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/MonthlyUsageTable.tsx#L82) |
| 일반세금계산서 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `generalTaxInvoiceGroup`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/MonthlyUsageTable.tsx#L88) |
| 지로일반세금계산서 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `giroGeneralTaxInvoiceGroup`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/MonthlyUsageTable.tsx#L94) |
| 이용업체수 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `electronicContractCompaniesHeader`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/MonthlyUsageTable.tsx#L100) |
| 이용건수 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `electronicContractUsagesHeader`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/MonthlyUsageTable.tsx#L107) |
| 발행건수 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `totalIssuesHeader`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/MonthlyUsageTable.tsx#L117) |
| 발행업체수 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `generalTaxInvoiceCompaniesHeader`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/MonthlyUsageTable.tsx#L123) |
| 발행건수 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `generalTaxInvoiceIssuesHeader`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/MonthlyUsageTable.tsx#L129) |
| 발행업체수 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `giroGeneralTaxInvoiceCompaniesHeader`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/MonthlyUsageTable.tsx#L135) |
| 발행건수 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `giroGeneralTaxInvoiceIssuesHeader`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/MonthlyUsageTable.tsx#L141) |
| 월 | 출력 | API 타입 String | `month`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/MonthlyUsageTable.tsx#L162) |
| 누적가입자수 | 출력 | API 타입 Long | `cumulativeSubscribers`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/MonthlyUsageTable.tsx#L169) |
| 발행건수 | 출력 | API 타입 Long | `totalIssues`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/MonthlyUsageTable.tsx#L180) |
| 발행업체수 | 출력 | API 타입 Long | `generalTaxInvoiceCompanies`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/MonthlyUsageTable.tsx#L191) |
| 발행건수 | 출력 | API 타입 Long | `generalTaxInvoiceIssues`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/MonthlyUsageTable.tsx#L209) |
| 발행업체수 | 출력 | API 타입 Long | `giroGeneralTaxInvoiceCompanies`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/MonthlyUsageTable.tsx#L227) |
| 발행건수 | 출력 | API 타입 Long | `giroGeneralTaxInvoiceIssues`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/MonthlyUsageTable.tsx#L245) |
| 이용업체수 | 출력 | API 타입 Long | `electronicContractCompanies`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/MonthlyUsageTable.tsx#L263) |
| 이용건수 | 출력 | API 타입 Long | `electronicContractUsages`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/MonthlyUsageTable.tsx#L281) |

화면 필드 키와 API 필드명이 다른 경우 변환은 Hook/API의 검색·저장 매핑에서 수행된다. 요청·응답 필드와 DB 컬럼 매핑은 아래 API 계약 및 DB 객체 계약에 연결했다.

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
|---|---|---|---|
| 월별 이용 현황 리스트 조회 | [GET /api/v1/service-status/usage/monthly](../../references/api-contracts.md#api124); `/statistics/monthly-usage` / `VIEW` | `usageMonthStart, usageMonthEnd, page, size` → `content, totalElements, totalPages, currentPage, size, month, cumulativeSubscribers, totalIssues, totalIssuingCompanies, generalTaxInvoiceIssues, generalTaxInvoiceCompanies, giroGe` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
|---|---|---|---|
| [office.dbo.upGW_Sch_SumMonthDCT01](../../references/database-contracts.md#db037) | `@from_yymm varchar(7) IN, @to_yymm varchar(7) IN` | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.mng_monthly_dct_sum | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [office.dbo.upGW_Sch_SumMonthDTI01](../../references/database-contracts.md#db038) | `@from_yymm varchar(7) IN, @to_yymm varchar(7) IN` | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.mng_monthly_sum | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |

위 DB 계약 링크에는 실제 파라미터 타입·기본값·IN/OUT, Mapper 결과 컬럼, RETURN 바인딩, 참조 테이블·하위 프로시저·정의 필터/정렬을 기록했다. DTO·Service·Repository·Mapper의 상세 호출 경로는 각 API 계약에서 확인한다.

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
|---|---|---|
| 검색 결과가 없습니다. | [문구·처리 코드](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/components/MonthlyUsageTable.tsx#L304); 현재 조건·대상·권한 확인 | 검색·조회 오류면 조건을 확인 후 재조회. 변경·발송 결과가 불명확하면 처리 여부와 이력을 확인한 뒤 재시도 여부를 판단한다. |
| 결과가 없거나 기대 건수와 다름 | 적용된 검색 기준·기간·탭·대상 상태·서버 필터·페이징·목록/다운로드 조건 | 조건을 다시 확인하고 조회한다. 지속되면 경로·작업 시각·마스킹한 식별자·필터를 업무/기술 담당에게 전달한다. |
| 메뉴·버튼 미표시 또는 접근 거부 | 사용자 그룹의 메뉴 접근·VIEW 및 API별 PROCESS/EXECUTE/DELETE/EXCEL_DOWNLOAD/UNMASK 등 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. 프런트 버튼 표시만으로 서버 권한을 판단하지 않는다. |
| 저장·삭제·외부 실행의 결과가 불명확 | 대상 현재 상태·중복 요청·감사 이력·API 오류·파일/외부 소비 로그 | 기존 반영 여부를 먼저 조회한다. 중복 발송·초기화·금액 처리를 피하기 위해 기술 담당 확인 후 재시도한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
|---|---|---|
| 대상 선정 | 사용자가 WBS 탭 내용으로 제공한 텍스트의 No. 223; [선정 태스크](../../inventory/wbs-tasks.csv) | 제공 텍스트 확인 2026-11-09. 원본 Excel의 탭/병합 셀을 독립 재열람한 것은 아님. |
| 메뉴·라우트·화면 | [menuConfig.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts); [StatisticsRoutes.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/StatisticsRoutes.tsx); [MonthlyUsagePage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/statistics/MonthlyUsagePage.tsx) | 코드 확인 2026-11-09, 기준 dc216b313 |
| 기능·권한·API | 이 문서의 API 계약 링크 및 연결 Hook/API·Controller·DTO·Service·Repository·Mapper | 코드 확인 2026-11-09. 요청 실행·권한 계정별 재현은 미확인. |
| DB 정의 | [개발 DB 계약](../../references/database-contracts.md), 이 문서의 연결 객체 | 개발 DB 정의 확인 2026-11-09. 동적 SQL·CLR 내부·정의 미공개 참조의 미확정 범위는 객체별 기록; 후속 확인 DB 담당. |
| 브라우저 화면·배포 환경 | 실제 검증 계정의 정상·빈 결과·권한 부족·입력 오류 및 현재 배포본 | 미확인: 브라우저 실행 검증을 수행하지 않음. 배포 전 업무 담당·QA·기술 담당 확인. |
| 업무 프로시저·쓰기·외부 결과 | 격리된 검증 환경·테스트 데이터의 실행 결과 | 미확인: 공유 개발 DB의 업무 프로시저·쓰기·발송을 실행하지 않음. 격리 환경에서 기술 담당 확인. |

코드 확인과 DB 정의 확인은 실행 성공·업무 승인·다른 환경 적용을 보장하지 않는다. 업무·기술 담당 검토 후 조사 목록의 상태를 완료로 변경한다.

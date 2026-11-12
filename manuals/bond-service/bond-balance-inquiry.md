# [SB 서비스관리] 채권잔액 확인서 조회 (조회·관리) 관리자 매뉴얼

작성 기준: `dc216b313` · 확인일 2026-11-09 · 조사 상태 **검토 대기**. 코드·개발 DB 정의 확인. 브라우저: **화면 대조**; 저장·발송 등 업무 실행 결과는 미검증이다.

## 1) 화면 기본 정보

### 도메인 이해

특정 기준일에 거래 상대방과 확인할 채권잔액 확인서와 첨부를 찾는 문서 조사 업무다.

| 구분 | 설명 |
|---|---|
| 업무 영역 | 채권잔액 확인 서비스 > 채권잔액 확인서 조회 조회·관리 |
| 언제 사용하는가 | 업체·기준일에 해당하는 확인서의 상태나 원본을 확인할 때 |
| 주요 대상·데이터 | 기준일·채권잔액·계약자·문서 상태는 확인서의 범위를, 회사·사업자번호는 거래 당사자를 나타낸다. |
| 업무 흐름 | 기준일·업체·상태 검색 → 확인서 식별 → 상세·첨부 확인 |
| 이 페이지의 역할 | 채권잔액 확인서 중 **채권잔액 확인서 조회 조회·관리** 단계. 특정 기준일에 거래 상대방과 확인할 채권잔액 확인서와 첨부를 찾는 문서 조사 업무다. |
| 판단 결과·다음 업무 | 선택한 확인서의 회사 정보·잔액 확인 정보·파일을 상세에서 대조한다. |
| 다른 화면과의 구분 | 잔액을 실제 입금하거나 예치금으로 충전하는 화면이 아니며 송수신 장애는 전송·연동 로그에서 조사한다. |

설명 근거: [BondBalanceInquiryPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/BondBalanceInquiryPage.tsx), 이 문서 4·5·7번의 항목·API·업무 규칙. [상위 업무 영역](../../references/domain-overview.md#bond)은 공통 배경이며 현재 화면의 데이터·동작은 위 설명을 따른다. 설명 수정일 **2026-11-10**; 새 업무 실행 검증을 수행한 것은 아니다.

### 화면 정보

| 항목 | 작성 내용 |
|---|---|
| 업무 도메인·목적 | 특정 기준일에 거래 상대방과 확인할 채권잔액 확인서와 첨부를 찾는 문서 조사 업무다. |
| 메뉴·화면 경로 | SB 서비스관리 > 채권잔액 확인 서비스 > 채권잔액 확인서 조회; `/bond-service/bond-balance-inquiry`; 메뉴 또는 관련 화면에서 진입한다. |
| 화면 유형·담당 | 조회·관리; WBS 작업자 유지윤. 업무·기술 담당 팀명은 원문에 없어 배포 전 해당 도메인 담당자가 확정한다. |
| 관련 화면 | [상세](bond-balance-inquiry__by-drcNo.md) |

WBS 근거: No. 109 (사용자가 제공한 텍스트 행 140). API 개발/화면 개발의 중복 행은 같은 화면으로 통합했다.

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
|---|---|---|
| 화면 진입·조회 | `/bond-service/bond-balance-inquiry` 메뉴 접근·하위 경로 작업 권한. 조회 API는 VIEW, 등록/수정 경로는 PROCESS 등 아래 서버 액션과 라우트 가드를 함께 적용한다. | 로그인된 관리자 계정; 아래 검색·입력 항목을 준비한다. |

서버가 최종 권한을 검사한다. 버튼 모양(kind)으로 권한을 추정하지 않는다. 특히 등록·수정이 PROCESS를 사용하는 API와 EXECUTE·UNMASK·EXCEL_DOWNLOAD는 서로 구분한다.

## 3) 화면 사용 절차

**검증 시 화면 버튼**: 검색, 초기화. 화면 상태·대상에 따라 달라지며 아래 작업 절차와 권한 조건을 함께 확인한다.

1. `SB 서비스관리 > 채권잔액 확인 서비스 > 채권잔액 확인서 조회` 메뉴를 연다. 경로 변수는 주소에서 임의로 바꾸지 않고 이전 화면이 전달한 식별자를 사용한다.
2. 현재 검색 조건과 아래 기본값을 확인한다. **기준일, 업체 조건** 항목에 필요한 값을 입력하고 **검색**을 누른다.
3. 결과 행에서 업무 대상을 선택하여 관련 상세 화면으로 이동한다. 페이지 이동·검색 조건 변경 후에는 현재 조건과 조회 대상을 다시 확인한다.

**이 화면에서 유의할 업무 규칙**: 목록에서 확인서를 선택해 상세로 이동한다. 첨부파일은 백엔드 다운로드 경로로 제공되며 파일명·대상 확인서 번호·파일 보관 위치를 구분한다.

## 4) 입력·표시 데이터

**검증 시 표시된 날짜 필터**: 시작일 `2026-03-01`, 종료일 `2026-11-09`. 검증 날짜·조건 복원에 따른 표시값이며 모든 실행의 고정 기본값을 뜻하지 않는다.

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
|---|---|---|---|
| 기준일 | 출력 | API 타입 String | `basicDate`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/BondBalanceInquiryPage.tsx#L59) |
| 채권잔액 | 출력 | API 타입 String? | `receivableBalance`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/BondBalanceInquiryPage.tsx#L60) |
| 계약자 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `contractor`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/BondBalanceInquiryPage.tsx#L61) |
| 상태 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `status`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/BondBalanceInquiryPage.tsx#L62) |
| 요금제 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `contractors.billType`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/BondBalanceInquiryPage.tsx#L63) |
| 구분 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `contractors.category`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/BondBalanceInquiryPage.tsx#L66) |
| 사업자번호 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `contractors.comRegno`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/BondBalanceInquiryPage.tsx#L67) |
| 회사명 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `contractors.comName`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/BondBalanceInquiryPage.tsx#L68) |
| 담당자 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `contractors.memName`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/BondBalanceInquiryPage.tsx#L69) |
| 요금제 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `contractors`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/BondBalanceInquiryPage.tsx#L146) |
| 기준일 | 입력·선택(조건부 검증 별도) | 화면 타입 dateRange; 초기값 {getDefaultDateRange()} | `dateRange`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/BondBalanceInquiryPage.tsx#L185) |
| 업체 조건 | 입력·선택(조건부 검증 별도) | 화면 타입 selectWithInput; 선택: 전체=all, 사업자번호=bizNo, 회사명=companyName; 초기값 selectValue=bizNo; inputValue=빈값 | `companyCondition`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/BondBalanceInquiryPage.tsx#L189) |
| 전자문서 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `docs-yn`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/BondBalanceInquiryPage.tsx#L232) |
| 구분 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/BondBalanceInquiryPage.tsx#L331) |
| 채무자 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `com-type-D`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/BondBalanceInquiryPage.tsx#L338) |
| 채권자 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `com-type-C`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/BondBalanceInquiryPage.tsx#L346) |
| 상태별 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/BondBalanceInquiryPage.tsx#L352) |
| 미승인 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `status-C`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/BondBalanceInquiryPage.tsx#L359) |
| 승인 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `status-A`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/BondBalanceInquiryPage.tsx#L367) |
| 거부 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `status-R`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/BondBalanceInquiryPage.tsx#L375) |
| 취소 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `status-Q`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/BondBalanceInquiryPage.tsx#L384) |
| 회원구분 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/BondBalanceInquiryPage.tsx#L390) |
| 회원 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `nm-N`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/BondBalanceInquiryPage.tsx#L401) |
| 비회원 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `nm-Y`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/BondBalanceInquiryPage.tsx#L405) |

입력 검증 근거: [BondBalanceInquiryPage.checks.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/service/bondservice/BondBalanceInquiryPage.checks.ts). 프런트 검증과 서버 DTO 제약이 다르면 서버 검증이 최종 기준이다.

**복합 검색·폼의 초기 상태**

| 초기값 근거 | 기본 상태 |
|---|---|
| [DEFAULT_FILTER_VALUES](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/BondBalanceInquiryPage.tsx#L164) | dateRange={getDefaultDateRange()}; companyCondition=selectValue=bizNo; inputValue=빈값; docsYn=N; isCreditor=켜짐; isDebtor=켜짐; isUnapproved=켜짐; isApproved=켜짐; isRejected=켜짐; isCanceled=켜짐; nmYn=N |
| [initialApplied](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/BondBalanceInquiryPage.tsx#L243) | startDate={defaultRange.startDate.slice(0, 10)}; endDate={defaultRange.endDate.slice(0, 10)}; searchType=ALL; keyword=빈값; comTypes=C, D; statusCodes=C, A, R, Q; nmYn=N; docsYn=N |

화면 필드 키와 API 필드명이 다른 경우 변환은 Hook/API의 검색·저장 매핑에서 수행된다. 요청·응답 필드와 DB 컬럼 매핑은 아래 API 계약 및 DB 객체 계약에 연결했다.

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
|---|---|---|---|
| 채권잔액 확인서 목록 조회 | [GET /api/v1/bond-service/creditor-balance-certificates](../../references/api-contracts.md#api028); `/bond-service/bond-balance-inquiry` / `VIEW` | `startDate, endDate, searchType, keyword, comTypes, statusCodes, nmYn, docsYn, page, size` → `content, totalElements, totalPages, page, size, drcNo, basicDate, receivableBalance, creditor, debtor, statusLabel, transferStatusLabel, comRegno, comName, memName, billType` | Mapper 프로시저의 정적 테이블 쓰기 미검출; 동적 SQL의 런타임 대상은 미확정 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
|---|---|---|---|
| [smartwork.dbo.UspDrcContractComLst](../../references/database-contracts.md#db327) | `@StartDate varchar(10) IN, @EndDate varchar(10) IN, @SearchType char(1) IN, @SearchText varchar(200) IN, @Com_Type varchar(100) IN, @Status_Code varchar(100) IN` | 확정한 테이블 쓰기 없음. 참조: sb_drc.dbo.drc_company, sb_drc.dbo.drc_main, sb_drc.dbo.drc_status, sb_drc.dbo.drc_use, smartbill3.dbo.company, smartbill3.dbo.member 동적 SQL 포함, 런타임 조합 대상 미확정. | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.UspDrcContractComLstNm](../../references/database-contracts.md#db328) | `@StartDate varchar(10) IN, @EndDate varchar(10) IN, @SearchType char(1) IN, @SearchText varchar(200) IN, @Com_Type varchar(100) IN, @Status_Code varchar(100) IN` | 확정한 테이블 쓰기 없음. 참조: sb_drc.dbo.drc_company_nm, sb_drc.dbo.drc_main, sb_drc.dbo.drc_status_nm, sb_drc.dbo.drc_use, smartbill3.dbo.company, smartbill3.dbo.member 동적 SQL 포함, 런타임 조합 대상 미확정. | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| 파일: storage.drc | 확인서 파일 상대 경로 + 설정 루트 | 확인서 첨부를 파일시스템에서 읽는다. 다운로드 권한·정규화된 경로·파일 존재 확인 | [StorageProperties.kt](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/shared/upload/config/StorageProperties.kt) |

위 DB 계약 링크에는 실제 파라미터 타입·기본값·IN/OUT, Mapper 결과 컬럼, RETURN 바인딩, 참조 테이블·하위 프로시저·정의 필터/정렬을 기록했다. DTO·Service·Repository·Mapper의 상세 호출 경로는 각 API 계약에서 확인한다.

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
|---|---|---|
| 결과가 없거나 기대 건수와 다름 | 적용된 검색 기준·기간·탭·대상 상태·서버 필터·페이징·목록/다운로드 조건 | 조건을 다시 확인하고 조회한다. 지속되면 경로·작업 시각·마스킹한 식별자·필터를 업무/기술 담당에게 전달한다. |
| 메뉴·버튼 미표시 또는 접근 거부 | 사용자 그룹의 메뉴 접근·VIEW 및 API별 PROCESS/EXECUTE/DELETE/EXCEL_DOWNLOAD/UNMASK 등 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. 프런트 버튼 표시만으로 서버 권한을 판단하지 않는다. |
| 저장·삭제·외부 실행의 결과가 불명확 | 대상 현재 상태·중복 요청·감사 이력·API 오류·파일/외부 소비 로그 | 기존 반영 여부를 먼저 조회한다. 중복 발송·초기화·금액 처리를 피하기 위해 기술 담당 확인 후 재시도한다. |

## 7) 검증·출처

**브라우저 검증(2026-11-09)**: 화면 대조. [경로별 결과와 제한](../../references/browser-verification.md#page021). 역할별 권한 거부·저장 성공·파일 반출·외부 연계 완료는 이 결과로 보장하지 않는다.

| 검증 항목 | 근거·환경 | 상태·확인일 |
|---|---|---|
| 대상 선정 | 사용자가 WBS 탭 내용으로 제공한 텍스트의 No. 109; [선정 태스크](../../inventory/wbs-tasks.csv) | 제공 텍스트 확인 2026-11-09. 원본 Excel의 탭/병합 셀을 독립 재열람한 것은 아님. |
| 메뉴·라우트·화면 | [menuConfig.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts); [BondServiceRoutes.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/BondServiceRoutes.tsx); [BondBalanceInquiryPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/BondBalanceInquiryPage.tsx) | 코드 확인 2026-11-09, 기준 dc216b313 |
| 기능·권한·API | 이 문서의 API 계약 링크 및 연결 Hook/API·Controller·DTO·Service·Repository·Mapper | 코드 확인 2026-11-09. 조회 요청·화면 대조 범위는 아래 브라우저 근거 참조. 권한 계정별 허용·거부 및 변경 요청 실행은 미확인. |
| DB 정의 | [개발 DB 계약](../../references/database-contracts.md), 이 문서의 연결 객체 | 개발 DB 정의 확인 2026-11-09. 동적 SQL·CLR 내부·정의 미공개 참조의 미확정 범위는 객체별 기록; 후속 확인 DB 담당. |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-7cd21e16d0fcce8a) | Demo 메타데이터 2/2개 확인 · 2026-11-11 |
| 브라우저 화면·배포 환경 | 로컬 인증 계정·Playwright CLI; [화면별 검증표](../../references/browser-verification.md#page021) | 화면 대조, 2026-11-09. 배포본·타 역할·업무 변경 결과는 미확인. |
| 업무 프로시저·쓰기·외부 결과 | 격리된 검증 환경·테스트 데이터의 실행 결과 | 미확인: 명시적인 저장·삭제·발송·초기화 요청은 실행하지 않음. 브라우저 GET의 업무 조회 프로시저·조회수·감사 기록은 별도 영향으로 구분. 격리 환경에서 기술 담당 확인. |

코드 확인과 DB 정의 확인은 실행 성공·업무 승인·다른 환경 적용을 보장하지 않는다. 업무·기술 담당 검토 후 조사 목록의 상태를 완료로 변경한다.

브라우저 직접 근거: [test-company-search](../../evidence/browser/targeted-stable.json). 경로·고정 버튼명·입력 속성·표 머리글·API 상태를 보관했고 실제 데이터 값·식별자·인증정보는 제외했다.

# [SB 고객관리] 스마트빌 가입조회 (조회·관리) 관리자 매뉴얼

작성 기준: `dc216b313` · 확인일 2026-11-09 · 조사 상태 **검토 대기**. 코드·개발 DB 정의 확인. 브라우저: **화면 대조**; 저장·발송 등 업무 실행 결과는 미검증이다.

## 1) 화면 기본 정보

| 항목 | 작성 내용 |
|---|---|
| 업무 도메인·목적 | 거래업체 파일을 업로드하여 스마트빌 가입 여부를 확인하고 업로드별 처리 결과를 조회한다. |
| 메뉴·화면 경로 | SB 고객관리 > 스마트빌 회원·회사정보 관리 > 스마트빌 가입조회; `/company-management/registration-inquiry`; 메뉴 또는 관련 화면에서 진입한다. |
| 화면 유형·담당 | 조회·관리; WBS 작업자 유지윤. 업무·기술 담당 팀명은 원문에 없어 배포 전 해당 도메인 담당자가 확정한다. |
| 관련 화면 | [상세](registration-inquiry__by-uploadId.md) |

WBS 근거: No. 25 (사용자가 제공한 텍스트 행 45). API 개발/화면 개발의 중복 행은 같은 화면으로 통합했다.

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
|---|---|---|
| 화면 진입·조회 | `/company-management/registration-inquiry` 메뉴 접근·하위 경로 작업 권한. 조회 API는 VIEW, 등록/수정 경로는 PROCESS 등 아래 서버 액션과 라우트 가드를 함께 적용한다. | 로그인된 관리자 계정; 아래 검색·입력 항목을 준비한다. |
| 가입 여부 확인 | `/company-management/registration-inquiry`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |

서버가 최종 권한을 검사한다. 버튼 모양(kind)으로 권한을 추정하지 않는다. 특히 등록·수정이 PROCESS를 사용하는 API와 EXECUTE·UNMASK·EXCEL_DOWNLOAD는 서로 구분한다.

## 3) 화면 사용 절차

**검증 시 화면 버튼**: 파일 선택, 업로드 (비활성), 샘플 다운로드, 검색 필터 열기. 화면 상태·대상에 따라 달라지며 아래 작업 절차와 권한 조건을 함께 확인한다.

1. **SB 고객관리 > 스마트빌 회원·회사정보 관리 > 스마트빌 가입조회**를 연다. 날짜·파일명 검색 영역은 처음에 접혀 있다.
2. 기존 결과를 찾을 때 **검색 필터 열기**를 누르고 날짜조건·파일명을 지정한 뒤 **검색**한다.
3. 목록에서 대상 업로드의 **가입 여부 확인**을 눌러 상세 결과로 이동한다.
4. 새 파일은 **샘플 다운로드**로 양식을 확인한 뒤 **파일 선택**한다. 파일 선택만으로 업로드되지 않는다. 기존 데이터 교체 영향을 확인한 뒤 **업로드**한다. 완료 후 성공·실패 행 수와 상세 결과를 확인한다. 실제 업로드 완료는 격리 환경 후속 검증 대상이다.

**이 화면에서 유의할 업무 규칙**: 양식은 순번/사업자번호/회사명/이메일을 사용하며 첫 시트의 헤더 이름으로 열을 찾는다. 사업자번호 열이 필수이고 회사명·이메일 열은 선택이다. xls/xlsx는 파일 내용으로 판별하고 사업자번호는 하이픈 제거 후 숫자 10자리로 검증한다. 유효 행이 0개면 저장 전에 중단한다. 유효 행이 있는 업로드는 고정 cafe_id=frontier의 기존 TAX_MEMCFRM·TAX_MEMCFRM_DETAIL을 삭제한 뒤 최신 메타와 유효 행으로 교체한다. 따라서 과거 파일을 단순 누적하는 업로드가 아니며 다른 담당자의 같은 범위 결과에도 영향을 줄 수 있다. 업로드 원본은 서비스에서 메모리로 파싱하며 이 처리 경로에 원본 파일 영구 보관 호출은 없다. 완료 후 성공·실패 행 수를 확인하고 상세 결과를 조회한다.

**실제 진입·검색 버튼**: 최초에는 날짜·파일명 검색 영역이 접혀 있다. **검색 필터 열기**를 눌러 조건을 펼친 뒤 **검색**한다. 목록의 **가입 여부 확인** 버튼으로 해당 업로드의 상세 결과에 진입한다. 파일 작업 버튼의 실제 표기는 **파일 선택 → 업로드**, 양식 받기는 **샘플 다운로드**다.

비식별 화면 캡처: [초기 화면·빈값 검증](../../evidence/screenshots/registration-initial.png). 입력·사용자 영역·표 본문은 마스킹했다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
|---|---|---|---|
| 날짜조건 | 입력·선택(조건부 검증 별도) | 화면 타입 selectWithDateRange; API 타입 String; 선택: 전체=all, 업로드 일자=uploadDate; 초기값 selectValue=all; dateRange=startDate=빈값; endDate=빈값 | `uploadDate`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/pages/RegistrationInquiryListPage.tsx#L196) |
| 파일명 | 입력·선택(조건부 검증 별도) | 화면 타입 toggleableText; API 타입 String; 초기값 isAll=꺼짐; inputValue=빈값 | `filename`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/pages/RegistrationInquiryListPage.tsx#L210) |
| 파일 첨부 | 입력·선택(조건부 검증 별도) | 길이·형식·조건부 필수는 검증 코드와 API DTO 참조 | `file`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/pages/RegistrationInquiryListPage.tsx#L237) |
| 업로드 일자 | 출력 | API 타입 String; 초기값 selectValue=all; dateRange=startDate=빈값; endDate=빈값 | `uploadDate`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/RegistrationInquiryTable.tsx#L37) |
| 파일명 | 출력 | API 타입 String; 초기값 isAll=꺼짐; inputValue=빈값 | `filename`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/RegistrationInquiryTable.tsx#L44) |
| 업체수 | 출력 | API 타입 Int | `companyCount`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/RegistrationInquiryTable.tsx#L50) |
| 스마트빌 가입 확인 | 출력 | API 타입 Int | `id`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/RegistrationInquiryTable.tsx#L56) |

입력 검증 근거: [RegistrationInquiryListPage.schema.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/customer/company/pages/RegistrationInquiryListPage.schema.ts). 프런트 검증과 서버 DTO 제약이 다르면 서버 검증이 최종 기준이다.

**복합 검색·폼의 초기 상태**

| 초기값 근거 | 기본 상태 |
|---|---|
| [INITIAL_FILTER_VALUES](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/pages/RegistrationInquiryListPage.tsx#L46) | uploadDate=selectValue=all; dateRange=startDate=빈값; endDate=빈값; filename=isAll=꺼짐; inputValue=빈값 |

화면 필드 키와 API 필드명이 다른 경우 변환은 Hook/API의 검색·저장 매핑에서 수행된다. 요청·응답 필드와 DB 컬럼 매핑은 아래 API 계약 및 DB 객체 계약에 연결했다.

파일 선택 제약은 `.xls`·`.xlsx`, 빈 파일 제외, 최대 10MB다. 서버는 확장자와 별도로 실제 엑셀 내용을 파싱하고 첫 시트의 사업자번호 헤더를 확인한다. 파일을 선택하는 동작과 기존 조회 결과를 교체하는 **업로드** 실행을 구분한다.

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
|---|---|---|---|
| 업로드 이력 조회 | [GET /api/v1/registration-inquiry/uploads](../../references/api-contracts.md#api075); `/company-management/registration-inquiry` / `VIEW` | `경로·쿼리·본문 계약 참조` → `content, totalElements, totalPages, page, size, id, uploadDate, filename, companyCount` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 샘플 엑셀 다운로드 | [GET /api/v1/registration-inquiry/sample-template](../../references/api-contracts.md#api074); `/company-management/registration-inquiry` / `VIEW` | `경로·쿼리·본문 계약 참조` → `응답 DTO·파일/처리 결과 계약 참조` | 파일·외부 연계·공통 저장소/검사 호출: 상세 계약 참조 |
| 엑셀 파일 업로드 | [POST /api/v1/registration-inquiry/upload](../../references/api-contracts.md#api223); `/company-management/registration-inquiry` / `EXCEL_UPLOAD` | `경로·쿼리·본문 계약 참조` → `uploadId, filename, companyCount, uploadDate, totalCount, successCount, errorCount, errors, rowNumber, message` | 쓰기 대상 smartbill3.dbo.tax_memcfrm, smartbill3.dbo.tax_memcfrm_detail |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
|---|---|---|---|
| [Office.dbo.upCafe_Lst_MemCfrm_File](../../references/database-contracts.md#db012) | `@cafe_id varchar(15) IN` | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.tax_memcfrm, smartbill3.dbo.tax_memcfrm_detail | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Office.dbo.upCafe_Sav_Memcfrm02](../../references/database-contracts.md#db013) | `@cafe_id varchar(15) IN, @com_regno varchar(13) IN, @com_name varchar(70) IN, @mem_email varchar(70) IN, @mem_hp varchar(14) IN` | 쓰기: smartbill3.dbo.tax_memcfrm_detail. 참조: smartbill3.dbo.tax_memcfrm_detail | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Office.dbo.upCafe_Sav_MemcfrmFile](../../references/database-contracts.md#db014) | `@cafe_id varchar(15) IN, @mem_name varchar(24) IN, @bulk_file varchar(100) IN` | 쓰기: smartbill3.dbo.tax_memcfrm, smartbill3.dbo.tax_memcfrm_detail. 참조: smartbill3.dbo.tax_memcfrm, smartbill3.dbo.tax_memcfrm_detail | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| 업로드 원본·엑셀 생성 | 첫 시트 헤더: 사업자번호 필수, 회사명/이메일 선택; 데이터 2행부터 | 원본 bytes를 메모리 파싱. cafe_id=frontier의 기존 조회 메타·상세를 교체; 유효 행 0개면 교체 전 중단 | [RegistrationInquiryService.kt](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/registrationinquiry/service/RegistrationInquiryService.kt) |

위 DB 계약 링크에는 실제 파라미터 타입·기본값·IN/OUT, Mapper 결과 컬럼, RETURN 바인딩, 참조 테이블·하위 프로시저·정의 필터/정렬을 기록했다. DTO·Service·Repository·Mapper의 상세 호출 경로는 각 API 계약에서 확인한다.

**파일**: 업로드·다운로드의 소유 대상, 원래 파일명, 저장 경로 설정, 파일 존재 여부를 구분한다. 저장소 경로와 비밀값은 사용자 입력으로 대체하지 않는다. 파일·외부 연계 상세는 API의 연결 Service·설정 키 근거를 참조한다.

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
|---|---|---|
| 검색 결과가 없습니다. | [문구·처리 코드](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/RegistrationInquiryTable.tsx#L74); 현재 조건·대상·권한 확인 | 검색·조회 오류면 조건을 확인 후 재조회. 변경·발송 결과가 불명확하면 처리 여부와 이력을 확인한 뒤 재시도 여부를 판단한다. |
| 결과가 없거나 기대 건수와 다름 | 적용된 검색 기준·기간·탭·대상 상태·서버 필터·페이징·목록/다운로드 조건 | 조건을 다시 확인하고 조회한다. 지속되면 경로·작업 시각·마스킹한 식별자·필터를 업무/기술 담당에게 전달한다. |
| 메뉴·버튼 미표시 또는 접근 거부 | 사용자 그룹의 메뉴 접근·VIEW 및 API별 PROCESS/EXECUTE/DELETE/EXCEL_DOWNLOAD/UNMASK 등 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. 프런트 버튼 표시만으로 서버 권한을 판단하지 않는다. |
| 저장·삭제·외부 실행의 결과가 불명확 | 대상 현재 상태·중복 요청·감사 이력·API 오류·파일/외부 소비 로그 | 기존 반영 여부를 먼저 조회한다. 중복 발송·초기화·금액 처리를 피하기 위해 기술 담당 확인 후 재시도한다. |

## 7) 검증·출처

**브라우저 검증(2026-11-09)**: 화면 대조. [경로별 결과와 제한](../../references/browser-verification.md#page006). 역할별 권한 거부·저장 성공·파일 반출·외부 연계 완료는 이 결과로 보장하지 않는다.

| 검증 항목 | 근거·환경 | 상태·확인일 |
|---|---|---|
| 대상 선정 | 사용자가 WBS 탭 내용으로 제공한 텍스트의 No. 25; [선정 태스크](../../inventory/wbs-tasks.csv) | 제공 텍스트 확인 2026-11-09. 원본 Excel의 탭/병합 셀을 독립 재열람한 것은 아님. |
| 메뉴·라우트·화면 | [menuConfig.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts); [CustomerRoutes.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/CustomerRoutes.tsx); [RegistrationInquiryListPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/pages/RegistrationInquiryListPage.tsx) | 코드 확인 2026-11-09, 기준 dc216b313 |
| 기능·권한·API | 이 문서의 API 계약 링크 및 연결 Hook/API·Controller·DTO·Service·Repository·Mapper | 코드 확인 2026-11-09. 조회 요청·화면 대조 범위는 아래 브라우저 근거 참조. 권한 계정별 허용·거부 및 변경 요청 실행은 미확인. |
| DB 정의 | [개발 DB 계약](../../references/database-contracts.md), 이 문서의 연결 객체 | 개발 DB 정의 확인 2026-11-09. 동적 SQL·CLR 내부·정의 미공개 참조의 미확정 범위는 객체별 기록; 후속 확인 DB 담당. |
| 브라우저 화면·배포 환경 | 로컬 인증 계정·Playwright CLI; [화면별 검증표](../../references/browser-verification.md#page006) | 화면 대조, 2026-11-09. 배포본·타 역할·업무 변경 결과는 미확인. |
| 업무 프로시저·쓰기·외부 결과 | 격리된 검증 환경·테스트 데이터의 실행 결과 | 미확인: 명시적인 저장·삭제·발송·초기화 요청은 실행하지 않음. 브라우저 GET의 업무 조회 프로시저·조회수·감사 기록은 별도 영향으로 구분. 격리 환경에서 기술 담당 확인. |

코드 확인과 DB 정의 확인은 실행 성공·업무 승인·다른 환경 적용을 보장하지 않는다. 업무·기술 담당 검토 후 조사 목록의 상태를 완료로 변경한다.

브라우저 직접 근거: [settled-static-recheck](../../evidence/browser/static-stable.json). 경로·고정 버튼명·입력 속성·표 머리글·API 상태를 보관했고 실제 데이터 값·식별자·인증정보는 제외했다.

# [SB 서비스관리] 이메일파싱 모니터링 (조회·관리) 관리자 매뉴얼

작성 기준: `dc216b313` · 확인일 2026-11-09 · 조사 상태 **검토 대기**. 코드와 개발 DB 정의를 확인했으며 실제 화면·업무 실행은 미재현이다.

## 1) 화면 기본 정보

| 항목 | 작성 내용 |
|---|---|
| 업무 도메인·목적 | 이메일 파싱 자동 수집 실행 상태와 상세 오류 로그를 확인한다. |
| 메뉴·화면 경로 | SB 서비스관리 > 홈택스 DTI 수집 > 이메일파싱 모니터링; `/hometax-dti/email-parsing`; 메뉴 또는 관련 화면에서 진입한다. |
| 화면 유형·담당 | 조회·관리; WBS 작업자 유지윤. 업무·기술 담당 팀명은 원문에 없어 배포 전 해당 도메인 담당자가 확정한다. |
| 관련 화면 | 같은 메뉴에 별도 독립 경로 없음. 팝업·탭은 이 문서 참조. |

WBS 근거: No. 131 (사용자가 제공한 텍스트 행 165). API 개발/화면 개발의 중복 행은 같은 화면으로 통합했다.

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
|---|---|---|
| 화면 진입·조회 | `/hometax-dti/email-parsing` 메뉴 접근·하위 경로 작업 권한. 조회 API는 VIEW, 등록/수정 경로는 PROCESS 등 아래 서버 액션과 라우트 가드를 함께 적용한다. | 로그인된 관리자 계정; 아래 검색·입력 항목을 준비한다. |
| 엑셀 다운로드 | `/hometax-dti/email-parsing`; 엑셀 download 화면 게이트. 다운로드/업로드 API의 서버 권한과 사유 입력을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |

서버가 최종 권한을 검사한다. 버튼 모양(kind)으로 권한을 추정하지 않는다. 특히 등록·수정이 PROCESS를 사용하는 API와 EXECUTE·UNMASK·EXCEL_DOWNLOAD는 서로 구분한다.

## 3) 화면 사용 절차

1. `SB 서비스관리 > 홈택스 DTI 수집 > 이메일파싱 모니터링` 메뉴를 연다. 경로 변수는 주소에서 임의로 바꾸지 않고 이전 화면이 전달한 식별자를 사용한다.
2. 현재 검색 조건과 아래 기본값을 확인한다. **실행일자, 허브업체명, 실행여부, 사용여부, 연동 구분, 운영여부, 오류발생** 항목에 필요한 값을 입력하고 **검색**을 누른다.
3. 결과 표·탭·팝업에서 대상의 상태와 합계·이력을 확인한다. 다른 조회 조건으로 바꾼 경우 다시 검색하여 결과를 갱신한다.

**이 화면에서 유의할 업무 규칙**: 실행일자는 기본 오늘, 운영여부는 운영(O)이다. 검색 결과에서 상세 로그를 확인한다. 다운로드는 목록 정보 외에 최신 오류 메시지 확인을 위해 상세 로그를 추가 조회할 수 있다.

**반출**: 적용된 검색 조건과 반출 범위를 확인한 후 다운로드한다. 사유 입력창이 표시되면 업무 사유를 입력한다. 사유 등록 실패·파일 오류는 성공으로 간주하지 않고 다운로드 결과를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
|---|---|---|---|
| 실행일자 | 입력·필수 | 화면 타입 date; 초기값 오늘 | `date`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/EmailParsingMonitoringPage.tsx#L118) |
| 허브업체명 | 입력·선택(조건부 검증 별도) | 화면 타입 text; API 타입 String?; 기본 null; 서버 검증 @field:Size(max = 50, message = "hubName 은 50자 이하여야 합니다."); 초기값 빈값 | `hubName`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/EmailParsingMonitoringPage.tsx#L119) |
| 실행여부 | 입력·선택(조건부 검증 별도) | 화면 타입 radio; API 타입 String?; 기본 null; 서버 검증 @field:Pattern(regexp = "^(O\|X\|)$", message = "isUse 는 O/X 또는 빈값이어야 합니다."); 선택: 전체=all, O=O, X=X; 초기값 all | `isUse`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/EmailParsingMonitoringPage.tsx#L120) |
| 사용여부 | 입력·선택(조건부 검증 별도) | 화면 타입 radio; API 타입 String?; 기본 null; 서버 검증 @field:Pattern(regexp = "^(Y\|N\|)$", message = "useYn 은 Y/N 또는 빈값이어야 합니다."); 선택: 전체=all, 사용=Y, 미사용=N; 초기값 all | `useYn`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/EmailParsingMonitoringPage.tsx#L121) |
| 연동 구분 | 입력·선택(조건부 검증 별도) | 화면 타입 radio; API 타입 String?; 기본 null; 서버 검증 @field:Pattern(regexp = "^(SAP\|NONSAP\|)$", message = "isDiv 는 SAP/NONSAP 또는 빈값이어야 합니다."); 선택: 전체=all, SAP=SAP, NONSAP=NONSAP; 초기값 all | `isDiv`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/EmailParsingMonitoringPage.tsx#L122) |
| 운영여부 | 입력·선택(조건부 검증 별도) | 화면 타입 radio; API 타입 String?; 기본 null; 서버 검증 @field:Pattern(regexp = "^(O\|T\|A\|)$", message = "isClass 는 O/T/A 또는 빈값이어야 합니다."); 선택: 전체=A, 운영=O, 테스트=T; 초기값 O | `isClass`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/EmailParsingMonitoringPage.tsx#L123) |
| 오류발생 | 입력·선택(조건부 검증 별도) | 화면 타입 radio; API 타입 String?; 기본 null; 서버 검증 @field:Pattern(regexp = "^(O\|X\|)$", message = "isError 는 O/X 또는 빈값이어야 합니다."); 선택: 전체=all, 오류발생=O, 오류미발생=X; 초기값 all | `isError`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/EmailParsingMonitoringPage.tsx#L124) |
| 허브업체명 | 출력 | API 타입 String? | `hubRealname`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/EmailParsingMonitoringPage.tsx#L232) |
| 연동여부 | 출력 | API 타입 String? | `division`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/EmailParsingMonitoringPage.tsx#L233) |
| 실행여부 | 출력 | API 타입 Boolean | `executionRan`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/EmailParsingMonitoringPage.tsx#L234) |
| 시작 | 출력 | API 타입 String? | `startDay`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/EmailParsingMonitoringPage.tsx#L241) |
| 생존시간 | 출력 | API 타입 String? | `endDay`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/EmailParsingMonitoringPage.tsx#L248) |
| 오류발생 | 출력 | API 타입 Boolean | `errOccurred`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/EmailParsingMonitoringPage.tsx#L255) |
| 로그보기 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `logView`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/EmailParsingMonitoringPage.tsx#L262) |
| 제목 | 출력 | API 타입 String? | `logTitle`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/components/EmailParsingMonitoringDetailDialog.tsx#L129) |
| 사업자번호 | 출력 | API 타입 String?; 기본 null; 서버 검증 @field:Size(max = 13, message = "comRegno 는 13자 이하여야 합니다.") | `comRegno`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/components/EmailParsingMonitoringDetailDialog.tsx#L130) |
| 내용 | 출력 | API 타입 String? | `logContent`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/components/EmailParsingMonitoringDetailDialog.tsx#L136) |
| 일시 | 출력 | API 타입 String? | `logDate`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/components/EmailParsingMonitoringDetailDialog.tsx#L137) |
| 에러 | 출력 | API 타입 String? | `errMessage`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/components/EmailParsingMonitoringDetailDialog.tsx#L138) |
| ISSUE_ID | 출력 | API 타입 String? | `issueId`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/components/EmailParsingMonitoringDetailDialog.tsx#L149) |

**복합 검색·폼의 초기 상태**

| 초기값 근거 | 기본 상태 |
|---|---|
| [createDefaultFilters](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/EmailParsingMonitoringPage.tsx#L55) | date=오늘; hubName=빈값; isUse=all; useYn=all; isDiv=all; isClass=O; isError=all |

화면 필드 키와 API 필드명이 다른 경우 변환은 Hook/API의 검색·저장 매핑에서 수행된다. 요청·응답 필드와 DB 컬럼 매핑은 아래 API 계약 및 DB 객체 계약에 연결했다.

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
|---|---|---|---|
| 이메일파싱 모니터링 목록 (in-memory 페이징) | [GET /api/v1/sb-service/hometax-dti-installed/email-parsing-monitoring](../../references/api-contracts.md#api088); `/hometax-dti/email-parsing` / `VIEW` | `startDate, endDate, hubName, useYn, isUse, isError, isDiv, isClass, page, size` → `content, totalElements, totalPages, page, size, sbKey, hubRealname, startDay, endDay, errCnt, mode, division, useYn, klass, errOccurred, executionRan` | Mapper 프로시저의 정적 테이블 쓰기 미검출; 동적 SQL의 런타임 대상은 미확정 |
| 이메일파싱 모니터링 상세 로그 (KEY 기준, 서버 페이징) | [GET /api/v1/sb-service/hometax-dti-installed/email-parsing-monitoring/detail](../../references/api-contracts.md#api089); `/hometax-dti/email-parsing` / `VIEW` | `key, startDate, endDate, isError, comRegno, page, size` → `content, totalElements, totalPages, page, size, comRegno, logTitle, logContent, logDate, errCode, errMessage, issueId, errOccurred` | Mapper 프로시저의 정적 테이블 쓰기 미검출; 동적 SQL의 런타임 대상은 미확정 |
| 이메일파싱 모니터링 엑셀 다운로드 | [GET /api/v1/sb-service/hometax-dti-installed/email-parsing-monitoring/download](../../references/api-contracts.md#api090); `/hometax-dti/email-parsing` / `EXCEL_DOWNLOAD` | `startDate, endDate, hubName, useYn, isUse, isError, isDiv, isClass, page, size` → `응답 DTO·파일/처리 결과 계약 참조` | Mapper 프로시저의 정적 테이블 쓰기 미검출; 동적 SQL의 런타임 대상은 미확정 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
|---|---|---|---|
| [SB_SCRAPER.dbo.USE_COMPANY_INFO](../../references/database-contracts.md#db181) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: sb_scraper.dbo.use_company_info | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_SCRAPER.dbo.SSP_EP_ESERO_MONITOR_AUTO](../../references/database-contracts.md#db172) | `@START datetime IN, @END datetime IN, @HUBNAME varchar(50) IN, @USEYN char(1) IN, @ISUSE char(1) IN, @ISERROR char(1) IN, @ISDIV varchar(6) IN, @ISCLASS char(1) IN` | 확정한 테이블 쓰기 없음. 참조: sb_scraper.dbo.ep_use_log, sb_scraper.dbo.use_company_info 동적 SQL 포함, 런타임 조합 대상 미확정. | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_SCRAPER.dbo.SSP_EP_ESERO_DETAIL](../../references/database-contracts.md#db171) | `@KEY varchar(36) IN, @START datetime IN, @END datetime IN, @PAGENUM int IN, @PAGESIZE int IN, @ISERROR char(1) IN, @COM_REGNO varchar(10) IN` | 확정한 테이블 쓰기 없음. 참조: sb_scraper.dbo.ep_use_log 동적 SQL 포함, 런타임 조합 대상 미확정. | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |

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
| 대상 선정 | 사용자가 WBS 탭 내용으로 제공한 텍스트의 No. 131; [선정 태스크](../../inventory/wbs-tasks.csv) | 제공 텍스트 확인 2026-11-09. 원본 Excel의 탭/병합 셀을 독립 재열람한 것은 아님. |
| 메뉴·라우트·화면 | [menuConfig.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts); [HometaxDtiRoutes.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/HometaxDtiRoutes.tsx); [EmailParsingMonitoringPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/EmailParsingMonitoringPage.tsx) | 코드 확인 2026-11-09, 기준 dc216b313 |
| 기능·권한·API | 이 문서의 API 계약 링크 및 연결 Hook/API·Controller·DTO·Service·Repository·Mapper | 코드 확인 2026-11-09. 요청 실행·권한 계정별 재현은 미확인. |
| DB 정의 | [개발 DB 계약](../../references/database-contracts.md), 이 문서의 연결 객체 | 개발 DB 정의 확인 2026-11-09. 동적 SQL·CLR 내부·정의 미공개 참조의 미확정 범위는 객체별 기록; 후속 확인 DB 담당. |
| 브라우저 화면·배포 환경 | 실제 검증 계정의 정상·빈 결과·권한 부족·입력 오류 및 현재 배포본 | 미확인: 브라우저 실행 검증을 수행하지 않음. 배포 전 업무 담당·QA·기술 담당 확인. |
| 업무 프로시저·쓰기·외부 결과 | 격리된 검증 환경·테스트 데이터의 실행 결과 | 미확인: 공유 개발 DB의 업무 프로시저·쓰기·발송을 실행하지 않음. 격리 환경에서 기술 담당 확인. |

코드 확인과 DB 정의 확인은 실행 성공·업무 승인·다른 환경 적용을 보장하지 않는다. 업무·기술 담당 검토 후 조사 목록의 상태를 완료로 변경한다.

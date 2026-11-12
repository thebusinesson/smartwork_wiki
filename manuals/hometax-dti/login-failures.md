# [SB 서비스관리] 인증서 로그인 실패 조회 (조회·관리) 관리자 매뉴얼

작성 기준: `dc216b313` · 확인일 2026-11-09 · 조사 상태 **검토 대기**. 코드·개발 DB 정의 확인. 브라우저: **화면 대조**; 저장·발송 등 업무 실행 결과는 미검증이다.

## 1) 화면 기본 정보

### 도메인 이해

인증서를 사용한 로그인 시도 중 실패한 업체와 최초 발생 시점·사유를 찾는다.

| 구분 | 설명 |
|---|---|
| 업무 영역 | 설치형 홈택스 세금계산서 수집 > 인증서 로그인 실패 조회 조회·관리 |
| 언제 사용하는가 | 수집 실패가 인증 단계의 문제인지 확인할 때 |
| 주요 대상·데이터 | 검색일자·연동 구분·사업자정보·최초 발생시간·실패사유가 인증 실패 건의 조사 근거다. |
| 업무 흐름 | 실패 발생일·연동 구분 선택 → 업체·실패사유 확인 → 만료·등록 상태와 비교 |
| 이 페이지의 역할 | 인증서 로그인 실패 중 **인증서 로그인 실패 조회 조회·관리** 단계. 인증서를 사용한 로그인 시도 중 실패한 업체와 최초 발생 시점·사유를 찾는다. |
| 판단 결과·다음 업무 | 사유에 따라 인증서 갱신·등록 정보·연동 설정을 이어 조사한다. |
| 다른 화면과의 구분 | 만료 예정 목록과 달리 실제 로그인 실패 기록이며, 수집 실행 오류 전체를 의미하지 않는다. |

설명 근거: [CertificateLoginFailuresPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/CertificateLoginFailuresPage.tsx), 이 문서 4·5·7번의 항목·API·업무 규칙. [상위 업무 영역](../../references/domain-overview.md#hometax)은 공통 배경이며 현재 화면의 데이터·동작은 위 설명을 따른다. 설명 수정일 **2026-11-10**; 새 업무 실행 검증을 수행한 것은 아니다.

### 화면 정보

| 항목 | 작성 내용 |
|---|---|
| 업무 도메인·목적 | 인증서를 사용한 로그인 시도 중 실패한 업체와 최초 발생 시점·사유를 찾는다. |
| 메뉴·화면 경로 | SB 서비스관리 > 홈택스 DTI 수집 > 인증서 로그인 실패 조회; `/hometax-dti/login-failures`; 메뉴 또는 관련 화면에서 진입한다. |
| 화면 유형·담당 | 조회·관리; WBS 작업자 유지윤. 업무·기술 담당 팀명은 원문에 없어 배포 전 해당 도메인 담당자가 확정한다. |
| 관련 화면 | 같은 메뉴에 별도 독립 경로 없음. 팝업·탭은 이 문서 참조. |

WBS 근거: No. 130 (사용자가 제공한 텍스트 행 164). API 개발/화면 개발의 중복 행은 같은 화면으로 통합했다.

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
|---|---|---|
| 화면 진입·조회 | `/hometax-dti/login-failures` 메뉴 접근·하위 경로 작업 권한. 조회 API는 VIEW, 등록/수정 경로는 PROCESS 등 아래 서버 액션과 라우트 가드를 함께 적용한다. | 로그인된 관리자 계정; 아래 검색·입력 항목을 준비한다. |

서버가 최종 권한을 검사한다. 버튼 모양(kind)으로 권한을 추정하지 않는다. 특히 등록·수정이 PROCESS를 사용하는 API와 EXECUTE·UNMASK·EXCEL_DOWNLOAD는 서로 구분한다.

## 3) 화면 사용 절차

**검증 시 화면 버튼**: 검색, 초기화. 화면 상태·대상에 따라 달라지며 아래 작업 절차와 권한 조건을 함께 확인한다.

1. `SB 서비스관리 > 홈택스 DTI 수집 > 인증서 로그인 실패 조회` 메뉴를 연다. 경로 변수는 주소에서 임의로 바꾸지 않고 이전 화면이 전달한 식별자를 사용한다.
2. 현재 검색 조건과 아래 기본값을 확인한다. **검색일자, 연동 구분** 항목에 필요한 값을 입력하고 **검색**을 누른다.
3. 결과 표·탭·팝업에서 대상의 상태와 합계·이력을 확인한다. 다른 조회 조건으로 바꾼 경우 다시 검색하여 결과를 갱신한다.

**이 화면에서 유의할 업무 규칙**: 검색일자는 기본 오늘이고 연동 구분은 전체다. 실패 현황은 인증서 재등록이나 잠금 해제를 직접 보장하지 않으므로 오류 내용과 실제 수집 시스템의 상태를 함께 확인한다.

## 4) 입력·표시 데이터

**검증 시 표시된 날짜 필터**: 검색일자 `2026-11-09`. 검증 날짜·조건 복원에 따른 표시값이며 모든 실행의 고정 기본값을 뜻하지 않는다.

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
|---|---|---|---|
| 검색일자 | 입력·필수 | 화면 타입 dateInput; API 타입 String; 기본 ""; 서버 검증 @field:NotBlank(message = "startDay 는 필수입니다."); @field:Size(max = 10); 초기값 오늘 | `startDay`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/CertificateLoginFailuresPage.tsx#L69) |
| 연동 구분 | 입력·선택(조건부 검증 별도) | 화면 타입 select; API 타입 String?; 기본 null; 서버 검증 @field:Pattern; 선택: 전체=all, SAP=SAP, NonSAP=NonSAP; 초기값 all | `division`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/CertificateLoginFailuresPage.tsx#L70) |
| 연동 | 출력 | API 타입 String?; 기본 null; 서버 검증 @field:Pattern; 초기값 all | `division`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/CertificateLoginFailuresPage.tsx#L132) |
| 허브업체명 | 출력 | API 타입 String? | `hubRealname`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/CertificateLoginFailuresPage.tsx#L139) |
| 사업자번호 | 출력 | API 타입 String? | `comRegno`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/CertificateLoginFailuresPage.tsx#L146) |
| 사업자명 | 출력 | API 타입 String? | `comName`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/CertificateLoginFailuresPage.tsx#L153) |
| 최초 발생시간 | 출력 | API 타입 String? | `logDate`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/CertificateLoginFailuresPage.tsx#L160) |
| 실패사유 | 출력 | API 타입 String? | `failReason`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/CertificateLoginFailuresPage.tsx#L167) |

**복합 검색·폼의 초기 상태**

| 초기값 근거 | 기본 상태 |
|---|---|
| [createDefaultFilters](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/CertificateLoginFailuresPage.tsx#L44) | startDay=오늘; division=all |

화면 필드 키와 API 필드명이 다른 경우 변환은 Hook/API의 검색·저장 매핑에서 수행된다. 요청·응답 필드와 DB 컬럼 매핑은 아래 API 계약 및 DB 객체 계약에 연결했다.

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
|---|---|---|---|
| 인증서 로그인 실패 목록 조회 (in-memory 페이징) | [GET /api/v1/sb-service/hometax-dti-installed/certificate-login-fail](../../references/api-contracts.md#api084); `/hometax-dti/login-failures` / `VIEW` | `startDay, division, page, size` → `content, totalElements, totalPages, page, size, division, hubRealname, comRegno, comName, logDate, failReason` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
|---|---|---|---|
| [SB_SCRAPER.dbo.SSP_CERT_LOGIN_FAIL_LIST](../../references/database-contracts.md#db169) | `@START_DAY varchar(10) IN, @DIVISION varchar(10) IN` | 확정한 테이블 쓰기 없음. 참조: sb_scraper.dbo.use_company_detail, sb_scraper.dbo.use_company_detail_his, sb_scraper.dbo.use_company_info, sb_scraper.dbo.use_log | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |

위 DB 계약 링크에는 실제 파라미터 타입·기본값·IN/OUT, Mapper 결과 컬럼, RETURN 바인딩, 참조 테이블·하위 프로시저·정의 필터/정렬을 기록했다. DTO·Service·Repository·Mapper의 상세 호출 경로는 각 API 계약에서 확인한다.

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
|---|---|---|
| 결과가 없거나 기대 건수와 다름 | 적용된 검색 기준·기간·탭·대상 상태·서버 필터·페이징·목록/다운로드 조건 | 조건을 다시 확인하고 조회한다. 지속되면 경로·작업 시각·마스킹한 식별자·필터를 업무/기술 담당에게 전달한다. |
| 메뉴·버튼 미표시 또는 접근 거부 | 사용자 그룹의 메뉴 접근·VIEW 및 API별 PROCESS/EXECUTE/DELETE/EXCEL_DOWNLOAD/UNMASK 등 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. 프런트 버튼 표시만으로 서버 권한을 판단하지 않는다. |
| 저장·삭제·외부 실행의 결과가 불명확 | 대상 현재 상태·중복 요청·감사 이력·API 오류·파일/외부 소비 로그 | 기존 반영 여부를 먼저 조회한다. 중복 발송·초기화·금액 처리를 피하기 위해 기술 담당 확인 후 재시도한다. |

## 7) 검증·출처

**브라우저 검증(2026-11-09)**: 화면 대조. [경로별 결과와 제한](../../references/browser-verification.md#page039). 역할별 권한 거부·저장 성공·파일 반출·외부 연계 완료는 이 결과로 보장하지 않는다.

| 검증 항목 | 근거·환경 | 상태·확인일 |
|---|---|---|
| 대상 선정 | 사용자가 WBS 탭 내용으로 제공한 텍스트의 No. 130; [선정 태스크](../../inventory/wbs-tasks.csv) | 제공 텍스트 확인 2026-11-09. 원본 Excel의 탭/병합 셀을 독립 재열람한 것은 아님. |
| 메뉴·라우트·화면 | [menuConfig.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts); [HometaxDtiRoutes.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/HometaxDtiRoutes.tsx); [CertificateLoginFailuresPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/CertificateLoginFailuresPage.tsx) | 코드 확인 2026-11-09, 기준 dc216b313 |
| 기능·권한·API | 이 문서의 API 계약 링크 및 연결 Hook/API·Controller·DTO·Service·Repository·Mapper | 코드 확인 2026-11-09. 조회 요청·화면 대조 범위는 아래 브라우저 근거 참조. 권한 계정별 허용·거부 및 변경 요청 실행은 미확인. |
| DB 정의 | [개발 DB 계약](../../references/database-contracts.md), 이 문서의 연결 객체 | 개발 DB 정의 확인 2026-11-09. 동적 SQL·CLR 내부·정의 미공개 참조의 미확정 범위는 객체별 기록; 후속 확인 DB 담당. |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-5b9557151aece640) | Demo 메타데이터 1/1개 확인 · 2026-11-11 |
| 브라우저 화면·배포 환경 | 로컬 인증 계정·Playwright CLI; [화면별 검증표](../../references/browser-verification.md#page039) | 화면 대조, 2026-11-09. 배포본·타 역할·업무 변경 결과는 미확인. |
| 업무 프로시저·쓰기·외부 결과 | 격리된 검증 환경·테스트 데이터의 실행 결과 | 미확인: 명시적인 저장·삭제·발송·초기화 요청은 실행하지 않음. 브라우저 GET의 업무 조회 프로시저·조회수·감사 기록은 별도 영향으로 구분. 격리 환경에서 기술 담당 확인. |

코드 확인과 DB 정의 확인은 실행 성공·업무 승인·다른 환경 적용을 보장하지 않는다. 업무·기술 담당 검토 후 조사 목록의 상태를 완료로 변경한다.

브라우저 직접 근거: [settled-static-recheck](../../evidence/browser/static-stable.json). 경로·고정 버튼명·입력 속성·표 머리글·API 상태를 보관했고 실제 데이터 값·식별자·인증정보는 제외했다.

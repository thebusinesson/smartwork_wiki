# [고객지원] 공지사항 (등록) 관리자 매뉴얼

작성 기준: `dc216b313` · 확인일 2026-11-09 · 조사 상태 **검토 대기**. 코드·개발 DB 정의 확인. 브라우저: **화면 대조**; 저장·발송 등 업무 실행 결과는 미검증이다.

## 1) 화면 기본 정보

### 도메인 이해

고객 공지에 아직 없는 안내·문의·자료를 새 게시물로 작성한다. 웹·모바일·모바일 팝업의 노출 여부·기간도 정한다.

| 구분 | 설명 |
|---|---|
| 업무 영역 | 고객 게시판·문의 응대 > 공지사항 등록 |
| 언제 사용하는가 | 서비스 안내를 게시하거나 어떤 채널에 공지가 노출되는지 점검할 때에 해당하고 기존 게시물로 처리할 수 없어 신규 작성이 필요할 때 |
| 주요 대상·데이터 | 제목·내용은 안내문, 웹 공지·모바일 공지·모바일 팝업·팝업 기간은 노출 설정이다. 이번 입력은 새 게시물의 제목·본문과 해당 화면의 분류·파일/노출 항목이다. |
| 업무 흐름 | 고객 공지 목록의 작성 선택 → 새 제목·본문과 부가 항목 입력 → 필수값 확인 → 저장 후 새 게시물 조회 |
| 이 페이지의 역할 | 고객 공지 중 **공지사항 등록** 단계. 고객 공지에 아직 없는 안내·문의·자료를 새 게시물로 작성한다. 웹·모바일·모바일 팝업의 노출 여부·기간도 정한다. |
| 판단 결과·다음 업무 | 새 게시물이 고객 공지의 올바른 분류·내용·첨부/노출 설정으로 등록되었는지 확인한다. |
| 다른 화면과의 구분 | 기존 고객 공지 게시물의 수정과 달리 새 번호를 만드는 단계다. 실제 저장 성공·노출 결과는 별도 검증 범위를 따른다. |

설명 근거: [AdminNoticeFormPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/board/notice/AdminNoticeFormPage.tsx), 이 문서 4·5·7번의 항목·API·업무 규칙. [상위 업무 영역](../../references/domain-overview.md#board)은 공통 배경이며 현재 화면의 데이터·동작은 위 설명을 따른다. 설명 수정일 **2026-11-10**; 새 업무 실행 검증을 수행한 것은 아니다.

### 화면 정보

| 항목 | 작성 내용 |
|---|---|
| 업무 도메인·목적 | 고객 공지에 아직 없는 안내·문의·자료를 새 게시물로 작성한다. 웹·모바일·모바일 팝업의 노출 여부·기간도 정한다. |
| 메뉴·화면 경로 | 고객지원 > 고객 게시판 관리 > 공지사항; `/customer-support/notice/new`; 메뉴 또는 관련 화면에서 진입한다. |
| 화면 유형·담당 | 등록; WBS 작업자 유지윤. 업무·기술 담당 팀명은 원문에 없어 배포 전 해당 도메인 담당자가 확정한다. |
| 관련 화면 | [조회·관리](notice.md); [상세](notice__by-id.md); [수정](notice__by-id__edit.md) |

WBS 근거: No. 334, 335 (사용자가 제공한 텍스트 행 457, 458). API 개발/화면 개발의 중복 행은 같은 화면으로 통합했다.

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
|---|---|---|
| 화면 진입·조회 | `/customer-support/notice` 메뉴 접근·하위 경로 작업 권한. 조회 API는 VIEW, 등록/수정 경로는 PROCESS 등 아래 서버 액션과 라우트 가드를 함께 적용한다. | 로그인된 관리자 계정; 아래 검색·입력 항목을 준비한다. |
| 저장 | `/customer-support/notice`; 화면 게이트 PROCESS. 실제 서버 액션은 API별 표 참조. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 취소 | `/customer-support/notice`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |

서버가 최종 권한을 검사한다. 버튼 모양(kind)으로 권한을 추정하지 않는다. 특히 등록·수정이 PROCESS를 사용하는 API와 EXECUTE·UNMASK·EXCEL_DOWNLOAD는 서로 구분한다.

## 3) 화면 사용 절차

**검증 시 화면 버튼**: HTML로 작성, 저장, 목록. 화면 상태·대상에 따라 달라지며 아래 작업 절차와 권한 조건을 함께 확인한다.

1. 관련 화면에서 대상 또는 작업을 선택하여 `/customer-support/notice/new`로 이동한다. 경로 변수는 주소에서 임의로 바꾸지 않고 이전 화면이 전달한 식별자를 사용한다.
2. **내용, 제목, 웹 공지, 모바일 공지, 모바일 팝업**의 입력값을 확인한다. 신규 값을 입력한다. 필수값과 형식 오류가 표시되면 해당 항목을 수정한다.
3. **저장**을 누르고 확인창이 있으면 대상·작업을 확인한다. 첨부가 있으면 기존 파일의 유지·삭제·교체 선택을 함께 확인한다.
4. 처리 결과 메시지를 확인한 뒤 목록 또는 상세에서 결과를 다시 조회한다. 오류가 나면 아래 예외 대응과 API 오류를 확인하고 중복 저장 전에 기존 처리 여부를 확인한다.

**이 화면에서 유의할 업무 규칙**: 제목 또는 내용으로 검색하고 작성 버튼으로 새 공지를 등록한다. 상세의 조회수 증가와 수정 입력을 위한 incrementHit=false 조회를 구분한다.

공통 폼이 등록·수정·상세 입력값 조회 함수를 함께 포함할 수 있다. 아래 API 표에 공통 구현의 다른 모드가 표시되어도 현재 경로의 작업으로 모두 실행하는 것은 아니다.

**본문 표시·편집 모드**: 현재 내용과 모드에 따라 **HTML로 전환**, **HTML로 작성**, **WYSIWYG 보기** 등의 버튼이 표시된다. 상세의 표시 모드 전환과 등록·수정 폼의 편집 모드 전환을 구분한다. 기존 HTML을 수정하는 경우 현재 편집 모드와 저장할 본문을 확인한다.

## 4) 입력·표시 데이터

**검증 시 표시된 날짜 필터**: 시작일 `2026-11-09`, 종료일 `2026-12-14`. 검증 날짜·조건 복원에 따른 표시값이며 모든 실행의 고정 기본값을 뜻하지 않는다.

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
|---|---|---|---|
| 내용 | 입력·선택(조건부 검증 별도) | 길이·형식·조건부 필수는 검증 코드와 API DTO 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/board/notice/AdminNoticeFormPage.tsx#L281) |
| 제목 | 입력·필수 | 최대 100자; API 타입 String; 서버 검증 @field:NotBlank(message = "제목은 필수입니다."); @field:Size(max = 100, message = "제목은 100자 이하여야 합니다."); 초기값 빈값 | `title`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/board/notice/components/form/AdminNoticeFormFields.tsx#L44) |
| 웹 공지 | 입력·선택(조건부 검증 별도) | API 타입 String; 서버 검증 @field:Pattern(regexp = "^[YN]$", message = "webNoticeYn 은 Y / N 이어야 합니다."); 초기값 Y | `webNoticeYn`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/board/notice/components/form/AdminNoticeFormFields.tsx#L61) |
| 모바일 공지 | 입력·선택(조건부 검증 별도) | API 타입 String; 서버 검증 @field:Pattern(regexp = "^[YN]$", message = "mobileNoticeYn 은 Y / N 이어야 합니다."); 초기값 N | `mobileNoticeYn`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/board/notice/components/form/AdminNoticeFormFields.tsx#L81) |
| 모바일 팝업 | 입력·선택(조건부 검증 별도) | API 타입 String; 서버 검증 @field:Pattern(regexp = "^[YN]$", message = "mobilePopYn 은 Y / N 이어야 합니다."); 초기값 N | `mobilePopYn`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/board/notice/components/form/AdminNoticeFormFields.tsx#L101) |
| 팝업 기간 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/board/notice/components/form/AdminNoticePopupRange.tsx#L32) |

입력 검증 근거: [AdminNoticeFormPage.schema.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/support/board/notice/AdminNoticeFormPage.schema.ts), [sharedTitleContent.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/support/board/sharedTitleContent.ts). 프런트 검증과 서버 DTO 제약이 다르면 서버 검증이 최종 기준이다.

**복합 검색·폼의 초기 상태**

| 초기값 근거 | 기본 상태 |
|---|---|
| [buildInitialForm](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/board/notice/AdminNoticeFormPage.tsx#L37) | noticeType=N; title=빈값; content=빈값; webNoticeYn=Y; mobileNoticeYn=N; mobilePopYn=N; mobilePopBeginDate={todayIso()}; mobilePopEndDate={fiveWeeksLaterIso()}; isHtmlMode=꺼짐 |

화면 필드 키와 API 필드명이 다른 경우 변환은 Hook/API의 검색·저장 매핑에서 수행된다. 요청·응답 필드와 DB 컬럼 매핑은 아래 API 계약 및 DB 객체 계약에 연결했다.

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
|---|---|---|---|
| 공지사항 신규 등록 | [POST /api/v1/support/notices](../../references/api-contracts.md#api240); `/customer-support/notice` / `PROCESS` | `noticeType, title, content, mobileNoticeYn, webNoticeYn, mobilePopYn, mobilePopBeginDate, mobilePopEndDate` → `응답 DTO·파일/처리 결과 계약 참조` | 쓰기 대상 smartbill3.dbo.notice |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
|---|---|---|---|
| [SMARTBILL3.dbo.upAdmSB_SavNotice](../../references/database-contracts.md#db240) | `@gubun varchar(3) IN, @div varchar(1) IN, @num no IN, @Notice_title title IN, @Notice_contents contents IN, @MobileNoticeYN varchar(1) IN, @WebNoticeYN varchar(1) IN, @MobilePopYN varchar(1) IN, @MobilePopBeginDate datetime IN, @MobilePopEndDate datetime IN` | 쓰기: smartbill3.dbo.notice. 참조: smartbill3.dbo.notice | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |

위 DB 계약 링크에는 실제 파라미터 타입·기본값·IN/OUT, Mapper 결과 컬럼, RETURN 바인딩, 참조 테이블·하위 프로시저·정의 필터/정렬을 기록했다. DTO·Service·Repository·Mapper의 상세 호출 경로는 각 API 계약에서 확인한다.

## 6) 예외 상황과 운영 확인

**빈값 입력 재현**: 제목을 입력해 주세요.; 내용을 입력해 주세요.. 빈 입력에서 확인한 클라이언트 오류이며 저장 요청 성공·서버 검증 재현은 아니다.

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
|---|---|---|
| 결과가 없거나 기대 건수와 다름 | 적용된 검색 기준·기간·탭·대상 상태·서버 필터·페이징·목록/다운로드 조건 | 조건을 다시 확인하고 조회한다. 지속되면 경로·작업 시각·마스킹한 식별자·필터를 업무/기술 담당에게 전달한다. |
| 메뉴·버튼 미표시 또는 접근 거부 | 사용자 그룹의 메뉴 접근·VIEW 및 API별 PROCESS/EXECUTE/DELETE/EXCEL_DOWNLOAD/UNMASK 등 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. 프런트 버튼 표시만으로 서버 권한을 판단하지 않는다. |
| 저장·삭제·외부 실행의 결과가 불명확 | 대상 현재 상태·중복 요청·감사 이력·API 오류·파일/외부 소비 로그 | 기존 반영 여부를 먼저 조회한다. 중복 발송·초기화·금액 처리를 피하기 위해 기술 담당 확인 후 재시도한다. |

## 7) 검증·출처

**브라우저 검증(2026-11-09)**: 화면 대조. [경로별 결과와 제한](../../references/browser-verification.md#page090). 역할별 권한 거부·저장 성공·파일 반출·외부 연계 완료는 이 결과로 보장하지 않는다.

| 검증 항목 | 근거·환경 | 상태·확인일 |
|---|---|---|
| 대상 선정 | 사용자가 WBS 탭 내용으로 제공한 텍스트의 No. 334, 335; [선정 태스크](../../inventory/wbs-tasks.csv) | 제공 텍스트 확인 2026-11-09. 원본 Excel의 탭/병합 셀을 독립 재열람한 것은 아님. |
| 메뉴·라우트·화면 | [menuConfig.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts); [CustomerSupportRoutes.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/CustomerSupportRoutes.tsx); [AdminNoticeFormPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/board/notice/AdminNoticeFormPage.tsx) | 코드 확인 2026-11-09, 기준 dc216b313 |
| 기능·권한·API | 이 문서의 API 계약 링크 및 연결 Hook/API·Controller·DTO·Service·Repository·Mapper | 코드 확인 2026-11-09. 조회 요청·화면 대조 범위는 아래 브라우저 근거 참조. 권한 계정별 허용·거부 및 변경 요청 실행은 미확인. |
| DB 정의 | [개발 DB 계약](../../references/database-contracts.md), 이 문서의 연결 객체 | 개발 DB 정의 확인 2026-11-09. 동적 SQL·CLR 내부·정의 미공개 참조의 미확정 범위는 객체별 기록; 후속 확인 DB 담당. |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-35998633a2c74dec) | Demo 메타데이터 1/1개 확인 · 2026-11-11 |
| 브라우저 화면·배포 환경 | 로컬 인증 계정·Playwright CLI; [화면별 검증표](../../references/browser-verification.md#page090) | 화면 대조, 2026-11-09. 배포본·타 역할·업무 변경 결과는 미확인. |
| 업무 프로시저·쓰기·외부 결과 | 격리된 검증 환경·테스트 데이터의 실행 결과 | 미확인: 명시적인 저장·삭제·발송·초기화 요청은 실행하지 않음. 브라우저 GET의 업무 조회 프로시저·조회수·감사 기록은 별도 영향으로 구분. 격리 환경에서 기술 담당 확인. |

코드 확인과 DB 정의 확인은 실행 성공·업무 승인·다른 환경 적용을 보장하지 않는다. 업무·기술 담당 검토 후 조사 목록의 상태를 완료로 변경한다.

브라우저 직접 근거: [settled-static-recheck](../../evidence/browser/static-stable.json). 경로·고정 버튼명·입력 속성·표 머리글·API 상태를 보관했고 실제 데이터 값·식별자·인증정보는 제외했다.

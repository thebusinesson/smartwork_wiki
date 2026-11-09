# [고객지원] 1:1 문의 (수정) 관리자 매뉴얼

작성 기준: `dc216b313` · 확인일 2026-11-09 · 조사 상태 **검토 대기**. 코드·개발 DB 정의 확인. 브라우저: **진입 미재현**; 저장·발송 등 업무 실행 결과는 미검증이다.

## 1) 화면 기본 정보

| 항목 | 작성 내용 |
|---|---|
| 업무 도메인·목적 | 고객의 1:1 문의를 구분·분류별로 조회하고 문의와 답글을 관리한다. |
| 메뉴·화면 경로 | 고객지원 > 고객 게시판 관리 > 1:1 문의; `/customer-support/qna/:id/edit`; 목록에서 선택한 대상의 경로 변수를 유지하여 진입한다. |
| 화면 유형·담당 | 수정; WBS 작업자 유지윤. 업무·기술 담당 팀명은 원문에 없어 배포 전 해당 도메인 담당자가 확정한다. |
| 관련 화면 | [조회·관리](qna.md); [등록](qna__new.md); [상세](qna__by-id.md); [답글 등록](qna__by-id__reply.md) |

WBS 근거: No. 338, 339 (사용자가 제공한 텍스트 행 463, 464). API 개발/화면 개발의 중복 행은 같은 화면으로 통합했다.

## 2) 사용 권한과 사전 준비

**Q&A 수정 조건**: 서버 도메인의 `canEdit`는 `memberNo == 0 && step > 0`일 때 참이다. 메뉴의 작업 권한 외에 이 데이터 조건을 만족해야 한다. 선택한 검증 게시물에서는 수정 버튼이 비활성화되었고 수정 URL 진입도 상세로 돌아왔다. 임의의 게시물을 수정 가능한 것으로 안내하지 않는다. 서버 Service도 같은 조건을 검사한다.

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
|---|---|---|
| 화면 진입·조회 | `/customer-support/qna` 메뉴 접근·하위 경로 작업 권한. 조회 API는 VIEW, 등록/수정 경로는 PROCESS 등 아래 서버 액션과 라우트 가드를 함께 적용한다. | 로그인된 관리자 계정; id 식별자는 이전 화면에서 선택한다. |
| 저장 | `/customer-support/qna`; 화면 게이트 PROCESS. 실제 서버 액션은 API별 표 참조. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 목록 | `/customer-support/qna`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |

서버가 최종 권한을 검사한다. 버튼 모양(kind)으로 권한을 추정하지 않는다. 특히 등록·수정이 PROCESS를 사용하는 API와 EXECUTE·UNMASK·EXCEL_DOWNLOAD는 서로 구분한다.

## 3) 화면 사용 절차

1. 관련 화면에서 대상 또는 작업을 선택하여 `/customer-support/qna/:id/edit`로 이동한다. 경로 변수는 주소에서 임의로 바꾸지 않고 이전 화면이 전달한 식별자를 사용한다.
2. **내용, 제목**의 입력값을 확인한다. 기존 정보와 원문을 확인한 뒤 변경한다. 필수값과 형식 오류가 표시되면 해당 항목을 수정한다.
3. **저장**을 누르고 확인창이 있으면 대상·작업을 확인한다. 첨부가 있으면 기존 파일의 유지·삭제·교체 선택을 함께 확인한다.
4. 처리 결과 메시지를 확인한 뒤 목록 또는 상세에서 결과를 다시 조회한다. 오류가 나면 아래 예외 대응과 API 오류를 확인하고 중복 저장 전에 기존 처리 여부를 확인한다.

**이 화면에서 유의할 업무 규칙**: 목록에서 구분·분류·검색 조건을 지정한다. 답글은 원문의 별도 답글 경로에서 작성하며 원문의 분류·인용 내용을 확인한다. 기본 답글 문구를 실제 문의에 맞게 수정한 뒤 저장한다.

공통 폼이 등록·수정·상세 입력값 조회 함수를 함께 포함할 수 있다. 아래 API 표에 공통 구현의 다른 모드가 표시되어도 현재 경로의 작업으로 모두 실행하는 것은 아니다.

**본문 표시·편집 모드**: 현재 내용과 모드에 따라 **HTML로 전환**, **HTML로 작성**, **WYSIWYG 보기** 등의 버튼이 표시된다. 상세의 표시 모드 전환과 등록·수정 폼의 편집 모드 전환을 구분한다. 기존 HTML을 수정하는 경우 현재 편집 모드와 저장할 본문을 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
|---|---|---|---|
| 내용 | 입력·필수 | API 타입 String; 서버 검증 @field:NotBlank(message = "내용은 필수입니다."); 초기값 빈값 | `content`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/board/qna/AdminQnaFormPage.tsx#L283) |
| 분류 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/board/qna/components/form/AdminQnaFormFields.tsx#L41) |
| 제목 | 입력·필수 | 최대 100자; API 타입 String; 서버 검증 @field:NotBlank(message = "제목은 필수입니다."); @field:Size(max = 100, message = "제목은 100자 이하여야 합니다."); 초기값 빈값 | `title`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/board/qna/components/form/AdminQnaFormFields.tsx#L63) |

입력 검증 근거: [sharedTitleContent.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/support/board/sharedTitleContent.ts). 프런트 검증과 서버 DTO 제약이 다르면 서버 검증이 최종 기준이다.

**복합 검색·폼의 초기 상태**

| 초기값 근거 | 기본 상태 |
|---|---|
| [buildInitialForm](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/board/qna/AdminQnaFormPage.tsx#L63) | qnaType=m; title=빈값; content=빈값; isHtmlMode=꺼짐 |

화면 필드 키와 API 필드명이 다른 경우 변환은 Hook/API의 검색·저장 매핑에서 수행된다. 요청·응답 필드와 DB 컬럼 매핑은 아래 API 계약 및 DB 객체 계약에 연결했다.

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
|---|---|---|---|
| 1:1 문의 신규 등록 | [POST /api/v1/support/qnas](../../references/api-contracts.md#api243); `/customer-support/qna` / `PROCESS` | `qnaType, title, content` → `응답 DTO·파일/처리 결과 계약 참조` | 공통 폼의 신규 등록 경로; 수정 저장에서는 사용하지 않음. 쓰기 대상 office.dbo.msg_queue, smartbill3.dbo.arreo_sms_sb, smartbill3.dbo.qna |
| 1:1 문의 수정 | [PUT /api/v1/support/qnas/{id}](../../references/api-contracts.md#api272); `/customer-support/qna` / `PROCESS` | `qnaType, title, content` → `응답 DTO·파일/처리 결과 계약 참조` | 쓰기 대상 office.dbo.msg_queue, smartbill3.dbo.arreo_sms_sb, smartbill3.dbo.qna; 동적 SQL의 런타임 대상은 미확정 |
| 1:1 문의 답글 등록 | [POST /api/v1/support/qnas/{id}/replies](../../references/api-contracts.md#api244); `/customer-support/qna` / `PROCESS` | `title, content` → `응답 DTO·파일/처리 결과 계약 참조` | 쓰기 대상 office.dbo.msg_queue, smartbill3.dbo.arreo_sms_sb, smartbill3.dbo.qna; 동적 SQL의 런타임 대상은 미확정 |
| 1:1 문의 단건 상세 | [GET /api/v1/support/qnas/{id}](../../references/api-contracts.md#api150); `/customer-support/qna` / `VIEW` | `경로·쿼리·본문 계약 참조` → `canEdit, id, qnaType, title, content, createdDate, viewCount, writer, parentId, step, replyCount, memberCompany, businessRegNo, companyName, memberName, memberId` | 쓰기 대상 smartbill3.dbo.qna; 동적 SQL의 런타임 대상은 미확정 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
|---|---|---|---|
| [SB_COMMON.dbo.upSBAdm_Sav_Qna](../../references/database-contracts.md#db113) | `@DIV varchar(3) IN, @QNA_TYPE varchar(3) IN, @NUM int IN, @QNA_WRITER varchar(30) IN, @QNA_TITLE varchar(100) IN, @QNA_CONTENTS text IN, @MEM_NO int IN` | 쓰기: office.dbo.msg_queue, smartbill3.dbo.arreo_sms_sb, smartbill3.dbo.qna. 참조: office.dbo.msg_queue, smartbill3.dbo.arreo_sms_sb, smartbill3.dbo.member, smartbill3.dbo.qna | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SMARTBILL3.dbo.upAdmSB_Lst_EachQna](../../references/database-contracts.md#db225) | `@div varchar(12) IN, @cnt varchar(12) IN, @num varchar(12) IN` | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.qna 동적 SQL 포함, 런타임 조합 대상 미확정. | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SMARTBILL3.dbo.upAdmSB_Cnt_QnaVisit](../../references/database-contracts.md#db214) | `@qnaNo no IN` | 쓰기: smartbill3.dbo.qna. 참조: smartbill3.dbo.qna | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SMARTBILL3.dbo.upAdmSB_LstMem](../../references/database-contracts.md#db229) | `@no varchar(10) IN, @GUBUN varchar(10) IN` | 확정한 테이블 쓰기 없음. 참조: sb_dti_log.dbo.dormant_member, sb_dti_log.dbo.member_login_his, sb_mobile.dbo.member, smartbill3.dbo.company, smartbill3.dbo.member, smartbill3.dbo.member_agreement | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |

위 DB 계약 링크에는 실제 파라미터 타입·기본값·IN/OUT, Mapper 결과 컬럼, RETURN 바인딩, 참조 테이블·하위 프로시저·정의 필터/정렬을 기록했다. DTO·Service·Repository·Mapper의 상세 호출 경로는 각 API 계약에서 확인한다.

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
|---|---|---|
| 결과가 없거나 기대 건수와 다름 | 적용된 검색 기준·기간·탭·대상 상태·서버 필터·페이징·목록/다운로드 조건 | 조건을 다시 확인하고 조회한다. 지속되면 경로·작업 시각·마스킹한 식별자·필터를 업무/기술 담당에게 전달한다. |
| 메뉴·버튼 미표시 또는 접근 거부 | 사용자 그룹의 메뉴 접근·VIEW 및 API별 PROCESS/EXECUTE/DELETE/EXCEL_DOWNLOAD/UNMASK 등 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. 프런트 버튼 표시만으로 서버 권한을 판단하지 않는다. |
| 저장·삭제·외부 실행의 결과가 불명확 | 대상 현재 상태·중복 요청·감사 이력·API 오류·파일/외부 소비 로그 | 기존 반영 여부를 먼저 조회한다. 중복 발송·초기화·금액 처리를 피하기 위해 기술 담당 확인 후 재시도한다. |

## 7) 검증·출처

**브라우저 검증(2026-11-09)**: 진입 미재현. 선택 게시물의 canEdit=false. 수정 버튼 비활성화와 URL 진입 시 상세 복귀를 확인했으나 편집 화면은 미재현. [경로별 결과와 제한](../../references/browser-verification.md#page097). 역할별 권한 거부·저장 성공·파일 반출·외부 연계 완료는 이 결과로 보장하지 않는다.

| 검증 항목 | 근거·환경 | 상태·확인일 |
|---|---|---|
| 대상 선정 | 사용자가 WBS 탭 내용으로 제공한 텍스트의 No. 338, 339; [선정 태스크](../../inventory/wbs-tasks.csv) | 제공 텍스트 확인 2026-11-09. 원본 Excel의 탭/병합 셀을 독립 재열람한 것은 아님. |
| 메뉴·라우트·화면 | [menuConfig.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts); [CustomerSupportRoutes.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/CustomerSupportRoutes.tsx); [AdminQnaEditPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/board/qna/AdminQnaEditPage.tsx) | 코드 확인 2026-11-09, 기준 dc216b313 |
| 기능·권한·API | 이 문서의 API 계약 링크 및 연결 Hook/API·Controller·DTO·Service·Repository·Mapper | 코드 확인 2026-11-09. 조회 요청·화면 대조 범위는 아래 브라우저 근거 참조. 권한 계정별 허용·거부 및 변경 요청 실행은 미확인. |
| DB 정의 | [개발 DB 계약](../../references/database-contracts.md), 이 문서의 연결 객체 | 개발 DB 정의 확인 2026-11-09. 동적 SQL·CLR 내부·정의 미공개 참조의 미확정 범위는 객체별 기록; 후속 확인 DB 담당. |
| 브라우저 화면·배포 환경 | 로컬 인증 계정·Playwright CLI; [화면별 검증표](../../references/browser-verification.md#page097) | 진입 미재현, 2026-11-09. 배포본·타 역할·업무 변경 결과는 미확인. |
| 업무 프로시저·쓰기·외부 결과 | 격리된 검증 환경·테스트 데이터의 실행 결과 | 미확인: 명시적인 저장·삭제·발송·초기화 요청은 실행하지 않음. 브라우저 GET의 업무 조회 프로시저·조회수·감사 기록은 별도 영향으로 구분. 격리 환경에서 기술 담당 확인. |

코드 확인과 DB 정의 확인은 실행 성공·업무 승인·다른 환경 적용을 보장하지 않는다. 업무·기술 담당 검토 후 조사 목록의 상태를 완료로 변경한다.

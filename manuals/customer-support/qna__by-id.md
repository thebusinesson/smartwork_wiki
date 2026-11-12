# [고객지원] 1:1 문의 (상세) 관리자 매뉴얼

작성 기준: `dc216b313` · 확인일 2026-11-09 · 조사 상태 **검토 대기**. 코드·개발 DB 정의 확인. 브라우저: **화면 대조**; 저장·발송 등 업무 실행 결과는 미검증이다.

## 1) 화면 기본 정보

### 도메인 이해

선택한 고객별 1:1 문의 게시물 한 건의 내용을 읽고 후속 지원 여부를 판단한다. 고객 원문·작성 맥락·기존 답글을 읽고 답글 또는 허용된 편집 필요성을 판단한다.

| 구분 | 설명 |
|---|---|
| 업무 영역 | 고객 게시판·문의 응대 > 1:1 문의 상세 |
| 언제 사용하는가 | 고객별 1:1 문의 목록에서 검색한 대상의 실제 설명·문의 내용 또는 파일을 확인할 때 |
| 주요 대상·데이터 | 구분·분류·제목·작성자·작성일은 문의의 성격과 접수 대상을 구분한다. 목록의 검색 조건 대신 선택한 게시글 ID의 내용을 다룬다. |
| 업무 흐름 | 고객별 1:1 문의 게시물 식별 확인 → 본문·부가 정보 확인 → 필요한 수정·답글 또는 목록 복귀 |
| 이 페이지의 역할 | 고객별 1:1 문의 중 **1:1 문의 상세** 단계. 선택한 고객별 1:1 문의 게시물 한 건의 내용을 읽고 후속 지원 여부를 판단한다. 고객 원문·작성 맥락·기존 답글을 읽고 답글 또는 허용된 편집 필요성을 판단한다. |
| 판단 결과·다음 업무 | 고객별 1:1 문의 내용으로 문의에 답할 수 있는지 판단하고 보완이 필요하면 해당 게시물의 수정·답글 경로로 이동한다. |
| 다른 화면과의 구분 | 다른 고객별 1:1 문의 글을 찾는 목록이나 내용을 저장하는 편집 단계와 다르다. 상세 열람에 따른 조회수 변화와 게시글 내용 변경도 구분한다. |

설명 근거: [AdminQnaDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/board/qna/AdminQnaDetailPage.tsx), 이 문서 4·5·7번의 항목·API·업무 규칙. [상위 업무 영역](../../references/domain-overview.md#board)은 공통 배경이며 현재 화면의 데이터·동작은 위 설명을 따른다. 설명 수정일 **2026-11-10**; 새 업무 실행 검증을 수행한 것은 아니다.

### 화면 정보

| 항목 | 작성 내용 |
|---|---|
| 업무 도메인·목적 | 선택한 고객별 1:1 문의 게시물 한 건의 내용을 읽고 후속 지원 여부를 판단한다. 고객 원문·작성 맥락·기존 답글을 읽고 답글 또는 허용된 편집 필요성을 판단한다. |
| 메뉴·화면 경로 | 고객지원 > 고객 게시판 관리 > 1:1 문의; `/customer-support/qna/:id`; 목록에서 선택한 대상의 경로 변수를 유지하여 진입한다. |
| 화면 유형·담당 | 상세; WBS 작업자 유지윤. 업무·기술 담당 팀명은 원문에 없어 배포 전 해당 도메인 담당자가 확정한다. |
| 관련 화면 | [조회·관리](qna.md); [등록](qna__new.md); [수정](qna__by-id__edit.md); [답글 등록](qna__by-id__reply.md) |

WBS 근거: No. 338, 339 (사용자가 제공한 텍스트 행 463, 464). API 개발/화면 개발의 중복 행은 같은 화면으로 통합했다.

## 2) 사용 권한과 사전 준비

**Q&A 수정 조건**: 서버 도메인의 `canEdit`는 `memberNo == 0 && step > 0`일 때 참이다. 메뉴의 작업 권한 외에 이 데이터 조건을 만족해야 한다. 선택한 검증 게시물에서는 수정 버튼이 비활성화되었고 수정 URL 진입도 상세로 돌아왔다. 임의의 게시물을 수정 가능한 것으로 안내하지 않는다. 서버 Service도 같은 조건을 검사한다.

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
|---|---|---|
| 화면 진입·조회 | `/customer-support/qna` 메뉴 접근·하위 경로 작업 권한. 조회 API는 VIEW, 등록/수정 경로는 PROCESS 등 아래 서버 액션과 라우트 가드를 함께 적용한다. | 로그인된 관리자 계정; id 식별자는 이전 화면에서 선택한다. |
| 답글 | `/customer-support/qna`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 수정 | `/customer-support/qna`; 화면 게이트 PROCESS. 실제 서버 액션은 API별 표 참조. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 삭제 | `/customer-support/qna`; 화면 게이트 DELETE. 실제 서버 액션은 API별 표 참조. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 목록 | `/customer-support/qna`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |

서버가 최종 권한을 검사한다. 버튼 모양(kind)으로 권한을 추정하지 않는다. 특히 등록·수정이 PROCESS를 사용하는 API와 EXECUTE·UNMASK·EXCEL_DOWNLOAD는 서로 구분한다.

## 3) 화면 사용 절차

**검증 시 화면 버튼**: HTML로 전환, 답글, 수정 (비활성), 삭제, 목록. 화면 상태·대상에 따라 달라지며 아래 작업 절차와 권한 조건을 함께 확인한다.

1. 관련 화면에서 대상 또는 작업을 선택하여 `/customer-support/qna/:id`로 이동한다. 경로 변수는 주소에서 임의로 바꾸지 않고 이전 화면이 전달한 식별자를 사용한다.
2. 대상의 기본 정보·상태·표시 항목을 확인한다. 목록의 식별자와 상세 대상이 일치하는지 확인한다.
3. **답글, 수정, 삭제** 중 필요한 작업을 선택한다. 버튼의 표시·활성 조건과 아래 API별 권한을 확인한다. 저장·삭제·외부 호출 전에는 대상과 현재 상태를 재확인한다.
4. 작업 결과 또는 다운로드 파일을 확인하고 관련 목록으로 돌아가 변경된 상태를 다시 조회한다.

**이 화면에서 유의할 업무 규칙**: 목록에서 구분·분류·검색 조건을 지정한다. 답글은 원문의 별도 답글 경로에서 작성하며 원문의 분류·인용 내용을 확인한다. 기본 답글 문구를 실제 문의에 맞게 수정한 뒤 저장한다.

**본문 표시·편집 모드**: 현재 내용과 모드에 따라 **HTML로 전환**, **HTML로 작성**, **WYSIWYG 보기** 등의 버튼이 표시된다. 상세의 표시 모드 전환과 등록·수정 폼의 편집 모드 전환을 구분한다. 기존 HTML을 수정하는 경우 현재 편집 모드와 저장할 본문을 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
|---|---|---|---|
| 내용 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/board/qna/AdminQnaDetailPage.tsx#L202) |

화면 필드 키와 API 필드명이 다른 경우 변환은 Hook/API의 검색·저장 매핑에서 수행된다. 요청·응답 필드와 DB 컬럼 매핑은 아래 API 계약 및 DB 객체 계약에 연결했다.

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
|---|---|---|---|
| 1:1 문의 단건 상세 | [GET /api/v1/support/qnas/{id}](../../references/api-contracts.md#api150); `/customer-support/qna` / `VIEW` | `경로·쿼리·본문 계약 참조` → `canEdit, id, qnaType, title, content, createdDate, viewCount, writer, parentId, step, replyCount, memberCompany, businessRegNo, companyName, memberName, memberId` | 쓰기 대상 smartbill3.dbo.qna; 동적 SQL의 런타임 대상은 미확정 |
| 1:1 문의 삭제 | [DELETE /api/v1/support/qnas/{id}](../../references/api-contracts.md#api007); `/customer-support/qna` / `DELETE` | `경로·쿼리·본문 계약 참조` → `응답 DTO·파일/처리 결과 계약 참조` | 쓰기 대상 smartbill3.dbo.qna, smartbill3.dbo.se_delete; 동적 SQL의 런타임 대상은 미확정 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
|---|---|---|---|
| [SMARTBILL3.dbo.upAdmSB_Cnt_QnaVisit](../../references/database-contracts.md#db214) | `@qnaNo no IN` | 쓰기: smartbill3.dbo.qna. 참조: smartbill3.dbo.qna | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SMARTBILL3.dbo.upAdmSB_LstMem](../../references/database-contracts.md#db229) | `@no varchar(10) IN, @GUBUN varchar(10) IN` | 확정한 테이블 쓰기 없음. 참조: sb_dti_log.dbo.dormant_member, sb_dti_log.dbo.member_login_his, sb_mobile.dbo.member, smartbill3.dbo.company, smartbill3.dbo.member, smartbill3.dbo.member_agreement | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SMARTBILL3.dbo.upAdmSB_Lst_EachQna](../../references/database-contracts.md#db225) | `@div varchar(12) IN, @cnt varchar(12) IN, @num varchar(12) IN` | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.qna 동적 SQL 포함, 런타임 조합 대상 미확정. | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SMARTBILL3.dbo.upAdmSB_DelQna](../../references/database-contracts.md#db220) | `@num no IN` | 쓰기: smartbill3.dbo.qna, smartbill3.dbo.se_delete. 참조: smartbill3.dbo.qna, smartbill3.dbo.se_delete | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |

위 DB 계약 링크에는 실제 파라미터 타입·기본값·IN/OUT, Mapper 결과 컬럼, RETURN 바인딩, 참조 테이블·하위 프로시저·정의 필터/정렬을 기록했다. DTO·Service·Repository·Mapper의 상세 호출 경로는 각 API 계약에서 확인한다.

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
|---|---|---|
| 결과가 없거나 기대 건수와 다름 | 적용된 검색 기준·기간·탭·대상 상태·서버 필터·페이징·목록/다운로드 조건 | 조건을 다시 확인하고 조회한다. 지속되면 경로·작업 시각·마스킹한 식별자·필터를 업무/기술 담당에게 전달한다. |
| 메뉴·버튼 미표시 또는 접근 거부 | 사용자 그룹의 메뉴 접근·VIEW 및 API별 PROCESS/EXECUTE/DELETE/EXCEL_DOWNLOAD/UNMASK 등 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. 프런트 버튼 표시만으로 서버 권한을 판단하지 않는다. |
| 저장·삭제·외부 실행의 결과가 불명확 | 대상 현재 상태·중복 요청·감사 이력·API 오류·파일/외부 소비 로그 | 기존 반영 여부를 먼저 조회한다. 중복 발송·초기화·금액 처리를 피하기 위해 기술 담당 확인 후 재시도한다. |

## 7) 검증·출처

**브라우저 검증(2026-11-09)**: 화면 대조. [경로별 결과와 제한](../../references/browser-verification.md#page096). 역할별 권한 거부·저장 성공·파일 반출·외부 연계 완료는 이 결과로 보장하지 않는다.

| 검증 항목 | 근거·환경 | 상태·확인일 |
|---|---|---|
| 대상 선정 | 사용자가 WBS 탭 내용으로 제공한 텍스트의 No. 338, 339; [선정 태스크](../../inventory/wbs-tasks.csv) | 제공 텍스트 확인 2026-11-09. 원본 Excel의 탭/병합 셀을 독립 재열람한 것은 아님. |
| 메뉴·라우트·화면 | [menuConfig.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts); [CustomerSupportRoutes.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/CustomerSupportRoutes.tsx); [AdminQnaDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/board/qna/AdminQnaDetailPage.tsx) | 코드 확인 2026-11-09, 기준 dc216b313 |
| 기능·권한·API | 이 문서의 API 계약 링크 및 연결 Hook/API·Controller·DTO·Service·Repository·Mapper | 코드 확인 2026-11-09. 조회 요청·화면 대조 범위는 아래 브라우저 근거 참조. 권한 계정별 허용·거부 및 변경 요청 실행은 미확인. |
| DB 정의 | [개발 DB 계약](../../references/database-contracts.md), 이 문서의 연결 객체 | 개발 DB 정의 확인 2026-11-09. 동적 SQL·CLR 내부·정의 미공개 참조의 미확정 범위는 객체별 기록; 후속 확인 DB 담당. |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-4a8be6dd38083cb0) | Demo 메타데이터 4/4개 확인 · 2026-11-11 |
| 브라우저 화면·배포 환경 | 로컬 인증 계정·Playwright CLI; [화면별 검증표](../../references/browser-verification.md#page096) | 화면 대조, 2026-11-09. 배포본·타 역할·업무 변경 결과는 미확인. |
| 업무 프로시저·쓰기·외부 결과 | 격리된 검증 환경·테스트 데이터의 실행 결과 | 미확인: 명시적인 저장·삭제·발송·초기화 요청은 실행하지 않음. 브라우저 GET의 업무 조회 프로시저·조회수·감사 기록은 별도 영향으로 구분. 격리 환경에서 기술 담당 확인. |

코드 확인과 DB 정의 확인은 실행 성공·업무 승인·다른 환경 적용을 보장하지 않는다. 업무·기술 담당 검토 후 조사 목록의 상태를 완료로 변경한다.

브라우저 직접 근거: [settled-detail-revisit](../../evidence/browser/ready-details-stable.json). 경로·고정 버튼명·입력 속성·표 머리글·API 상태를 보관했고 실제 데이터 값·식별자·인증정보는 제외했다.

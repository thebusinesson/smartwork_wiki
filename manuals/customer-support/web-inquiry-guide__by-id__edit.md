# [고객지원] WEB 문의 가이드 (수정) 관리자 매뉴얼

작성 기준: `dc216b313` · 확인일 2026-11-09 · 조사 상태 **검토 대기**. 코드·개발 DB 정의 확인. 브라우저: **화면 대조**; 저장·발송 등 업무 실행 결과는 미검증이다.

## 1) 화면 기본 정보

| 항목 | 작성 내용 |
|---|---|
| 업무 도메인·목적 | WEB 문의 가이드의 게시글·첨부파일·댓글을 관리한다. |
| 메뉴·화면 경로 | 고객지원 > 서비스 플랫폼 관리(자료실) > WEB 문의 가이드; `/customer-support/web-inquiry-guide/:id/edit`; 목록에서 선택한 대상의 경로 변수를 유지하여 진입한다. |
| 화면 유형·담당 | 수정; WBS 작업자 유지윤. 업무·기술 담당 팀명은 원문에 없어 배포 전 해당 도메인 담당자가 확정한다. |
| 관련 화면 | [조회·관리](web-inquiry-guide.md); [등록](web-inquiry-guide__new.md); [상세](web-inquiry-guide__by-id.md) |

WBS 근거: No. 346, 347 (사용자가 제공한 텍스트 행 478, 479). API 개발/화면 개발의 중복 행은 같은 화면으로 통합했다.

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
|---|---|---|
| 화면 진입·조회 | `/customer-support/web-inquiry-guide` 메뉴 접근·하위 경로 작업 권한. 조회 API는 VIEW, 등록/수정 경로는 PROCESS 등 아래 서버 액션과 라우트 가드를 함께 적용한다. | 로그인된 관리자 계정; id 식별자는 이전 화면에서 선택한다. |
| 저장 | `/customer-support/web-inquiry-guide`; 화면 게이트 PROCESS. 실제 서버 액션은 API별 표 참조. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 목록 | `/customer-support/web-inquiry-guide`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |

서버가 최종 권한을 검사한다. 버튼 모양(kind)으로 권한을 추정하지 않는다. 특히 등록·수정이 PROCESS를 사용하는 API와 EXECUTE·UNMASK·EXCEL_DOWNLOAD는 서로 구분한다.

## 3) 화면 사용 절차

**검증 시 화면 버튼**: 기존 파일 삭제, 파일 선택, HTML로 작성, 저장, 목록. 화면 상태·대상에 따라 달라지며 아래 작업 절차와 권한 조건을 함께 확인한다.

1. 관련 화면에서 대상 또는 작업을 선택하여 `/customer-support/web-inquiry-guide/:id/edit`로 이동한다. 경로 변수는 주소에서 임의로 바꾸지 않고 이전 화면이 전달한 식별자를 사용한다.
2. **내용, 제목, 파일 첨부**의 입력값을 확인한다. 기존 정보와 원문을 확인한 뒤 변경한다. 필수값과 형식 오류가 표시되면 해당 항목을 수정한다.
3. **저장**을 누르고 확인창이 있으면 대상·작업을 확인한다. 첨부가 있으면 기존 파일의 유지·삭제·교체 선택을 함께 확인한다.
4. 처리 결과 메시지를 확인한 뒤 목록 또는 상세에서 결과를 다시 조회한다. 오류가 나면 아래 예외 대응과 API 오류를 확인하고 중복 저장 전에 기존 처리 여부를 확인한다.

**이 화면에서 유의할 업무 규칙**: 이 화면의 게시판 유형은 F다. 제목·내용·전체 검색을 선택한 뒤 검색하고, 작성/상세/수정 화면에서도 같은 유형을 유지한다. 첨부 다운로드와 댓글 작성·삭제는 게시글 저장과 별도 작업이며 댓글 삭제의 작성자 조건을 확인한다.

공통 폼이 등록·수정·상세 입력값 조회 함수를 함께 포함할 수 있다. 아래 API 표에 공통 구현의 다른 모드가 표시되어도 현재 경로의 작업으로 모두 실행하는 것은 아니다.

**본문 표시·편집 모드**: 현재 내용과 모드에 따라 **HTML로 전환**, **HTML로 작성**, **WYSIWYG 보기** 등의 버튼이 표시된다. 상세의 표시 모드 전환과 등록·수정 폼의 편집 모드 전환을 구분한다. 기존 HTML을 수정하는 경우 현재 편집 모드와 저장할 본문을 확인한다.

**첨부 조작**: 새 첨부는 **파일 선택**, 기존 첨부 제거는 표시된 **기존 파일 삭제**를 사용한다. 제거 선택과 새 파일 교체 상태를 확인한 뒤 저장한다. 다운로드 버튼에 표시되는 실제 고객 파일명은 예시나 검증 자료에 복사하지 않는다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
|---|---|---|---|
| 내용 | 입력·필수 | API 타입 String?; 초기값 빈값 | `content`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/board/spfBoard/AdminSpfBoardFormPage.tsx#L221) |
| 제목 | 입력·필수 | 최대 50자; API 타입 String?; 초기값 빈값 | `title`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/board/spfBoard/components/form/AdminSpfBoardFormFields.tsx#L40) |
| 이전 파일 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/board/spfBoard/components/form/AdminSpfBoardFormFields.tsx#L57) |
| 파일 첨부 | 입력·선택(조건부 검증 별도) | 길이·형식·조건부 필수는 검증 코드와 API DTO 참조 | `file`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/board/spfBoard/components/form/AdminSpfBoardFormFields.tsx#L87) |

입력 검증 근거: [sharedTitleContent.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/support/board/sharedTitleContent.ts). 프런트 검증과 서버 DTO 제약이 다르면 서버 검증이 최종 기준이다.

**복합 검색·폼의 초기 상태**

| 초기값 근거 | 기본 상태 |
|---|---|
| [buildInitialForm](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/board/spfBoard/AdminSpfBoardFormPage.tsx#L29) | title=빈값; content=빈값; isHtmlMode=꺼짐; newFile=미지정; existingFileName=미지정; existingFileSize=미지정; removeExistingFile=꺼짐 |

화면 필드 키와 API 필드명이 다른 경우 변환은 Hook/API의 검색·저장 매핑에서 수행된다. 요청·응답 필드와 DB 컬럼 매핑은 아래 API 계약 및 DB 객체 계약에 연결했다.

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
|---|---|---|---|
| 게시판 단건 상세 | [GET /api/v1/support/spf-boards/{type}/{id}](../../references/api-contracts.md#api152); `/customer-support/web-inquiry-guide` / `VIEW` | `경로·쿼리·본문 계약 참조` → `id, notiType, title, sname, swNo, content, hit, createdDate, originalFileName, fileSize` | 쓰기 대상 office.dbo.notice; 동적 SQL의 런타임 대상은 미확정 |
| 게시판 신규 등록 | [POST /api/v1/support/spf-boards/{type}](../../references/api-contracts.md#api246); `/customer-support/web-inquiry-guide` / `PROCESS` | `title, content, removeFile` → `응답 DTO·파일/처리 결과 계약 참조` | 쓰기 대상 office.dbo.notice, smartwork.dbo.spf_board_attachment_meta |
| 게시판 수정 | [PUT /api/v1/support/spf-boards/{type}/{id}](../../references/api-contracts.md#api273); `/customer-support/web-inquiry-guide` / `PROCESS` | `title, content, removeFile` → `응답 DTO·파일/처리 결과 계약 참조` | 쓰기 대상 office.dbo.notice, smartwork.dbo.spf_board_attachment_meta; 동적 SQL의 런타임 대상은 미확정 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
|---|---|---|---|
| [smartwork.dbo.spf_board_attachment_meta](../../references/database-contracts.md#db275) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 쓰기: smartwork.dbo.spf_board_attachment_meta. 참조: smartwork.dbo.spf_board_attachment_meta | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [office.dbo.upNT_UpHitNotice](../../references/database-contracts.md#db057) | `@noti_id int IN` | 쓰기: office.dbo.notice. 참조: office.dbo.notice | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [office.dbo.upNT_LstNotice](../../references/database-contracts.md#db052) | `@sch_Code char(1) IN, @sch_Text varchar(100) IN, @noti_id int IN, @strDiv char(1) IN` | 확정한 테이블 쓰기 없음. 참조: office.dbo.notice, office.dbo.sawon 동적 SQL 포함, 런타임 조합 대상 미확정. | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [office.dbo.upNT_SavNotice](../../references/database-contracts.md#db055) | `@noti_type char(1) IN, @title varchar(50) IN, @content text IN, @att_file varchar(1000) IN, @hit int IN, @sw_no int IN` | 쓰기: office.dbo.notice. 참조: office.dbo.notice | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [office.dbo.upNT_ModNotice](../../references/database-contracts.md#db054) | `@note_id int IN, @title varchar(50) IN, @content text IN, @att_file varchar(1000) IN` | 쓰기: office.dbo.notice. 참조: office.dbo.notice | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| 파일: storage.support-file-pds | spf/{type}/{id}/attachment/{원본 파일명}; JSON payload + 선택 file | 기존 첨부 KEEP/REMOVE/REPLACE. 새 파일과 removeFile=true 동시 지정은 검증 오류. 원래 파일명·크기·저장 경로는 메타와 구분 | [StorageProperties.kt](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/shared/upload/config/StorageProperties.kt) |

위 DB 계약 링크에는 실제 파라미터 타입·기본값·IN/OUT, Mapper 결과 컬럼, RETURN 바인딩, 참조 테이블·하위 프로시저·정의 필터/정렬을 기록했다. DTO·Service·Repository·Mapper의 상세 호출 경로는 각 API 계약에서 확인한다.

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
|---|---|---|
| 결과가 없거나 기대 건수와 다름 | 적용된 검색 기준·기간·탭·대상 상태·서버 필터·페이징·목록/다운로드 조건 | 조건을 다시 확인하고 조회한다. 지속되면 경로·작업 시각·마스킹한 식별자·필터를 업무/기술 담당에게 전달한다. |
| 메뉴·버튼 미표시 또는 접근 거부 | 사용자 그룹의 메뉴 접근·VIEW 및 API별 PROCESS/EXECUTE/DELETE/EXCEL_DOWNLOAD/UNMASK 등 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. 프런트 버튼 표시만으로 서버 권한을 판단하지 않는다. |
| 저장·삭제·외부 실행의 결과가 불명확 | 대상 현재 상태·중복 요청·감사 이력·API 오류·파일/외부 소비 로그 | 기존 반영 여부를 먼저 조회한다. 중복 발송·초기화·금액 처리를 피하기 위해 기술 담당 확인 후 재시도한다. |

## 7) 검증·출처

**브라우저 검증(2026-11-09)**: 화면 대조. [경로별 결과와 제한](../../references/browser-verification.md#page113). 역할별 권한 거부·저장 성공·파일 반출·외부 연계 완료는 이 결과로 보장하지 않는다.

| 검증 항목 | 근거·환경 | 상태·확인일 |
|---|---|---|
| 대상 선정 | 사용자가 WBS 탭 내용으로 제공한 텍스트의 No. 346, 347; [선정 태스크](../../inventory/wbs-tasks.csv) | 제공 텍스트 확인 2026-11-09. 원본 Excel의 탭/병합 셀을 독립 재열람한 것은 아님. |
| 메뉴·라우트·화면 | [menuConfig.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts); [CustomerSupportRoutes.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/CustomerSupportRoutes.tsx); [AdminSpfBoardEditPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/board/spfBoard/AdminSpfBoardEditPage.tsx) | 코드 확인 2026-11-09, 기준 dc216b313 |
| 기능·권한·API | 이 문서의 API 계약 링크 및 연결 Hook/API·Controller·DTO·Service·Repository·Mapper | 코드 확인 2026-11-09. 조회 요청·화면 대조 범위는 아래 브라우저 근거 참조. 권한 계정별 허용·거부 및 변경 요청 실행은 미확인. |
| DB 정의 | [개발 DB 계약](../../references/database-contracts.md), 이 문서의 연결 객체 | 개발 DB 정의 확인 2026-11-09. 동적 SQL·CLR 내부·정의 미공개 참조의 미확정 범위는 객체별 기록; 후속 확인 DB 담당. |
| 브라우저 화면·배포 환경 | 로컬 인증 계정·Playwright CLI; [화면별 검증표](../../references/browser-verification.md#page113) | 화면 대조, 2026-11-09. 배포본·타 역할·업무 변경 결과는 미확인. |
| 업무 프로시저·쓰기·외부 결과 | 격리된 검증 환경·테스트 데이터의 실행 결과 | 미확인: 명시적인 저장·삭제·발송·초기화 요청은 실행하지 않음. 브라우저 GET의 업무 조회 프로시저·조회수·감사 기록은 별도 영향으로 구분. 격리 환경에서 기술 담당 확인. |

코드 확인과 DB 정의 확인은 실행 성공·업무 승인·다른 환경 적용을 보장하지 않는다. 업무·기술 담당 검토 후 조사 목록의 상태를 완료로 변경한다.

브라우저 직접 근거: [settled-detail-revisit](../../evidence/browser/ready-details-stable.json). 경로·고정 버튼명·입력 속성·표 머리글·API 상태를 보관했고 실제 데이터 값·식별자·인증정보는 제외했다.

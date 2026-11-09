# [고객지원] SAP 문의 가이드 (조회·관리) 관리자 매뉴얼

작성 기준: `dc216b313` · 확인일 2026-11-09 · 조사 상태 **검토 대기**. 코드·개발 DB 정의 확인. 브라우저: **화면 대조**; 저장·발송 등 업무 실행 결과는 미검증이다.

## 1) 화면 기본 정보

### 도메인 이해

WEB·SAP·NSAP 등 서비스 연동 구분별로 자료와 문의 대응 가이드를 게시하는 업무다. 연동 담당자가 대상 플랫폼의 설명·첨부파일·댓글을 찾아 보고 필요한 게시물을 관리할 때 사용한다.

| 구분 | 설명 |
|---|---|
| 업무 영역 | 연동 플랫폼 자료·문의 가이드 · 고객지원 > 서비스 플랫폼 관리(자료실) > SAP 문의 가이드 |
| 주요 대상·용어 | WEB·SAP·NSAP: 현재 메뉴가 구분하는 연동 자료 영역 / 자료실: 설명·파일 게시 / 문의 가이드: 문의 대응 안내 / 연동업체 소스 관리: 관련 소스 자료 게시판 |
| 업무 흐름 | 연동 구분·게시판 선택 → 게시물 검색 → 내용·첨부·댓글 확인 → 필요한 게시물 작성·수정 |
| 이 페이지의 역할 | SAP 문의 가이드 업무의 진입 화면이다. SAP 문의 가이드 게시판의 자료·본문·첨부파일·댓글을 해당 연동 구분 안에서 관리한다. 같은 메뉴의 팝업·탭은 이 문서에서, 독립 상세·등록·수정 화면은 관련 문서에서 다룬다. |
| 관련 업무와 구분 | 같은 제목·파일명이어도 게시판 유형과 게시글 ID가 다르면 다른 자료다. 여기의 소스 게시글 관리와 운영반영 관리의 배포 계획 기록은 별개다. |

도메인 설명 근거: 이 문서 7번의 현재 메뉴·라우트·화면 및 API·업무 규칙 소스. [전체 도메인 지도](../../references/domain-overview.md#platform). 설명 보강일 2026-11-09; 기존 실행 검증 범위와 미확인 상태는 변경하지 않았다.

### 화면 정보

| 항목 | 작성 내용 |
|---|---|
| 업무 도메인·목적 | SAP 문의 가이드의 게시글·첨부파일·댓글을 관리한다. |
| 메뉴·화면 경로 | 고객지원 > 서비스 플랫폼 관리(자료실) > SAP 문의 가이드; `/customer-support/sap-inquiry-guide`; 메뉴 또는 관련 화면에서 진입한다. |
| 화면 유형·담당 | 조회·관리; WBS 작업자 유지윤. 업무·기술 담당 팀명은 원문에 없어 배포 전 해당 도메인 담당자가 확정한다. |
| 관련 화면 | [등록](sap-inquiry-guide__new.md); [상세](sap-inquiry-guide__by-id.md); [수정](sap-inquiry-guide__by-id__edit.md) |

WBS 근거: No. 350, 351 (사용자가 제공한 텍스트 행 484, 485). API 개발/화면 개발의 중복 행은 같은 화면으로 통합했다.

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
|---|---|---|
| 화면 진입·조회 | `/customer-support/sap-inquiry-guide` 메뉴 접근·하위 경로 작업 권한. 조회 API는 VIEW, 등록/수정 경로는 PROCESS 등 아래 서버 액션과 라우트 가드를 함께 적용한다. | 로그인된 관리자 계정; 아래 검색·입력 항목을 준비한다. |
| 작성 | `/customer-support/sap-inquiry-guide`; 화면 게이트 PROCESS. 실제 서버 액션은 API별 표 참조. | 작업 대상과 현재 상태·변경 내용을 확인한다. |

서버가 최종 권한을 검사한다. 버튼 모양(kind)으로 권한을 추정하지 않는다. 특히 등록·수정이 PROCESS를 사용하는 API와 EXECUTE·UNMASK·EXCEL_DOWNLOAD는 서로 구분한다.

## 3) 화면 사용 절차

**검증 시 화면 버튼**: 검색, 작성. 화면 상태·대상에 따라 달라지며 아래 작업 절차와 권한 조건을 함께 확인한다.

1. `고객지원 > 서비스 플랫폼 관리(자료실) > SAP 문의 가이드` 메뉴를 연다. 경로 변수는 주소에서 임의로 바꾸지 않고 이전 화면이 전달한 식별자를 사용한다.
2. 현재 검색 조건과 아래 기본값을 확인한다. **검색** 항목에 필요한 값을 입력하고 **검색**을 누른다.
3. 결과 행에서 업무 대상을 선택하여 관련 상세 화면으로 이동한다. 페이지 이동·검색 조건 변경 후에는 현재 조건과 조회 대상을 다시 확인한다.

**이 화면에서 유의할 업무 규칙**: 이 화면의 게시판 유형은 G다. 제목·내용·전체 검색을 선택한 뒤 검색하고, 작성/상세/수정 화면에서도 같은 유형을 유지한다. 첨부 다운로드와 댓글 작성·삭제는 게시글 저장과 별도 작업이며 댓글 삭제의 작성자 조건을 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
|---|---|---|---|
| 검색 | 입력·선택(조건부 검증 별도) | 화면 타입 selectWithInput; 초기값 selectValue=A; inputValue=빈값; 입력 안내 검색어 | `search`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/board/spfBoard/AdminSpfBoardListPage.tsx#L82) |
| No | 출력 | API 타입 Int | `rowNumber`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/board/spfBoard/AdminSpfBoardListPage.tsx#L123) |
| 제목 | 출력 | API 타입 String? | `title`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/board/spfBoard/AdminSpfBoardListPage.tsx#L130) |
| 작성자 | 출력 | API 타입 String? | `sname`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/board/spfBoard/AdminSpfBoardListPage.tsx#L146) |
| 작성일 | 출력 | API 타입 String? | `createdDate`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/board/spfBoard/AdminSpfBoardListPage.tsx#L162) |
| 파일 | 출력 | API 타입 Boolean | `hasFile`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/board/spfBoard/AdminSpfBoardListPage.tsx#L169) |
| 조회수 | 출력 | API 타입 Int | `hit`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/board/spfBoard/AdminSpfBoardListPage.tsx#L191) |

**복합 검색·폼의 초기 상태**

| 초기값 근거 | 기본 상태 |
|---|---|
| [buildDefaultFilters](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/board/spfBoard/AdminSpfBoardListPage.tsx#L39) | selectValue=A; inputValue=빈값 |

화면 필드 키와 API 필드명이 다른 경우 변환은 Hook/API의 검색·저장 매핑에서 수행된다. 요청·응답 필드와 DB 컬럼 매핑은 아래 API 계약 및 DB 객체 계약에 연결했다.

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
|---|---|---|---|
| 게시판 목록 (검색 + 페이징) | [GET /api/v1/support/spf-boards/{type}](../../references/api-contracts.md#api151); `/customer-support/sap-inquiry-guide` / `VIEW` | `schCode, schText, page, size` → `content, totalElements, totalPages, page, size, id, rowNumber, notiType, title, sname, swNo, hasFile, hit, createdDate, replyCount` | Mapper 프로시저의 정적 테이블 쓰기 미검출; 동적 SQL의 런타임 대상은 미확정 |
| 게시판 첨부파일 다운로드 | [GET /api/v1/support/spf-boards/{type}/{id}/file](../../references/api-contracts.md#api153); `/customer-support/sap-inquiry-guide` / `VIEW` | `경로·쿼리·본문 계약 참조` → `응답 DTO·파일/처리 결과 계약 참조` | Mapper 프로시저의 정적 테이블 쓰기 미검출; 동적 SQL의 런타임 대상은 미확정 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
|---|---|---|---|
| [office.dbo.upNT_CnttNoticeReply](../../references/database-contracts.md#db049) | `@noti_id int IN` | 확정한 테이블 쓰기 없음. 참조: office.dbo.notice_reply | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [office.dbo.upNT_LstNotice](../../references/database-contracts.md#db052) | `@sch_Code char(1) IN, @sch_Text varchar(100) IN, @noti_id int IN, @strDiv char(1) IN` | 확정한 테이블 쓰기 없음. 참조: office.dbo.notice, office.dbo.sawon 동적 SQL 포함, 런타임 조합 대상 미확정. | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.spf_board_attachment_meta](../../references/database-contracts.md#db275) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: smartwork.dbo.spf_board_attachment_meta | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| 파일: storage.support-file-pds | spf/{type}/{id}/attachment/{원본 파일명}; JSON payload + 선택 file | 기존 첨부 KEEP/REMOVE/REPLACE. 새 파일과 removeFile=true 동시 지정은 검증 오류. 원래 파일명·크기·저장 경로는 메타와 구분 | [StorageProperties.kt](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/shared/upload/config/StorageProperties.kt) |

위 DB 계약 링크에는 실제 파라미터 타입·기본값·IN/OUT, Mapper 결과 컬럼, RETURN 바인딩, 참조 테이블·하위 프로시저·정의 필터/정렬을 기록했다. DTO·Service·Repository·Mapper의 상세 호출 경로는 각 API 계약에서 확인한다.

**파일**: 업로드·다운로드의 소유 대상, 원래 파일명, 저장 경로 설정, 파일 존재 여부를 구분한다. 저장소 경로와 비밀값은 사용자 입력으로 대체하지 않는다. 파일·외부 연계 상세는 API의 연결 Service·설정 키 근거를 참조한다.

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
|---|---|---|
| 조회된 자료가 없습니다. | [문구·처리 코드](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/board/spfBoard/AdminSpfBoardListPage.tsx#L221); 현재 조건·대상·권한 확인 | 검색·조회 오류면 조건을 확인 후 재조회. 변경·발송 결과가 불명확하면 처리 여부와 이력을 확인한 뒤 재시도 여부를 판단한다. |
| 결과가 없거나 기대 건수와 다름 | 적용된 검색 기준·기간·탭·대상 상태·서버 필터·페이징·목록/다운로드 조건 | 조건을 다시 확인하고 조회한다. 지속되면 경로·작업 시각·마스킹한 식별자·필터를 업무/기술 담당에게 전달한다. |
| 메뉴·버튼 미표시 또는 접근 거부 | 사용자 그룹의 메뉴 접근·VIEW 및 API별 PROCESS/EXECUTE/DELETE/EXCEL_DOWNLOAD/UNMASK 등 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. 프런트 버튼 표시만으로 서버 권한을 판단하지 않는다. |
| 저장·삭제·외부 실행의 결과가 불명확 | 대상 현재 상태·중복 요청·감사 이력·API 오류·파일/외부 소비 로그 | 기존 반영 여부를 먼저 조회한다. 중복 발송·초기화·금액 처리를 피하기 위해 기술 담당 확인 후 재시도한다. |

## 7) 검증·출처

**브라우저 검증(2026-11-09)**: 화면 대조. [경로별 결과와 제한](../../references/browser-verification.md#page119). 역할별 권한 거부·저장 성공·파일 반출·외부 연계 완료는 이 결과로 보장하지 않는다.

| 검증 항목 | 근거·환경 | 상태·확인일 |
|---|---|---|
| 대상 선정 | 사용자가 WBS 탭 내용으로 제공한 텍스트의 No. 350, 351; [선정 태스크](../../inventory/wbs-tasks.csv) | 제공 텍스트 확인 2026-11-09. 원본 Excel의 탭/병합 셀을 독립 재열람한 것은 아님. |
| 메뉴·라우트·화면 | [menuConfig.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts); [CustomerSupportRoutes.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/CustomerSupportRoutes.tsx); [AdminSpfBoardListPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/board/spfBoard/AdminSpfBoardListPage.tsx) | 코드 확인 2026-11-09, 기준 dc216b313 |
| 기능·권한·API | 이 문서의 API 계약 링크 및 연결 Hook/API·Controller·DTO·Service·Repository·Mapper | 코드 확인 2026-11-09. 조회 요청·화면 대조 범위는 아래 브라우저 근거 참조. 권한 계정별 허용·거부 및 변경 요청 실행은 미확인. |
| DB 정의 | [개발 DB 계약](../../references/database-contracts.md), 이 문서의 연결 객체 | 개발 DB 정의 확인 2026-11-09. 동적 SQL·CLR 내부·정의 미공개 참조의 미확정 범위는 객체별 기록; 후속 확인 DB 담당. |
| 브라우저 화면·배포 환경 | 로컬 인증 계정·Playwright CLI; [화면별 검증표](../../references/browser-verification.md#page119) | 화면 대조, 2026-11-09. 배포본·타 역할·업무 변경 결과는 미확인. |
| 업무 프로시저·쓰기·외부 결과 | 격리된 검증 환경·테스트 데이터의 실행 결과 | 미확인: 명시적인 저장·삭제·발송·초기화 요청은 실행하지 않음. 브라우저 GET의 업무 조회 프로시저·조회수·감사 기록은 별도 영향으로 구분. 격리 환경에서 기술 담당 확인. |

코드 확인과 DB 정의 확인은 실행 성공·업무 승인·다른 환경 적용을 보장하지 않는다. 업무·기술 담당 검토 후 조사 목록의 상태를 완료로 변경한다.

브라우저 직접 근거: [settled-static-recheck](../../evidence/browser/static-stable.json). 경로·고정 버튼명·입력 속성·표 머리글·API 상태를 보관했고 실제 데이터 값·식별자·인증정보는 제외했다.

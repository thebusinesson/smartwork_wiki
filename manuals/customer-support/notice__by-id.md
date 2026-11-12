# [고객지원] 공지사항 (상세) 관리자 매뉴얼

작성 기준: `dc216b313` · 확인일 2026-11-09 · 조사 상태 **검토 대기**. 코드·개발 DB 정의 확인. 브라우저: **화면 대조**; 저장·발송 등 업무 실행 결과는 미검증이다.

## 1) 화면 기본 정보

### 도메인 이해

선택한 고객 공지 게시물 한 건의 내용을 읽고 후속 지원 여부를 판단한다. 제목·본문과 채널별 공지·팝업 기간을 함께 읽는다.

| 구분 | 설명 |
|---|---|
| 업무 영역 | 고객 게시판·문의 응대 > 공지사항 상세 |
| 언제 사용하는가 | 고객 공지 목록에서 검색한 대상의 실제 설명·문의 내용 또는 파일을 확인할 때 |
| 주요 대상·데이터 | 제목·내용은 안내문, 웹 공지·모바일 공지·모바일 팝업·팝업 기간은 노출 설정이다. 목록의 검색 조건 대신 선택한 게시글 ID의 내용을 다룬다. |
| 업무 흐름 | 고객 공지 게시물 식별 확인 → 본문·부가 정보 확인 → 필요한 수정·자료 확인 또는 목록 복귀 |
| 이 페이지의 역할 | 고객 공지 중 **공지사항 상세** 단계. 선택한 고객 공지 게시물 한 건의 내용을 읽고 후속 지원 여부를 판단한다. 제목·본문과 채널별 공지·팝업 기간을 함께 읽는다. |
| 판단 결과·다음 업무 | 고객 공지 내용으로 문의에 답할 수 있는지 판단하고 보완이 필요하면 해당 게시물의 수정 경로로 이동한다. |
| 다른 화면과의 구분 | 다른 고객 공지 글을 찾는 목록이나 내용을 저장하는 편집 단계와 다르다. 상세 열람에 따른 조회수 변화와 게시글 내용 변경도 구분한다. |

설명 근거: [AdminNoticeDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/board/notice/AdminNoticeDetailPage.tsx), 이 문서 4·5·7번의 항목·API·업무 규칙. [상위 업무 영역](../../references/domain-overview.md#board)은 공통 배경이며 현재 화면의 데이터·동작은 위 설명을 따른다. 설명 수정일 **2026-11-10**; 새 업무 실행 검증을 수행한 것은 아니다.

### 화면 정보

| 항목 | 작성 내용 |
|---|---|
| 업무 도메인·목적 | 선택한 고객 공지 게시물 한 건의 내용을 읽고 후속 지원 여부를 판단한다. 제목·본문과 채널별 공지·팝업 기간을 함께 읽는다. |
| 메뉴·화면 경로 | 고객지원 > 고객 게시판 관리 > 공지사항; `/customer-support/notice/:id`; 목록에서 선택한 대상의 경로 변수를 유지하여 진입한다. |
| 화면 유형·담당 | 상세; WBS 작업자 유지윤. 업무·기술 담당 팀명은 원문에 없어 배포 전 해당 도메인 담당자가 확정한다. |
| 관련 화면 | [조회·관리](notice.md); [등록](notice__new.md); [수정](notice__by-id__edit.md) |

WBS 근거: No. 334, 335 (사용자가 제공한 텍스트 행 457, 458). API 개발/화면 개발의 중복 행은 같은 화면으로 통합했다.

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
|---|---|---|
| 화면 진입·조회 | `/customer-support/notice` 메뉴 접근·하위 경로 작업 권한. 조회 API는 VIEW, 등록/수정 경로는 PROCESS 등 아래 서버 액션과 라우트 가드를 함께 적용한다. | 로그인된 관리자 계정; id 식별자는 이전 화면에서 선택한다. |
| 수정 | `/customer-support/notice`; 화면 게이트 PROCESS. 실제 서버 액션은 API별 표 참조. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 삭제 | `/customer-support/notice`; 화면 게이트 DELETE. 실제 서버 액션은 API별 표 참조. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 목록 | `/customer-support/notice`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |

서버가 최종 권한을 검사한다. 버튼 모양(kind)으로 권한을 추정하지 않는다. 특히 등록·수정이 PROCESS를 사용하는 API와 EXECUTE·UNMASK·EXCEL_DOWNLOAD는 서로 구분한다.

## 3) 화면 사용 절차

**검증 시 화면 버튼**: HTML로 전환, 수정, 삭제, 목록. 화면 상태·대상에 따라 달라지며 아래 작업 절차와 권한 조건을 함께 확인한다.

1. 관련 화면에서 대상 또는 작업을 선택하여 `/customer-support/notice/:id`로 이동한다. 경로 변수는 주소에서 임의로 바꾸지 않고 이전 화면이 전달한 식별자를 사용한다.
2. 대상의 기본 정보·상태·표시 항목을 확인한다. 목록의 식별자와 상세 대상이 일치하는지 확인한다.
3. **수정, 삭제** 중 필요한 작업을 선택한다. 버튼의 표시·활성 조건과 아래 API별 권한을 확인한다. 저장·삭제·외부 호출 전에는 대상과 현재 상태를 재확인한다.
4. 작업 결과 또는 다운로드 파일을 확인하고 관련 목록으로 돌아가 변경된 상태를 다시 조회한다.

**이 화면에서 유의할 업무 규칙**: 제목 또는 내용으로 검색하고 작성 버튼으로 새 공지를 등록한다. 상세의 조회수 증가와 수정 입력을 위한 incrementHit=false 조회를 구분한다.

**본문 표시·편집 모드**: 현재 내용과 모드에 따라 **HTML로 전환**, **HTML로 작성**, **WYSIWYG 보기** 등의 버튼이 표시된다. 상세의 표시 모드 전환과 등록·수정 폼의 편집 모드 전환을 구분한다. 기존 HTML을 수정하는 경우 현재 편집 모드와 저장할 본문을 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
|---|---|---|---|
| 제목 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/board/notice/AdminNoticeDetailPage.tsx#L133) |
| 웹 공지 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/board/notice/AdminNoticeDetailPage.tsx#L139) |
| 모바일 공지 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/board/notice/AdminNoticeDetailPage.tsx#L143) |
| 모바일 팝업 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/board/notice/AdminNoticeDetailPage.tsx#L147) |
| 팝업 기간 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/board/notice/AdminNoticeDetailPage.tsx#L154) |
| 내용 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/board/notice/AdminNoticeDetailPage.tsx#L162) |

화면 필드 키와 API 필드명이 다른 경우 변환은 Hook/API의 검색·저장 매핑에서 수행된다. 요청·응답 필드와 DB 컬럼 매핑은 아래 API 계약 및 DB 객체 계약에 연결했다.

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
|---|---|---|---|
| 공지사항 단건 상세 | [GET /api/v1/support/notices/{id}](../../references/api-contracts.md#api145); `/customer-support/notice` / `VIEW` | `경로·쿼리·본문 계약 참조` → `id, noticeType, title, content, createdDate, viewCount, mobileNoticeYn, webNoticeYn, mobilePopYn, mobilePopBeginDate, mobilePopEndDate` | 쓰기 대상 smartbill3.dbo.notice; 동적 SQL의 런타임 대상은 미확정 |
| 공지사항 삭제 | [DELETE /api/v1/support/notices/{id}](../../references/api-contracts.md#api005); `/customer-support/notice` / `DELETE` | `경로·쿼리·본문 계약 참조` → `응답 DTO·파일/처리 결과 계약 참조` | 쓰기 대상 smartbill3.dbo.notice, smartbill3.dbo.se_delete; 동적 SQL의 런타임 대상은 미확정 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
|---|---|---|---|
| [SB_COMMON.dbo.upSup_HitNotice](../../references/database-contracts.md#db119) | `@NOTICE_NO int IN, @ERR_CODE varchar(10) OUT, @ISSUCCESS bit OUT` | 쓰기: smartbill3.dbo.notice. 참조: smartbill3.dbo.notice | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SMARTBILL3.dbo.upAdmSB_Lst_EachNotice](../../references/database-contracts.md#db224) | `@div varchar(1) IN, @num no IN` | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.notice 동적 SQL 포함, 런타임 조합 대상 미확정. | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SMARTBILL3.dbo.upAdmSB_DelNotice](../../references/database-contracts.md#db218) | `@num no IN` | 쓰기: smartbill3.dbo.notice, smartbill3.dbo.se_delete. 참조: smartbill3.dbo.notice, smartbill3.dbo.se_delete | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |

위 DB 계약 링크에는 실제 파라미터 타입·기본값·IN/OUT, Mapper 결과 컬럼, RETURN 바인딩, 참조 테이블·하위 프로시저·정의 필터/정렬을 기록했다. DTO·Service·Repository·Mapper의 상세 호출 경로는 각 API 계약에서 확인한다.

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
|---|---|---|
| 결과가 없거나 기대 건수와 다름 | 적용된 검색 기준·기간·탭·대상 상태·서버 필터·페이징·목록/다운로드 조건 | 조건을 다시 확인하고 조회한다. 지속되면 경로·작업 시각·마스킹한 식별자·필터를 업무/기술 담당에게 전달한다. |
| 메뉴·버튼 미표시 또는 접근 거부 | 사용자 그룹의 메뉴 접근·VIEW 및 API별 PROCESS/EXECUTE/DELETE/EXCEL_DOWNLOAD/UNMASK 등 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. 프런트 버튼 표시만으로 서버 권한을 판단하지 않는다. |
| 저장·삭제·외부 실행의 결과가 불명확 | 대상 현재 상태·중복 요청·감사 이력·API 오류·파일/외부 소비 로그 | 기존 반영 여부를 먼저 조회한다. 중복 발송·초기화·금액 처리를 피하기 위해 기술 담당 확인 후 재시도한다. |

## 7) 검증·출처

**브라우저 검증(2026-11-09)**: 화면 대조. [경로별 결과와 제한](../../references/browser-verification.md#page088). 역할별 권한 거부·저장 성공·파일 반출·외부 연계 완료는 이 결과로 보장하지 않는다.

| 검증 항목 | 근거·환경 | 상태·확인일 |
|---|---|---|
| 대상 선정 | 사용자가 WBS 탭 내용으로 제공한 텍스트의 No. 334, 335; [선정 태스크](../../inventory/wbs-tasks.csv) | 제공 텍스트 확인 2026-11-09. 원본 Excel의 탭/병합 셀을 독립 재열람한 것은 아님. |
| 메뉴·라우트·화면 | [menuConfig.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts); [CustomerSupportRoutes.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/CustomerSupportRoutes.tsx); [AdminNoticeDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/board/notice/AdminNoticeDetailPage.tsx) | 코드 확인 2026-11-09, 기준 dc216b313 |
| 기능·권한·API | 이 문서의 API 계약 링크 및 연결 Hook/API·Controller·DTO·Service·Repository·Mapper | 코드 확인 2026-11-09. 조회 요청·화면 대조 범위는 아래 브라우저 근거 참조. 권한 계정별 허용·거부 및 변경 요청 실행은 미확인. |
| DB 정의 | [개발 DB 계약](../../references/database-contracts.md), 이 문서의 연결 객체 | 개발 DB 정의 확인 2026-11-09. 동적 SQL·CLR 내부·정의 미공개 참조의 미확정 범위는 객체별 기록; 후속 확인 DB 담당. |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-097266cd73b44f92) | Demo 메타데이터 3/3개 확인 · 2026-11-11 |
| 브라우저 화면·배포 환경 | 로컬 인증 계정·Playwright CLI; [화면별 검증표](../../references/browser-verification.md#page088) | 화면 대조, 2026-11-09. 배포본·타 역할·업무 변경 결과는 미확인. |
| 업무 프로시저·쓰기·외부 결과 | 격리된 검증 환경·테스트 데이터의 실행 결과 | 미확인: 명시적인 저장·삭제·발송·초기화 요청은 실행하지 않음. 브라우저 GET의 업무 조회 프로시저·조회수·감사 기록은 별도 영향으로 구분. 격리 환경에서 기술 담당 확인. |

코드 확인과 DB 정의 확인은 실행 성공·업무 승인·다른 환경 적용을 보장하지 않는다. 업무·기술 담당 검토 후 조사 목록의 상태를 완료로 변경한다.

브라우저 직접 근거: [settled-detail-revisit](../../evidence/browser/ready-details-stable.json). 경로·고정 버튼명·입력 속성·표 머리글·API 상태를 보관했고 실제 데이터 값·식별자·인증정보는 제외했다.

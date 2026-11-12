# 전체 페이지 매뉴얼 전수 대조 2026-11-12

현재 SmartWork <code>b923849c5</code>를 기준으로 <code>docs/page-work-inventory</code> 작업본을 검사했다. 이전 기준 <code>dc216b313</code> 이후 커밋 13개를 대조했다. [전체 매뉴얼 목차](../inventory/all-pages.md) · [433개 화면별 검증표](../inventory/all-pages-audit-2026-11-12.csv)

## 전수 검사 결과

| 검사 항목 | 범위와 결과 |
| --- | --- |
| 메뉴와 경로 | 메뉴 진입점 216개와 등록 라우트 437개는 이전 기준과 동일하다. 독립 업무 화면 433개가 문서에 한 개씩 연결된다. 메뉴 경로가 설정된 화면 425개의 문서와 목차에서 메뉴 표기가 일치한다. |
| 구성 일관성 | 433개 문서의 공통 7개 절, 필수 표의 열과 순서, 화면 경로, 도메인 소제목과 사용 절차 기재 여부를 확인했다. 리다이렉트 3개, 미구현 1개, 공통 404의 사유도 확인했다. |
| API와 정적 권한 | 문서의 API 행 1,223개를 현재 Controller의 메서드·경로와 대조했다. 정적 권한 선언 1,104개 행의 액션이 일치한다. 동적 메뉴 권한과 배포 환경의 계정별 허용·거부는 별도 실행 검증 대상이다. |
| 링크 | 페이지에 있는 고유 소스 링크 6,634개와 페이지별 위키 링크 4,814개에서 파일·앵커·소스 줄 위치를 검사했다. |
| 최신 소스 반영 | 화면 코드 또는 연결된 API 파일이 달라진 59개 경로의 소스 근거를 확인했다. 절차나 계약 설명을 바꿔야 했던 26개 매뉴얼을 수정했다. |
| 개발·Demo DB | 기존 전수 조사 결과를 페이지에 유지했다. 변경 API에 연결되는 39개 객체의 메타데이터를 두 환경에서 읽기 전용으로 재확인했다. [이번 DB 대조](#latest-db) |

공통 메뉴 권한 검사는 권한 갱신 중 이미 허용된 같은 화면을 유지할 수 있다. 갱신 후 실제 접근과 작업 권한은 각 메뉴의 허용 조건을 따른다. [현재 메뉴 권한 가드](https://github.com/thebusinesson/smartwork/blob/b923849c5d878772e0de2b67becff0ae511f03b3/frontend/src/shared/components/MenuPermissionGuard.tsx)

## 이번에 수정한 매뉴얼

| 화면 | 수정 내용 |
| --- | --- |
| [연동업체 등록](../manuals/hub-vendor/vendor-management__new.md) | 연동업체 등록의 사업자번호 입력 형식 |
| [차세대 연동업체 등록](../manuals/hub-vendor/nextgen-vendor-management__new.md) | 연동업체 등록의 사업자번호 입력 형식 |
| [연동플랫폼 통합관리](../manuals/hub-vendor/platform-management.md) | 라우팅 검색의 영업상품 전체 옵션 |
| [연동플랫폼 통합관리 상세](../manuals/hub-vendor/platform-management__system-port__by-portId.md) | 시스템 포트 JSON 통합 저장과 상세정보 행별 등록·수정·삭제·첨부삭제 |
| [OpenAPI 허브 관리 상세](../manuals/hub-vendor/openapi-hub-management__by-hubId.md) | 오픈스크랩 부서사용자 조회 설정 추가 |
| [일별 이용료 발행](../manuals/billing-management/daily-usage-fee-billing.md) | 청구 업체 행 표시 |
| [영수 대량 발행](../manuals/billing-management/bulk-receipt-issue.md) | 영수 대량 발행의 순차 처리와 별도 진행 창 |
| [회원 정보 상세](../manuals/member-management/member__by-id.md) | 회원 상세의 상담용 복사와 조회·수정 권한 구분 |
| [회원 이메일 다운로드](../manuals/member-management/email-download.md) | 회원 이메일 초기 조건·EDM 반출 컬럼·서버 제한 |
| [회사 정보](../manuals/company-management/company-info.md) | 회사 목록 자동이체 이력 팝업과 관련 API 2개 |
| [회사 정보 상세](../manuals/company-management/company-info__by-id.md) | 자동이체 이력의 신청 유형과 서명값 |
| [WEB 자료실 상세](../manuals/customer-support/web-resources__by-id.md) | 게시글 단건 SQL과 작성자 본인 수정 조건 |
| [WEB 자료실 수정](../manuals/customer-support/web-resources__by-id__edit.md) | 게시글 단건 SQL과 작성자 본인 수정 조건 |
| [SAP 자료실 상세](../manuals/customer-support/sap-resources__by-id.md) | 게시글 단건 SQL과 작성자 본인 수정 조건 |
| [SAP 자료실 수정](../manuals/customer-support/sap-resources__by-id__edit.md) | 게시글 단건 SQL과 작성자 본인 수정 조건 |
| [NSAP 자료실 상세](../manuals/customer-support/nsap-resources__by-id.md) | 게시글 단건 SQL과 작성자 본인 수정 조건 |
| [NSAP 자료실 수정](../manuals/customer-support/nsap-resources__by-id__edit.md) | 게시글 단건 SQL과 작성자 본인 수정 조건 |
| [WEB 문의 가이드 상세](../manuals/customer-support/web-inquiry-guide__by-id.md) | 게시글 단건 SQL과 작성자 본인 수정 조건 |
| [WEB 문의 가이드 수정](../manuals/customer-support/web-inquiry-guide__by-id__edit.md) | 게시글 단건 SQL과 작성자 본인 수정 조건 |
| [SAP 문의 가이드 상세](../manuals/customer-support/sap-inquiry-guide__by-id.md) | 게시글 단건 SQL과 작성자 본인 수정 조건 |
| [SAP 문의 가이드 수정](../manuals/customer-support/sap-inquiry-guide__by-id__edit.md) | 게시글 단건 SQL과 작성자 본인 수정 조건 |
| [NSAP 문의 가이드 상세](../manuals/customer-support/nsap-inquiry-guide__by-id.md) | 게시글 단건 SQL과 작성자 본인 수정 조건 |
| [NSAP 문의 가이드 수정](../manuals/customer-support/nsap-inquiry-guide__by-id__edit.md) | 게시글 단건 SQL과 작성자 본인 수정 조건 |
| [연동업체 소스 관리 상세](../manuals/customer-support/vendor-source-management__by-id.md) | 게시글 단건 SQL과 작성자 본인 수정 조건 |
| [연동업체 소스 관리 수정](../manuals/customer-support/vendor-source-management__by-id__edit.md) | 게시글 단건 SQL과 작성자 본인 수정 조건 |
| [소스 관리](../manuals/source-management/source-management.md) | 소스 관리 종료일 경계와 별도 카운트 호출 제거 |

## 실행 확인과 남은 항목

- 변경 기능의 기존 프런트엔드 테스트 67건과 서버 테스트 45건이 통과했다. 프런트엔드 동시 실행에서 시간 초과된 회원 이메일 테스트는 단독 재실행에서 통과했다. 서버는 앱 모듈을 지정해 재실행했다.
- 브라우저 관찰은 11월 11일의 표본 범위를 그대로 기록한다. 이번 대조에서 전 화면의 실제 사용 절차와 배포 계정별 권한, 저장·삭제·발송 결과는 재현하지 않았다. [기존 화면 표본](../evidence/browser/all-pages-sample-2026-11-11.json) · [등록 화면 표본](../evidence/browser/all-pages-accuracy-2026-11-11.json)
- 제각 결과의 개별·업로드 화면과 계정 관리의 등록·수정 화면은 공용 구현에서 해당 모드에 쓰는 호출을 따로 확인했다. 프로젝트 완료 관리의 연동 요청과 청구 등록은 프런트엔드에 호출 선언이 있으며 현재 서버에서 대응 Controller가 확인되지 않는다. [프로젝트 완료 관리](../manuals/hub-collab/project-completion.md)

### 역할·저장·삭제·발송 추가 검증

2026-11-12에 위 소스 기준으로 프런트엔드 6개 파일 58건과 백엔드 8개 클래스 58건을 실행했고 모두 통과했다. 아래 항목은 해당 테스트의 확인 범위다.

| 항목 | 테스트에서 확인한 결과 | 배포 환경에서 확인할 항목 |
| --- | --- | --- |
| 역할과 권한 | 메뉴 권한에 따른 접근 허용·거부와 비로그인 요청 차단을 확인했다. 고객지원 게시판 7종에서 작성자와 처리 권한을 함께 검사하며, 비작성자는 `SUPER_ADMIN`, `ADMIN`, `USER` 모두 게시글 수정과 첨부 교체가 거부됐다. 근거는 `MenuPermissionGuard.test.tsx`, `MenuPermissionAspectTest`, `AdminSpfBoardEditingHttpTest`다. | 실제 계정에 배정된 그룹과 작업별 권한으로 메뉴 진입 및 API 허용·거부 재현 |
| 저장·삭제 | 공지 팝업 설정을 임시 JSON 파일에 저장·수정한 뒤 다시 읽고 삭제 결과를 확인했다. 플랫폼 상세 정보와 첨부의 저장·삭제 호출은 테스트용 저장소 대역으로 검증했다. 근거는 `NoticeFileServiceTest`, `PlatformMgmtDetailInfoGuardTest`다. | SQL Server 기반 기능의 실제 반영 및 재조회. 격리 DB와 테스트 데이터 필요 |
| 발송·발행 | 서비스 공지 메일의 큐 전달 요청과 일부 실패 및 이력 저장 실패 시 동작, 영수 대량 발행의 실패 처리와 중복 발행 방지 분기를 테스트용 외부 연계 대역으로 확인했다. 근거는 `ServiceNoticeMailServiceTest`, `MailFunctionPublisherTest`, `BulkReceiptIssueProcessorTest`다. | 테스트 수신함 도착 및 외부 발행 결과. 테스트 수신 주소와 외부 연계 검증 환경 필요 |

### 운영 절차 추가 검수

- 433개 문서의 경로·양식·링크와 API 1,223개 행, 정적 권한 1,104개 행을 재검사해 오류 0건을 확인했다.
- 로컬 검증 계정 1개로 사이드바 메뉴 11개에 진입을 시도했다. 9개는 진입했고, 그중 8개에서 문서의 화면 표기를 관찰했다. 프로젝트 완료 관리와 연동플랫폼 통합관리는 메뉴 진입 미확인이다. 프로젝트 완료 관리에 비로그인 상태로 직접 진입하면 로그인 화면으로 이동했다. 로그인 후 주소 직접 진입을 시작할 때 인증 갱신이 401을 반환해 이 방식으로 시도한 13개 화면은 표시를 확인하지 못했다. [Playwright 기록](../evidence/browser/all-pages-review-2026-11-12.json) · [화면별 검증 CSV](../inventory/all-pages-audit-2026-11-12.csv)
- 프로젝트 완료 관리에서 반출 사유 입력 절차를 소스와 맞췄다. 대응 Controller를 확인하지 못한 **연동 요청**과 **빌링등록 요청**은 기술 담당 확인이 필요한 작업으로 안내했다. [프로젝트 완료 관리 매뉴얼](../manuals/hub-collab/project-completion.md)
- 개발·Demo에서 본문 해시가 달랐던 23개 정의를 다시 비교했다. 줄바꿈과 줄 끝 공백을 정리한 텍스트 기준으로 7개가 일치했고, 16개에는 추가 텍스트 차이가 남았다. 별도로 테이블 2개의 컬럼 구성 차이가 확인됐다. 실행 영향은 해당 업무·DB 담당 확인이 필요하다. `SB_BILL_LINKED` 객체 2개는 Demo 시스템 카탈로그에서 재조회했으나 현재 계정으로 메타데이터를 확인하지 못했다. [Demo DB 재조회](all-pages-demo.md#추가-확인이-필요한-객체)
- 실제 계정별 권한은 권한 운영 담당, 업무 데이터 변경과 외부 처리 결과는 격리된 검증 환경에서 기능 담당, 매뉴얼 업무 절차의 최종 확인은 메뉴별 운영 담당이 확인해야 한다. 인벤토리의 **검토 대기**는 운영 담당자 검수 상태다.

<a id="latest-db"></a>

## 변경 API의 개발·Demo DB 대조

mssql-onprem 설정으로 sqlcmd를 직접 호출하고 서버 지정 직후 <code>-C</code>를 적용했다. 개발·Demo 시스템 카탈로그의 객체 유형·파라미터·컬럼·본문을 확인했다. 본문은 해시를 비교했다. 본문 해시 차이는 SQL 동작 차이를 확정하지 않는다. 고객 데이터 조회·업무 프로시저 실행은 확인 범위 밖이다.

| DB 객체 | 개발 본문 SHA-256 또는 객체 정보 | Demo 본문 SHA-256 또는 객체 정보 | 대조 결과 |
| --- | --- | --- | --- |
| <a id="db-078d762f5e67"></a> <code>office.dbo.notice</code> | USER_TABLE · 컬럼 8개 | USER_TABLE · 컬럼 8개 | 확인 범위 일치 |
| <a id="db-3a9ea6e368df"></a> <code>office.dbo.sawon</code> | USER_TABLE · 컬럼 18개 | USER_TABLE · 컬럼 18개 | 확인 범위 일치 |
| <a id="db-0784238d81a8"></a> <code>office.dbo.upgw_deptinfo</code> | 7744169c74e0ee2edfe9239533d475c4c185651c0d654b8185a09933b2797a48 | 7744169c74e0ee2edfe9239533d475c4c185651c0d654b8185a09933b2797a48 | 확인 범위 일치 |
| <a id="db-cf96b331fbc4"></a> <code>office.dbo.upgw_savesrcmng</code> | 069c04e2385968ec4ba7ec8b4c9d1fec4aae4ab3441233a640bc77acc085b684 | 5553c09820c98838c7661c692669e0e27b6db42c60ec358dab7dcc96dbefdc93 | 본문 해시 차이 |
| <a id="db-9d4cccdc488d"></a> <code>office.dbo.upgw_sawonlist</code> | bc32c7fa976fdf5df3620b596f4c138fbf030496853d888e4d49014a9af7ed53 | bc32c7fa976fdf5df3620b596f4c138fbf030496853d888e4d49014a9af7ed53 | 확인 범위 일치 |
| <a id="db-00c0df29388b"></a> <code>office.dbo.upgw_selectsrcmng</code> | a24df4771aeeefcc61af0d3f7ef64c6bd7c234941bf5f95311cc23818a06d6a7 | 63db6ee284b54ada9c2f4a207a161f1ce2e4640a7335bcb8766a6e4868388bad | 본문 해시 차이 |
| <a id="db-df847a6e511c"></a> <code>office.dbo.upgw_srclist</code> | 4a57bfb387fe3345c19dfb59e7b7cd95b8dc2673d80266960875012d80f08cde | 584e4071ac127446f17dbb7a1a19dd0336d02e49d94b9615e6b550899459e7ff | 본문 해시 차이 |
| <a id="db-6d802d502932"></a> <code>office.dbo.upmg_remove_attachfile_distribution_info</code> | 24a0a4a50f8057860ed88db10e7808acc1af2cc19777a46ead48c563d05f09c8 | 746bd1a5353be96835caf795fe515a60fc54f8dfddcd19e2e966ced421f0c9cd | 본문 해시 차이 |
| <a id="db-6faa3dbbe2b6"></a> <code>office.dbo.upmg_remove_each_distribution_info</code> | 2106b2e042df8f4ed19043ce98956b26d473b54feadd1d92e77150b38734d07f | d7d12356c5a7f33ae89a568d0884e315b2d4abfa8204c3c64e7527a9a2cc1ef7 | 본문 해시 차이 |
| <a id="db-5fd2baea1ee3"></a> <code>office.dbo.upnt_delnotice</code> | c7a8ff2da8efda13f56350c27b488369921a098655e60e7af40bf17493fa97b8 | c7a8ff2da8efda13f56350c27b488369921a098655e60e7af40bf17493fa97b8 | 확인 범위 일치 |
| <a id="db-be59e8d29564"></a> <code>office.dbo.upnt_delnotireply</code> | bdac0e06b6a2ff62724b2d386846100a44700b8aa55b0572ad21d8c65f0d6c46 | bdac0e06b6a2ff62724b2d386846100a44700b8aa55b0572ad21d8c65f0d6c46 | 확인 범위 일치 |
| <a id="db-03417e7cc054"></a> <code>office.dbo.upnt_lstnotice</code> | 6d26b3d1ccfa74f900c4388fd1d9b549ebb0ae415cbc0b7af8299ea76dea46e8 | 6d26b3d1ccfa74f900c4388fd1d9b549ebb0ae415cbc0b7af8299ea76dea46e8 | 확인 범위 일치 |
| <a id="db-63503326a1b1"></a> <code>office.dbo.upnt_lstnotireply</code> | 8724cbc4fbbbbcd023139e39ce4fd9c972f986c05a0eee8f5d8966778d8a1c29 | 8724cbc4fbbbbcd023139e39ce4fd9c972f986c05a0eee8f5d8966778d8a1c29 | 확인 범위 일치 |
| <a id="db-c00c3f1d8bbf"></a> <code>office.dbo.upnt_modnotice</code> | dd71be7d88999b823424610ed87453b0732b8ebad18ae6ef336313c64ae37b1a | dd71be7d88999b823424610ed87453b0732b8ebad18ae6ef336313c64ae37b1a | 확인 범위 일치 |
| <a id="db-5c4581f8c53f"></a> <code>office.dbo.upnt_savnotireply</code> | 432008c7890be2d83b575017f10c622b44bf758500bd9ff8288eba39a1c5304b | 432008c7890be2d83b575017f10c622b44bf758500bd9ff8288eba39a1c5304b | 확인 범위 일치 |
| <a id="db-f0734d0d95ac"></a> <code>office.dbo.upnt_uphitnotice</code> | 8d6caa51b66e5f06ce686e66095623dc589fd0305d81905602d54ea6d8cf141d | 8d6caa51b66e5f06ce686e66095623dc589fd0305d81905602d54ea6d8cf141d | 확인 범위 일치 |
| <a id="db-6275815456e1"></a> <code>office.dbo.upsw_modifyhubdetail_info</code> | 37dd6c59b2a58c7c2ff31ae466de703f17b6ab455a972aa24756366b058c07cd | b2edca8203aa7d42afb553835e95eff450124e7c3ee7d7d50287b4c671f88ab2 | 본문 해시 차이 |
| <a id="db-63a5f1274544"></a> <code>office.dbo.upsw_removehub_engineer_info</code> | c91f1b5b981d56948b1beb1f1b15b99108e646b2bdf2f65734b0c450cac84ac9 | 077c56921bd00d24d3385e86ba21482854415213fa91bc323760246d1dc2dc2d | 본문 해시 차이 |
| <a id="db-cfba18f9a967"></a> <code>office.dbo.upsw_savehub_engineer_info</code> | 4ba5fe81f484badcd0efeaa01edd0de22734ff5f19c56e765ce03adf71d4607b | 4ba5fe81f484badcd0efeaa01edd0de22734ff5f19c56e765ce03adf71d4607b | 확인 범위 일치 |
| <a id="db-eea33b196fc7"></a> <code>office.dbo.upsw_savehubdetail_info</code> | 041732c1c5f5fd61b5b1fd6f9d6fabe0e5a97ce853ce8b2a2d6a47c2353b83dd | f62380102f13398be075cfd96bcc82efba8860ddd11f9aada48ac99bfd41e356 | 본문 해시 차이 |
| <a id="db-71ef10f09b8b"></a> <code>office.dbo.upsw_savehuberpdetail</code> | 9d7897455773ff2e93ddff3aff87b7a81ec8a24ec6c182d020c0214ab4f32bcf | a8d68843d271da57ad9af8e402b4282dfa71acff2981d25a525ac6c03a63fe9f | 본문 해시 차이 |
| <a id="db-55aa7a70e571"></a> <code>office.dbo.upsw_saveroutingurl_detail</code> | fc67685b3d600f3d55aef110102efabe9ee5288a97b928e17b0765fcc0c45d23 | 1b98c28c0cbac50cec16f1a520e4031247943f7a29e470aec01b62729d2b6fe7 | 본문 해시 차이 |
| <a id="db-4e572295acdb"></a> <code>sb_bill.dbo.taxinvoice_control</code> | USER_TABLE · 컬럼 19개 | USER_TABLE · 컬럼 17개 | 컬럼 차이 |
| <a id="db-d087c7c6aa32"></a> <code>sb_common.dbo.upsbadm_del_dti</code> | 797d787106c52ccf460b2bdb3198d97ce2bfd77078e6bc0e6a2372f554cbb43a | 797d787106c52ccf460b2bdb3198d97ce2bfd77078e6bc0e6a2372f554cbb43a | 확인 범위 일치 |
| <a id="db-9b704ca2245f"></a> <code>sb_dti.dbo.dti_header_cub</code> | 71fdbaac60ba2e6fe8cd7eb4be663e177bcb435f2e4ed7a2ace2478ed250cf3d | 339d9913996270a2f6f7597fb606e8e7112f295d85a02185f7abd0ff8e35676f | 본문 해시 차이 |
| <a id="db-9042ff61b257"></a> <code>smartbill3.dbo.member</code> | USER_TABLE · 컬럼 23개 | USER_TABLE · 컬럼 24개 | 컬럼 차이 |
| <a id="db-4a78d6d98e21"></a> <code>smartbill3.dbo.upcms_lsteachcms</code> | 2d4a2f54ba85d52956de9d440ee704838b2c27fa93f9e1214031463ab15108a0 | 0931045d3189c57f7267a4c7ce5190a96f0b28619c393ef552f9b401ff6e609a | 본문 해시 차이 |
| <a id="db-bb15bafea21f"></a> <code>smartwork.dbo.spf_board_attachment_meta</code> | USER_TABLE · 컬럼 6개 | USER_TABLE · 컬럼 6개 | 확인 범위 일치 |
| <a id="db-c2e5fd5251bf"></a> <code>smartwork.dbo.usp_platform_mgmt_detail_relays_select</code> | 1223745391eabfc25ccba868ed4792c366ef7444685a5acce5432166b5c67ad2 | d2d68b8d78363fc9b836d4e5e27239f4f6e6679ae81ac8d068e3bcc081fa437c | 본문 해시 차이 |
| <a id="db-474a028cea9d"></a> <code>smartwork.dbo.usp_platform_mgmt_import_history_exec</code> | f5d43f3f05f51cab2897d1bf884862e6510bd614e588ec251aad2df45746766e | 6644d4b8fa50195e5a2a8af3fc7091d329d613c60520033fca8dfbe6fe326e6b | 본문 해시 차이 |
| <a id="db-575acc66425e"></a> <code>smartwork.dbo.usp_platform_mgmt_port_detail_access_select</code> | 049d5fc8127ede957706d1d4ffbed34784c59006b473e28f959633d92ead2897 | 39b8dfe7af55c99161fde994594e8b595394fa6201ca69f2ac81798b3ff0ce3f | 본문 해시 차이 |
| <a id="db-42bf88d0df14"></a> <code>smartwork.dbo.usp_platform_mgmt_port_detail_contacts_select</code> | 6168c4d4668fe7df84a0f4a18ea5fedb94af944c250d13c96cf97a255670a01d | 348bf331541ab6b8f32d70160b220d5ac2ac88a3bff3d6b8a903f1df27bf8fc7 | 본문 해시 차이 |
| <a id="db-03caf5dfb3a6"></a> <code>smartwork.dbo.usp_platform_mgmt_port_detail_erp_select</code> | 9bca53e35eb5bac03631bd62105d24ceeeb5bd218cf836f899595c0b801ce13e | 1efb0eb6f8567794dc925083c2ca2f487df5ba6e01715ffcbdc059489538d0bf | 본문 해시 차이 |
| <a id="db-2e3226077b04"></a> <code>smartwork.dbo.usp_platform_mgmt_port_detail_info_select</code> | 6caf2979c3e9373100393f00dc51b639cd4d8d6ceb2e992c505e21fc27b3cc4c | 7b28703646963fce5858551abde6abd4d45019db88e69b343b4436194d658002 | 본문 해시 차이 |
| <a id="db-f827772d5683"></a> <code>smartwork.dbo.usp_platform_mgmt_port_detail_ports_select</code> | 20cbf77a5fdb9ec6636c27aaee29986afd4aaced35da6e41f533786bcc0ec784 | 81d0d0a4f4429215bac9ffcd399b613bedf61e83d4533fdebec20bb1036dd180 | 본문 해시 차이 |
| <a id="db-fb0ec1391eab"></a> <code>smartwork.dbo.usp_platform_mgmt_port_detail_sap_select</code> | d57a34c849f37802c8c208621e79fea35d11040f7e25d84d471fe73383196369 | 1892f28cd58e1e1c3342a593e00c17add38fc72387c6c42631dc45a6d873bfab | 본문 해시 차이 |
| <a id="db-9690a307d7dc"></a> <code>smartwork.dbo.usp_platform_mgmt_sap_insert</code> | 5097f250a08b41be4b7e5f9f50f199a7a2379fbe7e49e33b0f54d12dd1ee9f0d | 0079b3ec11e18e1b8da8a223108d1c6db1bf02300c93f3453117e572e453539b | 본문 해시 차이 |
| <a id="db-e7ee81277c6d"></a> <code>smartwork.dbo.usp_platform_mgmt_sap_remove_all</code> | 0174c5b60befd324888b4f0bf38c95aef741e19c6dc4c363e77c4672b159f897 | 6c1a23e7d967692a50339a8b1917b8d0ef681e68cbe2ab17528c61a9d9e3adab | 본문 해시 차이 |
| <a id="db-b7ba94e0cc2f"></a> <code>smartwork.dbo.usp_sw_log_access_event_insert</code> | 47c3cb42f57d188d1e1e89cc9baa92e95246aaf835488e3106b8a6aa19666491 | 8b8012919e96b1dc27106f808f98e5f210cd6157d46480503f4c7a75e6c96b40 | 본문 해시 차이 |

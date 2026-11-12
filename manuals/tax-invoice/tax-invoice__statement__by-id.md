# [SB 서비스관리] 세금계산서 조회 ((단독) 거래명세서 상세) 관리자 매뉴얼

작성 기준: `dc216b313` · 확인일 2026-11-09 · 조사 상태 **검토 대기**. 코드·개발 DB 정의 확인. 브라우저: **화면 대조**; 저장·발송 등 업무 실행 결과는 미검증이다.

## 1) 화면 기본 정보

### 도메인 이해

현행 조회에 등록된 독립 거래명세서 미리보기 경로의 표시 내용을 확인하는 화면이다.

| 구분 | 설명 |
|---|---|
| 업무 영역 | 전자세금계산서·거래명세서 운영 > 세금계산서 조회 (단독) 거래명세서 상세 |
| 언제 사용하는가 | 해당 독립 경로의 사용 여부·표시 내용과 목록의 문서 이동 방식을 대조할 때 |
| 주요 대상·데이터 | 이 컴포넌트는 숫자 id로 세금계산서 상세 API를 재사용해 거래명세서 미리보기·연락처를 표시한다. |
| 업무 흐름 | 독립 경로·조회 대상 확인 → 미리보기·연락처 또는 오류 확인 → 원래 목록 복귀 |
| 이 페이지의 역할 | 현행 거래 문서 중 **세금계산서 조회 (단독) 거래명세서 상세** 단계. 현행 조회에 등록된 독립 거래명세서 미리보기 경로의 표시 내용을 확인하는 화면이다. |
| 판단 결과·다음 업무 | 표시된 문서 종류와 실제 조회 계약을 함께 확인한다. 파일 다운로드 핸들러는 미구현 상태이므로 반출 완료 단계로 안내하지 않는다. |
| 다른 화면과의 구분 | 일반 목록의 공통 상세에 document=transaction-statement를 붙이는 분기와 같은 경로가 아니다. 단독 거래명세서 전용 API를 사용한다고 해석하지 않는다. |

설명 근거: [StatementDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/StatementDetailPage.tsx), 이 문서 4·5·7번의 항목·API·업무 규칙. [상위 업무 영역](../../references/domain-overview.md#invoice)은 공통 배경이며 현재 화면의 데이터·동작은 위 설명을 따른다. 설명 수정일 **2026-11-10**; 새 업무 실행 검증을 수행한 것은 아니다.

### 화면 정보

| 항목 | 작성 내용 |
|---|---|
| 업무 도메인·목적 | 현행 조회에 등록된 독립 거래명세서 미리보기 경로의 표시 내용을 확인하는 화면이다. |
| 메뉴·화면 경로 | SB 서비스관리 > 전자세금계산서 > 세금계산서 조회; `/tax-invoice/tax-invoice/statement/:id`; 목록에서 선택한 대상의 경로 변수를 유지하여 진입한다. |
| 화면 유형·담당 | (단독) 거래명세서 상세; WBS 작업자 유지윤. 업무·기술 담당 팀명은 원문에 없어 배포 전 해당 도메인 담당자가 확정한다. |
| 관련 화면 | [조회·관리](tax-invoice.md); [상세](tax-invoice__by-id.md) |

WBS 근거: No. 43, 44, 45, 46, 47 (사용자가 제공한 텍스트 행 69, 70, 71, 72, 73). API 개발/화면 개발의 중복 행은 같은 화면으로 통합했다.

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
|---|---|---|
| 화면 진입·조회 | `/tax-invoice/tax-invoice` 메뉴 접근·하위 경로 작업 권한. 조회 API는 VIEW, 등록/수정 경로는 PROCESS 등 아래 서버 액션과 라우트 가드를 함께 적용한다. | 로그인된 관리자 계정; id 식별자는 이전 화면에서 선택한다. |
| 목록으로 돌아가기 | `/tax-invoice/tax-invoice`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 목록 | `/tax-invoice/tax-invoice`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |

서버가 최종 권한을 검사한다. 버튼 모양(kind)으로 권한을 추정하지 않는다. 특히 등록·수정이 PROCESS를 사용하는 API와 EXECUTE·UNMASK·EXCEL_DOWNLOAD는 서로 구분한다.

## 3) 화면 사용 절차

1. 이 독립 경로는 등록된 화면이지만 현재 목록의 일반적인 상세 진입 경로와 다르다. 일반 목록에서 실제 선택한 문서와 연결된 상세 링크를 우선 사용한다.
2. 코드상 이 화면은 `id`를 숫자로 변환해 세금계산서 상세 API를 호출하고 거래명세서 미리보기로 표시한다. 단독 거래명세서 전용 조회 API를 호출하는 화면이라고 해석하지 않는다.
3. 조회가 성공하면 미리보기와 연락처를 확인하고 **목록**으로 돌아간다. 조회 실패 시 **목록으로 돌아가기**를 사용한다.
4. 이 컴포넌트의 다운로드 핸들러는 로그만 남기는 TODO 상태이며 XML 다이얼로그를 여는 상태 변경도 연결되어 있지 않다. 이 경로에서 XML·뷰어·전자세금계산서 파일이 다운로드된다고 안내하지 않는다. 실제 파일 반출은 지원되는 공통 상세 화면에서 권한·지원 여부를 확인한다.

**진입 경로 구분**: 현재 세금계산서 목록은 공통 상세 `/:id`에 `wday`, `arap`을 전달하고 거래명세서이면 `document=transaction-statement`를 추가한다. 독립 `statement/:id` 경로를 이 분기와 동일하다고 단정하지 않는다. 과거 목록의 진입·별칭은 해당 라우트 소스를 함께 확인한다. 업무 담당·프런트 담당이 독립 경로의 사용 여부와 표기 의미를 검토해야 한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
|---|---|---|---|
| 화면 표시·작업 입력 | 복합 컴포넌트 | 세부 항목은 [StatementDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/StatementDetailPage.tsx)의 구성 요소·검증 규칙과 API 계약 표 참조 | 정적으로 추출한 고정 label/key 쌍 없음. 업무 담당 화면 검토 필요 |

화면 필드 키와 API 필드명이 다른 경우 변환은 Hook/API의 검색·저장 매핑에서 수행된다. 요청·응답 필드와 DB 컬럼 매핑은 아래 API 계약 및 DB 객체 계약에 연결했다.

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
|---|---|---|---|
| 세금계산서 상세 조회 | [GET /api/v1/tax-invoices/{id}/detail](../../references/api-contracts.md#api161); `/tax-invoice/tax-invoice` / `VIEW` | `경로·쿼리·본문 계약 참조` → `invoice, xmlDownloadAvailable, buyType, contactInfo, issuanceInfo, emailHistory, attachmentInfo, attachmentHistory, documentHistory, multiLinkInfo, linkedStatement, currentAttachme` | Mapper 프로시저의 정적 테이블 쓰기 미검출; 동적 SQL의 런타임 대상은 미확정 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
|---|---|---|---|
| [SB_DTI.dbo.upCHK_ClosingStampTemp](../../references/database-contracts.md#db145) | `@SUP_MEM_NO varchar(10) IN, @BYR_MEM_NO varchar(10) IN, @BRK_MEM_NO varchar(10) IN, @DTI_WDAY varchar(10) IN, @BRK_DTI_YN varchar(1) IN, @ISSUCCESS bit OUT` | 확정한 테이블 쓰기 없음. 참조: sb_dti.dbo.bizplace_member, sb_dti.dbo.dti_closing, smartbill3.dbo.member | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_Customize.dbo.upSEC_CodeInfo](../../references/database-contracts.md#db121) | `@COM_REGNO varchar(13) IN, @CODE varchar(20) IN, @CODE_TYPE varchar(20) IN` | 확정한 테이블 쓰기 없음. 참조: sb_customize.dbo.sec_code | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DTI.dbo.COMPANY_QUIT_STATUS](../../references/database-contracts.md#db138) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: sb_dti.dbo.company_quit_status | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DTI.dbo.DTI_SIGN](../../references/database-contracts.md#db140) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: sb_dti.dbo.dti_sign, sb_dti.dbo.dti_sign_cub, sb_dti.dbo.dti_sign_cub_2023_07, sb_dti.dbo.dti_sign_cub_part, sb_dti.dbo.dti_sign_cub_prev_buffer, sb_dti.dbo.dti_sign_xml, sb_dti.dbo.dti_sign_xml_2023_07, sb_dti.dbo.dti_sign_xml_part 외 1개 | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DTI.dbo.DTI_HEADER_CUB](../../references/database-contracts.md#db139) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: sb_dti.dbo.dti_header_cub, sb_dti.dbo.dti_header_cub_2023_07, sb_dti.dbo.dti_header_cub_part, sb_dti.dbo.dti_header_cub_prev_buffer | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DTI.dbo.DTT_HEADER_CUB](../../references/database-contracts.md#db141) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: sb_dti.dbo.dtt_header_cub, sb_dti.dbo.dtt_header_cub_2020_01, sb_dti.dbo.dtt_header_cub_2021_01, sb_dti.dbo.dtt_header_cub_2022_01, sb_dti.dbo.dtt_header_cub_2023_01, sb_dti.dbo.dtt_header_cub_bf, sb_dti.dbo.dtt_header_cub_part | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DTI.dbo.upSelect_DTI_STATUS_HIS](../../references/database-contracts.md#db152) | `@DIV varchar(10) IN, @DTI_WDAY varchar(10) IN, @DTI_IDX varchar(10) IN` | 확정한 테이블 쓰기 없음. 참조: sb_dti.dbo.dti_header_cub, sb_dti.dbo.dti_header_cub_2023_07, sb_dti.dbo.dti_header_cub_part, sb_dti.dbo.dti_header_cub_prev_buffer, sb_dti.dbo.dti_status_his, sb_dti.dbo.dti_status_his_2023_07, sb_dti.dbo.dti_status_his_part, sb_dti.dbo.dti_status_his_prev_buffer 외 2개 | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DTI.dbo.upSelect_MultiLinkInfo](../../references/database-contracts.md#db155) | `@CONVERSATION_ID varchar(35) IN` | 확정한 테이블 쓰기 없음. 참조: sb_dti_log.dbo.multi_link_his | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DTI.dbo.upSELECT_MailStatus](../../references/database-contracts.md#db154) | `@DTI_WDAY varchar(10) IN, @DTI_IDX int IN` | 확정한 테이블 쓰기 없음. 참조: sb_dti_log.dbo.dti_email_his, sb_dti_log.dbo.dti_email_rcv_his, sb_dti_log.dbo.dti_email_rcv_his_old, sb_dti_log.dbo.dti_email_rcv_his_part, sb_dti_log.dbo.dti_email_send_his, sb_dti_log.dbo.dti_email_send_his_old, sb_dti_log.dbo.dti_email_send_his_part | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DTI.dbo.upSelect_DTIChangeReceiverHis](../../references/database-contracts.md#db153) | `@DTI_WDAY char(10) IN, @DTI_IDX int IN` | 확정한 테이블 쓰기 없음. 참조: sb_dti.dbo.dti_header_cub, sb_dti.dbo.dti_header_cub_2023_07, sb_dti.dbo.dti_header_cub_part, sb_dti.dbo.dti_header_cub_prev_buffer, sb_dti_log.dbo.dti_change_receiver, sb_dti_log.dbo.dti_change_receiver_his, smartbill3.dbo.member | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DTI.dbo.ATTACH_FILE_INFO](../../references/database-contracts.md#db134) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: sb_dti.dbo.attach_file_info | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_COMMON.dbo.upSBAdm_QryEmailLog](../../references/database-contracts.md#db108) | `@ETC_PCS_NO varchar(35) IN` | 확정한 테이블 쓰기 없음. 참조: sb_dti.dbo.dti_email_send_his, sb_dti.dbo.dti_header_cub, sb_dti.dbo.dti_header_cub_2023_07, sb_dti.dbo.dti_header_cub_part, sb_dti.dbo.dti_header_cub_prev_buffer, sb_dti_log.dbo.dti_email_his, sb_dti_log.dbo.dti_email_send_his, sb_dti_log.dbo.dti_email_send_his_old 외 1개 | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_COMMON.dbo.upSBAdm_QryMemID](../../references/database-contracts.md#db110) | `@DTI_WDAY varchar(10) IN, @DTI_IDX int IN` | 확정한 테이블 쓰기 없음. 참조: sb_common.dbo.neobill_oapi_log_b2b, sb_dti.dbo.dti_header_cub, sb_dti.dbo.dti_header_cub_2023_07, sb_dti.dbo.dti_header_cub_part, sb_dti.dbo.dti_header_cub_prev_buffer, sb_dti.dbo.dti_header_detail, sb_dti.dbo.dti_header_detail_2020_01, sb_dti.dbo.dti_header_detail_2020_02 외 49개 | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DTI.dbo.upSelect_DTI_PAYMETHOD](../../references/database-contracts.md#db151) | `@DTI_IDX varchar(10) IN, @DTI_WDAY varchar(10) IN` | 확정한 테이블 쓰기 없음. 참조: sb_dti.dbo.dti_paymethod, sb_dti.dbo.dti_paymethod_2023_07, sb_dti.dbo.dti_paymethod_part, sb_dti.dbo.dti_paymethod_prev_buffer | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DTI.dbo.upSelect_DTI_ITEM](../../references/database-contracts.md#db150) | `@DTI_IDX varchar(10) IN, @DTI_WDAY varchar(10) IN` | 확정한 테이블 쓰기 없음. 참조: sb_dti.dbo.dti_item, sb_dti.dbo.dti_item_2023_07, sb_dti.dbo.dti_item_part, sb_dti.dbo.dti_item_prev_buffer | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DTI.dbo.upSelect_DTI_HEADER](../../references/database-contracts.md#db149) | `@DTI_IDX varchar(10) IN, @DTI_WDAY varchar(10) IN` | 확정한 테이블 쓰기 없음. 참조: sb_customize.dbo.sec_code, sb_dti.dbo.company_quit_status, sb_dti.dbo.dti_header_cub, sb_dti.dbo.dti_header_cub_2023_07, sb_dti.dbo.dti_header_cub_part, sb_dti.dbo.dti_header_cub_prev_buffer, sb_dti.dbo.dti_header_detail, sb_dti.dbo.dti_header_detail_2023_07 외 8개 동적 SQL 포함, 런타임 조합 대상 미확정. | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |

위 DB 계약 링크에는 실제 파라미터 타입·기본값·IN/OUT, Mapper 결과 컬럼, RETURN 바인딩, 참조 테이블·하위 프로시저·정의 필터/정렬을 기록했다. DTO·Service·Repository·Mapper의 상세 호출 경로는 각 API 계약에서 확인한다.

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
|---|---|---|
| 문서 이력이 없습니다. | [문구·처리 코드](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/StatementDetailPage.tsx#L152); 현재 조건·대상·권한 확인 | 검색·조회 오류면 조건을 확인 후 재조회. 변경·발송 결과가 불명확하면 처리 여부와 이력을 확인한 뒤 재시도 여부를 판단한다. |
| 결과가 없거나 기대 건수와 다름 | 적용된 검색 기준·기간·탭·대상 상태·서버 필터·페이징·목록/다운로드 조건 | 조건을 다시 확인하고 조회한다. 지속되면 경로·작업 시각·마스킹한 식별자·필터를 업무/기술 담당에게 전달한다. |
| 메뉴·버튼 미표시 또는 접근 거부 | 사용자 그룹의 메뉴 접근·VIEW 및 API별 PROCESS/EXECUTE/DELETE/EXCEL_DOWNLOAD/UNMASK 등 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. 프런트 버튼 표시만으로 서버 권한을 판단하지 않는다. |
| 저장·삭제·외부 실행의 결과가 불명확 | 대상 현재 상태·중복 요청·감사 이력·API 오류·파일/외부 소비 로그 | 기존 반영 여부를 먼저 조회한다. 중복 발송·초기화·금액 처리를 피하기 위해 기술 담당 확인 후 재시도한다. |

## 7) 검증·출처

**브라우저 검증(2026-11-09)**: 화면 대조. [경로별 결과와 제한](../../references/browser-verification.md#page017). 역할별 권한 거부·저장 성공·파일 반출·외부 연계 완료는 이 결과로 보장하지 않는다.

| 검증 항목 | 근거·환경 | 상태·확인일 |
|---|---|---|
| 대상 선정 | 사용자가 WBS 탭 내용으로 제공한 텍스트의 No. 43, 44, 45, 46, 47; [선정 태스크](../../inventory/wbs-tasks.csv) | 제공 텍스트 확인 2026-11-09. 원본 Excel의 탭/병합 셀을 독립 재열람한 것은 아님. |
| 메뉴·라우트·화면 | [menuConfig.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts); [TaxInvoiceRoutes.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/TaxInvoiceRoutes.tsx); [StatementDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/StatementDetailPage.tsx) | 코드 확인 2026-11-09, 기준 dc216b313 |
| 기능·권한·API | 이 문서의 API 계약 링크 및 연결 Hook/API·Controller·DTO·Service·Repository·Mapper | 코드 확인 2026-11-09. 조회 요청·화면 대조 범위는 아래 브라우저 근거 참조. 권한 계정별 허용·거부 및 변경 요청 실행은 미확인. |
| DB 정의 | [개발 DB 계약](../../references/database-contracts.md), 이 문서의 연결 객체 | 개발 DB 정의 확인 2026-11-09. 동적 SQL·CLR 내부·정의 미공개 참조의 미확정 범위는 객체별 기록; 후속 확인 DB 담당. |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-ad02464e94e34e14) | Demo 메타데이터 16/16개 확인 · 2026-11-11 |
| 브라우저 화면·배포 환경 | 로컬 인증 계정·Playwright CLI; [화면별 검증표](../../references/browser-verification.md#page017) | 화면 대조, 2026-11-09. 배포본·타 역할·업무 변경 결과는 미확인. |
| 업무 프로시저·쓰기·외부 결과 | 격리된 검증 환경·테스트 데이터의 실행 결과 | 미확인: 명시적인 저장·삭제·발송·초기화 요청은 실행하지 않음. 브라우저 GET의 업무 조회 프로시저·조회수·감사 기록은 별도 영향으로 구분. 격리 환경에서 기술 담당 확인. |

코드 확인과 DB 정의 확인은 실행 성공·업무 승인·다른 환경 적용을 보장하지 않는다. 업무·기술 담당 검토 후 조사 목록의 상태를 완료로 변경한다.

브라우저 직접 근거: [same-observed-invoice-id-independent-statement-route](../../evidence/browser/targeted-stable.json). 경로·고정 버튼명·입력 속성·표 머리글·API 상태를 보관했고 실제 데이터 값·식별자·인증정보는 제외했다.

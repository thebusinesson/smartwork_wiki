# [SB 서비스관리] 세금계산서 조회 (상세) 관리자 매뉴얼

작성 기준: `dc216b313` · 확인일 2026-11-09 · 조사 상태 **검토 대기**. 코드·개발 DB 정의 확인. 브라우저: **화면 대조**; 저장·발송 등 업무 실행 결과는 미검증이다.

## 1) 화면 기본 정보

### 도메인 이해

보나뱅크 구분으로 관리되는 회사·회원과 전자세금계산서 업무를 운영하는 영역이다. 고객 정보, 문서 현황, 국세청 신고 실패, 이용 통계와 공지를 함께 확인하되 현재 메뉴의 보나뱅크 범위를 유지한다.

| 구분 | 설명 |
|---|---|
| 업무 영역 | 보나뱅크 서비스 운영 · SB 서비스관리 > 보나뱅크 > 세금계산서 조회 |
| 주요 대상·용어 | 보나뱅크 회사·회원: 이 서비스 구분의 고객 정보 / 신고 실패: 국세청 관련 처리에서 실패로 분류된 내역 / 공지: 서비스 안내 게시물 |
| 업무 흐름 | 보나뱅크 고객 식별 → 회사·회원 또는 문서·통계 선택 → 상태·이력 확인 → 필요한 지원 작업 |
| 이 페이지의 역할 | 보나뱅크 거래 문서에서 선택한 한 대상의 상세 내용·상태·관련 이력을 확인하는 화면이다. 보나뱅크 범위의 세금계산서를 찾고 공통 상세와 연결해 문서 상태·내용을 확인한다. |
| 관련 업무와 구분 | 스마트빌 전체 고객 목록과 보나뱅크 목록은 범위가 다를 수 있다. 세금계산서 목록의 상세 이동은 공통 세금계산서 화면으로 연결되는 현재 구현을 따른다. |

도메인 설명 근거: 이 문서 7번의 현재 메뉴·라우트·화면 및 API·업무 규칙 소스. [전체 도메인 지도](../../references/domain-overview.md#bonabank). 설명 보강일 2026-11-09; 기존 실행 검증 범위와 미확인 상태는 변경하지 않았다.

### 화면 정보

| 항목 | 작성 내용 |
|---|---|
| 업무 도메인·목적 | 보나뱅크 세금계산서의 문서 상태와 상세 내용을 조회하고 재발송·다운로드를 수행한다. |
| 메뉴·화면 경로 | SB 서비스관리 > 보나뱅크 > 세금계산서 조회; `/bonabank/tax-invoice/:dtiIdx`; 목록에서 선택한 대상의 경로 변수를 유지하여 진입한다. |
| 화면 유형·담당 | 상세; WBS 작업자 유지윤. 업무·기술 담당 팀명은 원문에 없어 배포 전 해당 도메인 담당자가 확정한다. |
| 관련 화면 | [조회·관리](tax-invoice.md) |

WBS 근거: No. 142, 143 (사용자가 제공한 텍스트 행 178, 179). API 개발/화면 개발의 중복 행은 같은 화면으로 통합했다.

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
|---|---|---|
| 화면 진입·조회 | `/bonabank/tax-invoice` 메뉴 접근·하위 경로 작업 권한. 조회 API는 VIEW, 등록/수정 경로는 PROCESS 등 아래 서버 액션과 라우트 가드를 함께 적용한다. | 로그인된 관리자 계정; dtiIdx 식별자는 이전 화면에서 선택한다. |
| 목록 | `/bonabank/tax-invoice`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| XML 원본 다운로드 | `/bonabank/tax-invoice`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 거래명세서 보기 | `/bonabank/tax-invoice`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 세금계산서 보기 | `/bonabank/tax-invoice`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 닫기 | `/bonabank/tax-invoice`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 확인 | `/bonabank/tax-invoice`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 전자세금계산서 다운로드 | `/bonabank/tax-invoice`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| XML로 다운로드 | `/bonabank/tax-invoice`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 전용뷰어 다운로드 | `/bonabank/tax-invoice`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |

서버가 최종 권한을 검사한다. 버튼 모양(kind)으로 권한을 추정하지 않는다. 특히 등록·수정이 PROCESS를 사용하는 API와 EXECUTE·UNMASK·EXCEL_DOWNLOAD는 서로 구분한다.

## 3) 화면 사용 절차

**검증 시 화면 버튼**: 목록. 화면 상태·대상에 따라 달라지며 아래 작업 절차와 권한 조건을 함께 확인한다.

**현재 상세 이동**: `BonabankTaxInvoiceListPage`의 행 선택은 `/tax-invoice/tax-invoice/:id?wday=...` 공통 상세로 이동한다. `/bonabank/tax-invoice/:dtiIdx`도 라우트에 등록되어 있지만 현재 목록의 기본 진입 경로는 아니다. 실제 행에서 받은 문서 ID와 `wday`를 유지한다. 보나뱅크 상세 경로를 공통 상세와 별개로 검사한 결과는 검증표에서 구분한다.

1. 관련 화면에서 대상 또는 작업을 선택하여 `/bonabank/tax-invoice/:dtiIdx`로 이동한다. 경로 변수는 주소에서 임의로 바꾸지 않고 이전 화면이 전달한 식별자를 사용한다.
2. 대상의 기본 정보·상태·표시 항목을 확인한다. 목록의 식별자와 상세 대상이 일치하는지 확인한다.
3. **XML 원본 다운로드, 거래명세서 보기, 세금계산서 보기, 닫기, 확인, 전자세금계산서 다운로드, XML로 다운로드, 전용뷰어 다운로드** 중 필요한 작업을 선택한다. 버튼의 표시·활성 조건과 아래 API별 권한을 확인한다. 저장·삭제·외부 호출 전에는 대상과 현재 상태를 재확인한다.
4. 작업 결과 또는 다운로드 파일을 확인하고 관련 목록으로 돌아가 변경된 상태를 다시 조회한다.

**이 화면에서 유의할 업무 규칙**: 공급자 또는 공급받는자 조건 중 필요한 값을 입력하여 검색한다. 상세에서 문서·담당자·전송 정보를 확인하고 재발송 시 수신 이메일을 검증한다.

**반출**: 적용된 검색 조건과 반출 범위를 확인한 후 다운로드한다. 사유 입력창이 표시되면 업무 사유를 입력한다. 사유 등록 실패·파일 오류는 성공으로 간주하지 않고 다운로드 결과를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
|---|---|---|---|
| 화면 표시·작업 입력 | 복합 컴포넌트 | 세부 항목은 [BonabankTaxInvoiceDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/BonabankTaxInvoiceDetailPage.tsx)의 구성 요소·검증 규칙과 API 계약 표 참조 | 정적으로 추출한 고정 label/key 쌍 없음. 업무 담당 화면 검토 필요 |

화면 필드 키와 API 필드명이 다른 경우 변환은 Hook/API의 검색·저장 매핑에서 수행된다. 요청·응답 필드와 DB 컬럼 매핑은 아래 API 계약 및 DB 객체 계약에 연결했다.

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
|---|---|---|---|
| 보나뱅크 세금계산서 상세 (3 섹션) | [GET /api/v1/bonabank/tax-invoices/{dtiIdx}](../../references/api-contracts.md#api027); `/bonabank/tax-invoice` / `VIEW` | `경로·쿼리·본문 계약 참조` → `basicInfo, emailHistories, attachFiles, dtiIdx, writeDate, issueDate, ntsSendDate, supplierId, buyerId, supplierBusinessNumber, supplierCompanyName, buyerBusinessNumber, buyerCompa` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 세금계산서 상세 조회 | [GET /api/v1/tax-invoices/{id}/detail](../../references/api-contracts.md#api161); `/tax-invoice/tax-invoice` / `VIEW` | `경로·쿼리·본문 계약 참조` → `invoice, xmlDownloadAvailable, buyType, contactInfo, issuanceInfo, emailHistory, attachmentInfo, attachmentHistory, documentHistory, multiLinkInfo, linkedStatement, currentAttachme` | Mapper 프로시저의 정적 테이블 쓰기 미검출; 동적 SQL의 런타임 대상은 미확정 |
| downloadXml | [GET /api/v1/tax-invoices/{id}/xml](../../references/api-contracts.md#api164); `/tax-invoice/tax-invoice` / `VIEW` | `경로·쿼리·본문 계약 참조` → `응답 DTO·파일/처리 결과 계약 참조` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| downloadDti | [GET /api/v1/tax-invoices/{id}/dti](../../references/api-contracts.md#api162); `/tax-invoice/tax-invoice` / `VIEW` | `경로·쿼리·본문 계약 참조` → `응답 DTO·파일/처리 결과 계약 참조` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
|---|---|---|---|
| [SB_DTI.dbo.upSBAdm_QryDTIAttachFile_Info](../../references/database-contracts.md#db148) | `@ETC_PCS_NO varchar(35) IN` | 확정한 테이블 쓰기 없음. 참조: sb_dti.dbo.attach_file_info | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_COMMON.dbo.upSBAdm_QryEmailLog](../../references/database-contracts.md#db108) | `@ETC_PCS_NO varchar(35) IN` | 확정한 테이블 쓰기 없음. 참조: sb_dti.dbo.dti_email_send_his, sb_dti.dbo.dti_header_cub, sb_dti.dbo.dti_header_cub_2023_07, sb_dti.dbo.dti_header_cub_part, sb_dti.dbo.dti_header_cub_prev_buffer, sb_dti_log.dbo.dti_email_his, sb_dti_log.dbo.dti_email_send_his, sb_dti_log.dbo.dti_email_send_his_old 외 1개 | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_COMMON.dbo.upSBAdm_QryMemID](../../references/database-contracts.md#db110) | `@DTI_WDAY varchar(10) IN, @DTI_IDX int IN` | 확정한 테이블 쓰기 없음. 참조: sb_common.dbo.neobill_oapi_log_b2b, sb_dti.dbo.dti_header_cub, sb_dti.dbo.dti_header_cub_2023_07, sb_dti.dbo.dti_header_cub_part, sb_dti.dbo.dti_header_cub_prev_buffer, sb_dti.dbo.dti_header_detail, sb_dti.dbo.dti_header_detail_2020_01, sb_dti.dbo.dti_header_detail_2020_02 외 49개 | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DTI.dbo.DTI_HEADER_CUB](../../references/database-contracts.md#db139) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: sb_dti.dbo.dti_header_cub, sb_dti.dbo.dti_header_cub_2023_07, sb_dti.dbo.dti_header_cub_part, sb_dti.dbo.dti_header_cub_prev_buffer | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DTI.dbo.upCHK_ClosingStampTemp](../../references/database-contracts.md#db145) | `@SUP_MEM_NO varchar(10) IN, @BYR_MEM_NO varchar(10) IN, @BRK_MEM_NO varchar(10) IN, @DTI_WDAY varchar(10) IN, @BRK_DTI_YN varchar(1) IN, @ISSUCCESS bit OUT` | 확정한 테이블 쓰기 없음. 참조: sb_dti.dbo.bizplace_member, sb_dti.dbo.dti_closing, smartbill3.dbo.member | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_Customize.dbo.upSEC_CodeInfo](../../references/database-contracts.md#db121) | `@COM_REGNO varchar(13) IN, @CODE varchar(20) IN, @CODE_TYPE varchar(20) IN` | 확정한 테이블 쓰기 없음. 참조: sb_customize.dbo.sec_code | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DTI.dbo.COMPANY_QUIT_STATUS](../../references/database-contracts.md#db138) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: sb_dti.dbo.company_quit_status | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DTI.dbo.DTI_SIGN](../../references/database-contracts.md#db140) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: sb_dti.dbo.dti_sign, sb_dti.dbo.dti_sign_cub, sb_dti.dbo.dti_sign_cub_2023_07, sb_dti.dbo.dti_sign_cub_part, sb_dti.dbo.dti_sign_cub_prev_buffer, sb_dti.dbo.dti_sign_xml, sb_dti.dbo.dti_sign_xml_2023_07, sb_dti.dbo.dti_sign_xml_part 외 1개 | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DTI.dbo.DTT_HEADER_CUB](../../references/database-contracts.md#db141) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: sb_dti.dbo.dtt_header_cub, sb_dti.dbo.dtt_header_cub_2020_01, sb_dti.dbo.dtt_header_cub_2021_01, sb_dti.dbo.dtt_header_cub_2022_01, sb_dti.dbo.dtt_header_cub_2023_01, sb_dti.dbo.dtt_header_cub_bf, sb_dti.dbo.dtt_header_cub_part | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DTI.dbo.upSelect_DTI_STATUS_HIS](../../references/database-contracts.md#db152) | `@DIV varchar(10) IN, @DTI_WDAY varchar(10) IN, @DTI_IDX varchar(10) IN` | 확정한 테이블 쓰기 없음. 참조: sb_dti.dbo.dti_header_cub, sb_dti.dbo.dti_header_cub_2023_07, sb_dti.dbo.dti_header_cub_part, sb_dti.dbo.dti_header_cub_prev_buffer, sb_dti.dbo.dti_status_his, sb_dti.dbo.dti_status_his_2023_07, sb_dti.dbo.dti_status_his_part, sb_dti.dbo.dti_status_his_prev_buffer 외 2개 | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DTI.dbo.upSelect_MultiLinkInfo](../../references/database-contracts.md#db155) | `@CONVERSATION_ID varchar(35) IN` | 확정한 테이블 쓰기 없음. 참조: sb_dti_log.dbo.multi_link_his | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DTI.dbo.upSELECT_MailStatus](../../references/database-contracts.md#db154) | `@DTI_WDAY varchar(10) IN, @DTI_IDX int IN` | 확정한 테이블 쓰기 없음. 참조: sb_dti_log.dbo.dti_email_his, sb_dti_log.dbo.dti_email_rcv_his, sb_dti_log.dbo.dti_email_rcv_his_old, sb_dti_log.dbo.dti_email_rcv_his_part, sb_dti_log.dbo.dti_email_send_his, sb_dti_log.dbo.dti_email_send_his_old, sb_dti_log.dbo.dti_email_send_his_part | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DTI.dbo.upSelect_DTIChangeReceiverHis](../../references/database-contracts.md#db153) | `@DTI_WDAY char(10) IN, @DTI_IDX int IN` | 확정한 테이블 쓰기 없음. 참조: sb_dti.dbo.dti_header_cub, sb_dti.dbo.dti_header_cub_2023_07, sb_dti.dbo.dti_header_cub_part, sb_dti.dbo.dti_header_cub_prev_buffer, sb_dti_log.dbo.dti_change_receiver, sb_dti_log.dbo.dti_change_receiver_his, smartbill3.dbo.member | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DTI.dbo.ATTACH_FILE_INFO](../../references/database-contracts.md#db134) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: sb_dti.dbo.attach_file_info | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DTI.dbo.upSelect_DTI_PAYMETHOD](../../references/database-contracts.md#db151) | `@DTI_IDX varchar(10) IN, @DTI_WDAY varchar(10) IN` | 확정한 테이블 쓰기 없음. 참조: sb_dti.dbo.dti_paymethod, sb_dti.dbo.dti_paymethod_2023_07, sb_dti.dbo.dti_paymethod_part, sb_dti.dbo.dti_paymethod_prev_buffer | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DTI.dbo.upSelect_DTI_ITEM](../../references/database-contracts.md#db150) | `@DTI_IDX varchar(10) IN, @DTI_WDAY varchar(10) IN` | 확정한 테이블 쓰기 없음. 참조: sb_dti.dbo.dti_item, sb_dti.dbo.dti_item_2023_07, sb_dti.dbo.dti_item_part, sb_dti.dbo.dti_item_prev_buffer | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DTI.dbo.upSelect_DTI_HEADER](../../references/database-contracts.md#db149) | `@DTI_IDX varchar(10) IN, @DTI_WDAY varchar(10) IN` | 확정한 테이블 쓰기 없음. 참조: sb_customize.dbo.sec_code, sb_dti.dbo.company_quit_status, sb_dti.dbo.dti_header_cub, sb_dti.dbo.dti_header_cub_2023_07, sb_dti.dbo.dti_header_cub_part, sb_dti.dbo.dti_header_cub_prev_buffer, sb_dti.dbo.dti_header_detail, sb_dti.dbo.dti_header_detail_2023_07 외 8개 동적 SQL 포함, 런타임 조합 대상 미확정. | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |

위 DB 계약 링크에는 실제 파라미터 타입·기본값·IN/OUT, Mapper 결과 컬럼, RETURN 바인딩, 참조 테이블·하위 프로시저·정의 필터/정렬을 기록했다. DTO·Service·Repository·Mapper의 상세 호출 경로는 각 API 계약에서 확인한다.

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
|---|---|---|
| 결과가 없거나 기대 건수와 다름 | 적용된 검색 기준·기간·탭·대상 상태·서버 필터·페이징·목록/다운로드 조건 | 조건을 다시 확인하고 조회한다. 지속되면 경로·작업 시각·마스킹한 식별자·필터를 업무/기술 담당에게 전달한다. |
| 메뉴·버튼 미표시 또는 접근 거부 | 사용자 그룹의 메뉴 접근·VIEW 및 API별 PROCESS/EXECUTE/DELETE/EXCEL_DOWNLOAD/UNMASK 등 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. 프런트 버튼 표시만으로 서버 권한을 판단하지 않는다. |
| 저장·삭제·외부 실행의 결과가 불명확 | 대상 현재 상태·중복 요청·감사 이력·API 오류·파일/외부 소비 로그 | 기존 반영 여부를 먼저 조회한다. 중복 발송·초기화·금액 처리를 피하기 위해 기술 담당 확인 후 재시도한다. |

## 7) 검증·출처

**브라우저 검증(2026-11-09)**: 화면 대조. [경로별 결과와 제한](../../references/browser-verification.md#page048). 역할별 권한 거부·저장 성공·파일 반출·외부 연계 완료는 이 결과로 보장하지 않는다.

| 검증 항목 | 근거·환경 | 상태·확인일 |
|---|---|---|
| 대상 선정 | 사용자가 WBS 탭 내용으로 제공한 텍스트의 No. 142, 143; [선정 태스크](../../inventory/wbs-tasks.csv) | 제공 텍스트 확인 2026-11-09. 원본 Excel의 탭/병합 셀을 독립 재열람한 것은 아님. |
| 메뉴·라우트·화면 | [menuConfig.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts); [BonabankRoutes.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/BonabankRoutes.tsx); [BonabankTaxInvoiceDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bonabank/BonabankTaxInvoiceDetailPage.tsx) | 코드 확인 2026-11-09, 기준 dc216b313 |
| 기능·권한·API | 이 문서의 API 계약 링크 및 연결 Hook/API·Controller·DTO·Service·Repository·Mapper | 코드 확인 2026-11-09. 조회 요청·화면 대조 범위는 아래 브라우저 근거 참조. 권한 계정별 허용·거부 및 변경 요청 실행은 미확인. |
| DB 정의 | [개발 DB 계약](../../references/database-contracts.md), 이 문서의 연결 객체 | 개발 DB 정의 확인 2026-11-09. 동적 SQL·CLR 내부·정의 미공개 참조의 미확정 범위는 객체별 기록; 후속 확인 DB 담당. |
| 브라우저 화면·배포 환경 | 로컬 인증 계정·Playwright CLI; [화면별 검증표](../../references/browser-verification.md#page048) | 화면 대조, 2026-11-09. 배포본·타 역할·업무 변경 결과는 미확인. |
| 업무 프로시저·쓰기·외부 결과 | 격리된 검증 환경·테스트 데이터의 실행 결과 | 미확인: 명시적인 저장·삭제·발송·초기화 요청은 실행하지 않음. 브라우저 GET의 업무 조회 프로시저·조회수·감사 기록은 별도 영향으로 구분. 격리 환경에서 기술 담당 확인. |

코드 확인과 DB 정의 확인은 실행 성공·업무 승인·다른 환경 적용을 보장하지 않는다. 업무·기술 담당 검토 후 조사 목록의 상태를 완료로 변경한다.

브라우저 직접 근거: [settled-detail-revisit](../../evidence/browser/ready-details-stable.json). 경로·고정 버튼명·입력 속성·표 머리글·API 상태를 보관했고 실제 데이터 값·식별자·인증정보는 제외했다.

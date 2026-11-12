# [회사·회원·서비스 권한] 대량 회원가입 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

대량 회원가입 업로드 이력을 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 회사·회원·서비스 권한 |
| 언제 사용하는가 | 업로드 이력 조회, 엑셀 양식 다운로드, 대량 회원가입 파일 업로드 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 회원 유형, 내국인 가입, 외국인 가입, 파일 첨부, 날짜조건, 전체 |
| 업무 흐름 | 업로드 이력 조회, 엑셀 양식 다운로드, 대량 회원가입 파일 업로드 |
| 이 페이지의 역할 | 조회 · 업로드 이력 조회 |
| 판단 결과·다음 업무 | 현재 화면에서 결과를 확인한다. |
| 다른 화면과의 구분 | 같은 경로에서 열리는 조회·팝업은 이 문서에서 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 대량 회원가입 업로드 이력을 조회한다. |
| 메뉴·화면 경로 | SB 고객관리 > 스마트빌 회원·회사정보 관리 > 대량 회원가입 · `/member-management/member/bulk-registration` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | 현재 화면에서 결과를 확인한다. |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/member-management/member/bulk-registration` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 업로드 이력 조회 | `/member-management/member/bulk-registration` `VIEW` | `dateCondition: String?` · `startDate: String?` · `endDate: String?` · `fileName: String?` · `processor: String?` · `page: Int` · `size: Int` |
| 엑셀 양식 다운로드 | `/member-management/member/bulk-registration` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 대량 회원가입 파일 업로드 | `/member-management/member/bulk-registration` `EXCEL_UPLOAD` | `file: MultipartFile` · `memberType: String` |
| 대량 회원가입 처리자명 원문 조회 | `/member-management/member/bulk-registration` / `UNMASK` | `id`, `field` |
| 대량 회원가입 실패 사유 아이디 원문 조회 | `/member-management/member/bulk-registration` / `UNMASK` | `id`, `rowNumber`, `field` |

코드에서 확인한 버튼·작업명은 **샘플 다운로드**, **파일 삭제**, **첨부파일**, **파일 선택**, **업로드**, **파일 업로드**, **검색 필터 열기**, **검색**, **실패 사유 보기**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **SB 고객관리 > 스마트빌 회원·회사정보 관리 > 대량 회원가입**를 연다. `/member-management/member/bulk-registration`를 연다.
2. **회원 유형**, **내국인 가입**, **외국인 가입**, **파일 첨부**, **날짜조건**, **전체**, **업로드 일자** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **샘플 다운로드**, **검색 필터 열기**, **검색** 중 해당 버튼을 선택한다.
3. **업로드 이력 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 회원 유형 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/BulkMemberRegistrationFileUpload.tsx#L76) |
| 내국인 가입 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/BulkMemberRegistrationFileUpload.tsx#L89) |
| 외국인 가입 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/BulkMemberRegistrationFileUpload.tsx#L95) |
| 파일 첨부 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/BulkMemberRegistrationFileUpload.tsx#L104) |
| 날짜조건 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/BulkMemberRegistrationPage.tsx#L32) |
| 전체 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `all` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/BulkMemberRegistrationPage.tsx#L68) |
| 업로드 일자 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `업로드 일자` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/BulkMemberRegistrationPage.tsx#L39) |
| 파일명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/BulkMemberRegistrationPage.tsx#L46) |
| 처리자 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/BulkMemberRegistrationPage.tsx#L61) |
| 회원수 | 출력 | 조회 응답 기준 | 화면 필드 `memberCount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/BulkMemberRegistrationTable.tsx#L49) |
| 업로드 결과 | 출력 | 조회 응답 기준 | 화면 필드 `uploadResult` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/BulkMemberRegistrationTable.tsx#L56) |
| 이름 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `MEMBER_NAME` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/BulkMemberRegistrationTable.tsx#L150) |
| 아이디 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `MEMBER_ID` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/BulkMemberRegistrationTable.tsx#L162) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 업로드 이력 조회 | `GET /api/v1/members/bulk-registrations` · `/member-management/member/bulk-registration` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/customer/member/BulkMemberRegistrationController.kt#L66) | `dateCondition: String?` · `startDate: String?` · `endDate: String?` · `fileName: String?` · `processor: String?` · `page: Int` · `size: Int` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `currentPage`, `size` | `smartwork.dbo.bulk_member_registration`, `office.dbo.SAWON` |
| 엑셀 양식 다운로드 | `GET /api/v1/members/bulk-registrations/template` · `/member-management/member/bulk-registration` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/customer/member/BulkMemberRegistrationController.kt#L166) | 추가 입력은 Controller 서명 참조 → 파일 또는 오류 응답 | 직접 DB 호출이 연결된 경로는 현재 소스에서 미확인. 세부 저장소는 Controller와 Service 참조. |
| 대량 회원가입 파일 업로드 | `POST /api/v1/members/bulk-registrations` · `/member-management/member/bulk-registration` `EXCEL_UPLOAD` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/customer/member/BulkMemberRegistrationController.kt#L94) | `file: MultipartFile` · `memberType: String` → `success`, `data`, `error`, `fileName`, `totalCount`, `successCount`, `failCount`, `errors` | `SmartBill3.dbo.upMem_SchMemberDormant`, `SB_COMMON.dbo.upAdm_SavFMemberInfo`, `SB_COMMON.dbo.upAdm_SavMemberInfo`, `smartwork.dbo.bulk_member_registration` · 정의에서 확인한 쓰기 `SmartBill3.dbo.COMPANY`, `SmartBill3.dbo.MEMBER`, `SB_DTI.dbo.DTI_RIGHT`, `SmartBill3.dbo.MEMBER_RIGHT` 외 11개 |
| 대량 회원가입 처리자명 원문 조회 | `POST /api/v1/members/bulk-registrations/{id}/sensitive-values/reveal` · `/member-management/member/bulk-registration` / `UNMASK` · [화면 컴포넌트](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/BulkMemberRegistrationTable.tsx#L103) · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/customer/member/BulkMemberRegistrationController.kt#L111) | `id`, `field` → 요청한 항목의 원문 응답 | 권한 검사 후 대상 값을 조회하고 감사 기록을 남긴다. |
| 대량 회원가입 실패 사유 아이디 원문 조회 | `POST /api/v1/members/bulk-registrations/{id}/errors/{rowNumber}/sensitive-values/reveal` · `/member-management/member/bulk-registration` / `UNMASK` · [화면 컴포넌트](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/BulkMemberRegistrationTable.tsx#L160) · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/customer/member/BulkMemberRegistrationController.kt#L133) | `id`, `rowNumber`, `field` → 요청한 항목의 원문 응답 | 권한 검사 후 대상 값을 조회하고 감사 기록을 남긴다. |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.bulk_member_registration` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/member/repository/BulkMemberRegistrationMapper.kt#L126) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-33d96579a7a55e69) |
| `office.dbo.SAWON` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/member/repository/BulkMemberRegistrationMapper.kt#L126) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3a9ea6e368df5cb3) |
| `SmartBill3.dbo.upMem_SchMemberDormant` | @MEM_ID varchar(50), @MEM_NAME varchar(50), @MEM_REGNO varchar(13), @MEM_EMAIL varchar(50) | 정의 참조 `SB_DTI_LOG.dbo.DORMANT_MEMBER` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/member/repository/BulkMemberRegistrationMapper.kt#L43) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-04f76f6a6305d4b2) |
| `SB_COMMON.dbo.upAdm_SavFMemberInfo` | @MEM_REALNAME varchar(35), @MEM_NICKNAME varchar(35), @MEM_REGNO varchar(13), @MEM_ID varchar(12), @MEM_PW varchar(35), @MEM_SHA_PW varchar(70), @MEM_TEL varchar(20), @MEM_HP varchar(20), @MEM_EMAIL varchar(70), @MEM_FGN char(1), @MEM_EMAILRCV char(1), @MEM_FAX varchar(20), @BIZPLACE_CODE varchar(35), @COM_NAME varchar(70), @COM_REGNO varchar(13), @COM_PRESIDENT varchar(35), @COM_BIZSTATUS varchar(70), @COM_BIZCLASS varchar(70), @COM_ZIPCODE varchar(7), @COM_ADDRESS varchar(150), @COM_SEAL varchar(255), @BIZ_CTG varchar(4), @BIZ_CTG_DETAIL varchar(3), @MA_ID varchar(12), @SP_RESULT int OUT | 정의 참조 `SB_DTI.dbo.BIZPLACE_MEMBER`, `SB_DTI.dbo.BIZPLACE_MEMBER_HIS`, `SmartBill3.dbo.COMPANY`, `SB_DTI.dbo.COMPANY_DTICONFIG`, `SB_DTI_LOG.dbo.DBGS_IF_MSG` 외 8개 · 정적 쓰기 `SmartBill3.dbo.COMPANY`, `SmartBill3.dbo.MEMBER`, `SB_DTI.dbo.DTI_RIGHT`, `SmartBill3.dbo.MEMBER_RIGHT` 외 9개 · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/member/repository/BulkMemberRegistrationMapper.kt#L76) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-dfe4623e90da5ba8) |
| `SB_COMMON.dbo.upAdm_SavMemberInfo` | @MEM_REALNAME varchar(35), @MEM_NICKNAME varchar(35), @MEM_REGNO varchar(8), @MEM_ID varchar(12), @MEM_PW varchar(35), @MEM_SHA_PW varchar(70), @MEM_TEL varchar(20), @MEM_HP varchar(20), @MEM_EMAIL varchar(70), @MEM_FGN char(1), @MEM_EMAILRCV char(1), @MEM_FAX varchar(20), @BIZPLACE_CODE varchar(35), @COM_NAME varchar(70), @COM_REGNO varchar(13), @COM_PRESIDENT varchar(35), @COM_BIZSTATUS varchar(70), @COM_BIZCLASS varchar(70), @COM_ZIPCODE varchar(7), @COM_ADDRESS varchar(150), @COM_SEAL varchar(255), @BIZ_CTG varchar(4), @BIZ_CTG_DETAIL varchar(3), @MA_ID varchar(12), @SP_RESULT int OUT | 정의 참조 `SB_DTI.dbo.BIZPLACE_MEMBER`, `SB_DTI.dbo.BIZPLACE_MEMBER_HIS`, `SmartBill3.dbo.COMPANY`, `SB_DTI.dbo.COMPANY_DTICONFIG`, `SB_DTI_LOG.dbo.DBGS_IF_MSG` 외 10개 · 정적 쓰기 `SmartBill3.dbo.COMPANY`, `SmartBill3.dbo.MEMBER`, `SB_DTI.dbo.DTI_RIGHT`, `SmartBill3.dbo.MEMBER_RIGHT` 외 10개 · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/member/repository/BulkMemberRegistrationMapper.kt#L62) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-0bcd76d944d578f3) |
| `smartwork.dbo.usp_sw_log_access_event_insert` | @EVENT_TYPE varchar(30) IN, @STATUS varchar(20) IN, @USER_ID bigint IN, @MEMBER_ID nvarchar(50) IN, @USER_NAME nvarchar(100) IN, @DEPARTMENT_NAME nvarchar(100) IN, @PAGE_TITLE nvarchar(200) IN, @PATH nvarchar(500) IN, @MENU_PATH nvarchar(500) IN, @MENU_LABEL nvarchar(200) IN, @CATEGORY_NAME nvarchar(200) IN, @SUB_CATEGORY_NAME nvarchar(200) IN, @MENU_ORDER int IN, @IP_ADDRESS varchar(45) IN, @USER_AGENT nvarchar(1000) IN, @BROWSER varchar(100) IN, @OS varchar(100) IN, @REFERRER nvarchar(500) IN, @DETAIL nvarchar(1000) IN, @RESULT int OUT, @COUNTS_AS_VISIT bit IN | 원문 조회 또는 감사 흐름에서 호출 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/logmanagement/repository/LogManagementMapper.kt#L92) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 회원 유형, 내국인 가입, 외국인 가입, 파일 첨부, 날짜조건, 전체 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 고객관리 > 스마트빌 회원·회사정보 관리 > 대량 회원가입의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 데이터를 불러오는 중 오류가 발생했습니다. | 회원 유형, 내국인 가입, 외국인 가입, 파일 첨부, 날짜조건, 전체 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 양식 다운로드에 실패했습니다. | 회원 유형, 내국인 가입, 외국인 가입, 파일 첨부, 날짜조건, 전체 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 검색 결과가 존재하지 않습니다. | 회원 유형, 내국인 가입, 외국인 가입, 파일 첨부, 날짜조건, 전체 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/CustomerRoutes.tsx#L44) · [BulkMemberRegistrationPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/BulkMemberRegistrationPage.tsx#L78) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/api/bulkMemberRegistrationApi.ts#L42) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/api/bulkMemberRegistrationApi.ts#L49) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/api/bulkMemberRegistrationApi.ts#L63) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 5개 중 개발 메타데이터 확인 5개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-c93beabff2e26c9f) | Demo 메타데이터 6/6개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

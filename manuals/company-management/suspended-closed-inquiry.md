# [가입·탈퇴와 휴폐업] 휴폐업 조회 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

사업자번호로 국세청 휴폐업 상태를 조회한다. 결과는 0~1건입니다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 가입·탈퇴와 휴폐업 |
| 언제 사용하는가 | 휴폐업 조회, 휴폐업 등록 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 사업자번호, 국세청 적용일, 국세청 조회일자, 폐업일자, 과세유형, 등록자 |
| 업무 흐름 | 휴폐업 조회, 휴폐업 등록 |
| 이 페이지의 역할 | 조회·관리 · 휴폐업 조회 |
| 판단 결과·다음 업무 | 현재 화면에서 결과를 확인한다. |
| 다른 화면과의 구분 | 같은 경로에서 열리는 조회·팝업은 이 문서에서 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 확인 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/pages/SuspendedClosedInquiryPage.tsx#L170) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 사업자번호로 국세청 휴폐업 상태를 조회한다. 결과는 0~1건입니다. |
| 메뉴·화면 경로 | SB 고객관리 > 스마트빌 회원·회사정보 관리 > 휴폐업 조회 · `/company-management/suspended-closed-inquiry` |
| 화면 유형·담당 | 조회·관리 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | 현재 화면에서 결과를 확인한다. |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/company-management/suspended-closed-inquiry` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 휴폐업 조회 | `/company-management/suspended-closed-inquiry` `VIEW` | `businessNumber: String` |
| 휴폐업 등록 | `/company-management/suspended-closed-inquiry` `PROCESS` | `businessNumber: String` · `CompanyQuitStatusSaveRequest` `taxType`, `quitDate` |
| 휴폐업 등록자명 원문 조회 | `/company-management/suspended-closed-inquiry` / `UNMASK` | `businessNumber`, `field` |

코드에서 확인한 버튼·작업명은 **검색**, **등록**, **확인**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **SB 고객관리 > 스마트빌 회원·회사정보 관리 > 휴폐업 조회**를 연다. `/company-management/suspended-closed-inquiry`를 연다.
2. **사업자번호** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색**, **등록**, **확인** 중 해당 버튼을 선택한다.
3. **휴폐업 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 사업자번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/pages/SuspendedClosedInquiryPage.tsx#L64) |
| 국세청 적용일 | 출력 | 조회 응답 기준 | 화면 필드 `ntsApplyDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CompanyQuitStatusTable.tsx#L70) |
| 국세청 조회일자 | 출력 | 조회 응답 기준 | 화면 필드 `searchDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CompanyQuitStatusTable.tsx#L77) |
| 폐업일자 | 입력 또는 선택 | API 기본값 null | API 요청 `quitDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CompanyQuitStatusTable.tsx#L84) |
| 과세유형 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | API 요청 `taxType` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CompanyQuitStatusTable.tsx#L105) |
| 등록자 | 출력 | 조회 응답 기준 | 화면 필드 `registrant` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CompanyQuitStatusTable.tsx#L130) |
| 등록일자 | 출력 | 조회 응답 기준 | 화면 필드 `registrationDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CompanyQuitStatusTable.tsx#L145) |
| 처리 | 출력 | 조회 응답 기준 | 화면 필드 `action` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CompanyQuitStatusTable.tsx#L152) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 휴폐업 조회 | `GET /api/v1/company-management/suspended-closed-inquiry` · `/company-management/suspended-closed-inquiry` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/customer/company/CompanyQuitStatusController.kt#L57) | `businessNumber: String` → `success`, `data`, `error`, `content` | `smartwork.dbo.usp_company_quit_status_select` · 코드 연계 트랜잭션 |
| 휴폐업 등록 | `PUT /api/v1/company-management/suspended-closed-inquiry/{businessNumber}` · `/company-management/suspended-closed-inquiry` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/customer/company/CompanyQuitStatusController.kt#L74) | `businessNumber: String` · `CompanyQuitStatusSaveRequest` `taxType`, `quitDate` → `success`, `data`, `error` | `smartwork.dbo.usp_company_quit_status_save` · 정의에서 확인한 쓰기 `SB_DTI.dbo.COMPANY_QUIT_STATUS` · 코드 연계 트랜잭션 |
| 휴폐업 등록자명 원문 조회 | `POST /api/v1/company-management/suspended-closed-inquiry/{businessNumber}/sensitive-values/reveal` · `/company-management/suspended-closed-inquiry` / `UNMASK` · [화면 컴포넌트](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CompanyQuitStatusTable.tsx#L135) · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/customer/company/CompanyQuitStatusController.kt#L89) | `businessNumber`, `field` → 요청한 항목의 원문 응답 | 권한 검사 후 대상 값을 조회하고 감사 기록을 남긴다. |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.usp_company_quit_status_select` | @COM_REGNO varchar(10) | 정의 참조 `SmartBill3.dbo.ADMIN_INFO`, `SB_DTI.dbo.COMPANY_QUIT_STATUS`, `office.dbo.SAWON` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/companyquit/repository/CompanyQuitStatusMapper.kt#L41) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-fc360e2d465fe9e0) |
| `smartwork.dbo.usp_company_quit_status_save` | @COM_REGNO varchar(10), @TAX_TYPE varchar(2), @QUIT_DATE varchar(10), @REG_USER int | 정의 참조 `SB_DTI.dbo.COMPANY_QUIT_STATUS` · 정적 쓰기 `SB_DTI.dbo.COMPANY_QUIT_STATUS` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/companyquit/repository/CompanyQuitStatusMapper.kt#L53) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-9a28441a15e8870e) |
| `smartwork.dbo.usp_sw_log_access_event_insert` | @EVENT_TYPE varchar(30) IN, @STATUS varchar(20) IN, @USER_ID bigint IN, @MEMBER_ID nvarchar(50) IN, @USER_NAME nvarchar(100) IN, @DEPARTMENT_NAME nvarchar(100) IN, @PAGE_TITLE nvarchar(200) IN, @PATH nvarchar(500) IN, @MENU_PATH nvarchar(500) IN, @MENU_LABEL nvarchar(200) IN, @CATEGORY_NAME nvarchar(200) IN, @SUB_CATEGORY_NAME nvarchar(200) IN, @MENU_ORDER int IN, @IP_ADDRESS varchar(45) IN, @USER_AGENT nvarchar(1000) IN, @BROWSER varchar(100) IN, @OS varchar(100) IN, @REFERRER nvarchar(500) IN, @DETAIL nvarchar(1000) IN, @RESULT int OUT, @COUNTS_AS_VISIT bit IN | 원문 조회 또는 감사 흐름에서 호출 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/logmanagement/repository/LogManagementMapper.kt#L92) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 사업자번호, 국세청 적용일, 국세청 조회일자, 폐업일자, 과세유형, 등록자 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 고객관리 > 스마트빌 회원·회사정보 관리 > 휴폐업 조회의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 휴폐업 조회 중 오류가 발생했습니다. | 사업자번호, 국세청 적용일, 국세청 조회일자, 폐업일자, 과세유형, 등록자 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 휴폐업 등록 중 오류가 발생했습니다. | 사업자번호, 국세청 적용일, 국세청 조회일자, 폐업일자, 과세유형, 등록자 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 조회된 휴폐업 정보가 없습니다. | 사업자번호, 국세청 적용일, 국세청 조회일자, 폐업일자, 과세유형, 등록자 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/CustomerRoutes.tsx#L66) · [SuspendedClosedInquiryPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/pages/SuspendedClosedInquiryPage.tsx#L36) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/api/companyQuitStatusApi.ts#L16) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/api/companyQuitStatusApi.ts#L25) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 2개 중 개발 메타데이터 확인 2개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-07ad2053403396d7) | Demo 메타데이터 3/3개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

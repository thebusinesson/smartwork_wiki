# [입금·예치금·배분·취소·환불] 본사 입금 관리 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

본사 입금 리스트를 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 입금·예치금·배분·취소·환불 |
| 언제 사용하는가 | 본사 입금 목록 조회, 본사 입금 목록 다운로드, 본사 입금 삭제 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 입금일, 업체 조건, 처리 상태, 청구 구분, 입금자명, 입금액 |
| 업무 흐름 | 본사 입금 목록 조회, 본사 입금 목록 다운로드, 본사 입금 삭제 |
| 이 페이지의 역할 | 조회·관리 · 본사 입금 목록 조회 |
| 판단 결과·다음 업무 | [본사 입금 관리 상세](head-office-deposit__by-id.md) |
| 다른 화면과의 구분 | 이 경로에서 볼 수 있는 조건·결과를 기준으로 사용한다. 독립 경로의 상세·등록은 관련 화면에 연결한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 확인 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/HeadOfficeDepositDeleteDialog.tsx#L70) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 본사 입금 리스트를 조회한다. |
| 메뉴·화면 경로 | 서비스 현황 > 입금관리 > 본사 입금 관리 · `/payment/head-office-deposit` |
| 화면 유형·담당 | 조회·관리 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [본사 입금 관리 상세](head-office-deposit__by-id.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/payment/head-office-deposit` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 본사 입금 목록 조회 | `/payment/head-office-deposit` `VIEW` | `HeadOfficeDepositSearchRequest` `page`, `pageSize`, `fromDate`, `toDate`, `searchCode`, `searchText`, `state`, `gubun` |
| 본사 입금 목록 다운로드 | `/payment/head-office-deposit` `EXCEL_DOWNLOAD` | `HeadOfficeDepositSearchRequest` `page`, `pageSize`, `fromDate`, `toDate`, `searchCode`, `searchText`, `state`, `gubun` |
| 본사 입금 삭제 | `/payment/head-office-deposit` `DELETE` | `HeadOfficeDepositDeleteRequest` `idxList`, `reason` · 서버 필수 `idxList`, `reason` |
| 본사 입금 입금자명 원문 조회 | `/payment/head-office-deposit` / `UNMASK` | `idx`, `field` |

코드에서 확인한 버튼·작업명은 **검색**, **다운로드**, **삭제**, **확인**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **서비스 현황 > 입금관리 > 본사 입금 관리**를 연다. `/payment/head-office-deposit`를 연다.
2. **입금일**, **업체 조건**, **처리 상태**, **청구 구분** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색**, **다운로드**, **확인** 중 해당 버튼을 선택한다.
3. **본사 입금 목록 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [본사 입금 관리 상세](head-office-deposit__by-id.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 입금일 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositManagementListPage.tsx#L168) |
| 업체 조건 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositManagementListPage.tsx#L178) |
| 처리 상태 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositManagementListPage.tsx#L205) |
| 청구 구분 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositManagementListPage.tsx#L218) |
| 입금자명 | 출력 | 조회 응답 기준 | 화면 필드 `depositorName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositManagementListPage.tsx#L346) |
| 입금액 | 출력 | 조회 응답 기준 | 화면 필드 `depositAmount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositManagementListPage.tsx#L360) |
| 잔액 | 출력 | 조회 응답 기준 | 화면 필드 `balanceAmount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositManagementListPage.tsx#L361) |
| 회사명 | 출력 | 조회 응답 기준 | 화면 필드 `processes.comName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositManagementListPage.tsx#L366) |
| 사업자번호 | 출력 | 조회 응답 기준 | 화면 필드 `processes.comRegno` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositManagementListPage.tsx#L371) |
| 처리금액 | 출력 | 조회 응답 기준 | 화면 필드 `processes.processedAmount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositManagementListPage.tsx#L376) |
| 처리상태 | 출력 | 조회 응답 기준 | 화면 필드 `status` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositManagementListPage.tsx#L381) |
| 청구구분 | 입력 또는 선택 | API 기본값 null | API 요청 `gubun` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositManagementListPage.tsx#L399) |
| 삭제 사유 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/HeadOfficeDepositDeleteDialog.tsx#L88) |
| 삭제 사유를 입력하세요 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/HeadOfficeDepositDeleteDialog.tsx#L94) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 본사 입금 목록 조회 | `GET /api/v1/status/payment/head-office-deposit` · `/payment/head-office-deposit` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/headofficedeposit/HeadOfficeDepositController.kt#L83) | `HeadOfficeDepositSearchRequest` `page`, `pageSize`, `fromDate`, `toDate`, `searchCode`, `searchText`, `state`, `gubun` → `success`, `data`, `error`, `content`, `totalElements` | `smartwork.dbo.UspBill_HeadOfficeDepositList_SELECT` · 코드 연계 트랜잭션 |
| 본사 입금 목록 다운로드 | `GET /api/v1/status/payment/head-office-deposit/download` · `/payment/head-office-deposit` `EXCEL_DOWNLOAD` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/headofficedeposit/HeadOfficeDepositController.kt#L106) | `HeadOfficeDepositSearchRequest` `page`, `pageSize`, `fromDate`, `toDate`, `searchCode`, `searchText`, `state`, `gubun` → 파일 또는 오류 응답 | `smartwork.dbo.UspBill_HeadOfficeDepositList_SELECT` · 코드 연계 트랜잭션 |
| 본사 입금 삭제 | `DELETE /api/v1/status/payment/head-office-deposit` · `/payment/head-office-deposit` `DELETE` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/headofficedeposit/HeadOfficeDepositController.kt#L259) | `HeadOfficeDepositDeleteRequest` `idxList`, `reason` · 서버 필수 `idxList`, `reason` → `success`, `data`, `error` | `SB_BILL.dbo.UspBill_PaymentBalanceDepositProcessInfo_DELETE`, `smartwork.dbo.deposit_deduction`, `smartwork.dbo.action_reason` · 정의에서 확인한 쓰기 `smartwork.dbo.deposit_deduction`, `smartwork.dbo.action_reason` · 코드 연계 트랜잭션 |
| 본사 입금 입금자명 원문 조회 | `POST /api/v1/status/payment/head-office-deposit/{idx}/sensitive-values/reveal` · `/payment/head-office-deposit` / `UNMASK` · [화면 컴포넌트](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositManagementListPage.tsx#L352) · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/headofficedeposit/HeadOfficeDepositController.kt#L156) | `idx`, `field` → 요청한 항목의 원문 응답 | 권한 검사 후 대상 값을 조회하고 감사 기록을 남긴다. |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.UspBill_HeadOfficeDepositList_SELECT` | @PAGE int, @TOP int, @FROMDATE varchar(10), @TODATE varchar(10), @SEARCHCODE varchar(10), @SEARCHTEXT varchar(100), @STATE varchar(10), @GUBUN varchar(100) | 정의 참조 `SmartBill3.dbo.COMPANY`, `SB_BILL_LINKED.dbo.CRM_T_CR_OS_IV`, `smartwork.dbo.d`, `smartwork.dbo.deposit_deduction`, `SB_BILL.dbo.HEADOFFICE_DEPOSIT` 외 2개 · 쓰기 구문 존재 · 대상 별칭 또는 하위 정의 확인 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/headofficedeposit/repository/HeadOfficeDepositMapper.kt#L51) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-a946fb9f1b96ef65) |
| `SB_BILL.dbo.UspBill_PaymentBalanceDepositProcessInfo_DELETE` | @IDXS varchar(max), @RESULT varchar(5) OUT | 동적 SQL 포함 · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/headofficedeposit/repository/HeadOfficeDepositMapper.kt#L126) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-2103318b4929b1e6) |
| `smartwork.dbo.deposit_deduction` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL DELETE FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/depositdeduction/repository/DepositDeductionMapper.kt#L127) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-cc106276f1e9c83e) |
| `smartwork.dbo.action_reason` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL INSERT INTO | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/shared/actionreason/repository/ActionReasonMapper.kt#L16) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b0430106ffe0743f) |
| `smartwork.dbo.UspBill_HeadOfficeDepositDetailInfo_SELECT` | @IDX bigint IN | 원문 조회 또는 감사 흐름에서 호출 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/headofficedeposit/repository/HeadOfficeDepositMapper.kt#L70) |
| `smartwork.dbo.usp_sw_log_access_event_insert` | @EVENT_TYPE varchar(30) IN, @STATUS varchar(20) IN, @USER_ID bigint IN, @MEMBER_ID nvarchar(50) IN, @USER_NAME nvarchar(100) IN, @DEPARTMENT_NAME nvarchar(100) IN, @PAGE_TITLE nvarchar(200) IN, @PATH nvarchar(500) IN, @MENU_PATH nvarchar(500) IN, @MENU_LABEL nvarchar(200) IN, @CATEGORY_NAME nvarchar(200) IN, @SUB_CATEGORY_NAME nvarchar(200) IN, @MENU_ORDER int IN, @IP_ADDRESS varchar(45) IN, @USER_AGENT nvarchar(1000) IN, @BROWSER varchar(100) IN, @OS varchar(100) IN, @REFERRER nvarchar(500) IN, @DETAIL nvarchar(1000) IN, @RESULT int OUT, @COUNTS_AS_VISIT bit IN | 원문 조회 또는 감사 흐름에서 호출 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/logmanagement/repository/LogManagementMapper.kt#L92) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 입금일, 업체 조건, 처리 상태, 청구 구분, 입금자명, 입금액 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 서비스 현황 > 입금관리 > 본사 입금 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 다운로드할 데이터가 없습니다. | 입금일, 업체 조건, 처리 상태, 청구 구분, 입금자명, 입금액 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 다운로드 중 오류가 발생했습니다. | 입금일, 업체 조건, 처리 상태, 청구 구분, 입금자명, 입금액 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 삭제할 항목을 선택해주세요. | 입금일, 업체 조건, 처리 상태, 청구 구분, 입금자명, 입금액 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 삭제 중 오류가 발생했습니다. | 입금일, 업체 조건, 처리 상태, 청구 구분, 입금자명, 입금액 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/PaymentRoutes.tsx#L63) · [HeadOfficeDepositManagementListPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositManagementListPage.tsx#L77) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/headOfficeDepositManagementApi.ts#L42) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/headOfficeDepositManagementApi.ts#L61) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/headOfficeDepositManagementApi.ts#L106) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 4개 중 개발 메타데이터 확인 4개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-75049b4e3565210f) | Demo 메타데이터 6/6개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

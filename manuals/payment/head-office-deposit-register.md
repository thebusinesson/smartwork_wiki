# [입금·예치금·배분·취소·환불] 본사 입금 등록 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

업로드 목록을 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 입금·예치금·배분·취소·환불 |
| 언제 사용하는가 | 업로드 파일 목록 조회, 파일 업로드, 업로드 파일 삭제 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 업로드 일자, 파일명, 총 건수, 자동매칭, 입금등록, 업로드 상태 |
| 업무 흐름 | 업로드 파일 목록 조회, 파일 업로드, 업로드 파일 삭제 |
| 이 페이지의 역할 | 조회·관리 · 업로드 파일 목록 조회 |
| 판단 결과·다음 업무 | [본사 입금 등록](head-office-deposit-register__detail.md) |
| 다른 화면과의 구분 | 이 경로에서 볼 수 있는 조건·결과를 기준으로 사용한다. 독립 경로의 상세·등록은 관련 화면에 연결한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 확인 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositRegistrationPage.tsx#L448) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 업로드 목록을 조회한다. |
| 메뉴·화면 경로 | 서비스 현황 > 입금관리 > 본사 입금 등록 · `/payment/head-office-deposit-register` |
| 화면 유형·담당 | 조회·관리 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [본사 입금 등록](head-office-deposit-register__detail.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/payment/head-office-deposit-register` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 업로드 파일 목록 조회 | `/payment/head-office-deposit-register` `VIEW` | `DepositUploadSearchRequest` `startDate`, `endDate`, `depositConversion`, `page`, `size` |
| 파일 업로드 | `/payment/head-office-deposit-register` `EXCEL_UPLOAD` | `file: MultipartFile` |
| 업로드 파일 삭제 | `/payment/head-office-deposit-register` `DELETE` | `DepositFileDeleteRequest` `fileIds`, `reason` · 서버 필수 `fileIds`, `reason` |

코드에서 확인한 버튼·작업명은 **파일 삭제**, **첨부파일**, **업로드**, **검색**, **삭제**, **확인**, **취소**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **서비스 현황 > 입금관리 > 본사 입금 등록**를 연다. `/payment/head-office-deposit-register`를 연다.
2. **입금 전환**, **삭제 사유** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색**, **확인** 중 해당 버튼을 선택한다.
3. **업로드 파일 목록 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [본사 입금 등록](head-office-deposit-register__detail.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 업로드 일자 | 출력 | 조회 응답 기준 | 화면 필드 `uploadDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositRegistrationPage.tsx#L312) |
| 파일명 | 출력 | 조회 응답 기준 | 화면 필드 `fileName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositRegistrationPage.tsx#L318) |
| 총 건수 | 출력 | 조회 응답 기준 | 화면 필드 `totalCount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositRegistrationPage.tsx#L331) |
| 자동매칭 | 출력 | 조회 응답 기준 | 화면 필드 `autoMatching` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositRegistrationPage.tsx#L338) |
| 입금등록 | 출력 | 조회 응답 기준 | 화면 필드 `depositRegistration` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositRegistrationPage.tsx#L345) |
| 업로드 상태 | 출력 | 조회 응답 기준 | 화면 필드 `uploadStatus` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositRegistrationPage.tsx#L351) |
| 입금 전환 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositRegistrationPage.tsx#L75) |
| 삭제 사유 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositRegistrationPage.tsx#L473) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 업로드 파일 목록 조회 | `GET /api/v1/status/payment/head-office-deposit/registration` · `/payment/head-office-deposit-register` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/headofficedeposit/HeadOfficeDepositRegistrationController.kt#L83) | `DepositUploadSearchRequest` `startDate`, `endDate`, `depositConversion`, `page`, `size` → `success`, `data`, `error`, `content`, `totalElements` | `smartwork.dbo.usp_bill_head_office_deposit_upload_list_select` · 코드 연계 트랜잭션 |
| 파일 업로드 | `POST /api/v1/status/payment/head-office-deposit/registration/upload` · `/payment/head-office-deposit-register` `EXCEL_UPLOAD` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/headofficedeposit/HeadOfficeDepositRegistrationController.kt#L102) | `file: MultipartFile` → `success`, `data`, `error` | `SB_BILL.dbo.UspBill_HeadOffice_Deposit_FileSave_INSERT`, `smartwork.dbo.headoffice_deposit_register`, `smartwork.dbo.headoffice_deposit_register_process`, `smartwork.dbo.deposit_deduction`, `SB_BILL.dbo.HEADOFFICE_DEPOSIT_UPLOAD` 외 3개 · 정의에서 확인한 쓰기 `SB_BILL.dbo.HEADOFFICE_DEPOSIT_UPLOAD`, `smartwork.dbo.headoffice_deposit_register`, `smartwork.dbo.headoffice_deposit_register_process` · 코드 연계 트랜잭션 |
| 업로드 파일 삭제 | `DELETE /api/v1/status/payment/head-office-deposit/registration/files` · `/payment/head-office-deposit-register` `DELETE` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/headofficedeposit/HeadOfficeDepositRegistrationController.kt#L116) | `DepositFileDeleteRequest` `fileIds`, `reason` · 서버 필수 `fileIds`, `reason` → `success`, `data`, `error` | `SB_BILL.dbo.HEADOFFICE_DEPOSIT`, `SB_BILL.dbo.HEADOFFICE_DEPOSIT_UPLOAD`, `smartwork.dbo.headoffice_deposit_register_process`, `smartwork.dbo.headoffice_deposit_register`, `smartwork.dbo.deposit_deduction` 외 1개 · 정의에서 확인한 쓰기 `smartwork.dbo.action_reason` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.usp_bill_head_office_deposit_upload_list_select` | @page int, @pagesize int, @is_all_dates bit, @start_date varchar(10), @end_date varchar(10), @deposit_conversion varchar(1) | 정의 참조 `SB_BILL.dbo.HEADOFFICE_DEPOSIT`, `smartwork.dbo.headoffice_deposit_register`, `SB_BILL.dbo.HEADOFFICE_DEPOSIT_UPLOAD` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/headofficedeposit/repository/HeadOfficeDepositRegistrationMapper.kt#L60) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b7e1315b1985158d) |
| `SB_BILL.dbo.UspBill_HeadOffice_Deposit_FileSave_INSERT` | @FILENAME varchar(100), @FILEPATH varchar(300), @SWNO int, @IDX int OUT | 정의 참조 `SB_BILL.dbo.HEADOFFICE_DEPOSIT_UPLOAD` · 정적 쓰기 `SB_BILL.dbo.HEADOFFICE_DEPOSIT_UPLOAD` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/headofficedeposit/repository/HeadOfficeDepositRegistrationMapper.kt#L42) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-a9e853d6c6961e27) |
| `smartwork.dbo.headoffice_deposit_register` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL INSERT INTO | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/headofficedeposit/repository/HeadOfficeDepositRegistrationMapper.kt#L145) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-748cfdfef3387e76) |
| `smartwork.dbo.headoffice_deposit_register_process` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL INSERT INTO | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/headofficedeposit/repository/HeadOfficeDepositRegistrationMapper.kt#L160) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-d5b2a63e22e82e4e) |
| `smartwork.dbo.deposit_deduction` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/headofficedeposit/repository/HeadOfficeDepositRegistrationMapper.kt#L89) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-cc106276f1e9c83e) |
| `SB_BILL.dbo.HEADOFFICE_DEPOSIT_UPLOAD` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL DELETE FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/headofficedeposit/repository/HeadOfficeDepositRegistrationMapper.kt#L101) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-c7e863ba93448043) |
| `smartwork.dbo.usp_bill_head_office_deposit_auto_match_select` | @deposit_month varchar(6), @deposit_amount money, @deposit_name varchar(100) | 정의 참조 `SmartBill3.dbo.COMPANY`, `SB_BILL.dbo.INVOICE`, `SB_BILL.dbo.PAYMENT` · 쓰기 구문 존재 · 대상 별칭 또는 하위 정의 확인 · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/headofficedeposit/repository/HeadOfficeDepositRegistrationMapper.kt#L421) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-36c8dd1a881425b6) |
| `SB_BILL_LINKED.dbo.CRM_T_CR_OS_IV` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/headofficedeposit/repository/HeadOfficeDepositRegistrationMapper.kt#L474) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-d49e19cdab81cd25) |
| `SmartBill3.dbo.COMPANY` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/headofficedeposit/repository/HeadOfficeDepositRegistrationMapper.kt#L474) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-0e6fcaa6b5086c07) |
| `SB_BILL.dbo.HEADOFFICE_DEPOSIT` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/headofficedeposit/repository/HeadOfficeDepositRegistrationMapper.kt#L128) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-729ca08029e7d734) |
| `smartwork.dbo.action_reason` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL INSERT INTO | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/shared/actionreason/repository/ActionReasonMapper.kt#L16) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b0430106ffe0743f) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 업로드 일자, 파일명, 총 건수, 자동매칭, 입금등록, 업로드 상태 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 서비스 현황 > 입금관리 > 본사 입금 등록의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 파일 업로드 중 오류가 발생했습니다. | 업로드 일자, 파일명, 총 건수, 자동매칭, 입금등록, 업로드 상태 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 삭제할 항목을 선택해주세요. | 업로드 일자, 파일명, 총 건수, 자동매칭, 입금등록, 업로드 상태 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 파일 삭제 중 오류가 발생했습니다. | 업로드 일자, 파일명, 총 건수, 자동매칭, 입금등록, 업로드 상태 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/PaymentRoutes.tsx#L64) · [HeadOfficeDepositRegistrationPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/HeadOfficeDepositRegistrationPage.tsx#L98) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/headOfficeDepositRegistrationApi.ts#L46) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/headOfficeDepositRegistrationApi.ts#L59) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/headOfficeDepositRegistrationApi.ts#L69) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 11개 중 개발 메타데이터 확인 11개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-4cc65ea9dd0950f6) | Demo 메타데이터 10/11개 확인 · 미확인 1개 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

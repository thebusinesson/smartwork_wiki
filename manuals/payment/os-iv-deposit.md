# [입금·예치금·배분·취소·환불] 단발성 입금 관리 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

단발성 청구별 입금 현황을 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 입금·예치금·배분·취소·환불 |
| 언제 사용하는가 | 단발성 입금 관리 목록 조회, 단발성 입금 관리 목록 다운로드, 단발성 CRM 통보 재시도 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 청구월, 입금일, 업체 조건, 입금 방식, 입금 상태, 청구코드 |
| 업무 흐름 | 단발성 입금 관리 목록 조회, 단발성 입금 관리 목록 다운로드, 단발성 CRM 통보 재시도 |
| 이 페이지의 역할 | 조회 · 단발성 입금 관리 목록 조회 |
| 판단 결과·다음 업무 | 현재 화면에서 결과를 확인한다. |
| 다른 화면과의 구분 | 같은 경로에서 열리는 조회·팝업은 이 문서에서 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 단발성 청구별 입금 현황을 조회한다. |
| 메뉴·화면 경로 | 서비스 현황 > 입금관리 > 단발성 입금 관리 · `/payment/os-iv-deposit` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | 현재 화면에서 결과를 확인한다. |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/payment/os-iv-deposit` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 단발성 입금 관리 목록 조회 | `/payment/os-iv-deposit` `VIEW` | `OsIvPaymentSearchRequest` `page`, `pageSize`, `chargeFrom`, `chargeTo`, `payFrom`, `payTo`, `searchCode`, `searchText`, `channel`, `payStatus` |
| 단발성 입금 관리 목록 다운로드 | `/payment/os-iv-deposit` `EXCEL_DOWNLOAD` | `OsIvPaymentSearchRequest` `page`, `pageSize`, `chargeFrom`, `chargeTo`, `payFrom`, `payTo`, `searchCode`, `searchText`, `channel`, `payStatus` |
| 단발성 CRM 통보 재시도 | `/payment/os-iv-deposit` `PROCESS` | `osIvPaymentIdx: Long` |
| 단발성 입금 목록 원문 조회 | `/payment/os-iv-deposit` / `UNMASK` | `osIvPaymentIdx`, `field` |

코드에서 확인한 버튼·작업명은 **연동 재시도**, **검색**, **다운로드**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **서비스 현황 > 입금관리 > 단발성 입금 관리**를 연다. `/payment/os-iv-deposit`를 연다.
2. **청구월**, **입금일**, **업체 조건**, **입금 방식**, **입금 상태** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색**, **다운로드** 중 해당 버튼을 선택한다.
3. **단발성 입금 관리 목록 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 청구월 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/AdHocDepositManagementListPage.tsx#L129) |
| 입금일 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/AdHocDepositManagementListPage.tsx#L140) |
| 업체 조건 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/AdHocDepositManagementListPage.tsx#L150) |
| 입금 방식 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/AdHocDepositManagementListPage.tsx#L175) |
| 입금 상태 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/AdHocDepositManagementListPage.tsx#L185) |
| 청구코드 | 출력 | 조회 응답 기준 | 화면 필드 `crCd` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/AdHocDepositManagementListPage.tsx#L277) |
| 서비스명 | 출력 | 조회 응답 기준 | 화면 필드 `serviceNm` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/AdHocDepositManagementListPage.tsx#L278) |
| 회사명 | 출력 | 조회 응답 기준 | 화면 필드 `comName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/AdHocDepositManagementListPage.tsx#L279) |
| 사업자번호 | 출력 | 조회 응답 기준 | 화면 필드 `comRegno` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/AdHocDepositManagementListPage.tsx#L280) |
| 입금담당자 | 출력 | 조회 응답 기준 | 화면 필드 `swName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/AdHocDepositManagementListPage.tsx#L282) |
| 청구액 | 출력 | 조회 응답 기준 | 화면 필드 `totalAmt` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/AdHocDepositManagementListPage.tsx#L293) |
| 입금액 | 출력 | 조회 응답 기준 | 화면 필드 `payAmount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/AdHocDepositManagementListPage.tsx#L295) |
| 입금상태 | 입력 또는 선택 | API 기본값 null | API 요청 `payStatus` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/AdHocDepositManagementListPage.tsx#L298) |
| 입금방식 | 입력 또는 선택 | API 기본값 null | API 요청 `channel` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/AdHocDepositManagementListPage.tsx#L299) |
| 입금자 | 출력 | 조회 응답 기준 | 화면 필드 `depositName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/AdHocDepositManagementListPage.tsx#L302) |
| CRM 통보 | 출력 | 조회 응답 기준 | 화면 필드 `crmResult` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/AdHocDepositManagementListPage.tsx#L315) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 단발성 입금 관리 목록 조회 | `GET /api/v1/status/payment/os-iv-deposit` · `/payment/os-iv-deposit` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/osivdeposit/OsIvDepositController.kt#L82) | `OsIvPaymentSearchRequest` `page`, `pageSize`, `chargeFrom`, `chargeTo`, `payFrom`, `payTo`, `searchCode`, `searchText`, `channel`, `payStatus` → `success`, `data`, `error`, `content`, `totalElements` | `smartwork.dbo.UspBill_OsIvPaymentList_SELECT` |
| 단발성 입금 관리 목록 다운로드 | `GET /api/v1/status/payment/os-iv-deposit/download` · `/payment/os-iv-deposit` `EXCEL_DOWNLOAD` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/osivdeposit/OsIvDepositController.kt#L97) | `OsIvPaymentSearchRequest` `page`, `pageSize`, `chargeFrom`, `chargeTo`, `payFrom`, `payTo`, `searchCode`, `searchText`, `channel`, `payStatus` → 파일 또는 오류 응답 | `smartwork.dbo.UspBill_OsIvPaymentList_SELECT` |
| 단발성 CRM 통보 재시도 | `POST /api/v1/status/payment/os-iv-deposit/{osIvPaymentIdx}/crm-retry` · `/payment/os-iv-deposit` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/osivdeposit/OsIvDepositController.kt#L251) | `osIvPaymentIdx: Long` → `success`, `data`, `error`, `osIvPaymentIdx`, `crmNotified`, `crmMessage` | `smartwork.dbo.OS_IV_PAYMENT`, `SB_BILL_LINKED.dbo.CRM_API_LOG` · 정의에서 확인한 쓰기 `SB_BILL_LINKED.dbo.CRM_API_LOG` · 코드 연계 CrmOsIvApiClient |
| 단발성 입금 목록 원문 조회 | `POST /api/v1/status/payment/os-iv-deposit/{osIvPaymentIdx}/sensitive-values/reveal` · `/payment/os-iv-deposit` / `UNMASK` · [화면 컴포넌트](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/AdHocDepositManagementListPage.tsx#L305) · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/osivdeposit/OsIvDepositController.kt#L261) | `osIvPaymentIdx`, `field` → 요청한 항목의 원문 응답 | 권한 검사 후 대상 값을 조회하고 감사 기록을 남긴다. |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.UspBill_OsIvPaymentList_SELECT` | @PAGE int, @TOP int, @CHARGE_FROM varchar(6), @CHARGE_TO varchar(6), @PAY_FROM varchar(8), @PAY_TO varchar(8), @SEARCH_CODE varchar(1), @SEARCH_TEXT varchar(100), @CHANNEL varchar(50), @PAY_STATUS varchar(50) | 정의 참조 `SB_BILL_LINKED.dbo.CRM_T_CR_OS_IV`, `smartwork.dbo.OS_IV_PAYMENT`, `office.dbo.SAWON` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/osivdeposit/repository/OsIvDepositMapper.kt#L88) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-74cc68669ab0d9dc) |
| `smartwork.dbo.OS_IV_PAYMENT` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/osivdeposit/repository/OsIvDepositMapper.kt#L130) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-11a2c0b6456c84a6) |
| `SB_BILL_LINKED.dbo.CRM_API_LOG` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL INSERT INTO | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/osivdeposit/repository/CrmApiLogMapper.kt#L25) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-49c412a8654ee2db) |
| `SB_BILL_LINKED.dbo.CRM_T_CR_OS_IV` | 개발 컬럼 메타데이터 확인 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/osivdeposit/repository/OsIvDepositMapper.kt#L206) |
| `office.dbo.SAWON` | 개발 컬럼 메타데이터 확인 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/osivdeposit/repository/OsIvDepositMapper.kt#L225) |
| `smartwork.dbo.usp_sw_log_access_event_insert` | @EVENT_TYPE varchar(30) IN, @STATUS varchar(20) IN, @USER_ID bigint IN, @MEMBER_ID nvarchar(50) IN, @USER_NAME nvarchar(100) IN, @DEPARTMENT_NAME nvarchar(100) IN, @PAGE_TITLE nvarchar(200) IN, @PATH nvarchar(500) IN, @MENU_PATH nvarchar(500) IN, @MENU_LABEL nvarchar(200) IN, @CATEGORY_NAME nvarchar(200) IN, @SUB_CATEGORY_NAME nvarchar(200) IN, @MENU_ORDER int IN, @IP_ADDRESS varchar(45) IN, @USER_AGENT nvarchar(1000) IN, @BROWSER varchar(100) IN, @OS varchar(100) IN, @REFERRER nvarchar(500) IN, @DETAIL nvarchar(1000) IN, @RESULT int OUT, @COUNTS_AS_VISIT bit IN | 원문 조회 또는 감사 흐름에서 호출 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/logmanagement/repository/LogManagementMapper.kt#L92) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 청구월, 입금일, 업체 조건, 입금 방식, 입금 상태, 청구코드 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 서비스 현황 > 입금관리 > 단발성 입금 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| CRM 연동 재시도에 실패했습니다. 잠시 후 다시 시도해 주세요. | 청구월, 입금일, 업체 조건, 입금 방식, 입금 상태, 청구코드 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 다운로드할 데이터가 없습니다. | 청구월, 입금일, 업체 조건, 입금 방식, 입금 상태, 청구코드 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 다운로드 중 오류가 발생했습니다. | 청구월, 입금일, 업체 조건, 입금 방식, 입금 상태, 청구코드 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 검색 결과가 없습니다. | 청구월, 입금일, 업체 조건, 입금 방식, 입금 상태, 청구코드 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/PaymentRoutes.tsx#L67) · [AdHocDepositManagementListPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/AdHocDepositManagementListPage.tsx#L92) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/adHocDepositManagementApi.ts#L39) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/adHocDepositManagementApi.ts#L60) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/osIvDepositApi.ts#L101) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 3개 중 개발 메타데이터 확인 3개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-030f355f870317ec) | Demo 메타데이터 4/6개 확인 · 미확인 2개 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

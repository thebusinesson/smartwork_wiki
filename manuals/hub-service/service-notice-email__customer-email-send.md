# [서비스 공지 메일과 발송 이력] 고객 이메일 발송 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

mailType 에 따라 세금계산서/게스트/보나뱅크/서비스공지/CMS 실패안내 메일을 발송한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 서비스 공지 메일과 발송 이력 |
| 언제 사용하는가 | 메일 발송 (통합) 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 제목, 메일 내용 |
| 업무 흐름 | 메일 발송 (통합) |
| 이 페이지의 역할 | 조회 · 메일 발송 (통합) |
| 판단 결과·다음 업무 | 현재 화면에서 결과를 확인한다. |
| 다른 화면과의 구분 | 같은 경로에서 열리는 조회·팝업은 이 문서에서 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 확인 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/service-notice-email/components/customerEmailSend/CustomerEmailSendForm.tsx#L166) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | mailType 에 따라 세금계산서/게스트/보나뱅크/서비스공지/CMS 실패안내 메일을 발송한다. |
| 메뉴·화면 경로 | 연동 서비스 관리 > 서비스 공지 메일관리 > 고객 이메일 발송 · `/hub-service/service-notice-email/customer-email-send` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | 현재 화면에서 결과를 확인한다. |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/hub-service/service-notice-email/customer-email-send` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 메일 발송 (통합) | 정적 메뉴 액션 미확인 · Controller·공통 보안 검사 확인 | `MailSendRequest` `mailType`, `ids`, `items`, `emailAddress`, `title`, `emailContent`, `targetId` · 서버 필수 `mailType` |

코드에서 확인한 버튼·작업명은 **메일 발송**, **확인**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **연동 서비스 관리 > 서비스 공지 메일관리 > 고객 이메일 발송**를 연다. `/hub-service/service-notice-email/customer-email-send`를 연다.
2. **제목**, **메일 내용** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **확인** 중 해당 버튼을 선택한다.
3. **메일 발송 (통합)**을 실행하기 전에 변경 대상과 입력값을 확인한다. 표시되는 **메일이 발송되었습니다.** 메시지와 대상 상태를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 메일 내용을 입력해 주세요 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/service-notice-email/components/customerEmailSend/CustomerEmailSendForm.tsx#L42) |
| 제목 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/service-notice-email/components/customerEmailSend/CustomerEmailSendForm.tsx#L119) |
| 제목을 입력해 주세요 (최대 100바이트) | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/service-notice-email/components/customerEmailSend/CustomerEmailSendForm.tsx#L123) |
| 메일 내용 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/service-notice-email/components/customerEmailSend/CustomerEmailSendForm.tsx#L134) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 메일 발송 (통합) | `POST /api/v1/mail/send` · 정적 메뉴 액션 미확인 · Controller·공통 보안 검사 확인 · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/shared/mail/MailController.kt#L48) · [기존 상세 계약](../../references/api-contracts.md#api220) | `MailSendRequest` `mailType`, `ids`, `items`, `emailAddress`, `title`, `emailContent`, `targetId` · 서버 필수 `mailType` → `success`, `data`, `error`, `isAllSuccess`, `successCount`, `failedCount`, `message` | `SB_DTI.dbo.DTI_HEADER_CUB`, `SB_COMMON.dbo.upSBAdm_LstDTI04`, `SB_DTI_DW.dbo.DTI_HEADER_CUB`, `SB_COMMON.dbo.upSBAdm_LstDTI04_DW`, `office.dbo.upSM_mailSendList` 외 9개 · 정의에서 확인한 쓰기 `SB_DTI_LOG.dbo.DTI_CUSTOMER_PWD`, `office.dbo.ServiceMail_Send` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `SB_DTI.dbo.DTI_HEADER_CUB` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM · 정의 참조 `sb_dti.dbo.dti_header_cub_2023_07`, `sb_dti.dbo.dti_header_cub_part`, `sb_dti.dbo.dti_header_cub_prev_buffer` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/repository/TaxInvoiceMapper.kt#L453) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-9b704ca2245fb3f1) |
| `SB_COMMON.dbo.upSBAdm_LstDTI04` | @DTI_WDAY varchar(10), @DTI_IDX int | 정의 참조 `SB_DTI_LOG.dbo.DTI_CUSTOMER_PWD`, `SB_DTI.dbo.DTI_HEADER_CUB`, `SmartBill3.dbo.fnRanByEmail`, `SB_DTI_LOG.dbo.V_DTI_CUSTOMER_PWD` · 정적 쓰기 `SB_DTI_LOG.dbo.DTI_CUSTOMER_PWD` · 하위 호출 `SmartBill3.dbo.fnRanByEmail` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/taxinvoice/repository/BonabankTaxInvoiceMapper.kt#L231) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b70e5915dd1d37bd) |
| `SB_DTI_DW.dbo.DTI_HEADER_CUB` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM · 정의 참조 `sb_dti.dbo.dti_header_cub_2020_01`, `sb_dti.dbo.dti_header_cub_2020_02`, `sb_dti.dbo.dti_header_cub_2020_03`, `sb_dti.dbo.dti_header_cub_2020_04`, `sb_dti.dbo.dti_header_cub_2020_05` 외 37개 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/legacytaxinvoice/repository/LegacyTaxInvoiceMapper.kt#L332) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-ad6e47ef0f0ed643) |
| `SB_COMMON.dbo.upSBAdm_LstDTI04_DW` | @DTI_WDAY varchar(10), @DTI_IDX int | 정의 참조 `SB_DTI_LOG.dbo.DTI_CUSTOMER_PWD`, `SB_DTI_DW.dbo.DTI_HEADER_CUB`, `SmartBill3.dbo.fnRanByEmail`, `SB_DTI_LOG.dbo.V_DTI_CUSTOMER_PWD` · 정적 쓰기 `SB_DTI_LOG.dbo.DTI_CUSTOMER_PWD` · 하위 호출 `SmartBill3.dbo.fnRanByEmail` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/legacytaxinvoice/repository/LegacyTaxInvoiceMapper.kt#L356) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-4999b219d6165194) |
| `office.dbo.upSM_mailSendList` | @DIV varchar(10) | 정의 참조 `office.dbo.ServiceMail` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/servicenoticemail/repository/EmailVendorMapper.kt#L114) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-80ee241109d15682) |
| `office.dbo.upSM_mailSend_Insert` | @TITLE varchar(100), @CONTENT text, @CUSER varchar(20), @RESULT int OUT | 정의 참조 `office.dbo.ServiceMail_Send` · 정적 쓰기 `office.dbo.ServiceMail_Send` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/servicenoticemail/repository/EmailVendorMapper.kt#L125) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-51da5c7d65aa6b46) |
| `SmartBill3.dbo.CMS_EA14` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb14AccountMapper.kt#L55) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3229f827e97f2667) |
| `SmartBill3.dbo.CMS_EA14_DETAIL_CUB` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb14AccountMapper.kt#L166) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-9a14be878da3eade) |
| `SmartBill3.dbo.COMPANY` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb14AccountMapper.kt#L166) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-0e6fcaa6b5086c07) |
| `SmartBill3.dbo.MEMBER` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb14AccountMapper.kt#L166) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-9042ff61b257b012) |
| `SmartBill3.dbo.COMMON_CODE` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb14AccountMapper.kt#L166) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-49b15682b4d4770c) |
| `SB_BILL.dbo.BILL_COMMON_CODE` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb14AccountMapper.kt#L166) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b05907f373842dd1) |
| `SmartBill3.dbo.CMS_EA22_DETAIL_CUB` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmseb22/repository/Eb22Mapper.kt#L281) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-2d8296b635adbf7b) |
| `SmartBill3.dbo.CMS_EA22` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmseb22/repository/Eb22Mapper.kt#L281) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-8cc8fe0c5cb8684a) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 제목, 메일 내용 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 연동 서비스 관리 > 서비스 공지 메일관리 > 고객 이메일 발송의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 메일 발송에 실패했습니다. | 제목, 메일 내용 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 메일 발송이 취소되었습니다. | 제목, 메일 내용 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/IntegrationRoutes.tsx#L130) · [CustomerEmailSendPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/service-notice-email/pages/CustomerEmailSendPage.tsx#L5) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/api/mailApi.ts#L45) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 14개 중 개발 메타데이터 확인 14개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-c6b9f167bc60a3ab) | Demo 메타데이터 14/14개 확인 · Dev와 계약 차이 3개 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

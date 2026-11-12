# [연동 문의·점검·라우팅·복구] 자동이체 예외업체 등록 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

자동이체 예외업체 등록에서 대상과 입력값을 확인해 **자동이체 예외업체 등록** 업무를 처리한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 연동 문의·점검·라우팅·복구 |
| 언제 사용하는가 | 자동이체 예외업체 등록용 회사 조회, 자동이체 예외업체 등록 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 사업자번호, 회사명 |
| 업무 흐름 | 자동이체 예외업체 등록용 회사 조회, 자동이체 예외업체 등록 |
| 이 페이지의 역할 | 등록 · 자동이체 예외업체 등록 |
| 판단 결과·다음 업무 | [자동이체 예외 설정](auto-transfer-exception.md) |
| 다른 화면과의 구분 | 연동 서비스 관리 > 연동 서비스 관리 > 자동이체 예외 설정에서 사용하는 등록 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 자동이체 예외업체 등록에서 대상과 입력값을 확인해 **자동이체 예외업체 등록** 업무를 처리한다. |
| 메뉴·화면 경로 | 연동 서비스 관리 > 연동 서비스 관리 > 자동이체 예외 설정 · `/hub-service/auto-transfer-exception/new` |
| 화면 유형·담당 | 등록 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [자동이체 예외 설정](auto-transfer-exception.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/hub-service/auto-transfer-exception` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 자동이체 예외업체 등록용 회사 조회 | `/hub-service/auto-transfer-exception` `VIEW` | `businessNumber: String` |
| 자동이체 예외업체 등록 | `/hub-service/auto-transfer-exception` `PROCESS` | `AutoTransferExceptionCreateRequest` `businessNumber` · 서버 필수 `businessNumber` |

코드에서 확인한 버튼·작업명은 **검색**, **저장**, **목록**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [자동이체 예외 설정](auto-transfer-exception.md)에서 대상 또는 작업을 선택한다. `/hub-service/auto-transfer-exception/new`를 연다.
2. **사업자번호** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색**, **저장** 중 해당 버튼을 선택한다.
3. **자동이체 예외업체 등록**을 실행하기 전에 변경 대상과 입력값을 확인한다. 표시되는 **자동이체 예외업체를 등록하였습니다.** 메시지와 대상 상태를 확인한다.
4. 후속 조회나 목록 복귀가 필요하면 [자동이체 예외 설정](auto-transfer-exception.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 사업자번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/autoTransferException/components/register/RegistrationForm.tsx#L29) |
| 회사명 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/autoTransferException/components/detail/CompanyInfoSection.tsx#L32) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 자동이체 예외업체 등록용 회사 조회 | `GET /api/v1/hub-service/auto-transfer-exception/search-company` · `/hub-service/auto-transfer-exception` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/autotransferexception/AutoTransferExceptionController.kt#L95) | `businessNumber: String` → `success`, `data`, `error`, `businessNumber`, `companyName`, `isSmartbillMember`, `exists` | `SmartBill3.dbo.COMPANY` |
| 자동이체 예외업체 등록 | `POST /api/v1/hub-service/auto-transfer-exception` · `/hub-service/auto-transfer-exception` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/autotransferexception/AutoTransferExceptionController.kt#L109) | `AutoTransferExceptionCreateRequest` `businessNumber` · 서버 필수 `businessNumber` → `success`, `data`, `error`, `id`, `businessNumber`, `companyName`, `isIntegrated`, `isSmartbillMember`, `registeredAt`, `registeredBy`, `deletedAt`, `deletedBy` | `office.dbo.SSP_EXCEPT_INSERT`, `office.dbo.SSP_AUTO_EXCEPT` · 정의에서 확인한 쓰기 `office.dbo.MNG_COMPANY_EXCEPT`, `office.dbo.MNG_COMPANY_EXCEPT_HIS` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `SmartBill3.dbo.COMPANY` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/autotransferexception/repository/AutoTransferExceptionMapper.kt#L76) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-0e6fcaa6b5086c07) |
| `office.dbo.SSP_EXCEPT_INSERT` | @COM_REGNO varchar(13), @EXCEPT_CODE1 varchar(20), @EXCEPT_CODE2 varchar(20), @EXCEPT_CODE3 varchar(20), @EXCEPT_CODE4 varchar(20), @CUSER varchar(20), @DIVISION varchar(7), @RESULT varchar(1) OUT | 정의 참조 `office.dbo.MNG_COMPANY_EXCEPT`, `office.dbo.MNG_COMPANY_EXCEPT_HIS` · 정적 쓰기 `office.dbo.MNG_COMPANY_EXCEPT`, `office.dbo.MNG_COMPANY_EXCEPT_HIS` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/autotransferexception/repository/AutoTransferExceptionMapper.kt#L57) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-288b8718040da13a) |
| `office.dbo.SSP_AUTO_EXCEPT` | @DIV varchar(7), @TXTSEARCH varchar(70), @PAGENUM int, @PAGESIZE int | 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/autotransferexception/repository/AutoTransferExceptionMapper.kt#L40) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-ed592f13a1367218) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 사업자번호, 회사명 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 연동 서비스 관리 > 연동 서비스 관리 > 자동이체 예외 설정의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 회사 조회에 실패했습니다. | 사업자번호, 회사명 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 자동이체 예외업체 등록을 취소하였습니다. | 사업자번호, 회사명 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/IntegrationRoutes.tsx#L149) · [AutoTransferExceptionRegisterPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/autoTransferException/AutoTransferExceptionRegisterPage.tsx#L8) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/api/autoTransferExceptionApi.ts#L100) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/api/autoTransferExceptionApi.ts#L60) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 3개 중 개발 메타데이터 확인 3개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-33e9a906811aeab3) | Demo 메타데이터 3/3개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

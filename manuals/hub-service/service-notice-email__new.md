# [서비스 공지 메일과 발송 이력] 메일 발송 업체 관리 등록 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

메일 발송 업체 관리 등록에서 대상과 입력값을 확인해 **메일링 업체 등록** 업무를 처리한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 서비스 공지 메일과 발송 이력 |
| 언제 사용하는가 | 사업자번호 조회, 메일링 업체 등록 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 사업자번호, 회사명, 담당자명, 이메일 |
| 업무 흐름 | 사업자번호 조회, 메일링 업체 등록 |
| 이 페이지의 역할 | 등록 · 메일링 업체 등록 |
| 판단 결과·다음 업무 | [메일 발송 업체 관리](service-notice-email.md) |
| 다른 화면과의 구분 | 연동 서비스 관리 > 서비스 공지 메일관리 > 메일 발송 업체 관리에서 사용하는 등록 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 메일 발송 업체 관리 등록에서 대상과 입력값을 확인해 **메일링 업체 등록** 업무를 처리한다. |
| 메뉴·화면 경로 | 연동 서비스 관리 > 서비스 공지 메일관리 > 메일 발송 업체 관리 · `/hub-service/service-notice-email/new` |
| 화면 유형·담당 | 등록 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [메일 발송 업체 관리](service-notice-email.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/hub-service/service-notice-email` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 사업자번호 조회 | `/hub-service/service-notice-email` `VIEW` | `businessNumber: String` |
| 메일링 업체 등록 | `/hub-service/service-notice-email` `PROCESS` | `CreateEmailVendorRequest` `businessNumber`, `companyName`, `contactName`, `email` · 서버 필수 `businessNumber`, `contactName`, `email` |

코드에서 확인한 버튼·작업명은 **검색**, **취소**, **저장**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [메일 발송 업체 관리](service-notice-email.md)에서 대상 또는 작업을 선택한다. `/hub-service/service-notice-email/new`를 연다.
2. **사업자번호** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색**, **저장** 중 해당 버튼을 선택한다.
3. **메일링 업체 등록**을 실행하기 전에 변경 대상과 입력값을 확인한다. 표시되는 **메일 발송 업체 정보가 등록되었습니다.** 메시지와 대상 상태를 확인한다.
4. 후속 조회나 목록 복귀가 필요하면 [메일 발송 업체 관리](service-notice-email.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 사업자번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/serviceNoticeEmail/ServiceNoticeEmailCreatePage.tsx#L13) |
| 회사명 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/serviceNoticeEmail/components/common/EmailVendorInfoSection.tsx#L36) |
| 담당자명 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/serviceNoticeEmail/components/common/EmailVendorInfoSection.tsx#L40) |
| 담당자명을 입력하세요 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/serviceNoticeEmail/components/common/EmailVendorInfoSection.tsx#L48) |
| 이메일 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/serviceNoticeEmail/components/common/EmailVendorInfoSection.tsx#L57) |
| 이메일을 입력하세요 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/serviceNoticeEmail/components/common/EmailVendorInfoSection.tsx#L66) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 사업자번호 조회 | `GET /api/v1/service-notice-email/search-business-number` · `/hub-service/service-notice-email` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/servicenoticemail/ServiceNoticeEmailVendorController.kt#L89) | `businessNumber: String` → `success`, `data`, `error`, `businessNumber`, `companyName` | `office.dbo.upSM_CompanyInfo` |
| 메일링 업체 등록 | `POST /api/v1/service-notice-email` · `/hub-service/service-notice-email` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/servicenoticemail/ServiceNoticeEmailVendorController.kt#L134) | `CreateEmailVendorRequest` `businessNumber`, `companyName`, `contactName`, `email` · 서버 필수 `businessNumber`, `contactName`, `email` → `success`, `data`, `error`, `id`, `businessNumber`, `companyName`, `contactName`, `email`, `createdAt`, `createdBy`, `updatedAt`, `updatedBy` | `office.dbo.upSM_mailCom_Insert`, `office.dbo.upSM_mailComList` · 정의에서 확인한 쓰기 `office.dbo.ServiceMail` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `office.dbo.upSM_CompanyInfo` | @COM_REGNO varchar(10) | 정의 참조 `SmartBill3.dbo.COMPANY` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/servicenoticemail/repository/EmailVendorMapper.kt#L88) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-68e3093344a5df50) |
| `office.dbo.upSM_mailCom_Insert` | @COM_REGNO varchar(13), @Email varchar(70), @Name varchar(35), @CUSER varchar(20), @NO int, @DIVISION varchar(7), @RESULT varchar(1) OUT | 정의 참조 `office.dbo.ServiceMail` · 정적 쓰기 `office.dbo.ServiceMail` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/servicenoticemail/repository/EmailVendorMapper.kt#L99) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-bcff33a0d6972116) |
| `office.dbo.upSM_mailComList` | @PAGENUM int, @PAGESIZE int | 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/servicenoticemail/repository/EmailVendorMapper.kt#L53) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-dcf5c0aba79a23a8) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 사업자번호, 회사명, 담당자명, 이메일 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 연동 서비스 관리 > 서비스 공지 메일관리 > 메일 발송 업체 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 등록에 실패했습니다. | 사업자번호, 회사명, 담당자명, 이메일 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/IntegrationRoutes.tsx#L128) · [ServiceNoticeEmailCreatePage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/serviceNoticeEmail/ServiceNoticeEmailCreatePage.tsx#L29) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/api/serviceNoticeEmailApi.ts#L48) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/api/serviceNoticeEmailApi.ts#L55) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 3개 중 개발 메타데이터 확인 3개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-f67ede828798f694) | Demo 메타데이터 3/3개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

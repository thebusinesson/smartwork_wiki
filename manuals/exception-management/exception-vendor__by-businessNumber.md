# [업체·비회원 예외와 SMS 수신거부] [업체]예외 처리 정보 상세 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

[업체]예외 처리 정보 상세에서 **예외 업체 상세 조회 (등록·수정 화면 진입 시에도 동일 엔드포인트 사용)** 결과를 확인한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 업체·비회원 예외와 SMS 수신거부 |
| 언제 사용하는가 | 예외 업체 상세 조회 (등록·수정 화면 진입 시에도 동일 엔드포인트 사용), 예외 업체 저장 (신규 등록·수정·삭제 모두 처리) 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 사업자번호, 회사명, 예외처리 등록일시 :, 결재번호 : |
| 업무 흐름 | 예외 업체 상세 조회 (등록·수정 화면 진입 시에도 동일 엔드포인트 사용), 예외 업체 저장 (신규 등록·수정·삭제 모두 처리) |
| 이 페이지의 역할 | 상세 · 예외 업체 상세 조회 (등록·수정 화면 진입 시에도 동일 엔드포인트 사용) |
| 판단 결과·다음 업무 | [[업체]예외 처리 정보](exception-vendor.md) |
| 다른 화면과의 구분 | SB 고객관리 > 예외 관리 > [업체]예외 처리 정보에서 사용하는 상세 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 확인 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/exception/components/IndividualRegistrationTab.tsx#L369) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | [업체]예외 처리 정보 상세에서 **예외 업체 상세 조회 (등록·수정 화면 진입 시에도 동일 엔드포인트 사용)** 결과를 확인한다. |
| 메뉴·화면 경로 | SB 고객관리 > 예외 관리 > [업체]예외 처리 정보 · `/exception-management/exception-vendor/:businessNumber` · 경로 변수 `businessNumber` |
| 화면 유형·담당 | 상세 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [[업체]예외 처리 정보](exception-vendor.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/exception-management/exception-vendor` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `businessNumber` |
| 예외 업체 상세 조회 (등록·수정 화면 진입 시에도 동일 엔드포인트 사용) | `/exception-management/exception-vendor` `VIEW` | `businessNumber: String` |
| 예외 업체 저장 (신규 등록·수정·삭제 모두 처리) | `/exception-management/exception-vendor` `PROCESS` | `businessNumber: String` · `ExceptCompanySaveRequest` `businessNumber`, `services` |

코드에서 확인한 버튼·작업명은 **검색**, **저장**, **이전**, **확인**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [[업체]예외 처리 정보](exception-vendor.md)에서 대상 또는 작업을 선택한다. `/exception-management/exception-vendor/:businessNumber`에서 이전 화면이 전달한 `businessNumber`와 현재 대상을 확인한다.
2. **사업자번호**, **회사명**, **예외처리 등록일시 :**, **결재번호 :** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색**, **저장**, **확인** 중 해당 버튼을 선택한다.
3. **예외 업체 상세 조회 (등록·수정 화면 진입 시에도 동일 엔드포인트 사용)** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [[업체]예외 처리 정보](exception-vendor.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `businessNumber` |
| 사업자번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/exception/components/IndividualRegistrationTab.tsx#L228) |
| 회사명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/exception/components/IndividualRegistrationTab.tsx#L258) |
| 예외처리 등록일시 : | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/exception/components/IndividualRegistrationTab.tsx#L287) |
| 결재번호 : | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/exception/components/IndividualRegistrationTab.tsx#L321) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 예외 업체 상세 조회 (등록·수정 화면 진입 시에도 동일 엔드포인트 사용) | `GET /api/v1/customer/exception-companies/{businessNumber}` · `/exception-management/exception-vendor` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/customer/exception/ExceptionVendorController.kt#L93) | `businessNumber: String` → `success`, `data`, `error`, `businessNumber`, `companyName`, `taxFreeAllowed`, `isRegistered`, `lastProcessedDate`, `services` | `smartwork.dbo.usp_except_company_detail_select` |
| 예외 업체 저장 (신규 등록·수정·삭제 모두 처리) | `PUT /api/v1/customer/exception-companies/{businessNumber}` · `/exception-management/exception-vendor` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/customer/exception/ExceptionVendorController.kt#L150) | `businessNumber: String` · `ExceptCompanySaveRequest` `businessNumber`, `services` → `success`, `data`, `error` | `office.dbo.MNG_COMPANY_EXCEPT`, `office.dbo.SSP_EXCEPT_COMPANY_MANAGE`, `smartwork.dbo.mng_company_except_approval` · 정의에서 확인한 쓰기 `office.dbo.MNG_COMPANY_EXCEPT`, `office.dbo.MNG_COMPANY_EXCEPT_HIS`, `smartwork.dbo.mng_company_except_approval` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.usp_except_company_detail_select` | @COM_REGNO varchar(13) | 정의 참조 `SmartBill3.dbo.COMPANY`, `office.dbo.MNG_COMPANY_EXCEPT`, `smartwork.dbo.mng_company_except_approval`, `SB_DTI.dbo.NTS_TRANSMIT_METHOD` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/exception/repository/ExceptCompanyMapper.kt#L69) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-2223d570294312d7) |
| `office.dbo.MNG_COMPANY_EXCEPT` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/exception/repository/ExceptCompanyMapper.kt#L78) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3d8c0e9716c73ec8) |
| `office.dbo.SSP_EXCEPT_COMPANY_MANAGE` | @COM_REGNO varchar(13), @DTI_EXCEPT varchar(20), @DCT_EXCEPT varchar(20), @DRC_EXCEPT varchar(20), @BANNER_EXCEPT varchar(20), @TAXFREE_EXCEPT varchar(20), @EMAIL_EXCEPT varchar(20), @CUSER varchar(20), @DIV varchar(7), @SBP_EXCEPT varchar(20), @INVOICE_EXCEPT varchar(20), @KEYWORD_EXCEPT varchar(20), @RESULT varchar(1) OUT | 정의 참조 `office.dbo.MNG_COMPANY_EXCEPT`, `office.dbo.MNG_COMPANY_EXCEPT_HIS` · 정적 쓰기 `office.dbo.MNG_COMPANY_EXCEPT`, `office.dbo.MNG_COMPANY_EXCEPT_HIS` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/exception/repository/ExceptCompanyMapper.kt#L89) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-4ecc113ee4871463) |
| `smartwork.dbo.mng_company_except_approval` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL DELETE FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/exception/repository/ExceptCompanyMapper.kt#L112) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-537d9baea7d108e8) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 사업자번호, 회사명, 예외처리 등록일시 :, 결재번호 : | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 고객관리 > 예외 관리 > [업체]예외 처리 정보의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/CustomerRoutes.tsx#L53) · [ExceptionVendorRegistrationPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/exception/ExceptionVendorRegistrationPage.tsx#L7) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/exception/api/exceptionVendorApi.ts#L168) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/exception/api/exceptionVendorApi.ts#L284) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 4개 중 개발 메타데이터 확인 4개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-80ab220e805cc851) | Demo 메타데이터 4/4개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

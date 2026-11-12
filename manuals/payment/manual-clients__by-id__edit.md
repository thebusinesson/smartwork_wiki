# [입금·예치금·배분·취소·환불] 단발성 거래처 관리 수정 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

단발성 거래처 정보를 수정한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 입금·예치금·배분·취소·환불 |
| 언제 사용하는가 | 단발성 거래처 상세 조회, 단발성 거래처 수정 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 회사명, 대표자명, 사업자번호, 법인번호, 주소, 업태 |
| 업무 흐름 | 단발성 거래처 상세 조회, 단발성 거래처 수정 |
| 이 페이지의 역할 | 수정 · 단발성 거래처 수정 |
| 판단 결과·다음 업무 | [단발성 거래처 관리](manual-clients.md) |
| 다른 화면과의 구분 | 서비스 현황 > 입금관리 > 단발성 거래처 관리에서 사용하는 수정 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 단발성 거래처 정보를 수정한다. |
| 메뉴·화면 경로 | 서비스 현황 > 입금관리 > 단발성 거래처 관리 · `/payment/manual-clients/:id/edit` · 경로 변수 `id` |
| 화면 유형·담당 | 수정 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [단발성 거래처 관리](manual-clients.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/payment/manual-clients` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `id` |
| 단발성 거래처 상세 조회 | `/payment/manual-clients` `VIEW` | `id: Long` |
| 단발성 거래처 수정 | `/payment/manual-clients` `PROCESS` | `id: Long` · `ManualClientUpdateRequest` `companyName`, `representativeName`, `corporateNumber`, `zipCode`, `address`, `businessType`, `businessCategory`, `managerName`, `email`, `phone`, `mobilePhone` |

코드에서 확인한 버튼·작업명은 **주소 찾기**, **목록**, **저장**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [단발성 거래처 관리](manual-clients.md)에서 대상 또는 작업을 선택한다. `/payment/manual-clients/:id/edit`에서 이전 화면이 전달한 `id`와 현재 대상을 확인한다.
2. **회사명**, **대표자명**, **사업자번호**, **법인번호**, **주소**, **업태**, **종목** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **저장** 중 해당 버튼을 선택한다.
3. **단발성 거래처 수정**을 실행하기 전에 변경 대상과 입력값을 확인한다. 처리 응답을 확인하고 관련 조회에서 대상의 상태를 확인한다.
4. 후속 조회나 목록 복귀가 필요하면 [단발성 거래처 관리](manual-clients.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `id` |
| 회사명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/ManualClientForm.tsx#L228) |
| 대표자명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/ManualClientForm.tsx#L245) |
| 사업자번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/ManualClientForm.tsx#L262) |
| 법인번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/ManualClientForm.tsx#L285) |
| 주소 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/ManualClientForm.tsx#L308) |
| 우편번호 | 출력 | 조회 응답 기준 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/ManualClientForm.tsx#L320) |
| 업태 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/ManualClientForm.tsx#L357) |
| 종목 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/ManualClientForm.tsx#L373) |
| 담당자명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/ManualClientForm.tsx#L389) |
| 이메일 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/ManualClientForm.tsx#L409) |
| 연락처 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/ManualClientForm.tsx#L460) |
| 핸드폰 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/ManualClientForm.tsx#L474) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 단발성 거래처 상세 조회 | `GET /api/v1/status/payment/manual-clients/{id}` · `/payment/manual-clients` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/manualclient/ManualClientController.kt#L61) | `id: Long` → `success`, `data`, `error`, `id`, `companyName`, `representativeName`, `businessNumber`, `corporateNumber`, `zipCode`, `address`, `businessType`, `businessCategory` | `SB_BILL.dbo.USPBILL_MANUALLY_SALES_CLIENT_DETAIL` |
| 단발성 거래처 수정 | `PUT /api/v1/status/payment/manual-clients/{id}` · `/payment/manual-clients` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/manualclient/ManualClientController.kt#L101) | `id: Long` · `ManualClientUpdateRequest` `companyName`, `representativeName`, `corporateNumber`, `zipCode`, `address`, `businessType`, `businessCategory`, `managerName`, `email`, `phone`, `mobilePhone` → `success`, `data`, `error` | `SB_BILL.dbo.UPMODIFY_MANUALLY_SALES_CLIENT`, `SB_BILL.dbo.MANUALLY_SALES_CLIENT` · 정의에서 확인한 쓰기 `SB_BILL.dbo.MANUALLY_SALES_CLIENT` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `SB_BILL.dbo.USPBILL_MANUALLY_SALES_CLIENT_DETAIL` | @COM_NO int | 정의 참조 `SB_BILL.dbo.MANUALLY_SALES_CLIENT` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/manualclient/repository/ManualClientMapper.kt#L58) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-d09cbac1a39f5469) |
| `SB_BILL.dbo.UPMODIFY_MANUALLY_SALES_CLIENT` | @COM_NO int, @COM_NAME varchar(70), @PARTY varchar(35), @COM_REGNO varchar(10), @COR_REGNO varchar(13), @ZIPCODE varchar(6), @ADDRESS varchar(200), @BIZTYPE varchar(40), @BIZCLASS varchar(60), @MEM_NAME varchar(30), @MEM_EMAIL varchar(40), @MEM_TEL varchar(20), @MEM_HP varchar(20), @CUSER int, @ERR_CODE varchar(10) OUT | 정의 참조 `SB_BILL.dbo.MANUALLY_SALES_CLIENT` · 정적 쓰기 `SB_BILL.dbo.MANUALLY_SALES_CLIENT` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/manualclient/repository/ManualClientMapper.kt#L90) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-f4a1eab0d51d56ad) |
| `SB_BILL.dbo.MANUALLY_SALES_CLIENT` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/manualclient/repository/ManualClientMapper.kt#L70) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-7582813e423bf995) |
| `SB_BILL.dbo.UPSAVE_MANUALLY_SALES_CLIENT` | @COM_NAME varchar(70), @PARTY varchar(35), @COM_REGNO varchar(10), @COR_REGNO varchar(13), @ZIPCODE varchar(6), @ADDRESS varchar(200), @BIZTYPE varchar(40), @BIZCLASS varchar(60), @MEM_NAME varchar(30), @MEM_EMAIL varchar(40), @MEM_TEL varchar(20), @MEM_HP varchar(20), @CUSER int, @ERR_CODE varchar(10) OUT | 정의 참조 `SB_BILL.dbo.MANUALLY_SALES_CLIENT` · 정적 쓰기 `SB_BILL.dbo.MANUALLY_SALES_CLIENT` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/manualclient/repository/ManualClientMapper.kt#L80) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-5c06db93b1244a3c) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 회사명, 대표자명, 사업자번호, 법인번호, 주소, 업태 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 서비스 현황 > 입금관리 > 단발성 거래처 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 주소 찾기 서비스를 불러오지 못했습니다. 주소를 직접 입력해 주세요. | 회사명, 대표자명, 사업자번호, 법인번호, 주소, 업태 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/PaymentRoutes.tsx#L74) · [ManualClientFormPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/ManualClientFormPage.tsx#L20) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/manualClientApi.ts#L42) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/manualClientApi.ts#L56) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/manualClientApi.ts#L48) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 4개 중 개발 메타데이터 확인 4개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-6b3303c8859dd9ad) | Demo 메타데이터 4/4개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

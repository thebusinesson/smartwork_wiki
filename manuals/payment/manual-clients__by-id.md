# [입금·예치금·배분·취소·환불] 단발성 거래처 관리 상세 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

단발성 거래처의 상세 정보를 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 입금·예치금·배분·취소·환불 |
| 언제 사용하는가 | 단발성 거래처 상세 조회, 단발성 거래처 삭제 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 회사명, 대표자명, 사업자번호, 법인번호, 우편번호, 주소 |
| 업무 흐름 | 단발성 거래처 상세 조회, 단발성 거래처 삭제 |
| 이 페이지의 역할 | 상세 · 단발성 거래처 상세 조회 |
| 판단 결과·다음 업무 | [단발성 거래처 관리](manual-clients.md) · [단발성 거래처 관리 수정](manual-clients__by-id__edit.md) |
| 다른 화면과의 구분 | 서비스 현황 > 입금관리 > 단발성 거래처 관리에서 사용하는 상세 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 삭제 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/ManualClientDetailPage.tsx#L160) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 단발성 거래처의 상세 정보를 조회한다. |
| 메뉴·화면 경로 | 서비스 현황 > 입금관리 > 단발성 거래처 관리 · `/payment/manual-clients/:id` · 경로 변수 `id` |
| 화면 유형·담당 | 상세 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [단발성 거래처 관리](manual-clients.md) · [단발성 거래처 관리 수정](manual-clients__by-id__edit.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/payment/manual-clients` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `id` |
| 단발성 거래처 상세 조회 | `/payment/manual-clients` `VIEW` | `id: Long` |
| 단발성 거래처 삭제 | `/payment/manual-clients` `DELETE` | `id: Long` |

코드에서 확인한 버튼·작업명은 **목록**, **삭제**, **수정**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [단발성 거래처 관리](manual-clients.md)에서 대상 또는 작업을 선택한다. `/payment/manual-clients/:id`에서 이전 화면이 전달한 `id`와 현재 대상을 확인한다.
2. **회사명**, **대표자명**, **사업자번호**, **법인번호**, **우편번호**, **주소**, **업태**에서 현재 대상과 입력 또는 표시 내용을 확인한다.
3. **단발성 거래처 상세 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [단발성 거래처 관리 수정](manual-clients__by-id__edit.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `id` |
| 회사명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/ManualClientDetailPage.tsx#L72) |
| 대표자명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/ManualClientDetailPage.tsx#L73) |
| 사업자번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `-` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/ManualClientDetailPage.tsx#L75) |
| 법인번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `-` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/ManualClientDetailPage.tsx#L81) |
| 우편번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/ManualClientDetailPage.tsx#L86) |
| 주소 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/ManualClientDetailPage.tsx#L87) |
| 업태 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/ManualClientDetailPage.tsx#L88) |
| 종목 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/ManualClientDetailPage.tsx#L89) |
| 담당자명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/ManualClientDetailPage.tsx#L90) |
| 이메일 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/ManualClientDetailPage.tsx#L91) |
| 연락처 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/ManualClientDetailPage.tsx#L92) |
| 핸드폰 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/ManualClientDetailPage.tsx#L93) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 단발성 거래처 상세 조회 | `GET /api/v1/status/payment/manual-clients/{id}` · `/payment/manual-clients` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/manualclient/ManualClientController.kt#L61) | `id: Long` → `success`, `data`, `error`, `id`, `companyName`, `representativeName`, `businessNumber`, `corporateNumber`, `zipCode`, `address`, `businessType`, `businessCategory` | `SB_BILL.dbo.USPBILL_MANUALLY_SALES_CLIENT_DETAIL` |
| 단발성 거래처 삭제 | `DELETE /api/v1/status/payment/manual-clients/{id}` · `/payment/manual-clients` `DELETE` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/manualclient/ManualClientController.kt#L113) | `id: Long` → `success`, `data`, `error` | `SB_BILL.dbo.UPREMOVE_MANUALLY_SALES_CLIENT`, `SB_BILL.dbo.MANUALLY_SALES_CLIENT` · 정의에서 확인한 쓰기 `SB_BILL.dbo.MANUALLY_SALES_CLIENT` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `SB_BILL.dbo.USPBILL_MANUALLY_SALES_CLIENT_DETAIL` | @COM_NO int | 정의 참조 `SB_BILL.dbo.MANUALLY_SALES_CLIENT` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/manualclient/repository/ManualClientMapper.kt#L58) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-d09cbac1a39f5469) |
| `SB_BILL.dbo.UPREMOVE_MANUALLY_SALES_CLIENT` | @COM_NO int, @CUSER int, @ERR_CODE varchar(10) OUT | 정의 참조 `SB_BILL.dbo.MANUALLY_SALES_CLIENT` · 정적 쓰기 `SB_BILL.dbo.MANUALLY_SALES_CLIENT` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/manualclient/repository/ManualClientMapper.kt#L97) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-8c9d2ecdc79eff7f) |
| `SB_BILL.dbo.MANUALLY_SALES_CLIENT` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/manualclient/repository/ManualClientMapper.kt#L70) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-7582813e423bf995) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 회사명, 대표자명, 사업자번호, 법인번호, 우편번호, 주소 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 서비스 현황 > 입금관리 > 단발성 거래처 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/PaymentRoutes.tsx#L75) · [ManualClientDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/ManualClientDetailPage.tsx#L22) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/manualClientApi.ts#L42) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/manualClientApi.ts#L62) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 3개 중 개발 메타데이터 확인 3개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-f53ae0fae1d0d307) | Demo 메타데이터 3/3개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

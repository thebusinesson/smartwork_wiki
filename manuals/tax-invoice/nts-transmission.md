# [전송 전·후 오류와 국세청 결과] 국세청 전송 개별 조회 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

참조번호 또는 승인번호로 단건 세금계산서를 조회한다. 둘 중 정확히 하나만 지정.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 전송 전·후 오류와 국세청 결과 |
| 언제 사용하는가 | 국세청 전송 개별 조회, 국세청 단일건 전송 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 검색 조건, 참조번호(ETC_PCS_NO), 승인번호(ISSUE_ID) |
| 업무 흐름 | 국세청 전송 개별 조회, 국세청 단일건 전송 |
| 이 페이지의 역할 | 조회 · 국세청 전송 개별 조회 |
| 판단 결과·다음 업무 | 현재 화면에서 결과를 확인한다. |
| 다른 화면과의 구분 | 같은 경로에서 열리는 조회·팝업은 이 문서에서 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 공급자 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/NtsTransmissionListPage.tsx#L191) |
| 공급받는자 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/NtsTransmissionListPage.tsx#L194) |
| 상태 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/NtsTransmissionListPage.tsx#L197) |
| 공급가액 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/NtsTransmissionListPage.tsx#L200) |
| 전송상태 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/NtsTransmissionListPage.tsx#L223) |
| 전송 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/NtsTransmissionListPage.tsx#L206) |
| 공급자사업자번호 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/NtsTransmissionListPage.tsx#L211) |
| 공급자사업자명 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/NtsTransmissionListPage.tsx#L214) |
| 공받자사업자번호 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/NtsTransmissionListPage.tsx#L217) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 참조번호 또는 승인번호로 단건 세금계산서를 조회한다. 둘 중 정확히 하나만 지정. |
| 메뉴·화면 경로 | SB 서비스관리 > 전자세금계산서 > 국세청 전송 개별 조회 · `/tax-invoice/nts-transmission` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | 현재 화면에서 결과를 확인한다. |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/tax-invoice/nts-transmission` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 국세청 전송 개별 조회 | `/tax-invoice/nts-transmission` `VIEW` | `NtsTransmissionStatusDetailRequest` `referenceNumber`, `approvalNumber` |
| 국세청 단일건 전송 | `/tax-invoice/nts-transmission` `PROCESS` | `NtsTransmissionSubmitRequest` `dtiIdx`, `dtiWday`, `referenceNumber`, `approvalNumber` |

코드에서 확인한 버튼·작업명은 **검색**, **전송**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **SB 서비스관리 > 전자세금계산서 > 국세청 전송 개별 조회**를 연다. `/tax-invoice/nts-transmission`를 연다.
2. **검색 조건**, **참조번호(ETC_PCS_NO)**, **승인번호(ISSUE_ID)** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색**, **전송** 중 해당 버튼을 선택한다.
3. **국세청 전송 개별 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 검색 조건 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/NtsTransmissionListPage.tsx#L59) |
| 참조번호(ETC_PCS_NO) | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `reference` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/NtsTransmissionListPage.tsx#L71) |
| 승인번호(ISSUE_ID) | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `approval` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/NtsTransmissionListPage.tsx#L72) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 국세청 전송 개별 조회 | `GET /api/v1/etax/nts-transmission-status/detail` · `/tax-invoice/nts-transmission` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/taxinvoice/ntstransmissionstatus/NtsTransmissionStatusController.kt#L44) | `NtsTransmissionStatusDetailRequest` `referenceNumber`, `approvalNumber` → `success`, `data`, `error`, `item`, `stats` | `SmartBill3.dbo.upAdmSB_Lst_NtsTargetDTI` · 코드 연계 트랜잭션 |
| 국세청 단일건 전송 | `POST /api/v1/etax/nts-transmission-status/transmit` · `/tax-invoice/nts-transmission` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/taxinvoice/ntstransmissionstatus/NtsTransmissionStatusController.kt#L58) | `NtsTransmissionSubmitRequest` `dtiIdx`, `dtiWday`, `referenceNumber`, `approvalNumber` → `success`, `data`, `error`, `resultCode`, `message` | `SmartBill3.dbo.upAdmSB_NtsSingleSubmit`, `SmartBill3.dbo.upAdmSB_Lst_NtsTargetDTI` · 정의에서 확인한 쓰기 `SB_DTI.dbo.NTS_RESERVATION_DATA` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `SmartBill3.dbo.upAdmSB_Lst_NtsTargetDTI` | @SCH_TYPE char(1), @SCH_TEXT varchar(35) | 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/ntstransmissionstatus/repository/NtsTransmissionStatusMapper.kt#L47) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-62b78dfcba507f23) |
| `SmartBill3.dbo.upAdmSB_NtsSingleSubmit` | @DTI_WDAY varchar(10), @DTI_IDX int, @REMARK_TEXT varchar(100) | 정의 참조 `SmartBill3.dbo.COMPANY`, `SB_DTI.dbo.DTI_HEADER_CUB`, `SB_DTI.dbo.NTS_RESERVATION_DATA`, `SB_DTI.dbo.SERVICE_ADMIN` · 정적 쓰기 `SB_DTI.dbo.NTS_RESERVATION_DATA` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/ntstransmissionstatus/repository/NtsTransmissionStatusMapper.kt#L82) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-c51b2263d152685b) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 검색 조건, 참조번호(ETC_PCS_NO), 승인번호(ISSUE_ID) | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 서비스관리 > 전자세금계산서 > 국세청 전송 개별 조회의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/TaxInvoiceRoutes.tsx#L51) · [NtsTransmissionListPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/NtsTransmissionListPage.tsx#L80) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/api/ntsTransmissionApi.ts#L33) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxinvoice/api/ntsTransmissionApi.ts#L43) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 2개 중 개발 메타데이터 확인 2개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-994616d4fa7825ea) | Demo 메타데이터 2/2개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

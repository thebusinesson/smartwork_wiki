# [발행 장애·상태불일치·운영 일정] 오류코드 상세보기 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

참조번호로 세금계산서 처리 로그 목록을 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 발행 장애·상태불일치·운영 일정 |
| 언제 사용하는가 | 참조번호별 로그 조회, 오류 코드 단건 조회 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 공급자 사업자번호, 공급자 회사명, 공급받는자 사업자번호, 공급받는자 회사명, 작업자, 참조번호 |
| 업무 흐름 | 참조번호별 로그 조회, 오류 코드 단건 조회 |
| 이 페이지의 역할 | 상세 · 참조번호별 로그 조회 |
| 판단 결과·다음 업무 | [참조번호별 로그 조회](reference-log.md) · [연동오류 로그조회](integration-error-logs.md) |
| 다른 화면과의 구분 | SB 서비스관리 > 세금계산서 운영/관리 > 참조번호별 로그 조회에서 사용하는 상세 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 참조번호로 세금계산서 처리 로그 목록을 조회한다. |
| 메뉴·화면 경로 | SB 서비스관리 > 세금계산서 운영/관리 > 참조번호별 로그 조회 · `/tax-operations/reference-log/:referenceNumber` · 경로 변수 `referenceNumber` |
| 화면 유형·담당 | 상세 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [참조번호별 로그 조회](reference-log.md) · [연동오류 로그조회](integration-error-logs.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/tax-operations/reference-log` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `referenceNumber` |
| 참조번호별 로그 조회 | `/tax-operations/reference-log` `VIEW` | `ReferenceLogSearchRequest` `referenceNumber` |
| 오류 코드 단건 조회 | `/error-management/error-code-management` `VIEW` | `errorCode: String` |

코드에서 확인한 버튼·작업명은 **검색**, **목록**, **목록으로 이동**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [참조번호별 로그 조회](reference-log.md)에서 대상 또는 작업을 선택한다. `/tax-operations/reference-log/:referenceNumber`에서 이전 화면이 전달한 `referenceNumber`와 현재 대상을 확인한다.
2. **작업자**, **참조번호** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색** 중 해당 버튼을 선택한다.
3. **참조번호별 로그 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [연동오류 로그조회](integration-error-logs.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `referenceNumber` |
| 공급자 사업자번호 | 출력 | 조회 응답 기준 | 화면 필드 `supplierCorpNo` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxoperations/ReferenceLogPage.tsx#L245) |
| 공급자 회사명 | 출력 | 조회 응답 기준 | 화면 필드 `supplierName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxoperations/ReferenceLogPage.tsx#L252) |
| 공급받는자 사업자번호 | 출력 | 조회 응답 기준 | 화면 필드 `receiverCorpNo` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxoperations/ReferenceLogPage.tsx#L259) |
| 공급받는자 회사명 | 출력 | 조회 응답 기준 | 화면 필드 `receiverName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxoperations/ReferenceLogPage.tsx#L266) |
| (로그)일시 | 출력 | 조회 응답 기준 | 화면 필드 `occurredAt` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxoperations/ReferenceLogPage.tsx#L317) |
| 작업자 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `WORKER_NAME` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxoperations/ReferenceLogPage.tsx#L336) |
| 참조번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxoperations/ReferenceLogPage.tsx#L131) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 참조번호별 로그 조회 | `GET /api/v1/tax-operations/reference-log` · `/tax-operations/reference-log` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/taxoperations/referencelog/ReferenceLogController.kt#L54) | `ReferenceLogSearchRequest` `referenceNumber` → `success`, `data`, `error`, `content`, `totalElements` | `SmartBill3.dbo.SELECT_BCERRORLOG`, `SmartBill3.dbo.COMPANY` · 코드 연계 트랜잭션 |
| 오류 코드 단건 조회 | `GET /api/v1/tax-operations/error-codes/by-code/{errorCode}` · `/error-management/error-code-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/operations/errorcode/ErrorCodeController.kt#L78) · [기존 상세 계약](../../references/api-contracts.md#api166) | `errorCode: String` → `success`, `data`, `error`, `id`, `process`, `errorCode`, `technicalCheckRequired`, `description`, `userScreen`, `customerGuide` | `SmartBill3.dbo.MSG_N_ERROR_CODE`, `SmartBill3.dbo.MSG_M_ERROR_CODE` |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `SmartBill3.dbo.SELECT_BCERRORLOG` | @REFID varchar(35) | 정의 참조 `SmartBill3.dbo.ADMIN_INFO`, `SB_DTI_LOG.dbo.BC_ERROR_LOG`, `SB_DTI.dbo.DifSystem_Link_DTI_DATA`, `SB_DTI.dbo.DTI_HEADER_CUB`, `SB_DTI.dbo.DTI_STATUS_HIS` 외 3개 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxoperations/referencelog/repository/ReferenceLogMapper.kt#L35) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3f26c472d333eb5c) |
| `SmartBill3.dbo.COMPANY` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxoperations/referencelog/repository/ReferenceLogMapper.kt#L63) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-0e6fcaa6b5086c07) |
| `SmartBill3.dbo.MSG_N_ERROR_CODE` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/errorcode/repository/ErrorCodeMapper.kt#L99) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-2fd36974b51745a6) |
| `SmartBill3.dbo.MSG_M_ERROR_CODE` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/errorcode/repository/ErrorCodeMapper.kt#L99) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-ae7b7026e1e01204) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 공급자 사업자번호, 공급자 회사명, 공급받는자 사업자번호, 공급받는자 회사명, 작업자, 참조번호 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 서비스관리 > 세금계산서 운영/관리 > 참조번호별 로그 조회의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 검색 결과가 없습니다. | 공급자 사업자번호, 공급자 회사명, 공급받는자 사업자번호, 공급받는자 회사명, 작업자, 참조번호 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/TaxOperationsRoutes.tsx#L19) · [ReferenceLogPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxoperations/ReferenceLogPage.tsx#L153) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxoperations/api/opsReferenceApi.ts#L95) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxoperations/api/opsReferenceApi.ts#L105) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 4개 중 개발 메타데이터 확인 4개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-102806318c21d1d1) | Demo 메타데이터 4/4개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

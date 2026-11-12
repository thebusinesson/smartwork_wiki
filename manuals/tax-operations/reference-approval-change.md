# [발행 장애·상태불일치·운영 일정] 참조/승인번호 변경 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

참조번호로 세금계산서를 조회하고 변경 예정 번호를 반환한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 발행 장애·상태불일치·운영 일정 |
| 언제 사용하는가 | 참조/승인번호 변경 대상 조회, 참조/승인번호 변경 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 참조번호, 작성일자, 공급가액, 변경 참조번호, 승인번호, 변경 승인번호 |
| 업무 흐름 | 참조/승인번호 변경 대상 조회, 참조/승인번호 변경 |
| 이 페이지의 역할 | 조회·관리 · 참조/승인번호 변경 대상 조회 |
| 판단 결과·다음 업무 | 현재 화면에서 결과를 확인한다. |
| 다른 화면과의 구분 | 같은 경로에서 열리는 조회·팝업은 이 문서에서 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 참조번호로 세금계산서를 조회하고 변경 예정 번호를 반환한다. |
| 메뉴·화면 경로 | SB 서비스관리 > 세금계산서 운영/관리 > 참조/승인번호 변경 · `/tax-operations/reference-approval-change` |
| 화면 유형·담당 | 조회·관리 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | 현재 화면에서 결과를 확인한다. |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/tax-operations/reference-approval-change` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 참조/승인번호 변경 대상 조회 | `/tax-operations/reference-approval-change` `VIEW` | `ReferenceApprovalSearchRequest` `referenceNumber` · 서버 필수 `referenceNumber` |
| 참조/승인번호 변경 | `/tax-operations/reference-approval-change` `PROCESS` | `ReferenceApprovalUpdateRequest` `searchReferenceNumber`, `changedReferenceNumber`, `changedApprovalNumber` · 서버 필수 `searchReferenceNumber`, `changedReferenceNumber`, `changedApprovalNumber` |

코드에서 확인한 버튼·작업명은 **검색**, **저장**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **SB 서비스관리 > 세금계산서 운영/관리 > 참조/승인번호 변경**를 연다. `/tax-operations/reference-approval-change`를 연다.
2. **참조번호** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색**, **저장** 중 해당 버튼을 선택한다.
3. **참조/승인번호 변경 대상 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 참조번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxoperations/ReferenceApprovalChangePage.tsx#L55) |
| 작성일자 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxoperations/ReferenceApprovalChangePage.tsx#L182) |
| 공급가액 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxoperations/ReferenceApprovalChangePage.tsx#L188) |
| 변경 참조번호 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxoperations/ReferenceApprovalChangePage.tsx#L202) |
| 승인번호 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxoperations/ReferenceApprovalChangePage.tsx#L219) |
| 변경 승인번호 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxoperations/ReferenceApprovalChangePage.tsx#L225) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 참조/승인번호 변경 대상 조회 | `GET /api/v1/tax-operations/reference-approvals` · `/tax-operations/reference-approval-change` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/taxoperations/referenceapproval/ReferenceApprovalController.kt#L46) | `ReferenceApprovalSearchRequest` `referenceNumber` · 서버 필수 `referenceNumber` → `success`, `data`, `error`, `issueDate`, `referenceNumber`, `approvalNumber`, `supplyAmount`, `changedReferenceNumber`, `changedApprovalNumber` | `office.dbo.SCH_ETCPCSNO` · 코드 연계 트랜잭션 |
| 참조/승인번호 변경 | `PUT /api/v1/tax-operations/reference-approvals` · `/tax-operations/reference-approval-change` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/taxoperations/referenceapproval/ReferenceApprovalController.kt#L56) | `ReferenceApprovalUpdateRequest` `searchReferenceNumber`, `changedReferenceNumber`, `changedApprovalNumber` · 서버 필수 `searchReferenceNumber`, `changedReferenceNumber`, `changedApprovalNumber` → `success`, `data`, `error`, `message`, `code` | `office.dbo.SCH_ETCPCSNO`, `office.dbo.upEtcPcsNo_chgupt` · 정의에서 확인한 쓰기 `SB_DTI.dbo.DTI_HEADER_CUB`, `office.dbo.CHG_ETCPCSNO_HIS` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `office.dbo.SCH_ETCPCSNO` | @SCHETCPCSNO varchar(50) | 정의 참조 `SB_DTI.dbo.DTI_HEADER_CUB` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxoperations/referenceapproval/repository/ReferenceApprovalMapper.kt#L27) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-c9d70fff30892299) |
| `office.dbo.upEtcPcsNo_chgupt` | @SawonID varchar(10), @stcSchEtcPcsNo varchar(35), @strchgEtc_PN varchar(35), @strchgIssue_Id varchar(24) | 정의 참조 `office.dbo.CHG_ETCPCSNO_HIS`, `SB_DTI.dbo.DTI_HEADER_CUB` · 정적 쓰기 `SB_DTI.dbo.DTI_HEADER_CUB`, `office.dbo.CHG_ETCPCSNO_HIS` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxoperations/referenceapproval/repository/ReferenceApprovalMapper.kt#L37) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-1dccf69f804a6351) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 참조번호, 작성일자, 공급가액, 변경 참조번호, 승인번호, 변경 승인번호 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 서비스관리 > 세금계산서 운영/관리 > 참조/승인번호 변경의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/TaxOperationsRoutes.tsx#L31) · [ReferenceApprovalChangePage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxoperations/ReferenceApprovalChangePage.tsx#L45) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxoperations/api/opsReferenceApi.ts#L45) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/taxoperations/api/opsReferenceApi.ts#L73) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 2개 중 개발 메타데이터 확인 2개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-51803f22889dc731) | Demo 메타데이터 2/2개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

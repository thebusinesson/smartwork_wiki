# [계약 연동 업체·인증서와 장애] 연동업체 관리 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

검색 조건으로 전자계약 연동업체 목록을 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 계약 연동 업체·인증서와 장애 |
| 언제 사용하는가 | 전자계약 연동업체 목록 조회 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 전체, 사업자번호, 회사명, 업체 조건, 사업자번호 / 업체명, 구분 |
| 업무 흐름 | 전자계약 연동업체 목록 조회 |
| 이 페이지의 역할 | 조회 · 전자계약 연동업체 목록 조회 |
| 판단 결과·다음 업무 | [연동업체 관리 상세](linked-vendor-manage__by-comNo.md) · [전자계약 연동업체 등록](linked-vendor-manage__new.md) |
| 다른 화면과의 구분 | 이 경로에서 볼 수 있는 조건·결과를 기준으로 사용한다. 독립 경로의 상세·등록은 관련 화면에 연결한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 검색 조건으로 전자계약 연동업체 목록을 조회한다. |
| 메뉴·화면 경로 | SB 서비스관리 > 전자계약 > 연동업체 관리 · `/electronic-contract/linked-vendor-manage` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [연동업체 관리 상세](linked-vendor-manage__by-comNo.md) · [전자계약 연동업체 등록](linked-vendor-manage__new.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/electronic-contract/linked-vendor-manage` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 전자계약 연동업체 목록 조회 | `/electronic-contract/linked-vendor-manage` `VIEW` | `LinkedVendorSearchRequest` `searchCode`, `keyword` |

코드에서 확인한 버튼·작업명은 **검색**, **연동업체 등록**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **SB 서비스관리 > 전자계약 > 연동업체 관리**를 연다. `/electronic-contract/linked-vendor-manage`를 연다.
2. **전체**, **사업자번호**, **회사명**, **업체 조건** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색**, **연동업체 등록** 중 해당 버튼을 선택한다.
3. **전자계약 연동업체 목록 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [연동업체 관리 상세](linked-vendor-manage__by-comNo.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 전체 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `A` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/LinkedVendorManagePage.tsx#L51) |
| 사업자번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `B` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/LinkedVendorManagePage.tsx#L52) |
| 회사명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `C` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/LinkedVendorManagePage.tsx#L53) |
| 업체 조건 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/LinkedVendorManagePage.tsx#L60) |
| 사업자번호 / 업체명 | 출력 | 조회 응답 기준 | 화면 필드 `companyDisplay` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/LinkedVendorManagePage.tsx#L160) |
| 구분 | 출력 | 조회 응답 기준 | 화면 필드 `type` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/LinkedVendorManagePage.tsx#L172) |
| [기간시스템] -> [SB] | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `periodSystem` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/LinkedVendorManagePage.tsx#L173) |
| [SB] -> [기간시스템] | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `sbToPeriodSystem` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/LinkedVendorManagePage.tsx#L174) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 전자계약 연동업체 목록 조회 | `GET /api/v1/electronic-contract/linked-vendors` · `/electronic-contract/linked-vendor-manage` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/electroniccontract/linkedvendor/LinkedVendorController.kt#L60) | `LinkedVendorSearchRequest` `searchCode`, `keyword` → `success`, `data`, `error`, `content`, `totalElements` | `office.dbo.upStm_LstDCTCompanyLinkInfo01`, `office.dbo.upStm_LstDCTCompanyLinkInfo` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `office.dbo.upStm_LstDCTCompanyLinkInfo01` | @SchCode char(1), @SchContent varchar(100) | 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/linkedvendor/repository/LinkedVendorMapper.kt#L38) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-53924acc9ae5078f) |
| `office.dbo.upStm_LstDCTCompanyLinkInfo` | @COM_NO varchar(10) | 정의 참조 `SmartBill3.dbo.DCT_COMPANY_LINK_IN`, `SmartBill3.dbo.DCT_COMPANY_LINK_OUT` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/linkedvendor/repository/LinkedVendorMapper.kt#L63) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-0b187d74447cf64f) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 전체, 사업자번호, 회사명, 업체 조건, 사업자번호 / 업체명, 구분 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 서비스관리 > 전자계약 > 연동업체 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 검색 결과가 없습니다. | 전체, 사업자번호, 회사명, 업체 조건, 사업자번호 / 업체명, 구분 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/ElectronicContractRoutes.tsx#L34) · [LinkedVendorManagePage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/LinkedVendorManagePage.tsx#L42) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/api/linkedVendorManageApi.ts#L29) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 2개 중 개발 메타데이터 확인 2개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-e8a51206a4766d27) | Demo 메타데이터 2/2개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

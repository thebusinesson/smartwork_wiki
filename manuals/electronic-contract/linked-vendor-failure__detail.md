# [계약 연동 업체·인증서와 장애] 연동업체 장애관리 상세 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

(routingUrl, port) 기준으로 현재 장애 등록 정보, 포트 목록, 점검 이력을 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 계약 연동 업체·인증서와 장애 |
| 언제 사용하는가 | 전자계약 연동업체 장애 단건 상세 조회, 전자계약 연동업체 장애 저장 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 등록시간, 등록/해제, 시작시간, 종료시간, 포트, 등록자 |
| 업무 흐름 | 전자계약 연동업체 장애 단건 상세 조회, 전자계약 연동업체 장애 저장 |
| 이 페이지의 역할 | 상세 · 전자계약 연동업체 장애 단건 상세 조회 |
| 판단 결과·다음 업무 | [연동업체 장애관리](linked-vendor-failure.md) |
| 다른 화면과의 구분 | SB 서비스관리 > 전자계약 > 연동업체 장애관리에서 사용하는 상세 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 확인 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/LinkedVendorFailureRegist.tsx#L450) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | (routingUrl, port) 기준으로 현재 장애 등록 정보, 포트 목록, 점검 이력을 조회한다. |
| 메뉴·화면 경로 | SB 서비스관리 > 전자계약 > 연동업체 장애관리 · `/electronic-contract/linked-vendor-failure/detail` |
| 화면 유형·담당 | 상세 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [연동업체 장애관리](linked-vendor-failure.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/electronic-contract/linked-vendor-failure` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 전자계약 연동업체 장애 단건 상세 조회 | `/electronic-contract/linked-vendor-failure` `VIEW` | `LinkedVendorFailureDetailRequest` `routingUrl`, `port` · 서버 필수 `routingUrl`, `port` |
| 전자계약 연동업체 장애 저장 | `/electronic-contract/linked-vendor-failure` `PROCESS` | `LinkedVendorFailureSaveApiRequest` `routingUrl`, `port`, `errorYn`, `errorMsg`, `fromDatetime`, `toDatetime` · 서버 필수 `routingUrl`, `port`, `fromDatetime`, `toDatetime` |

코드에서 확인한 버튼·작업명은 **저장**, **목록**, **확인**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [연동업체 장애관리](linked-vendor-failure.md)에서 대상 또는 작업을 선택한다. `/electronic-contract/linked-vendor-failure/detail`를 연다.
2. **허브업체 정보**, **허브업체 명**, **서버 주소**, **장애 등록**, **장애 해제**, **서비스 점검 내역** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **저장**, **확인** 중 해당 버튼을 선택한다.
3. **전자계약 연동업체 장애 단건 상세 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [연동업체 장애관리](linked-vendor-failure.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 등록시간 | 출력 | 조회 응답 기준 | 화면 필드 `registeredAt` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/LinkedVendorFailureRegist.tsx#L175) |
| 등록/해제 | 입력 또는 선택 | 서버 형식 검사 | API 요청 `errorYn` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/LinkedVendorFailureRegist.tsx#L181) |
| 시작시간 | 출력 | 조회 응답 기준 | API 응답 `fromDatetime` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/LinkedVendorFailureRegist.tsx#L187) |
| 종료시간 | 출력 | 조회 응답 기준 | API 응답 `toDatetime` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/LinkedVendorFailureRegist.tsx#L193) |
| 포트 | 입력·필수 | 길이·개수 최대 10 | API 요청 `port` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/LinkedVendorFailureRegist.tsx#L197) |
| 등록자 | 출력 | 조회 응답 기준 | 화면 필드 `operatorName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/LinkedVendorFailureRegist.tsx#L198) |
| 허브업체 정보 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/LinkedVendorFailureRegist.tsx#L292) |
| 허브업체 명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/LinkedVendorFailureRegist.tsx#L297) |
| 서버 주소 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/LinkedVendorFailureRegist.tsx#L302) |
| 장애 등록 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/LinkedVendorFailureRegist.tsx#L415) |
| • 서비스 점검 시간 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/LinkedVendorFailureRegist.tsx#L330) |
| 시 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/LinkedVendorFailureRegist.tsx#L372) |
| • 장애 안내 문구 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/LinkedVendorFailureRegist.tsx#L391) |
| 에러 메시지를 입력하세요 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/LinkedVendorFailureRegist.tsx#L393) |
| 장애 해제 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/LinkedVendorFailureRegist.tsx#L419) |
| 서비스 점검 내역 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/LinkedVendorFailureRegist.tsx#L434) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 전자계약 연동업체 장애 단건 상세 조회 | `GET /api/v1/electronic-contract/linked-vendor-failures/detail` · `/electronic-contract/linked-vendor-failure` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/electroniccontract/linkedvendorfailure/LinkedVendorFailureController.kt#L97) | `LinkedVendorFailureDetailRequest` `routingUrl`, `port` · 서버 필수 `routingUrl`, `port` → `success`, `data`, `error`, `routingUrl`, `port`, `currentErrorYn`, `errorMsg`, `fromDatetime`, `toDatetime`, `availablePorts`, `histories` | `smartwork.dbo.UspDctHubErrorRegDetail`, `smartwork.dbo.UspDctHubErrorPortList`, `SmartBill3.dbo.upDCT_Routing_Error_Reg_history` |
| 전자계약 연동업체 장애 저장 | `POST /api/v1/electronic-contract/linked-vendor-failures` · `/electronic-contract/linked-vendor-failure` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/electroniccontract/linkedvendorfailure/LinkedVendorFailureController.kt#L110) | `LinkedVendorFailureSaveApiRequest` `routingUrl`, `port`, `errorYn`, `errorMsg`, `fromDatetime`, `toDatetime` · 서버 필수 `routingUrl`, `port`, `fromDatetime`, `toDatetime` → `success`, `data`, `error` | `smartwork.dbo.UspDctHubErrorRegDetail`, `SmartBill3.dbo.upDCT_ROUTING_ERROR_REG`, `smartwork.dbo.UspDctHubErrorPortList` · 정의에서 확인한 쓰기 `SmartBill3.dbo.DCT_ROUTING_ERROR_REG_HIS`, `SmartBill3.dbo.DCT_ROUTING_ERROR_REG` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.UspDctHubErrorRegDetail` | @ROUTINGURL varchar(50), @PORT varchar(10) | 정의 참조 `SmartBill3.dbo.DCT_ROUTING_ERROR_REG` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/linkedvendorfailure/repository/LinkedVendorFailureMapper.kt#L77) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b63667a3ca0608c6) |
| `smartwork.dbo.UspDctHubErrorPortList` | @ROUTINGURL varchar(50) | 정의 참조 `SmartBill3.dbo.DCT_COMPANY_LINK_OUT` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/linkedvendorfailure/repository/LinkedVendorFailureMapper.kt#L82) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-e42024ca492c6f19) |
| `SmartBill3.dbo.upDCT_Routing_Error_Reg_history` | @ROUTINGURL varchar(50) | 정의 참조 `SmartBill3.dbo.DCT_ROUTING_ERROR_REG_HIS`, `office.dbo.SAWON` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/linkedvendorfailure/repository/LinkedVendorFailureMapper.kt#L97) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-80451bb3a8f64493) |
| `SmartBill3.dbo.upDCT_ROUTING_ERROR_REG` | @ERROR_YN varchar(5), @ERROR_REG_SIG varchar(10), @PORT varchar(10), @ROUTINGURL varchar(50), @SW_NO varchar(10), @SB_USE_CODE varchar(5), @FROM_DATETIME varchar(30), @TO_DATETIME varchar(30), @ERROR_MSG varchar(1000) | 정의 참조 `SmartBill3.dbo.DCT_COMPANY_LINK_OUT`, `SmartBill3.dbo.DCT_ROUTING_ERROR_REG`, `SmartBill3.dbo.DCT_ROUTING_ERROR_REG_HIS` · 정적 쓰기 `SmartBill3.dbo.DCT_ROUTING_ERROR_REG_HIS`, `SmartBill3.dbo.DCT_ROUTING_ERROR_REG` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/linkedvendorfailure/repository/LinkedVendorFailureMapper.kt#L105) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-ede9224224abb514) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 등록시간, 등록/해제, 시작시간, 종료시간, 포트, 등록자 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 서비스관리 > 전자계약 > 연동업체 장애관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/ElectronicContractRoutes.tsx#L41) · [LinkedVendorFailureRegist.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/LinkedVendorFailureRegist.tsx#L92) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/api/linkedVendorFailureManagementApi.ts#L48) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/api/linkedVendorFailureManagementApi.ts#L54) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 4개 중 개발 메타데이터 확인 4개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-ca848c9a20195d3f) | Demo 메타데이터 4/4개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

# [OpenAPI 인증·로그·인증서 구분] 인증서 OID 등록 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

인증서 OID 등록에서 대상과 입력값을 확인해 **인증서 OID 등록** 업무를 처리한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | OpenAPI 인증·로그·인증서 구분 |
| 언제 사용하는가 | 인증서 OID 등록, 인증서 OID 수정 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 인증서 정책번호(OID), 발급기관(CA), 발급용도, 만료일자, 사용여부, 사용 |
| 업무 흐름 | 인증서 OID 등록, 인증서 OID 수정 |
| 이 페이지의 역할 | 등록 · 인증서 OID 등록 |
| 판단 결과·다음 업무 | [인증서 OID 관리](certificate-oid.md) |
| 다른 화면과의 구분 | 연동 서비스 관리 > 연동 서비스 관리 > 인증서 OID 관리에서 사용하는 등록 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 인증서 OID 등록에서 대상과 입력값을 확인해 **인증서 OID 등록** 업무를 처리한다. |
| 메뉴·화면 경로 | 연동 서비스 관리 > 연동 서비스 관리 > 인증서 OID 관리 · `/hub-service/certificate-oid/new` |
| 화면 유형·담당 | 등록 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [인증서 OID 관리](certificate-oid.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/hub-service/certificate-oid` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 인증서 OID 등록 | `/hub-service/certificate-oid` `PROCESS` | `CertificateOidSaveRequest` `oidNumber`, `caIssuer`, `purpose`, `expiryDate`, `isActive`, `usageLocations`, `notes` · 서버 필수 `oidNumber`, `caIssuer`, `purpose`, `expiryDate`, `notes` |
| 인증서 OID 수정 | `/hub-service/certificate-oid` `PROCESS` | `oid: String` · `CertificateOidSaveRequest` `oidNumber`, `caIssuer`, `purpose`, `expiryDate`, `isActive`, `usageLocations`, `notes` · 서버 필수 `oidNumber`, `caIssuer`, `purpose`, `expiryDate`, `notes` |

코드에서 확인한 버튼·작업명은 **저장**, **목록**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [인증서 OID 관리](certificate-oid.md)에서 대상 또는 작업을 선택한다. `/hub-service/certificate-oid/new`를 연다.
2. **사용**, **미사용**, **포털**, **모바일**, **구연동**, **신연동**, **연동** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **저장** 중 해당 버튼을 선택한다.
3. **인증서 OID 등록**을 실행하기 전에 변경 대상과 입력값을 확인한다. 처리 응답을 확인하고 관련 조회에서 대상의 상태를 확인한다.
4. 후속 조회나 목록 복귀가 필요하면 [인증서 OID 관리](certificate-oid.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 인증서 정책번호(OID) | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/certificateOid/components/detail/CertificateOidInfoSection.tsx#L78) |
| 예: tst230222-02 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/certificateOid/components/detail/CertificateOidInfoSection.tsx#L86) |
| 발급기관(CA) | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/certificateOid/components/detail/CertificateOidInfoSection.tsx#L102) |
| 예: 한국정보인증 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/certificateOid/components/detail/CertificateOidInfoSection.tsx#L109) |
| 발급용도 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/certificateOid/components/detail/CertificateOidInfoSection.tsx#L122) |
| 예: 전자세금계산서용 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/certificateOid/components/detail/CertificateOidInfoSection.tsx#L129) |
| 만료일자 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/certificateOid/components/detail/CertificateOidInfoSection.tsx#L142) |
| 만료일자 선택 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/certificateOid/components/detail/CertificateOidInfoSection.tsx#L157) |
| 사용여부 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/certificateOid/components/detail/CertificateOidInfoSection.tsx#L166) |
| 사용 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/certificateOid/components/detail/CertificateOidInfoSection.tsx#L180) |
| 미사용 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/certificateOid/components/detail/CertificateOidInfoSection.tsx#L186) |
| 사용처 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/certificateOid/components/detail/CertificateOidInfoSection.tsx#L196) |
| 포털 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/certificateOid/components/common/UsageLocationCheckboxGroup.tsx#L128) |
| 모바일 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/certificateOid/components/common/UsageLocationCheckboxGroup.tsx#L70) |
| 구연동 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/certificateOid/components/common/UsageLocationCheckboxGroup.tsx#L85) |
| 신연동 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/certificateOid/components/common/UsageLocationCheckboxGroup.tsx#L97) |
| 연동 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/certificateOid/components/common/UsageLocationCheckboxGroup.tsx#L143) |
| 비고 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/certificateOid/components/detail/CertificateOidInfoSection.tsx#L211) |
| 비고 사항을 입력하세요 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/certificateOid/components/detail/CertificateOidInfoSection.tsx#L217) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 인증서 OID 등록 | `POST /api/v1/hub/certificate-oids` · `/hub-service/certificate-oid` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/certificateoid/CertificateOidController.kt#L109) | `CertificateOidSaveRequest` `oidNumber`, `caIssuer`, `purpose`, `expiryDate`, `isActive`, `usageLocations`, `notes` · 서버 필수 `oidNumber`, `caIssuer`, `purpose`, `expiryDate`, `notes` → `success`, `data`, `error`, `id`, `oidNumber`, `caIssuer`, `purpose`, `expiryDate`, `isActive`, `usageLocations`, `notes`, `createdAt` | `office.dbo.upSBAdm_REG_OID`, `smartwork.dbo.upSBAdm_GET_OID` · 정의에서 확인한 쓰기 `SB_COMMON.dbo.CERT_MASTER`, `SB_COMMON.dbo.CERT_POLICY` · 코드 연계 트랜잭션 |
| 인증서 OID 수정 | `PUT /api/v1/hub/certificate-oids/{oid}` · `/hub-service/certificate-oid` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/certificateoid/CertificateOidController.kt#L120) | `oid: String` · `CertificateOidSaveRequest` `oidNumber`, `caIssuer`, `purpose`, `expiryDate`, `isActive`, `usageLocations`, `notes` · 서버 필수 `oidNumber`, `caIssuer`, `purpose`, `expiryDate`, `notes` → `success`, `data`, `error`, `id`, `oidNumber`, `caIssuer`, `purpose`, `expiryDate`, `isActive`, `usageLocations`, `notes`, `createdAt` | `smartwork.dbo.upSBAdm_GET_OID`, `smartwork.dbo.upSBAdm_UPD_OID` · 정의에서 확인한 쓰기 `SB_COMMON.dbo.CERT_MASTER_HIS`, `SB_COMMON.dbo.CERT_POLICY_HIS`, `SB_COMMON.dbo.CERT_MASTER`, `SB_COMMON.dbo.CERT_POLICY` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `office.dbo.upSBAdm_REG_OID` | @OID varchar(100), @CA varchar(50), @PURPOSE varchar(400), @EXPIRE_DATE varchar(10), @CUSER int, @REMARK nvarchar(100), @DELYN varchar(2), @USE_SYSTEM_DTI varchar(50), @USE_SYSTEM_DCT varchar(50), @RESULTCODE int OUT | 정의 참조 `SB_COMMON.dbo.CERT_MASTER`, `SB_COMMON.dbo.CERT_POLICY`, `office.dbo.Split` · 정적 쓰기 `SB_COMMON.dbo.CERT_MASTER`, `SB_COMMON.dbo.CERT_POLICY` · 하위 호출 `office.dbo.Split` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/certificateoid/repository/CertificateOidMapper.kt#L112) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-30aaa0c235fda463) |
| `smartwork.dbo.upSBAdm_GET_OID` | @OID varchar(100) | 정의 참조 `SB_COMMON.dbo.CERT_MASTER`, `SB_COMMON.dbo.CERT_POLICY`, `office.dbo.SAWON` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/certificateoid/repository/CertificateOidMapper.kt#L65) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-4be38aecc624bd90) |
| `smartwork.dbo.upSBAdm_UPD_OID` | @OID varchar(100), @CA varchar(50), @PURPOSE varchar(400), @EXPIRE_DATE varchar(10), @UUSER int, @REMARK nvarchar(100), @DELYN varchar(2), @USE_SYSTEM_DTI varchar(50), @USE_SYSTEM_DCT varchar(50) | 정의 참조 `SB_COMMON.dbo.CERT_MASTER`, `SB_COMMON.dbo.CERT_MASTER_HIS`, `SB_COMMON.dbo.CERT_POLICY`, `SB_COMMON.dbo.CERT_POLICY_HIS`, `office.dbo.Split` · 정적 쓰기 `SB_COMMON.dbo.CERT_MASTER_HIS`, `SB_COMMON.dbo.CERT_POLICY_HIS`, `SB_COMMON.dbo.CERT_MASTER`, `SB_COMMON.dbo.CERT_POLICY` · 하위 호출 `office.dbo.Split` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/certificateoid/repository/CertificateOidMapper.kt#L120) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-d5951f3309e118a8) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 인증서 정책번호(OID), 발급기관(CA), 발급용도, 만료일자, 사용여부, 사용 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 연동 서비스 관리 > 연동 서비스 관리 > 인증서 OID 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 인증서 OID 등록을 취소하였습니다. | 인증서 정책번호(OID), 발급기관(CA), 발급용도, 만료일자, 사용여부, 사용 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/IntegrationRoutes.tsx#L138) · [CertificateOidRegisterPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/certificateOid/CertificateOidRegisterPage.tsx#L12) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/api/certificateOidApi.ts#L105) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/api/certificateOidApi.ts#L116) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 3개 중 개발 메타데이터 확인 3개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-1068d564e49e2995) | Demo 메타데이터 3/3개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

# [계약 연동 업체·인증서와 장애] 스마트빌 인증서 관리 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

스마트빌 인증서 관리에서 **스마트빌 인증서 목록 조회** 결과를 확인한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 계약 연동 업체·인증서와 장애 |
| 언제 사용하는가 | 스마트빌 인증서 목록 조회, 스마트빌 인증서 삭제 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 순번, 인증서 SERIAL(전송 상태 확인), 인증서 유효기간 |
| 업무 흐름 | 스마트빌 인증서 목록 조회, 스마트빌 인증서 삭제 |
| 이 페이지의 역할 | 조회·관리 · 스마트빌 인증서 목록 조회 |
| 판단 결과·다음 업무 | [스마트빌 인증서 관리 상세](smartbill-certificate__by-certificateSerial.md) · [스마트빌 인증서 관리 등록](smartbill-certificate__new.md) |
| 다른 화면과의 구분 | 이 경로에서 볼 수 있는 조건·결과를 기준으로 사용한다. 독립 경로의 상세·등록은 관련 화면에 연결한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 확인 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/SmartbillCertificateManagePage.tsx#L165) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 스마트빌 인증서 관리에서 **스마트빌 인증서 목록 조회** 결과를 확인한다. |
| 메뉴·화면 경로 | SB 서비스관리 > 전자계약 > 스마트빌 인증서 관리 · `/electronic-contract/smartbill-certificate` |
| 화면 유형·담당 | 조회·관리 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [스마트빌 인증서 관리 상세](smartbill-certificate__by-certificateSerial.md) · [스마트빌 인증서 관리 등록](smartbill-certificate__new.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/electronic-contract/smartbill-certificate` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 스마트빌 인증서 목록 조회 | `/electronic-contract/smartbill-certificate` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 스마트빌 인증서 삭제 | `/electronic-contract/smartbill-certificate` `DELETE` | `certSeq: Int` |

코드에서 확인한 버튼·작업명은 **삭제**, **인증서 등록**, **확인**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **SB 서비스관리 > 전자계약 > 스마트빌 인증서 관리**를 연다. `/electronic-contract/smartbill-certificate`를 연다.
2. **스마트빌 인증서 목록 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
3. 후속 조회나 목록 복귀가 필요하면 [스마트빌 인증서 관리 상세](smartbill-certificate__by-certificateSerial.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 순번 | 출력 | 조회 응답 기준 | 화면 필드 `id` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/SmartbillCertificateManagePage.tsx#L85) |
| 인증서 SERIAL(전송 상태 확인) | 출력 | 조회 응답 기준 | 화면 필드 `certificateSerial` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/SmartbillCertificateManagePage.tsx#L91) |
| 인증서 유효기간 | 출력 | 조회 응답 기준 | 화면 필드 `validFrom` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/SmartbillCertificateManagePage.tsx#L106) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 스마트빌 인증서 목록 조회 | `GET /api/v1/electronic-contract/smartbill-certificates` · `/electronic-contract/smartbill-certificate` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/electroniccontract/smartbillcertificate/SmartbillCertificateController.kt#L54) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `content`, `totalElements` | `office.dbo.DCT_BIZON_CERT` · 코드 연계 트랜잭션 |
| 스마트빌 인증서 삭제 | `DELETE /api/v1/electronic-contract/smartbill-certificates/{certSeq}` · `/electronic-contract/smartbill-certificate` `DELETE` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/electroniccontract/smartbillcertificate/SmartbillCertificateController.kt#L93) | `certSeq: Int` → `success`, `data`, `error` | `office.dbo.upStm_DelBizOnCert` · 정의에서 확인한 쓰기 `office.dbo.DCT_BIZON_CERT` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `office.dbo.DCT_BIZON_CERT` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/smartbillcertificate/repository/SmartbillCertificateMapper.kt#L55) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-376dfdf00f67ab4f) |
| `office.dbo.upStm_DelBizOnCert` | @CERT_SEQ int | 정의 참조 `office.dbo.DCT_BIZON_CERT` · 정적 쓰기 `office.dbo.DCT_BIZON_CERT` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/smartbillcertificate/repository/SmartbillCertificateMapper.kt#L105) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-d50bd79afd674795) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 순번, 인증서 SERIAL(전송 상태 확인), 인증서 유효기간 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 서비스관리 > 전자계약 > 스마트빌 인증서 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 삭제할 항목을 찾지 못했습니다. | 순번, 인증서 SERIAL(전송 상태 확인), 인증서 유효기간 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 삭제 처리 중 오류가 발생했습니다. | 순번, 인증서 SERIAL(전송 상태 확인), 인증서 유효기간 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 등록된 인증서가 없습니다. | 순번, 인증서 SERIAL(전송 상태 확인), 인증서 유효기간 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/ElectronicContractRoutes.tsx#L36) · [SmartbillCertificateManagePage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/SmartbillCertificateManagePage.tsx#L12) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/api/smartbillCertificateManageApi.ts#L12) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/api/smartbillCertificateManageApi.ts#L27) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 2개 중 개발 메타데이터 확인 2개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-9a8f22ae700406fb) | Demo 메타데이터 2/2개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

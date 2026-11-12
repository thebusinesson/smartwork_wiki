# [전자계약 원문·이용과 접근] 전자계약 용량 조회 상세 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

회사번호로 전자계약 용량 상세와 상태별 사용 현황을 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 전자계약 원문·이용과 접근 |
| 언제 사용하는가 | 전자계약 용량 조회 상세 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 총 사용가능 용량, 현재 사용용량, 남아있는 용량, 신청날짜, 변경용량(Mbyte), 총용량(Mbyte) |
| 업무 흐름 | 전자계약 용량 조회 상세 |
| 이 페이지의 역할 | 상세 · 전자계약 용량 조회 상세 |
| 판단 결과·다음 업무 | [전자계약 용량 조회](electronic-contract-capacity.md) · [회사 정보 상세](../company-management/company-info__by-id.md) |
| 다른 화면과의 구분 | SB 서비스관리 > 전자계약 > 전자계약 용량 조회에서 사용하는 상세 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 회사번호로 전자계약 용량 상세와 상태별 사용 현황을 조회한다. |
| 메뉴·화면 경로 | SB 서비스관리 > 전자계약 > 전자계약 용량 조회 · `/electronic-contract/electronic-contract-capacity/:comNo` · 경로 변수 `comNo` |
| 화면 유형·담당 | 상세 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [전자계약 용량 조회](electronic-contract-capacity.md) · [회사 정보 상세](../company-management/company-info__by-id.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/electronic-contract/electronic-contract-capacity` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `comNo` |
| 전자계약 용량 조회 상세 | `/electronic-contract/electronic-contract-capacity` `VIEW` | `comNo: Int` |

코드에서 확인한 버튼·작업명은 **이전**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [전자계약 용량 조회](electronic-contract-capacity.md)에서 대상 또는 작업을 선택한다. `/electronic-contract/electronic-contract-capacity/:comNo`에서 이전 화면이 전달한 `comNo`와 현재 대상을 확인한다.
2. **전자계약 용량 조회 상세** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
3. 후속 조회나 목록 복귀가 필요하면 [회사 정보 상세](../company-management/company-info__by-id.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `comNo` |
| 총 사용가능 용량 | 출력 | 조회 응답 기준 | 화면 필드 `totalAvailableCapacity` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/ElectronicContractCapacityDetail.tsx#L38) |
| 현재 사용용량 | 출력 | 조회 응답 기준 | 화면 필드 `usedCapacity` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/ElectronicContractCapacityDetail.tsx#L39) |
| 남아있는 용량 | 출력 | 조회 응답 기준 | 화면 필드 `remainingCapacity` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/ElectronicContractCapacityDetail.tsx#L40) |
| 신청날짜 | 출력 | 조회 응답 기준 | 화면 필드 `entryDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/ElectronicContractCapacityDetail.tsx#L44) |
| 변경용량(Mbyte) | 출력 | 조회 응답 기준 | 화면 필드 `changedCapacityMb` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/ElectronicContractCapacityDetail.tsx#L45) |
| 총용량(Mbyte) | 출력 | 조회 응답 기준 | 화면 필드 `totalCapacity` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/ElectronicContractCapacityDetail.tsx#L46) |
| 전자계약 상태 | 출력 | 조회 응답 기준 | 화면 필드 `statusLabel` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/ElectronicContractCapacityDetail.tsx#L50) |
| 사용량 | 출력 | 조회 응답 기준 | 화면 필드 `usedCapacity` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/ElectronicContractCapacityDetail.tsx#L51) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 전자계약 용량 조회 상세 | `GET /api/v1/electronic-contract/electronic-contract-capacity/{comNo}` · `/electronic-contract/electronic-contract-capacity` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/electroniccontract/capacity/ElectronicContractCapacityController.kt#L70) | `comNo: Int` → `success`, `data`, `error`, `company`, `summary`, `capacityChangeHistories`, `statusUsages` | `SmartBill3.dbo.COMPANY`, `SmartBill3.dbo.upDCT_ChkPremium`, `SmartBill3.dbo.upDCT_Sch_CompanyConfig`, `SmartBill3.dbo.upDCT_Get_AllFileSize2`, `SmartBill3.dbo.upDCT_PremiumCreateHistory` 외 1개 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `SmartBill3.dbo.COMPANY` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/capacity/repository/ElectronicContractCapacityMapper.kt#L51) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-0e6fcaa6b5086c07) |
| `SmartBill3.dbo.upDCT_ChkPremium` | @com_no int | 정의 참조 `SmartBill3.dbo.DCT_PREMIUM` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/capacity/repository/ElectronicContractCapacityMapper.kt#L60) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-01b997a45cafc04e) |
| `SmartBill3.dbo.upDCT_Sch_CompanyConfig` | @COM_NO int | 정의 참조 `SmartBill3.dbo.DCT_COMPANY_CONFIG` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/capacity/repository/ElectronicContractCapacityMapper.kt#L78) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-92d73b73c544ca5f) |
| `SmartBill3.dbo.upDCT_Get_AllFileSize2` | @com_no int | 정의 참조 `SmartBill3.dbo.DCT_CON_INFO_FILE`, `SmartBill3.dbo.DCT_FILE`, `SmartBill3.dbo.DCT_MAIN`, `SmartBill3.dbo.DCT_PUBLIC_FILE`, `SmartBill3.dbo.DCT_SECRET_FILE` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/capacity/repository/ElectronicContractCapacityMapper.kt#L69) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-ea2b7d03636c0042) |
| `SmartBill3.dbo.upDCT_PremiumCreateHistory` | @COMNO int, @CREATE_DATE varchar(10) | 정의 참조 `SmartBill3.dbo.DCT_PREMIUM`, `SmartBill3.dbo.DCT_PREMIUM_BALANCE` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/capacity/repository/ElectronicContractCapacityMapper.kt#L90) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-04474a44857e637e) |
| `SmartBill3.dbo.upAdmSB_Lst_DCT_status_FileSize` | @com_no no | 정의 참조 `SmartBill3.dbo.DCT_CON_INFO_FILE`, `SmartBill3.dbo.DCT_FILE`, `SmartBill3.dbo.DCT_MAIN`, `smartbill3.dbo.no` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/capacity/repository/ElectronicContractCapacityMapper.kt#L103) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-eb68de385a9ef5e0) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 총 사용가능 용량, 현재 사용용량, 남아있는 용량, 신청날짜, 변경용량(Mbyte), 총용량(Mbyte) | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 서비스관리 > 전자계약 > 전자계약 용량 조회의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/ElectronicContractRoutes.tsx#L44) · [ElectronicContractCapacityDetail.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/ElectronicContractCapacityDetail.tsx#L80) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/api/electronicContractCapacityApi.ts#L26) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 6개 중 개발 메타데이터 확인 6개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-094335f46c986f9c) | Demo 메타데이터 6/6개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

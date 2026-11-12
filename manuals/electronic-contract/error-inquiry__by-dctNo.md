# [계약 연동 업체·인증서와 장애] 전자계약 오류 조회 상세 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

전자계약 고유번호로 오류 로그와 전자계약 상세 정보를 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 계약 연동 업체·인증서와 장애 |
| 언제 사용하는가 | 전자계약 오류 상세 조회, 계약업체 직인 이미지 조회, 전자계약 오류 재전송 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 전송 사업자번호, 전송 업체명, 수신 사업자번호, 수신 업체명, 전송 시스템, 상태 |
| 업무 흐름 | 전자계약 오류 상세 조회, 계약업체 직인 이미지 조회, 전자계약 오류 재전송 |
| 이 페이지의 역할 | 상세 · 전자계약 오류 상세 조회 |
| 판단 결과·다음 업무 | [전자계약 오류 조회](error-inquiry.md) |
| 다른 화면과의 구분 | SB 서비스관리 > 전자계약 > 전자계약 오류 조회에서 사용하는 상세 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 계약유형 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/components/ElectronicContractDocument.tsx#L61) |
| 현재상태 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/components/ElectronicContractDocument.tsx#L63) |
| 계약차수 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/components/ElectronicContractDocument.tsx#L65) |
| 계약번호 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/components/ElectronicContractDocument.tsx#L74) |
| 계약명 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/components/ElectronicContractDocument.tsx#L78) |
| 계약일자 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/components/ElectronicContractDocument.tsx#L82) |
| 계약기간 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/components/ElectronicContractDocument.tsx#L84) |
| 계약금액 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/components/ElectronicContractDocument.tsx#L90) |
| 지급일자 | 구역 확인 | 탭 또는 구역을 선택해 관련 입력·결과를 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/components/ElectronicContractDocument.tsx#L92) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 전자계약 고유번호로 오류 로그와 전자계약 상세 정보를 조회한다. |
| 메뉴·화면 경로 | SB 서비스관리 > 전자계약 > 전자계약 오류 조회 · `/electronic-contract/error-inquiry/:dctNo` · 경로 변수 `dctNo` |
| 화면 유형·담당 | 상세 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [전자계약 오류 조회](error-inquiry.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/electronic-contract/error-inquiry` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `dctNo` |
| 전자계약 오류 상세 조회 | `/electronic-contract/error-inquiry` `VIEW` | `dctNo: Long` |
| 계약업체 직인 이미지 조회 | `/electronic-contract/electronic-contract-inquiry` `VIEW` | `dctNo: Long` · `memNo: Long` |
| 전자계약 오류 재전송 | `/electronic-contract/error-inquiry` `PROCESS` | `dctNo: Long` |

코드에서 확인한 버튼·작업명은 **전송**, **목록**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [전자계약 오류 조회](error-inquiry.md)에서 대상 또는 작업을 선택한다. `/electronic-contract/error-inquiry/:dctNo`에서 이전 화면이 전달한 `dctNo`와 현재 대상을 확인한다.
2. **참조 번호** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **전송** 중 해당 버튼을 선택한다.
3. **전자계약 오류 상세 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [전자계약 오류 조회](error-inquiry.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `dctNo` |
| 전송 사업자번호 | 출력 | 조회 응답 기준 | 화면 필드 `senderBizNo` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/EContractErrorInquiryDetail.tsx#L183) |
| 전송 업체명 | 출력 | 조회 응답 기준 | 화면 필드 `senderCompanyName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/EContractErrorInquiryDetail.tsx#L190) |
| 수신 사업자번호 | 출력 | 조회 응답 기준 | 화면 필드 `receiverBizNo` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/EContractErrorInquiryDetail.tsx#L196) |
| 수신 업체명 | 출력 | 조회 응답 기준 | 화면 필드 `receiverCompanyName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/EContractErrorInquiryDetail.tsx#L203) |
| 전송 시스템 | 출력 | 조회 응답 기준 | 화면 필드 `transmissionSystem` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/EContractErrorInquiryDetail.tsx#L209) |
| 상태 | 출력 | 조회 응답 기준 | 화면 필드 `status` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/EContractErrorInquiryDetail.tsx#L215) |
| 전자계약 상세 로그 | 출력 | 조회 응답 기준 | 화면 필드 `processLog` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/EContractErrorInquiryDetail.tsx#L221) |
| 일시 | 출력 | 조회 응답 기준 | 화면 필드 `timestamp` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/EContractErrorInquiryDetail.tsx#L228) |
| 에러 내용 | 출력 | 조회 응답 기준 | 화면 필드 `errorMessage` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/EContractErrorInquiryDetail.tsx#L235) |
| 참조 번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/EContractErrorInquiryDetail.tsx#L258) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 전자계약 오류 상세 조회 | `GET /api/v1/electronic-contract/error-inquiries/{dctNo}` · `/electronic-contract/error-inquiry` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/electroniccontract/errorinquiry/ElectronicContractErrorInquiryController.kt#L66) | `dctNo: Long` → `success`, `data`, `error`, `errorLogs`, `contract`, `retry` | `SmartBill3.dbo.upDCT_Sch_Contract`, `SmartBill3.dbo.upDCT_Sch_ConInfo`, `SmartBill3.dbo.upAdmSB_Lst_DCT_File`, `SmartBill3.dbo.upAdmSB_Lst_DCT_FileCert`, `SmartBill3.dbo.upDCT_SchChgStatus_History` 외 7개 |
| 계약업체 직인 이미지 조회 | `GET /api/v1/electronic-contract/contracts/{dctNo}/contractors/{memNo}/seal` · `/electronic-contract/electronic-contract-inquiry` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/electroniccontract/contractinquiry/ElectronicContractInquiryController.kt#L132) | `dctNo: Long` · `memNo: Long` → 파일 또는 오류 응답 | `SmartBill3.dbo.upDCT_Sch_ConInfo`, `SmartBill3.dbo.upDCT_UserInfo_DctNo` |
| 전자계약 오류 재전송 | `POST /api/v1/electronic-contract/error-inquiries/{dctNo}/retry` · `/electronic-contract/error-inquiry` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/electroniccontract/errorinquiry/ElectronicContractErrorInquiryController.kt#L81) | `dctNo: Long` → `success`, `data`, `error`, `message`, `outcome`, `returnCode` | `SmartBill3.dbo.UPSWDCT_DCTSTATUS_SNDCOM_Q`, `SmartBill3.dbo.upDCT_Sch_Contract`, `SmartBill3.dbo.upDCT_ChkComLinkIn`, `SmartBill3.dbo.upDCT_Sch_SndLinkDctData`, `SmartBill3.dbo.upDCT_Sch_ContractMember` 외 3개 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `SmartBill3.dbo.upDCT_Sch_Contract` | @DCT_NO int, @COM_NO int | 정의 참조 `SmartBill3.dbo.DCT_CONTRACT_TYPE`, `SmartBill3.dbo.DCT_FILE_FORM`, `SmartBill3.dbo.DCT_MAIN`, `SmartBill3.dbo.DCT_STATUS` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/errorinquiry/repository/ElectronicContractErrorInquiryMapper.kt#L98) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-9dabb5f42f670db0) |
| `SmartBill3.dbo.upDCT_Sch_ConInfo` | @dct_no int | 정의 참조 `SmartBill3.dbo.DCT_CON_INFO` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/contractinquiry/repository/ElectronicContractInquiryMapper.kt#L173) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-2db86a06cf4ed0f9) |
| `SmartBill3.dbo.upAdmSB_Lst_DCT_File` | @dct_no int | 정의 참조 `SmartBill3.dbo.DCT_FILE`, `SmartBill3.dbo.MEMBER` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/contractinquiry/repository/ElectronicContractInquiryMapper.kt#L202) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-29c69413b81805a5) |
| `SmartBill3.dbo.upAdmSB_Lst_DCT_FileCert` | @dct_no int, @dct_file_no int | 정의 참조 `SmartBill3.dbo.COMPANY`, `SmartBill3.dbo.DCT_CON_INFO_FILE` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/contractinquiry/repository/ElectronicContractInquiryMapper.kt#L214) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-5859bf1665949025) |
| `SmartBill3.dbo.upDCT_SchChgStatus_History` | @dct_no int, @status varchar(1) | 정의 참조 `SmartBill3.dbo.COMPANY`, `SmartBill3.dbo.DCT_CON_INFO`, `SmartBill3.dbo.DCT_MAIN`, `SmartBill3.dbo.DCT_STATUS` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/contractinquiry/repository/ElectronicContractInquiryMapper.kt#L227) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-9fa3dc6ab0a2d740) |
| `SmartBill3.dbo.DCT_STATUS` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/contractinquiry/repository/ElectronicContractInquiryMapper.kt#L256) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-8a0276a511d6238e) |
| `SmartBill3.dbo.MEMBER` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/contractinquiry/repository/ElectronicContractInquiryMapper.kt#L256) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-9042ff61b257b012) |
| `SmartBill3.dbo.TB_CODE` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/contractinquiry/repository/ElectronicContractInquiryMapper.kt#L256) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-1395084fab0058a7) |
| `SmartBill3.dbo.upDCT_SchRevenueStampFile` | @DCT_NO int | 정의 참조 `SmartBill3.dbo.DCT_REVENUESTAMP_FILE`, `SmartBill3.dbo.MEMBER` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/contractinquiry/repository/ElectronicContractInquiryMapper.kt#L284) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-c66a8f5b81ed5974) |
| `SmartBill3.dbo.upAdmSB_Lst_DCT_ErrorLog` | @dct_no int | 정의 참조 `SmartBill3.dbo.COMPANY`, `SmartBill3.dbo.DCT_ERROR_LOG`, `SmartBill3.dbo.DCT_MAIN`, `SmartBill3.dbo.DCT_STATUS` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/errorinquiry/repository/ElectronicContractErrorInquiryMapper.kt#L57) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-eabefeec8a100300) |
| `SmartBill3.dbo.UPSWDCT_DCTSTATUS_SNDCOM_Q` | @DCT_NO int | 정의 참조 `SmartBill3.dbo.COMPANY`, `SmartBill3.dbo.DCT_MAIN`, `SmartBill3.dbo.DCT_STATUS`, `SmartBill3.dbo.MEMBER` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/errorinquiry/repository/ElectronicContractErrorInquiryMapper.kt#L78) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-facc9da8ee34cbce) |
| `SmartBill3.dbo.upDCT_ChkComLinkIn` | @COM_NO int, @DCT_NO int | 정의 참조 `SmartBill3.dbo.DCT_COMPANY_LINK_IN`, `SmartBill3.dbo.DCT_MAIN` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/errorinquiry/repository/ElectronicContractErrorInquiryMapper.kt#L120) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-2fba70fd2a069a56) |
| `SmartBill3.dbo.upDCT_UserInfo_DctNo` | @mem_no int, @dct_no int | 정의 참조 `SmartBill3.dbo.COMPANY`, `SmartBill3.dbo.DCT_CON_INFO` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/contractinquiry/repository/ElectronicContractInquiryMapper.kt#L190) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-1a00ec7123616751) |
| `SmartBill3.dbo.upDCT_Sch_SndLinkDctData` | @dct_no int | 정의 참조 `SmartBill3.dbo.DCT_CON_INFO`, `SmartBill3.dbo.DCT_FILE`, `SmartBill3.dbo.DCT_MAIN`, `SmartBill3.dbo.DCT_STATUS` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/errorinquiry/repository/ElectronicContractTransmissionMapper.kt#L45) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-96a7414b302bbe82) |
| `SmartBill3.dbo.upDCT_Sch_ContractMember` | @DIV char(1), @dct_no varchar(100), @com_no varchar(100) | 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/errorinquiry/repository/ElectronicContractTransmissionMapper.kt#L63) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-0d20924a924866f4) |
| `SmartBill3.dbo.upDCT_Sch_FileInfo` | @DCT_NO int | 정의 참조 `SmartBill3.dbo.DCT_FILE` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/errorinquiry/repository/ElectronicContractTransmissionMapper.kt#L76) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-2429e3b1a0d77774) |
| `SmartBill3.dbo.upDCT_Sch_SignedInfo` | @dct_no int | 정의 참조 `SmartBill3.dbo.COMPANY`, `SmartBill3.dbo.DCT_CON_INFO_FILE`, `SmartBill3.dbo.DCT_FILE` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/errorinquiry/repository/ElectronicContractTransmissionMapper.kt#L87) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-eb1a16c611dbe203) |
| `SmartBill3.dbo.upDCT_Sch_Securities` | @DCT_NO int | 정의 참조 `SmartBill3.dbo.COMPANY`, `SmartBill3.dbo.MEMBER`, `SmartBill3.dbo.SECURITIES` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/errorinquiry/repository/ElectronicContractTransmissionMapper.kt#L100) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-a71d97faefa66a8f) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 전송 사업자번호, 전송 업체명, 수신 사업자번호, 수신 업체명, 전송 시스템, 상태 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 서비스관리 > 전자계약 > 전자계약 오류 조회의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 재전송 요청은 완료되었으나 상세 정보를 갱신하지 못했습니다. | 전송 사업자번호, 전송 업체명, 수신 사업자번호, 수신 업체명, 전송 시스템, 상태 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 데이터가 없습니다. | 전송 사업자번호, 전송 업체명, 수신 사업자번호, 수신 업체명, 전송 시스템, 상태 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/ElectronicContractRoutes.tsx#L48) · [EContractErrorInquiryDetail.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/EContractErrorInquiryDetail.tsx#L61) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/api/eContractErrorInquiryDetailApi.ts#L13) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/api/electronicContractInquiryApi.ts#L45) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/api/eContractErrorInquiryDetailApi.ts#L21) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 18개 중 개발 메타데이터 확인 18개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-36b13d5696f17357) | Demo 메타데이터 18/18개 확인 · Dev와 계약 차이 1개 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

# [송신거래 약정키와 식별자] 송신거래 약정키 등록 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

송신거래 약정키 등록에서 대상과 입력값을 확인해 **송신거래 약정키 신규 등록** 업무를 처리한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 송신거래 약정키와 식별자 |
| 언제 사용하는가 | 스마트빌 회원 확인, 자사식별자 중복 확인, 사업자+식별자+은행코드 중복 확인, 송신거래 약정키 신규 등록 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 최초등록일, 최초등록자, 자동생성, 전송여부, 신청업체 사업자번호, 동보전송여부 |
| 업무 흐름 | 스마트빌 회원 확인, 자사식별자 중복 확인, 사업자+식별자+은행코드 중복 확인, 송신거래 약정키 신규 등록 |
| 이 페이지의 역할 | 등록 · 송신거래 약정키 신규 등록 |
| 판단 결과·다음 업무 | [송신거래 약정키 등록](transmission-agreement-key.md) |
| 다른 화면과의 구분 | SB 서비스관리 > 구매확인서 > 송신거래 약정키 등록에서 사용하는 등록 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 확인 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/AgreementKeyRegister.tsx#L616) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 송신거래 약정키 등록에서 대상과 입력값을 확인해 **송신거래 약정키 신규 등록** 업무를 처리한다. |
| 메뉴·화면 경로 | SB 서비스관리 > 구매확인서 > 송신거래 약정키 등록 · `/purchase-confirmation/transmission-agreement-key/new` |
| 화면 유형·담당 | 등록 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [송신거래 약정키 등록](transmission-agreement-key.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/purchase-confirmation/transmission-agreement-key` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 스마트빌 회원 확인 | `/purchase-confirmation/transmission-agreement-key` `VIEW` | `applicationIdentifier: String` |
| 자사식별자 중복 확인 | `/purchase-confirmation/transmission-agreement-key` `VIEW` | `localId: String` |
| 사업자+식별자+은행코드 중복 확인 | `/purchase-confirmation/transmission-agreement-key` `VIEW` | `applicationIdentifier: String` · `localId: String` · `confirmBankCode: String` |
| 송신거래 약정키 신규 등록 | `/purchase-confirmation/transmission-agreement-key` `PROCESS` | `TransmissionAgreementKeySaveRequest` `applicationIdentifier`, `localId`, `localQual`, `localDivisionId`, `localDivisionQual`, `partnerId`, `partnerQual`, `partnerDivisionId`, `partnerDivisionQual`, `confirmBankCode`, `confirmBankName`, `confirmBankBranch`, `viewUrl`, `excelUrl` · 서버 필수 `applicationIdentifier`, `localId`, `localDivisionId`, `partnerId`, `partnerDivisionId`, `confirmBankCode`, `viewUrl`, `excelUrl` |

코드에서 확인한 버튼·작업명은 **회원확인**, **중복확인**, **동일사업자&은행코드 중복확인**, **저장**, **목록**, **확인**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [송신거래 약정키 등록](transmission-agreement-key.md)에서 대상 또는 작업을 선택한다. `/purchase-confirmation/transmission-agreement-key/new`를 연다.
2. **최초등록일**, **최초등록자**, **자동생성**, **전송여부**, **신청업체 사업자번호**, **동보전송여부**, **사용** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **회원확인**, **중복확인**, **동일사업자&은행코드 중복확인**, **저장**, **확인** 중 해당 버튼을 선택한다.
3. **송신거래 약정키 신규 등록**을 실행하기 전에 변경 대상과 입력값을 확인한다. 표시되는 **송신거래 약정키가 등록되었습니다.** 메시지와 대상 상태를 확인한다.
4. 후속 조회나 목록 복귀가 필요하면 [송신거래 약정키 등록](transmission-agreement-key.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 최초등록일 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/AgreementKeyRegister.tsx#L317) |
| 최초등록자 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/AgreementKeyRegister.tsx#L323) |
| 자동생성 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/AgreementKeyRegister.tsx#L334) |
| 전송여부 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/AgreementKeyRegister.tsx#L339) |
| 신청업체 사업자번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/AgreementKeyRegister.tsx#L360) |
| 동보전송여부 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/AgreementKeyRegister.tsx#L384) |
| 사용 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/AgreementKeyRegister.tsx#L394) |
| 사용안함 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/AgreementKeyRegister.tsx#L398) |
| 자사식별자 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/AgreementKeyRegister.tsx#L405) |
| 자사식별자한정어 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/AgreementKeyRegister.tsx#L426) |
| 자사상세식별자 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/AgreementKeyRegister.tsx#L438) |
| 자사상세식별자한정어 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/AgreementKeyRegister.tsx#L452) |
| 파트너식별자 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/AgreementKeyRegister.tsx#L464) |
| 파트너식별자한정어 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/AgreementKeyRegister.tsx#L478) |
| 파트너상세식별자 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/AgreementKeyRegister.tsx#L490) |
| 파트너상세식별자한정어 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/AgreementKeyRegister.tsx#L504) |
| 신청업체 은행코드 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/AgreementKeyRegister.tsx#L520) |
| 신청업체 은행명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/AgreementKeyRegister.tsx#L546) |
| 신청업체 은행 지점명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/AgreementKeyRegister.tsx#L556) |
| 구매확인서 상세페이지 URL | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/AgreementKeyRegister.tsx#L570) |
| 구매확인서 EXCEL URL | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/AgreementKeyRegister.tsx#L586) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 스마트빌 회원 확인 | `GET /api/v1/purchase-confirmation/transmission-agreement-keys/check-member` · `/purchase-confirmation/transmission-agreement-key` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/purchaseconfirmation/transmissionagreementkey/validation/TransmissionAgreementKeyValidationController.kt#L37) | `applicationIdentifier: String` → `success`, `data`, `error`, `isMember`, `memberCount` | `SmartBill3.dbo.COMPANY` · 코드 연계 트랜잭션 |
| 자사식별자 중복 확인 | `GET /api/v1/purchase-confirmation/transmission-agreement-keys/check-identifier` · `/purchase-confirmation/transmission-agreement-key` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/purchaseconfirmation/transmissionagreementkey/validation/TransmissionAgreementKeyValidationController.kt#L51) | `localId: String` → `success`, `data`, `error`, `duplicated`, `duplicateCount` | `KT_Net.dbo.SRID_M` |
| 사업자+식별자+은행코드 중복 확인 | `GET /api/v1/purchase-confirmation/transmission-agreement-keys/check-bank` · `/purchase-confirmation/transmission-agreement-key` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/purchaseconfirmation/transmissionagreementkey/validation/TransmissionAgreementKeyValidationController.kt#L68) | `applicationIdentifier: String` · `localId: String` · `confirmBankCode: String` → `success`, `data`, `error`, `duplicated`, `duplicateCount` | `KT_Net.dbo.SRID_M` |
| 송신거래 약정키 신규 등록 | `POST /api/v1/purchase-confirmation/transmission-agreement-keys` · `/purchase-confirmation/transmission-agreement-key` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/purchaseconfirmation/transmissionagreementkey/save/TransmissionAgreementKeySaveController.kt#L40) | `TransmissionAgreementKeySaveRequest` `applicationIdentifier`, `localId`, `localQual`, `localDivisionId`, `localDivisionQual`, `partnerId`, `partnerQual`, `partnerDivisionId`, `partnerDivisionQual`, `confirmBankCode`, `confirmBankName`, `confirmBankBranch`, `viewUrl`, `excelUrl` · 서버 필수 `applicationIdentifier`, `localId`, `localDivisionId`, `partnerId`, `partnerDivisionId`, `confirmBankCode`, `viewUrl`, `excelUrl` → `success`, `data`, `error` | `office.dbo.upPurchase_SRIDSav` · 정의에서 확인한 쓰기 `KT_Net.dbo.SRID_M`, `SmartBill3.dbo.PUR_ONESTEP` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `SmartBill3.dbo.COMPANY` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/purchaseconfirmation/transmissionagreementkey/validation/repository/TransmissionAgreementKeyValidationMapper.kt#L31) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-0e6fcaa6b5086c07) |
| `KT_Net.dbo.SRID_M` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/purchaseconfirmation/transmissionagreementkey/validation/repository/TransmissionAgreementKeyValidationMapper.kt#L41) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-d46149337d208c80) |
| `office.dbo.upPurchase_SRIDSav` | @StrLocalID varchar(35), @StrLocalQUAL varchar(4), @StrLocalDivisionID varchar(35), @StrLocalDivisionQUAL varchar(4), @StrPartnerID varchar(35), @StrPartnerQUAL varchar(4), @StrPartnerDivisionID varchar(35), @StrPartnerDivisionQUAL varchar(4), @StrRegDate varchar(14), @StrReg_MemNo int, @StrApplicationIdentifier varchar(10), @StrconfirmBankCode varchar(4), @StrConfirmBankName varchar(70), @StrConfirmBankBranch varchar(70), @StrViewUrl varchar(50), @StrExcelUrl varchar(50), @broadcastyn char(1), @onestep char(1) | 정의 참조 `SmartBill3.dbo.COMPANY`, `office.dbo.fnFillDigit`, `SmartBill3.dbo.PUR_ONESTEP`, `KT_Net.dbo.SRID_M` · 정적 쓰기 `KT_Net.dbo.SRID_M`, `SmartBill3.dbo.PUR_ONESTEP` · 하위 호출 `office.dbo.fnFillDigit` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/purchaseconfirmation/transmissionagreementkey/save/repository/TransmissionAgreementKeySaveMapper.kt#L51) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b5a46657f01a992f) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 최초등록일, 최초등록자, 자동생성, 전송여부, 신청업체 사업자번호, 동보전송여부 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 서비스관리 > 구매확인서 > 송신거래 약정키 등록의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 송신거래 약정키 등록에 실패했습니다. | 최초등록일, 최초등록자, 자동생성, 전송여부, 신청업체 사업자번호, 동보전송여부 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 회원 확인 중 오류가 발생했습니다. | 최초등록일, 최초등록자, 자동생성, 전송여부, 신청업체 사업자번호, 동보전송여부 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 중복 확인 중 오류가 발생했습니다. | 최초등록일, 최초등록자, 자동생성, 전송여부, 신청업체 사업자번호, 동보전송여부 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/PurchaseConfirmationRoutes.tsx#L15) · [AgreementKeyRegister.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/AgreementKeyRegister.tsx#L66) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/api/transmissionAgreementKeyRegisterDetailApi.ts#L62) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/api/transmissionAgreementKeyRegisterDetailApi.ts#L73) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/api/transmissionAgreementKeyRegisterDetailApi.ts#L88) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/api/transmissionAgreementKeyRegisterDetailApi.ts#L99) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 3개 중 개발 메타데이터 확인 3개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-5d406197226d238f) | Demo 메타데이터 3/3개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

# [송신거래 약정키와 식별자] 상세페이지 URL 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

INTER_IDX 단건 상세 정보를 반환한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 송신거래 약정키와 식별자 |
| 언제 사용하는가 | 식별자 등록 상세 조회, 은행식별자/URL 옵션 목록, 식별자 중복 확인, 식별자 등록 다건 삭제, 식별자 등록 수정 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 등록일, 등록자, 공급업체 사업자번호, 은행 식별자, 수발신 식별자, 상세 수발신식별자 |
| 업무 흐름 | 식별자 등록 상세 조회, 은행식별자/URL 옵션 목록, 식별자 중복 확인, 식별자 등록 다건 삭제, 식별자 등록 수정 |
| 이 페이지의 역할 | 상세 · 식별자 등록 상세 조회 |
| 판단 결과·다음 업무 | [식별자 정보 등록](identifier-key.md) |
| 다른 화면과의 구분 | SB 서비스관리 > 구매확인서 > 식별자 정보 등록에서 사용하는 상세 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 삭제 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/IdentifierKeyRegisterDetailPage.tsx#L498) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | INTER_IDX 단건 상세 정보를 반환한다. |
| 메뉴·화면 경로 | SB 서비스관리 > 구매확인서 > 식별자 정보 등록 · `/purchase-confirmation/identifier-key/:interIdx` · 경로 변수 `interIdx` |
| 화면 유형·담당 | 상세 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [식별자 정보 등록](identifier-key.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/purchase-confirmation/identifier-key` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `interIdx` |
| 식별자 등록 상세 조회 | `/purchase-confirmation/identifier-key` `VIEW` | `interIdx: Int` |
| 은행식별자/URL 옵션 목록 | `/purchase-confirmation/identifier-key` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 식별자 중복 확인 | `/purchase-confirmation/identifier-key` `VIEW` | `localId: String` · `comRegNo: String` |
| 식별자 등록 다건 삭제 | `/purchase-confirmation/identifier-key` `DELETE` | `DeleteRequest` `interIdxes`, `reason` · 서버 필수 `interIdxes`, `reason` |
| 식별자 등록 수정 | `/purchase-confirmation/identifier-key` `PROCESS` | `interIdx: Int` · `IdentifierKeySaveRequest` `comRegno`, `localId`, `localDivisionId`, `confirmKey`, `partnerId`, `viewUrl`, `excelUrl` · 서버 필수 `comRegno`, `localId`, `localDivisionId`, `confirmKey`, `partnerId`, `viewUrl`, `excelUrl` |

코드에서 확인한 버튼·작업명은 **중복확인**, **선택**, **삭제**, **저장**, **목록**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [식별자 정보 등록](identifier-key.md)에서 대상 또는 작업을 선택한다. `/purchase-confirmation/identifier-key/:interIdx`에서 이전 화면이 전달한 `interIdx`와 현재 대상을 확인한다.
2. **등록일**, **등록자**, **공급업체 사업자번호**, **은행 식별자**, **수발신 식별자**, **상세 수발신식별자**, **인증키** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **중복확인**, **저장** 중 해당 버튼을 선택한다.
3. **식별자 등록 상세 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [식별자 정보 등록](identifier-key.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `interIdx` |
| 등록일 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/IdentifierKeyRegisterDetailPage.tsx#L358) |
| 등록자 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/IdentifierKeyRegisterDetailPage.tsx#L364) |
| 공급업체 사업자번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/IdentifierKeyRegisterDetailPage.tsx#L372) |
| 은행 식별자 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/IdentifierKeyRegisterDetailPage.tsx#L384) |
| 수발신 식별자 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/IdentifierKeyRegisterDetailPage.tsx#L397) |
| 상세 수발신식별자 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/IdentifierKeyRegisterDetailPage.tsx#L416) |
| 인증키 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/IdentifierKeyRegisterDetailPage.tsx#L431) |
| 상세페이지 URL | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/IdentifierKeyRegisterDetailPage.tsx#L446) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 식별자 등록 상세 조회 | `GET /api/v1/purchase-confirmation/identifier-keys/{interIdx}` · `/purchase-confirmation/identifier-key` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/purchaseconfirmation/identifierkey/detail/IdentifierKeyDetailController.kt#L34) | `interIdx: Int` → `success`, `data`, `error`, `interIdx`, `comRegno`, `localId`, `localDivisionId`, `confirmKey`, `partnerId`, `viewUrl`, `excelUrl`, `regDate` | `office.dbo.upPurchase_SBView`, `office.dbo.upGW_ErrCretMemName` · 코드 연계 트랜잭션 |
| 은행식별자/URL 옵션 목록 | `GET /api/v1/purchase-confirmation/identifier-keys/bank-options` · `/purchase-confirmation/identifier-key` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/purchaseconfirmation/identifierkey/bankoption/IdentifierKeyBankOptionController.kt#L35) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `content` | `office.dbo.upPurchase_Sch_LocalID` · 코드 연계 트랜잭션 |
| 식별자 중복 확인 | `GET /api/v1/purchase-confirmation/identifier-keys/check-identifier` · `/purchase-confirmation/identifier-key` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/purchaseconfirmation/identifierkey/validation/IdentifierKeyValidationController.kt#L54) | `localId: String` · `comRegNo: String` → `success`, `data`, `error`, `duplicated`, `duplicateCount` | `SmartBill3.dbo.SB_INTERFACE_ID` |
| 식별자 등록 다건 삭제 | `DELETE /api/v1/purchase-confirmation/identifier-keys` · `/purchase-confirmation/identifier-key` `DELETE` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/purchaseconfirmation/identifierkey/delete/IdentifierKeyDeleteController.kt#L39) | `DeleteRequest` `interIdxes`, `reason` · 서버 필수 `interIdxes`, `reason` → `success`, `data`, `error`, `deletedCount` | `SmartBill3.dbo.SB_INTERFACE_ID_HISTORY`, `SmartBill3.dbo.SB_INTERFACE_ID`, `smartwork.dbo.action_reason` · 정의에서 확인한 쓰기 `SmartBill3.dbo.SB_INTERFACE_ID_HISTORY`, `smartwork.dbo.action_reason` · 코드 연계 트랜잭션 |
| 식별자 등록 수정 | `PUT /api/v1/purchase-confirmation/identifier-keys/{interIdx}` · `/purchase-confirmation/identifier-key` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/purchaseconfirmation/identifierkey/save/IdentifierKeySaveController.kt#L59) | `interIdx: Int` · `IdentifierKeySaveRequest` `comRegno`, `localId`, `localDivisionId`, `confirmKey`, `partnerId`, `viewUrl`, `excelUrl` · 서버 필수 `comRegno`, `localId`, `localDivisionId`, `confirmKey`, `partnerId`, `viewUrl`, `excelUrl` → `success`, `data`, `error` | `SmartBill3.dbo.SB_INTERFACE_ID`, `office.dbo.upPurchase_SBMod` · 정의에서 확인한 쓰기 `SmartBill3.dbo.SB_INTERFACE_ID_HISTORY`, `SmartBill3.dbo.SB_INTERFACE_ID` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `office.dbo.upPurchase_SBView` | @strInterIDX int | 정의 참조 `SmartBill3.dbo.SB_INTERFACE_ID` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/purchaseconfirmation/identifierkey/detail/repository/IdentifierKeyDetailMapper.kt#L38) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-67da20212757d00b) |
| `office.dbo.upGW_ErrCretMemName` | @sw_no int | 정의 참조 `office.dbo.SAWON` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/purchaseconfirmation/identifierkey/detail/repository/IdentifierKeyDetailMapper.kt#L45) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-463a757e635a918a) |
| `office.dbo.upPurchase_Sch_LocalID` | 컬럼·결과 계약은 매퍼 참조 | 정의 참조 `SmartBill3.dbo.COMPANY`, `KT_Net.dbo.SRID_M` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/purchaseconfirmation/identifierkey/bankoption/repository/IdentifierKeyBankOptionMapper.kt#L34) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-02b85a1dd3d17513) |
| `SmartBill3.dbo.SB_INTERFACE_ID` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/purchaseconfirmation/identifierkey/validation/repository/IdentifierKeyValidationMapper.kt#L41) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-2c36b09de569757a) |
| `SmartBill3.dbo.SB_INTERFACE_ID_HISTORY` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL INSERT INTO | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/purchaseconfirmation/identifierkey/delete/repository/IdentifierKeyDeleteMapper.kt#L46) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-ab608b79a505a554) |
| `smartwork.dbo.action_reason` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL INSERT INTO | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/shared/actionreason/repository/ActionReasonMapper.kt#L16) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b0430106ffe0743f) |
| `office.dbo.upPurchase_SBMod` | @strInterIDX int, @StrcomRegno varchar(10), @StrLocalID varchar(35), @StrLocalDivID varchar(35), @StrCONFIRM_KEY varchar(35), @StrpartnerID varchar(35), @StrReg_MemNo int, @StrViewURL varchar(50), @StrExcelURL varchar(50), @sawonid int | 정의 참조 `SmartBill3.dbo.SB_INTERFACE_ID`, `SmartBill3.dbo.SB_INTERFACE_ID_HISTORY` · 정적 쓰기 `SmartBill3.dbo.SB_INTERFACE_ID_HISTORY`, `SmartBill3.dbo.SB_INTERFACE_ID` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/purchaseconfirmation/identifierkey/save/repository/IdentifierKeySaveMapper.kt#L64) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-aa9213adb8e89bbb) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 등록일, 등록자, 공급업체 사업자번호, 은행 식별자, 수발신 식별자, 상세 수발신식별자 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 서비스관리 > 구매확인서 > 식별자 정보 등록의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 삭제할 항목을 선택하세요. | 등록일, 등록자, 공급업체 사업자번호, 은행 식별자, 수발신 식별자, 상세 수발신식별자 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 식별자 등록 삭제에 실패했습니다. | 등록일, 등록자, 공급업체 사업자번호, 은행 식별자, 수발신 식별자, 상세 수발신식별자 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 상세 조회 파라미터가 없습니다. | 등록일, 등록자, 공급업체 사업자번호, 은행 식별자, 수발신 식별자, 상세 수발신식별자 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 중복 확인 중 오류가 발생했습니다. | 등록일, 등록자, 공급업체 사업자번호, 은행 식별자, 수발신 식별자, 상세 수발신식별자 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/PurchaseConfirmationRoutes.tsx#L22) · [IdentifierKeyRegisterDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/IdentifierKeyRegisterDetailPage.tsx#L65) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/api/identifierKeyRegisterDetailApi.ts#L43) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/api/identifierKeyRegisterDetailApi.ts#L93) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/api/identifierKeyRegisterDetailApi.ts#L67) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/api/identifierKeyRegisterApi.ts#L54) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/api/identifierKeyRegisterDetailApi.ts#L113) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 7개 중 개발 메타데이터 확인 7개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-e40a8040d86bfd44) | Demo 메타데이터 7/7개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

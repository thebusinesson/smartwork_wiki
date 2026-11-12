# [송신거래 약정키와 식별자] 식별자 정보 등록 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

식별자(SB_INTERFACE_ID) 목록을 조회한다. 모든 검색 조건은 LIKE 매칭이며, 빈값이면 조건 제외됩니다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 송신거래 약정키와 식별자 |
| 언제 사용하는가 | 식별자 등록 목록 조회, 식별자 등록 다건 삭제 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 사업장명, 사업자번호, 식별자, 상세 식별자, 은행 식별자, 인증키 |
| 업무 흐름 | 식별자 등록 목록 조회, 식별자 등록 다건 삭제 |
| 이 페이지의 역할 | 조회·관리 · 식별자 등록 목록 조회 |
| 판단 결과·다음 업무 | [상세페이지 URL](identifier-key__by-interIdx.md) · [식별자 정보 등록](identifier-key__new.md) |
| 다른 화면과의 구분 | 이 경로에서 볼 수 있는 조건·결과를 기준으로 사용한다. 독립 경로의 상세·등록은 관련 화면에 연결한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 삭제 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/IdentifierKeyRegisterPage.tsx#L274) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 식별자(SB_INTERFACE_ID) 목록을 조회한다. 모든 검색 조건은 LIKE 매칭이며, 빈값이면 조건 제외됩니다. |
| 메뉴·화면 경로 | SB 서비스관리 > 구매확인서 > 식별자 정보 등록 · `/purchase-confirmation/identifier-key` |
| 화면 유형·담당 | 조회·관리 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [상세페이지 URL](identifier-key__by-interIdx.md) · [식별자 정보 등록](identifier-key__new.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/purchase-confirmation/identifier-key` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 식별자 등록 목록 조회 | `/purchase-confirmation/identifier-key` `VIEW` | `IdentifierKeyListSearchRequest` `localId`, `partnerId`, `comRegNo`, `page`, `size` |
| 식별자 등록 다건 삭제 | `/purchase-confirmation/identifier-key` `DELETE` | `DeleteRequest` `interIdxes`, `reason` · 서버 필수 `interIdxes`, `reason` |

코드에서 확인한 버튼·작업명은 **검색**, **식별자 정보 등록**, **삭제**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **SB 서비스관리 > 구매확인서 > 식별자 정보 등록**를 연다. `/purchase-confirmation/identifier-key`를 연다.
2. **식별자 등록 목록 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
3. 후속 조회나 목록 복귀가 필요하면 [상세페이지 URL](identifier-key__by-interIdx.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 사업장명 | 출력 | 조회 응답 기준 | 화면 필드 `comName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/IdentifierKeyRegisterPage.tsx#L179) |
| 사업자번호 | 입력 또는 선택 | 길이·개수 최대 10 · API 기본값 null | API 요청 `comRegNo` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/IdentifierKeyRegisterPage.tsx#L182) |
| 식별자 | 입력 또는 선택 | 길이·개수 최대 35 · API 기본값 null | API 요청 `localId` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/IdentifierKeyRegisterPage.tsx#L186) |
| 상세 식별자 | 출력 | 조회 응답 기준 | 화면 필드 `localDivisionId` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/IdentifierKeyRegisterPage.tsx#L187) |
| 은행 식별자 | 입력 또는 선택 | 길이·개수 최대 35 · API 기본값 null | API 요청 `partnerId` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/IdentifierKeyRegisterPage.tsx#L188) |
| 인증키 | 출력 | 조회 응답 기준 | 화면 필드 `confirmKey` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/IdentifierKeyRegisterPage.tsx#L189) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 식별자 등록 목록 조회 | `GET /api/v1/purchase-confirmation/identifier-keys` · `/purchase-confirmation/identifier-key` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/purchaseconfirmation/identifierkey/list/IdentifierKeyListController.kt#L49) | `IdentifierKeyListSearchRequest` `localId`, `partnerId`, `comRegNo`, `page`, `size` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `currentPage`, `size` | `smartwork.dbo.sp_GetIdentifierKeyList` · 코드 연계 트랜잭션 |
| 식별자 등록 다건 삭제 | `DELETE /api/v1/purchase-confirmation/identifier-keys` · `/purchase-confirmation/identifier-key` `DELETE` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/purchaseconfirmation/identifierkey/delete/IdentifierKeyDeleteController.kt#L39) | `DeleteRequest` `interIdxes`, `reason` · 서버 필수 `interIdxes`, `reason` → `success`, `data`, `error`, `deletedCount` | `SmartBill3.dbo.SB_INTERFACE_ID_HISTORY`, `SmartBill3.dbo.SB_INTERFACE_ID`, `smartwork.dbo.action_reason` · 정의에서 확인한 쓰기 `SmartBill3.dbo.SB_INTERFACE_ID_HISTORY`, `smartwork.dbo.action_reason` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.sp_GetIdentifierKeyList` | @LocalID varchar(35) = NULL, @PartnerID varchar(35) = NULL, @ComRegNo varchar(10) = NULL, @PageNumber int, @PageSize int | 정의 참조 `SmartBill3.dbo.COMPANY`, `SmartBill3.dbo.SB_INTERFACE_ID` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/purchaseconfirmation/identifierkey/list/repository/IdentifierKeyListMapper.kt#L45) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-aabda9a725813344) |
| `SmartBill3.dbo.SB_INTERFACE_ID_HISTORY` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL INSERT INTO | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/purchaseconfirmation/identifierkey/delete/repository/IdentifierKeyDeleteMapper.kt#L46) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-ab608b79a505a554) |
| `SmartBill3.dbo.SB_INTERFACE_ID` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/purchaseconfirmation/identifierkey/delete/repository/IdentifierKeyDeleteMapper.kt#L46) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-2c36b09de569757a) |
| `smartwork.dbo.action_reason` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL INSERT INTO | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/shared/actionreason/repository/ActionReasonMapper.kt#L16) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b0430106ffe0743f) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 사업장명, 사업자번호, 식별자, 상세 식별자, 은행 식별자, 인증키 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 서비스관리 > 구매확인서 > 식별자 정보 등록의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 전체 선택에 실패했습니다. | 사업장명, 사업자번호, 식별자, 상세 식별자, 은행 식별자, 인증키 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 삭제할 항목을 선택하세요. | 사업장명, 사업자번호, 식별자, 상세 식별자, 은행 식별자, 인증키 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 식별자 등록 삭제에 실패했습니다. | 사업장명, 사업자번호, 식별자, 상세 식별자, 은행 식별자, 인증키 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 검색 결과가 없습니다. | 사업장명, 사업자번호, 식별자, 상세 식별자, 은행 식별자, 인증키 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/PurchaseConfirmationRoutes.tsx#L18) · [IdentifierKeyRegisterPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/IdentifierKeyRegisterPage.tsx#L66) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/api/identifierKeyRegisterApi.ts#L39) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/api/identifierKeyRegisterApi.ts#L54) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 4개 중 개발 메타데이터 확인 4개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-1aa4f39c5116bcaf) | Demo 메타데이터 4/4개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

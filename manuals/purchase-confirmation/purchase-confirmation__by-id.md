# [구매확인서 원문과 품목·참조] 구매확인서 조회 상세 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

list 응답의 mainkey 와 source(A=저장 / B=신청 / C=개설) 로 정확한 1행 조회. 공급자 모드(SUPPLIER_OPEN_COMPLETE) 도 source='C' 로 통합 처리.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 구매확인서 원문과 품목·참조 |
| 언제 사용하는가 | 구매확인서 상세 조회 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | HS부호, 품명 및 규격, 단위, 수량, 구매(공급)일, 단가 |
| 업무 흐름 | 구매확인서 상세 조회 |
| 이 페이지의 역할 | 상세 · 구매확인서 상세 조회 |
| 판단 결과·다음 업무 | [구매확인서 조회](purchase-confirmation.md) |
| 다른 화면과의 구분 | SB 서비스관리 > 구매확인서 > 구매확인서 조회에서 사용하는 상세 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | list 응답의 mainkey 와 source(A=저장 / B=신청 / C=개설) 로 정확한 1행 조회. 공급자 모드(SUPPLIER_OPEN_COMPLETE) 도 source='C' 로 통합 처리. |
| 메뉴·화면 경로 | SB 서비스관리 > 구매확인서 > 구매확인서 조회 · `/purchase-confirmation/purchase-confirmation/:id` · 경로 변수 `id` |
| 화면 유형·담당 | 상세 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [구매확인서 조회](purchase-confirmation.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/purchase-confirmation/purchase-confirmation` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `id` |
| 구매확인서 상세 조회 | `/purchase-confirmation/purchase-confirmation` `VIEW` | `mainkey: String` · `source: String` |

코드에서 확인한 버튼·작업명은 **목록**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [구매확인서 조회](purchase-confirmation.md)에서 대상 또는 작업을 선택한다. `/purchase-confirmation/purchase-confirmation/:id`에서 이전 화면이 전달한 `id`와 현재 대상을 확인한다.
2. **구매확인서 상세 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
3. 후속 조회나 목록 복귀가 필요하면 [구매확인서 조회](purchase-confirmation.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `id` |
| HS부호 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/PurchaseConfirmationDetailPage.tsx#L133) |
| 품명 및 규격 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/PurchaseConfirmationDetailPage.tsx#L134) |
| 단위 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/PurchaseConfirmationDetailPage.tsx#L135) |
| 수량 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/PurchaseConfirmationDetailPage.tsx#L136) |
| 구매(공급)일 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/PurchaseConfirmationDetailPage.tsx#L137) |
| 단가 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/PurchaseConfirmationDetailPage.tsx#L138) |
| 통화코드 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/PurchaseConfirmationDetailPage.tsx#L139) |
| 금액 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/PurchaseConfirmationDetailPage.tsx#L140) |
| 비고 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/PurchaseConfirmationDetailPage.tsx#L141) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 구매확인서 상세 조회 | `GET /api/v1/purchase-confirmation/purchase-confirmations/{mainkey}` · `/purchase-confirmation/purchase-confirmation` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/purchaseconfirmation/detail/PurchaseConfirmationDetailController.kt#L42) | `mainkey: String` · `source: String` → `success`, `data`, `error`, `main`, `items`, `refs` | `smartwork.dbo.sp_GetPurchaseConfirmationDetail`, `SmartBill3.dbo.upDCT_View_PurchaseItem`, `SmartBill3.dbo.upDCT_View_PurchaseItem_s`, `SmartBill3.dbo.upDCT_View_PurchaseREF`, `SmartBill3.dbo.upDCT_View_PurchaseREF_s` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.sp_GetPurchaseConfirmationDetail` | @mainkey varchar(35), @source char(1) | 정의 참조 `KT_Net.dbo.APPPCR_M`, `KT_Net.dbo.PCRLIC_M`, `SmartBill3.dbo.SB_APPPCR_M` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/purchaseconfirmation/detail/repository/PurchaseConfirmationDetailMapper.kt#L98) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-de6663a73e1dc07d) |
| `SmartBill3.dbo.upDCT_View_PurchaseItem` | @strMainKey varchar(35), @div varchar(20) | 정의 참조 `KT_Net.dbo.APPPCR_ITEM`, `KT_Net.dbo.PCRLIC_ITEM`, `SmartBill3.dbo.SB_APPPCR_ITEM` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/purchaseconfirmation/detail/repository/PurchaseConfirmationDetailMapper.kt#L138) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-05f3b8ecf71b2355) |
| `SmartBill3.dbo.upDCT_View_PurchaseItem_s` | @ItemKey varchar(35), @div char(1) | 정의 참조 `KT_Net.dbo.APPPCR_ITEM_S`, `KT_Net.dbo.PCRLIC_ITEM_S`, `SmartBill3.dbo.SB_APPPCR_ITEM_S` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/purchaseconfirmation/detail/repository/PurchaseConfirmationDetailMapper.kt#L158) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b442d19519be8518) |
| `SmartBill3.dbo.upDCT_View_PurchaseREF` | @strMainKey varchar(35), @div varchar(20) | 정의 참조 `KT_Net.dbo.APPPCR_REF`, `KT_Net.dbo.PCRLIC_REF`, `SmartBill3.dbo.SB_APPPCR_REF` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/purchaseconfirmation/detail/repository/PurchaseConfirmationDetailMapper.kt#L185) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3167b130ab942e3b) |
| `SmartBill3.dbo.upDCT_View_PurchaseREF_s` | @strRefKey varchar(35), @div varchar(1) | 정의 참조 `KT_Net.dbo.APPPCR_REF_S`, `KT_Net.dbo.PCRLIC_REF_S`, `SmartBill3.dbo.SB_APPPCR_REF_S` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/purchaseconfirmation/detail/repository/PurchaseConfirmationDetailMapper.kt#L204) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-c63d40c6befef04c) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | HS부호, 품명 및 규격, 단위, 수량, 구매(공급)일, 단가 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 서비스관리 > 구매확인서 > 구매확인서 조회의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 잘못된 접근입니다. | HS부호, 품명 및 규격, 단위, 수량, 구매(공급)일, 단가 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| source 파라미터가 누락되었거나 올바르지 않습니다. | HS부호, 품명 및 규격, 단위, 수량, 구매(공급)일, 단가 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 구매확인서 상세 정보를 불러오는데 실패했습니다. | HS부호, 품명 및 규격, 단위, 수량, 구매(공급)일, 단가 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/PurchaseConfirmationRoutes.tsx#L20) · [PurchaseConfirmationDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/PurchaseConfirmationDetailPage.tsx#L45) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/purchaseconfirmation/api/purchaseConfirmationApi.ts#L60) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 5개 중 개발 메타데이터 확인 5개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-91401c40d6b5548f) | Demo 메타데이터 5/5개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

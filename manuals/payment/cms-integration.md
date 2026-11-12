# [CMS·카드 자동결제와 예외] (EB11) CMS 통합 변경내역 반영 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

금융기관에서 받은 EB11 통합 변경 파일을 등록하고 처리한다. 파일 수신, 업로드, 변경 반영 결과를 각각 확인한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | CMS·카드 자동결제와 예외 |
| 언제 사용하는가 | EB11 헤더 목록 조회, EB11 처리 실행, EB11 파일 업로드 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | EB11 통합 변경 파일과 처리 이력 |
| 업무 흐름 | EB11 헤더 목록 조회, EB11 처리 실행, EB11 파일 업로드 |
| 이 페이지의 역할 | 조회·관리 · EB11 헤더 목록 조회 |
| 판단 결과·다음 업무 | [(EB11) CMS 통합 변경내역 반영 상세](cms-integration__by-fileId.md) |
| 다른 화면과의 구분 | 이 경로에서 볼 수 있는 조건·결과를 기준으로 사용한다. 독립 경로의 상세·등록은 관련 화면에 연결한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 금융기관에서 받은 EB11 통합 변경 파일을 등록하고 처리한다. 파일 수신, 업로드, 변경 반영 결과를 각각 확인한다. |
| 메뉴·화면 경로 | 서비스 현황 > 입금관리 > (EB11) CMS 통합 변경내역 반영 · `/payment/cms-integration` |
| 화면 유형·담당 | 조회·관리 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [(EB11) CMS 통합 변경내역 반영 상세](cms-integration__by-fileId.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/payment/cms-integration` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| EB11 헤더 목록 조회 | `/payment/cms-integration` `VIEW` | `Eb11SearchRequest` `sendYn`, `fileName`, `requestFromDate`, `requestEndDate`, `orderColumn`, `sort`, `fromDate`, `toDate`, `pageSize`, `pageNum` |
| EB11 처리 실행 | `/payment/cms-integration` `PROCESS` | `Eb11ProcessRequest?` `fileIds` |
| EB11 파일 업로드 | `/payment/cms-integration` `PROCESS` | `files: List<MultipartFile>` |

코드에서 확인한 버튼·작업명은 **EB11 파일 등록**, **변경내역 처리**, **파일 선택**, **삭제**, **업로드 진행률**, **취소**, **업로드**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **서비스 현황 > 입금관리 > (EB11) CMS 통합 변경내역 반영**를 연다. `/payment/cms-integration`를 연다.
2. **EB11 파일** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **EB11 파일 등록** 중 해당 버튼을 선택한다.
3. **EB11 헤더 목록 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [(EB11) CMS 통합 변경내역 반영 상세](cms-integration__by-fileId.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 파일명 | 입력 또는 선택 | API 기본값 null | API 요청 `fileName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/CmsIntegrationListPage.tsx#L52) |
| 신청일자 | 출력 | 조회 응답 기준 | 화면 필드 `applicationDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/CmsIntegrationListPage.tsx#L66) |
| 신규건수 | 출력 | 조회 응답 기준 | 화면 필드 `newCount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/CmsIntegrationListPage.tsx#L73) |
| 수정건수 | 출력 | 조회 응답 기준 | 화면 필드 `modifyCount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/CmsIntegrationListPage.tsx#L80) |
| 해지건수 | 출력 | 조회 응답 기준 | 화면 필드 `cancelCount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/CmsIntegrationListPage.tsx#L87) |
| 임의해지건수 | 출력 | 조회 응답 기준 | 화면 필드 `arbitraryCancelCount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/CmsIntegrationListPage.tsx#L94) |
| 계 | 출력 | 조회 응답 기준 | 화면 필드 `totalCount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/CmsIntegrationListPage.tsx#L101) |
| 전송적용여부 | 출력 | 조회 응답 기준 | 화면 필드 `transmissionStatus` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/CmsIntegrationListPage.tsx#L108) |
| 등록일시 | 출력 | 조회 응답 기준 | 화면 필드 `registrationDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/CmsIntegrationListPage.tsx#L115) |
| EB11 파일 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CmsFileInput.tsx#L32) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| EB11 헤더 목록 조회 | `GET /api/v1/payment/cms-eb11` · `/payment/cms-integration` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/cmseb11/Eb11HeaderController.kt#L72) | `Eb11SearchRequest` `sendYn`, `fileName`, `requestFromDate`, `requestEndDate`, `orderColumn`, `sort`, `fromDate`, `toDate`, `pageSize`, `pageNum` → `success`, `data`, `error`, `content`, `totalElements` | `SB_BILL.dbo.UspCMS_LIST_EB11_HEADER` · 코드 연계 트랜잭션 |
| EB11 처리 실행 | `PUT /api/v1/payment/cms-eb11/process` · `/payment/cms-integration` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/cmseb11/Eb11HeaderController.kt#L131) | `Eb11ProcessRequest?` `fileIds` → `success`, `data`, `error`, `processedCount`, `resultCode` | `smartwork.dbo.USPCMS_PROCESS_EB11_IDX` · 정의에서 확인한 쓰기 `SmartBill3.dbo.CMS_ACCOUNT_MAIN_CUB`, `SmartBill3.dbo.CMS_ACCOUNT_EB11_CUB`, `SmartBill3.dbo.CMS_MAPPING_CUB`, `SmartBill3.dbo.CMS_EA11` · 코드 연계 트랜잭션 |
| EB11 파일 업로드 | `POST /api/v1/payment/cms-eb11/create` · `/payment/cms-integration` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/cmseb11/Eb11HeaderController.kt#L146) | `files: List<MultipartFile>` → `success`, `data`, `error` | `SB_BILL.dbo.UspCMS_SAVE_EB11_HEADER`, `SB_BILL.dbo.UspCMS_SAVE_EB11_DATA` · 정의에서 확인한 쓰기 `SmartBill3.dbo.CMS_EA11`, `SmartBill3.dbo.CMS_EA11_DETAIL_CUB` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `SB_BILL.dbo.UspCMS_LIST_EB11_HEADER` | @SENDYN varchar(1), @FILENAME varchar(8), @REQUESTFROMDATE varchar(6), @REQUESTENDDATE varchar(6), @ORDERCOLUMN varchar(30), @SORT varchar(5), @FROMDATE datetime, @TODATE datetime, @PAGESIZE int, @PAGENUM int | 정의 참조 `SmartBill3.dbo.CMS_EA11` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmseb11/repository/Eb11HeaderMapper.kt#L37) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-c2a3369e6aa5deaa) |
| `smartwork.dbo.USPCMS_PROCESS_EB11_IDX` | @IDXS nvarchar(max), @RESULT varchar(5) OUT | 정의 참조 `master.dbo.CLR_sqlsplit`, `SmartBill3.dbo.CMS_ACCOUNT_EB11_CUB`, `SmartBill3.dbo.CMS_ACCOUNT_MAIN_CUB`, `SmartBill3.dbo.CMS_EA11`, `SmartBill3.dbo.CMS_EA11_DETAIL_CUB` 외 1개 · 정적 쓰기 `SmartBill3.dbo.CMS_ACCOUNT_MAIN_CUB`, `SmartBill3.dbo.CMS_ACCOUNT_EB11_CUB`, `SmartBill3.dbo.CMS_MAPPING_CUB`, `SmartBill3.dbo.CMS_EA11` · 하위 호출 `master.dbo.CLR_sqlsplit` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmseb11/repository/Eb11DetailMapper.kt#L93) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-1417fe7e1eda09df) |
| `SB_BILL.dbo.UspCMS_SAVE_EB11_HEADER` | @RECORDFLAG varchar(1), @SERIALNUM varchar(8), @ORGANCODE varchar(10), @FILENAME varchar(8), @REQUESTDATE varchar(6), @FILLER varchar(87), @NEW_CNT int, @MOD_CNT int, @END_CNT int, @ENDOWN_CNT int, @TOTAL_CNT int, @RESULT varchar(5) OUT, @IDX int OUT | 정의 참조 `SmartBill3.dbo.CMS_EA11` · 정적 쓰기 `SmartBill3.dbo.CMS_EA11` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmseb11/repository/Eb11CreateMapper.kt#L17) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-48680375b92a441e) |
| `SB_BILL.dbo.UspCMS_SAVE_EB11_DATA` | @EB11_IDX int, @RECORDFLAG varchar(1), @DATASERIALNUM varchar(8), @ORGANCODE varchar(10), @REQUESTDATE varchar(6), @REQUESTTYPE varchar(1), @PAYERNUM varchar(20), @BANKCODE varchar(7), @ACCOUNTNUM varchar(16), @REGNUM varchar(16), @DEALERCODE varchar(4), @FUNDTYPE varchar(2), @TRANRESULTCODE varchar(1), @TRANDISCODE varchar(4), @TELNUM varchar(12), @RESULT varchar(5) OUT | 정의 참조 `SmartBill3.dbo.CMS_EA11_DETAIL_CUB`, `master.dbo.enc_char_ins_tc` · 정적 쓰기 `SmartBill3.dbo.CMS_EA11_DETAIL_CUB` · 하위 호출 `master.dbo.enc_char_ins_tc` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmseb11/repository/Eb11CreateMapper.kt#L21) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-8c19c2e2ebaf4511) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | EB11 통합 변경 파일과 처리 이력 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 서비스 현황 > 입금관리 > (EB11) CMS 통합 변경내역 반영의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 파일 목록 조회 중 오류가 발생했습니다. | EB11 통합 변경 파일과 처리 이력 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 처리할 파일을 선택해주세요. | EB11 통합 변경 파일과 처리 이력 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 변경내역 처리 중 오류가 발생했습니다. | EB11 통합 변경 파일과 처리 이력 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 파일 업로드 중 오류가 발생했습니다. | EB11 통합 변경 파일과 처리 이력 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/PaymentRoutes.tsx#L85) · [CmsIntegrationListPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/CmsIntegrationListPage.tsx#L19) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/cmsIntegrationApi.ts#L137) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/cmsIntegrationApi.ts#L228) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/cmsIntegrationApi.ts#L194) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 4개 중 개발 메타데이터 확인 4개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-719710b3c7f6a2e5) | Demo 메타데이터 4/4개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

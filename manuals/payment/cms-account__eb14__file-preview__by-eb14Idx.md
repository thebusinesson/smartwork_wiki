# [CMS·카드 자동결제와 예외] (EB13/EB14) CMS 계좌 관리 상세 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

EB14 미반영 파일 반영 데이터를 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | CMS·카드 자동결제와 예외 |
| 언제 사용하는가 | EB14 파일 미리보기, EB14 파일 미리보기 적용 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 회사명, 사업자번호, 이체은행, 계좌번호, 주민/사업자번호, 예금주명 |
| 업무 흐름 | EB14 파일 미리보기, EB14 파일 미리보기 적용 |
| 이 페이지의 역할 | 상세 · EB14 파일 미리보기 |
| 판단 결과·다음 업무 | [(EB13/EB14) CMS 계좌 관리](cms-account.md) |
| 다른 화면과의 구분 | 서비스 현황 > 입금관리 > (EB13/EB14) CMS 계좌 관리에서 사용하는 상세 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 확인 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/CmsAccountPendingResultDetailPage.tsx#L154) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | EB14 미반영 파일 반영 데이터를 조회한다. |
| 메뉴·화면 경로 | 서비스 현황 > 입금관리 > (EB13/EB14) CMS 계좌 관리 · `/payment/cms-account/eb14/file-preview/:eb14Idx` · 경로 변수 `eb14Idx` |
| 화면 유형·담당 | 상세 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [(EB13/EB14) CMS 계좌 관리](cms-account.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/payment/cms-account` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `eb14Idx` |
| EB14 파일 미리보기 | `/payment/cms-account` `VIEW` | `idx: Long` |
| EB14 파일 미리보기 적용 | `/payment/cms-account` `PROCESS` | `idx: Long` |

코드에서 확인한 버튼·작업명은 **목록**, **계좌신청(EB13)**, **계좌결과 반영(EB14)**, **파일반영하기**, **확인**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [(EB13/EB14) CMS 계좌 관리](cms-account.md)에서 대상 또는 작업을 선택한다. `/payment/cms-account/eb14/file-preview/:eb14Idx`에서 이전 화면이 전달한 `eb14Idx`와 현재 대상을 확인한다.
2. **EB14 파일 미리보기** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
3. 후속 조회나 목록 복귀가 필요하면 [(EB13/EB14) CMS 계좌 관리](cms-account.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `eb14Idx` |
| 회사명 | 출력 | 조회 응답 기준 | 화면 필드 `companyName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CmsAccountPendingResultDetailTable.tsx#L18) |
| 사업자번호 | 출력 | 조회 응답 기준 | 화면 필드 `businessNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CmsAccountPendingResultDetailTable.tsx#L19) |
| 이체은행 | 출력 | 조회 응답 기준 | 화면 필드 `bankName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CmsAccountPendingResultDetailTable.tsx#L20) |
| 계좌번호 | 출력 | 조회 응답 기준 | 화면 필드 `accountNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CmsAccountPendingResultDetailTable.tsx#L22) |
| 주민/사업자번호 | 출력 | 조회 응답 기준 | 화면 필드 `businessOrPersonalNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CmsAccountPendingResultDetailTable.tsx#L26) |
| 예금주명 | 출력 | 조회 응답 기준 | 화면 필드 `accountHolder` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CmsAccountPendingResultDetailTable.tsx#L29) |
| 결과코드 | 출력 | 조회 응답 기준 | 화면 필드 `resultCode` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CmsAccountPendingResultDetailTable.tsx#L30) |
| 불능코드 | 출력 | 조회 응답 기준 | 화면 필드 `errorCode` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CmsAccountPendingResultDetailTable.tsx#L31) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| EB14 파일 미리보기 | `GET /api/v1/payment/cms-account/eb14/file-preview/{idx}` · `/payment/cms-account` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/cmsaccount/CmsAccountEb14Controller.kt#L146) | `idx: Long` → `success`, `data`, `error`, `id`, `eb14FileName`, `fileAppDate`, `newFailedCount`, `endFailedCount`, `resultList`, `totalElements` | `SmartBill3.dbo.CMS_EA14`, `SmartBill3.dbo.upCMS_SchErrCom14` |
| EB14 파일 미리보기 적용 | `POST /api/v1/payment/cms-account/eb14/file-preview/{idx}/apply` · `/payment/cms-account` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/cmsaccount/CmsAccountEb14Controller.kt#L166) | `idx: Long` → `success`, `data`, `error` | `SmartBill3.dbo.CMS_EA14`, `SmartBill3.dbo.upCMS_UptEA14`, `SmartBill3.dbo.upCMS_UptEA14Dtl`, `SmartBill3.dbo.upCMS_UptEA14Dtl02`, `SmartBill3.dbo.CMS_EA14_DETAIL_CUB` 외 5개 · 정의에서 확인한 쓰기 `SmartBill3.dbo.CMS_EA14`, `SmartBill3.dbo.CMS_EA14_DETAIL_CUB`, `SmartBill3.dbo.CMS_EA14_DETAIL`, `SmartBill3.dbo.CMS_ACCOUNT_MAIN_CUB` 외 1개 · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `SmartBill3.dbo.CMS_EA14` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb14AccountMapper.kt#L55) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3229f827e97f2667) |
| `SmartBill3.dbo.upCMS_SchErrCom14` | @payer_no int | 정의 참조 `SB_BILL.dbo.BILL_COMMON_CODE`, `SmartBill3.dbo.CMS_ACCOUNT_MAIN`, `SmartBill3.dbo.COMPANY` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb14AccountMapper.kt#L178) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-e05e306de0775695) |
| `SmartBill3.dbo.upCMS_UptEA14` | @idx int, @file_appdate varchar(6), @newcnt int, @modcnt int, @endcnt int, @endowncnt int | 정의 참조 `SmartBill3.dbo.CMS_EA14` · 정적 쓰기 `SmartBill3.dbo.CMS_EA14` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb14AccountMapper.kt#L190) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-12549616f77f3820) |
| `SmartBill3.dbo.upCMS_UptEA14Dtl` | @EA14_IDX int, @PAYER_NO char(20), @RSLT_CODE char(1), @ERR_CODE varchar(4) | 정의 참조 `SmartBill3.dbo.CMS_EA14_DETAIL_CUB` · 정적 쓰기 `SmartBill3.dbo.CMS_EA14_DETAIL_CUB` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb14AccountMapper.kt#L201) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-81420d4aa6676910) |
| `SmartBill3.dbo.upCMS_UptEA14Dtl02` | @EA14_IDX int | 정의 참조 `SmartBill3.dbo.CMS_EA14_DETAIL` · 정적 쓰기 `SmartBill3.dbo.CMS_EA14_DETAIL` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb14AccountMapper.kt#L210) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3d4bb05787e88dac) |
| `SmartBill3.dbo.CMS_EA14_DETAIL_CUB` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb14AccountMapper.kt#L166) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-9a14be878da3eade) |
| `SmartBill3.dbo.COMPANY` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb14AccountMapper.kt#L166) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-0e6fcaa6b5086c07) |
| `SmartBill3.dbo.MEMBER` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb14AccountMapper.kt#L166) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-9042ff61b257b012) |
| `SmartBill3.dbo.COMMON_CODE` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb14AccountMapper.kt#L166) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-49b15682b4d4770c) |
| `SB_BILL.dbo.BILL_COMMON_CODE` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb14AccountMapper.kt#L166) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b05907f373842dd1) |
| `SmartBill3.dbo.upCMS_UptCmsMain` | @PAYER_NO int, @RSLT_CODE varchar(1) | 정의 참조 `SmartBill3.dbo.CMS_ACCOUNT_MAIN_CUB`, `SmartBill3.dbo.CMS_MAPPING_CUB` · 정적 쓰기 `SmartBill3.dbo.CMS_ACCOUNT_MAIN_CUB`, `SmartBill3.dbo.CMS_MAPPING_CUB` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb14AccountMapper.kt#L214) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-321da3996a28dd5b) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 회사명, 사업자번호, 이체은행, 계좌번호, 주민/사업자번호, 예금주명 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 서비스 현황 > 입금관리 > (EB13/EB14) CMS 계좌 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 결제원으로 신청한 모든 업체가 승인되었습니다. 결과를 적용해주세요. | 회사명, 사업자번호, 이체은행, 계좌번호, 주민/사업자번호, 예금주명 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/PaymentRoutes.tsx#L82) · [CmsAccountPendingResultDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/CmsAccountPendingResultDetailPage.tsx#L16) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/cmsAccountResultApi.ts#L212) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/cmsAccountResultApi.ts#L330) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 11개 중 개발 메타데이터 확인 11개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-b5cfbd89c8c4a250) | Demo 메타데이터 11/11개 확인 · Dev와 계약 차이 3개 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

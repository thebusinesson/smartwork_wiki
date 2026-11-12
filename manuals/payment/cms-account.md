# [CMS·카드 자동결제와 예외] (EB13/EB14) CMS 계좌 관리 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

CMS 출금 계좌 신청 자료(EB13)와 금융기관 처리 결과(EB14)를 관리한다. 신청, 전송 확인, 결과 수신을 단계별로 확인한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | CMS·카드 자동결제와 예외 |
| 언제 사용하는가 | EB13 목록 조회, EB14 목록 조회, EB13 전송 확인, EB13 파일 삭제 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | EB13 신청 파일, EB14 결과 파일 |
| 업무 흐름 | EB13 목록 조회, EB14 목록 조회, EB13 전송 확인, EB13 파일 삭제 |
| 이 페이지의 역할 | 조회·관리 · EB13 목록 조회 |
| 판단 결과·다음 업무 | [(EB13/EB14) CMS 계좌 관리 조회·관리](cms-account__apply.md) · [EB13 계좌신청 상세 다운로드](cms-account__eb13__by-id.md) · [(EB13/EB14) CMS 계좌 관리 신청 정보](cms-account__eb14__application__by-eb13Idx.md) · [(EB13/EB14) CMS 계좌 관리 등록](cms-account__eb14__upload__by-eb13Idx__new.md) · [(EB13/EB14) CMS 계좌 관리 처리 결과](cms-account__eb14__result__by-eb14Idx.md) · [(EB13/EB14) CMS 계좌 관리 상세](cms-account__eb14__file__by-eb14Idx.md) · [(EB13/EB14) CMS 계좌 관리 상세](cms-account__eb14__file-preview__by-eb14Idx.md) |
| 다른 화면과의 구분 | 이 경로에서 볼 수 있는 조건·결과를 기준으로 사용한다. 독립 경로의 상세·등록은 관련 화면에 연결한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 확인 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/CmsAccountListPage.tsx#L263) |
| 삭제 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/CmsAccountListPage.tsx#L278) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | CMS 출금 계좌 신청 자료(EB13)와 금융기관 처리 결과(EB14)를 관리한다. 신청, 전송 확인, 결과 수신을 단계별로 확인한다. |
| 메뉴·화면 경로 | 서비스 현황 > 입금관리 > (EB13/EB14) CMS 계좌 관리 · `/payment/cms-account` |
| 화면 유형·담당 | 조회·관리 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [(EB13/EB14) CMS 계좌 관리 조회·관리](cms-account__apply.md) · [EB13 계좌신청 상세 다운로드](cms-account__eb13__by-id.md) · [(EB13/EB14) CMS 계좌 관리 신청 정보](cms-account__eb14__application__by-eb13Idx.md) · [(EB13/EB14) CMS 계좌 관리 등록](cms-account__eb14__upload__by-eb13Idx__new.md) · [(EB13/EB14) CMS 계좌 관리 처리 결과](cms-account__eb14__result__by-eb14Idx.md) · [(EB13/EB14) CMS 계좌 관리 상세](cms-account__eb14__file__by-eb14Idx.md) · [(EB13/EB14) CMS 계좌 관리 상세](cms-account__eb14__file-preview__by-eb14Idx.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/payment/cms-account` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| EB13 목록 조회 | `/payment/cms-account` `VIEW` | `Eb13SearchRequest` `dateAll`, `fromDate`, `toDate` |
| EB14 목록 조회 | `/payment/cms-account` `VIEW` | `Eb14SearchRequest` `dateAll`, `fromDate`, `toDate` |
| EB13 전송 확인 | `/payment/cms-account` `PROCESS` | `Eb13SendConfirmRequest` `idx` |
| EB13 파일 삭제 | `/payment/cms-account` `DELETE` | `idx: Long` |

코드에서 확인한 버튼·작업명은 **계좌신청(EB13)**, **계좌결과 반영(EB14)**, **검색**, **계좌신청 생성**, **확인**, **삭제**, **업로드**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **서비스 현황 > 입금관리 > (EB13/EB14) CMS 계좌 관리**를 연다. `/payment/cms-account`를 연다.
2. **자료 생성일**, **출금이체 신청일** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색**, **확인** 중 해당 버튼을 선택한다.
3. **EB13 목록 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [(EB13/EB14) CMS 계좌 관리 조회·관리](cms-account__apply.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 자료 생성일 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/CmsAccountListPage.tsx#L49) |
| 계좌이체 신청일자 | 출력 | 조회 응답 기준 | 화면 필드 `accountTransferRequestDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CmsAccountTable.tsx#L44) |
| 신규업체수 | 출력 | 조회 응답 기준 | 화면 필드 `newCompanyCount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CmsAccountTable.tsx#L58) |
| 해지업체수 | 출력 | 조회 응답 기준 | 화면 필드 `terminatedCompanyCount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CmsAccountTable.tsx#L64) |
| EB13파일명 | 출력 | 조회 응답 기준 | 화면 필드 `eb13FileName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CmsAccountTable.tsx#L70) |
| 송신여부 | 출력 | 조회 응답 기준 | 화면 필드 `transmissionStatus` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CmsAccountTable.tsx#L92) |
| 비고 | 출력 | 조회 응답 기준 | 화면 필드 `remarks` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CmsAccountTable.tsx#L112) |
| 출금이체 신청일 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/CmsAccountResultListPage.tsx#L35) |
| 출금이체신청 일자 | 출력 | 조회 응답 기준 | 화면 필드 `accountTransferRequestDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CmsAccountResultTable.tsx#L161) |
| 신청정보 | 출력 | 조회 응답 기준 | 화면 필드 `applicationInfo` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CmsAccountResultTable.tsx#L41) |
| 결과정보 | 출력 | 조회 응답 기준 | 화면 필드 `resultInfo` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CmsAccountResultTable.tsx#L48) |
| 파일명 | 출력 | 조회 응답 기준 | 화면 필드 `applicationFileName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CmsAccountResultTable.tsx#L57) |
| 결과반영여부 | 출력 | 조회 응답 기준 | 화면 필드 `resultReflectionStatus` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CmsAccountResultTable.tsx#L128) |
| 오류업체수 | 출력 | 조회 응답 기준 | 화면 필드 `errorCompanyCount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CmsAccountResultTable.tsx#L150) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| EB13 목록 조회 | `GET /api/v1/payment/cms-account/eb13` · `/payment/cms-account` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/cmsaccount/CmsAccountEb13Controller.kt#L81) | `Eb13SearchRequest` `dateAll`, `fromDate`, `toDate` → `success`, `data`, `error`, `content`, `totalElements` | `SmartBill3.dbo.upCMS_Lst_EA13` |
| EB14 목록 조회 | `GET /api/v1/payment/cms-account/eb14` · `/payment/cms-account` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/cmsaccount/CmsAccountEb14Controller.kt#L71) | `Eb14SearchRequest` `dateAll`, `fromDate`, `toDate` → `success`, `data`, `error`, `content`, `totalElements` | `SmartBill3.dbo.upCMS_Lst1314` · 코드 연계 트랜잭션 |
| EB13 전송 확인 | `POST /api/v1/payment/cms-account/eb13/registration/send-confirm` · `/payment/cms-account` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/cmsaccount/CmsAccountEb13Controller.kt#L217) | `Eb13SendConfirmRequest` `idx` → `success`, `data`, `error`, `message` | `SmartBill3.dbo.upCMS_Sav_EA13Status` · 정의에서 확인한 쓰기 `SmartBill3.dbo.CMS_EA13` · 코드 연계 트랜잭션 |
| EB13 파일 삭제 | `DELETE /api/v1/payment/cms-account/eb13/{idx}` · `/payment/cms-account` `DELETE` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/cmsaccount/CmsAccountEb13Controller.kt#L276) | `idx: Long` → `success`, `data`, `error` | `SmartBill3.dbo.CMS_EA13`, `SmartBill3.dbo.upCMS_Del_EA13` · 정의에서 확인한 쓰기 `SmartBill3.dbo.CMS_EA13_DETAIL_CUB`, `SmartBill3.dbo.CMS_EA13` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `SmartBill3.dbo.upCMS_Lst_EA13` | @fromdate varchar(10), @todate varchar(10) | 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb13AccountMapper.kt#L49) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-a0539bac0c9dd014) |
| `SmartBill3.dbo.upCMS_Lst1314` | @fmDate varchar(8), @toDate varchar(8) | 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb14AccountMapper.kt#L71) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-f580bd43163d5f1d) |
| `SmartBill3.dbo.upCMS_Sav_EA13Status` | @EA13_IDX int | 정의 참조 `SmartBill3.dbo.CMS_EA13` · 정적 쓰기 `SmartBill3.dbo.CMS_EA13` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb13AccountMapper.kt#L214) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b646aaf1bcc92e33) |
| `SmartBill3.dbo.CMS_EA13` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb13AccountMapper.kt#L232) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-07d8f558e1ace85d) |
| `SmartBill3.dbo.upCMS_Del_EA13` | @IDX int | 정의 참조 `SmartBill3.dbo.CMS_EA13`, `SmartBill3.dbo.CMS_EA13_DETAIL_CUB` · 정적 쓰기 `SmartBill3.dbo.CMS_EA13_DETAIL_CUB`, `SmartBill3.dbo.CMS_EA13` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb13AccountMapper.kt#L236) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-1cc6d50bcf44b5c9) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | EB13 신청 파일, EB14 결과 파일 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 서비스 현황 > 입금관리 > (EB13/EB14) CMS 계좌 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 생성된 파일을 목록에서 찾지 못했습니다. 조회 조건을 확인해 주세요. | EB13 신청 파일, EB14 결과 파일 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 검색 결과가 없습니다. | EB13 신청 파일, EB14 결과 파일 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/PaymentRoutes.tsx#L76) · [CmsAccountManagementPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/CmsAccountManagementPage.tsx#L9) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/cmsAccountApi.ts#L51) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/cmsAccountResultApi.ts#L151) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/cmsAccountApi.ts#L71) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/cmsAccountApi.ts#L108) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 5개 중 개발 메타데이터 확인 5개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-9b8023977c5eb8b2) | Demo 메타데이터 5/5개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

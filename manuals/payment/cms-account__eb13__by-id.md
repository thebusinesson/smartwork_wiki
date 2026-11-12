# [CMS·카드 자동결제와 예외] EB13 계좌신청 상세 다운로드 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

EB13 계좌신청 상세 전체를 엑셀로 다운로드한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | CMS·카드 자동결제와 예외 |
| 언제 사용하는가 | EB13 상세 조회, EB13 상세 엑셀 다운로드 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 회사명, 사업자번호, 이체은행, 계좌번호, 예금주, 납부자번호 |
| 업무 흐름 | EB13 상세 조회, EB13 상세 엑셀 다운로드 |
| 이 페이지의 역할 | 상세 · EB13 상세 엑셀 다운로드 |
| 판단 결과·다음 업무 | [(EB13/EB14) CMS 계좌 관리](cms-account.md) |
| 다른 화면과의 구분 | 서비스 현황 > 입금관리 > (EB13/EB14) CMS 계좌 관리에서 사용하는 상세 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | EB13 계좌신청 상세 전체를 엑셀로 다운로드한다. |
| 메뉴·화면 경로 | 서비스 현황 > 입금관리 > (EB13/EB14) CMS 계좌 관리 · `/payment/cms-account/eb13/:id` · 경로 변수 `id` |
| 화면 유형·담당 | 상세 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [(EB13/EB14) CMS 계좌 관리](cms-account.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/payment/cms-account` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `id` |
| EB13 상세 조회 | `/payment/cms-account` `VIEW` | `idx: Long` · `searchKeyword: String?` |
| EB13 상세 엑셀 다운로드 | `/payment/cms-account` `EXCEL_DOWNLOAD` | `idx: Long` · `searchKeyword: String?` |

코드에서 확인한 버튼·작업명은 **목록으로 돌아가기**, **계좌신청(EB13)**, **계좌결과 반영(EB14)**, **검색**, **다운로드**, **목록**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [(EB13/EB14) CMS 계좌 관리](cms-account.md)에서 대상 또는 작업을 선택한다. `/payment/cms-account/eb13/:id`에서 이전 화면이 전달한 `id`와 현재 대상을 확인한다.
2. **EB13 상세 엑셀 다운로드** 처리 결과를 확인하고 받은 파일의 대상과 적용 조건을 대조한다.
3. 후속 조회나 목록 복귀가 필요하면 [(EB13/EB14) CMS 계좌 관리](cms-account.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `id` |
| 회사명 | 출력 | 조회 응답 기준 | 화면 필드 `companyName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CmsAccountDetailTable.tsx#L8) |
| 사업자번호 | 출력 | 조회 응답 기준 | 화면 필드 `businessNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CmsAccountDetailTable.tsx#L9) |
| 이체은행 | 출력 | 조회 응답 기준 | 화면 필드 `bankName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CmsAccountDetailTable.tsx#L10) |
| 계좌번호 | 출력 | 조회 응답 기준 | 화면 필드 `accountNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CmsAccountDetailTable.tsx#L12) |
| 예금주 | 출력 | 조회 응답 기준 | 화면 필드 `accountHolder` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CmsAccountDetailTable.tsx#L15) |
| 납부자번호 | 출력 | 조회 응답 기준 | 화면 필드 `payerNumber` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CmsAccountDetailTable.tsx#L18) |
| 구분 | 출력 | 조회 응답 기준 | 화면 필드 `processTypeLabel` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/components/CmsAccountDetailTable.tsx#L30) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| EB13 상세 조회 | `GET /api/v1/payment/cms-account/eb13/{idx}` · `/payment/cms-account` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/cmsaccount/CmsAccountEb13Controller.kt#L98) | `idx: Long` · `searchKeyword: String?` → `success`, `data`, `error`, `items`, `totalElements` | `SmartBill3.dbo.CMS_EA13_DETAIL_CUB`, `SmartBill3.dbo.COMPANY`, `SB_BILL.dbo.BILL_COMMON_CODE` · 코드 연계 트랜잭션 |
| EB13 상세 엑셀 다운로드 | `GET /api/v1/payment/cms-account/eb13/{idx}/detail/download` · `/payment/cms-account` `EXCEL_DOWNLOAD` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/status/payment/cmsaccount/CmsAccountEb13Controller.kt#L111) | `idx: Long` · `searchKeyword: String?` → 파일 또는 오류 응답 | `SmartBill3.dbo.CMS_EA13_DETAIL_CUB`, `SmartBill3.dbo.COMPANY`, `SB_BILL.dbo.BILL_COMMON_CODE` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `SmartBill3.dbo.CMS_EA13_DETAIL_CUB` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb13AccountMapper.kt#L128) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-c7612d73cdc975a4) |
| `SmartBill3.dbo.COMPANY` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb13AccountMapper.kt#L128) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-0e6fcaa6b5086c07) |
| `SB_BILL.dbo.BILL_COMMON_CODE` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb13AccountMapper.kt#L128) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b05907f373842dd1) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 회사명, 사업자번호, 이체은행, 계좌번호, 예금주, 납부자번호 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 서비스 현황 > 입금관리 > (EB13/EB14) CMS 계좌 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 다운로드에 실패했습니다. | 회사명, 사업자번호, 이체은행, 계좌번호, 예금주, 납부자번호 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 계좌 정보가 없습니다. | 회사명, 사업자번호, 이체은행, 계좌번호, 예금주, 납부자번호 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/PaymentRoutes.tsx#L78) · [CmsAccountDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/CmsAccountDetailPage.tsx#L22) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/cmsAccountApi.ts#L86) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/status/payment/api/cmsAccountApi.ts#L98) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 3개 중 개발 메타데이터 확인 3개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-a133f02686736a1e) | Demo 메타데이터 3/3개 확인 · Dev와 계약 차이 1개 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

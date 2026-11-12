# [서비스 공지 메일과 발송 이력] 메일 발송 고객 정보 조회 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

메일 발송 고객 정보 조회에서 **발송 이력 목록** 결과를 확인한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 서비스 공지 메일과 발송 이력 |
| 언제 사용하는가 | 발송 이력 단건 상세, 발송 이력 목록, 발송 대상 업체 다운로드 (CSV) 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 발송일시, 제목, 발송대상 업체수, 발송결과, 다운로드, 발송일자 |
| 업무 흐름 | 발송 이력 단건 상세, 발송 이력 목록, 발송 대상 업체 다운로드 (CSV) |
| 이 페이지의 역할 | 이력 조회 · 발송 이력 목록 |
| 판단 결과·다음 업무 | 현재 화면에서 결과를 확인한다. |
| 다른 화면과의 구분 | 같은 경로에서 열리는 조회·팝업은 이 문서에서 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 메일 발송 고객 정보 조회에서 **발송 이력 목록** 결과를 확인한다. |
| 메뉴·화면 경로 | 연동 서비스 관리 > 서비스 공지 메일관리 > 메일 발송 고객 정보 조회 · `/hub-service/service-notice-email/send-history` |
| 화면 유형·담당 | 이력 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | 현재 화면에서 결과를 확인한다. |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/hub-service/service-notice-email/send-history` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 발송 이력 단건 상세 | `/hub-service/service-notice-email/send-history` `VIEW` | `id: Long` |
| 발송 이력 목록 | `/hub-service/service-notice-email/send-history` `VIEW` | `startDate: String?` · `endDate: String?` · `page: Int` · `size: Int` |
| 발송 대상 업체 다운로드 (CSV) | `/hub-service/service-notice-email/send-history` `EXCEL_DOWNLOAD` | `id: Long` |

코드에서 확인한 버튼·작업명은 **발송대상 업체 다운로드**, **검색**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **연동 서비스 관리 > 서비스 공지 메일관리 > 메일 발송 고객 정보 조회**를 연다. `/hub-service/service-notice-email/send-history`를 연다.
2. **발송일자**, **발송 대상 업체수**, **발송 결과**, **메일 내용** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **발송대상 업체 다운로드**, **검색** 중 해당 버튼을 선택한다.
3. **발송 이력 목록** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 발송일시 | 출력 | 조회 응답 기준 | API 응답 `sendDateTime` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/service-notice-email/pages/EmailSendingHistoryPage.tsx#L198) |
| 제목 | 출력 | 조회 응답 기준 | API 응답 `emailTitle` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/service-notice-email/pages/EmailSendingHistoryPage.tsx#L206) |
| 발송대상 업체수 | 출력 | 조회 응답 기준 | API 응답 `targetCompanyCount` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/service-notice-email/pages/EmailSendingHistoryPage.tsx#L220) |
| 발송결과 | 출력 | 조회 응답 기준 | API 응답 `sendResult` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/service-notice-email/pages/EmailSendingHistoryPage.tsx#L228) |
| 다운로드 | 출력 | 조회 응답 기준 | 화면 필드 `download` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/service-notice-email/pages/EmailSendingHistoryPage.tsx#L237) |
| 발송일자 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/service-notice-email/pages/EmailSendingHistoryPage.tsx#L25) |
| 발송 대상 업체수 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/service-notice-email/pages/EmailSendingHistoryPage.tsx#L300) |
| 발송 결과 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/service-notice-email/pages/EmailSendingHistoryPage.tsx#L304) |
| 메일 내용 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/service-notice-email/pages/EmailSendingHistoryPage.tsx#L310) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 발송 이력 단건 상세 | `GET /api/v1/service-notice-email/send-history/{id}` · `/hub-service/service-notice-email/send-history` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/servicenoticemail/ServiceNoticeMailController.kt#L85) | `id: Long` → `success`, `data`, `error`, `id`, `sendDateTime`, `emailTitle`, `emailContent`, `targetCompanyCount`, `sendResult`, `recipientCompanies` | `smartwork.dbo.UspServiceNoticeMailSend_Detail`, `office.dbo.upSM_mailComList` |
| 발송 이력 목록 | `GET /api/v1/service-notice-email/send-history` · `/hub-service/service-notice-email/send-history` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/servicenoticemail/ServiceNoticeMailController.kt#L66) | `startDate: String?` · `endDate: String?` · `page: Int` · `size: Int` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `size`, `number` | `smartwork.dbo.UspServiceNoticeMailSend_List` |
| 발송 대상 업체 다운로드 (CSV) | `GET /api/v1/service-notice-email/send-history/{id}/recipients/download` · `/hub-service/service-notice-email/send-history` `EXCEL_DOWNLOAD` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubservice/servicenoticemail/ServiceNoticeMailController.kt#L101) | `id: Long` → 파일 또는 오류 응답 | `smartwork.dbo.UspServiceNoticeMailSend_Detail`, `office.dbo.upSM_mailComList` |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.UspServiceNoticeMailSend_Detail` | @no int | 정의 참조 `office.dbo.ServiceMail_Send` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/servicenoticemail/repository/ServiceNoticeMailSendMapper.kt#L56) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-13d2b9af035a795f) |
| `office.dbo.upSM_mailComList` | @PAGENUM int, @PAGESIZE int | 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/servicenoticemail/repository/EmailVendorMapper.kt#L53) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-dcf5c0aba79a23a8) |
| `smartwork.dbo.UspServiceNoticeMailSend_List` | @startDate datetime, @endDate datetime | 정의 참조 `office.dbo.ServiceMail`, `office.dbo.ServiceMail_Send` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/servicenoticemail/repository/ServiceNoticeMailSendMapper.kt#L40) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-88984d44d714a714) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 발송일시, 제목, 발송대상 업체수, 발송결과, 다운로드, 발송일자 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 연동 서비스 관리 > 서비스 공지 메일관리 > 메일 발송 고객 정보 조회의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 상세 정보 조회에 실패했습니다 | 발송일시, 제목, 발송대상 업체수, 발송결과, 다운로드, 발송일자 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 다운로드에 실패했습니다 | 발송일시, 제목, 발송대상 업체수, 발송결과, 다운로드, 발송일자 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 검색 결과가 없습니다 | 발송일시, 제목, 발송대상 업체수, 발송결과, 다운로드, 발송일자 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/IntegrationRoutes.tsx#L131) · [EmailSendingHistoryPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/service-notice-email/pages/EmailSendingHistoryPage.tsx#L51) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/service-notice-email/api/emailSendingHistoryApi.ts#L36) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/service-notice-email/api/emailSendingHistoryApi.ts#L29) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/service-notice-email/api/emailSendingHistoryApi.ts#L43) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 3개 중 개발 메타데이터 확인 3개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-9e7cf228fa5d461e) | Demo 메타데이터 3/3개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

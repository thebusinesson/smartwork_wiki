# [회사·회원·서비스 권한] 회원 이메일 다운로드 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

검색 조건에 맞는 회원 이메일 건수를 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 회사·회원·서비스 권한 |
| 언제 사용하는가 | 이메일 다운로드 건수 조회, 이메일 다운로드 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 다운로드 목적, 일반, 마케팅 이메일 동의, 동의 회원만, 수신불가 계정 제외, 날짜 조건 |
| 업무 흐름 | 이메일 다운로드 건수 조회, 이메일 다운로드 |
| 이 페이지의 역할 | 조회 · 이메일 다운로드 건수 조회 |
| 판단 결과·다음 업무 | [회원 이메일 다운로드 내역 조회](email-download__history.md) |
| 다른 화면과의 구분 | 이 경로에서 볼 수 있는 조건·결과를 기준으로 사용한다. 독립 경로의 상세·등록은 관련 화면에 연결한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 검색 조건에 맞는 회원 이메일 건수를 조회한다. |
| 메뉴·화면 경로 | SB 고객관리 > 스마트빌 회원·회사정보 관리 > 회원 이메일 다운로드 · `/member-management/email-download` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [회원 이메일 다운로드 내역 조회](email-download__history.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/member-management/email-download` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 이메일 다운로드 건수 조회 | `/member-management/email-download` `VIEW` | `MemberEmailDownloadSearchRequest` `dateStart`, `dateEnd`, `companyCondition`, `companyValue`, `personalCondition`, `personalValue`, `memberType`, `memberCategory`, `memberStatus`, `webIntegrationType`, `integrationServices`, `downloadPurpose`, `marketingEmailConsentOnly`, `excludeUndeliverableEmails` |
| 이메일 다운로드 | `/member-management/email-download` `EXCEL_DOWNLOAD` | `MemberEmailDownloadRequest` `dateStart`, `dateEnd`, `companyCondition`, `companyValue`, `personalCondition`, `personalValue`, `memberType`, `memberCategory`, `memberStatus`, `webIntegrationType`, `integrationServices`, `downloadPurpose`, `marketingEmailConsentOnly`, `excludeUndeliverableEmails` |

코드에서 확인한 버튼·작업명은 **이메일 다운로드 내역**, **검색**, **다운로드**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **SB 고객관리 > 스마트빌 회원·회사정보 관리 > 회원 이메일 다운로드**를 연다. `/member-management/email-download`를 연다.
2. **다운로드 목적**, **일반**, **마케팅 이메일 동의**, **동의 회원만**, **수신불가 계정 제외**, **날짜 조건**, **업체 조건** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **이메일 다운로드 내역**, **검색**, **다운로드** 중 해당 버튼을 선택한다.
3. **이메일 다운로드 건수 조회** 처리 결과를 확인하고 받은 파일의 대상과 적용 조건을 대조한다.
4. 후속 조회나 목록 복귀가 필요하면 [회원 이메일 다운로드 내역 조회](email-download__history.md)에서 후속 절차를 확인한다.

업체 조건의 초기값은 **전체**다. **회사명** 또는 **사업자번호**를 고르면 검색어를 입력한다. 다운로드에는 마지막으로 적용한 검색 조건이 사용된다. 다운로드 목적이 **마케팅 이메일(EDM)**이면 파일에 이메일만 포함된다. 건수 조회 서버 제한은 60초, 다운로드 파일 생성 서버 제한은 5분이다. 시간이 초과되면 기간·업체 등 조건을 좁혀 다시 시도한다. [초기 검색 조건](https://github.com/thebusinesson/smartwork/blob/b923849c5d878772e0de2b67becff0ae511f03b3/frontend/src/feature/customer/member/constants/memberEmailDownload.ts) · [서버 제한](https://github.com/thebusinesson/smartwork/blob/b923849c5d878772e0de2b67becff0ae511f03b3/backend/src/main/kotlin/com/bizon/smartwork/infra/config/MemberEmailRequestDeadline.kt)

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 다운로드 목적 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/emailDownload/MemberEmailDownloadPage.tsx#L145) |
| 일반 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `GENERAL` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/emailDownload/MemberEmailDownloadPage.tsx#L149) |
| 마케팅 이메일 동의 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/emailDownload/MemberEmailDownloadPage.tsx#L154) |
| 동의 회원만 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/emailDownload/MemberEmailDownloadPage.tsx#L163) |
| 수신불가 계정 제외 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/emailDownload/MemberEmailDownloadPage.tsx#L166) |
| 날짜 조건 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/emailDownload/MemberEmailDownloadPage.tsx#L178) |
| 업체 조건 | 입력 또는 선택 | 초기값 전체. 회사명·사업자번호를 선택하면 검색어 필요 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/emailDownload/MemberEmailDownloadPage.tsx#L193) |
| 개인 조건 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/emailDownload/MemberEmailDownloadPage.tsx#L215) |
| 회원 구분 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/emailDownload/MemberEmailDownloadPage.tsx#L239) |
| 회원 종류 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/emailDownload/MemberEmailDownloadPage.tsx#L253) |
| 회원 상태 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/emailDownload/MemberEmailDownloadPage.tsx#L267) |
| 웹/연동 구분 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/emailDownload/MemberEmailDownloadPage.tsx#L282) |
| 연동 서비스 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/emailDownload/MemberEmailDownloadPage.tsx#L296) |
| 검색결과 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/emailDownload/components/MemberEmailDownloadArea.tsx#L88) |
| 다운로드 목적 | 입력·선택 | EDM 선택 시 이메일만 반출 | downloadPurpose. EDM 요청은 서버에서 downloadItems를 email로 제한 |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 이메일 다운로드 건수 조회 | `GET /api/v1/members/email-download` · `/member-management/email-download` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/customer/member/MemberEmailDownloadController.kt#L83) | `MemberEmailDownloadSearchRequest` `dateStart`, `dateEnd`, `companyCondition`, `companyValue`, `personalCondition`, `personalValue`, `memberType`, `memberCategory`, `memberStatus`, `webIntegrationType`, `integrationServices`, `downloadPurpose`, `marketingEmailConsentOnly`, `excludeUndeliverableEmails` → `success`, `data`, `error`, `totalCount` | `sb_mig.sys.tables`, `sb_mig.sys.schemas` |
| 이메일 다운로드 | `POST /api/v1/members/email-download` · `/member-management/email-download` `EXCEL_DOWNLOAD` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/customer/member/MemberEmailDownloadController.kt#L96) | `MemberEmailDownloadRequest` `dateStart`, `dateEnd`, `companyCondition`, `companyValue`, `personalCondition`, `personalValue`, `memberType`, `memberCategory`, `memberStatus`, `webIntegrationType`, `integrationServices`, `downloadPurpose`, `marketingEmailConsentOnly`, `excludeUndeliverableEmails` → 파일 또는 오류 응답 | `sb_mig.sys.tables`, `sb_mig.sys.schemas`, `smartwork.dbo.action_reason` · 정의에서 확인한 쓰기 `smartwork.dbo.action_reason` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `sb_mig.sys.tables` | 메타데이터 확인 필요 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/member/repository/MemberInfoMapper.kt#L88) · 개발 정의 미확인 |
| `sb_mig.sys.schemas` | 메타데이터 확인 필요 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/member/repository/MemberInfoMapper.kt#L88) · 개발 정의 미확인 |
| `smartwork.dbo.action_reason` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL INSERT INTO | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/shared/actionreason/repository/ActionReasonMapper.kt#L16) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b0430106ffe0743f) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 다운로드 목적, 일반, 마케팅 이메일 동의, 동의 회원만, 수신불가 계정 제외, 날짜 조건 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 고객관리 > 스마트빌 회원·회사정보 관리 > 회원 이메일 다운로드의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/CustomerRoutes.tsx#L47) · [MemberEmailDownloadPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/emailDownload/MemberEmailDownloadPage.tsx#L84) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/api/memberEmailDownloadApi.ts#L117) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/api/memberEmailDownloadApi.ts#L127) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 3개 중 개발 메타데이터 확인 1개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-c788bdea9b6ccd14) | 2026-11-11 기준으로 Demo 메타데이터 3/3개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |
| 최신 변경 대조 | [11월 12일 전수 대조](../../references/all-pages-audit-2026-11-12.md) | 현재 코드 b923849c5 · 2026-11-12 |

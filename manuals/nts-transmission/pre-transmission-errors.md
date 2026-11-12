# [전송 전·후 오류와 국세청 결과] 전송 전 오류 조회 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

등록일자·승인번호 조건으로 국세청 전송 전 오류 목록을 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 전송 전·후 오류와 국세청 결과 |
| 언제 사용하는가 | 전송 전 오류 목록 조회 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 등록일시, 승인번호, 오류내용, 등록일자 |
| 업무 흐름 | 전송 전 오류 목록 조회 |
| 이 페이지의 역할 | 조회 · 전송 전 오류 목록 조회 |
| 판단 결과·다음 업무 | [전송 전 오류 조회 상세](pre-transmission-errors__by-issueId.md) |
| 다른 화면과의 구분 | 이 경로에서 볼 수 있는 조건·결과를 기준으로 사용한다. 독립 경로의 상세·등록은 관련 화면에 연결한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 등록일자·승인번호 조건으로 국세청 전송 전 오류 목록을 조회한다. |
| 메뉴·화면 경로 | SB 서비스관리 > 국세청 전송 관리 > 전송 전 오류 조회 · `/nts-transmission/pre-transmission-errors` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [전송 전 오류 조회 상세](pre-transmission-errors__by-issueId.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/nts-transmission/pre-transmission-errors` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 전송 전 오류 목록 조회 | `/nts-transmission/pre-transmission-errors` `VIEW` | `PreTransmissionErrorSearchRequest` `fromDate`, `toDate`, `issueId`, `page`, `size` · 서버 필수 `fromDate`, `toDate` |

코드에서 확인한 버튼·작업명은 **검색**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **SB 서비스관리 > 국세청 전송 관리 > 전송 전 오류 조회**를 연다. `/nts-transmission/pre-transmission-errors`를 연다.
2. **등록일자** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색** 중 해당 버튼을 선택한다.
3. **전송 전 오류 목록 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [전송 전 오류 조회 상세](pre-transmission-errors__by-issueId.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 등록일시 | 출력 | 조회 응답 기준 | 화면 필드 `createTs` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/ntstransmission/PreTransmissionErrorsPage.tsx#L121) |
| 승인번호 | 입력 또는 선택 | 길이·개수 최대 35 | API 요청 `issueId` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/ntstransmission/PreTransmissionErrorsPage.tsx#L126) |
| 오류내용 | 출력 | 조회 응답 기준 | 화면 필드 `errorReason` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/ntstransmission/PreTransmissionErrorsPage.tsx#L127) |
| 등록일자 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/ntstransmission/PreTransmissionErrorsPage.tsx#L19) |
| 승인번호를 입력해주세요 | 입력 또는 선택 | 길이·개수 최대 35 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/ntstransmission/PreTransmissionErrorsPage.tsx#L30) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 전송 전 오류 목록 조회 | `GET /api/v1/nts-transmission/pre-transmission-errors` · `/nts-transmission/pre-transmission-errors` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/ntstransmission/pretransmissionerror/PreTransmissionErrorController.kt#L52) | `PreTransmissionErrorSearchRequest` `fromDate`, `toDate`, `issueId`, `page`, `size` · 서버 필수 `fromDate`, `toDate` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `currentPage`, `size` | `smartwork.dbo.usp_pre_transmission_error_select` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.usp_pre_transmission_error_select` | @PAGE int, @PAGESIZE int, @START_DATE varchar(10), @END_DATE varchar(10), @ISSUE_ID varchar(35) | 정의 참조 `torpedo.dbo.ET_TIDOC_IF` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/ntstransmission/pretransmissionerror/repository/PreTransmissionErrorMapper.kt#L27) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-d738a2b67b13f99b) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 등록일시, 승인번호, 오류내용, 등록일자 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 서비스관리 > 국세청 전송 관리 > 전송 전 오류 조회의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 검색 결과가 없습니다. | 등록일시, 승인번호, 오류내용, 등록일자 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/NtsTransmissionRoutes.tsx#L20) · [PreTransmissionErrorsPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/ntstransmission/PreTransmissionErrorsPage.tsx#L75) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/ntstransmission/api/ntsErrorManagementApi.ts#L37) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 1개 중 개발 메타데이터 확인 1개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-43382c8a6b73f8ba) | Demo 메타데이터 1/1개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

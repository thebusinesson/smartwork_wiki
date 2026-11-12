# [운영 공지·인증 정책과 감사 로그] 공지 관리 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

관리할 공지 전체를 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 운영 공지·인증 정책과 감사 로그 |
| 언제 사용하는가 | 공지 목록 조회, 공지 수정, 공지 등록, 공지 삭제 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 제목, 노출 위치, 1단계 메뉴, 2단계 메뉴, 상단 안내문구, 상세 내용 |
| 업무 흐름 | 공지 목록 조회, 공지 수정, 공지 등록, 공지 삭제 |
| 이 페이지의 역할 | 조회·관리 · 공지 목록 조회 |
| 판단 결과·다음 업무 | 현재 화면에서 결과를 확인한다. |
| 다른 화면과의 구분 | 같은 경로에서 열리는 조회·팝업은 이 문서에서 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 삭제 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/notice/NoticeManagementPage.tsx#L191) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 관리할 공지 전체를 조회한다. |
| 메뉴·화면 경로 | SmartWork 관리 > 공지 관리 · `/settings/notice-management` |
| 화면 유형·담당 | 조회·관리 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | 현재 화면에서 결과를 확인한다. |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/settings/notice-management` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 공지 목록 조회 | `/settings/notice-management` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 공지 수정 | `/settings/notice-management` `PROCESS` | `id: String` · `request: Notice` |
| 공지 등록 | `/settings/notice-management` `PROCESS` | `request: Notice` |
| 공지 삭제 | `/settings/notice-management` `DELETE` | `id: String` |

코드에서 확인한 버튼·작업명은 **공지 등록**, **취소**, **저장**, **수정**, **삭제**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **SmartWork 관리 > 공지 관리**를 연다. `/settings/notice-management`를 연다.
2. **제목**, **노출 위치**, **1단계 메뉴**, **2단계 메뉴**, **상단 안내문구**, **상세 내용**, **노출 일정** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **공지 등록**, **저장** 중 해당 버튼을 선택한다.
3. **공지 목록 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 제목 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/notice/NoticeManagementPage.tsx#L155) |
| 노출 위치 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/notice/NoticeManagementPage.tsx#L156) |
| 1단계 메뉴 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/notice/NoticeManagementPage.tsx#L159) |
| 2단계 메뉴 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/notice/NoticeManagementPage.tsx#L160) |
| 상단 안내문구 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/notice/NoticeManagementPage.tsx#L162) |
| 상세 내용 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/notice/NoticeManagementPage.tsx#L163) |
| 노출 일정 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/notice/NoticeManagementPage.tsx#L165) |
| 사용 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/notice/NoticeManagementPage.tsx#L166) |
| 시작 (한국 시간) | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/notice/NoticeManagementPage.tsx#L169) |
| 종료 (한국 시간, 미포함) | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/notice/NoticeManagementPage.tsx#L170) |
| 시작일 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/notice/NoticeManagementPage.tsx#L174) |
| 종료일 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/notice/NoticeManagementPage.tsx#L175) |
| 시작 시각 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/notice/NoticeManagementPage.tsx#L176) |
| 종료 시각 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/notice/NoticeManagementPage.tsx#L177) |
| 일정 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/notice/NoticeManagementPage.tsx#L185) |
| 상태 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/notice/NoticeManagementPage.tsx#L185) |
| 관리 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/notice/NoticeManagementPage.tsx#L185) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 공지 목록 조회 | `GET /api/v1/settings/notices` · `/settings/notice-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/settings/notice/NoticeController.kt#L36) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error` | 서버 설정의 공지 JSON 파일 읽기 또는 쓰기 · [NoticeFileService](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/notice/NoticeFileService.kt#L44) |
| 공지 수정 | `PUT /api/v1/settings/notices/{id}` · `/settings/notice-management` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/settings/notice/NoticeController.kt#L48) | `id: String` · `request: Notice` → `success`, `data`, `error` | 서버 설정의 공지 JSON 파일 읽기 또는 쓰기 · [NoticeFileService](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/notice/NoticeFileService.kt#L44) |
| 공지 등록 | `POST /api/v1/settings/notices` · `/settings/notice-management` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/settings/notice/NoticeController.kt#L42) | `request: Notice` → `success`, `data`, `error` | 서버 설정의 공지 JSON 파일 읽기 또는 쓰기 · [NoticeFileService](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/notice/NoticeFileService.kt#L44) |
| 공지 삭제 | `DELETE /api/v1/settings/notices/{id}` · `/settings/notice-management` `DELETE` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/settings/notice/NoticeController.kt#L55) | `id: String` → `success`, `data`, `error` | 서버 설정의 공지 JSON 파일 읽기 또는 쓰기 · [NoticeFileService](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/notice/NoticeFileService.kt#L44) |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| 공지 JSON 파일 | 설정 키 <code>smartwork.notice.file</code>. 기본 <code>./data/notices.json</code> | 조회는 파일을 읽는다. 등록·수정·삭제는 파일 잠금을 잡고 저장한다. | [NoticeFileService](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/notice/NoticeFileService.kt#L44) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 제목, 노출 위치, 1단계 메뉴, 2단계 메뉴, 상단 안내문구, 상세 내용 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SmartWork 관리 > 공지 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 공지 목록을 불러오지 못했습니다. | 제목, 노출 위치, 1단계 메뉴, 2단계 메뉴, 상단 안내문구, 상세 내용 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 노출할 화면이 없는 메뉴입니다. | 제목, 노출 위치, 1단계 메뉴, 2단계 메뉴, 상단 안내문구, 상세 내용 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 공지를 저장하지 못했습니다. | 제목, 노출 위치, 1단계 메뉴, 2단계 메뉴, 상단 안내문구, 상세 내용 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 공지를 삭제하지 못했습니다. | 제목, 노출 위치, 1단계 메뉴, 2단계 메뉴, 상단 안내문구, 상세 내용 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/SettingsRoutes.tsx#L35) · [NoticeManagementPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/notice/NoticeManagementPage.tsx#L58) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/notice/api/noticeApi.ts#L28) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/notice/api/noticeApi.ts#L31) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/notice/api/noticeApi.ts#L30) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/settings/notice/api/noticeApi.ts#L32) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 코드 확인 · 공지 JSON 파일 사용. 직접 DB 호출 해당 없음 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-03206d70e4b3d386) | 해당 없음 · 공지 등록·수정·삭제는 설정 키 smartwork.notice.file의 JSON 파일을 사용한다. 직접 DB 호출 없음 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

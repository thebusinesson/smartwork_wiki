# [전송 대상과 일정·설정] 국세청 전송 설정 관리 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

업체별 국세청 전송 설정을 조회하고 필요한 업체의 설정을 변경한다. 설정 저장 결과는 해당 문서의 전송 결과와 별도로 확인한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 전송 대상과 일정·설정 |
| 언제 사용하는가 | 전송 설정 목록 조회, 사업자번호 기준 설정 단건 조회, 전송 설정 저장 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 사업자번호, 전송 설정 |
| 업무 흐름 | 전송 설정 목록 조회, 사업자번호 기준 설정 단건 조회, 전송 설정 저장 |
| 이 페이지의 역할 | 조회 · 전송 설정 목록 조회 |
| 판단 결과·다음 업무 | 현재 화면에서 결과를 확인한다. |
| 다른 화면과의 구분 | 같은 경로에서 열리는 조회·팝업은 이 문서에서 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 저장 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/ntstransmission/TransmissionSettingDialog.tsx#L140) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 업체별 국세청 전송 설정을 조회하고 필요한 업체의 설정을 변경한다. 설정 저장 결과는 해당 문서의 전송 결과와 별도로 확인한다. |
| 메뉴·화면 경로 | SB 서비스관리 > 국세청 전송 관리 > 국세청 전송 설정 관리 · `/nts-transmission/transmission-settings` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | 현재 화면에서 결과를 확인한다. |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/nts-transmission/transmission-settings` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 전송 설정 목록 조회 | `/nts-transmission/transmission-settings` `VIEW` | `TransmissionSettingSearchRequest` `transmissionStatus`, `companyCondition`, `searchKeyword`, `page`, `size` |
| 사업자번호 기준 설정 단건 조회 | `/nts-transmission/transmission-settings` `VIEW` | `businessNumber: String` |
| 전송 설정 저장 | `/nts-transmission/transmission-settings` `PROCESS` | `TransmissionSettingSaveRequest` `id`, `businessNumber`, `status` |
| 최종 수정자 원문 조회 | `/nts-transmission/transmission-settings` / `UNMASK` | `id`, `field` |

코드에서 확인한 버튼·작업명은 **검색**, **국세청 전송 설정**, **저장**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **SB 서비스관리 > 국세청 전송 관리 > 국세청 전송 설정 관리**를 연다. `/nts-transmission/transmission-settings`를 연다.
2. **전체**, **즉시전송**, **익일전송**, **전송 제외**, **사업자번호**, **회사명**, **전송 설정 상태** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색**, **국세청 전송 설정**, **저장** 중 해당 버튼을 선택한다.
3. **전송 설정 목록 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 전체 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `all` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/ntstransmission/NtsTransmissionSettingsPage.tsx#L40) |
| 즉시전송 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `즉시전송` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/ntstransmission/NtsTransmissionSettingsPage.tsx#L34) |
| 익일전송 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `익일전송` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/ntstransmission/NtsTransmissionSettingsPage.tsx#L35) |
| 전송 제외 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `전송 제외` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/ntstransmission/NtsTransmissionSettingsPage.tsx#L36) |
| 사업자번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `사업자번호` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/ntstransmission/NtsTransmissionSettingsPage.tsx#L41) |
| 회사명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `회사명` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/ntstransmission/NtsTransmissionSettingsPage.tsx#L42) |
| 전송 설정 상태 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/ntstransmission/NtsTransmissionSettingsPage.tsx#L48) |
| 업체 조건 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/ntstransmission/NtsTransmissionSettingsPage.tsx#L54) |
| 설정상태 | 입력 또는 선택 | API 기본값 null | API 요청 `transmissionStatus` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/ntstransmission/NtsTransmissionSettingsPage.tsx#L210) |
| 생성일 | 출력 | 조회 응답 기준 | 화면 필드 `createdDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/ntstransmission/NtsTransmissionSettingsPage.tsx#L211) |
| 최종수정일 | 출력 | 조회 응답 기준 | 화면 필드 `lastModifiedDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/ntstransmission/NtsTransmissionSettingsPage.tsx#L213) |
| 최종수정자 | 출력 | 조회 응답 기준 | 화면 필드 `lastModifiedBy` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/ntstransmission/NtsTransmissionSettingsPage.tsx#L217) |
| 최종 수정자 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `LAST_MODIFIED_BY` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/ntstransmission/NtsTransmissionSettingsPage.tsx#L222) |
| 사업자 번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/ntstransmission/TransmissionSettingDialog.tsx#L151) |
| 숫자 10자리를 입력하세요 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/ntstransmission/TransmissionSettingDialog.tsx#L154) |
| 검색 버튼을 눌러 회사명을 조회하세요 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/ntstransmission/TransmissionSettingDialog.tsx#L189) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 전송 설정 목록 조회 | `GET /api/v1/nts-transmission/settings` · `/nts-transmission/transmission-settings` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/ntstransmission/transmissionsetting/TransmissionSettingController.kt#L55) | `TransmissionSettingSearchRequest` `transmissionStatus`, `companyCondition`, `searchKeyword`, `page`, `size` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `currentPage`, `size` | `smartwork.dbo.usp_transmission_setting_list_select` · 코드 연계 트랜잭션 |
| 사업자번호 기준 설정 단건 조회 | `GET /api/v1/nts-transmission/settings/lookup` · `/nts-transmission/transmission-settings` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/ntstransmission/transmissionsetting/TransmissionSettingController.kt#L94) | `businessNumber: String` → `success`, `data`, `error`, `id`, `businessNumber`, `companyName`, `transmissionStatus`, `registered` | `SmartBill3.dbo.COMPANY`, `SB_DTI.dbo.NTS_TRANSMIT_METHOD` |
| 전송 설정 저장 | `POST /api/v1/nts-transmission/settings` · `/nts-transmission/transmission-settings` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/ntstransmission/transmissionsetting/TransmissionSettingController.kt#L121) | `TransmissionSettingSaveRequest` `id`, `businessNumber`, `status` → `success`, `data`, `error`, `resultCode`, `message` | `office.dbo.upGW_NtsSend_Status_Save` · 정의에서 확인한 쓰기 `SB_DTI.dbo.NTS_TRANSMIT_METHOD`, `SB_DTI.dbo.NTS_TRANSMIT_METHOD_HIS` · 코드 연계 트랜잭션 |
| 최종 수정자 원문 조회 | `POST /api/v1/nts-transmission/settings/{id}/sensitive-values/reveal` · `/nts-transmission/transmission-settings` / `UNMASK` · [화면 컴포넌트](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/ntstransmission/NtsTransmissionSettingsPage.tsx#L220) · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/ntstransmission/transmissionsetting/TransmissionSettingController.kt#L69) | `id`, `field` → 요청한 항목의 원문 응답 | 권한 검사 후 대상 값을 조회하고 감사 기록을 남긴다. |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.usp_transmission_setting_list_select` | @PAGE int, @PAGESIZE int, @STATUS varchar(10), @SEARCH_TYPE varchar(1), @SEARCH_TEXT varchar(100) | 정의 참조 `SmartBill3.dbo.COMPANY`, `SmartBill3.dbo.MEMBER`, `SB_DTI.dbo.NTS_TRANSMIT_METHOD`, `office.dbo.SAWON` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/ntstransmission/transmissionsetting/repository/TransmissionSettingMapper.kt#L34) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-4a5752f10d724aba) |
| `SmartBill3.dbo.COMPANY` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/ntstransmission/transmissionsetting/repository/TransmissionSettingMapper.kt#L96) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-0e6fcaa6b5086c07) |
| `SB_DTI.dbo.NTS_TRANSMIT_METHOD` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/ntstransmission/transmissionsetting/repository/TransmissionSettingMapper.kt#L96) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-bfe883894125b999) |
| `office.dbo.upGW_NtsSend_Status_Save` | @COM_REGNO varchar(13), @SEND_TYPE varchar(1), @SW_NO int, @MODE varchar(1) | 정의 참조 `SmartBill3.dbo.COMPANY`, `SB_DTI.dbo.COMPANY_LINK_IN`, `SB_DTI.dbo.COMPANY_LINK_OUT`, `SB_DTI.dbo.NTS_TRANSMIT_METHOD`, `SB_DTI.dbo.NTS_TRANSMIT_METHOD_HIS` · 정적 쓰기 `SB_DTI.dbo.NTS_TRANSMIT_METHOD`, `SB_DTI.dbo.NTS_TRANSMIT_METHOD_HIS` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/ntstransmission/transmissionsetting/repository/TransmissionSettingMapper.kt#L100) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-f5bee19dbdf58d5e) |
| `SmartBill3.dbo.MEMBER` | 개발 컬럼 메타데이터 확인 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/ntstransmission/transmissionsetting/repository/TransmissionSettingMapper.kt#L65) |
| `office.dbo.SAWON` | 개발 컬럼 메타데이터 확인 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/ntstransmission/transmissionsetting/repository/TransmissionSettingMapper.kt#L65) |
| `smartwork.dbo.usp_sw_log_access_event_insert` | @EVENT_TYPE varchar(30) IN, @STATUS varchar(20) IN, @USER_ID bigint IN, @MEMBER_ID nvarchar(50) IN, @USER_NAME nvarchar(100) IN, @DEPARTMENT_NAME nvarchar(100) IN, @PAGE_TITLE nvarchar(200) IN, @PATH nvarchar(500) IN, @MENU_PATH nvarchar(500) IN, @MENU_LABEL nvarchar(200) IN, @CATEGORY_NAME nvarchar(200) IN, @SUB_CATEGORY_NAME nvarchar(200) IN, @MENU_ORDER int IN, @IP_ADDRESS varchar(45) IN, @USER_AGENT nvarchar(1000) IN, @BROWSER varchar(100) IN, @OS varchar(100) IN, @REFERRER nvarchar(500) IN, @DETAIL nvarchar(1000) IN, @RESULT int OUT, @COUNTS_AS_VISIT bit IN | 원문 조회 또는 감사 흐름에서 호출 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/logmanagement/repository/LogManagementMapper.kt#L92) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 사업자번호, 전송 설정 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 서비스관리 > 국세청 전송 관리 > 국세청 전송 설정 관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 저장 중 오류가 발생했습니다. | 사업자번호, 전송 설정 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 검색 결과가 없습니다. | 사업자번호, 전송 설정 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 해당 사업자번호의 회사를 찾을 수 없습니다. | 사업자번호, 전송 설정 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/NtsTransmissionRoutes.tsx#L17) · [NtsTransmissionSettingsPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/ntstransmission/NtsTransmissionSettingsPage.tsx#L28) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/ntstransmission/api/ntsTransmissionSettingsApi.ts#L79) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/ntstransmission/api/ntsTransmissionSettingsApi.ts#L109) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/ntstransmission/api/ntsTransmissionSettingsApi.ts#L94) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 4개 중 개발 메타데이터 확인 4개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-1536fe186cdc435e) | Demo 메타데이터 7/7개 확인 · Dev와 계약 차이 1개 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

# [시스템 키·벌크계좌·업체 연결 설정] 연동플랫폼 통합관리 상세 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

DB ATTACHFILEFULLPATH (storedName) 으로 파일을 다운로드.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 시스템 키·벌크계좌·업체 연결 설정 |
| 언제 사용하는가 | 상세정보 첨부파일 다운로드, 시스템 포트 상세 통합 저장 (multipart/form-data), 이전 이력 가져오기 (이전 IP/PORT → 현재 IP/PORT 복사) 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 기타, 원격터미널, 방문, 특이사항, 요청사항, 배포 |
| 업무 흐름 | 포트 선택 → 연결 설정 확인 → 통합 저장 또는 상세정보 행별 처리 |
| 이 페이지의 역할 | 상세 · 상세정보 첨부파일 다운로드 |
| 판단 결과·다음 업무 | [연동플랫폼 통합관리](platform-management.md) |
| 다른 화면과의 구분 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > 연동플랫폼 통합관리에서 사용하는 상세 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 저장 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/platformManagement/components/ImportHistoryDialog.tsx#L94) |
| 확인 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/SystemPortDetailPage.tsx#L226) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | DB ATTACHFILEFULLPATH (storedName) 으로 파일을 다운로드. |
| 메뉴·화면 경로 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > 연동플랫폼 통합관리 · `/hub-vendor/platform-management/system-port/:portId` · 경로 변수 `portId` |
| 화면 유형·담당 | 상세 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [연동플랫폼 통합관리](platform-management.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/hub-vendor/platform-management` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `portId` |
| 상세정보 첨부파일 다운로드 | `/hub-vendor/platform-management` `VIEW` | `storedName: String` · `originalFileName: String?` |
| 이전 이력 가져오기 (이전 IP/PORT → 현재 IP/PORT 복사) | `/hub-vendor/platform-management` `PROCESS` | `id: Int` · `routingUrl: String` · `port: String` · `productCode: String` · `PlatformMgmtImportHistoryRequest` `oldIp`, `oldPort`, `importAccessMethod`, `importEngineers`, `importErp`, `importDetailInfo` |
| 시스템 포트 상세 조회 | 연동플랫폼 통합관리 메뉴 `VIEW` | 시스템 ID와 대상 라우팅 주소·포트 |
| 접근방법·담당자·ERP·SAP 통합 저장 | 연동플랫폼 통합관리 메뉴 `PROCESS` | 시스템 ID, 라우팅 주소·포트, JSON 본문 |
| 상세정보 행 등록 | 연동플랫폼 통합관리 메뉴 `PROCESS` | 시스템 ID, 라우팅 주소·포트, JSON payload, 선택 파일 |
| 상세정보 행 수정 | 연동플랫폼 통합관리 메뉴 `PROCESS` | 시스템 ID, 상세정보 번호, 라우팅 주소·포트, JSON payload, 선택 파일 |
| 상세정보 행 삭제 | 연동플랫폼 통합관리 메뉴 `DELETE` | 시스템 ID, 상세정보 번호, 라우팅 주소·포트 |
| 상세정보 첨부만 삭제 | 연동플랫폼 통합관리 메뉴 `DELETE` | 시스템 ID, 상세정보 번호, 라우팅 주소·포트 |

코드에서 확인한 버튼·작업명은 **이전**, **이전 이력 가져오기**, **저장**, **삭제**, **담당자 추가**, **추가**, **비밀번호 보기**, **상세정보 추가**, **첨부파일**, **더보기**, **목록**, **확인**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. 연동플랫폼 상세에서 시스템 포트를 선택한다. 현재 포트와 조회된 접근방법·담당자·ERP·상세정보를 확인한다.
2. 접근방법·담당자·ERP(SAP 연결정보 포함)를 변경하면 화면 하단 **저장**을 사용한다.
3. **상세정보**에서는 새 행을 추가하거나 기존 행의 **수정**을 누른다. 상세내용 또는 첨부를 확인한 뒤 행 안의 **저장**을 눌러 해당 행만 반영한다.
4. 기존 행의 **삭제**와 **첨부파일 삭제**를 구분한다. 확인창에 표시된 대상을 확인하고 결과를 상세정보 목록에서 확인한다.
5. 이전 이력이 필요하면 **이전 이력 가져오기**의 대상 포트와 복사할 항목을 확인한다.

[행별 버튼](https://github.com/thebusinesson/smartwork/blob/b923849c5d878772e0de2b67becff0ae511f03b3/frontend/src/feature/integration/hubvendor/platformManagement/components/SystemPortDetailInfoSection.tsx)

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `portId` |
| -----선택----- | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/constants/integrationPlatform.ts#L59) |
| 기타 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `Etc` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/constants/integrationPlatform.ts#L51) |
| 원격터미널 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `Remote` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/constants/integrationPlatform.ts#L47) |
| 방문 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `Visit` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/constants/integrationPlatform.ts#L50) |
| -----전체----- | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/constants/integrationPlatform.ts#L86) |
| 특이사항 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `A` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/constants/integrationPlatform.ts#L87) |
| 요청사항 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `B` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/constants/integrationPlatform.ts#L88) |
| 배포 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `C` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/constants/integrationPlatform.ts#L89) |
| 중계서버 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/platformManagement/components/SystemPortHeaderInfoSection.tsx#L41) |
| 포트 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/platformManagement/components/SystemPortHeaderInfoSection.tsx#L45) |
| OLD 중계서버 IP | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/platformManagement/components/ImportHistoryDialog.tsx#L126) |
| OLD 중계서버 PORT | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/platformManagement/components/ImportHistoryDialog.tsx#L138) |
| IP 기준 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/platformManagement/components/ImportHistoryDialog.tsx#L152) |
| PORT 기준 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/platformManagement/components/ImportHistoryDialog.tsx#L164) |
| OS종류 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/platformManagement/components/SystemAccessMethodSection.tsx#L28) |
| OS 비고 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/platformManagement/components/SystemAccessMethodSection.tsx#L47) |
| 접근방법 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/platformManagement/components/SystemAccessMethodSection.tsx#L54) |
| 접근방법 비고 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/platformManagement/components/SystemAccessMethodSection.tsx#L75) |
| 담당자명 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/platformManagement/components/SystemPortContactSection.tsx#L34) |
| 이메일 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/platformManagement/components/SystemPortContactSection.tsx#L37) |
| 연락처1 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/platformManagement/components/SystemPortContactSection.tsx#L40) |
| 연락처2 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/platformManagement/components/SystemPortContactSection.tsx#L43) |
| 비고 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/platformManagement/components/SystemPortContactSection.tsx#L46) |
| ERP 종류 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/platformManagement/components/ErpTemplateSection.tsx#L60) |
| ERP 비고 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/platformManagement/components/ErpTemplateSection.tsx#L79) |
| DB종류 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/platformManagement/components/ErpTemplateSection.tsx#L86) |
| DB 비고 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/platformManagement/components/ErpTemplateSection.tsx#L105) |
| 기타 메시지 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/platformManagement/components/ErpTemplateSection.tsx#L118) |
| SAP 종류 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/platformManagement/components/ErpTemplateSection.tsx#L131) |
| IP(도메인) | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/platformManagement/components/ErpTemplateSection.tsx#L132) |
| 구분 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/platformManagement/components/SystemPortDetailInfoSection.tsx#L130) |
| 첨부파일 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/platformManagement/components/SystemPortDetailInfoSection.tsx#L147) |
| 상세내용 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/platformManagement/components/SystemPortDetailInfoSection.tsx#L241) |
| 상세 내용을 입력하세요 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/platformManagement/components/SystemPortDetailInfoSection.tsx#L248) |
| 상세정보 첨부 | 입력·선택 | 4MB 이하. 새 파일을 선택한 행의 저장에 사용 | 행별 multipart의 file |
| 상세내용 | 입력 | 새 행은 상세내용 또는 첨부가 있어야 저장 | payload.description |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 상세정보 첨부파일 다운로드 | `GET /api/v1/hub-vendor/platform-management/attachments/{storedName}` · `/hub-vendor/platform-management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/platformmgmt/PlatformMgmtController.kt#L234) | `storedName: String` · `originalFileName: String?` → 파일 또는 오류 응답 | 직접 DB 호출이 연결된 경로는 현재 소스에서 미확인. 세부 저장소는 Controller와 Service 참조. |
| 이전 이력 가져오기 (이전 IP/PORT → 현재 IP/PORT 복사) | `POST /api/v1/hub-vendor/platform-management/{id}/system-port-detail/import` · `/hub-vendor/platform-management` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/platformmgmt/PlatformMgmtController.kt#L201) | `id: Int` · `routingUrl: String` · `port: String` · `productCode: String` · `PlatformMgmtImportHistoryRequest` `oldIp`, `oldPort`, `importAccessMethod`, `importEngineers`, `importErp`, `importDetailInfo` → `success`, `data`, `error`, `result` | `smartwork.dbo.usp_platform_mgmt_import_history_exec` · 정의에서 확인한 쓰기 `office.dbo.HUB_ROUTINGURL_DETAIL`, `office.dbo.Hub_Engineer`, `office.dbo.HUB_ERP_DETAIL`, `office.dbo.HUB_DETAIL_INFO` · 코드 연계 트랜잭션 |
| 시스템 포트 상세 조회 | `GET /api/v1/hub-vendor/platform-management/{id}/system-port-detail` · `/hub-vendor/platform-management` `VIEW` · [현재 Controller](https://github.com/thebusinesson/smartwork/blob/b923849c5d878772e0de2b67becff0ae511f03b3/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/platformmgmt/PlatformMgmtController.kt#L120) | 시스템 ID와 대상 라우팅 주소·포트 → 조회 결과 | 접근방법·담당자·ERP·SAP·상세정보 조회 |
| 접근방법·담당자·ERP·SAP 통합 저장 | `PATCH /api/v1/hub-vendor/platform-management/{id}/system-port-detail` · `/hub-vendor/platform-management` `PROCESS` · [현재 Controller](https://github.com/thebusinesson/smartwork/blob/b923849c5d878772e0de2b67becff0ae511f03b3/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/platformmgmt/PlatformMgmtController.kt#L137) | 시스템 ID, 라우팅 주소·포트, JSON 본문 → 처리 결과 | 상세정보 행을 제외한 영역을 한 트랜잭션으로 저장 |
| 상세정보 행 등록 | `POST /api/v1/hub-vendor/platform-management/{id}/system-port-detail/details` · `/hub-vendor/platform-management` `PROCESS` · [현재 Controller](https://github.com/thebusinesson/smartwork/blob/b923849c5d878772e0de2b67becff0ae511f03b3/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/platformmgmt/PlatformMgmtController.kt#L184) | 시스템 ID, 라우팅 주소·포트, JSON payload, 선택 파일 → 처리 결과 | 상세정보 1건 저장. 본문과 첨부 중 하나 이상 필요 |
| 상세정보 행 수정 | `PATCH /api/v1/hub-vendor/platform-management/{id}/system-port-detail/details/{idx}` · `/hub-vendor/platform-management` `PROCESS` · [현재 Controller](https://github.com/thebusinesson/smartwork/blob/b923849c5d878772e0de2b67becff0ae511f03b3/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/platformmgmt/PlatformMgmtController.kt#L210) | 시스템 ID, 상세정보 번호, 라우팅 주소·포트, JSON payload, 선택 파일 → 처리 결과 | 수정 행만 저장. 새 파일이 있으면 교체하고 없으면 기존 첨부 유지 |
| 상세정보 행 삭제 | `DELETE /api/v1/hub-vendor/platform-management/{id}/system-port-detail/details/{idx}` · `/hub-vendor/platform-management` `DELETE` · [현재 Controller](https://github.com/thebusinesson/smartwork/blob/b923849c5d878772e0de2b67becff0ae511f03b3/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/platformmgmt/PlatformMgmtController.kt#L235) | 시스템 ID, 상세정보 번호, 라우팅 주소·포트 → 처리 결과 | 상세정보를 논리 삭제 |
| 상세정보 첨부만 삭제 | `DELETE /api/v1/hub-vendor/platform-management/{id}/system-port-detail/details/{idx}/attachment` · `/hub-vendor/platform-management` `DELETE` · [현재 Controller](https://github.com/thebusinesson/smartwork/blob/b923849c5d878772e0de2b67becff0ae511f03b3/backend/src/main/kotlin/com/bizon/smartwork/api/integration/hubvendor/platformmgmt/PlatformMgmtController.kt#L249) | 시스템 ID, 상세정보 번호, 라우팅 주소·포트 → 처리 결과 | 상세정보 행을 유지하고 첨부를 제거 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.usp_platform_mgmt_import_history_exec` | @SERVICETYPE varchar(20), @OLD_IP varchar(100), @OLD_PORT varchar(10), @NEW_IP varchar(100), @NEW_PORT varchar(10), @ROUTINGURL_YN varchar(2), @ENGINEER_YN varchar(2), @ERP_YN varchar(2), @DETAIL_YN varchar(2), @CUSER int | 정의 참조 `office.dbo.upMg_Import_HubDetailInfo` · 하위 호출 `office.dbo.upMg_Import_HubDetailInfo` · 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubvendor/platformmgmt/repository/PlatformMgmtMapper.kt#L405) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-474a028cea9db52a) |
| `smartwork.dbo.usp_platform_mgmt_detail_relays_select` | 두 환경의 메타데이터 확인 | 접근방법·담당자·ERP·SAP·상세정보 조회 | [개발·Demo 정의](../../references/all-pages-audit-2026-11-12.md#db-c2e5fd5251bf) |
| `smartwork.dbo.usp_platform_mgmt_port_detail_ports_select` | 두 환경의 메타데이터 확인 | 접근방법·담당자·ERP·SAP·상세정보 조회 | [개발·Demo 정의](../../references/all-pages-audit-2026-11-12.md#db-f827772d5683) |
| `smartwork.dbo.usp_platform_mgmt_port_detail_access_select` | 두 환경의 메타데이터 확인 | 접근방법·담당자·ERP·SAP·상세정보 조회 | [개발·Demo 정의](../../references/all-pages-audit-2026-11-12.md#db-575acc66425e) |
| `smartwork.dbo.usp_platform_mgmt_port_detail_contacts_select` | 두 환경의 메타데이터 확인 | 접근방법·담당자·ERP·SAP·상세정보 조회 | [개발·Demo 정의](../../references/all-pages-audit-2026-11-12.md#db-42bf88d0df14) |
| `smartwork.dbo.usp_platform_mgmt_port_detail_erp_select` | 두 환경의 메타데이터 확인 | 접근방법·담당자·ERP·SAP·상세정보 조회 | [개발·Demo 정의](../../references/all-pages-audit-2026-11-12.md#db-03caf5dfb3a6) |
| `smartwork.dbo.usp_platform_mgmt_port_detail_sap_select` | 두 환경의 메타데이터 확인 | 접근방법·담당자·ERP·SAP·상세정보 조회 | [개발·Demo 정의](../../references/all-pages-audit-2026-11-12.md#db-fb0ec1391eab) |
| `smartwork.dbo.usp_platform_mgmt_port_detail_info_select` | 두 환경의 메타데이터 확인 | 접근방법·담당자·ERP·SAP·상세정보 조회 | [개발·Demo 정의](../../references/all-pages-audit-2026-11-12.md#db-2e3226077b04) |
| `office.dbo.upsw_saveroutingurl_detail` | 두 환경의 메타데이터 확인 | 상세정보 행을 제외한 영역을 한 트랜잭션으로 저장 | [개발·Demo 정의](../../references/all-pages-audit-2026-11-12.md#db-55aa7a70e571) |
| `office.dbo.upsw_removehub_engineer_info` | 두 환경의 메타데이터 확인 | 상세정보 행을 제외한 영역을 한 트랜잭션으로 저장 | [개발·Demo 정의](../../references/all-pages-audit-2026-11-12.md#db-63a5f1274544) |
| `office.dbo.upsw_savehub_engineer_info` | 두 환경의 메타데이터 확인 | 상세정보 행을 제외한 영역을 한 트랜잭션으로 저장 | [개발·Demo 정의](../../references/all-pages-audit-2026-11-12.md#db-cfba18f9a967) |
| `office.dbo.upsw_savehuberpdetail` | 두 환경의 메타데이터 확인 | 상세정보 행을 제외한 영역을 한 트랜잭션으로 저장 | [개발·Demo 정의](../../references/all-pages-audit-2026-11-12.md#db-71ef10f09b8b) |
| `smartwork.dbo.usp_platform_mgmt_sap_remove_all` | 두 환경의 메타데이터 확인 | 상세정보 행을 제외한 영역을 한 트랜잭션으로 저장 | [개발·Demo 정의](../../references/all-pages-audit-2026-11-12.md#db-e7ee81277c6d) |
| `smartwork.dbo.usp_platform_mgmt_sap_insert` | 두 환경의 메타데이터 확인 | 상세정보 행을 제외한 영역을 한 트랜잭션으로 저장 | [개발·Demo 정의](../../references/all-pages-audit-2026-11-12.md#db-9690a307d7dc) |
| `office.dbo.upsw_savehubdetail_info` | 두 환경의 메타데이터 확인 | 상세정보 1건 저장. 본문과 첨부 중 하나 이상 필요 | [개발·Demo 정의](../../references/all-pages-audit-2026-11-12.md#db-eea33b196fc7) |
| `office.dbo.upsw_modifyhubdetail_info` | 두 환경의 메타데이터 확인 | 수정 행만 저장. 새 파일이 있으면 교체하고 없으면 기존 첨부 유지 | [개발·Demo 정의](../../references/all-pages-audit-2026-11-12.md#db-6275815456e1) |
| `office.dbo.upmg_remove_each_distribution_info` | 두 환경의 메타데이터 확인 | 상세정보를 논리 삭제 | [개발·Demo 정의](../../references/all-pages-audit-2026-11-12.md#db-6faa3dbbe2b6) |
| `office.dbo.upmg_remove_attachfile_distribution_info` | 두 환경의 메타데이터 확인 | 상세정보 행을 유지하고 첨부를 제거 | [개발·Demo 정의](../../references/all-pages-audit-2026-11-12.md#db-6d802d502932) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 기타, 원격터미널, 방문, 특이사항, 요청사항, 배포 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > 연동플랫폼 통합관리의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/IntegrationRoutes.tsx#L114) · [SystemPortDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/SystemPortDetailPage.tsx#L19) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/api/integrationPlatformApi.ts#L373) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/api/integrationPlatformApi.ts#L537) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubvendor/api/integrationPlatformApi.ts#L495) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 이전 근거는 11월 11일 기준. 현재 행별 저장과 삭제는 아래 최신 변경 대조를 참조한다. |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-3a95920a3db197ed) | 2026-11-11 기준으로 Demo 메타데이터 1/1개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |
| 최신 변경 대조 | [11월 12일 전수 대조](../../references/all-pages-audit-2026-11-12.md) | 현재 코드 b923849c5 · 2026-11-12 |

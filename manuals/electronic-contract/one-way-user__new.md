# [전자계약 원문·이용과 접근] 단방향 이용 고객 조회 등록 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

단방향 이용 고객 조회 등록에서 대상과 입력값을 확인해 **단방향 이용고객 등록** 업무를 처리한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 전자계약 원문·이용과 접근 |
| 언제 사용하는가 | 단방향 이용고객 등록 회사 확인, 단방향 이용고객 등록 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 사업자 번호, 프로세스ID, 프로세스명, 파일개수, 파일첨부방식, 파일첨부방식1 |
| 업무 흐름 | 단방향 이용고객 등록 회사 확인, 단방향 이용고객 등록 |
| 이 페이지의 역할 | 등록 · 단방향 이용고객 등록 |
| 판단 결과·다음 업무 | [단방향 이용 고객 조회](one-way-user.md) |
| 다른 화면과의 구분 | SB 서비스관리 > 전자계약 > 단방향 이용 고객 조회에서 사용하는 등록 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 단방향 이용 고객 조회 등록에서 대상과 입력값을 확인해 **단방향 이용고객 등록** 업무를 처리한다. |
| 메뉴·화면 경로 | SB 서비스관리 > 전자계약 > 단방향 이용 고객 조회 · `/electronic-contract/one-way-user/new` |
| 화면 유형·담당 | 등록 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [단방향 이용 고객 조회](one-way-user.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/electronic-contract/one-way-user` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 단방향 이용고객 등록 회사 확인 | `/electronic-contract/one-way-user` `VIEW` | `bizNo: String` |
| 단방향 이용고객 등록 | `/electronic-contract/one-way-user` `PROCESS` | `OneWayUserSaveRequest` `companyNo`, `processId`, `processName`, `fileCount`, `contractFileMethod`, `attachmentFileMethod1`, `attachmentFileMethod2`, `attachmentFileMethod3`, `attachmentFileMethod4`, `contractFileName`, `attachmentFileName1`, `attachmentFileName2`, `attachmentFileName3`, `attachmentFileName4` · 서버 필수 `processId`, `processName`, `uploadPage` |

코드에서 확인한 버튼·작업명은 **검색**, **저장**, **취소**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [단방향 이용 고객 조회](one-way-user.md)에서 대상 또는 작업을 선택한다. `/electronic-contract/one-way-user/new`를 연다.
2. **사업자 번호** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색**, **저장** 중 해당 버튼을 선택한다.
3. **단방향 이용고객 등록**을 실행하기 전에 변경 대상과 입력값을 확인한다. 표시되는 **단방향 이용 고객 등록이 완료되었습니다.** 메시지와 대상 상태를 확인한다.
4. 후속 조회나 목록 복귀가 필요하면 [단방향 이용 고객 조회](one-way-user.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 사업자 번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/OneWayUserRegister.tsx#L40) |
| 프로세스ID | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/OneWayUserRegister.tsx#L230) |
| 프로세스명 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/OneWayUserRegister.tsx#L246) |
| 파일개수 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/OneWayUserRegister.tsx#L262) |
| 파일첨부방식 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/OneWayUserRegister.tsx#L280) |
| 파일첨부방식1 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/OneWayUserRegister.tsx#L296) |
| 파일첨부방식2 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/OneWayUserRegister.tsx#L312) |
| 파일첨부방식3 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/OneWayUserRegister.tsx#L328) |
| 파일첨부방식4 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/OneWayUserRegister.tsx#L344) |
| 계약서파일명 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/OneWayUserRegister.tsx#L360) |
| 첨부파일1 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/OneWayUserRegister.tsx#L372) |
| 첨부파일2 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/OneWayUserRegister.tsx#L380) |
| 첨부파일3 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/OneWayUserRegister.tsx#L388) |
| 첨부파일4 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/OneWayUserRegister.tsx#L396) |
| 업로드 파일명 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/OneWayUserRegister.tsx#L404) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 단방향 이용고객 등록 회사 확인 | `GET /api/v1/electronic-contract/one-way-users/companies/lookup` · `/electronic-contract/one-way-user` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/electroniccontract/onewayuser/OneWayUserController.kt#L75) | `bizNo: String` → `success`, `data`, `error`, `companyName`, `companyNo`, `bizNo` | `SmartBill3.dbo.upAdmSB_ChkComRegNo` |
| 단방향 이용고객 등록 | `POST /api/v1/electronic-contract/one-way-users` · `/electronic-contract/one-way-user` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/service/electroniccontract/onewayuser/OneWayUserController.kt#L111) | `OneWayUserSaveRequest` `companyNo`, `processId`, `processName`, `fileCount`, `contractFileMethod`, `attachmentFileMethod1`, `attachmentFileMethod2`, `attachmentFileMethod3`, `attachmentFileMethod4`, `contractFileName`, `attachmentFileName1`, `attachmentFileName2`, `attachmentFileName3`, `attachmentFileName4` · 서버 필수 `processId`, `processName`, `uploadPage` → `success`, `data`, `error`, `companyName`, `bizNo`, `companyNo`, `processIdNo`, `processId`, `processName`, `fileCount`, `contractFileMethod`, `attachmentFileMethod1` | `SmartBill3.dbo.upAdmSB_SavDctProcessID`, `SmartBill3.dbo.upAdmSB_Lst_DctProcessID`, `SmartBill3.dbo.upAdmSB_Lst_ModDctProcessID` · 정의에서 확인한 쓰기 `SmartBill3.dbo.DCT_PROCESSID` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `SmartBill3.dbo.upAdmSB_ChkComRegNo` | @comRegNo varchar(10) | 정의 참조 `SmartBill3.dbo.COMPANY` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/onewayuser/repository/OneWayUserMapper.kt#L47) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b7a098581a6f204b) |
| `SmartBill3.dbo.upAdmSB_SavDctProcessID` | @pid_no int, @com_no int, @processID varchar(10), @processID_name varchar(30), @File_Count int, @Co_File_Method char(2), @File_Method1 char(2), @File_Method2 char(2), @File_Method3 char(2), @File_Method4 char(2), @Co_FileName varchar(100), @FileName1 varchar(100), @FileName2 varchar(100), @FileName3 varchar(100), @FileName4 varchar(100), @upload_page varchar(100), @admin_no int, @div varchar(3) | 정의 참조 `SmartBill3.dbo.DCT_PROCESSID` · 정적 쓰기 `SmartBill3.dbo.DCT_PROCESSID` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/onewayuser/repository/OneWayUserMapper.kt#L85) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-ac6523e940ebcf4c) |
| `SmartBill3.dbo.upAdmSB_Lst_DctProcessID` | @strItem varchar(30), @strTextComno varchar(30), @strItem2 varchar(30), @strTextProcess varchar(30) | 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/onewayuser/repository/OneWayUserMapper.kt#L37) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-0d547c8d49bbc8f2) |
| `SmartBill3.dbo.upAdmSB_Lst_ModDctProcessID` | @com_no varchar(15), @idx int | 정의 참조 `SmartBill3.dbo.COMPANY`, `SmartBill3.dbo.DCT_PROCESSID` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/electroniccontract/onewayuser/repository/OneWayUserMapper.kt#L71) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-f5af4dcf2a48352e) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 사업자 번호, 프로세스ID, 프로세스명, 파일개수, 파일첨부방식, 파일첨부방식1 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 서비스관리 > 전자계약 > 단방향 이용 고객 조회의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 사업자 번호를 확인하세요. | 사업자 번호, 프로세스ID, 프로세스명, 파일개수, 파일첨부방식, 파일첨부방식1 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 단방향 이용 고객 등록 중 오류가 발생했습니다. | 사업자 번호, 프로세스ID, 프로세스명, 파일개수, 파일첨부방식, 파일첨부방식1 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 검색 중 오류가 발생했습니다. | 사업자 번호, 프로세스ID, 프로세스명, 파일개수, 파일첨부방식, 파일첨부방식1 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/ElectronicContractRoutes.tsx#L32) · [OneWayUserRegister.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/OneWayUserRegister.tsx#L60) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/api/oneWayUserSearchApi.ts#L29) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/electroniccontract/api/oneWayUserSearchApi.ts#L46) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 4개 중 개발 메타데이터 확인 4개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-9ff0b0ad703f0e67) | Demo 메타데이터 4/4개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

# [SB 서비스관리] 인증키 관리 (조회·관리) 관리자 매뉴얼

작성 기준: `dc216b313` · 확인일 2026-11-09 · 조사 상태 **검토 대기**. 코드·개발 DB 정의 확인. 브라우저: **화면 대조**; 저장·발송 등 업무 실행 결과는 미검증이다.

## 1) 화면 기본 정보

### 도메인 이해

설치형 수집 대상의 인증키별 사용·연동·운영 설정이 맞는지 확인하고 관리한다.

| 구분 | 설명 |
|---|---|
| 업무 영역 | 설치형 홈택스 세금계산서 수집 > 인증키 관리 조회·관리 |
| 언제 사용하는가 | 수집 대상을 새로 등록하거나 실행 주기·ERP/인증서 등록 조건을 점검할 때 |
| 주요 대상·데이터 | 인증키는 설치/연동 대상 식별자이며 사용여부·운영여부·DB 종류·실행간격은 수집 설정이다. |
| 업무 흐름 | 허브업체·설정 조건 검색 → 인증키 설정 확인 → 등록 팝업 또는 키 상세 선택 |
| 이 페이지의 역할 | 수집 연동 설정 중 **인증키 관리 조회·관리** 단계. 설치형 수집 대상의 인증키별 사용·연동·운영 설정이 맞는지 확인하고 관리한다. |
| 판단 결과·다음 업무 | 대상 설정을 맞춘 후 실제 실행 여부는 모니터링에서 확인한다. |
| 다른 화면과의 구분 | 인증키 사용 설정과 인증서의 유효기간·로그인 성공 여부는 서로 다른 점검 대상이다. |

**탭·영역·팝업별 업무 구분**

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
|---|---|---|---|
| 등록 팝업 | 새 설치·연동 대상을 추가할 때 | 새 인증키 대상의 업체·연동·운영 등 입력값 | 저장 성공 후 목록에서 새 대상을 확인한다. 기존 키 상세 조회와 구분한다. |
| 기존 행의 상세 이동 | 이미 등록된 키의 사용자·업체·인증서를 조사할 때 | 선택 sbKey에 연결된 담당자·사업자·인증서 정보 | 독립 상세 문서로 이동한다. 등록 팝업과 데이터 대상이 다르다. |

설명 근거: [AuthKeyManagementPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/AuthKeyManagementPage.tsx), 이 문서 4·5·7번의 항목·API·업무 규칙. [상위 업무 영역](../../references/domain-overview.md#hometax)은 공통 배경이며 현재 화면의 데이터·동작은 위 설명을 따른다. 설명 수정일 **2026-11-10**; 새 업무 실행 검증을 수행한 것은 아니다.

### 화면 정보

| 항목 | 작성 내용 |
|---|---|
| 업무 도메인·목적 | 설치형 수집 대상의 인증키별 사용·연동·운영 설정이 맞는지 확인하고 관리한다. |
| 메뉴·화면 경로 | SB 서비스관리 > 홈택스 DTI 수집 > 인증키 관리; `/hometax-dti/auth-key`; 메뉴 또는 관련 화면에서 진입한다. |
| 화면 유형·담당 | 조회·관리; WBS 작업자 유지윤. 업무·기술 담당 팀명은 원문에 없어 배포 전 해당 도메인 담당자가 확정한다. |
| 관련 화면 | [상세](auth-key__by-sbKey.md) |

WBS 근거: No. 124, 125 (사용자가 제공한 텍스트 행 158, 159). API 개발/화면 개발의 중복 행은 같은 화면으로 통합했다.

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
|---|---|---|
| 화면 진입·조회 | `/hometax-dti/auth-key` 메뉴 접근·하위 경로 작업 권한. 조회 API는 VIEW, 등록/수정 경로는 PROCESS 등 아래 서버 액션과 라우트 가드를 함께 적용한다. | 로그인된 관리자 계정; 아래 검색·입력 항목을 준비한다. |
| 등록 | `/hometax-dti/auth-key`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 엑셀 다운로드 | `/hometax-dti/auth-key`; 엑셀 download 화면 게이트. 다운로드/업로드 API의 서버 권한과 사유 입력을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 선택 | `/hometax-dti/auth-key`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |

서버가 최종 권한을 검사한다. 버튼 모양(kind)으로 권한을 추정하지 않는다. 특히 등록·수정이 PROCESS를 사용하는 API와 EXECUTE·UNMASK·EXCEL_DOWNLOAD는 서로 구분한다.

## 3) 화면 사용 절차

**검증 시 화면 버튼**: 검색, 초기화, 등록, 엑셀 다운로드. 화면 상태·대상에 따라 달라지며 아래 작업 절차와 권한 조건을 함께 확인한다.

1. `SB 서비스관리 > 홈택스 DTI 수집 > 인증키 관리` 메뉴를 연다. 경로 변수는 주소에서 임의로 바꾸지 않고 이전 화면이 전달한 식별자를 사용한다.
2. 현재 검색 조건과 아래 기본값을 확인한다. **허브업체명, 사용여부, 연동 구분, 운영 여부, 이메일파싱, DB 종류, ERP 등록 누락, 인증서 미등록, 실행간격 (시간)** 항목에 필요한 값을 입력하고 **검색**을 누른다.
3. 결과 행에서 업무 대상을 선택하여 관련 상세 화면으로 이동한다. 페이지 이동·검색 조건 변경 후에는 현재 조건과 조회 대상을 다시 확인한다.

**이 화면에서 유의할 업무 규칙**: 허브업체명과 사용/운영/연동 구분·이메일파싱·ERP 누락·인증서 미등록 조건으로 찾는다. 기존 인증키는 상세에서 설정을 확인한 뒤 수정하고, 신규 등록은 목록의 등록 팝업을 사용한다. 인증·DB 접속 관련 비밀값을 매뉴얼이나 문의 내용에 복사하지 않는다.

**반출**: 적용된 검색 조건과 반출 범위를 확인한 후 다운로드한다. 사유 입력창이 표시되면 업무 사유를 입력한다. 사유 등록 실패·파일 오류는 성공으로 간주하지 않고 다운로드 결과를 확인한다.

**등록 방식**: 목록의 **등록** 버튼은 새 경로로 이동하지 않고 **인증키 등록 팝업**을 연다. 팝업에서 허브업체와 연동·운영 구분 등 필수 정보를 선택한 뒤 **저장**한다. 기존 행 선택은 `/hometax-dti/auth-key/:sbKey` 상세로 이동하는 별도 흐름이다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
|---|---|---|---|
| 허브업체명 | 입력·필수 | 화면 타입 text; API 타입 String?; 기본 null; 서버 검증 @field:Size(max = 50, message = "hubName 은 50자 이하여야 합니다."); 초기값 빈값 | `hubName`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/AuthKeyManagementPage.tsx#L96) |
| 사용여부 | 입력·선택(조건부 검증 별도) | 화면 타입 radio; API 타입 String?; 기본 null; 서버 검증 @field:Pattern(regexp = "^(Y\|N\|)$", message = "useYn 은 Y/N 또는 빈값이어야 합니다."); 선택: 전체=all, Y=Y, N=N; 초기값 all | `useYn`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/AuthKeyManagementPage.tsx#L97) |
| 연동 구분 | 입력·선택(조건부 검증 별도) | 화면 타입 radio; API 타입 String?; 기본 null; 서버 검증 @field:Pattern(regexp = "^(SAP\|NONSAP\|)$", message = "division 은 SAP/NONSAP 또는 빈값이어야 합니다."); 선택: 전체=all, SAP=SAP, NONSAP=NONSAP; 초기값 all | `division`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/AuthKeyManagementPage.tsx#L98) |
| 운영 여부 | 입력·선택(조건부 검증 별도) | 화면 타입 radio; API 타입 String?; 기본 null; 서버 검증 @field:Pattern(regexp = "^(O\|T\|)$", message = "klass 는 O/T 또는 빈값이어야 합니다."); 선택: 전체=all, 운영=O, 테스트=T; 초기값 all | `klass`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/AuthKeyManagementPage.tsx#L99) |
| 이메일파싱 | 입력·선택(조건부 검증 별도) | 화면 타입 radio; API 타입 String?; 기본 null; 서버 검증 @field:Pattern(regexp = "^(Y\|N\|)$", message = "emailParsing 은 Y/N 또는 빈값이어야 합니다."); 선택: 전체=all, Y=Y, N=N; 초기값 all | `emailParsing`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/AuthKeyManagementPage.tsx#L101) |
| DB 종류 | 입력·선택(조건부 검증 별도) | 화면 타입 radio; API 타입 String?; 기본 null; 서버 검증 @field:Pattern(regexp = "^(MYSQL\|ORACLE\|MSSQL\|)$", message = "dbType 은 MYSQL/ORACLE/MSSQL 또는 빈값이어야 합니다."); 선택: 전체=all, MYSQL=MYSQL, ORACLE=ORACLE, MSSQL=MSSQL; 초기값 all | `dbType`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/AuthKeyManagementPage.tsx#L107) |
| ERP 등록 누락 | 입력·선택(조건부 검증 별도) | 화면 타입 radio; API 타입 String?; 기본 null; 서버 검증 @field:Pattern(regexp = "^(Y\|N\|)$", message = "erpMissing 은 Y/N 또는 빈값이어야 합니다."); 선택: 전체=all, Y=Y, N=N; 초기값 all | `erpMissing`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/AuthKeyManagementPage.tsx#L108) |
| 인증서 미등록 | 입력·선택(조건부 검증 별도) | 화면 타입 radio; API 타입 String?; 기본 null; 서버 검증 @field:Pattern(regexp = "^(Y\|N\|)$", message = "certMissing 은 Y/N 또는 빈값이어야 합니다."); 선택: 전체=all, Y=Y, N=N; 초기값 all | `certMissing`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/AuthKeyManagementPage.tsx#L109) |
| 실행간격 (시간) | 입력·선택(조건부 검증 별도) | 화면 타입 select; API 타입 String?; 기본 null; 서버 검증 @field:Pattern(regexp = "^(24\|12\|6\|NONE\|)$", message = "execInterval 은 24/12/6/NONE 또는 빈값이어야 합니다."); 선택: 전체=all, 미등록=NONE, 24=24, 12=12, 6=6; 초기값 all | `execInterval`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/AuthKeyManagementPage.tsx#L110) |
| 허브업체명 | 출력 | API 타입 String? | `hubRealname`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/AuthKeyManagementPage.tsx#L214) |
| Version | 출력 | API 타입 String? | `version`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/AuthKeyManagementPage.tsx#L221) |
| 사용 여부 | 출력 | API 타입 String?; 기본 null; 서버 검증 @field:Pattern(regexp = "^(Y\|N\|)$", message = "useYn 은 Y/N 또는 빈값이어야 합니다."); 초기값 all | `useYn`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/AuthKeyManagementPage.tsx#L228) |
| 신/구 | 출력 | API 타입 String? | `oldNew`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/AuthKeyManagementPage.tsx#L235) |
| DB | 출력 | API 타입 String?; 기본 null; 서버 검증 @field:Pattern(regexp = "^(MYSQL\|ORACLE\|MSSQL\|)$", message = "dbType 은 MYSQL/ORACLE/MSSQL 또는 빈값이어야 합니다."); 초기값 all | `dbType`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/AuthKeyManagementPage.tsx#L243) |
| 부서사용자 ID | 출력 | API 타입 String? | `deptUserId`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/AuthKeyManagementPage.tsx#L250) |
| 연동 구분 | 출력 | API 타입 String?; 기본 null; 서버 검증 @field:Pattern(regexp = "^(SAP\|NONSAP\|)$", message = "division 은 SAP/NONSAP 또는 빈값이어야 합니다."); 초기값 all | `division`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/AuthKeyManagementPage.tsx#L257) |
| 운영 여부 | 출력 | API 타입 String?; 기본 null; 서버 검증 @field:Pattern(regexp = "^(O\|T\|)$", message = "klass 는 O/T 또는 빈값이어야 합니다."); 초기값 all | `klass`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/AuthKeyManagementPage.tsx#L264) |
| SAP | 출력 | API 타입 Int? | `erpSap`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/AuthKeyManagementPage.tsx#L272) |
| NONSAP | 출력 | API 타입 Int? | `erpNonSap`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/AuthKeyManagementPage.tsx#L279) |
| 스케줄러 | 출력 | API 타입 String? | `scheduler`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/AuthKeyManagementPage.tsx#L286) |
| 실행간격(시간) | 출력 | API 타입 String?; 기본 null; 서버 검증 @field:Pattern(regexp = "^(24\|12\|6\|NONE\|)$", message = "execInterval 은 24/12/6/NONE 또는 빈값이어야 합니다."); 초기값 all | `execInterval`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/AuthKeyManagementPage.tsx#L293) |
| ERP | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `erp`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/AuthKeyManagementPage.tsx#L316) |

입력 검증 근거: [createAuthKeySchema.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/service/hometaxdti/createAuthKeySchema.ts). 프런트 검증과 서버 DTO 제약이 다르면 서버 검증이 최종 기준이다.

**복합 검색·폼의 초기 상태**

| 초기값 근거 | 기본 상태 |
|---|---|
| [DEFAULT_FILTERS](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/AuthKeyManagementPage.tsx#L31) | hubName=빈값; useYn=all; division=all; klass=all; emailParsing=all; dbType=all; erpMissing=all; certMissing=all; execInterval=all |

화면 필드 키와 API 필드명이 다른 경우 변환은 Hook/API의 검색·저장 매핑에서 수행된다. 요청·응답 필드와 DB 컬럼 매핑은 아래 API 계약 및 DB 객체 계약에 연결했다.

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
|---|---|---|---|
| 인증키 목록 조회 (in-memory 페이징) | [GET /api/v1/sb-service/hometax-dti-installed/auth-keys](../../references/api-contracts.md#api078); `/hometax-dti/auth-key` / `VIEW` | `hubName, useYn, division, klass, emailParsing, dbType, erpMissing, certMissing, execInterval, page, size` → `content, totalElements, totalPages, page, size, sbKey, hubName, hubRealname, useYn, division, klass, oldNew, cdate, cname, uname, version, dbType, deptUserId, scheduler, execInterv` | Mapper 프로시저의 정적 테이블 쓰기 미검출; 동적 SQL의 런타임 대상은 미확정 |
| 관련 허브업체 콤보 옵션 조회 | [GET /api/v1/sb-service/hometax-dti-installed/auth-keys/hub-vendors](../../references/api-contracts.md#api080); `/hometax-dti/auth-key` / `VIEW` | `경로·쿼리·본문 계약 참조` → `응답 DTO·파일/처리 결과 계약 참조` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 인증키 신규 등록 | [POST /api/v1/sb-service/hometax-dti-installed/auth-keys](../../references/api-contracts.md#api224); `/hometax-dti/auth-key` / `PROCESS` | `hubName, division, klass, oldNew, bnsId, epSdate, epEdate` → `응답 DTO·파일/처리 결과 계약 참조` | 쓰기 대상 sb_scraper.dbo.use_company_info |
| 인증키 관리 엑셀 다운로드 | [GET /api/v1/sb-service/hometax-dti-installed/auth-keys/download](../../references/api-contracts.md#api079); `/hometax-dti/auth-key` / `EXCEL_DOWNLOAD` | `hubName, useYn, division, klass, emailParsing, dbType, erpMissing, certMissing, execInterval, page, size` → `응답 DTO·파일/처리 결과 계약 참조` | Mapper 프로시저의 정적 테이블 쓰기 미검출; 동적 SQL의 런타임 대상은 미확정 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
|---|---|---|---|
| [smartwork.dbo.UspViewUseCompany](../../references/database-contracts.md#db342) | `@HUB_NAME nvarchar(50) IN, @ISUSE char(1) IN, @DIVISION varchar(10) IN, @CLASS char(1) IN, @EMAILPARSING char(1) IN, @DB_TYPE varchar(100) IN, @ERP_MISSING char(1) IN, @CERT_MISSING char(1) IN, @EXEC_INTERVAL int IN` | 확정한 테이블 쓰기 없음. 참조: office.dbo.sawon, sb_scraper.dbo.use_company_detail, sb_scraper.dbo.use_company_info 동적 SQL 포함, 런타임 조합 대상 미확정. | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [OFFICE.dbo.upPJT_MNGHubList](../../references/database-contracts.md#db059) | IN 파라미터 없음 | 확정한 테이블 쓰기 없음. 참조: office.dbo.business, office.dbo.function_code, office.dbo.mng_hub | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_SCRAPER.dbo.SSP_INSERT_USE_COMPANY](../../references/database-contracts.md#db177) | `@HUB_NAME varchar(50) IN, @DIVISION varchar(10) IN, @CLASS char(1) IN, @OLDNEW char(1) IN, @BNS_ID int IN, @CUSER int IN, @EP_SDATE varchar(10) IN, @EP_EDATE varchar(10) IN, @OUT_INSERT_YN varchar(1) OUT` | 쓰기: sb_scraper.dbo.use_company_info. 참조: sb_scraper.dbo.use_company_info | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |

위 DB 계약 링크에는 실제 파라미터 타입·기본값·IN/OUT, Mapper 결과 컬럼, RETURN 바인딩, 참조 테이블·하위 프로시저·정의 필터/정렬을 기록했다. DTO·Service·Repository·Mapper의 상세 호출 경로는 각 API 계약에서 확인한다.

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
|---|---|---|
| 결과가 없거나 기대 건수와 다름 | 적용된 검색 기준·기간·탭·대상 상태·서버 필터·페이징·목록/다운로드 조건 | 조건을 다시 확인하고 조회한다. 지속되면 경로·작업 시각·마스킹한 식별자·필터를 업무/기술 담당에게 전달한다. |
| 메뉴·버튼 미표시 또는 접근 거부 | 사용자 그룹의 메뉴 접근·VIEW 및 API별 PROCESS/EXECUTE/DELETE/EXCEL_DOWNLOAD/UNMASK 등 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. 프런트 버튼 표시만으로 서버 권한을 판단하지 않는다. |
| 저장·삭제·외부 실행의 결과가 불명확 | 대상 현재 상태·중복 요청·감사 이력·API 오류·파일/외부 소비 로그 | 기존 반영 여부를 먼저 조회한다. 중복 발송·초기화·금액 처리를 피하기 위해 기술 담당 확인 후 재시도한다. |

## 7) 검증·출처

**브라우저 검증(2026-11-09)**: 화면 대조. [경로별 결과와 제한](../../references/browser-verification.md#page034). 역할별 권한 거부·저장 성공·파일 반출·외부 연계 완료는 이 결과로 보장하지 않는다.

| 검증 항목 | 근거·환경 | 상태·확인일 |
|---|---|---|
| 대상 선정 | 사용자가 WBS 탭 내용으로 제공한 텍스트의 No. 124, 125; [선정 태스크](../../inventory/wbs-tasks.csv) | 제공 텍스트 확인 2026-11-09. 원본 Excel의 탭/병합 셀을 독립 재열람한 것은 아님. |
| 메뉴·라우트·화면 | [menuConfig.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts); [HometaxDtiRoutes.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/HometaxDtiRoutes.tsx); [AuthKeyManagementPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/hometaxdti/AuthKeyManagementPage.tsx) | 코드 확인 2026-11-09, 기준 dc216b313 |
| 기능·권한·API | 이 문서의 API 계약 링크 및 연결 Hook/API·Controller·DTO·Service·Repository·Mapper | 코드 확인 2026-11-09. 조회 요청·화면 대조 범위는 아래 브라우저 근거 참조. 권한 계정별 허용·거부 및 변경 요청 실행은 미확인. |
| DB 정의 | [개발 DB 계약](../../references/database-contracts.md), 이 문서의 연결 객체 | 개발 DB 정의 확인 2026-11-09. 동적 SQL·CLR 내부·정의 미공개 참조의 미확정 범위는 객체별 기록; 후속 확인 DB 담당. |
| 브라우저 화면·배포 환경 | 로컬 인증 계정·Playwright CLI; [화면별 검증표](../../references/browser-verification.md#page034) | 화면 대조, 2026-11-09. 배포본·타 역할·업무 변경 결과는 미확인. |
| 업무 프로시저·쓰기·외부 결과 | 격리된 검증 환경·테스트 데이터의 실행 결과 | 미확인: 명시적인 저장·삭제·발송·초기화 요청은 실행하지 않음. 브라우저 GET의 업무 조회 프로시저·조회수·감사 기록은 별도 영향으로 구분. 격리 환경에서 기술 담당 확인. |

코드 확인과 DB 정의 확인은 실행 성공·업무 승인·다른 환경 적용을 보장하지 않는다. 업무·기술 담당 검토 후 조사 목록의 상태를 완료로 변경한다.

브라우저 직접 근거: [settled-static-recheck](../../evidence/browser/static-stable.json). 경로·고정 버튼명·입력 속성·표 머리글·API 상태를 보관했고 실제 데이터 값·식별자·인증정보는 제외했다.

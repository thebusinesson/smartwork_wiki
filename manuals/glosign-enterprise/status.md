# [SB 고객관리] 비밀번호 초기화 관리자 매뉴얼

작성 기준: `dc216b313` · 확인일 2026-11-09 · 조사 상태 **검토 대기**. 코드·개발 DB 정의 확인. 브라우저: **화면 대조**; 저장·발송 등 업무 실행 결과는 미검증이다.

## 1) 화면 기본 정보

### 도메인 이해

글로싸인 인증 문제를 회사 블록체인·개인 블록체인·회원 로그인 비밀번호로 나눠 초기화하는 업무다.

| 구분 | 설명 |
|---|---|
| 업무 영역 | 글로싸인 엔터프라이즈 고객·인증 관리 > 비밀번호 초기화 비밀번호 초기화 |
| 언제 사용하는가 | 대상 계정과 초기화할 비밀번호 종류가 확인된 지원 요청을 처리할 때 |
| 주요 대상·데이터 | 회사 블록체인은 사업자번호→회사 주소와 새 비밀번호, 개인 블록체인은 회원 이메일→개인 주소와 새 비밀번호를 사용한다. 회원 비밀번호는 별도 데몬 관리 팝업에서 아이디·새 비밀번호를 입력한다. |
| 업무 흐름 | 초기화 종류 선택 → 해당 대상의 식별 정보 입력 → 활성 조건·권한 확인 → 필요한 초기화 |
| 이 페이지의 역할 | 비밀번호 초기화 중 **비밀번호 초기화 비밀번호 초기화** 단계. 글로싸인 인증 문제를 회사 블록체인·개인 블록체인·회원 로그인 비밀번호로 나눠 초기화하는 업무다. |
| 판단 결과·다음 업무 | 선택한 종류의 초기화 결과를 확인하고 동일 대상을 중복 처리하지 않는다. |
| 다른 화면과의 구분 | 계약을 열 때 인증 실패로 잠긴 경우는 열람인증 초기화 메뉴의 업무다. 비밀번호 종류가 다르면 같은 조치가 아니다. |

**탭·영역·팝업별 업무 구분**

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
|---|---|---|---|
| 회사 블록체인 비밀번호 초기화 | 회사의 블록체인 계정 비밀번호를 재설정할 때 | 사업자번호로 찾은 회사 블록체인 주소·새 비밀번호 | 대상 회사 주소·권한·입력 규칙을 확인한 후 회사 계정 초기화 결과를 확인한다. |
| 개인 블록체인 비밀번호 초기화 | 개인의 블록체인 계정 비밀번호를 재설정할 때 | 회원 이메일로 찾은 개인 블록체인 주소·새 비밀번호 | 회사 주소와 구분하여 개인 주소를 확인하고 해당 계정의 결과를 확인한다. |
| 회원 비밀번호 초기화 | 글로싸인 회원 로그인 비밀번호를 바꿀 때 | 열리는 데몬 관리 팝업의 아이디·새 비밀번호 | SmartWork의 블록체인 폼과 별도 화면에서 처리한다. 팝업이 열렸다고 초기화 완료로 보지 않는다. |

설명 근거: [BlockchainPasswordResetPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/glosign/BlockchainPasswordResetPage.tsx), 이 문서 4·5·7번의 항목·API·업무 규칙. [상위 업무 영역](../../references/domain-overview.md#glosign)은 공통 배경이며 현재 화면의 데이터·동작은 위 설명을 따른다. 설명 수정일 **2026-11-10**; 새 업무 실행 검증을 수행한 것은 아니다.

### 화면 정보

| 항목 | 작성 내용 |
|---|---|
| 업무 도메인·목적 | 글로싸인 인증 문제를 회사 블록체인·개인 블록체인·회원 로그인 비밀번호로 나눠 초기화하는 업무다. |
| 메뉴·화면 경로 | SB 고객관리 > 글로싸인 엔터프라이즈 > 비밀번호 초기화; `/glosign-enterprise/status`; 메뉴 또는 관련 화면에서 진입한다. |
| 화면 유형·담당 | 비밀번호 초기화; WBS 작업자 유지윤. 업무·기술 담당 팀명은 원문에 없어 배포 전 해당 도메인 담당자가 확정한다. |
| 관련 화면 | 같은 메뉴에 별도 독립 경로 없음. 팝업·탭은 이 문서 참조. |

WBS 근거: No. 40, 41 (사용자가 제공한 텍스트 행 63, 64). API 개발/화면 개발의 중복 행은 같은 화면으로 통합했다.

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
|---|---|---|
| 화면 진입·조회 | `/glosign-enterprise/status` 메뉴 접근·하위 경로 작업 권한. 조회 API는 VIEW, 등록/수정 경로는 PROCESS 등 아래 서버 액션과 라우트 가드를 함께 적용한다. | 로그인된 관리자 계정; 아래 검색·입력 항목을 준비한다. |
| 비밀번호 초기화 | `/glosign-enterprise/status`; 화면 게이트 PROCESS. 실제 서버 액션은 API별 표 참조. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 글로싸인 관리 화면 열기 | `/glosign-enterprise/status`; 화면 게이트 PROCESS. 실제 서버 액션은 API별 표 참조. | 작업 대상과 현재 상태·변경 내용을 확인한다. |

서버가 최종 권한을 검사한다. 버튼 모양(kind)으로 권한을 추정하지 않는다. 특히 등록·수정이 PROCESS를 사용하는 API와 EXECUTE·UNMASK·EXCEL_DOWNLOAD는 서로 구분한다.

## 3) 화면 사용 절차

**검증 시 화면 버튼**: 회사 블록체인 비밀번호 초기화, 개인 블록체인 비밀번호 초기화, 회원 비밀번호 초기화, 검색, 초기화, 비밀번호 초기화 (비활성). 화면 상태·대상에 따라 달라지며 아래 작업 절차와 권한 조건을 함께 확인한다.

1. `SB 고객관리 > 글로싸인 엔터프라이즈 > 비밀번호 초기화` 메뉴를 연다. 경로 변수는 주소에서 임의로 바꾸지 않고 이전 화면이 전달한 식별자를 사용한다.
2. 개인 또는 회사 블록체인 탭을 선택한다. 개인은 **회원 이메일**, 회사는 **사업자번호**를 입력하고 **검색**한다. 주소가 없으면 대상 정보를 확인하며 초기화를 진행하지 않는다.
3. 조회된 **블록체인 주소**를 확인하고 **새 비밀번호**를 영문과 숫자를 모두 포함한 6~12자리로 입력한다. **비밀번호 초기화**를 누른 뒤 확인창에서 대상 주소를 확인하고 **확인**한다.
4. 완료/실패 메시지를 확인한다. 회원 비밀번호는 회원 탭의 **글로싸인 관리 화면 열기**에서 외부 데몬 팝업으로 처리한다. 팝업 차단 시 브라우저 설정을 확인한다. 검색 대상이 변경되면 이전 주소와 새 비밀번호가 무효화되므로 다시 검색한다.

**이 화면에서 유의할 업무 규칙**: 개인·회사·회원 탭을 구분한다. 개인/회사는 새 비밀번호를 직접 입력해 데몬 초기화를 요청한다. 회원 탭은 글로싸인 관리 화면을 여는 외부 연계이며 이 문서에 실제 새 비밀번호를 기록하지 않는다. 외부 호출의 결과가 불명확하면 중복 초기화 전에 담당자에게 확인한다.

**실제 탭 표기**는 **회사 블록체인 비밀번호 초기화**, **개인 블록체인 비밀번호 초기화**, **회원 비밀번호 초기화**다. 회사·개인은 검색으로 블록체인 주소를 확보한 뒤 초기화하며, 회원 탭의 **글로싸인 관리 화면 열기**는 외부 관리 팝업을 연다. 주소가 없는 상태에서 새 비밀번호·초기화 버튼이 비활성화되는 조건을 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
|---|---|---|---|
| 회원 이메일 | 입력·필수 | 화면 타입 text; 초기값 빈값 | `email`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/glosign/PersonalPasswordReset.tsx#L34) |
| 블록체인 주소 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/glosign/PersonalPasswordReset.tsx#L149) |
| 새 비밀번호 | 입력·필수 | 최대 12자; API 타입 String; 기본 ""; 서버 검증 @field:NotBlank(message = "newPass 는 필수입니다."); @field:Pattern(regexp = "^(?=.*[a-zA-Z])(?=.*[0-9])[a-zA-Z0-9]{6,12}$", message = "newPass 는 영문과 숫자를 모두 포함한 6~12자여야 합니다."); 초기값 빈값 | `newPass`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/glosign/PersonalPasswordReset.tsx#L158) |
| 사업자번호 | 입력·선택(조건부 검증 별도) | 화면 타입 text; 최대 10자; 초기값 빈값 | `businessNumber`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/glosign/CompanyPasswordReset.tsx#L30) |

입력 검증 근거: [PersonalPasswordReset.schema.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/customer/glosign/PersonalPasswordReset.schema.ts), [blockchainPasswordUtils.checks.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/customer/glosign/utils/blockchainPasswordUtils.checks.ts), [CompanyPasswordReset.schema.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/customer/glosign/CompanyPasswordReset.schema.ts). 프런트 검증과 서버 DTO 제약이 다르면 서버 검증이 최종 기준이다.

**복합 검색·폼의 초기 상태**

| 초기값 근거 | 기본 상태 |
|---|---|
| [DEFAULT_VALUES](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/glosign/PersonalPasswordReset.tsx#L29) | email=빈값; newPass=빈값 |
| [DEFAULT_VALUES](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/glosign/CompanyPasswordReset.tsx#L24) | businessNumber=빈값; newPass=빈값 |

화면 필드 키와 API 필드명이 다른 경우 변환은 Hook/API의 검색·저장 매핑에서 수행된다. 요청·응답 필드와 DB 컬럼 매핑은 아래 API 계약 및 DB 객체 계약에 연결했다.

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
|---|---|---|---|
| 비밀번호 초기화 | [POST /api/v1/glosign-enterprise/password-reset](../../references/api-contracts.md#api219); `/glosign-enterprise/status` / `PROCESS` | `chainAddr, newPass, reason` → `message` | 쓰기 대상 smartwork.dbo.action_reason |
| 블록체인 주소 조회 | [GET /api/v1/glosign-enterprise/password-reset/address](../../references/api-contracts.md#api072); `/glosign-enterprise/status` / `VIEW` | `type, keyword` → `blockchainAddress` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
|---|---|---|---|
| [smartwork.dbo.action_reason](../../references/database-contracts.md#db266) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 쓰기: smartwork.dbo.action_reason. 참조: smartwork.dbo.action_reason | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SmartBill3.dbo.upAdmSB_BlockChainAddress](../../references/database-contracts.md#db211) | `@GUBUN char(1) IN, @SEARCHTEXT varchar(200) IN` | 확정한 테이블 쓰기 없음. 참조: sec_pt.dbo.tbl_pt_org, sec_pt.dbo.tbl_pt_usr | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| 외부 데몬: glosign.daemon.init-chain-pass-url | chainAddr→chainAddress 및 newPass; HTML RESULT 응답 | 개인/회사 비밀번호를 외부 POST로 변경한다. reason이 빈값이면 감사 이력 저장을 건너뛰며 비밀번호는 감사 메타에 포함하지 않는다. 회원 탭은 외부 관리 팝업 진입 | [BlockchainPasswordResetService.kt](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/glosign/passwordreset/service/BlockchainPasswordResetService.kt) |

위 DB 계약 링크에는 실제 파라미터 타입·기본값·IN/OUT, Mapper 결과 컬럼, RETURN 바인딩, 참조 테이블·하위 프로시저·정의 필터/정렬을 기록했다. DTO·Service·Repository·Mapper의 상세 호출 경로는 각 API 계약에서 확인한다.

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
|---|---|---|
| 결과가 없거나 기대 건수와 다름 | 적용된 검색 기준·기간·탭·대상 상태·서버 필터·페이징·목록/다운로드 조건 | 조건을 다시 확인하고 조회한다. 지속되면 경로·작업 시각·마스킹한 식별자·필터를 업무/기술 담당에게 전달한다. |
| 메뉴·버튼 미표시 또는 접근 거부 | 사용자 그룹의 메뉴 접근·VIEW 및 API별 PROCESS/EXECUTE/DELETE/EXCEL_DOWNLOAD/UNMASK 등 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. 프런트 버튼 표시만으로 서버 권한을 판단하지 않는다. |
| 저장·삭제·외부 실행의 결과가 불명확 | 대상 현재 상태·중복 요청·감사 이력·API 오류·파일/외부 소비 로그 | 기존 반영 여부를 먼저 조회한다. 중복 발송·초기화·금액 처리를 피하기 위해 기술 담당 확인 후 재시도한다. |

## 7) 검증·출처

**브라우저 검증(2026-11-09)**: 화면 대조. [경로별 결과와 제한](../../references/browser-verification.md#page013). 역할별 권한 거부·저장 성공·파일 반출·외부 연계 완료는 이 결과로 보장하지 않는다.

| 검증 항목 | 근거·환경 | 상태·확인일 |
|---|---|---|
| 대상 선정 | 사용자가 WBS 탭 내용으로 제공한 텍스트의 No. 40, 41; [선정 태스크](../../inventory/wbs-tasks.csv) | 제공 텍스트 확인 2026-11-09. 원본 Excel의 탭/병합 셀을 독립 재열람한 것은 아님. |
| 메뉴·라우트·화면 | [menuConfig.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts); [CustomerRoutes.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/CustomerRoutes.tsx); [BlockchainPasswordResetPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/glosign/BlockchainPasswordResetPage.tsx) | 코드 확인 2026-11-09, 기준 dc216b313 |
| 기능·권한·API | 이 문서의 API 계약 링크 및 연결 Hook/API·Controller·DTO·Service·Repository·Mapper | 코드 확인 2026-11-09. 조회 요청·화면 대조 범위는 아래 브라우저 근거 참조. 권한 계정별 허용·거부 및 변경 요청 실행은 미확인. |
| DB 정의 | [개발 DB 계약](../../references/database-contracts.md), 이 문서의 연결 객체 | 개발 DB 정의 확인 2026-11-09. 동적 SQL·CLR 내부·정의 미공개 참조의 미확정 범위는 객체별 기록; 후속 확인 DB 담당. |
| 브라우저 화면·배포 환경 | 로컬 인증 계정·Playwright CLI; [화면별 검증표](../../references/browser-verification.md#page013) | 화면 대조, 2026-11-09. 배포본·타 역할·업무 변경 결과는 미확인. |
| 업무 프로시저·쓰기·외부 결과 | 격리된 검증 환경·테스트 데이터의 실행 결과 | 미확인: 명시적인 저장·삭제·발송·초기화 요청은 실행하지 않음. 브라우저 GET의 업무 조회 프로시저·조회수·감사 기록은 별도 영향으로 구분. 격리 환경에서 기술 담당 확인. |

코드 확인과 DB 정의 확인은 실행 성공·업무 승인·다른 환경 적용을 보장하지 않는다. 업무·기술 담당 검토 후 조사 목록의 상태를 완료로 변경한다.

브라우저 직접 근거: [settled-static-recheck](../../evidence/browser/static-stable.json). 경로·고정 버튼명·입력 속성·표 머리글·API 상태를 보관했고 실제 데이터 값·식별자·인증정보는 제외했다.

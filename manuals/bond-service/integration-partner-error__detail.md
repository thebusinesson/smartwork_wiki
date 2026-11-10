# [SB 서비스관리] 연동업체 장애 관리 (장애 등록·수정) 관리자 매뉴얼

작성 기준: `dc216b313` · 확인일 2026-11-09 · 조사 상태 **검토 대기**. 코드·개발 DB 정의 확인. 브라우저: **화면 대조**; 저장·발송 등 업무 실행 결과는 미검증이다.

## 1) 화면 기본 정보

### 도메인 이해

허브업체의 장애·점검 안내를 등록·해제하고 점검 시간·문구를 관리한다.

| 구분 | 설명 |
|---|---|
| 업무 영역 | 채권잔액 확인 서비스 > 연동업체 장애 관리 장애 등록·수정 |
| 언제 사용하는가 | 장애 목록에서 특정 허브업체의 안내 설정을 조정해야 할 때 |
| 주요 대상·데이터 | 허브업체·서버·포트·등록/해제·시작/종료시간·안내 문구와 등록 정보가 대상이다. |
| 업무 흐름 | 대상 허브업체 확인 → 장애/점검 시간·문구 입력 → 등록/해제 선택 → 결과 확인 |
| 이 페이지의 역할 | 채권잔액 장애 안내 중 **연동업체 장애 관리 장애 등록·수정** 단계. 허브업체의 장애·점검 안내를 등록·해제하고 점검 시간·문구를 관리한다. |
| 판단 결과·다음 업무 | 현재 안내 상태를 목록에서 확인하고 실제 장애 복구 여부는 기술 조사 결과와 따로 판단한다. |
| 다른 화면과의 구분 | 실제 송수신 로그를 수정하거나 서버를 복구하는 화면이 아니라 장애 안내 설정을 관리하는 화면이다. |

설명 근거: [IntegrationPartnerErrorRegist.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/IntegrationPartnerErrorRegist.tsx), 이 문서 4·5·7번의 항목·API·업무 규칙. [상위 업무 영역](../../references/domain-overview.md#bond)은 공통 배경이며 현재 화면의 데이터·동작은 위 설명을 따른다. 설명 수정일 **2026-11-10**; 새 업무 실행 검증을 수행한 것은 아니다.

### 화면 정보

| 항목 | 작성 내용 |
|---|---|
| 업무 도메인·목적 | 허브업체의 장애·점검 안내를 등록·해제하고 점검 시간·문구를 관리한다. |
| 메뉴·화면 경로 | SB 서비스관리 > 채권잔액 확인 서비스 > 연동업체 장애 관리; `/bond-service/integration-partner-error/detail`; 메뉴 또는 관련 화면에서 진입한다. |
| 화면 유형·담당 | 장애 등록·수정; WBS 작업자 유지윤. 업무·기술 담당 팀명은 원문에 없어 배포 전 해당 도메인 담당자가 확정한다. |
| 관련 화면 | [조회·관리](integration-partner-error.md) |

WBS 근거: No. 116 (사용자가 제공한 텍스트 행 147). API 개발/화면 개발의 중복 행은 같은 화면으로 통합했다.

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
|---|---|---|
| 화면 진입·조회 | `/bond-service/integration-partner-error` 메뉴 접근·하위 경로 작업 권한. 조회 API는 VIEW, 등록/수정 경로는 PROCESS 등 아래 서버 액션과 라우트 가드를 함께 적용한다. | 로그인된 관리자 계정; 아래 검색·입력 항목을 준비한다. |
| 저장 | `/bond-service/integration-partner-error`; 화면 게이트 PROCESS. 실제 서버 액션은 API별 표 참조. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 목록 | `/bond-service/integration-partner-error`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |

서버가 최종 권한을 검사한다. 버튼 모양(kind)으로 권한을 추정하지 않는다. 특히 등록·수정이 PROCESS를 사용하는 API와 EXECUTE·UNMASK·EXCEL_DOWNLOAD는 서로 구분한다.

## 3) 화면 사용 절차

**검증 시 화면 버튼**: 저장, 목록. 화면 상태·대상에 따라 달라지며 아래 작업 절차와 권한 조건을 함께 확인한다.

1. 관련 화면에서 대상 또는 작업을 선택하여 `/bond-service/integration-partner-error/detail`로 이동한다. 경로 변수는 주소에서 임의로 바꾸지 않고 이전 화면이 전달한 식별자를 사용한다.
2. **허브업체 정보, 허브업체 명, 서버 주소, 장애 등록, • 서비스 점검 시간, 시작시간, 종료시간, • 장애 안내 문구**의 입력값을 확인한다. 기존 정보와 원문을 확인한 뒤 변경한다. 필수값과 형식 오류가 표시되면 해당 항목을 수정한다.
3. **저장**을 누르고 확인창이 있으면 대상·작업을 확인한다. 첨부가 있으면 기존 파일의 유지·삭제·교체 선택을 함께 확인한다.
4. 처리 결과 메시지를 확인한 뒤 목록 또는 상세에서 결과를 다시 조회한다. 오류가 나면 아래 예외 대응과 API 오류를 확인하고 중복 저장 전에 기존 처리 여부를 확인한다.

**이 화면에서 유의할 업무 규칙**: 허브업체를 선택하여 현재 장애 설정을 확인한다. 상세/등록 화면에서 점검 시간과 안내 문구를 입력하고 저장한다. 운영 중인 연동업체에 영향이 있으므로 대상·기간을 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
|---|---|---|---|
| 등록시간 | 출력 | API 타입 String? | `registeredAt`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/IntegrationPartnerErrorRegist.tsx#L141) |
| 등록/해제 | 출력 | API 타입 String? | `errorYn`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/IntegrationPartnerErrorRegist.tsx#L142) |
| 시작시간 | 출력 | API 타입 String? | `fromDatetime`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/IntegrationPartnerErrorRegist.tsx#L143) |
| 종료시간 | 출력 | API 타입 String? | `toDatetime`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/IntegrationPartnerErrorRegist.tsx#L144) |
| 포트 | 출력 | API 타입 String; 기본 ""; 서버 검증 @field:NotBlank(message = "port 는 필수입니다."); @field:Size(max = 10, message = "port 는 10자 이하여야 합니다.") | `port`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/IntegrationPartnerErrorRegist.tsx#L145) |
| 등록자 | 출력 | API 타입 String? | `operatorName`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/IntegrationPartnerErrorRegist.tsx#L146) |
| 허브업체 정보 | 입력·선택(조건부 검증 별도) | 길이·형식·조건부 필수는 검증 코드와 API DTO 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/IntegrationPartnerErrorRegist.tsx#L234) |
| 허브업체 명 | 입력·선택(조건부 검증 별도) | 길이·형식·조건부 필수는 검증 코드와 API DTO 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/IntegrationPartnerErrorRegist.tsx#L238) |
| 서버 주소 | 입력·선택(조건부 검증 별도) | 길이·형식·조건부 필수는 검증 코드와 API DTO 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/IntegrationPartnerErrorRegist.tsx#L245) |
| 장애 등록 | 입력·선택(조건부 검증 별도) | 길이·형식·조건부 필수는 검증 코드와 API DTO 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/IntegrationPartnerErrorRegist.tsx#L271) |
| • 서비스 점검 시간 | 입력·선택(조건부 검증 별도) | 길이·형식·조건부 필수는 검증 코드와 API DTO 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/IntegrationPartnerErrorRegist.tsx#L276) |
| 시작시간 | 입력·선택(조건부 검증 별도) | 길이·형식·조건부 필수는 검증 코드와 API DTO 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/IntegrationPartnerErrorRegist.tsx#L280) |
| 종료시간 | 입력·선택(조건부 검증 별도) | 길이·형식·조건부 필수는 검증 코드와 API DTO 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/IntegrationPartnerErrorRegist.tsx#L310) |
| • 장애 안내 문구 | 입력·선택(조건부 검증 별도) | 길이·형식·조건부 필수는 검증 코드와 API DTO 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/IntegrationPartnerErrorRegist.tsx#L344) |
| 장애 등록 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `register`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/IntegrationPartnerErrorRegist.tsx#L366) |
| 장애 해제 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `release`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/IntegrationPartnerErrorRegist.tsx#L370) |
| 서비스 점검 내역 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/IntegrationPartnerErrorRegist.tsx#L387) |

입력 검증 근거: [linkedVendorFailureSchema.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/service/linkedVendorFailureSchema.ts). 프런트 검증과 서버 DTO 제약이 다르면 서버 검증이 최종 기준이다.

화면 필드 키와 API 필드명이 다른 경우 변환은 Hook/API의 검색·저장 매핑에서 수행된다. 요청·응답 필드와 DB 컬럼 매핑은 아래 API 계약 및 DB 객체 계약에 연결했다.

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
|---|---|---|---|
| 연동 업체 장애 단건 상세 조회 | [GET /api/v1/bond-service/drc-hub-errors/detail](../../references/api-contracts.md#api036); `/bond-service/integration-partner-error` / `VIEW` | `routingUrl, port` → `routingUrl, port, currentErrorYn, errorMsg, fromDatetime, toDatetime, availablePorts, histories, registeredAt, errorYn, fromDatetime, toDatetime, port, operatorName` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 연동 업체 장애 저장 (등록/해제) | [POST /api/v1/bond-service/drc-hub-errors](../../references/api-contracts.md#api196); `/bond-service/integration-partner-error` / `PROCESS` | `routingUrl, port, errorYn, errorMsg, fromDatetime, toDatetime` → `응답 DTO·파일/처리 결과 계약 참조` | 쓰기 대상 sb_drc.dbo.drc_routing_error_reg, sb_drc.dbo.drc_routing_error_reg_his |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
|---|---|---|---|
| [SB_DRC.dbo.upDRC_Routing_Error_Reg_history](../../references/database-contracts.md#db130) | `@ROUTINGURL varchar(50) IN` | 확정한 테이블 쓰기 없음. 참조: office.dbo.sawon, sb_drc.dbo.drc_routing_error_reg_his | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.UspDrcHubErrorPortList](../../references/database-contracts.md#db329) | `@ROUTINGURL varchar(50) IN` | 확정한 테이블 쓰기 없음. 참조: sb_drc.dbo.drc_company_link | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.UspDrcHubErrorRegDetail](../../references/database-contracts.md#db330) | `@ROUTINGURL varchar(50) IN, @PORT varchar(10) IN` | 확정한 테이블 쓰기 없음. 참조: sb_drc.dbo.drc_routing_error_reg | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DRC.dbo.upDRC_Routing_Error_Reg](../../references/database-contracts.md#db129) | `@ERROR_YN varchar(5) IN, @ERROR_REG_SIG varchar(10) IN, @PORT varchar(10) IN, @ROUTINGURL varchar(50) IN, @SW_NO varchar(10) IN, @SB_USE_CODE varchar(5) IN, @FROM_DATETIME varchar(30) IN, @TO_DATETIME varchar(30) IN, @ERROR_MSG varchar(1000) IN` | 쓰기: sb_drc.dbo.drc_routing_error_reg, sb_drc.dbo.drc_routing_error_reg_his. 참조: sb_drc.dbo.drc_company_link, sb_drc.dbo.drc_routing_error_reg, sb_drc.dbo.drc_routing_error_reg_his | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |

위 DB 계약 링크에는 실제 파라미터 타입·기본값·IN/OUT, Mapper 결과 컬럼, RETURN 바인딩, 참조 테이블·하위 프로시저·정의 필터/정렬을 기록했다. DTO·Service·Repository·Mapper의 상세 호출 경로는 각 API 계약에서 확인한다.

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
|---|---|---|
| 결과가 없거나 기대 건수와 다름 | 적용된 검색 기준·기간·탭·대상 상태·서버 필터·페이징·목록/다운로드 조건 | 조건을 다시 확인하고 조회한다. 지속되면 경로·작업 시각·마스킹한 식별자·필터를 업무/기술 담당에게 전달한다. |
| 메뉴·버튼 미표시 또는 접근 거부 | 사용자 그룹의 메뉴 접근·VIEW 및 API별 PROCESS/EXECUTE/DELETE/EXCEL_DOWNLOAD/UNMASK 등 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. 프런트 버튼 표시만으로 서버 권한을 판단하지 않는다. |
| 저장·삭제·외부 실행의 결과가 불명확 | 대상 현재 상태·중복 요청·감사 이력·API 오류·파일/외부 소비 로그 | 기존 반영 여부를 먼저 조회한다. 중복 발송·초기화·금액 처리를 피하기 위해 기술 담당 확인 후 재시도한다. |

## 7) 검증·출처

**브라우저 검증(2026-11-09)**: 화면 대조. [경로별 결과와 제한](../../references/browser-verification.md#page030). 역할별 권한 거부·저장 성공·파일 반출·외부 연계 완료는 이 결과로 보장하지 않는다.

| 검증 항목 | 근거·환경 | 상태·확인일 |
|---|---|---|
| 대상 선정 | 사용자가 WBS 탭 내용으로 제공한 텍스트의 No. 116; [선정 태스크](../../inventory/wbs-tasks.csv) | 제공 텍스트 확인 2026-11-09. 원본 Excel의 탭/병합 셀을 독립 재열람한 것은 아님. |
| 메뉴·라우트·화면 | [menuConfig.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts); [BondServiceRoutes.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/BondServiceRoutes.tsx); [IntegrationPartnerErrorRegist.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/IntegrationPartnerErrorRegist.tsx) | 코드 확인 2026-11-09, 기준 dc216b313 |
| 기능·권한·API | 이 문서의 API 계약 링크 및 연결 Hook/API·Controller·DTO·Service·Repository·Mapper | 코드 확인 2026-11-09. 조회 요청·화면 대조 범위는 아래 브라우저 근거 참조. 권한 계정별 허용·거부 및 변경 요청 실행은 미확인. |
| DB 정의 | [개발 DB 계약](../../references/database-contracts.md), 이 문서의 연결 객체 | 개발 DB 정의 확인 2026-11-09. 동적 SQL·CLR 내부·정의 미공개 참조의 미확정 범위는 객체별 기록; 후속 확인 DB 담당. |
| 브라우저 화면·배포 환경 | 로컬 인증 계정·Playwright CLI; [화면별 검증표](../../references/browser-verification.md#page030) | 화면 대조, 2026-11-09. 배포본·타 역할·업무 변경 결과는 미확인. |
| 업무 프로시저·쓰기·외부 결과 | 격리된 검증 환경·테스트 데이터의 실행 결과 | 미확인: 명시적인 저장·삭제·발송·초기화 요청은 실행하지 않음. 브라우저 GET의 업무 조회 프로시저·조회수·감사 기록은 별도 영향으로 구분. 격리 환경에서 기술 담당 확인. |

코드 확인과 DB 정의 확인은 실행 성공·업무 승인·다른 환경 적용을 보장하지 않는다. 업무·기술 담당 검토 후 조사 목록의 상태를 완료로 변경한다.

브라우저 직접 근거: [settled-static-recheck](../../evidence/browser/static-stable.json). 경로·고정 버튼명·입력 속성·표 머리글·API 상태를 보관했고 실제 데이터 값·식별자·인증정보는 제외했다.

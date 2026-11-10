# [SB 서비스관리] 채권잔액 전송 관리 (상세) 관리자 매뉴얼

작성 기준: `dc216b313` · 확인일 2026-11-09 · 조사 상태 **검토 대기**. 코드·개발 DB 정의 확인. 브라우저: **진입 미재현**; 저장·발송 등 업무 실행 결과는 미검증이다.

## 1) 화면 기본 정보

### 도메인 이해

하나의 채권잔액 송수신 대화에서 요청·응답·전문이 어떻게 처리되었는지 순서대로 조사한다.

| 구분 | 설명 |
|---|---|
| 업무 영역 | 채권잔액 확인 서비스 > 채권잔액 전송 관리 상세 |
| 언제 사용하는가 | 전송 목록에서 문제가 있는 conversation ID를 선택한 뒤 반환 결과를 분석할 때 |
| 주요 대상·데이터 | Send→Receive·Status·returnCode·return Msg·XML·파일경로·일시와 전송 번호가 해당 대화의 근거다. |
| 업무 흐름 | 대화 식별 확인 → 방향·발생 시각 비교 → 반환 코드·메시지·전문 확인 |
| 이 페이지의 역할 | 채권잔액 송수신 중 **채권잔액 전송 관리 상세** 단계. 하나의 채권잔액 송수신 대화에서 요청·응답·전문이 어떻게 처리되었는지 순서대로 조사한다. |
| 판단 결과·다음 업무 | 실패 구간과 반환 내용을 정리해 재전송 판단·연계 담당 문의에 사용한다. |
| 다른 화면과의 구분 | 업체별 설정이나 전체 전송 목록이 아닌 한 conversation의 로그다. 재시도 전 기존 상대방 처리 여부를 별도로 확인한다. |

설명 근거: [ReceivableBalanceTransferDetail.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/ReceivableBalanceTransferDetail.tsx), 이 문서 4·5·7번의 항목·API·업무 규칙. [상위 업무 영역](../../references/domain-overview.md#bond)은 공통 배경이며 현재 화면의 데이터·동작은 위 설명을 따른다. 설명 수정일 **2026-11-10**; 새 업무 실행 검증을 수행한 것은 아니다.

### 화면 정보

| 항목 | 작성 내용 |
|---|---|
| 업무 도메인·목적 | 하나의 채권잔액 송수신 대화에서 요청·응답·전문이 어떻게 처리되었는지 순서대로 조사한다. |
| 메뉴·화면 경로 | SB 서비스관리 > 채권잔액 확인 서비스 > 채권잔액 전송 관리; `/bond-service/receivable-balance-transfer/:conversationId`; 목록에서 선택한 대상의 경로 변수를 유지하여 진입한다. |
| 화면 유형·담당 | 상세; WBS 작업자 유지윤. 업무·기술 담당 팀명은 원문에 없어 배포 전 해당 도메인 담당자가 확정한다. |
| 관련 화면 | [조회·관리](receivable-balance-transfer.md) |

WBS 근거: No. 117, 118 (사용자가 제공한 텍스트 행 148, 149). API 개발/화면 개발의 중복 행은 같은 화면으로 통합했다.

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
|---|---|---|
| 화면 진입·조회 | `/bond-service/receivable-balance-transfer` 메뉴 접근·하위 경로 작업 권한. 조회 API는 VIEW, 등록/수정 경로는 PROCESS 등 아래 서버 액션과 라우트 가드를 함께 적용한다. | 로그인된 관리자 계정; conversationId 식별자는 이전 화면에서 선택한다. |
| 이전 | `/bond-service/receivable-balance-transfer`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |

서버가 최종 권한을 검사한다. 버튼 모양(kind)으로 권한을 추정하지 않는다. 특히 등록·수정이 PROCESS를 사용하는 API와 EXECUTE·UNMASK·EXCEL_DOWNLOAD는 서로 구분한다.

## 3) 화면 사용 절차

1. 관련 화면에서 대상 또는 작업을 선택하여 `/bond-service/receivable-balance-transfer/:conversationId`로 이동한다. 경로 변수는 주소에서 임의로 바꾸지 않고 이전 화면이 전달한 식별자를 사용한다.
2. 대상의 기본 정보·상태·표시 항목을 확인한다. 목록의 식별자와 상세 대상이 일치하는지 확인한다.
3. 표·탭·이력 영역에서 필요한 내역을 확인한다. 버튼의 표시·활성 조건과 아래 API별 권한을 확인한다. 저장·삭제·외부 호출 전에는 대상과 현재 상태를 재확인한다.
4. 작업 결과 또는 다운로드 파일을 확인하고 관련 목록으로 돌아가 변경된 상태를 다시 조회한다.

**이 화면에서 유의할 업무 규칙**: 기준일·거래처·conversation ID·진행/전송 상태로 조회한다. 상세의 로그에서 WholeMsg/BodyMsg를 선택해 전문을 확인한다. 재전송은 SOAP 외부 요청을 발생시키므로 대상 방향·상태를 확인하고 결과가 불명확하면 중복 실행 전에 로그를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
|---|---|---|---|
| Send → Receive | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `direction`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/ReceivableBalanceTransferDetail.tsx#L98) |
| Status | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `status`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/ReceivableBalanceTransferDetail.tsx#L99) |
| returnCode | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `returnCode`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/ReceivableBalanceTransferDetail.tsx#L100) |
| return Msg | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `returnMsg`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/ReceivableBalanceTransferDetail.tsx#L101) |
| XML | 출력 | API 타입 Int | `logIdx`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/ReceivableBalanceTransferDetail.tsx#L102) |
| 파일경로 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `filePath`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/ReceivableBalanceTransferDetail.tsx#L130) |
| 일시 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `occurredAt`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/ReceivableBalanceTransferDetail.tsx#L136) |
| 채권잔액 전송 번호 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/ReceivableBalanceTransferDetail.tsx#L166) |

화면 필드 키와 API 필드명이 다른 경우 변환은 Hook/API의 검색·저장 매핑에서 수행된다. 요청·응답 필드와 DB 컬럼 매핑은 아래 API 계약 및 DB 객체 계약에 연결했다.

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
|---|---|---|---|
| 로그 목록 조회 | [GET /api/v1/bond-service/receivable-balance-transfers/{conversationId}/logs](../../references/api-contracts.md#api043); `/bond-service/receivable-balance-transfer` / `VIEW` | `경로·쿼리·본문 계약 참조` → `응답 DTO·파일/처리 결과 계약 참조` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 로그 XML 단건 조회 | [GET /api/v1/bond-service/receivable-balance-transfers/logs/{logIdx}](../../references/api-contracts.md#api042); `/bond-service/receivable-balance-transfer` / `VIEW` | `type` → `logIdx, type, content` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
|---|---|---|---|
| [smartwork.dbo.UspDrcMonitoringLogList](../../references/database-contracts.md#db334) | `@ConversationId varchar(35) IN, @LogIdx int IN, @ActionStatus varchar(10) IN, @TransferStatus varchar(10) IN, @DrcNo int IN` | 확정한 테이블 쓰기 없음. 참조: sb_drc.dbo.drc_log, sb_drc.dbo.drc_main | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| 외부 SOAP: drc-resend.* | enabled, rcv-endpoint-url, snd-endpoint-url, default-target-url, connect/read-timeout-seconds | 설정 클래스 기본 enabled=false이며 비활성은 501. C/Q는 수신 서비스, A/R은 송신 서비스 분기. 요청 성공과 외부 반영을 구분 | [DrcResendProperties.kt](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/infra/config/DrcResendProperties.kt) |

위 DB 계약 링크에는 실제 파라미터 타입·기본값·IN/OUT, Mapper 결과 컬럼, RETURN 바인딩, 참조 테이블·하위 프로시저·정의 필터/정렬을 기록했다. DTO·Service·Repository·Mapper의 상세 호출 경로는 각 API 계약에서 확인한다.

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
|---|---|---|
| WholeMsg | [문구·처리 코드](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/ReceivableBalanceTransferDetail.tsx#L47); 현재 조건·대상·권한 확인 | 검색·조회 오류면 조건을 확인 후 재조회. 변경·발송 결과가 불명확하면 처리 여부와 이력을 확인한 뒤 재시도 여부를 판단한다. |
| 메시지를 불러오는 중 오류가 발생했습니다. | [문구·처리 코드](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/ReceivableBalanceTransferDetail.tsx#L54); 현재 조건·대상·권한 확인 | 검색·조회 오류면 조건을 확인 후 재조회. 변경·발송 결과가 불명확하면 처리 여부와 이력을 확인한 뒤 재시도 여부를 판단한다. |
| WHOLE | [문구·처리 코드](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/ReceivableBalanceTransferDetail.tsx#L110); 현재 조건·대상·권한 확인 | 검색·조회 오류면 조건을 확인 후 재조회. 변경·발송 결과가 불명확하면 처리 여부와 이력을 확인한 뒤 재시도 여부를 판단한다. |
| BODY | [문구·처리 코드](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/ReceivableBalanceTransferDetail.tsx#L120); 현재 조건·대상·권한 확인 | 검색·조회 오류면 조건을 확인 후 재조회. 변경·발송 결과가 불명확하면 처리 여부와 이력을 확인한 뒤 재시도 여부를 판단한다. |
| 결과가 없거나 기대 건수와 다름 | 적용된 검색 기준·기간·탭·대상 상태·서버 필터·페이징·목록/다운로드 조건 | 조건을 다시 확인하고 조회한다. 지속되면 경로·작업 시각·마스킹한 식별자·필터를 업무/기술 담당에게 전달한다. |
| 메뉴·버튼 미표시 또는 접근 거부 | 사용자 그룹의 메뉴 접근·VIEW 및 API별 PROCESS/EXECUTE/DELETE/EXCEL_DOWNLOAD/UNMASK 등 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. 프런트 버튼 표시만으로 서버 권한을 판단하지 않는다. |
| 저장·삭제·외부 실행의 결과가 불명확 | 대상 현재 상태·중복 요청·감사 이력·API 오류·파일/외부 소비 로그 | 기존 반영 여부를 먼저 조회한다. 중복 발송·초기화·금액 처리를 피하기 위해 기술 담당 확인 후 재시도한다. |

## 7) 검증·출처

**브라우저 검증(2026-11-09)**: 진입 미재현. 목록·기간·회사명 조건에서 상세 진입 가능한 테스트 행을 확보하지 못함. 임의 ID 사용·데이터 생성은 하지 않음. [경로별 결과와 제한](../../references/browser-verification.md#page032). 역할별 권한 거부·저장 성공·파일 반출·외부 연계 완료는 이 결과로 보장하지 않는다.

| 검증 항목 | 근거·환경 | 상태·확인일 |
|---|---|---|
| 대상 선정 | 사용자가 WBS 탭 내용으로 제공한 텍스트의 No. 117, 118; [선정 태스크](../../inventory/wbs-tasks.csv) | 제공 텍스트 확인 2026-11-09. 원본 Excel의 탭/병합 셀을 독립 재열람한 것은 아님. |
| 메뉴·라우트·화면 | [menuConfig.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts); [BondServiceRoutes.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/BondServiceRoutes.tsx); [ReceivableBalanceTransferDetail.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/service/bondservice/ReceivableBalanceTransferDetail.tsx) | 코드 확인 2026-11-09, 기준 dc216b313 |
| 기능·권한·API | 이 문서의 API 계약 링크 및 연결 Hook/API·Controller·DTO·Service·Repository·Mapper | 코드 확인 2026-11-09. 조회 요청·화면 대조 범위는 아래 브라우저 근거 참조. 권한 계정별 허용·거부 및 변경 요청 실행은 미확인. |
| DB 정의 | [개발 DB 계약](../../references/database-contracts.md), 이 문서의 연결 객체 | 개발 DB 정의 확인 2026-11-09. 동적 SQL·CLR 내부·정의 미공개 참조의 미확정 범위는 객체별 기록; 후속 확인 DB 담당. |
| 브라우저 화면·배포 환경 | 로컬 인증 계정·Playwright CLI; [화면별 검증표](../../references/browser-verification.md#page032) | 진입 미재현, 2026-11-09. 배포본·타 역할·업무 변경 결과는 미확인. |
| 업무 프로시저·쓰기·외부 결과 | 격리된 검증 환경·테스트 데이터의 실행 결과 | 미확인: 명시적인 저장·삭제·발송·초기화 요청은 실행하지 않음. 브라우저 GET의 업무 조회 프로시저·조회수·감사 기록은 별도 영향으로 구분. 격리 환경에서 기술 담당 확인. |

코드 확인과 DB 정의 확인은 실행 성공·업무 승인·다른 환경 적용을 보장하지 않는다. 업무·기술 담당 검토 후 조사 목록의 상태를 완료로 변경한다.

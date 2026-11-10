# [SB 고객관리] 회사 정보 (상세) 관리자 매뉴얼

작성 기준: `dc216b313` · 확인일 2026-11-09 · 조사 상태 **검토 대기**. 코드·개발 DB 정의 확인. 브라우저: **화면 대조**; 저장·발송 등 업무 실행 결과는 미검증이다.

## 1) 화면 기본 정보

### 도메인 이해

선택한 스마트빌 회사의 현재 정보와 서비스 설정을 한 회사 범위에서 확인·관리한다.

| 구분 | 설명 |
|---|---|
| 업무 영역 | 스마트빌 회사·회원 관리 > 회사 정보 상세 |
| 언제 사용하는가 | 회사 목록에서 문의 업체를 식별한 뒤 설정·관리자·미납 관련 내용을 더 조사할 때 |
| 주요 대상·데이터 | 회사명·사업자번호·관리자 정보, 세금계산서 전송·전자계약 등 서비스 설정이 대상이다. |
| 업무 흐름 | 회사 식별 확인 → 현재 설정·상태 확인 → 필요한 설정 작업 또는 회원·권한·이력 선택 |
| 이 페이지의 역할 | 회사 정보 중 **회사 정보 상세** 단계. 선택한 스마트빌 회사의 현재 정보와 서비스 설정을 한 회사 범위에서 확인·관리한다. |
| 판단 결과·다음 업무 | 설정과 문제 증상을 대조하고, 개인 문제는 소속 회원·권한으로, 변경 원인 조사는 변경 이력으로 이어간다. |
| 다른 화면과의 구분 | 회사 목록은 대상을 찾는 곳이고 이 상세는 선택 회사의 설정을 보는 곳이다. 조회와 실제 설정 저장을 구분한다. |

설명 근거: [CompanyInfoDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/pages/CompanyInfoDetailPage.tsx), 이 문서 4·5·7번의 항목·API·업무 규칙. [상위 업무 영역](../../references/domain-overview.md#company)은 공통 배경이며 현재 화면의 데이터·동작은 위 설명을 따른다. 설명 수정일 **2026-11-10**; 새 업무 실행 검증을 수행한 것은 아니다.

### 화면 정보

| 항목 | 작성 내용 |
|---|---|
| 업무 도메인·목적 | 선택한 스마트빌 회사의 현재 정보와 서비스 설정을 한 회사 범위에서 확인·관리한다. |
| 메뉴·화면 경로 | SB 고객관리 > 스마트빌 회원·회사정보 관리 > 회사 정보; `/company-management/company-info/:id`; 목록에서 선택한 대상의 경로 변수를 유지하여 진입한다. |
| 화면 유형·담당 | 상세; WBS 작업자 유지윤. 업무·기술 담당 팀명은 원문에 없어 배포 전 해당 도메인 담당자가 확정한다. |
| 관련 화면 | [조회·관리](company-info.md); [변경 이력](company-info__by-id__change-history.md); [전체 회원 조회](company-info__by-companyId__members.md); [회원 권한 조회](company-info__by-companyKey__member-permissions.md) |

WBS 근거: No. 17, 18, 19, 20, 21, 22, 23, 24 (사용자가 제공한 텍스트 행 36, 37, 38, 39, 40, 41, 42, 43). API 개발/화면 개발의 중복 행은 같은 화면으로 통합했다.

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
|---|---|---|
| 화면 진입·조회 | `/company-management/company-info` 메뉴 접근·하위 경로 작업 권한. 조회 API는 VIEW, 등록/수정 경로는 PROCESS 등 아래 서버 액션과 라우트 가드를 함께 적용한다. | 로그인된 관리자 계정; id 식별자는 이전 화면에서 선택한다. |
| 회사정보 변경내역 | `/company-management/company-info`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 목록 | `/company-management/company-info`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 등록 | `/company-management/company-info`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 삭제 | `/company-management/company-info`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 변경 | `/company-management/company-info`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 저장 | `/company-management/company-info`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 취소 | `/company-management/company-info`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 자동이체 이력 조회 | `/company-management/company-info`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 회사 관리자 변경 | `/company-management/company-info`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 전체 회원 조회 | `/company-management/company-info`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |
| 회원 권한 조회 | `/company-management/company-info`; 화면 조건에 따라 표시·활성화된다. 아래 API별 서버 권한을 확인한다. | 작업 대상과 현재 상태·변경 내용을 확인한다. |

서버가 최종 권한을 검사한다. 버튼 모양(kind)으로 권한을 추정하지 않는다. 특히 등록·수정이 PROCESS를 사용하는 API와 EXECUTE·UNMASK·EXCEL_DOWNLOAD는 서로 구분한다.

## 3) 화면 사용 절차

**검증 시 화면 버튼**: 회사정보 변경내역, 접기, 등록 (비활성), 등록, 펼치기, 자동이체 이력 조회, 회사 관리자 변경, 전체 회원 조회, 회원 권한 조회, 목록. 화면 상태·대상에 따라 달라지며 아래 작업 절차와 권한 조건을 함께 확인한다.

1. 관련 화면에서 대상 또는 작업을 선택하여 `/company-management/company-info/:id`로 이동한다. 경로 변수는 주소에서 임의로 바꾸지 않고 이전 화면이 전달한 식별자를 사용한다.
2. 대상의 기본 정보·상태·표시 항목을 확인한다. 목록의 식별자와 상세 대상이 일치하는지 확인한다.
3. **회사정보 변경내역, 등록, 삭제, 변경, 저장, 자동이체 이력 조회, 회사 관리자 변경, 전체 회원 조회, 회원 권한 조회** 중 필요한 작업을 선택한다. 버튼의 표시·활성 조건과 아래 API별 권한을 확인한다. 저장·삭제·외부 호출 전에는 대상과 현재 상태를 재확인한다.
4. 작업 결과 또는 다운로드 파일을 확인하고 관련 목록으로 돌아가 변경된 상태를 다시 조회한다.

**이 화면에서 유의할 업무 규칙**: 진입 시 자동조회하지 않는다. 업체 조건 또는 가입일 기간 중 하나 이상을 입력하고 검색한다. 회사 상세에서는 SSO·WEB-HOOK·요금제 변경내역·자동이체 이력 팝업과 전체 회원·회원 권한·회사정보 변경내역 화면을 구분하여 사용한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
|---|---|---|---|
| 익일 자동전송 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `nextDay`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/NtsTransmissionSettingsSection.tsx#L160) |
| 발급즉시 전송 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `immediate`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/NtsTransmissionSettingsSection.tsx#L164) |
| 전송안함 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `none`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/NtsTransmissionSettingsSection.tsx#L168) |
| 서버 검증 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `cert-server`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/IntegrationServiceSettingsSection.tsx#L280) |
| 클라이언트 검증 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `cert-client`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/IntegrationServiceSettingsSection.tsx#L286) |
| 회사명 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/SsoRegistrationDialog.tsx#L153) |
| 사업자번호 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/SsoRegistrationDialog.tsx#L157) |
| 관리자 ID | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/SsoRegistrationDialog.tsx#L179) |
| 관리자명 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/SsoRegistrationDialog.tsx#L192) |
| UNIQUE_KEY | 입력·선택(조건부 검증 별도) | 길이·형식·조건부 필수는 검증 코드와 API DTO 참조 | `uniqueKey`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/SsoRegistrationDialog.tsx#L214) |
| MENU_CALLER | 입력·선택(조건부 검증 별도) | 길이·형식·조건부 필수는 검증 코드와 API DTO 참조 | `menuCaller`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/SsoRegistrationDialog.tsx#L222) |
| SYSTEM_CODE | 입력·선택(조건부 검증 별도) | 길이·형식·조건부 필수는 검증 코드와 API DTO 참조 | `systemCode`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/SsoRegistrationDialog.tsx#L230) |
| DEFAULT_URL | 입력·선택(조건부 검증 별도) | 길이·형식·조건부 필수는 검증 코드와 API DTO 참조 | `defaultUrl`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/SsoRegistrationDialog.tsx#L242) |
| ENCRYPTION_VALUE | 입력·선택(조건부 검증 별도) | 길이·형식·조건부 필수는 검증 코드와 API DTO 참조 | `encryptionValue`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/SsoRegistrationDialog.tsx#L252) |
| AUTH_OPTION | 입력·선택(조건부 검증 별도) | 길이·형식·조건부 필수는 검증 코드와 API DTO 참조 | `authOption`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/SsoRegistrationDialog.tsx#L260) |
| 업체명 / 사업자번호 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/WebhookRegistrationDialog.tsx#L267) |
| 관리자 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/WebhookRegistrationDialog.tsx#L288) |
| 서비스 기간 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/WebhookRegistrationDialog.tsx#L320) |
| 무기한 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `unlimited`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/WebhookRegistrationDialog.tsx#L361) |
| 라우팅 URL | 입력·선택(조건부 검증 별도) | 길이·형식·조건부 필수는 검증 코드와 API DTO 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/WebhookRegistrationDialog.tsx#L371) |
| CONTEXT / PORT | 입력·선택(조건부 검증 별도) | 길이·형식·조건부 필수는 검증 코드와 API DTO 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/WebhookRegistrationDialog.tsx#L387) |
| Context: | 입력·선택(조건부 검증 별도) | 길이·형식·조건부 필수는 검증 코드와 API DTO 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/WebhookRegistrationDialog.tsx#L392) |
| Port: | 입력·선택(조건부 검증 별도) | 길이·형식·조건부 필수는 검증 코드와 API DTO 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/WebhookRegistrationDialog.tsx#L401) |
| 사용여부 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/WebhookRegistrationDialog.tsx#L414) |
| 변경일시 | 출력 | API 타입 String | `changeDate`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/PricingPlanHistoryDialog.tsx#L90) |
| 요금제 | 출력 | API 타입 String | `pricingPlan`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/PricingPlanHistoryDialog.tsx#L91) |
| 사용기간 | 출력 | API 타입 String | `usagePeriod`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/PricingPlanHistoryDialog.tsx#L92) |
| 변경 담당자 | 출력 | API 타입 String | `changedBy`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/PricingPlanHistoryDialog.tsx#L93) |
| 충전일자 | 출력 | API 타입 String | `prepayDate`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/PrepayHistoryDialog.tsx#L61) |
| 충전금액 | 출력 | API 타입 Long | `prepayAmount`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/PrepayHistoryDialog.tsx#L62) |
| 이월금액 | 출력 | API 타입 Long | `carryoverAmount`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/PrepayHistoryDialog.tsx#L66) |
| 사용가능금액 | 출력 | API 타입 Long | `principalAmount`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/PrepayHistoryDialog.tsx#L70) |
| 사용한 금액 | 출력 | API 타입 Long | `useAmount`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/PrepayHistoryDialog.tsx#L74) |
| 입금방법 | 출력 | API 타입 String | `payMethod`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/PrepayHistoryDialog.tsx#L78) |
| 입금자 | 출력 | API 타입 String | `charger`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/PrepayHistoryDialog.tsx#L79) |
| 소멸 금액 | 출력 | API 타입 Long | `lapseAmount`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/PrepayHistoryDialog.tsx#L91) |
| 비고 | 출력 | API 타입 String | `remark`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/PrepayHistoryDialog.tsx#L95) |
| 자동이체 신청일 | 출력 | API 타입 String | `applicationDate`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CmsHistoryDialog.tsx#L37) |
| 주민/사업자 번호 | 출력 | API 타입 String | `residentOrBusinessNumber`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CmsHistoryDialog.tsx#L42) |
| 계좌 정보 | 출력 | API 타입 String | `accountInfo`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CmsHistoryDialog.tsx#L56) |
| 신청자 | 출력 | API 타입 String | `applicant`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CmsHistoryDialog.tsx#L73) |
| 상태/서명값 | 출력 | API 타입 String | `status`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CmsHistoryDialog.tsx#L87) |
| 종류 | 출력 | 원천 값의 형식·정렬·빈값 처리는 표시 코드 참조 | `role`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CompanyAdministratorSection.tsx#L134) |
| 실명 | 출력 | API 타입 String | `realName`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CompanyAdministratorSection.tsx#L141) |
| 닉네임 | 출력 | API 타입 String | `nickname`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CompanyAdministratorSection.tsx#L147) |
| 아이디 | 출력 | API 타입 String | `userId`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CompanyAdministratorSection.tsx#L153) |
| 연락처 | 출력 | API 타입 String | `phone`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CompanyAdministratorSection.tsx#L159) |
| 핸드폰 | 출력 | API 타입 String | `mobile`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CompanyAdministratorSection.tsx#L165) |
| 이메일 | 출력 | API 타입 String | `email`; [화면 필드 근거](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CompanyAdministratorSection.tsx#L171) |

입력 검증 근거: [TaxInvoiceSettingsSection.rules.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/customer/company/components/TaxInvoiceSettingsSection.rules.ts), [NtsTransmissionSettingsSection.schema.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/customer/company/components/NtsTransmissionSettingsSection.schema.ts), [EContractSettingsSection.schema.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/customer/company/components/EContractSettingsSection.schema.ts), [OtherManagementSettingsSection.schema.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/customer/company/components/OtherManagementSettingsSection.schema.ts), [IntegrationServiceSettingsSection.schema.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/customer/company/components/IntegrationServiceSettingsSection.schema.ts), [SsoRegistrationDialog.schema.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/customer/company/components/SsoRegistrationDialog.schema.ts), [WebhookRegistrationDialog.rules.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/shared/utils/validation/forms/customer/company/components/WebhookRegistrationDialog.rules.ts). 프런트 검증과 서버 DTO 제약이 다르면 서버 검증이 최종 기준이다.

**복합 검색·폼의 초기 상태**

| 초기값 근거 | 기본 상태 |
|---|---|
| [defaultValues](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/WebhookRegistrationDialog.tsx#L63) | serviceStartDate={new Date()}; serviceEndDate={new Date(now.getFullYear() + 1, now.getMonth(), now.getDate())}; unlimitedPeriod=꺼짐; routingUrl=빈값; context=빈값; port=빈값; inUse=꺼짐 |

화면 필드 키와 API 필드명이 다른 경우 변환은 Hook/API의 검색·저장 매핑에서 수행된다. 요청·응답 필드와 DB 컬럼 매핑은 아래 API 계약 및 DB 객체 계약에 연결했다.

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
|---|---|---|---|
| 회사 정보 상세 조회 | [GET /api/v1/company-management/company-info/{id}](../../references/api-contracts.md#api055); `/company-management/company-info` / `VIEW` | `경로·쿼리·본문 계약 참조` → `id, basicInfo, businessStatus, certificateAndSeal, migrationInfo, taxInvoiceSettings, ntsTransmissionSettings, eContractSettings, otherManagementSettings, integrationServiceSetting` | Mapper 프로시저의 정적 테이블 쓰기 미검출; 동적 SQL의 런타임 대상은 미확정 |
| CMS 자동이체 이력 조회 | [GET /api/v1/company-management/company-info/{companyId}/cms-history](../../references/api-contracts.md#api047); `/company-management/company-info` / `VIEW` | `경로·쿼리·본문 계약 참조` → `content, totalElements, totalPages, page, size, id, applicationDate, residentOrBusinessNumber, accountInfo, applicant, status, signatureValue, revealKey, bankName, accountNumber` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 회사 직인 삭제 | [DELETE /api/v1/company-management/company-info/{companyId}/seal](../../references/api-contracts.md#api002); `/company-management/company-info` / `DELETE` | `경로·쿼리·본문 계약 참조` → `응답 DTO·파일/처리 결과 계약 참조` | 쓰기 대상 smartbill3.dbo.company |
| 회사 직인 이미지 조회 | [GET /api/v1/company-management/company-info/{companyId}/seal](../../references/api-contracts.md#api051); `/company-management/company-info` / `VIEW` | `경로·쿼리·본문 계약 참조` → `응답 DTO·파일/처리 결과 계약 참조` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| SSO 정보 조회 | [GET /api/v1/company-management/company-info/{companyId}/sso](../../references/api-contracts.md#api052); `/company-management/company-info` / `VIEW` | `경로·쿼리·본문 계약 참조` → `응답 DTO·파일/처리 결과 계약 참조` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| SSO 정보 등록/수정 | [POST /api/v1/company-management/company-info/{companyId}/sso](../../references/api-contracts.md#api207); `/company-management/company-info` / `PROCESS` | `경로·쿼리·본문 계약 참조` → `응답 DTO·파일/처리 결과 계약 참조` | 쓰기 대상 sb_common.dbo.sso_info, smartwork.dbo.company_change_log |
| Webhook 정보 조회 | [GET /api/v1/company-management/company-info/{companyId}/webhook](../../references/api-contracts.md#api053); `/company-management/company-info` / `VIEW` | `경로·쿼리·본문 계약 참조` → `응답 DTO·파일/처리 결과 계약 참조` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| Webhook 정보 등록/수정 | [POST /api/v1/company-management/company-info/{companyId}/webhook](../../references/api-contracts.md#api209); `/company-management/company-info` / `PROCESS` | `경로·쿼리·본문 계약 참조` → `응답 DTO·파일/처리 결과 계약 참조` | 쓰기 대상 sb_dti_log.dbo.oapi_webhook_company_link_info, smartwork.dbo.company_change_log |
| 요금제 변경내역 조회 | [GET /api/v1/company-management/company-info/{companyId}/pricing-plan-history](../../references/api-contracts.md#api050); `/company-management/company-info` / `VIEW` | `경로·쿼리·본문 계약 참조` → `content, totalElements, totalPages, page, size, id, serviceType, changeDate, pricingPlan, usagePeriod, changedBy, revealKey` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 충전 내역 조회 | [GET /api/v1/company-management/company-info/{companyId}/prepay-history](../../references/api-contracts.md#api049); `/company-management/company-info` / `VIEW` | `경로·쿼리·본문 계약 참조` → `content, totalElements, prepayDate, prepayAmount, carryoverAmount, principalAmount, useAmount, payMethod, charger, lapseAmount, remark, prepayNo` | Mapper 프로시저의 정적 테이블 쓰기 미검출 |
| 회원 민감정보 원문 조회 | [POST /api/v1/members/{memNo}/sensitive-values/reveal](../../references/api-contracts.md#api221); `/member-management/member` / `UNMASK` | `field` → `field, value` | 쓰기 대상 smartwork.dbo.sw_log_access_event |
| 회사 관리자 민감정보 원문 조회 | [POST /api/v1/company-management/company-info/{comNo}/administrators/{memNo}/sensitive-values/reveal](../../references/api-contracts.md#api200); `/company-management/company-info` / `UNMASK` | `field` → `field, value` | 쓰기 대상 smartwork.dbo.sw_log_access_event |
| 세금계산서 설정 변경 | [PUT /api/v1/company-management/company-info/{companyId}/tax-invoice-settings](../../references/api-contracts.md#api264); `/company-management/company-info` / `PROCESS` | `field, value, field` → `success, data, error, content, totalElements, totalPages, page, size, changeDateTime, companyName, presidentName, businessStatus, businessClass, address, certDn, sealFileName, fiel` | 쓰기 대상 sb_dti.dbo.company_dticonfig, smartwork.dbo.company_change_log |
| 국세청 전송 설정 변경 | [PUT /api/v1/company-management/company-info/{companyId}/nts-transmission-settings](../../references/api-contracts.md#api262); `/company-management/company-info` / `PROCESS` | `field, value, field` → `success, data, error, content, totalElements, totalPages, page, size, changeDateTime, companyName, presidentName, businessStatus, businessClass, address, certDn, sealFileName, fiel` | 쓰기 대상 sb_dti.dbo.company_dticonfig, sb_dti.dbo.nts_transmit_method, sb_dti.dbo.nts_transmit_method_his, smartwork.dbo.company_change_log |
| 전자계약 설정 변경 | [PUT /api/v1/company-management/company-info/{companyId}/e-contract-settings](../../references/api-contracts.md#api260); `/company-management/company-info` / `PROCESS` | `field, value, field` → `success, data, error, content, totalElements, totalPages, page, size, changeDateTime, companyName, presidentName, businessStatus, businessClass, address, certDn, sealFileName, fiel` | 쓰기 대상 smartbill3.dbo.dct_company_config, smartbill3.dbo.dct_multi_use, smartwork.dbo.company_change_log |
| 연동서비스 설정 변경 | [PUT /api/v1/company-management/company-info/{companyId}/integration-service-settings](../../references/api-contracts.md#api261); `/company-management/company-info` / `PROCESS` | `field, value, field` → `success, data, error, content, totalElements, totalPages, page, size, changeDateTime, companyName, presidentName, businessStatus, businessClass, address, certDn, sealFileName, fiel` | 쓰기 대상 sb_dti.dbo.company_dticonfig, smartbill3.dbo.company_exception, smartwork.dbo.company_change_log |
| 기타 관리 정보 변경 | [PUT /api/v1/company-management/company-info/{companyId}/other-management-settings](../../references/api-contracts.md#api263); `/company-management/company-info` / `PROCESS` | `field, value, field` → `success, data, error, content, totalElements, totalPages, page, size, changeDateTime, companyName, presidentName, businessStatus, businessClass, address, certDn, sealFileName, fiel` | 쓰기 대상 sb_dti.dbo.company_dticonfig, smartwork.dbo.company_change_log |
| 회사 등록번호 원문 조회 | [POST /api/v1/company-management/company-info/{comNo}/sensitive-values/reveal](../../references/api-contracts.md#api203); `/company-management/company-info` / `UNMASK` | `field` → `field, value` | 쓰기 대상 smartwork.dbo.sw_log_access_event |
| 충전 내역 입금자 원문 조회 | [POST /api/v1/company-management/company-info/{companyId}/prepay-history/{prepayNo}/sensitive-values/reveal](../../references/api-contracts.md#api206); `/company-management/company-info` / `UNMASK` | `field` → `field, value` | 쓰기 대상 smartwork.dbo.sw_log_access_event |
| 자동이체 신청자 원문 조회 | [POST /api/v1/company-management/company-info/{comNo}/auto-payment/sensitive-values/reveal](../../references/api-contracts.md#api201); `/company-management/company-info` / `UNMASK` | `field` → `field, value` | 쓰기 대상 smartwork.dbo.sw_log_access_event |
| 회사 자동이체 계좌 원문 조회 | [POST /api/v1/company-management/company-info/{comNo}/accounts/{accountId}/sensitive-values/reveal](../../references/api-contracts.md#api199); `/company-management/company-info` / `UNMASK` | `field` → `field, value` | 쓰기 대상 smartwork.dbo.sw_log_access_event |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
|---|---|---|---|
| [smartwork.dbo.UspCompanyMaintenanceBilling_Select](../../references/database-contracts.md#db321) | `@COM_NO int IN` | 확정한 테이블 쓰기 없음. 참조: sb_bill.dbo.usecount_step3 | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DTI.dbo.NTS_TRANSMIT_METHOD](../../references/database-contracts.md#db143) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: sb_dti.dbo.nts_transmit_method | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DTI.dbo.COMPANY_MNG_INFO](../../references/database-contracts.md#db137) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: sb_dti.dbo.company_mng_info | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.COMPANY_TAX_INVOICE_EXT](../../references/database-contracts.md#db268) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: smartwork.dbo.company_tax_invoice_ext | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.COMPANY_UNIT_TAXATION_CONFIG](../../references/database-contracts.md#db269) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: smartwork.dbo.company_unit_taxation_config | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SMARTBILL3.dbo.DCT_COMPANY_CONFIG](../../references/database-contracts.md#db199) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.dct_company_config | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SMARTBILL3.dbo.DCT_MULTI_USE](../../references/database-contracts.md#db200) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.dct_multi_use | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SMARTBILL3.dbo.COMPANY](../../references/database-contracts.md#db197) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.company | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DTI.dbo.COMPANY_DTICONFIG](../../references/database-contracts.md#db135) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 쓰기: sb_dti.dbo.company_dticonfig. 참조: sb_dti.dbo.company_dticonfig | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SMARTBILL3.dbo.upGW_CompanyException_Info](../../references/database-contracts.md#db254) | `@COM_NO varchar(10) IN` | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.company_exception | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DTI_LOG.dbo.upWebHook_SELECT_COMPANY_LINK_INFO_USER](../../references/database-contracts.md#db167) | `@COM_REGNO varchar(10) IN` | 확정한 테이블 쓰기 없음. 참조: sb_dti_log.dbo.oapi_webhook_company_link_info, smartbill3.dbo.company | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Office.dbo.upGW_OrganSupport_Select](../../references/database-contracts.md#db031) | `@COM_REGNO varchar(10) IN` | 확정한 테이블 쓰기 없음. 참조: sb_common.dbo.sso_info | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Office.dbo.UPGW_SERVERCERTIYN](../../references/database-contracts.md#db041) | `@COM_NO int IN` | 확정한 테이블 쓰기 없음. 참조: sb_dti.dbo.company_dticonfig | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Office.dbo.upGW_MemAdminInfo4](../../references/database-contracts.md#db027) | `@comId varchar(10) IN` | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.company, smartbill3.dbo.dept_manager, smartbill3.dbo.member | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Office.dbo.upGW_MemAdminInfo3](../../references/database-contracts.md#db026) | `@com_no int IN` | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.member, smartbill3.dbo.tax_admin | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Office.dbo.upGW_MemAdminInfo2](../../references/database-contracts.md#db025) | `@service_type varchar(3) IN, @com_no int IN` | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.company, smartbill3.dbo.dept_manager, smartbill3.dbo.member | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_COMMON.dbo.upSBAdm_LstDeptMng](../../references/database-contracts.md#db101) | `@DIVISION varchar(3) IN, @COM_NO varchar(10) IN, @DEPT_NO varchar(10) IN` | 확정한 테이블 쓰기 없음. 참조: sb_dti.dbo.dept_admin, sb_dti.dbo.dept_member, sb_dti.dbo.service_admin, smartbill3.dbo.member | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Office.dbo.upGW_MemAdminInfo1](../../references/database-contracts.md#db024) | `@com_no int IN` | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.company, smartbill3.dbo.member | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SmartBill3.dbo.upAdmSB_SchCREDITACCOUNT](../../references/database-contracts.md#db247) | `@COM_NO int IN` | 확정한 테이블 쓰기 없음. 참조: sb_bill.dbo.cardbilling_auth, smartbill3.dbo.member | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SMARTBILL3.dbo.upAdmSB_SchCMSAccount](../../references/database-contracts.md#db244) | `@com_no int IN` | 확정한 테이블 쓰기 없음. 참조: sb_bill.dbo.bill_common_code, smartbill3.dbo.cms_account, smartbill3.dbo.cms_account_cub, smartbill3.dbo.cms_account_eb11, smartbill3.dbo.cms_account_eb11_cub, smartbill3.dbo.member | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SMARTBILL3.dbo.upMem_CfmPrepayAmt](../../references/database-contracts.md#db257) | `@com_no no IN` | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.service_prepay 동적 SQL 포함, 런타임 조합 대상 미확정. | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SMARTBILL3.dbo.upMem_CfmInvAmt](../../references/database-contracts.md#db256) | `@com_no no IN` | 확정한 테이블 쓰기 없음. 참조: sb_bill.dbo.invoice, sb_bill.dbo.payment, smartbill3.dbo.sum_invoice 동적 SQL 포함, 런타임 조합 대상 미확정. | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Office.dbo.upCOM_HubName](../../references/database-contracts.md#db015) | `@COM_NO int IN` | 확정한 테이블 쓰기 없음. 참조: office.dbo.business, office.dbo.mng_hub, office.dbo.mng_hub_detail, smartbill3.dbo.company | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Office.dbo.upMem_LstSettle](../../references/database-contracts.md#db048) | `@service_type varchar(3) IN, @com_no int IN` | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.company, smartbill3.dbo.settlement | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SmartBill3.dbo.COMPANY](../../references/database-contracts.md#db197) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.company | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DTI.dbo.COMPANY_QUIT_STATUS](../../references/database-contracts.md#db138) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: sb_dti.dbo.company_quit_status | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Office.dbo.upGW_CompanyINFO](../../references/database-contracts.md#db018) | `@COM_NO varchar(10) IN` | 확정한 테이블 쓰기 없음. 참조: migration_etcasp.dbo.migration_mapping_company, smartbill3.dbo.company, smartbill3.dbo.member | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SMARTBILL3.dbo.upCMS_LstEachCMS](../../references/database-contracts.md#db251) | `@COM_NO int IN` | 확정한 테이블 쓰기 없음. 참조: sb_bill.dbo.bill_common_code, smartbill3.dbo.cms_account, smartbill3.dbo.cms_account_cub, smartbill3.dbo.cms_account_eb11, smartbill3.dbo.cms_account_eb11_cub, smartbill3.dbo.cms_withdrawal_agreement, smartbill3.dbo.member | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SMARTBILL3.dbo.upMem_DelComSeal](../../references/database-contracts.md#db258) | `@com_no int IN` | 쓰기: smartbill3.dbo.company. 참조: smartbill3.dbo.company | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [Office.dbo.upGW_OrganSupport_Regist](../../references/database-contracts.md#db030) | `@SERVICE_NAME varchar(100) IN, @COM_REGNO varchar(10) IN, @UNIQUE_KEY varchar(100) IN, @STATUS int IN, @DEFAULT_URL varchar(100) IN, @MENU_CALLER varchar(20) IN, @ENCRYPTION_VALUE varchar(100) IN, @SYSTEM_CODE varchar(10) IN, @AUTH_OPTION varchar(1) IN` | 쓰기: sb_common.dbo.sso_info. 참조: sb_common.dbo.sso_info, smartbill3.dbo.company, smartbill3.dbo.member | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.COMPANY_CHANGE_LOG](../../references/database-contracts.md#db267) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 쓰기: smartwork.dbo.company_change_log. 참조: smartwork.dbo.company_change_log | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DTI_LOG.dbo.upWebHook_SAVE_COMPANY_LINK_INFO_ADMIN](../../references/database-contracts.md#db166) | `@COM_NO int IN, @ROUTINGURL varchar(100) IN, @PORT varchar(5) IN, @CONTEXT varchar(100) IN, @STARTROUTINGDATE varchar(10) IN, @ENDROUTINGDATE varchar(10) IN, @ACTIVE_YN varchar(1) IN, @BIZ_USER varchar(12) IN, @ERR_CODE varchar(5) OUT` | 쓰기: sb_dti_log.dbo.oapi_webhook_company_link_info. 참조: sb_dti_log.dbo.oapi_webhook_company_link_info, smartbill3.dbo.company | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SMARTBILL3.dbo.upMem_LstSettleHis](../../references/database-contracts.md#db261) | `@service_type varchar(3) IN, @com_no no IN` | 확정한 테이블 쓰기 없음. 참조: sb_bill.dbo.package_fee_mapping, sb_bill.dbo.package_fee_mapping_history, smartbill3.dbo.member, smartbill3.dbo.settlement, smartbill3.dbo.settlement_history | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SmartBill3.dbo.upMem_LstPrePay2](../../references/database-contracts.md#db260) | `@com_no no IN, @fromdate varchar(8) IN, @todate varchar(8) IN` | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.member, smartbill3.dbo.service_prepay, smartbill3.dbo.service_prepay_his | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [smartwork.dbo.usp_sw_log_access_event_insert](../../references/database-contracts.md#db294) | `@EVENT_TYPE varchar(30) IN, @STATUS varchar(20) IN, @USER_ID bigint IN, @MEMBER_ID nvarchar(50) IN, @USER_NAME nvarchar(100) IN, @DEPARTMENT_NAME nvarchar(100) IN, @PAGE_TITLE nvarchar(200) IN, @PATH nvarchar(500) IN, @MENU_PATH nvarchar(500) IN, @MENU_LABEL nvarchar(200) IN, @CATEGORY_NAME nvarchar(200) IN, @SUB_CATEGORY_NAME nvarchar(200) IN, @MENU_ORDER int IN, @IP_ADDRESS varchar(45) IN, @USER_AGENT nvarchar(1000) IN, @BROWSER varchar(100) IN, @OS varchar(100) IN, @REFERRER nvarchar(500) IN, @DETAIL nvarchar(1000) IN, @RESULT int OUT, @COUNTS_AS_VISIT bit IN` | 쓰기: smartwork.dbo.sw_log_access_event. 참조: smartwork.dbo.sw_log_access_event | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SMARTBILL3.dbo.MEMBER](../../references/database-contracts.md#db203) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.member | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DTI.dbo.SERVICE_ADMIN](../../references/database-contracts.md#db144) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: sb_dti.dbo.service_admin | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SMARTBILL3.dbo.DEPT_MANAGER](../../references/database-contracts.md#db201) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.dept_manager | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SMARTBILL3.dbo.TAX_ADMIN](../../references/database-contracts.md#db209) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.tax_admin | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SB_DTI.dbo.upMg_Save_AutoNtsTransmitInfo](../../references/database-contracts.md#db147) | `@MEM_NO int IN, @TRANSMIT_METHOD varchar(1) IN, @TRANSMIT_DAY varchar(1) IN, @AUTO_TRANSMIT_YN varchar(1) IN, @ISSUE_STATUS_YN varchar(1) IN, @ERROR_CODE int OUT` | 쓰기: sb_dti.dbo.nts_transmit_method, sb_dti.dbo.nts_transmit_method_his. 참조: sb_dti.dbo.company_link_in, sb_dti.dbo.company_link_out, sb_dti.dbo.neobill_company_link_in, sb_dti.dbo.neobill_company_link_out, sb_dti.dbo.nts_transmit_method, sb_dti.dbo.nts_transmit_method_his, sb_dti.dbo.service_admin | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SMARTBILL3.dbo.upDCT_SavDctDefaultDisk](../../references/database-contracts.md#db253) | `@COM_NO int IN, @DEFAULT_DISK int IN, @ATTACHFILE_DEL_YN char(1) IN, @ATTACHFILE_LIMIT_SIZE int IN` | 쓰기: smartbill3.dbo.dct_company_config. 참조: smartbill3.dbo.dct_company_config | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SMARTBILL3.dbo.upDCT_MultiUse_YN](../../references/database-contracts.md#db252) | `@COM_NO int IN, @USE_YN char(1) IN` | 쓰기: smartbill3.dbo.dct_multi_use. 참조: smartbill3.dbo.dct_multi_use | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SMARTBILL3.dbo.upGW_CompanyException_Info_Reg](../../references/database-contracts.md#db255) | `@COM_NO varchar(10) IN, @USE_YN char(1) IN, @USER int IN, @EXCEPT_CODE varchar(50) IN` | 쓰기: smartbill3.dbo.company_exception. 참조: smartbill3.dbo.company_exception | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SmartBill3.dbo.CMS_ACCOUNT](../../references/database-contracts.md#db190) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.cms_account, smartbill3.dbo.cms_account_cub | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| [SmartBill3.dbo.CMS_ACCOUNT_EB11](../../references/database-contracts.md#db191) | 직접 테이블/뷰 사용. 컬럼·Mapper 바인딩은 연결 계약 참조 | 확정한 테이블 쓰기 없음. 참조: smartbill3.dbo.cms_account_eb11, smartbill3.dbo.cms_account_eb11_cub | 개발 DB 정의 확인 2026-11-09; 결과 컬럼·RETURN·하위 호출은 연결 계약 참조 |
| 파일: storage.comseal | DB 직인 경로와 설정 루트 | 직인 이미지를 읽거나 삭제한다. 실제 파일·경로 정규화와 작업 권한 확인 | [StorageProperties.kt](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/shared/upload/config/StorageProperties.kt) |

위 DB 계약 링크에는 실제 파라미터 타입·기본값·IN/OUT, Mapper 결과 컬럼, RETURN 바인딩, 참조 테이블·하위 프로시저·정의 필터/정렬을 기록했다. DTO·Service·Repository·Mapper의 상세 호출 경로는 각 API 계약에서 확인한다.

**민감정보**: 기본 응답의 마스킹 값을 유지한다. 원문은 전용 reveal API와 UNMASK 등 추가 권한·사유·감사 로그를 확인한 뒤 조회한다. 화면·캡처·문의 문서에 원문을 남기지 않는다.

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
|---|---|---|
| 요금제 변경내역이 없습니다. | [문구·처리 코드](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/PricingPlanHistoryDialog.tsx#L120); 현재 조건·대상·권한 확인 | 검색·조회 오류면 조건을 확인 후 재조회. 변경·발송 결과가 불명확하면 처리 여부와 이력을 확인한 뒤 재시도 여부를 판단한다. |
| 충전 내역이 없습니다. | [문구·처리 코드](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/PrepayHistoryDialog.tsx#L114); 현재 조건·대상·권한 확인 | 검색·조회 오류면 조건을 확인 후 재조회. 변경·발송 결과가 불명확하면 처리 여부와 이력을 확인한 뒤 재시도 여부를 판단한다. |
| bank | [문구·처리 코드](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/AutoPaymentInfoSection.tsx#L44); 현재 조건·대상·권한 확인 | 검색·조회 오류면 조건을 확인 후 재조회. 변경·발송 결과가 불명확하면 처리 여부와 이력을 확인한 뒤 재시도 여부를 판단한다. |
| 이력이 없습니다 | [문구·처리 코드](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/components/CmsHistoryDialog.tsx#L115); 현재 조건·대상·권한 확인 | 검색·조회 오류면 조건을 확인 후 재조회. 변경·발송 결과가 불명확하면 처리 여부와 이력을 확인한 뒤 재시도 여부를 판단한다. |
| 결과가 없거나 기대 건수와 다름 | 적용된 검색 기준·기간·탭·대상 상태·서버 필터·페이징·목록/다운로드 조건 | 조건을 다시 확인하고 조회한다. 지속되면 경로·작업 시각·마스킹한 식별자·필터를 업무/기술 담당에게 전달한다. |
| 메뉴·버튼 미표시 또는 접근 거부 | 사용자 그룹의 메뉴 접근·VIEW 및 API별 PROCESS/EXECUTE/DELETE/EXCEL_DOWNLOAD/UNMASK 등 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. 프런트 버튼 표시만으로 서버 권한을 판단하지 않는다. |
| 저장·삭제·외부 실행의 결과가 불명확 | 대상 현재 상태·중복 요청·감사 이력·API 오류·파일/외부 소비 로그 | 기존 반영 여부를 먼저 조회한다. 중복 발송·초기화·금액 처리를 피하기 위해 기술 담당 확인 후 재시도한다. |

## 7) 검증·출처

**브라우저 검증(2026-11-09)**: 화면 대조. [경로별 결과와 제한](../../references/browser-verification.md#page004). 역할별 권한 거부·저장 성공·파일 반출·외부 연계 완료는 이 결과로 보장하지 않는다.

| 검증 항목 | 근거·환경 | 상태·확인일 |
|---|---|---|
| 대상 선정 | 사용자가 WBS 탭 내용으로 제공한 텍스트의 No. 17, 18, 19, 20, 21, 22, 23, 24; [선정 태스크](../../inventory/wbs-tasks.csv) | 제공 텍스트 확인 2026-11-09. 원본 Excel의 탭/병합 셀을 독립 재열람한 것은 아님. |
| 메뉴·라우트·화면 | [menuConfig.ts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts); [CustomerRoutes.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/CustomerRoutes.tsx); [CompanyInfoDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/company/pages/CompanyInfoDetailPage.tsx) | 코드 확인 2026-11-09, 기준 dc216b313 |
| 기능·권한·API | 이 문서의 API 계약 링크 및 연결 Hook/API·Controller·DTO·Service·Repository·Mapper | 코드 확인 2026-11-09. 조회 요청·화면 대조 범위는 아래 브라우저 근거 참조. 권한 계정별 허용·거부 및 변경 요청 실행은 미확인. |
| DB 정의 | [개발 DB 계약](../../references/database-contracts.md), 이 문서의 연결 객체 | 개발 DB 정의 확인 2026-11-09. 동적 SQL·CLR 내부·정의 미공개 참조의 미확정 범위는 객체별 기록; 후속 확인 DB 담당. |
| 브라우저 화면·배포 환경 | 로컬 인증 계정·Playwright CLI; [화면별 검증표](../../references/browser-verification.md#page004) | 화면 대조, 2026-11-09. 배포본·타 역할·업무 변경 결과는 미확인. |
| 업무 프로시저·쓰기·외부 결과 | 격리된 검증 환경·테스트 데이터의 실행 결과 | 미확인: 명시적인 저장·삭제·발송·초기화 요청은 실행하지 않음. 브라우저 GET의 업무 조회 프로시저·조회수·감사 기록은 별도 영향으로 구분. 격리 환경에서 기술 담당 확인. |

코드 확인과 DB 정의 확인은 실행 성공·업무 승인·다른 환경 적용을 보장하지 않는다. 업무·기술 담당 검토 후 조사 목록의 상태를 완료로 변경한다.

브라우저 직접 근거: [settled-detail-revisit](../../evidence/browser/ready-details-stable.json). 경로·고정 버튼명·입력 속성·표 머리글·API 상태를 보관했고 실제 데이터 값·식별자·인증정보는 제외했다.

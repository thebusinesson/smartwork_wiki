# [회사·회원·서비스 권한] 회원 정보 상세 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

회원번호로 회원 상세 정보를 조회한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 회사·회원·서비스 권한 |
| 언제 사용하는가 | 회원 상세 조회, 회원 서비스 이용 정보 조회, 회원 정보 수정, 법인 관리자 변경, 회원 탈퇴 처리 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 실명, 생년월일, 아이디, 닉네임, 이메일, 연락처 |
| 업무 흐름 | 회원 상세 조회, 회원 서비스 이용 정보 조회, 회원 정보 수정, 법인 관리자 변경, 회원 탈퇴 처리 |
| 이 페이지의 역할 | 상세 · 회원 상세 조회 |
| 판단 결과·다음 업무 | [회원 정보](member.md) · [회원 정보 변경 이력](member__by-id__change-history.md) · [회사 정보 상세](../company-management/company-info__by-id.md) |
| 다른 화면과의 구분 | SB 고객관리 > 스마트빌 회원·회사정보 관리 > 회원 정보에서 사용하는 상세 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 확인 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/MemberDetailPage.tsx#L494) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 회원번호로 회원 상세 정보를 조회한다. |
| 메뉴·화면 경로 | SB 고객관리 > 스마트빌 회원·회사정보 관리 > 회원 정보 · `/member-management/member/:id` · 경로 변수 `id` |
| 화면 유형·담당 | 상세 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [회원 정보](member.md) · [회원 정보 변경 이력](member__by-id__change-history.md) · [회사 정보 상세](../company-management/company-info__by-id.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/member-management/member` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `id` |
| 회원 상세 조회 | `/member-management/member` `VIEW` | `memNo: Long` |
| 회원 서비스 이용 정보 조회 | `/member-management/member` `VIEW` | `memNo: Long` |
| 회원 정보 수정 | `/member-management/member` `PROCESS` | `memNo: Long` · `MemberInfoUpdateRequest` `realName`, `dateOfBirth`, `email`, `receptionApprovalResultMail`, `marketingEmailConsent`, `marketingSmsConsent`, `marketingContactConsent` |
| 법인 관리자 변경 | `/member-management/member` `PROCESS` | `memNo: Long` |
| 회원 탈퇴 처리 | `/member-management/member` `PROCESS` | `memNo: Long` |
| 회원 민감정보 원문 조회 | `/member-management/member` `UNMASK` | `memNo: Long` · `MemberSensitiveValueRevealRequest` `field` |
| 상담용 정보 복사 | 회원 상세 화면 접근. 현재 화면에 표시된 값의 복사 | 복사할 표시값 |

코드에서 확인한 버튼·작업명은 **회원정보 변경내역**, **탈퇴 처리**, **기업관리자 변경**, **당월 사용 건수 조회**, **수정**, **회원정보 수정**, **탈퇴처리**, **목록**, **목록으로 이동**, **확인**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [회원 정보](member.md)에서 대상 또는 작업을 선택한다. `/member-management/member/:id`에서 이전 화면이 전달한 `id`와 현재 대상을 확인한다.
2. **실명**, **생년월일**, **아이디**, **닉네임**, **이메일**, **연락처**, **핸드폰** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **당월 사용 건수 조회**, **확인** 중 해당 버튼을 선택한다.
3. **회원 상세 조회** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [회원 정보 변경 이력](member__by-id__change-history.md)에서 후속 절차를 확인한다.

상담에 필요한 **실명**, **생년월일**, **아이디**, **닉네임**, **이메일**, **연락처**, **핸드폰**은 표시값 옆의 복사 버튼을 사용한다. 빈 값은 복사 버튼이 비활성화된다. 화면이 읽기 전용이어도 표시된 값은 복사할 수 있다. 클립보드 쓰기가 제한되면 수동 복사 창이 열린다. [복사 버튼과 읽기 전용 처리](https://github.com/thebusinesson/smartwork/blob/b923849c5d878772e0de2b67becff0ae511f03b3/frontend/src/feature/customer/member/components/MembershipInfoSection.tsx)

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `id` |
| 실명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/MembershipInfoSection.tsx#L121) |
| 생년월일 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/MembershipInfoSection.tsx#L135) |
| 생년월일 선택 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/MembershipInfoSection.tsx#L145) |
| 아이디 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/MembershipInfoSection.tsx#L157) |
| 닉네임 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/MembershipInfoSection.tsx#L165) |
| 이메일 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/MembershipInfoSection.tsx#L176) |
| 이메일을 입력하세요 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/MembershipInfoSection.tsx#L187) |
| 연락처 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/MembershipInfoSection.tsx#L194) |
| 핸드폰 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/MembershipInfoSection.tsx#L203) |
| 수신승인 결과 메일 설정 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/MembershipInfoSection.tsx#L215) |
| 회원 상태 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/MembershipInfoSection.tsx#L237) |
| 가입일 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/MembershipInfoSection.tsx#L253) |
| 탈퇴일 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/MembershipInfoSection.tsx#L257) |
| 회원 구분 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/MembershipInfoSection.tsx#L263) |
| 회원 종류 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/MembershipInfoSection.tsx#L268) |
| 대량 회원 가입 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/MembershipInfoSection.tsx#L283) |
| 마케팅 수신동의 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/CustomerConsentInfoSection.tsx#L45) |
| 모바일 푸쉬 동의 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/CustomerConsentInfoSection.tsx#L90) |
| 모바일 이벤트 푸쉬 동의 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/CustomerConsentInfoSection.tsx#L96) |
| 회사명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/CompanyInfoSection.tsx#L33) |
| 사업자 번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/CompanyInfoSection.tsx#L49) |
| 사업자/주민 번호 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `BUSINESS_NUMBER` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/CompanyInfoSection.tsx#L55) |
| 세금계산서 건수 (지로세금계산서 제외) | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/ServiceUsageInfoSection.tsx#L85) |
| 전자계약 건수 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/ServiceUsageInfoSection.tsx#L89) |
| 구매확인서 건수 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/ServiceUsageInfoSection.tsx#L93) |
| (부가) SMS 건수 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/ServiceUsageInfoSection.tsx#L97) |
| 채권 잔액 건수 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/ServiceUsageInfoSection.tsx#L105) |
| 전자계약 용량 사용여부 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/ServiceUsageInfoSection.tsx#L109) |
| TAX까페(SCM) 사용여부 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/ServiceUsageInfoSection.tsx#L113) |
| (부가) FAX 건수 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/ServiceUsageInfoSection.tsx#L117) |
| 충전금액 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/ServiceUsageInfoSection.tsx#L131) |
| 사용금액 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/ServiceUsageInfoSection.tsx#L133) |
| 환불 요청 금액 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/ServiceUsageInfoSection.tsx#L137) |
| 잔액 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/ServiceUsageInfoSection.tsx#L139) |
| (당월) 청구금액 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/ServiceUsageInfoSection.tsx#L143) |
| (당월) 미납금액 | 출력 | 조회 응답 기준 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/components/ServiceUsageInfoSection.tsx#L145) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 회원 상세 조회 | `GET /api/v1/members/{memNo}` · `/member-management/member` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/customer/member/MemberInfoController.kt#L128) | `memNo: Long` → `success`, `data`, `error`, `memNo`, `realName`, `dateOfBirth`, `memberId`, `nickname`, `email`, `contact`, `mobilePhone`, `receptionApprovalResultMail` | 직접 DB 호출이 연결된 경로는 현재 소스에서 미확인. 세부 저장소는 Controller와 Service 참조. |
| 회원 서비스 이용 정보 조회 | `GET /api/v1/members/{memNo}/service-usage` · `/member-management/member` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/customer/member/MemberInfoController.kt#L200) | `memNo: Long` → `success`, `data`, `error`, `taxInvoiceCount`, `electronicContractCount`, `purchaseConfirmationCount`, `smsCount`, `faxCount`, `electronicContractCapacityUsed`, `bondBalanceCount`, `taxCafeUsed`, `chargedAmount` | `SB_DTI.dbo.upMb_GetTheSaidMonthDtiCount`, `SB_DTI.dbo.upMb_GetTheSaidMonthEtcCount_AdmSB`, `SmartBill3.dbo.upAdmSB_memSchPay`, `SmartBill3.dbo.upAdmSB_SchInvAmt` |
| 회원 정보 수정 | `PUT /api/v1/members/{memNo}` · `/member-management/member` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/customer/member/MemberInfoController.kt#L141) | `memNo: Long` · `MemberInfoUpdateRequest` `realName`, `dateOfBirth`, `email`, `receptionApprovalResultMail`, `marketingEmailConsent`, `marketingSmsConsent`, `marketingContactConsent` → `success`, `data`, `error` | `smartwork.dbo.usp_member_info_update` · 정의에서 확인한 쓰기 `SmartBill3.dbo.MEMBER_HISTORY`, `SmartBill3.dbo.MEMBER`, `SmartBill3.dbo.MEMBER_Agreement` · 코드 연계 트랜잭션 |
| 법인 관리자 변경 | `POST /api/v1/members/{memNo}/change-corporate-admin` · `/member-management/member` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/customer/member/MemberInfoController.kt#L229) | `memNo: Long` → `success`, `data`, `error` | `SmartBill3.dbo.UPADMSB_CHGMEMTYPE` · 정의에서 확인한 쓰기 `SmartBill3.dbo.MEMBER_HISTORY`, `SmartBill3.dbo.MEMBER` · 코드 연계 트랜잭션 |
| 회원 탈퇴 처리 | `POST /api/v1/members/{memNo}/withdrawal` · `/member-management/member` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/customer/member/MemberInfoController.kt#L213) | `memNo: Long` → `success`, `data`, `error` | `smartwork.dbo.usp_member_withdraw` · 정의에서 확인한 쓰기 `SmartBill3.dbo.MEMBER_HISTORY`, `SmartBill3.dbo.MEMBER`, `SmartBill3.dbo.MEMBER_RIGHT`, `SmartBill3.dbo.COMPANY_HISTORY` 외 9개 · 코드 연계 CrmApiClient, 트랜잭션 |
| 회원 민감정보 원문 조회 | `POST /api/v1/members/{memNo}/sensitive-values/reveal` · `/member-management/member` `UNMASK` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/customer/member/MemberInfoController.kt#L106) · [기존 상세 계약](../../references/api-contracts.md#api221) | `memNo: Long` · `MemberSensitiveValueRevealRequest` `field` → `success`, `data`, `error`, `field`, `value` | `smartwork.dbo.usp_sw_log_access_event_insert` · 정의에서 확인한 쓰기 `smartwork.dbo.sw_log_access_event` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `SB_DTI.dbo.upMb_GetTheSaidMonthDtiCount` | @COM_NO int, @COM_REGNO varchar(10) | 정의 참조 `SB_DTI.dbo.DTI_HEADER_CUB`, `SB_DTI.dbo.DTI_SIGN` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/member/repository/MemberInfoMapper.kt#L297) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-cdd0a87711f96d66) |
| `SB_DTI.dbo.upMb_GetTheSaidMonthEtcCount_AdmSB` | @COM_NO int, @COM_REGNO varchar(10) | 정의 참조 `SmartBill3.dbo.ARREO_SMS_SB`, `SmartBill3.dbo.DCT_PREMIUM`, `SmartBill3.dbo.DCT_USE`, `SB_DRC.dbo.DRC_USE`, `SmartBill3.dbo.FAX_HIS` 외 7개 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/member/repository/MemberInfoMapper.kt#L310) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3423c5f55886a57b) |
| `SmartBill3.dbo.upAdmSB_memSchPay` | @no varchar(50) | 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/member/repository/MemberInfoMapper.kt#L323) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3f90afa6fb4b3d68) |
| `SmartBill3.dbo.upAdmSB_SchInvAmt` | @COM_NO int | 정의 참조 `SmartBill3.dbo.COMPANY`, `SmartBill3.dbo.fnFillDigit`, `SB_BILL.dbo.INVOICE`, `SB_BILL.dbo.PAYMENT` · 하위 호출 `SmartBill3.dbo.fnFillDigit` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/member/repository/MemberInfoMapper.kt#L332) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-9ef5f8731baa7953) |
| `smartwork.dbo.usp_member_info_update` | @NO bigint, @REALNAME varchar(35), @MEM_REGNO varchar(8), @RESULT_EMAIL char(1), @INFO_MAIL char(1), @INFO_SNS char(1), @INFO_TEL char(1), @UPDATE_SW_NO int, @EMAIL varchar(200) | 정의 참조 `SmartBill3.dbo.MEMBER`, `SmartBill3.dbo.MEMBER_Agreement`, `SmartBill3.dbo.MEMBER_HISTORY` · 정적 쓰기 `SmartBill3.dbo.MEMBER_HISTORY`, `SmartBill3.dbo.MEMBER`, `SmartBill3.dbo.MEMBER_Agreement` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/member/repository/MemberInfoMapper.kt#L212) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-8cc7fe864a28270b) |
| `SmartBill3.dbo.UPADMSB_CHGMEMTYPE` | @NO varchar(10), @SW_NO varchar(20) | 정의 참조 `SmartBill3.dbo.COMPANY`, `SmartBill3.dbo.MEMBER`, `SmartBill3.dbo.MEMBER_HISTORY` · 정적 쓰기 `SmartBill3.dbo.MEMBER_HISTORY`, `SmartBill3.dbo.MEMBER` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/member/repository/MemberInfoMapper.kt#L224) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-ea655e15205752b3) |
| `smartwork.dbo.usp_member_withdraw` | @MEM_NO bigint, @UPDATE_SW_NO bigint | 정의 참조 `SmartBill3.dbo.MEMBER`, `SmartBill3.dbo.MEMBER_HISTORY`, `SmartBill3.dbo.upAdmSB_memOut` · 정적 쓰기 `SmartBill3.dbo.MEMBER_HISTORY` · 하위 호출 `SmartBill3.dbo.upAdmSB_memOut` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/member/repository/MemberInfoMapper.kt#L218) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-ef012ac07392220b) |
| `smartwork.dbo.usp_sw_log_access_event_insert` | @EVENT_TYPE varchar(30), @STATUS varchar(20), @USER_ID bigint = NULL, @MEMBER_ID nvarchar(50) = NULL, @USER_NAME nvarchar(100) = NULL, @DEPARTMENT_NAME nvarchar(100) = NULL, @PAGE_TITLE nvarchar(200) = NULL, @PATH nvarchar(500) = NULL, @MENU_PATH nvarchar(500) = NULL, @MENU_LABEL nvarchar(200) = NULL, @CATEGORY_NAME nvarchar(200) = NULL, @SUB_CATEGORY_NAME nvarchar(200) = NULL, @MENU_ORDER int = NULL, @IP_ADDRESS varchar(45) = NULL, @USER_AGENT nvarchar(1000) = NULL, @BROWSER varchar(100) = NULL, @OS varchar(100) = NULL, @REFERRER nvarchar(500) = NULL, @DETAIL nvarchar(1000) = NULL, @RESULT int OUT, @COUNTS_AS_VISIT bit = 1 | 정의 참조 `smartwork.dbo.sw_log_access_event` · 정적 쓰기 `smartwork.dbo.sw_log_access_event` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/logmanagement/repository/LogManagementMapper.kt#L92) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b7ba94e0cc2f35c0) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 실명, 생년월일, 아이디, 닉네임, 이메일, 연락처 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | SB 고객관리 > 스마트빌 회원·회사정보 관리 > 회원 정보의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 회원정보 수정 중 오류가 발생했습니다. | 실명, 생년월일, 아이디, 닉네임, 이메일, 연락처 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| [청구데이터 생성기간]에는 탈퇴 처리가 불가능합니다. | 실명, 생년월일, 아이디, 닉네임, 이메일, 연락처 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 회원정보가 수정되었습니다. | 실명, 생년월일, 아이디, 닉네임, 이메일, 연락처 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 유효하지 않은 회원 ID입니다. | 실명, 생년월일, 아이디, 닉네임, 이메일, 연락처 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/CustomerRoutes.tsx#L42) · [MemberDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/MemberDetailPage.tsx#L47) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/api/memberManagementApi.ts#L90) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/api/memberManagementApi.ts#L124) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/api/memberManagementApi.ts#L99) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/api/memberManagementApi.ts#L110) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/api/memberManagementApi.ts#L117) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/customer/member/api/memberManagementApi.ts#L75) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 8개 중 개발 메타데이터 확인 8개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-53165179f77881d4) | 2026-11-11 기준으로 Demo 메타데이터 8/8개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |
| 최신 변경 대조 | [11월 12일 전수 대조](../../references/all-pages-audit-2026-11-12.md) | 현재 코드 b923849c5 · 2026-11-12 |

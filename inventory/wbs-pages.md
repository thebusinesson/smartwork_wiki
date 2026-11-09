# WBS 유지윤 담당 페이지별 관리자 매뉴얼

확인일 2026-11-09 · 소스 기준 `dc216b313` · 담당 선정 기준: 사용자가 제공한 **WBS 탭 원문**의 작업자 **유지윤**. WBS(최종)과 Git 변경 참여 목록은 선정 기준으로 사용하지 않았다.

선정 태스크 **105개**, 현재 메뉴 **56개**, 독립 화면 **134개**. 독립 경로마다 문서 한 개를 작성했으며 같은 경로의 팝업·탭은 해당 문서에 포함했다. API/화면 개발의 중복 태스크는 문서 수에 중복 가산하지 않았다.

모든 문서는 7개 항목으로 통일했다. 상태는 코드·개발 DB 정의 확인 후 **검토 대기**다. 실제 계정의 브라우저 대조와 빈 입력·검색 결과 검증을 추가했다. [경로별 검증 결과](../references/browser-verification.md)를 확인한다. 역할별 권한 거부·변경 기능·외부 결과·배포 환경과 미재현 상세의 후속 검증이 남아 있으므로 **완료**로 표시하지 않았다.

## 도메인별 독립 화면 수

| 도메인 | 독립 화면 수 |
|---|---|
| SB 서비스관리 | 40 |
| 서비스 현황 | 21 |
| SB 고객관리 | 14 |
| SB 운영관리 | 11 |
| 고객지원 | 48 |

## 조사 목록

### SB 서비스관리

| 도메인 | 메뉴 경로 | 화면·유형 | 라우트 | 담당 | 상태 | 문서·비고 |
|---|---|---|---|---|---|---|
| SB 서비스관리 | SB 서비스관리 > 전자세금계산서 > 세금계산서 조회 | 세금계산서 조회 조회·관리 | `/tax-invoice/tax-invoice` | 유지윤 | 검토 대기 | [문서](../manuals/tax-invoice/tax-invoice.md) · WBS 43, 44, 45, 46, 47 |
| SB 서비스관리 | SB 서비스관리 > 전자세금계산서 > 세금계산서 조회 | 세금계산서 조회 상세 | `/tax-invoice/tax-invoice/:id` | 유지윤 | 검토 대기 | [문서](../manuals/tax-invoice/tax-invoice__by-id.md) · WBS 43, 44, 45, 46, 47 |
| SB 서비스관리 | SB 서비스관리 > 전자세금계산서 > 세금계산서 조회 | 세금계산서 조회 (단독) 거래명세서 상세 | `/tax-invoice/tax-invoice/statement/:id` | 유지윤 | 검토 대기 | [문서](../manuals/tax-invoice/tax-invoice__statement__by-id.md) · WBS 43, 44, 45, 46, 47 |
| SB 서비스관리 | SB 서비스관리 > 전자세금계산서 > 과거 세금계산서 조회 | 과거 세금계산서 조회 조회·관리 | `/tax-invoice/legacy-tax-invoice` | 유지윤 | 검토 대기 | [문서](../manuals/tax-invoice/legacy-tax-invoice.md) · WBS 48 |
| SB 서비스관리 | SB 서비스관리 > 전자세금계산서 > 과거 세금계산서 조회 | 과거 세금계산서 조회 상세 | `/tax-invoice/legacy-tax-invoice/:id` | 유지윤 | 검토 대기 | [문서](../manuals/tax-invoice/legacy-tax-invoice__by-id.md) · WBS 48 |
| SB 서비스관리 | SB 서비스관리 > 전자세금계산서 > 과거 세금계산서 조회 | 과거 세금계산서 조회 (단독) 거래명세서 상세 | `/tax-invoice/legacy-tax-invoice/statement/:id` | 유지윤 | 검토 대기 | [문서](../manuals/tax-invoice/legacy-tax-invoice__statement__by-id.md) · WBS 48 |
| SB 서비스관리 | SB 서비스관리 > 채권잔액 확인 서비스 > 채권잔액 확인서 조회 | 채권잔액 확인서 조회 조회·관리 | `/bond-service/bond-balance-inquiry` | 유지윤 | 검토 대기 | [문서](../manuals/bond-service/bond-balance-inquiry.md) · WBS 109 |
| SB 서비스관리 | SB 서비스관리 > 채권잔액 확인 서비스 > 채권잔액 확인서 조회 | 채권잔액 확인서 조회 상세 | `/bond-service/bond-balance-inquiry/:drcNo` | 유지윤 | 검토 대기 | [문서](../manuals/bond-service/bond-balance-inquiry__by-drcNo.md) · WBS 109 |
| SB 서비스관리 | SB 서비스관리 > 채권잔액 확인 서비스 > 담당자 권한 조회 | 담당자 권한 조회 조회·관리 | `/bond-service/drc-right` | 유지윤 | 검토 대기 | [문서](../manuals/bond-service/drc-right.md) · WBS 110 |
| SB 서비스관리 | SB 서비스관리 > 채권잔액 확인 서비스 > 담당자 권한 조회 | 담당자 권한 조회 상세 | `/bond-service/drc-right/:comNo` | 유지윤 | 검토 대기 | [문서](../manuals/bond-service/drc-right__by-comNo.md) · WBS 110 |
| SB 서비스관리 | SB 서비스관리 > 채권잔액 확인 서비스 > 연동업체 관리 | 연동업체 관리 조회·관리 | `/bond-service/drc-company-link` | 유지윤 | 검토 대기 | [문서](../manuals/bond-service/drc-company-link.md) · WBS 111, 112, 113 |
| SB 서비스관리 | SB 서비스관리 > 채권잔액 확인 서비스 > 연동업체 관리 | 연동업체 관리 상세 | `/bond-service/drc-company-link/:comNo` | 유지윤 | 검토 대기 | [문서](../manuals/bond-service/drc-company-link__by-comNo.md) · WBS 111, 112, 113 |
| SB 서비스관리 | SB 서비스관리 > 채권잔액 확인 서비스 > 연동업체 관리 | 연동업체 관리 등록 | `/bond-service/drc-company-link/new` | 유지윤 | 검토 대기 | [문서](../manuals/bond-service/drc-company-link__new.md) · WBS 111, 112, 113 |
| SB 서비스관리 | SB 서비스관리 > 채권잔액 확인 서비스 > 연동 로그 조회 | 연동 로그 조회 조회·관리 | `/bond-service/integration-log` | 유지윤 | 검토 대기 | [문서](../manuals/bond-service/integration-log.md) · WBS 114, 115 |
| SB 서비스관리 | SB 서비스관리 > 채권잔액 확인 서비스 > 연동업체 장애 관리 | 연동업체 장애 관리 조회·관리 | `/bond-service/integration-partner-error` | 유지윤 | 검토 대기 | [문서](../manuals/bond-service/integration-partner-error.md) · WBS 116 |
| SB 서비스관리 | SB 서비스관리 > 채권잔액 확인 서비스 > 연동업체 장애 관리 | 연동업체 장애 관리 장애 등록·수정 | `/bond-service/integration-partner-error/detail` | 유지윤 | 검토 대기 | [문서](../manuals/bond-service/integration-partner-error__detail.md) · WBS 116 |
| SB 서비스관리 | SB 서비스관리 > 채권잔액 확인 서비스 > 채권잔액 전송 관리 | 채권잔액 전송 관리 조회·관리 | `/bond-service/receivable-balance-transfer` | 유지윤 | 검토 대기 | [문서](../manuals/bond-service/receivable-balance-transfer.md) · WBS 117, 118 |
| SB 서비스관리 | SB 서비스관리 > 채권잔액 확인 서비스 > 채권잔액 전송 관리 | 채권잔액 전송 관리 상세 | `/bond-service/receivable-balance-transfer/:conversationId` | 유지윤 | 검토 대기 | [문서](../manuals/bond-service/receivable-balance-transfer__by-conversationId.md) · WBS 117, 118 |
| SB 서비스관리 | SB 서비스관리 > 홈택스 DTI 수집 > 모니터링 | 모니터링 조회·관리 | `/hometax-dti/monitoring` | 유지윤 | 검토 대기 | [문서](../manuals/hometax-dti/monitoring.md) · WBS 123 |
| SB 서비스관리 | SB 서비스관리 > 홈택스 DTI 수집 > 인증키 관리 | 인증키 관리 조회·관리 | `/hometax-dti/auth-key` | 유지윤 | 검토 대기 | [문서](../manuals/hometax-dti/auth-key.md) · WBS 124, 125 |
| SB 서비스관리 | SB 서비스관리 > 홈택스 DTI 수집 > 인증키 관리 | 인증키 관리 상세 | `/hometax-dti/auth-key/:sbKey` | 유지윤 | 검토 대기 | [문서](../manuals/hometax-dti/auth-key__by-sbKey.md) · WBS 124, 125 |
| SB 서비스관리 | SB 서비스관리 > 홈택스 DTI 수집 > 오류 로그 조회 | 오류 로그 조회 조회·관리 | `/hometax-dti/error-logs` | 유지윤 | 검토 대기 | [문서](../manuals/hometax-dti/error-logs.md) · WBS 126, 127 |
| SB 서비스관리 | SB 서비스관리 > 홈택스 DTI 수집 > 인증서 등록 현황 조회 | 인증서 등록 현황 조회 조회·관리 | `/hometax-dti/certificate-status` | 유지윤 | 검토 대기 | [문서](../manuals/hometax-dti/certificate-status.md) · WBS 128 |
| SB 서비스관리 | SB 서비스관리 > 홈택스 DTI 수집 > 인증서 만료일 관리 | 인증서 만료일 관리 조회·관리 | `/hometax-dti/certificate-expiry` | 유지윤 | 검토 대기 | [문서](../manuals/hometax-dti/certificate-expiry.md) · WBS 129 |
| SB 서비스관리 | SB 서비스관리 > 홈택스 DTI 수집 > 인증서 로그인 실패 조회 | 인증서 로그인 실패 조회 조회·관리 | `/hometax-dti/login-failures` | 유지윤 | 검토 대기 | [문서](../manuals/hometax-dti/login-failures.md) · WBS 130 |
| SB 서비스관리 | SB 서비스관리 > 홈택스 DTI 수집 > 이메일파싱 모니터링 | 이메일파싱 모니터링 조회·관리 | `/hometax-dti/email-parsing` | 유지윤 | 검토 대기 | [문서](../manuals/hometax-dti/email-parsing.md) · WBS 131 |
| SB 서비스관리 | SB 서비스관리 > 보나뱅크 > 회사 정보 | 회사 정보 조회·관리 | `/bonabank/company` | 유지윤 | 검토 대기 | [문서](../manuals/bonabank/company.md) · WBS 138, 139 |
| SB 서비스관리 | SB 서비스관리 > 보나뱅크 > 회사 정보 | 회사 정보 전체 회원 조회 | `/bonabank/company/:companyId/members` | 유지윤 | 검토 대기 | [문서](../manuals/bonabank/company__by-companyId__members.md) · WBS 138, 139 |
| SB 서비스관리 | SB 서비스관리 > 보나뱅크 > 회사 정보 | 회사 정보 상세 | `/bonabank/company/:id` | 유지윤 | 검토 대기 | [문서](../manuals/bonabank/company__by-id.md) · WBS 138, 139 |
| SB 서비스관리 | SB 서비스관리 > 보나뱅크 > 회사 정보 | 회사 정보 변경 이력 | `/bonabank/company/:id/change-history` | 유지윤 | 검토 대기 | [문서](../manuals/bonabank/company__by-id__change-history.md) · WBS 138, 139 |
| SB 서비스관리 | SB 서비스관리 > 보나뱅크 > 회원 정보 | 회원 정보 조회·관리 | `/bonabank/member` | 유지윤 | 검토 대기 | [문서](../manuals/bonabank/member.md) · WBS 140, 141 |
| SB 서비스관리 | SB 서비스관리 > 보나뱅크 > 회원 정보 | 회원 정보 상세 | `/bonabank/member/:id` | 유지윤 | 검토 대기 | [문서](../manuals/bonabank/member__by-id.md) · WBS 140, 141 |
| SB 서비스관리 | SB 서비스관리 > 보나뱅크 > 세금계산서 조회 | 세금계산서 조회 조회·관리 | `/bonabank/tax-invoice` | 유지윤 | 검토 대기 | [문서](../manuals/bonabank/tax-invoice.md) · WBS 142, 143 |
| SB 서비스관리 | SB 서비스관리 > 보나뱅크 > 세금계산서 조회 | 세금계산서 조회 상세 | `/bonabank/tax-invoice/:dtiIdx` | 유지윤 | 검토 대기 | [문서](../manuals/bonabank/tax-invoice__by-dtiIdx.md) · WBS 142, 143 |
| SB 서비스관리 | SB 서비스관리 > 보나뱅크 > 세금계산서 통계 | 세금계산서 통계 조회·관리 | `/bonabank/tax-invoice-statistics` | 유지윤 | 검토 대기 | [문서](../manuals/bonabank/tax-invoice-statistics.md) · WBS 144, 145 |
| SB 서비스관리 | SB 서비스관리 > 보나뱅크 > 국세청 신고 실패 조회 | 국세청 신고 실패 조회 조회·관리 | `/bonabank/nts-failures` | 유지윤 | 검토 대기 | [문서](../manuals/bonabank/nts-failures.md) · WBS 146, 147; WBS “국세청 전송 조회” → 현재 “국세청 신고 실패 조회”, 업무 담당 명칭 검토 필요 |
| SB 서비스관리 | SB 서비스관리 > 보나뱅크 > 공지사항 관리 | 공지사항 관리 조회·관리 | `/bonabank/notices` | 유지윤 | 검토 대기 | [문서](../manuals/bonabank/notices.md) · WBS 148, 149 |
| SB 서비스관리 | SB 서비스관리 > 보나뱅크 > 공지사항 관리 | 공지사항 관리 상세 | `/bonabank/notices/:id` | 유지윤 | 검토 대기 | [문서](../manuals/bonabank/notices__by-id.md) · WBS 148, 149 |
| SB 서비스관리 | SB 서비스관리 > 보나뱅크 > 공지사항 관리 | 공지사항 관리 수정 | `/bonabank/notices/:id/edit` | 유지윤 | 검토 대기 | [문서](../manuals/bonabank/notices__by-id__edit.md) · WBS 148, 149 |
| SB 서비스관리 | SB 서비스관리 > 보나뱅크 > 공지사항 관리 | 공지사항 관리 등록 | `/bonabank/notices/new` | 유지윤 | 검토 대기 | [문서](../manuals/bonabank/notices__new.md) · WBS 148, 149 |

### 서비스 현황

| 도메인 | 메뉴 경로 | 화면·유형 | 라우트 | 담당 | 상태 | 문서·비고 |
|---|---|---|---|---|---|---|
| 서비스 현황 | 서비스 현황 > 입금관리 > 입금 현황 조회 | 입금 현황 조회 조회·관리 | `/payment/status` | 유지윤 | 검토 대기 | [문서](../manuals/payment/status.md) · WBS 184 |
| 서비스 현황 | 서비스 현황 > 입금관리 > 입금 현황 조회 | 입금 현황 조회 상세 | `/payment/status/:id` | 유지윤 | 검토 대기 | [문서](../manuals/payment/status__by-id.md) · WBS 184 |
| 서비스 현황 | 서비스 현황 > 입금관리 > 예치금 관리 | 예치금 관리 조회·관리 | `/payment/deposit` | 유지윤 | 검토 대기 | [문서](../manuals/payment/deposit.md) · WBS 185 |
| 서비스 현황 | 서비스 현황 > 입금관리 > 예치금 관리 | 예치금 관리 상세 | `/payment/deposit/:id` | 유지윤 | 검토 대기 | [문서](../manuals/payment/deposit__by-id.md) · WBS 185 |
| 서비스 현황 | 서비스 현황 > 입금관리 > 일별 예치금 조회 | 일별 예치금 조회 조회·관리 | `/payment/daily-deposit-inquiry` | 유지윤 | 검토 대기 | [문서](../manuals/payment/daily-deposit-inquiry.md) · WBS 186 |
| 서비스 현황 | 서비스 현황 > 입금관리 > 일별 예치금 조회 | 일별 예치금 조회 상세 | `/payment/daily-deposit-inquiry/:id` | 유지윤 | 검토 대기 | [문서](../manuals/payment/daily-deposit-inquiry__by-id.md) · WBS 186 |
| 서비스 현황 | 서비스 현황 > 입금관리 > 벌크식계좌 입금 관리 | 벌크식계좌 입금 관리 조회·관리 | `/payment/bulk-account-deposit` | 유지윤 | 검토 대기 | [문서](../manuals/payment/bulk-account-deposit.md) · WBS 187, 188, 189 |
| 서비스 현황 | 서비스 현황 > 입금관리 > 벌크식계좌 입금 관리 | 벌크식계좌 입금 관리 상세 | `/payment/bulk-account-deposit/:id` | 유지윤 | 검토 대기 | [문서](../manuals/payment/bulk-account-deposit__by-id.md) · WBS 187, 188, 189 |
| 서비스 현황 | 서비스 현황 > 입금관리 > 무통장입금 취소내역 조회 | 무통장입금 취소내역 조회 조회·관리 | `/payment/bank-transfer-cancel` | 유지윤 | 검토 대기 | [문서](../manuals/payment/bank-transfer-cancel.md) · WBS 212 |
| 서비스 현황 | 서비스 현황 > 입금관리 > 환불 관리 | 환불 관리 조회·관리 | `/payment/refund-management` | 유지윤 | 검토 대기 | [문서](../manuals/payment/refund-management.md) · WBS 213, 214, 215 |
| 서비스 현황 | 서비스 현황 > 입금관리 > 환불 관리 | 환불 관리 상세 | `/payment/refund-management/:refundNo` | 유지윤 | 검토 대기 | [문서](../manuals/payment/refund-management__by-refundNo.md) · WBS 213, 214, 215 |
| 서비스 현황 | 서비스 현황 > 입금관리 > 환불 관리 | 환불 관리 환불 가능 금액 조회 | `/payment/refund-management/inquiry` | 유지윤 | 검토 대기 | [문서](../manuals/payment/refund-management__inquiry.md) · WBS 213, 214, 215 |
| 서비스 현황 | 서비스 현황 > 입금관리 > 환불 관리 | 환불 관리 등록 | `/payment/refund-management/new` | 유지윤 | 검토 대기 | [문서](../manuals/payment/refund-management__new.md) · WBS 213, 214, 215 |
| 서비스 현황 | 서비스 현황 > 미납 예외업체 관리 > 미납 예외업체 관리 | 미납 예외업체 관리 조회·관리 | `/service-overview/unpaid-exception-manager` | 유지윤 | 검토 대기 | [문서](../manuals/service-overview/unpaid-exception-manager.md) · WBS 219, 220 |
| 서비스 현황 | 서비스 현황 > 통계 정보 > 월별 이용 현황 (세금, 계약) | 월별 이용 현황 (세금, 계약) 조회·관리 | `/statistics/monthly-usage` | 유지윤 | 검토 대기 | [문서](../manuals/statistics/monthly-usage.md) · WBS 223 |
| 서비스 현황 | 서비스 현황 > 통계 정보 > 월별 이용 현황 (세금, 계약) | 월별 이용 현황 (세금, 계약) 전자계약 일별 현황 | `/statistics/monthly-usage/daily-electronic-contract` | 유지윤 | 검토 대기 | [문서](../manuals/statistics/monthly-usage__daily-electronic-contract.md) · WBS 223 |
| 서비스 현황 | 서비스 현황 > 통계 정보 > 월별 이용 현황 (세금, 계약) | 월별 이용 현황 (세금, 계약) 세금계산서 일별 현황 | `/statistics/monthly-usage/daily-tax-invoice` | 유지윤 | 검토 대기 | [문서](../manuals/statistics/monthly-usage__daily-tax-invoice.md) · WBS 223 |
| 서비스 현황 | 서비스 현황 > 통계 정보 > 월별 세금계산서 이용 현황 (일반) | 월별 세금계산서 이용 현황 (일반) 조회·관리 | `/statistics/monthly-tax-invoice-usage` | 유지윤 | 검토 대기 | [문서](../manuals/statistics/monthly-tax-invoice-usage.md) · WBS 224 |
| 서비스 현황 | 서비스 현황 > 통계 정보 > 월별 세금계산서 이용 현황 (일반) | 월별 세금계산서 이용 현황 (일반) 일별 현황 | `/statistics/monthly-tax-invoice-usage/daily` | 유지윤 | 검토 대기 | [문서](../manuals/statistics/monthly-tax-invoice-usage__daily.md) · WBS 224 |
| 서비스 현황 | 서비스 현황 > 통계 정보 > 매출/매입 이용 현황 | 매출/매입 이용 현황 조회·관리 | `/statistics/sales-purchases-usage` | 유지윤 | 검토 대기 | [문서](../manuals/statistics/sales-purchases-usage.md) · WBS 225 |
| 서비스 현황 | 서비스 현황 > 통계 정보 > 세금계산서 일별 데이터 집계 | 세금계산서 일별 데이터 집계 조회·관리 | `/statistics/daily-tax-invoice-aggregate` | 유지윤 | 검토 대기 | [문서](../manuals/statistics/daily-tax-invoice-aggregate.md) · WBS 226 |

### SB 고객관리

| 도메인 | 메뉴 경로 | 화면·유형 | 라우트 | 담당 | 상태 | 문서·비고 |
|---|---|---|---|---|---|---|
| SB 고객관리 | SB 고객관리 > 스마트빌 회원·회사정보 관리 > 회사 정보 | 회사 정보 조회·관리 | `/company-management/company-info` | 유지윤 | 검토 대기 | [문서](../manuals/company-management/company-info.md) · WBS 17, 18, 19, 20, 21, 22, 23, 24 |
| SB 고객관리 | SB 고객관리 > 스마트빌 회원·회사정보 관리 > 회사 정보 | 회사 정보 전체 회원 조회 | `/company-management/company-info/:companyId/members` | 유지윤 | 검토 대기 | [문서](../manuals/company-management/company-info__by-companyId__members.md) · WBS 17, 18, 19, 20, 21, 22, 23, 24 |
| SB 고객관리 | SB 고객관리 > 스마트빌 회원·회사정보 관리 > 회사 정보 | 회사 정보 회원 권한 조회 | `/company-management/company-info/:companyKey/member-permissions` | 유지윤 | 검토 대기 | [문서](../manuals/company-management/company-info__by-companyKey__member-permissions.md) · WBS 17, 18, 19, 20, 21, 22, 23, 24 |
| SB 고객관리 | SB 고객관리 > 스마트빌 회원·회사정보 관리 > 회사 정보 | 회사 정보 상세 | `/company-management/company-info/:id` | 유지윤 | 검토 대기 | [문서](../manuals/company-management/company-info__by-id.md) · WBS 17, 18, 19, 20, 21, 22, 23, 24 |
| SB 고객관리 | SB 고객관리 > 스마트빌 회원·회사정보 관리 > 회사 정보 | 회사 정보 변경 이력 | `/company-management/company-info/:id/change-history` | 유지윤 | 검토 대기 | [문서](../manuals/company-management/company-info__by-id__change-history.md) · WBS 17, 18, 19, 20, 21, 22, 23, 24 |
| SB 고객관리 | SB 고객관리 > 스마트빌 회원·회사정보 관리 > 스마트빌 가입조회 | 스마트빌 가입조회 조회·관리 | `/company-management/registration-inquiry` | 유지윤 | 검토 대기 | [문서](../manuals/company-management/registration-inquiry.md) · WBS 25 |
| SB 고객관리 | SB 고객관리 > 스마트빌 회원·회사정보 관리 > 스마트빌 가입조회 | 스마트빌 가입조회 상세 | `/company-management/registration-inquiry/:uploadId` | 유지윤 | 검토 대기 | [문서](../manuals/company-management/registration-inquiry__by-uploadId.md) · WBS 25 |
| SB 고객관리 | SB 고객관리 > 스마트빌 이용 현황 > 가입 현황 | 가입 현황 조회·관리 | `/smartbill-status/status` | 유지윤 | 검토 대기 | [문서](../manuals/smartbill-status/status.md) · WBS 33, 35 |
| SB 고객관리 | SB 고객관리 > 스마트빌 이용 현황 > 탈퇴 현황 | 탈퇴 현황 조회·관리 | `/smartbill-status/withdrawal-status` | 유지윤 | 검토 대기 | [문서](../manuals/smartbill-status/withdrawal-status.md) · WBS 34, 36 |
| SB 고객관리 | SB 고객관리 > 글로싸인 엔터프라이즈 > 회원 정보 | 회원 정보 조회·관리 | `/glosign-enterprise/members` | 유지윤 | 검토 대기 | [문서](../manuals/glosign-enterprise/members.md) · WBS 37 |
| SB 고객관리 | SB 고객관리 > 글로싸인 엔터프라이즈 > 회사 정보 | 회사 정보 조회·관리 | `/glosign-enterprise/companies` | 유지윤 | 검토 대기 | [문서](../manuals/glosign-enterprise/companies.md) · WBS 38, 39 |
| SB 고객관리 | SB 고객관리 > 글로싸인 엔터프라이즈 > 회사 정보 | 회사 정보 전체 회원 조회 | `/glosign-enterprise/companies/:orgSeq` | 유지윤 | 검토 대기 | [문서](../manuals/glosign-enterprise/companies__by-orgSeq.md) · WBS 38, 39 |
| SB 고객관리 | SB 고객관리 > 글로싸인 엔터프라이즈 > 비밀번호 초기화 | 비밀번호 초기화 비밀번호 초기화 | `/glosign-enterprise/status` | 유지윤 | 검토 대기 | [문서](../manuals/glosign-enterprise/status.md) · WBS 40, 41 |
| SB 고객관리 | SB 고객관리 > 글로싸인 엔터프라이즈 > 열람인증 초기화 | 열람인증 초기화 조회·관리 | `/glosign-enterprise/personal-password-reset` | 유지윤 | 검토 대기 | [문서](../manuals/glosign-enterprise/personal-password-reset.md) · WBS 42 |

### SB 운영관리

| 도메인 | 메뉴 경로 | 화면·유형 | 라우트 | 담당 | 상태 | 문서·비고 |
|---|---|---|---|---|---|---|
| SB 운영관리 | SB 운영관리 > 오류 관리 > 전체 오류 조회/처리 | 전체 오류 조회/처리 조회·관리 | `/error-management/error-reports` | 유지윤 | 검토 대기 | [문서](../manuals/error-management/error-reports.md) · WBS 150, 151, 152, 153, 154 |
| SB 운영관리 | SB 운영관리 > 오류 관리 > 전체 오류 조회/처리 | 전체 오류 조회/처리 상세 | `/error-management/error-reports/:id` | 유지윤 | 검토 대기 | [문서](../manuals/error-management/error-reports__by-id.md) · WBS 150, 151, 152, 153, 154 |
| SB 운영관리 | SB 운영관리 > 오류 관리 > 전체 오류 조회/처리 | 전체 오류 조회/처리 오류 처리내역 등록 | `/error-management/error-reports/:id/process` | 유지윤 | 검토 대기 | [문서](../manuals/error-management/error-reports__by-id__process.md) · WBS 150, 151, 152, 153, 154 |
| SB 운영관리 | SB 운영관리 > 오류 관리 > 오류 접수/등록 | 오류 접수/등록 등록 | `/error-management/error-reports/new` | 유지윤 | 검토 대기 | [문서](../manuals/error-management/error-reports__new.md) · WBS 150, 151, 152, 153, 154 |
| SB 운영관리 | SB 운영관리 > 오류 관리 > 오류 코드 관리 | 오류 코드 관리 조회·관리 | `/error-management/error-code-management` | 유지윤 | 검토 대기 | [문서](../manuals/error-management/error-code-management.md) · WBS 155, 156 |
| SB 운영관리 | SB 운영관리 > 오류 관리 > 오류 코드 관리 | 오류 코드 관리 상세 | `/error-management/error-code-management/:errorCode` | 유지윤 | 검토 대기 | [문서](../manuals/error-management/error-code-management__by-errorCode.md) · WBS 155, 156 |
| SB 운영관리 | SB 운영관리 > 오류 관리 > 오류 코드 관리 | 오류 코드 관리 등록 | `/error-management/error-code-management/new` | 유지윤 | 검토 대기 | [문서](../manuals/error-management/error-code-management__new.md) · WBS 155, 156 |
| SB 운영관리 | SB 운영관리 > 운영반영 관리 > 소스 관리 | 소스 관리 조회·관리 | `/source-management/source-management` | 유지윤 | 검토 대기 | [문서](../manuals/source-management/source-management.md) · WBS 157, 158 |
| SB 운영관리 | SB 운영관리 > 운영반영 관리 > 소스 관리 | 소스 관리 상세 | `/source-management/source-management/:id` | 유지윤 | 검토 대기 | [문서](../manuals/source-management/source-management__by-id.md) · WBS 157, 158 |
| SB 운영관리 | SB 운영관리 > 운영반영 관리 > 소스 관리 | 소스 관리 수정 | `/source-management/source-management/:id/edit` | 유지윤 | 검토 대기 | [문서](../manuals/source-management/source-management__by-id__edit.md) · WBS 157, 158 |
| SB 운영관리 | SB 운영관리 > 운영반영 관리 > 소스 관리 | 소스 관리 등록 | `/source-management/source-management/new` | 유지윤 | 검토 대기 | [문서](../manuals/source-management/source-management__new.md) · WBS 157, 158 |

### 고객지원

| 도메인 | 메뉴 경로 | 화면·유형 | 라우트 | 담당 | 상태 | 문서·비고 |
|---|---|---|---|---|---|---|
| 고객지원 | 고객지원 > 고객 게시판 관리 > 공지사항 | 공지사항 조회·관리 | `/customer-support/notice` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/notice.md) · WBS 334, 335 |
| 고객지원 | 고객지원 > 고객 게시판 관리 > 공지사항 | 공지사항 상세 | `/customer-support/notice/:id` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/notice__by-id.md) · WBS 334, 335 |
| 고객지원 | 고객지원 > 고객 게시판 관리 > 공지사항 | 공지사항 수정 | `/customer-support/notice/:id/edit` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/notice__by-id__edit.md) · WBS 334, 335 |
| 고객지원 | 고객지원 > 고객 게시판 관리 > 공지사항 | 공지사항 등록 | `/customer-support/notice/new` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/notice__new.md) · WBS 334, 335 |
| 고객지원 | 고객지원 > 고객 게시판 관리 > FAQ | FAQ 조회·관리 | `/customer-support/faq` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/faq.md) · WBS 336, 337 |
| 고객지원 | 고객지원 > 고객 게시판 관리 > FAQ | FAQ 상세 | `/customer-support/faq/:id` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/faq__by-id.md) · WBS 336, 337 |
| 고객지원 | 고객지원 > 고객 게시판 관리 > FAQ | FAQ 수정 | `/customer-support/faq/:id/edit` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/faq__by-id__edit.md) · WBS 336, 337 |
| 고객지원 | 고객지원 > 고객 게시판 관리 > FAQ | FAQ 등록 | `/customer-support/faq/new` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/faq__new.md) · WBS 336, 337 |
| 고객지원 | 고객지원 > 고객 게시판 관리 > 1:1 문의 | 1:1 문의 조회·관리 | `/customer-support/qna` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/qna.md) · WBS 338, 339 |
| 고객지원 | 고객지원 > 고객 게시판 관리 > 1:1 문의 | 1:1 문의 상세 | `/customer-support/qna/:id` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/qna__by-id.md) · WBS 338, 339 |
| 고객지원 | 고객지원 > 고객 게시판 관리 > 1:1 문의 | 1:1 문의 수정 | `/customer-support/qna/:id/edit` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/qna__by-id__edit.md) · WBS 338, 339 |
| 고객지원 | 고객지원 > 고객 게시판 관리 > 1:1 문의 | 1:1 문의 답글 등록 | `/customer-support/qna/:id/reply` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/qna__by-id__reply.md) · WBS 338, 339 |
| 고객지원 | 고객지원 > 고객 게시판 관리 > 1:1 문의 | 1:1 문의 등록 | `/customer-support/qna/new` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/qna__new.md) · WBS 338, 339 |
| 고객지원 | 고객지원 > 고객 게시판 관리 > 자료실 | 자료실 조회·관리 | `/customer-support/pds` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/pds.md) · WBS 340, 341 |
| 고객지원 | 고객지원 > 고객 게시판 관리 > 자료실 | 자료실 상세 | `/customer-support/pds/:id` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/pds__by-id.md) · WBS 340, 341 |
| 고객지원 | 고객지원 > 고객 게시판 관리 > 자료실 | 자료실 수정 | `/customer-support/pds/:id/edit` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/pds__by-id__edit.md) · WBS 340, 341 |
| 고객지원 | 고객지원 > 고객 게시판 관리 > 자료실 | 자료실 등록 | `/customer-support/pds/new` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/pds__new.md) · WBS 340, 341 |
| 고객지원 | 고객지원 > 멤버십 쿠폰관리 > 쿠폰 조회 | 쿠폰 조회 조회·관리 | `/customer-support/coupon` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/coupon.md) · WBS 342 |
| 고객지원 | 고객지원 > 멤버십 쿠폰관리 > 쿠폰 조회 | 쿠폰 조회 상세 | `/customer-support/coupon/:couponNo` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/coupon__by-couponNo.md) · WBS 342 |
| 고객지원 | 고객지원 > 멤버십 쿠폰관리 > 쿠폰 이력 조회 | 쿠폰 이력 조회 조회·관리 | `/customer-support/coupon-history` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/coupon-history.md) · WBS 343 |
| 고객지원 | 고객지원 > 서비스 플랫폼 관리(자료실) > WEB 자료실 | WEB 자료실 조회·관리 | `/customer-support/web-resources` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/web-resources.md) · WBS 344, 345; 게시판 type=C |
| 고객지원 | 고객지원 > 서비스 플랫폼 관리(자료실) > WEB 자료실 | WEB 자료실 상세 | `/customer-support/web-resources/:id` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/web-resources__by-id.md) · WBS 344, 345; 게시판 type=C |
| 고객지원 | 고객지원 > 서비스 플랫폼 관리(자료실) > WEB 자료실 | WEB 자료실 수정 | `/customer-support/web-resources/:id/edit` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/web-resources__by-id__edit.md) · WBS 344, 345; 게시판 type=C |
| 고객지원 | 고객지원 > 서비스 플랫폼 관리(자료실) > WEB 자료실 | WEB 자료실 등록 | `/customer-support/web-resources/new` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/web-resources__new.md) · WBS 344, 345; 게시판 type=C |
| 고객지원 | 고객지원 > 서비스 플랫폼 관리(자료실) > WEB 문의 가이드 | WEB 문의 가이드 조회·관리 | `/customer-support/web-inquiry-guide` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/web-inquiry-guide.md) · WBS 346, 347; 게시판 type=F |
| 고객지원 | 고객지원 > 서비스 플랫폼 관리(자료실) > WEB 문의 가이드 | WEB 문의 가이드 상세 | `/customer-support/web-inquiry-guide/:id` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/web-inquiry-guide__by-id.md) · WBS 346, 347; 게시판 type=F |
| 고객지원 | 고객지원 > 서비스 플랫폼 관리(자료실) > WEB 문의 가이드 | WEB 문의 가이드 수정 | `/customer-support/web-inquiry-guide/:id/edit` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/web-inquiry-guide__by-id__edit.md) · WBS 346, 347; 게시판 type=F |
| 고객지원 | 고객지원 > 서비스 플랫폼 관리(자료실) > WEB 문의 가이드 | WEB 문의 가이드 등록 | `/customer-support/web-inquiry-guide/new` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/web-inquiry-guide__new.md) · WBS 346, 347; 게시판 type=F |
| 고객지원 | 고객지원 > 서비스 플랫폼 관리(자료실) > SAP 자료실 | SAP 자료실 조회·관리 | `/customer-support/sap-resources` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/sap-resources.md) · WBS 348, 349; 게시판 type=D |
| 고객지원 | 고객지원 > 서비스 플랫폼 관리(자료실) > SAP 자료실 | SAP 자료실 상세 | `/customer-support/sap-resources/:id` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/sap-resources__by-id.md) · WBS 348, 349; 게시판 type=D |
| 고객지원 | 고객지원 > 서비스 플랫폼 관리(자료실) > SAP 자료실 | SAP 자료실 수정 | `/customer-support/sap-resources/:id/edit` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/sap-resources__by-id__edit.md) · WBS 348, 349; 게시판 type=D |
| 고객지원 | 고객지원 > 서비스 플랫폼 관리(자료실) > SAP 자료실 | SAP 자료실 등록 | `/customer-support/sap-resources/new` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/sap-resources__new.md) · WBS 348, 349; 게시판 type=D |
| 고객지원 | 고객지원 > 서비스 플랫폼 관리(자료실) > SAP 문의 가이드 | SAP 문의 가이드 조회·관리 | `/customer-support/sap-inquiry-guide` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/sap-inquiry-guide.md) · WBS 350, 351; 게시판 type=G |
| 고객지원 | 고객지원 > 서비스 플랫폼 관리(자료실) > SAP 문의 가이드 | SAP 문의 가이드 상세 | `/customer-support/sap-inquiry-guide/:id` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/sap-inquiry-guide__by-id.md) · WBS 350, 351; 게시판 type=G |
| 고객지원 | 고객지원 > 서비스 플랫폼 관리(자료실) > SAP 문의 가이드 | SAP 문의 가이드 수정 | `/customer-support/sap-inquiry-guide/:id/edit` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/sap-inquiry-guide__by-id__edit.md) · WBS 350, 351; 게시판 type=G |
| 고객지원 | 고객지원 > 서비스 플랫폼 관리(자료실) > SAP 문의 가이드 | SAP 문의 가이드 등록 | `/customer-support/sap-inquiry-guide/new` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/sap-inquiry-guide__new.md) · WBS 350, 351; 게시판 type=G |
| 고객지원 | 고객지원 > 서비스 플랫폼 관리(자료실) > NSAP 자료실 | NSAP 자료실 조회·관리 | `/customer-support/nsap-resources` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/nsap-resources.md) · WBS 352, 353; 게시판 type=E |
| 고객지원 | 고객지원 > 서비스 플랫폼 관리(자료실) > NSAP 자료실 | NSAP 자료실 상세 | `/customer-support/nsap-resources/:id` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/nsap-resources__by-id.md) · WBS 352, 353; 게시판 type=E |
| 고객지원 | 고객지원 > 서비스 플랫폼 관리(자료실) > NSAP 자료실 | NSAP 자료실 수정 | `/customer-support/nsap-resources/:id/edit` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/nsap-resources__by-id__edit.md) · WBS 352, 353; 게시판 type=E |
| 고객지원 | 고객지원 > 서비스 플랫폼 관리(자료실) > NSAP 자료실 | NSAP 자료실 등록 | `/customer-support/nsap-resources/new` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/nsap-resources__new.md) · WBS 352, 353; 게시판 type=E |
| 고객지원 | 고객지원 > 서비스 플랫폼 관리(자료실) > NSAP 문의 가이드 | NSAP 문의 가이드 조회·관리 | `/customer-support/nsap-inquiry-guide` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/nsap-inquiry-guide.md) · WBS 354, 355; 게시판 type=N |
| 고객지원 | 고객지원 > 서비스 플랫폼 관리(자료실) > NSAP 문의 가이드 | NSAP 문의 가이드 상세 | `/customer-support/nsap-inquiry-guide/:id` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/nsap-inquiry-guide__by-id.md) · WBS 354, 355; 게시판 type=N |
| 고객지원 | 고객지원 > 서비스 플랫폼 관리(자료실) > NSAP 문의 가이드 | NSAP 문의 가이드 수정 | `/customer-support/nsap-inquiry-guide/:id/edit` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/nsap-inquiry-guide__by-id__edit.md) · WBS 354, 355; 게시판 type=N |
| 고객지원 | 고객지원 > 서비스 플랫폼 관리(자료실) > NSAP 문의 가이드 | NSAP 문의 가이드 등록 | `/customer-support/nsap-inquiry-guide/new` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/nsap-inquiry-guide__new.md) · WBS 354, 355; 게시판 type=N |
| 고객지원 | 고객지원 > 서비스 플랫폼 관리(자료실) > 연동업체 소스 관리 | 연동업체 소스 관리 조회·관리 | `/customer-support/vendor-source-management` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/vendor-source-management.md) · WBS 356, 357; 게시판 type=H |
| 고객지원 | 고객지원 > 서비스 플랫폼 관리(자료실) > 연동업체 소스 관리 | 연동업체 소스 관리 상세 | `/customer-support/vendor-source-management/:id` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/vendor-source-management__by-id.md) · WBS 356, 357; 게시판 type=H |
| 고객지원 | 고객지원 > 서비스 플랫폼 관리(자료실) > 연동업체 소스 관리 | 연동업체 소스 관리 수정 | `/customer-support/vendor-source-management/:id/edit` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/vendor-source-management__by-id__edit.md) · WBS 356, 357; 게시판 type=H |
| 고객지원 | 고객지원 > 서비스 플랫폼 관리(자료실) > 연동업체 소스 관리 | 연동업체 소스 관리 등록 | `/customer-support/vendor-source-management/new` | 유지윤 | 검토 대기 | [문서](../manuals/customer-support/vendor-source-management__new.md) · WBS 356, 357; 게시판 type=H |

## 범위와 명칭 대응

- WBS 회사정보의 SSO·WEB-HOOK·요금제 변경내역·자동이체 이력은 회사 상세의 팝업/영역이며 별도 문서를 중복 생성하지 않았다. 전체 회원·회원 권한·회사정보 변경내역은 독립 경로 문서로 연결했다.
- 가입회원·가입사업장과 탈퇴회원·탈퇴사업장은 각각 현재의 가입 현황·탈퇴 현황 안에서 처리한다. 글로싸인 개인·회사·회원 비밀번호 초기화는 같은 경로의 탭이다.
- 세금계산서/과거 세금계산서의 statement 상세 경로와 document 쿼리 분기는 실제 라우트·화면 구현 기준으로 구분했다. 일괄 메일·문서 이력·XML 팝업은 해당 화면 안에 포함했다.
- WBS 보나뱅크 “국세청 전송 조회”(No.146·147)는 현재 메뉴 “국세청 신고 실패 조회”로 대응했다. 업무 범위 차이 여부는 보나뱅크 담당 검토가 필요하다.
- WBS 수정 태스크가 현재 상세 화면의 인라인 저장 또는 팝업으로 구현되어 있으면 존재하지 않는 수정 URL을 만들지 않았다. 예: 환불 관리, 미납 예외업체 관리, 오류 코드 관리.
- 게시판 유형: WEB 자료실 C, SAP 자료실 D, NSAP 자료실 E, WEB 문의 가이드 F, SAP 문의 가이드 G, 연동업체 소스 관리 H, NSAP 문의 가이드 N. 주석에 과거 mock 설명이 남아 있어도 현재 라우트 element와 Controller·Service 구현을 기준으로 작성했다.
- 선정 범위의 리다이렉트/별칭 전용 라우트는 없다. 같은 화면 컴포넌트를 쓰는 별개 업무 경로(예치금 상세/일별 예치금 상세, 회사 회원 조회/보나뱅크 회원 조회)는 경로마다 별도 문서로 작성했다.

## 선정 근거

- 사용자가 제공한 텍스트 SHA-256: `907a8a13484dab10bdd062cdccec221ac7330b9bc91f98774de6a2d984c6f147`. 행 번호는 원본 Excel 행 번호가 아니라 제공 텍스트의 행 번호다.
- 원본 SharePoint 통합문서를 직접 재열람하지 않았으며 사용자의 “WBS 탭” 설명과 제공 텍스트를 근거로 삼았다.
- [선정 태스크 CSV](wbs-tasks.csv), [페이지 조사 목록 CSV](wbs-pages.csv), [제외 경로 CSV](excluded-routes.csv).
- [API 계약](../references/api-contracts.md), [개발 DB 객체 계약](../references/database-contracts.md), [검증 범위와 후속 확인](../references/verification.md).

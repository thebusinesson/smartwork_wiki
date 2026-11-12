# SmartWork 전체 페이지별 관리자 매뉴얼

2026-11-11 현재 소스 <code>dc216b313</code>의 메뉴 설정과 실제 라우트를 대조했다. 업무 화면 433개에 문서를 연결했다. 기존 WBS 매뉴얼 134개를 재사용하고, 나머지 299개는 같은 7개 항목으로 작성했다. [전체 대응 CSV](all-pages.csv) · [기존 WBS 매뉴얼](wbs-pages.md)

아래의 **검토 대기**는 운영 담당의 문서 검토 상태다. 신규 문서는 현재 소스와 확인 가능한 개발·Demo DB 정의를 근거로 작성했다. 실제 브라우저 진입·표시를 확인한 범위는 표본 결과와 해당 매뉴얼의 7절에 기록했다. 역할별 접근과 저장·삭제·전송의 실제 결과는 각 환경의 운영 확인이 필요하다. [개발 DB 확인 범위](../references/all-pages-database.md) · [Demo DB 대조](../references/all-pages-demo.md) · [정확성·일관성 검증](../references/all-pages-accuracy.md) · [Playwright 표본 결과](../evidence/browser/all-pages-sample-2026-11-11.json)

현재 기준과 변경 내역은 최신 전수 검사에서 확인한다. [2026-11-12 최신 전수 대조](../references/all-pages-audit-2026-11-12.md) · [화면별 검증 CSV](all-pages-audit-2026-11-12.csv)

## 화면 목록

| 도메인 | 메뉴 경로 | 화면·유형 | 라우트 | 담당 | 상태 | 문서·비고 |
| --- | --- | --- | --- | --- | --- | --- |
| 직원 인증·내 계정·세션 | SmartWork 공통 > 로그인 | 로그인 · 인증 | `/` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/common/login.md) |
| 직원 인증·내 계정·세션 | SmartWork 공통 > 비밀번호 변경 | New-SmartWork 비밀번호 변경 · 인증 | `/change-password` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/common/change-password.md) |
| 직원 인증·내 계정·세션 | SmartWork 공통 > 초기 계정 설정 | 초기 계정 설정 · 인증 | `/initial-account-setup` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/common/initial-account-setup.md) |
| 직원 인증·내 계정·세션 | SmartWork 공통 > 비밀번호 재설정 | 비밀번호 재설정 · 인증 | `/forgot-password` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/common/forgot-password.md) |
| 직원 인증·내 계정·세션 | SmartWork 공통 > 대시보드 | 대시보드 · 대시보드 | `/dashboard` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/common/dashboard.md) |
| 직원 인증·내 계정·세션 | SmartWork 공통 > 조직도 | 조직도 · 조직 조회 | `/organization-chart` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/common/organization-chart.md) |
| 발행 장애·상태불일치·운영 일정 | SB 서비스관리 > 세금계산서 운영/관리 > 참조번호별 로그 조회 | 참조번호별 로그 조회 · 조회 | `/tax-operations/reference-log` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/tax-operations/reference-log.md) |
| 발행 장애·상태불일치·운영 일정 | SB 서비스관리 > 세금계산서 운영/관리 > 참조번호별 로그 조회 | 오류코드 상세보기 · 상세 | `/tax-operations/reference-log/:referenceNumber` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/tax-operations/reference-log__by-referenceNumber.md) |
| 발행 장애·상태불일치·운영 일정 | SB 서비스관리 > 세금계산서 운영/관리 > Error 발생 현황 | Error 발생 현황 · 조회 | `/tax-operations/error-status` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/tax-operations/error-status.md) |
| 발행 장애·상태불일치·운영 일정 | SB 서비스관리 > 세금계산서 운영/관리 > 사업자별 로그 조회 | 사업자별 로그 조회 · 이력 조회 | `/tax-operations/logs-by-business` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/tax-operations/logs-by-business.md) |
| 발행 장애·상태불일치·운영 일정 | SB 서비스관리 > 세금계산서 운영/관리 > 상태불일치 조회 | 상태불일치 조회 · 조회 | `/tax-operations/status-mismatch` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/tax-operations/status-mismatch.md) |
| 발행 장애·상태불일치·운영 일정 | SB 서비스관리 > 세금계산서 운영/관리 > 상태불일치 처리 등록 | 상태불일치 처리 등록 · 조회 | `/tax-operations/status-mismatch-register` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/tax-operations/status-mismatch-register.md) |
| 발행 장애·상태불일치·운영 일정 | SB 서비스관리 > 세금계산서 운영/관리 > 연동오류 로그조회 | 연동오류 로그조회 · 조회 | `/tax-operations/integration-error-logs` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/tax-operations/integration-error-logs.md) |
| 발행 장애·상태불일치·운영 일정 | SB 서비스관리 > 세금계산서 운영/관리 > 대량서비스 모니터링 | 대량서비스 모니터링 · 모니터링 | `/tax-operations/bulk-service-monitoring` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/tax-operations/bulk-service-monitoring.md) |
| 발행 장애·상태불일치·운영 일정 | SB 서비스관리 > 세금계산서 운영/관리 > 공휴일 관리 | 공휴일 관리 · 조회·관리 | `/tax-operations/holiday-management` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/tax-operations/holiday-management.md) |
| 발행 장애·상태불일치·운영 일정 | SB 서비스관리 > 세금계산서 운영/관리 > 합계표 마감일 관리 | 합계표 마감일 관리 · 조회·관리 | `/tax-operations/summary-deadline-management` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/tax-operations/summary-deadline-management.md) |
| 발행 장애·상태불일치·운영 일정 | SB 서비스관리 > 세금계산서 운영/관리 > 합계표 마감일 관리 | 합계표 마감일 등록 취소 · 등록 | `/tax-operations/summary-deadline-management/new` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/tax-operations/summary-deadline-management__new.md) |
| 발행 장애·상태불일치·운영 일정 | SB 서비스관리 > 세금계산서 운영/관리 > 지연발행일 관리 | 지연발행일 관리 · 조회·관리 | `/tax-operations/delayed-issuance-management` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/tax-operations/delayed-issuance-management.md) |
| 발행 장애·상태불일치·운영 일정 | SB 서비스관리 > 세금계산서 운영/관리 > 지연발행일 관리 | 지연발행일 등록 취소 · 등록 | `/tax-operations/delayed-issuance-management/new` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/tax-operations/delayed-issuance-management__new.md) |
| 발행 장애·상태불일치·운영 일정 | SB 서비스관리 > 세금계산서 운영/관리 > 참조/승인번호 변경 | 참조/승인번호 변경 · 조회·관리 | `/tax-operations/reference-approval-change` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/tax-operations/reference-approval-change.md) |
| 수신 변경·알림·다운로드 | SB 서비스관리 > 전자세금계산서 > 수신자 변경 이력 조회 | 수신자 변경 이력 조회 · 이력 조회 | `/tax-invoice/recipient-change-history` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/tax-invoice/recipient-change-history.md) |
| 문서 당사자와 발행·수신 조건 | SB 서비스관리 > 전자세금계산서 > 내 거래처 조회 | 내 거래처 조회 · 조회 | `/tax-invoice/my-customers` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/tax-invoice/my-customers.md) |
| 문서 당사자와 발행·수신 조건 | SB 서비스관리 > 전자세금계산서 > 담당자 권한 조회 | 담당자 권한 조회 · 조회 | `/tax-invoice/manager-permission` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/tax-invoice/manager-permission.md) |
| 문서 당사자와 발행·수신 조건 | SB 서비스관리 > 전자세금계산서 > 부서 조회 | 부서 조회 · 조회 | `/tax-invoice/departments` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/tax-invoice/departments.md) |
| 문서 당사자와 발행·수신 조건 | SB 서비스관리 > 전자세금계산서 > 지사(사업장) 조회 | 지사(사업장) 조회 · 조회 | `/tax-invoice/branches` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/tax-invoice/branches.md) |
| 문서 당사자와 발행·수신 조건 | SB 서비스관리 > 전자세금계산서 > 마감설정 조회 | 마감설정 조회 · 조회 | `/tax-invoice/closing-settings` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/tax-invoice/closing-settings.md) |
| 문서 당사자와 발행·수신 조건 | SB 서비스관리 > 전자세금계산서 > 매입 자동 승인 설정 조회 | 매입 자동 승인 설정 조회 · 조회 | `/tax-invoice/purchase-auto-approval-settings` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/tax-invoice/purchase-auto-approval-settings.md) |
| 수신 변경·알림·다운로드 | SB 서비스관리 > 전자세금계산서 > 알림발송 서비스 설정 조회 | 알림발송 서비스 설정 조회 · 조회 | `/tax-invoice/notification-service-settings` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/tax-invoice/notification-service-settings.md) |
| 수신 변경·알림·다운로드 | SB 서비스관리 > 전자세금계산서 > 알림발송 서비스 이용내역 | 알림발송 서비스 이용내역 · 이력 조회 | `/tax-invoice/notification-service-history` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/tax-invoice/notification-service-history.md) |
| 수신 변경·알림·다운로드 | SB 서비스관리 > 전자세금계산서 > 다운로드 요청/처리 조회 | 다운로드 요청/처리 조회 · 조회 | `/tax-invoice/download-requests` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/tax-invoice/download-requests.md) |
| 문서 당사자와 발행·수신 조건 | SB 서비스관리 > 전자세금계산서 > 비회원 수신 비밀번호 조회 | 비회원 수신 비밀번호 조회 · 조회 | `/tax-invoice/guest-password` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/tax-invoice/guest-password.md) |
| 문서 당사자와 발행·수신 조건 | SB 서비스관리 > 전자세금계산서 > 이벤트당첨(역매입대납) 업체 조회 | 이벤트당첨(역매입대납) 업체 조회 · 조회 | `/tax-invoice/event-winner-vendors` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/tax-invoice/event-winner-vendors.md) |
| 세금계산서·거래명세서 원문과 증빙 | SB 서비스관리 > 전자세금계산서 > 세금계산서 조회 | 세금계산서 조회 · 조회 | `/tax-invoice/tax-invoice` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/tax-invoice/tax-invoice.md) |
| 세금계산서·거래명세서 원문과 증빙 | SB 서비스관리 > 전자세금계산서 > 과거 세금계산서 조회 | 과거 세금계산서 조회 · 조회 | `/tax-invoice/legacy-tax-invoice` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/tax-invoice/legacy-tax-invoice.md) |
| 세금계산서·거래명세서 원문과 증빙 | SB 서비스관리 > 전자세금계산서 > 거래명세서 조회 | 거래명세서 조회 · 조회 | `/tax-invoice/transaction-statement` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/tax-invoice/transaction-statement.md) |
| 문서 당사자와 발행·수신 조건 | SB 서비스관리 > 전자세금계산서 > 비회원 수신설정 조회 | 비회원 수신설정 조회 · 조회 | `/tax-invoice/guest-reception-settings` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/tax-invoice/guest-reception-settings.md) |
| 세금계산서·거래명세서 원문과 증빙 | SB 서비스관리 > 전자세금계산서 > 지로세금계산서 조회 | 지로세금계산서 조회 · 조회 | `/tax-invoice/giro-tax-invoice` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/tax-invoice/giro-tax-invoice.md) |
| 세금계산서·거래명세서 원문과 증빙 | SB 서비스관리 > 전자세금계산서 > 지로 원본 다운로드 | 지로 원본 다운로드 · 조회 | `/tax-invoice/giro-original-download` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/tax-invoice/giro-original-download.md) |
| 전송 전·후 오류와 국세청 결과 | SB 서비스관리 > 전자세금계산서 > 국세청 전송 현황 | 국세청 전송 현황 · 조회 | `/tax-invoice/nts-transmission-status` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/tax-invoice/nts-transmission-status.md) |
| 전송 전·후 오류와 국세청 결과 | SB 서비스관리 > 전자세금계산서 > 국세청 전송 개별 조회 | 국세청 전송 개별 조회 · 조회 | `/tax-invoice/nts-transmission` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/tax-invoice/nts-transmission.md) |
| 수신 변경·알림·다운로드 | SB 서비스관리 > 전자세금계산서 > SMTP 전송결과 조회 | SMTP 전송결과 조회 · 결과 조회 | `/tax-invoice/smtp-transmission-results` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/tax-invoice/smtp-transmission-results.md) |
| 세금계산서·거래명세서 원문과 증빙 | SB 서비스관리 > 전자세금계산서 > 세금계산서 조회 | 세금계산서 조회 상세 · 상세 | `/tax-invoice/tax-invoice/:id` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/tax-invoice/tax-invoice__by-id.md) |
| 세금계산서·거래명세서 원문과 증빙 | SB 서비스관리 > 전자세금계산서 > 세금계산서 조회 | 세금계산서 조회 거래명세서 상세 · 거래명세서 상세 | `/tax-invoice/tax-invoice/statement/:id` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/tax-invoice/tax-invoice__statement__by-id.md) |
| 세금계산서·거래명세서 원문과 증빙 | SB 서비스관리 > 전자세금계산서 > 과거 세금계산서 조회 | 과거 세금계산서 조회 상세 · 상세 | `/tax-invoice/legacy-tax-invoice/:id` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/tax-invoice/legacy-tax-invoice__by-id.md) |
| 세금계산서·거래명세서 원문과 증빙 | SB 서비스관리 > 전자세금계산서 > 과거 세금계산서 조회 | 과거 세금계산서 조회 거래명세서 상세 · 거래명세서 상세 | `/tax-invoice/legacy-tax-invoice/statement/:id` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/tax-invoice/legacy-tax-invoice__statement__by-id.md) |
| 세금계산서·거래명세서 원문과 증빙 | SB 서비스관리 > 전자세금계산서 > 거래명세서 조회 | 거래명세서 조회 상세 · 상세 | `/tax-invoice/transaction-statement/:id` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/tax-invoice/transaction-statement__by-id.md) |
| 전송 대상과 일정·설정 | SB 서비스관리 > 국세청 전송 관리 > 국세청 전송 설정 관리 | 국세청 전송 설정 관리 · 조회 | `/nts-transmission/transmission-settings` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/nts-transmission/transmission-settings.md) |
| 전송 대상과 일정·설정 | SB 서비스관리 > 세금계산서 운영/관리 > 국세청전송 마감일 관리 | 국세청전송 마감일 관리 · 조회 | `/nts-transmission/transmission-deadlines` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/nts-transmission/transmission-deadlines.md) |
| 전송 전·후 오류와 국세청 결과 | SB 서비스관리 > 국세청 전송 관리 > 예약전송 모니터링 | 예약전송 모니터링 · 모니터링 | `/nts-transmission/scheduled-transmission-monitoring` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/nts-transmission/scheduled-transmission-monitoring.md) |
| 전송 전·후 오류와 국세청 결과 | SB 서비스관리 > 국세청 전송 관리 > 전송 전 오류 조회 | 전송 전 오류 조회 · 조회 | `/nts-transmission/pre-transmission-errors` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/nts-transmission/pre-transmission-errors.md) |
| 전송 전·후 오류와 국세청 결과 | SB 서비스관리 > 국세청 전송 관리 > 전송 전 오류 조회 | 전송 전 오류 조회 상세 · 상세 | `/nts-transmission/pre-transmission-errors/:issueId` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/nts-transmission/pre-transmission-errors__by-issueId.md) |
| 전송 전·후 오류와 국세청 결과 | SB 서비스관리 > 국세청 전송 관리 > 처리결과 오류 조회 | 처리결과 오류 조회 · 결과 조회 | `/nts-transmission/result-errors` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/nts-transmission/result-errors.md) |
| 전송 전·후 오류와 국세청 결과 | SB 서비스관리 > 국세청 전송 관리 > 일자별 전송결과 | 일자별 전송결과 · 결과 조회 | `/nts-transmission/transmission-results-by-date` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/nts-transmission/transmission-results-by-date.md) |
| 전송 대상과 일정·설정 | SB 서비스관리 > 국세청 전송 관리 > 전송 거부업체 조회 | 전송 거부업체 조회 · 조회 | `/nts-transmission/rejected-vendors` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/nts-transmission/rejected-vendors.md) |
| 전송 전·후 오류와 국세청 결과 | SB 서비스관리 > 국세청 전송 관리 > 국세청 수집 관리 조회 | 국세청 수집 관리 조회 · 조회 | `/nts-transmission/collection-management` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/nts-transmission/collection-management.md) |
| 전송 전·후 오류와 국세청 결과 | SB 서비스관리 > 국세청 전송 관리 > 예약전송 모니터링 | 예약전송 모니터링 상세 · 상세 | `/nts-transmission/scheduled-transmission-monitoring/detail` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/nts-transmission/scheduled-transmission-monitoring__detail.md) |
| 전송 전·후 오류와 국세청 결과 | SB 서비스관리 > 국세청 전송 관리 > 처리결과 오류 조회 | 처리결과 오류 조회 상세 · 상세 | `/nts-transmission/result-errors/:resultCode` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/nts-transmission/result-errors__by-resultCode.md) |
| 배너·키워드의 등록과 노출 | 광고/마케팅 운영 관리 > 광고배너 관리 > 광고배너 등록 및 조회 | 광고배너 등록 및 조회 · 조회·관리 | `/banner/management` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/banner/management.md) |
| 배너·키워드의 등록과 노출 | 광고/마케팅 운영 관리 > 광고배너 관리 > 광고배너 등록 및 조회 | 등록 취소 · 등록 | `/banner/management/new` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/banner/management__new.md) |
| 배너·키워드의 등록과 노출 | 광고/마케팅 운영 관리 > 광고배너 관리 > 광고배너 등록 및 조회 | 광고배너 등록 및 조회 상세 · 상세 | `/banner/management/:id` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/banner/management__by-id.md) |
| 배너·키워드의 등록과 노출 | 광고/마케팅 운영 관리 > 광고배너 관리 > 키워드 배너등록 | 키워드 배너등록 · 조회 | `/banner/keyword` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/banner/keyword.md) |
| 배너·키워드의 등록과 노출 | 광고/마케팅 운영 관리 > 광고배너 관리 > 키워드 배너등록 | 등록 · 등록 | `/banner/keyword/new` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/banner/keyword__new.md) |
| 배너·키워드의 등록과 노출 | 광고/마케팅 운영 관리 > 광고배너 관리 > 키워드 배너등록 | 키워드 배너등록 상세 · 상세 | `/banner/keyword/:id` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/banner/keyword__by-id.md) |
| 배너·키워드의 등록과 노출 | 광고/마케팅 운영 관리 > 광고배너 관리 > 신규 검색페이지별 검색어로그 | 신규 검색페이지별 검색어로그 · 조회 | `/banner/search-term-log` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/banner/search-term-log.md) |
| 광고 효과와 통계 | 광고/마케팅 운영 관리 > 배너 통계정보 > 배너광고 효과 측정 | 배너광고 효과 측정 · 조회 | `/banner/effect-measurement` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/banner/effect-measurement.md) |
| 배너·키워드의 등록과 노출 | 광고/마케팅 운영 관리 > 광고배너 관리 > 키워드 모수 조회 | 키워드 모수 조회 · 조회 | `/banner/keyword-volume` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/banner/keyword-volume.md) |
| 광고 효과와 통계 | 광고/마케팅 운영 관리 > 배너 통계정보 > 배너광고 통계 | 배너광고 통계 · 조회 | `/banner/daily-statistics` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/banner/daily-statistics.md) |
| 광고 효과와 통계 | 광고/마케팅 운영 관리 > 배너 통계정보 > 키워드 배너 광고 통계 | 키워드 배너 광고 통계 · 조회 | `/banner/keyword-daily-statistics` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/banner/keyword-daily-statistics.md) |
| 광고 효과와 통계 | 광고/마케팅 운영 관리 > 배너 통계정보 > 키워드 배너 광고 통계 | 키워드 배너광고 상세 통계 다운로드 · 상세 | `/banner/keyword-daily-statistics/:id` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/banner/keyword-daily-statistics__by-id.md) |
| 카페·SCM·사업장 운영 | SB 서비스관리 > SCM > 카페 조회 | 카페 조회 · 조회 | `/smartbill-scm/cafe` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/smartbill-scm/cafe.md) |
| 카페·SCM·사업장 운영 | SB 서비스관리 > SCM > 카페 조회 | 카페 조회 상세 · 상세 | `/smartbill-scm/cafe/:id` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/smartbill-scm/cafe__by-id.md) |
| 카페·SCM·사업장 운영 | SB 서비스관리 > SCM > SCM 조회 | SCM 조회 · 조회 | `/smartbill-scm/scm` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/smartbill-scm/scm.md) |
| 카페·SCM·사업장 운영 | SB 서비스관리 > SCM > SCM 조회 | SCM 조회 메인 수정 · 메인 수정 | `/smartbill-scm/scm/main-edit/:id` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/smartbill-scm/scm__main-edit__by-id.md) |
| 카페·SCM·사업장 운영 | SB 서비스관리 > SCM > SCM 조회 | SCM 조회 메뉴 관리 · 메뉴 관리 | `/smartbill-scm/scm/menu-management/:id` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/smartbill-scm/scm__menu-management__by-id.md) |
| 카페·SCM·사업장 운영 | SB 서비스관리 > SCM > SCM 조회 | SCM 조회 디자인 관리 · 디자인 관리 | `/smartbill-scm/scm/design-management/:id` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/smartbill-scm/scm__design-management__by-id.md) |
| 홈택스 수집·인증·오류 | SB 서비스관리 > 홈택스 DTI 수집 > 모니터링 | 모니터링 · 모니터링 | `/hometax-dti/monitoring` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/hometax-dti/monitoring.md) |
| 홈택스 수집·인증·오류 | SB 서비스관리 > 홈택스 DTI 수집 > 인증키 관리 | 인증키 관리 · 조회 | `/hometax-dti/auth-key` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/hometax-dti/auth-key.md) |
| 홈택스 수집·인증·오류 | SB 서비스관리 > 홈택스 DTI 수집 > 인증키 관리 | 인증키 관리 상세 · 상세 | `/hometax-dti/auth-key/:sbKey` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/hometax-dti/auth-key__by-sbKey.md) |
| 홈택스 수집·인증·오류 | SB 서비스관리 > 홈택스 DTI 수집 > 오류 로그 조회 | 오류 로그 조회 · 이력 조회 | `/hometax-dti/error-logs` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/hometax-dti/error-logs.md) |
| 홈택스 수집·인증·오류 | SB 서비스관리 > 홈택스 DTI 수집 > 인증서 만료일 관리 | 인증서 만료일 관리 · 조회 | `/hometax-dti/certificate-expiry` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/hometax-dti/certificate-expiry.md) |
| 홈택스 수집·인증·오류 | SB 서비스관리 > 홈택스 DTI 수집 > 인증서 등록 현황 조회 | 인증서 등록 현황 조회 · 조회 | `/hometax-dti/certificate-status` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/hometax-dti/certificate-status.md) |
| 홈택스 수집·인증·오류 | SB 서비스관리 > 홈택스 DTI 수집 > 인증서 로그인 실패 조회 | 인증서 로그인 실패 조회 · 조회 | `/hometax-dti/login-failures` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/hometax-dti/login-failures.md) |
| 홈택스 수집·인증·오류 | SB 서비스관리 > 홈택스 DTI 수집 > 이메일파싱 모니터링 | 이메일파싱 모니터링 · 모니터링 | `/hometax-dti/email-parsing` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/hometax-dti/email-parsing.md) |
| 위택스 납부대상 등록·이력 | SB 서비스관리 > 홈택스 DTI 수집 > Wetax 납부대상 관리 | Wetax 납부대상 관리 · 조회 | `/hometax-dti/wetax-payment-targets` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hometax-dti/wetax-payment-targets.md) |
| 위택스 납부대상 등록·이력 | SB 서비스관리 > 홈택스 DTI 수집 > Wetax 납부대상 관리 | Wetax 납부대상 관리 업로드 이력 · 업로드 이력 | `/hometax-dti/wetax-payment-targets/uploads/:uploadSeq` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hometax-dti/wetax-payment-targets__uploads__by-uploadSeq.md) |
| 보나뱅크 고객·문서·신고·공지 | SB 서비스관리 > 보나뱅크 > 회사 정보 | 회사 정보 · 조회 | `/bonabank/company` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/bonabank/company.md) |
| 보나뱅크 고객·문서·신고·공지 | SB 서비스관리 > 보나뱅크 > 회사 정보 | 회사 정보 상세 · 상세 | `/bonabank/company/:id` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/bonabank/company__by-id.md) |
| 보나뱅크 고객·문서·신고·공지 | SB 서비스관리 > 보나뱅크 > 회사 정보 | 회사 정보 변경 이력 · 변경 이력 | `/bonabank/company/:id/change-history` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/bonabank/company__by-id__change-history.md) |
| 보나뱅크 고객·문서·신고·공지 | SB 서비스관리 > 보나뱅크 > 회사 정보 | 회사 정보 회원 목록 · 회원 목록 | `/bonabank/company/:companyId/members` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/bonabank/company__by-companyId__members.md) |
| 보나뱅크 고객·문서·신고·공지 | SB 서비스관리 > 보나뱅크 > 회원 정보 | 회원 정보 · 조회 | `/bonabank/member` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/bonabank/member.md) |
| 보나뱅크 고객·문서·신고·공지 | SB 서비스관리 > 보나뱅크 > 회원 정보 | 회원 정보 상세 · 상세 | `/bonabank/member/:id` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/bonabank/member__by-id.md) |
| 보나뱅크 고객·문서·신고·공지 | SB 서비스관리 > 보나뱅크 > 세금계산서 조회 | 세금계산서 조회 · 조회 | `/bonabank/tax-invoice` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/bonabank/tax-invoice.md) |
| 보나뱅크 고객·문서·신고·공지 | SB 서비스관리 > 보나뱅크 > 세금계산서 조회 | 세금계산서 조회 상세 · 상세 | `/bonabank/tax-invoice/:dtiIdx` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/bonabank/tax-invoice__by-dtiIdx.md) |
| 보나뱅크 고객·문서·신고·공지 | SB 서비스관리 > 보나뱅크 > 세금계산서 통계 | 세금계산서 통계 · 조회 | `/bonabank/tax-invoice-statistics` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/bonabank/tax-invoice-statistics.md) |
| 보나뱅크 고객·문서·신고·공지 | SB 서비스관리 > 보나뱅크 > 국세청 신고 실패 조회 | 국세청 신고 실패 조회 · 조회 | `/bonabank/nts-failures` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/bonabank/nts-failures.md) |
| 보나뱅크 고객·문서·신고·공지 | SB 서비스관리 > 보나뱅크 > 공지사항 관리 | 공지사항 관리 · 조회 | `/bonabank/notices` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/bonabank/notices.md) |
| 보나뱅크 고객·문서·신고·공지 | SB 서비스관리 > 보나뱅크 > 공지사항 관리 | 공지사항 관리 등록 · 등록 | `/bonabank/notices/new` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/bonabank/notices__new.md) |
| 보나뱅크 고객·문서·신고·공지 | SB 서비스관리 > 보나뱅크 > 공지사항 관리 | 공지사항 관리 상세 · 상세 | `/bonabank/notices/:id` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/bonabank/notices__by-id.md) |
| 보나뱅크 고객·문서·신고·공지 | SB 서비스관리 > 보나뱅크 > 공지사항 관리 | 공지사항 관리 수정 · 수정 | `/bonabank/notices/:id/edit` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/bonabank/notices__by-id__edit.md) |
| 오픈스크랩 대상·수집과 결과 | SB 서비스관리 > 오픈스크랩 > 모니터링 | 모니터링 · 모니터링 | `/openscrap/monitoring` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/openscrap/monitoring.md) |
| 오픈스크랩 대상·수집과 결과 | SB 서비스관리 > 오픈스크랩 > 모니터링 | 모니터링 상세 · 상세 | `/openscrap/monitoring/:batchId` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/openscrap/monitoring__by-batchId.md) |
| 오픈스크랩 대상·수집과 결과 | SB 서비스관리 > 오픈스크랩 > 업체 관리 | 업체 관리 · 조회 | `/openscrap/vendors` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/openscrap/vendors.md) |
| 오픈스크랩 대상·수집과 결과 | SB 서비스관리 > 오픈스크랩 > 업체 관리 | 업체 관리 상세 · 상세 | `/openscrap/vendors/:id` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/openscrap/vendors__by-id.md) |
| 오픈스크랩 대상·수집과 결과 | SB 서비스관리 > 오픈스크랩 > 매출/매입 조회 | 매출/매입 조회 · 조회 | `/openscrap/sales-purchases` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/openscrap/sales-purchases.md) |
| 오픈스크랩 대상·수집과 결과 | SB 서비스관리 > 오픈스크랩 > 매출/매입 조회 | 매출/매입 조회 상세 · 상세 | `/openscrap/sales-purchases/:issueId` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/openscrap/sales-purchases__by-issueId.md) |
| 오픈스크랩 대상·수집과 결과 | SB 서비스관리 > 오픈스크랩 > 오류 로그 조회 | 오류 로그 조회 · 이력 조회 | `/openscrap/error-logs` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/openscrap/error-logs.md) |
| 입금·예치금·배분·취소·환불 | 서비스 현황 > 입금관리 > 입금 현황 조회 | 입금 현황 조회 · 조회 | `/payment/status` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/payment/status.md) |
| 입금·예치금·배분·취소·환불 | 서비스 현황 > 입금관리 > 입금 현황 조회 | 입금 현황 조회 상세 · 상세 | `/payment/status/:id` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/payment/status__by-id.md) |
| 입금·예치금·배분·취소·환불 | 서비스 현황 > 입금관리 > 예치금 관리 | 예치금 관리 · 조회 | `/payment/deposit` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/payment/deposit.md) |
| 입금·예치금·배분·취소·환불 | 서비스 현황 > 입금관리 > 예치금 관리 | 예치금 관리 상세 · 상세 | `/payment/deposit/:id` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/payment/deposit__by-id.md) |
| 입금·예치금·배분·취소·환불 | 서비스 현황 > 입금관리 > 일별 예치금 조회 | 일별 예치금 조회 · 조회 | `/payment/daily-deposit-inquiry` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/payment/daily-deposit-inquiry.md) |
| 입금·예치금·배분·취소·환불 | 서비스 현황 > 입금관리 > 일별 예치금 조회 | 일별 예치금 조회 상세 · 상세 | `/payment/daily-deposit-inquiry/:id` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/payment/daily-deposit-inquiry__by-id.md) |
| 입금·예치금·배분·취소·환불 | 서비스 현황 > 입금관리 > 벌크식계좌 입금 관리 | 벌크식계좌 입금 관리 · 조회 | `/payment/bulk-account-deposit` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/payment/bulk-account-deposit.md) |
| 입금·예치금·배분·취소·환불 | 서비스 현황 > 입금관리 > 벌크식계좌 입금 관리 | 벌크식계좌 입금 관리 상세 · 상세 | `/payment/bulk-account-deposit/:id` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/payment/bulk-account-deposit__by-id.md) |
| 입금·예치금·배분·취소·환불 | 서비스 현황 > 입금관리 > 본사 입금 관리 | 본사 입금 관리 · 조회·관리 | `/payment/head-office-deposit` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/payment/head-office-deposit.md) |
| 입금·예치금·배분·취소·환불 | 서비스 현황 > 입금관리 > 본사 입금 등록 | 본사 입금 등록 · 조회·관리 | `/payment/head-office-deposit-register` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/payment/head-office-deposit-register.md) |
| 입금·예치금·배분·취소·환불 | 서비스 현황 > 입금관리 > 본사 입금 등록 | 본사 입금 등록 · 상세 | `/payment/head-office-deposit-register/detail` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/payment/head-office-deposit-register__detail.md) |
| 입금·예치금·배분·취소·환불 | 서비스 현황 > 입금관리 > 본사 입금 관리 | 본사 입금 관리 상세 · 상세 | `/payment/head-office-deposit/:id` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/payment/head-office-deposit__by-id.md) |
| 입금·예치금·배분·취소·환불 | 서비스 현황 > 입금관리 > 단발성 입금 관리 | 단발성 입금 관리 · 조회 | `/payment/os-iv-deposit` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/payment/os-iv-deposit.md) |
| 입금·예치금·배분·취소·환불 | 서비스 현황 > 입금관리 > 단발성 매출·입금 등록 | 단발성 매출·입금 등록 · 조회 | `/payment/manual-transactions` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/payment/manual-transactions.md) |
| 입금·예치금·배분·취소·환불 | 서비스 현황 > 입금관리 > 단발성 매출·입금 등록 | 단발성 매출·입금 등록 · 등록 | `/payment/manual-transactions/new` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/payment/manual-transactions__new.md) |
| 입금·예치금·배분·취소·환불 | 서비스 현황 > 입금관리 > 단발성 매출·입금 등록 | 단발성 매출·입금 등록 수정 · 수정 | `/payment/manual-transactions/:id/edit` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/payment/manual-transactions__by-id__edit.md) |
| 입금·예치금·배분·취소·환불 | 서비스 현황 > 입금관리 > 단발성 매출·입금 등록 | 단발성 매출·입금 등록 상세 · 상세 | `/payment/manual-transactions/:id` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/payment/manual-transactions__by-id.md) |
| 입금·예치금·배분·취소·환불 | 서비스 현황 > 입금관리 > 단발성 거래처 관리 | 단발성 거래처 관리 · 조회 | `/payment/manual-clients` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/payment/manual-clients.md) |
| 입금·예치금·배분·취소·환불 | 서비스 현황 > 입금관리 > 단발성 거래처 관리 | 단발성 거래처 관리 등록 · 등록 | `/payment/manual-clients/new` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/payment/manual-clients__new.md) |
| 입금·예치금·배분·취소·환불 | 서비스 현황 > 입금관리 > 단발성 거래처 관리 | 단발성 거래처 관리 수정 · 수정 | `/payment/manual-clients/:id/edit` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/payment/manual-clients__by-id__edit.md) |
| 입금·예치금·배분·취소·환불 | 서비스 현황 > 입금관리 > 단발성 거래처 관리 | 단발성 거래처 관리 상세 · 상세 | `/payment/manual-clients/:id` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/payment/manual-clients__by-id.md) |
| CMS·카드 자동결제와 예외 | 서비스 현황 > 입금관리 > (EB13/EB14) CMS 계좌 관리 | (EB13/EB14) CMS 계좌 관리 · 조회·관리 | `/payment/cms-account` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/payment/cms-account.md) |
| CMS·카드 자동결제와 예외 | 서비스 현황 > 입금관리 > (EB13/EB14) CMS 계좌 관리 | (EB13/EB14) CMS 계좌 관리 조회·관리 · 조회·관리 | `/payment/cms-account/apply` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/payment/cms-account__apply.md) |
| CMS·카드 자동결제와 예외 | 서비스 현황 > 입금관리 > (EB13/EB14) CMS 계좌 관리 | EB13 계좌신청 상세 다운로드 · 상세 | `/payment/cms-account/eb13/:id` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/payment/cms-account__eb13__by-id.md) |
| CMS·카드 자동결제와 예외 | 서비스 현황 > 입금관리 > (EB13/EB14) CMS 계좌 관리 | (EB13/EB14) CMS 계좌 관리 신청 정보 · 신청 정보 | `/payment/cms-account/eb14/application/:eb13Idx` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/payment/cms-account__eb14__application__by-eb13Idx.md) |
| CMS·카드 자동결제와 예외 | 서비스 현황 > 입금관리 > (EB13/EB14) CMS 계좌 관리 | (EB13/EB14) CMS 계좌 관리 처리 결과 · 처리 결과 | `/payment/cms-account/eb14/result/:eb14Idx` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/payment/cms-account__eb14__result__by-eb14Idx.md) |
| CMS·카드 자동결제와 예외 | 서비스 현황 > 입금관리 > (EB13/EB14) CMS 계좌 관리 | (EB13/EB14) CMS 계좌 관리 상세 · 상세 | `/payment/cms-account/eb14/file/:eb14Idx` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/payment/cms-account__eb14__file__by-eb14Idx.md) |
| CMS·카드 자동결제와 예외 | 서비스 현황 > 입금관리 > (EB13/EB14) CMS 계좌 관리 | (EB13/EB14) CMS 계좌 관리 상세 · 상세 | `/payment/cms-account/eb14/file-preview/:eb14Idx` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/payment/cms-account__eb14__file-preview__by-eb14Idx.md) |
| CMS·카드 자동결제와 예외 | 서비스 현황 > 입금관리 > (EB13/EB14) CMS 계좌 관리 | (EB13/EB14) CMS 계좌 관리 등록 · 등록 | `/payment/cms-account/eb14/upload/:eb13Idx/new` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/payment/cms-account__eb14__upload__by-eb13Idx__new.md) |
| CMS·카드 자동결제와 예외 | 서비스 현황 > 입금관리 > (EB13/EB14) CMS 계좌 관리 | 파일 수정 · 수정 | `/payment/cms-account/eb14/upload/:eb14Idx/edit` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/payment/cms-account__eb14__upload__by-eb14Idx__edit.md) |
| CMS·카드 자동결제와 예외 | 서비스 현황 > 입금관리 > (EB11) CMS 통합 변경내역 반영 | (EB11) CMS 통합 변경내역 반영 · 조회·관리 | `/payment/cms-integration` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/payment/cms-integration.md) |
| CMS·카드 자동결제와 예외 | 서비스 현황 > 입금관리 > (EB11) CMS 통합 변경내역 반영 | (EB11) CMS 통합 변경내역 반영 상세 · 상세 | `/payment/cms-integration/:fileId` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/payment/cms-integration__by-fileId.md) |
| CMS·카드 자동결제와 예외 | 서비스 현황 > 입금관리 > (EB21/EB22) CMS 자동이체 관리 | (EB21/EB22) CMS 자동이체 관리 · 조회·관리 | `/payment/cms-withdrawal-request` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/payment/cms-withdrawal-request.md) |
| CMS·카드 자동결제와 예외 | 서비스 현황 > 입금관리 > (EB21/EB22) CMS 자동이체 관리 | (EB21/EB22) CMS 자동이체 관리 조회 · 조회 | `/payment/cms-withdrawal-request/eb21/apply` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/payment/cms-withdrawal-request__eb21__apply.md) |
| CMS·카드 자동결제와 예외 | 서비스 현황 > 입금관리 > (EB21/EB22) CMS 자동이체 관리 | (EB21/EB22) CMS 자동이체 관리 상세 · 상세 | `/payment/cms-withdrawal-request/eb21/:id` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/payment/cms-withdrawal-request__eb21__by-id.md) |
| CMS·카드 자동결제와 예외 | 서비스 현황 > 입금관리 > (EB21/EB22) CMS 자동이체 관리 | (EB21/EB22) CMS 자동이체 관리 신청 정보 · 신청 정보 | `/payment/cms-withdrawal-request/eb22/:id/application` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/payment/cms-withdrawal-request__eb22__by-id__application.md) |
| CMS·카드 자동결제와 예외 | 서비스 현황 > 입금관리 > (EB21/EB22) CMS 자동이체 관리 | (EB21/EB22) CMS 자동이체 관리 처리 결과 · 처리 결과 | `/payment/cms-withdrawal-request/eb22/:id/result` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/payment/cms-withdrawal-request__eb22__by-id__result.md) |
| CMS·카드 자동결제와 예외 | 서비스 현황 > 입금관리 > (EB21/EB22) CMS 자동이체 관리 | (EB21/EB22) CMS 자동이체 관리 상세 · 상세 | `/payment/cms-withdrawal-request/eb22/file/:eb22Idx` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/payment/cms-withdrawal-request__eb22__file__by-eb22Idx.md) |
| CMS·카드 자동결제와 예외 | 서비스 현황 > 입금관리 > (EB21/EB22) CMS 자동이체 관리 | (EB21/EB22) CMS 자동이체 관리 상세 · 상세 | `/payment/cms-withdrawal-request/eb22/file-preview/:eb22Idx` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/payment/cms-withdrawal-request__eb22__file-preview__by-eb22Idx.md) |
| CMS·카드 자동결제와 예외 | 서비스 현황 > 입금관리 > (EB21/EB22) CMS 자동이체 관리 | (EB21/EB22) CMS 자동이체 관리 등록 · 등록 | `/payment/cms-withdrawal-request/eb22/upload/:ea21Idx/new` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/payment/cms-withdrawal-request__eb22__upload__by-ea21Idx__new.md) |
| CMS·카드 자동결제와 예외 | 서비스 현황 > 입금관리 > (EB21/EB22) CMS 자동이체 관리 | 결과 파일 수정 업로드 · 수정 | `/payment/cms-withdrawal-request/eb22/upload/:eb22Idx/edit` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/payment/cms-withdrawal-request__eb22__upload__by-eb22Idx__edit.md) |
| CMS·카드 자동결제와 예외 | 서비스 현황 > 입금관리 > 업체별 CMS 계좌 현황 | 업체별 CMS 계좌 현황 · 조회 | `/payment/cms-account-status` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/payment/cms-account-status.md) |
| 입금·예치금·배분·취소·환불 | 서비스 현황 > 입금관리 > 무통장입금 취소내역 조회 | 무통장입금 취소내역 조회 · 조회 | `/payment/bank-transfer-cancel` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/payment/bank-transfer-cancel.md) |
| 입금·예치금·배분·취소·환불 | 서비스 현황 > 입금관리 > 환불 관리 | 환불 관리 · 조회 | `/payment/refund-management` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/payment/refund-management.md) |
| 입금·예치금·배분·취소·환불 | 서비스 현황 > 입금관리 > 환불 관리 | 환불 등록 · 등록 | `/payment/refund-management/new` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/payment/refund-management__new.md) |
| 입금·예치금·배분·취소·환불 | 서비스 현황 > 입금관리 > 환불 관리 | 환불 관리 조회 · 조회 | `/payment/refund-management/inquiry` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/payment/refund-management__inquiry.md) |
| 입금·예치금·배분·취소·환불 | 서비스 현황 > 입금관리 > 환불 관리 | 환불요청상세내역 · 상세 | `/payment/refund-management/:refundNo` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/payment/refund-management__by-refundNo.md) |
| CMS·카드 자동결제와 예외 | 서비스 현황 > 입금관리 > 출금신청 예외처리 관리 | 출금신청 예외처리 관리 · 조회 | `/payment/withdrawal-exception` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/payment/withdrawal-exception.md) |
| CMS·카드 자동결제와 예외 | 서비스 현황 > 입금관리 > 출금신청 예외처리 관리 | 출금신청 예외처리 등록 · 등록 | `/payment/withdrawal-exception/new` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/payment/withdrawal-exception__new.md) |
| CMS·카드 자동결제와 예외 | 서비스 현황 > 입금관리 > 출금신청 예외처리 관리 | 출금신청 예외처리 관리 등록 · 등록 | `/payment/withdrawal-exception/bulk` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/payment/withdrawal-exception__bulk.md) |
| CMS·카드 자동결제와 예외 | 서비스 현황 > 입금관리 > 출금신청 예외처리 관리 | 출금신청 예외처리 관리 상세 · 상세 | `/payment/withdrawal-exception/:serviceCode/:comNo` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/payment/withdrawal-exception__by-serviceCode__by-comNo.md) |
| CMS·카드 자동결제와 예외 | 서비스 현황 > 입금관리 > 신용카드 자동결제 승인요청 | 신용카드 자동결제 승인요청 · 조회 | `/payment/credit-card-auto-payment` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/payment/credit-card-auto-payment.md) |
| CMS·카드 자동결제와 예외 | 서비스 현황 > 입금관리 > 신용카드 자동결제 승인요청 | 신용카드 자동결제 승인요청 상세 · 상세 | `/payment/credit-card-auto-payment/:withdrawalMonth/:division` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/payment/credit-card-auto-payment__by-withdrawalMonth__by-division.md) |
| 전자계약 원문·이용과 접근 | SB 서비스관리 > 전자계약 > 전자계약 조회 | 전자계약 조회 · 조회 | `/electronic-contract/electronic-contract-inquiry` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/electronic-contract/electronic-contract-inquiry.md) |
| 전자계약 원문·이용과 접근 | SB 서비스관리 > 전자계약 > 담당자 권한 조회 | 담당자 권한 조회 · 조회 | `/electronic-contract/manager-access-info` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/electronic-contract/manager-access-info.md) |
| 전자계약 원문·이용과 접근 | SB 서비스관리 > 전자계약 > 전자계약 용량 조회 | 전자계약 용량 조회 · 조회 | `/electronic-contract/electronic-contract-capacity` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/electronic-contract/electronic-contract-capacity.md) |
| 전자계약 원문·이용과 접근 | SB 서비스관리 > 전자계약 > 다운로드 조회 | 다운로드 조회 · 이력 조회 | `/electronic-contract/download-history` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/electronic-contract/download-history.md) |
| 전자계약 원문·이용과 접근 | SB 서비스관리 > 전자계약 > 단방향 이용 고객 조회 | 단방향 이용 고객 조회 · 조회 | `/electronic-contract/one-way-user` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/electronic-contract/one-way-user.md) |
| 전자계약 원문·이용과 접근 | SB 서비스관리 > 전자계약 > 단방향 이용 고객 조회 | 단방향 이용 고객 조회 등록 · 등록 | `/electronic-contract/one-way-user/new` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/electronic-contract/one-way-user__new.md) |
| 전자계약 원문·이용과 접근 | SB 서비스관리 > 전자계약 > 삼양사 사용내역 조회 | 삼양사 사용내역 조회 · 이력 조회 | `/electronic-contract/samyang-usage-history` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/electronic-contract/samyang-usage-history.md) |
| 계약 연동 업체·인증서와 장애 | SB 서비스관리 > 전자계약 > 연동업체 관리 | 연동업체 관리 · 조회 | `/electronic-contract/linked-vendor-manage` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/electronic-contract/linked-vendor-manage.md) |
| 계약 연동 업체·인증서와 장애 | SB 서비스관리 > 전자계약 > 연동업체 관리 | 전자계약 연동업체 등록 · 등록 | `/electronic-contract/linked-vendor-manage/new` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/electronic-contract/linked-vendor-manage__new.md) |
| 계약 연동 업체·인증서와 장애 | SB 서비스관리 > 전자계약 > 스마트빌 인증서 관리 | 스마트빌 인증서 관리 · 조회·관리 | `/electronic-contract/smartbill-certificate` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/electronic-contract/smartbill-certificate.md) |
| 계약 연동 업체·인증서와 장애 | SB 서비스관리 > 전자계약 > 스마트빌 인증서 관리 | 스마트빌 인증서 관리 등록 · 등록 | `/electronic-contract/smartbill-certificate/new` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/electronic-contract/smartbill-certificate__new.md) |
| 계약 연동 업체·인증서와 장애 | SB 서비스관리 > 전자계약 > 전자계약 오류 조회 | 전자계약 오류 조회 · 조회 | `/electronic-contract/error-inquiry` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/electronic-contract/error-inquiry.md) |
| 전자계약 원문·이용과 접근 | SB 서비스관리 > 전자계약 > 참조번호별 로그 조회 | 참조번호별 로그 조회 · 조회 | `/electronic-contract/reference-log` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/electronic-contract/reference-log.md) |
| 계약 연동 업체·인증서와 장애 | SB 서비스관리 > 전자계약 > 연동업체 장애관리 | 연동업체 장애관리 · 조회 | `/electronic-contract/linked-vendor-failure` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/electronic-contract/linked-vendor-failure.md) |
| 계약 연동 업체·인증서와 장애 | SB 서비스관리 > 전자계약 > 연동업체 장애관리 | 연동업체 장애관리 상세 · 상세 | `/electronic-contract/linked-vendor-failure/detail` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/electronic-contract/linked-vendor-failure__detail.md) |
| 전자계약 원문·이용과 접근 | SB 서비스관리 > 전자계약 > 전자계약 조회 | 전자계약 조회 상세 · 상세 | `/electronic-contract/electronic-contract-inquiry/:dctNo` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/electronic-contract/electronic-contract-inquiry__by-dctNo.md) |
| 전자계약 원문·이용과 접근 | SB 서비스관리 > 전자계약 > 전자계약 용량 조회 | 전자계약 용량 조회 상세 · 상세 | `/electronic-contract/electronic-contract-capacity/:comNo` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/electronic-contract/electronic-contract-capacity__by-comNo.md) |
| 전자계약 원문·이용과 접근 | SB 서비스관리 > 전자계약 > 단방향 이용 고객 조회 | 단방향 이용 고객 조회 상세 · 상세 | `/electronic-contract/one-way-user/:companyNo/:processIdNo` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/electronic-contract/one-way-user__by-companyNo__by-processIdNo.md) |
| 계약 연동 업체·인증서와 장애 | SB 서비스관리 > 전자계약 > 연동업체 관리 | 연동업체 관리 상세 · 상세 | `/electronic-contract/linked-vendor-manage/:comNo` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/electronic-contract/linked-vendor-manage__by-comNo.md) |
| 계약 연동 업체·인증서와 장애 | SB 서비스관리 > 전자계약 > 스마트빌 인증서 관리 | 스마트빌 인증서 관리 상세 · 상세 | `/electronic-contract/smartbill-certificate/:certificateSerial` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/electronic-contract/smartbill-certificate__by-certificateSerial.md) |
| 계약 연동 업체·인증서와 장애 | SB 서비스관리 > 전자계약 > 전자계약 오류 조회 | 전자계약 오류 조회 상세 · 상세 | `/electronic-contract/error-inquiry/:dctNo` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/electronic-contract/error-inquiry__by-dctNo.md) |
| 월·일·서비스별 이용과 집계 | 서비스 현황 > 통계 정보 > 월별 이용 현황 (세금, 계약) | 월별 이용 현황 (세금, 계약) · 조회 | `/statistics/monthly-usage` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/statistics/monthly-usage.md) |
| 월·일·서비스별 이용과 집계 | 서비스 현황 > 통계 정보 > 월별 이용 현황 (세금, 계약) | 월별 이용 현황 (세금, 계약) 일별 세금계산서 · 일별 세금계산서 | `/statistics/monthly-usage/daily-tax-invoice` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/statistics/monthly-usage__daily-tax-invoice.md) |
| 월·일·서비스별 이용과 집계 | 서비스 현황 > 통계 정보 > 월별 이용 현황 (세금, 계약) | 월별 이용 현황 (세금, 계약) 일별 전자계약 · 일별 전자계약 | `/statistics/monthly-usage/daily-electronic-contract` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/statistics/monthly-usage__daily-electronic-contract.md) |
| 고객·매출·연동과 외부 호출 지표 | 서비스 현황 > 통계 정보 > 허브업체 이용 현황 | 허브업체 이용 현황 · 조회 | `/statistics/hub-company-usage` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/statistics/hub-company-usage.md) |
| 고객·매출·연동과 외부 호출 지표 | 서비스 현황 > 통계 정보 > 허브업체 이용 현황 | 허브업체 이용 현황 상세 · 상세 | `/statistics/hub-company-usage/:id` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/statistics/hub-company-usage__by-id.md) |
| 월·일·서비스별 이용과 집계 | 서비스 현황 > 통계 정보 > 월별 세금계산서 이용 현황 (일반) | 월별 세금계산서 이용 현황 (일반) · 조회 | `/statistics/monthly-tax-invoice-usage` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/statistics/monthly-tax-invoice-usage.md) |
| 월·일·서비스별 이용과 집계 | 서비스 현황 > 통계 정보 > 월별 세금계산서 이용 현황 (일반) | 월별 세금계산서 이용 현황 (일반) 조회 · 조회 | `/statistics/monthly-tax-invoice-usage/daily` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/statistics/monthly-tax-invoice-usage__daily.md) |
| 월·일·서비스별 이용과 집계 | 서비스 현황 > 통계 정보 > 매출/매입 이용 현황 | 매출/매입 이용 현황 · 조회 | `/statistics/sales-purchases-usage` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/statistics/sales-purchases-usage.md) |
| 월·일·서비스별 이용과 집계 | 서비스 현황 > 통계 정보 > 세금계산서 일별 데이터 집계 | 세금계산서 일별 데이터 집계 · 조회 | `/statistics/daily-tax-invoice-aggregate` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/statistics/daily-tax-invoice-aggregate.md) |
| 고객·매출·연동과 외부 호출 지표 | 서비스 현황 > 통계 정보 > 세금계산서 매출 분석 다운로드 | 세금계산서 매출 분석 다운로드 · 조회 | `/statistics/dti-sales-analysis` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/statistics/dti-sales-analysis.md) |
| 고객·매출·연동과 외부 호출 지표 | 서비스 현황 > 통계 정보 > 웹→연동 인식 사업장 발행현황 | 웹→연동 인식 사업장 발행현황 · 조회 | `/statistics/web-link-issue` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/statistics/web-link-issue.md) |
| 고객·매출·연동과 외부 호출 지표 | 서비스 현황 > 통계 정보 > 월별 고객·매출 통합 현황 | 월별 고객·매출 통합 현황 · 조회 | `/statistics/monthly-customer-sales` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/statistics/monthly-customer-sales.md) |
| 고객·매출·연동과 외부 호출 지표 | 서비스 현황 > 통계 정보 > 월별 웹·연동 고객 현황 | 월별 웹·연동 고객 현황 · 조회 | `/statistics/monthly-web-link-customer` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/statistics/monthly-web-link-customer.md) |
| 월·일·서비스별 이용과 집계 | 서비스 현황 > 통계 정보 > 전자계약 서비스 월간 지표 | 전자계약 서비스 월간 지표 · 조회 | `/statistics/dct-monthly-metrics` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/statistics/dct-monthly-metrics.md) |
| 고객·매출·연동과 외부 호출 지표 | 서비스 현황 > 통계 정보 > 청구 월별 웹·연동 고객 사용 데이터 | 청구 월별 웹·연동 고객 사용 데이터 · 조회 | `/statistics/billing-monthly-web-link-usage` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/statistics/billing-monthly-web-link-usage.md) |
| 고객·매출·연동과 외부 호출 지표 | 서비스 현황 > 통계 정보 > 신규 연동 고객 등록 현황 | 신규 연동 고객 등록 현황 · 조회 | `/statistics/new-link-registration` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/statistics/new-link-registration.md) |
| 고객·매출·연동과 외부 호출 지표 | 서비스 현황 > 통계 정보 > 보나뱅크 발행 현황 | 보나뱅크 발행 현황 · 조회 | `/statistics/bonabank-issue` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/statistics/bonabank-issue.md) |
| 고객·매출·연동과 외부 호출 지표 | 서비스 현황 > 통계 정보 > 서비스별 매출액 조회 | 서비스별 매출액 조회 · 조회 | `/statistics/service-sales` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/statistics/service-sales.md) |
| 고객·매출·연동과 외부 호출 지표 | 서비스 현황 > 통계 정보 > OpenAPI 사용현황 | OpenAPI 사용현황 · 조회 | `/statistics/open-api-usage` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/statistics/open-api-usage.md) |
| 고객·매출·연동과 외부 호출 지표 | 서비스 현황 > 통계 정보 > WORKPLACE 월별 OAPI 사용량 집계 | WORKPLACE 월별 OAPI 사용량 집계 · 조회 | `/statistics/workplace-monthly-oapi-usage` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/statistics/workplace-monthly-oapi-usage.md) |
| 고객·매출·연동과 외부 호출 지표 | 서비스 현황 > 통계 정보 > 현금영수증 틸코블렛 API 호출 현황 | 현금영수증 틸코블렛 API 호출 현황 · 조회 | `/statistics/cash-receipt-tilko-bullet-api-call` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/statistics/cash-receipt-tilko-bullet-api-call.md) |
| 고객·매출·연동과 외부 호출 지표 | 서비스 현황 > 통계 정보 > 매출 데이터 다운로드 | 매출 데이터 다운로드 · 조회 | `/statistics/sales-data-download` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/statistics/sales-data-download.md) |
| 매출채권과 회수·대손 기록 | 서비스 현황 > 통계 정보 > 매출채권 데이터 다운로드 | 매출채권 데이터 다운로드 · 조회 | `/statistics/ar-data-download` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/statistics/ar-data-download.md) |
| 고객·매출·연동과 외부 호출 지표 | 서비스 현황 > 통계 정보 > 휴폐업 업체 요약 | 휴폐업 업체 요약 · 조회 | `/statistics/suspended-closed-company-summary` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/statistics/suspended-closed-company-summary.md) |
| 고객·매출·연동과 외부 호출 지표 | 서비스 현황 > 통계 정보 > 휴폐업 업체 리스트 | 휴폐업 업체 리스트 · 조회 | `/statistics/suspended-closed-company` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/statistics/suspended-closed-company.md) |
| 매출채권과 회수·대손 기록 | 서비스 현황 > 채권 관리 > 매출 채권 현황 다운로드 | 매출 채권 현황 다운로드 · 조회 | `/ar-management/account-receivable-status-download` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/ar-management/account-receivable-status-download.md) |
| 매출채권과 회수·대손 기록 | 서비스 현황 > 채권 관리 > 매출 채권 현황 다운로드 | 매출 채권 현황 다운로드 개별 등록 · 개별 등록 | `/ar-management/account-receivable-status-download/write-off-registration/individual` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/ar-management/account-receivable-status-download__write-off-registration__individual.md) |
| 매출채권과 회수·대손 기록 | 서비스 현황 > 채권 관리 > 매출 채권 현황 다운로드 | 매출 채권 현황 다운로드 처리 결과 · 처리 결과 | `/ar-management/account-receivable-status-download/write-off-registration/individual/result` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/ar-management/account-receivable-status-download__write-off-registration__individual__result.md) |
| 매출채권과 회수·대손 기록 | 서비스 현황 > 채권 관리 > 매출 채권 현황 다운로드 | 매출 채권 현황 다운로드 업로드 이력 · 업로드 이력 | `/ar-management/account-receivable-status-download/write-off-registration/uploads` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/ar-management/account-receivable-status-download__write-off-registration__uploads.md) |
| 매출채권과 회수·대손 기록 | 서비스 현황 > 채권 관리 > 매출 채권 현황 다운로드 | 매출 채권 현황 다운로드 처리 결과 · 처리 결과 | `/ar-management/account-receivable-status-download/write-off-registration/uploads/:uploadId/result` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/ar-management/account-receivable-status-download__write-off-registration__uploads__by-uploadId__result.md) |
| 매출채권과 회수·대손 기록 | 서비스 현황 > 채권 관리 > 매출 채권 현황 다운로드 | 매출 채권 현황 다운로드 업로드 이력 · 업로드 이력 | `/ar-management/account-receivable-status-download/write-off-registration/uploads/:uploadId` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/ar-management/account-receivable-status-download__write-off-registration__uploads__by-uploadId.md) |
| 연동 영업과 프로젝트 완료 | 연동 협업 관리 > 연동 협업 관리 > 영업 관리 | 영업 관리 · 조회 | `/hub-collab/sales-management` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-collab/sales-management.md) |
| 연동 영업과 프로젝트 완료 | 연동 협업 관리 > 연동 협업 관리 > 영업 관리 | 영업 관리 업체 등록 · 등록 | `/hub-collab/sales-management/new` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-collab/sales-management__new.md) |
| 연동 영업과 프로젝트 완료 | 연동 협업 관리 > 연동 협업 관리 > 영업 관리 | 영업 관리 업체 등록 · 수정 | `/hub-collab/sales-management/:id/edit` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-collab/sales-management__by-id__edit.md) |
| 연동 영업과 프로젝트 완료 | 연동 협업 관리 > 연동 협업 관리 > 영업 관리 | 영업 관리 상세 · 상세 | `/hub-collab/sales-management/:id` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-collab/sales-management__by-id.md) |
| 연동 영업과 프로젝트 완료 | 연동 협업 관리 > 연동 협업 관리 > 프로젝트 완료 관리 | 프로젝트 완료 관리 · 조회 | `/hub-collab/project-completion` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-collab/project-completion.md) |
| 시스템 키·벌크계좌·업체 연결 설정 | 연동 협업 관리 > 연동 협업 관리 > System Key 관리 | System Key 관리 · 조회 | `/hub-collab/system-key-management` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-collab/system-key-management.md) |
| 시스템 키·벌크계좌·업체 연결 설정 | 연동 협업 관리 > 연동 협업 관리 > System Key 관리 | System Key 관리 등록 · 등록 | `/hub-collab/system-key-management/new` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-collab/system-key-management__new.md) |
| 시스템 키·벌크계좌·업체 연결 설정 | 연동 협업 관리 > 연동 협업 관리 > System Key 관리 | System Key 관리 상세 · 상세 | `/hub-collab/system-key-management/:id` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-collab/system-key-management__by-id.md) |
| 시스템 키·벌크계좌·업체 연결 설정 | 연동 협업 관리 > 연동 협업 관리 > System Key 관리 | System Key 관리 수정 · 수정 | `/hub-collab/system-key-management/:id/edit` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-collab/system-key-management__by-id__edit.md) |
| 시스템 키·벌크계좌·업체 연결 설정 | 연동 협업 관리 > 연동 협업 관리 > 벌크계좌 관리 | 벌크계좌 관리 · 조회 | `/hub-collab/bulk-account-management` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-collab/bulk-account-management.md) |
| 시스템 키·벌크계좌·업체 연결 설정 | 연동 협업 관리 > 연동 협업 관리 > 벌크계좌 관리 | 벌크계좌 관리 등록 · 등록 | `/hub-collab/bulk-account-management/new` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-collab/bulk-account-management__new.md) |
| 시스템 키·벌크계좌·업체 연결 설정 | 연동 협업 관리 > 연동 협업 관리 > 벌크계좌 관리 | 벌크계좌 관리 상세 · 상세 | `/hub-collab/bulk-account-management/:id` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-collab/bulk-account-management__by-id.md) |
| 시스템 키·벌크계좌·업체 연결 설정 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > 허브업체 관리 | 허브업체 관리 · 조회 | `/hub-vendor/hub-vendor-management` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-vendor/hub-vendor-management.md) |
| 시스템 키·벌크계좌·업체 연결 설정 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > 허브업체 관리 | 허브업체 관리 등록 · 등록 | `/hub-vendor/hub-vendor-management/new` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-vendor/hub-vendor-management__new.md) |
| 시스템 키·벌크계좌·업체 연결 설정 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > 허브업체 관리 | 허브업체 관리 상세 · 상세 | `/hub-vendor/hub-vendor-management/:id` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-vendor/hub-vendor-management__by-id.md) |
| 시스템 키·벌크계좌·업체 연결 설정 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > 허브업체 관리 | 허브업체 관리 수정 · 수정 | `/hub-vendor/hub-vendor-management/:id/edit` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-vendor/hub-vendor-management__by-id__edit.md) |
| 시스템 키·벌크계좌·업체 연결 설정 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > 허브업체 관리 | 허브업체 체크리스트 다운로드 · 체크리스트 | `/hub-vendor/hub-vendor-management/:id/checklist` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-vendor/hub-vendor-management__by-id__checklist.md) |
| 시스템 키·벌크계좌·업체 연결 설정 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > [구연동]연동업체 관리 | [구연동]연동업체 관리 · 조회 | `/hub-vendor/vendor-management` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-vendor/vendor-management.md) |
| 시스템 키·벌크계좌·업체 연결 설정 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > [구연동]연동업체 관리 | 연동업체 등록 · 등록 | `/hub-vendor/vendor-management/new` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-vendor/vendor-management__new.md) |
| 시스템 키·벌크계좌·업체 연결 설정 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > [구연동]연동업체 관리 | [구연동]연동업체 관리 일괄 수정 · 일괄 수정 | `/hub-vendor/vendor-management/bulk-edit` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-vendor/vendor-management__bulk-edit.md) |
| 시스템 키·벌크계좌·업체 연결 설정 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > [구연동]연동업체 관리 | [구연동]연동업체 관리 상세 · 상세 | `/hub-vendor/vendor-management/:id` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-vendor/vendor-management__by-id.md) |
| 시스템 키·벌크계좌·업체 연결 설정 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > [구연동]연동업체 관리 | 연동업체 수정 · 수정 | `/hub-vendor/vendor-management/:id/edit` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-vendor/vendor-management__by-id__edit.md) |
| 시스템 키·벌크계좌·업체 연결 설정 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > [구연동]연동업체 관리 | [구연동]연동업체 관리 체크리스트 · 체크리스트 | `/hub-vendor/vendor-management/:id/checklist` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-vendor/vendor-management__by-id__checklist.md) |
| 시스템 키·벌크계좌·업체 연결 설정 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > [차세대]연동업체 관리 | [차세대]연동업체 관리 · 조회 | `/hub-vendor/nextgen-vendor-management` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-vendor/nextgen-vendor-management.md) |
| 시스템 키·벌크계좌·업체 연결 설정 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > [차세대]연동업체 관리 | 차세대 연동업체 등록 · 등록 | `/hub-vendor/nextgen-vendor-management/new` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-vendor/nextgen-vendor-management__new.md) |
| 시스템 키·벌크계좌·업체 연결 설정 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > [차세대]연동업체 관리 | [차세대]연동업체 관리 일괄 수정 · 일괄 수정 | `/hub-vendor/nextgen-vendor-management/bulk-edit` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-vendor/nextgen-vendor-management__bulk-edit.md) |
| 시스템 키·벌크계좌·업체 연결 설정 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > [차세대]연동업체 관리 | [차세대]연동업체 관리 상세 · 상세 | `/hub-vendor/nextgen-vendor-management/:id` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-vendor/nextgen-vendor-management__by-id.md) |
| 시스템 키·벌크계좌·업체 연결 설정 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > 조직도/비회원 연동 사용 조회 | 조직도/비회원 연동 사용 조회 · 조회 | `/hub-vendor/orgchart-guest-integration` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-vendor/orgchart-guest-integration.md) |
| 시스템 키·벌크계좌·업체 연결 설정 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > 연동플랫폼 통합관리 | 연동플랫폼 통합관리 · 조회 | `/hub-vendor/platform-management` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-vendor/platform-management.md) |
| 시스템 키·벌크계좌·업체 연결 설정 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > 연동플랫폼 통합관리 | 연동플랫폼 통합관리 상세 · 상세 | `/hub-vendor/platform-management/:platformId` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-vendor/platform-management__by-platformId.md) |
| 시스템 키·벌크계좌·업체 연결 설정 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > 연동플랫폼 통합관리 | 연동플랫폼 통합관리 상세 · 상세 | `/hub-vendor/platform-management/system-port/:portId` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-vendor/platform-management__system-port__by-portId.md) |
| 시스템 키·벌크계좌·업체 연결 설정 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > 첨부파일 연동업체관리 | 첨부파일 연동업체관리 · 조회 | `/hub-vendor/attachment-vendor-management` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-vendor/attachment-vendor-management.md) |
| 시스템 키·벌크계좌·업체 연결 설정 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > 첨부파일 연동업체관리 | 연동 등록 업체 · 등록 | `/hub-vendor/attachment-vendor-management/new` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-vendor/attachment-vendor-management__new.md) |
| 시스템 키·벌크계좌·업체 연결 설정 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > 첨부파일 연동업체관리 | 첨부파일 연동업체관리 상세 · 상세 | `/hub-vendor/attachment-vendor-management/:vendorId` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-vendor/attachment-vendor-management__by-vendorId.md) |
| 시스템 키·벌크계좌·업체 연결 설정 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > OpenAPI 허브 관리 | OpenAPI 허브 관리 · 조회 | `/hub-vendor/openapi-hub-management` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-vendor/openapi-hub-management.md) |
| 시스템 키·벌크계좌·업체 연결 설정 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > OpenAPI 허브 관리 | OAPI 허브 등록 · 등록 | `/hub-vendor/openapi-hub-management/new` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-vendor/openapi-hub-management__new.md) |
| 시스템 키·벌크계좌·업체 연결 설정 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > OpenAPI 허브 관리 | OpenAPI 허브 관리 상세 · 상세 | `/hub-vendor/openapi-hub-management/:hubId` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-vendor/openapi-hub-management__by-hubId.md) |
| 연동 문의·점검·라우팅·복구 | 연동 서비스 관리 > 연동 서비스 관리 > 연동업체 문의 처리 | 연동업체 문의 처리 · 조회 | `/hub-service/inquiry-management` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-service/inquiry-management.md) |
| 연동 문의·점검·라우팅·복구 | 연동 서비스 관리 > 연동 서비스 관리 > 연동업체 문의 처리 | 연동업체 문의 처리 상세 · 상세 | `/hub-service/inquiry-management/:id` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-service/inquiry-management__by-id.md) |
| 연동 문의·점검·라우팅·복구 | 연동 서비스 관리 > 연동 서비스 관리 > 연동업체 문의 처리 | 연동업체 문의 처리 등록 · 수정 | `/hub-service/inquiry-management/:id/edit` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-service/inquiry-management__by-id__edit.md) |
| 연동 문의·점검·라우팅·복구 | 연동 서비스 관리 > 연동 서비스 관리 > 연동업체 문의 처리 | 연동업체 문의 처리 등록 · 등록 | `/hub-service/inquiry-management/new` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-service/inquiry-management__new.md) |
| 서비스 공지 메일과 발송 이력 | 연동 서비스 관리 > 서비스 공지 메일관리 > 메일 발송 업체 관리 | 메일 발송 업체 관리 · 조회 | `/hub-service/service-notice-email` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-service/service-notice-email.md) |
| 서비스 공지 메일과 발송 이력 | 연동 서비스 관리 > 서비스 공지 메일관리 > 메일 발송 업체 관리 | 메일 발송 업체 관리 등록 · 등록 | `/hub-service/service-notice-email/new` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-service/service-notice-email__new.md) |
| 서비스 공지 메일과 발송 이력 | 연동 서비스 관리 > 서비스 공지 메일관리 > 메일 발송 업체 관리 | 메일 발송 업체 관리 상세 · 상세 | `/hub-service/service-notice-email/:id` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-service/service-notice-email__by-id.md) |
| 서비스 공지 메일과 발송 이력 | 연동 서비스 관리 > 서비스 공지 메일관리 > 고객 이메일 발송 | 고객 이메일 발송 · 조회 | `/hub-service/service-notice-email/customer-email-send` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-service/service-notice-email__customer-email-send.md) |
| 서비스 공지 메일과 발송 이력 | 연동 서비스 관리 > 서비스 공지 메일관리 > 메일 발송 고객 정보 조회 | 메일 발송 고객 정보 조회 · 이력 조회 | `/hub-service/service-notice-email/send-history` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-service/service-notice-email__send-history.md) |
| 연동 문의·점검·라우팅·복구 | 연동 서비스 관리 > 연동 서비스 관리 > 허브업체 서비스 점검 관리 | 허브업체 서비스 점검 관리 · 조회 | `/hub-service/maintenance` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-service/maintenance.md) |
| 연동 문의·점검·라우팅·복구 | 연동 서비스 관리 > 연동 서비스 관리 > 허브업체 서비스 점검 관리 | 허브업체 서비스 점검 관리 상세 · 상세 | `/hub-service/maintenance/:id` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-service/maintenance__by-id.md) |
| OpenAPI 인증·로그·인증서 구분 | 연동 서비스 관리 > 연동 서비스 관리 > OpenAPI 로그 조회 | OpenAPI 로그 조회 · 조회 | `/hub-service/openapi-log` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-service/openapi-log.md) |
| OpenAPI 인증·로그·인증서 구분 | 연동 서비스 관리 > 연동 서비스 관리 > OpenAPI 로그 조회 | OpenAPI 로그 조회 상세 · 상세 | `/hub-service/openapi-log/:id` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-service/openapi-log__by-id.md) |
| OpenAPI 인증·로그·인증서 구분 | 연동 서비스 관리 > 연동 서비스 관리 > OpenAPI 인증토큰 관리 | OpenAPI 인증토큰 관리 · 조회 | `/hub-service/openapi-auth-token` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-service/openapi-auth-token.md) |
| OpenAPI 인증·로그·인증서 구분 | 연동 서비스 관리 > 연동 서비스 관리 > 인증서 OID 관리 | 인증서 OID 관리 · 조회 | `/hub-service/certificate-oid` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-service/certificate-oid.md) |
| OpenAPI 인증·로그·인증서 구분 | 연동 서비스 관리 > 연동 서비스 관리 > 인증서 OID 관리 | 인증서 OID 등록 · 등록 | `/hub-service/certificate-oid/new` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-service/certificate-oid__new.md) |
| OpenAPI 인증·로그·인증서 구분 | 연동 서비스 관리 > 연동 서비스 관리 > 인증서 OID 관리 | 인증서 OID 관리 상세 · 상세 | `/hub-service/certificate-oid/:id` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-service/certificate-oid__by-id.md) |
| 연동 문의·점검·라우팅·복구 | 연동 서비스 관리 > 연동 서비스 관리 > 연동업체 라우팅 일괄 변경 | 연동업체 라우팅 일괄 변경 · 조회·관리 | `/hub-service/vendor-routing-bulk-change` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-service/vendor-routing-bulk-change.md) |
| 연동 문의·점검·라우팅·복구 | 연동 서비스 관리 > 연동 서비스 관리 > [구연동] 라우팅 예외 관리 | [구연동] 라우팅 예외 관리 · 조회·관리 | `/hub-service/routing-exception` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-service/routing-exception.md) |
| 연동 문의·점검·라우팅·복구 | 연동 서비스 관리 > 연동 서비스 관리 > 자동이체 예외 설정 | 자동이체 예외 설정 · 조회 | `/hub-service/auto-transfer-exception` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-service/auto-transfer-exception.md) |
| 연동 문의·점검·라우팅·복구 | 연동 서비스 관리 > 연동 서비스 관리 > 자동이체 예외 설정 | 자동이체 예외업체 등록 · 등록 | `/hub-service/auto-transfer-exception/new` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-service/auto-transfer-exception__new.md) |
| 연동 문의·점검·라우팅·복구 | 연동 서비스 관리 > 연동 서비스 관리 > 자동이체 예외 설정 | 자동이체 예외 설정 상세 · 상세 | `/hub-service/auto-transfer-exception/:id` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-service/auto-transfer-exception__by-id.md) |
| 연동 문의·점검·라우팅·복구 | 연동 서비스 관리 > 연동 서비스 관리 > [구연동] 복구솔루션 | [구연동] 복구솔루션 · 조회 | `/hub-service/status-change-recovery` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-service/status-change-recovery.md) |
| 연동 문의·점검·라우팅·복구 | 연동 서비스 관리 > 연동 서비스 관리 > [차세대] 복구솔루션 | [차세대] 복구솔루션 · 연계 진입 | `/hub-service/new-integration-recovery` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-service/new-integration-recovery.md) |
| OpenAPI 인증·로그·인증서 구분 | 연동 서비스 관리 > 연동 서비스 관리 > [차세대] 발행전문 조회 | [차세대] 발행전문 조회 · 조회 | `/hub-service/nextgen-issuance-inquiry` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/hub-service/nextgen-issuance-inquiry.md) |
| 구매확인서 원문과 품목·참조 | SB 서비스관리 > 구매확인서 > 구매확인서 조회 | 구매확인서 조회 · 조회 | `/purchase-confirmation/purchase-confirmation` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/purchase-confirmation/purchase-confirmation.md) |
| 송신거래 약정키와 식별자 | SB 서비스관리 > 구매확인서 > 송신거래 약정키 등록 | 송신거래 약정키 등록 · 등록 | `/purchase-confirmation/transmission-agreement-key/new` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/purchase-confirmation/transmission-agreement-key__new.md) |
| 송신거래 약정키와 식별자 | SB 서비스관리 > 구매확인서 > 송신거래 약정키 등록 | 송신거래 약정키 등록 · 조회·관리 | `/purchase-confirmation/transmission-agreement-key` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/purchase-confirmation/transmission-agreement-key.md) |
| 송신거래 약정키와 식별자 | SB 서비스관리 > 구매확인서 > 식별자 정보 등록 | 식별자 정보 등록 · 등록 | `/purchase-confirmation/identifier-key/new` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/purchase-confirmation/identifier-key__new.md) |
| 송신거래 약정키와 식별자 | SB 서비스관리 > 구매확인서 > 식별자 정보 등록 | 식별자 정보 등록 · 조회·관리 | `/purchase-confirmation/identifier-key` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/purchase-confirmation/identifier-key.md) |
| 구매확인서 원문과 품목·참조 | SB 서비스관리 > 구매확인서 > 구매확인서 조회 | 구매확인서 조회 상세 · 상세 | `/purchase-confirmation/purchase-confirmation/:id` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/purchase-confirmation/purchase-confirmation__by-id.md) |
| 송신거래 약정키와 식별자 | SB 서비스관리 > 구매확인서 > 송신거래 약정키 등록 | 송신거래 약정키 등록 상세 · 상세 | `/purchase-confirmation/transmission-agreement-key/:sridkey` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/purchase-confirmation/transmission-agreement-key__by-sridkey.md) |
| 송신거래 약정키와 식별자 | SB 서비스관리 > 구매확인서 > 식별자 정보 등록 | 상세페이지 URL · 상세 | `/purchase-confirmation/identifier-key/:interIdx` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/purchase-confirmation/identifier-key__by-interIdx.md) |
| 채권잔액 요청·확인·회신 | SB 서비스관리 > 채권잔액 확인 서비스 > 채권잔액 확인서 조회 | 채권잔액 확인서 조회 · 조회 | `/bond-service/bond-balance-inquiry` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/bond-service/bond-balance-inquiry.md) |
| 채권잔액 요청·확인·회신 | SB 서비스관리 > 채권잔액 확인 서비스 > 담당자 권한 조회 | 담당자 권한 조회 · 조회 | `/bond-service/drc-right` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/bond-service/drc-right.md) |
| 채권잔액 요청·확인·회신 | SB 서비스관리 > 채권잔액 확인 서비스 > 연동업체 관리 | 연동업체 관리 · 조회 | `/bond-service/drc-company-link` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/bond-service/drc-company-link.md) |
| 채권잔액 요청·확인·회신 | SB 서비스관리 > 채권잔액 확인 서비스 > 연동업체 관리 | 연동업체 관리 등록 · 등록 | `/bond-service/drc-company-link/new` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/bond-service/drc-company-link__new.md) |
| 채권잔액 요청·확인·회신 | SB 서비스관리 > 채권잔액 확인 서비스 > 연동 로그 조회 | 연동 로그 조회 · 조회 | `/bond-service/integration-log` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/bond-service/integration-log.md) |
| 채권잔액 요청·확인·회신 | SB 서비스관리 > 채권잔액 확인 서비스 > 연동업체 장애 관리 | 연동업체 장애 관리 · 조회 | `/bond-service/integration-partner-error` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/bond-service/integration-partner-error.md) |
| 채권잔액 요청·확인·회신 | SB 서비스관리 > 채권잔액 확인 서비스 > 연동업체 장애 관리 | 연동업체 장애 관리 상세 · 상세 | `/bond-service/integration-partner-error/detail` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/bond-service/integration-partner-error__detail.md) |
| 채권잔액 요청·확인·회신 | SB 서비스관리 > 채권잔액 확인 서비스 > 채권잔액 전송 관리 | 채권잔액 전송 관리 · 조회 | `/bond-service/receivable-balance-transfer` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/bond-service/receivable-balance-transfer.md) |
| 채권잔액 요청·확인·회신 | SB 서비스관리 > 채권잔액 확인 서비스 > 채권잔액 확인서 조회 | 채권잔액 확인서 조회 상세 · 상세 | `/bond-service/bond-balance-inquiry/:drcNo` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/bond-service/bond-balance-inquiry__by-drcNo.md) |
| 채권잔액 요청·확인·회신 | SB 서비스관리 > 채권잔액 확인 서비스 > 담당자 권한 조회 | 담당자 권한 조회 상세 · 상세 | `/bond-service/drc-right/:comNo` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/bond-service/drc-right__by-comNo.md) |
| 채권잔액 요청·확인·회신 | SB 서비스관리 > 채권잔액 확인 서비스 > 연동업체 관리 | 연동업체 관리 상세 · 상세 | `/bond-service/drc-company-link/:comNo` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/bond-service/drc-company-link__by-comNo.md) |
| 채권잔액 요청·확인·회신 | SB 서비스관리 > 채권잔액 확인 서비스 > 채권잔액 전송 관리 | 채권잔액 전송 관리 상세 · 상세 | `/bond-service/receivable-balance-transfer/:conversationId` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/bond-service/receivable-balance-transfer__by-conversationId.md) |
| 이용료 청구·일일 정산·영수 발행 | 서비스 현황 > 요금관리 > 일별 이용료 발행 | 일별 이용료 발행 · 조회·관리 | `/billing-management/daily-usage-fee-billing` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/billing-management/daily-usage-fee-billing.md) |
| 이용료 청구·일일 정산·영수 발행 | 서비스 현황 > 요금관리 > 결제 방식별 일일 정산 | 결제 방식별 일일 정산 · 조회 | `/billing-management/daily-settlement-by-payment` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/billing-management/daily-settlement-by-payment.md) |
| 이용료 청구·일일 정산·영수 발행 | 서비스 현황 > 요금관리 > 영수 대량 발행 | 영수 대량 발행 · 조회 | `/billing-management/bulk-receipt-issue` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/billing-management/bulk-receipt-issue.md) |
| 이용료 청구·일일 정산·영수 발행 | 서비스 현황 > 요금관리 > 영수 대량 발행 오류 로그 조회 | 영수 대량 발행 오류 로그 조회 · 이력 조회 | `/billing-management/bulk-receipt-issue-logs` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/billing-management/bulk-receipt-issue-logs.md) |
| 이용료 청구·일일 정산·영수 발행 | 서비스 현황 > 요금관리 > KT 대납 리스트 | KT 대납 리스트 · 조회 | `/billing-management/kt-proxy-payment-list` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/billing-management/kt-proxy-payment-list.md) |
| 이용료 청구·일일 정산·영수 발행 | 서비스 현황 > 요금관리 > 클로버 관리 | 클로버 관리 · 조회 | `/billing-management/clover-charge` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/billing-management/clover-charge.md) |
| 이용료 청구·일일 정산·영수 발행 | 서비스 현황 > 요금관리 > 클로버 관리 | 클로버 관리 조회 · 조회 | `/billing-management/clover-charge/input` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/billing-management/clover-charge__input.md) |
| 이용료 청구·일일 정산·영수 발행 | 서비스 현황 > 요금관리 > 클로버 관리 | 클로버 관리 상세 · 상세 | `/billing-management/clover-charge/:businessNumber` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/billing-management/clover-charge__by-businessNumber.md) |
| CMS·카드 자동결제와 예외 | 서비스 현황 > 미납 예외업체 관리 > 미납 예외업체 관리 | 미납 예외업체 관리 · 조회·관리 | `/service-overview/unpaid-exception-manager` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/service-overview/unpaid-exception-manager.md) |
| 가입·탈퇴와 휴폐업 | SB 고객관리 > 스마트빌 이용 현황 > 가입 현황 | 가입 현황 · 조회 | `/smartbill-status/status` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/smartbill-status/status.md) |
| 가입·탈퇴와 휴폐업 | SB 고객관리 > 스마트빌 이용 현황 > 탈퇴 현황 | 탈퇴 현황 · 조회 | `/smartbill-status/withdrawal-status` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/smartbill-status/withdrawal-status.md) |
| 글로싸인 조직·회원·인증 지원 | SB 고객관리 > 글로싸인 엔터프라이즈 > 회사 정보 | 회사 정보 · 조회 | `/glosign-enterprise/companies` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/glosign-enterprise/companies.md) |
| 글로싸인 조직·회원·인증 지원 | SB 고객관리 > 글로싸인 엔터프라이즈 > 회원 정보 | 회원 정보 · 조회 | `/glosign-enterprise/members` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/glosign-enterprise/members.md) |
| 글로싸인 조직·회원·인증 지원 | SB 고객관리 > 글로싸인 엔터프라이즈 > 열람인증 초기화 | 열람인증 초기화 · 조회·관리 | `/glosign-enterprise/personal-password-reset` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/glosign-enterprise/personal-password-reset.md) |
| 글로싸인 조직·회원·인증 지원 | SB 고객관리 > 글로싸인 엔터프라이즈 > 회사 정보 | 회사 정보 상세 · 상세 | `/glosign-enterprise/companies/:orgSeq` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/glosign-enterprise/companies__by-orgSeq.md) |
| 글로싸인 조직·회원·인증 지원 | SB 고객관리 > 글로싸인 엔터프라이즈 > 비밀번호 초기화 | 비밀번호 초기화 · 조회 | `/glosign-enterprise/status` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/glosign-enterprise/status.md) |
| 회사·회원·서비스 권한 | SB 고객관리 > 스마트빌 회원·회사정보 관리 > 회원 정보 | 회원 정보 · 조회 | `/member-management/member` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/member-management/member.md) |
| 회사·회원·서비스 권한 | SB 고객관리 > 스마트빌 회원·회사정보 관리 > 회원 정보 | 회원 정보 상세 · 상세 | `/member-management/member/:id` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/member-management/member__by-id.md) |
| 회사·회원·서비스 권한 | SB 고객관리 > 스마트빌 회원·회사정보 관리 > 회원 정보 | 회원 정보 변경 이력 · 변경 이력 | `/member-management/member/:id/change-history` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/member-management/member__by-id__change-history.md) |
| 회사·회원·서비스 권한 | SB 고객관리 > 스마트빌 회원·회사정보 관리 > 대량 회원가입 | 대량 회원가입 · 조회 | `/member-management/member/bulk-registration` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/member-management/member__bulk-registration.md) |
| 회사·회원·서비스 권한 | SB 고객관리 > 스마트빌 회원·회사정보 관리 > 아이디/비밀번호 관리 | 아이디/비밀번호 관리 · 조회 | `/member-management/id-password` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/member-management/id-password.md) |
| 회사·회원·서비스 권한 | SB 고객관리 > 스마트빌 회원·회사정보 관리 > 회원 비밀번호 초기화 | 회원 비밀번호 초기화 · 조회·관리 | `/member-management/id-password/password-reset` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/member-management/id-password__password-reset.md) |
| 회사·회원·서비스 권한 | SB 고객관리 > 스마트빌 회원·회사정보 관리 > 회원 이메일 다운로드 | 회원 이메일 다운로드 · 조회 | `/member-management/email-download` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/member-management/email-download.md) |
| 회사·회원·서비스 권한 | SB 고객관리 > 스마트빌 회원·회사정보 관리 > 회원 이메일 다운로드 | 회원 이메일 다운로드 내역 조회 · 이력 | `/member-management/email-download/history` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/member-management/email-download__history.md) |
| 업체·비회원 예외와 SMS 수신거부 | SB 고객관리 > 예외 관리 > [업체]예외 처리 정보 | [업체]예외 처리 정보 · 조회 | `/exception-management/exception-vendor` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/exception-management/exception-vendor.md) |
| 업체·비회원 예외와 SMS 수신거부 | SB 고객관리 > 예외 관리 > [업체]예외 처리 정보 | [업체]예외 처리 정보 등록 · 등록 | `/exception-management/exception-vendor/new` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/exception-management/exception-vendor__new.md) |
| 업체·비회원 예외와 SMS 수신거부 | SB 고객관리 > 예외 관리 > [업체]예외 처리 정보 | [업체]예외 처리 정보 상세 · 상세 | `/exception-management/exception-vendor/:businessNumber` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/exception-management/exception-vendor__by-businessNumber.md) |
| 업체·비회원 예외와 SMS 수신거부 | SB 고객관리 > 예외 관리 > [비회원]예외 처리 정보 | [비회원]예외 처리 정보 · 조회 | `/exception-management/exception-non-member` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/exception-management/exception-non-member.md) |
| 업체·비회원 예외와 SMS 수신거부 | SB 고객관리 > 예외 관리 > [비회원]예외 처리 정보 | [비회원]예외 처리 정보 등록 · 등록 | `/exception-management/exception-non-member/register` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/exception-management/exception-non-member__register.md) |
| 업체·비회원 예외와 SMS 수신거부 | SB 고객관리 > 예외 관리 > SMS 수신거부 관리 | SMS 수신거부 관리 · 조회·관리 | `/exception-management/sms-opt-out` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/exception-management/sms-opt-out.md) |
| 회사·회원·서비스 권한 | SB 고객관리 > 스마트빌 회원·회사정보 관리 > 회사 정보 | 회사 정보 · 조회 | `/company-management/company-info` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/company-management/company-info.md) |
| 회사·회원·서비스 권한 | SB 고객관리 > 스마트빌 회원·회사정보 관리 > 회사 정보 | 회사 정보 상세 · 상세 | `/company-management/company-info/:id` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/company-management/company-info__by-id.md) |
| 회사·회원·서비스 권한 | SB 고객관리 > 스마트빌 회원·회사정보 관리 > 회사 정보 | 회사 정보 변경 이력 · 변경 이력 | `/company-management/company-info/:id/change-history` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/company-management/company-info__by-id__change-history.md) |
| 회사·회원·서비스 권한 | SB 고객관리 > 스마트빌 회원·회사정보 관리 > 회사 정보 | 회사 정보 회원 목록 · 회원 목록 | `/company-management/company-info/:companyId/members` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/company-management/company-info__by-companyId__members.md) |
| 회사·회원·서비스 권한 | SB 고객관리 > 스마트빌 회원·회사정보 관리 > 회사 정보 | 회사 정보 상세 · 상세 | `/company-management/company-info/:companyKey/member-permissions` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/company-management/company-info__by-companyKey__member-permissions.md) |
| 회사·회원·서비스 권한 | SB 고객관리 > 스마트빌 회원·회사정보 관리 > 스마트빌 가입조회 | 스마트빌 가입조회 · 조회 | `/company-management/registration-inquiry` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/company-management/registration-inquiry.md) |
| 회사·회원·서비스 권한 | SB 고객관리 > 스마트빌 회원·회사정보 관리 > 스마트빌 가입조회 | 가입문의 상세 다운로드 · 상세 | `/company-management/registration-inquiry/:uploadId` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/company-management/registration-inquiry__by-uploadId.md) |
| 가입·탈퇴와 휴폐업 | SB 고객관리 > 스마트빌 회원·회사정보 관리 > 휴폐업 조회 | 휴폐업 조회 · 조회·관리 | `/company-management/suspended-closed-inquiry` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/company-management/suspended-closed-inquiry.md) |
| 오류 접수·처리와 분류 | SB 운영관리 > 오류 관리 > 전체 오류 조회/처리 | 전체 오류 조회/처리 · 조회 | `/error-management/error-reports` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/error-management/error-reports.md) |
| 오류 접수·처리와 분류 | SB 운영관리 > 오류 관리 > 오류 접수/등록 | 오류 접수/등록 · 조회·관리 | `/error-management/error-reports/new` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/error-management/error-reports__new.md) |
| 오류 접수·처리와 분류 | SB 운영관리 > 오류 관리 > 전체 오류 조회/처리 | 전체 오류 조회/처리 상세 · 상세 | `/error-management/error-reports/:id` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/error-management/error-reports__by-id.md) |
| 오류 접수·처리와 분류 | SB 운영관리 > 오류 관리 > 전체 오류 조회/처리 | 전체 오류 조회/처리 · 처리 | `/error-management/error-reports/:id/process` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/error-management/error-reports__by-id__process.md) |
| 오류 접수·처리와 분류 | SB 운영관리 > 오류 관리 > 오류 코드 관리 | 오류 코드 관리 · 조회 | `/error-management/error-code-management` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/error-management/error-code-management.md) |
| 오류 접수·처리와 분류 | SB 운영관리 > 오류 관리 > 오류 코드 관리 | 오류 코드 관리 상세 · 상세 | `/error-management/error-code-management/:errorCode` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/error-management/error-code-management__by-errorCode.md) |
| 오류 접수·처리와 분류 | SB 운영관리 > 오류 관리 > 오류 코드 관리 | 오류 코드 등록 · 등록 | `/error-management/error-code-management/new` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/error-management/error-code-management__new.md) |
| 업무·개선 요청·식별자·접속 기록 | SB 운영관리 > 시스템 관리 > 업무개선 및 요청리스트 | 업무개선 및 요청리스트 · 조회 | `/system-management/request-improve` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/system-management/request-improve.md) |
| 업무·개선 요청·식별자·접속 기록 | SB 운영관리 > 시스템 관리 > 업무개선 및 요청리스트 | 요청 및 개선사항 등록 · 등록 | `/system-management/request-improve/new` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/system-management/request-improve__new.md) |
| 업무·개선 요청·식별자·접속 기록 | SB 운영관리 > 시스템 관리 > 업무개선 및 요청리스트 | 업무개선 및 요청리스트 상세 · 상세 | `/system-management/request-improve/:id` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/system-management/request-improve__by-id.md) |
| 업무·개선 요청·식별자·접속 기록 | SB 운영관리 > 시스템 관리 > 업무개선 및 요청리스트 | 요청 및 개선사항 수정 · 수정 | `/system-management/request-improve/:id/edit` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/system-management/request-improve__by-id__edit.md) |
| 서버·시스템·연동 서버 관측 | SB 운영관리 > 시스템 관리 > 서버 용량 관리 | 서버 용량 관리 · 조회 | `/system-management/server-capacity` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/system-management/server-capacity.md) |
| 서버·시스템·연동 서버 관측 | SB 운영관리 > 시스템 관리 > 서버 용량 관리 | 서버 용량 관리 상세 · 상세 | `/system-management/server-capacity/:id` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/system-management/server-capacity__by-id.md) |
| 서버·시스템·연동 서버 관측 | SB 운영관리 > 시스템 관리 > 시스템 모니터링 | 시스템 모니터링 · 모니터링 | `/system-management/system-monitoring` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/system-management/system-monitoring.md) |
| 시스템 메시지·발행·이메일 확인 | SB 운영관리 > 시스템 관리 > 시스템 SMS 모니터링 | 시스템 SMS 모니터링 · 모니터링 | `/system-management/sms-monitoring` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/system-management/sms-monitoring.md) |
| 시스템 메시지·발행·이메일 확인 | SB 운영관리 > 시스템 관리 > 발행 관리 | 발행 관리 · 조회 | `/system-management/issue-management` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/system-management/issue-management.md) |
| 시스템 메시지·발행·이메일 확인 | SB 운영관리 > 시스템 관리 > 이메일 전송 모니터링 | 이메일 전송 모니터링 · 모니터링 | `/system-management/email-monitoring` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/system-management/email-monitoring.md) |
| 시스템 메시지·발행·이메일 확인 | SB 운영관리 > 시스템 관리 > 이메일 전송 모니터링 | 이메일 전송 모니터링 상세 · 상세 | `/system-management/email-monitoring/details` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/system-management/email-monitoring__details.md) |
| 서버·시스템·연동 서버 관측 | SB 운영관리 > 시스템 관리 > 연동 서버 모니터링 | 연동 서버 모니터링 · 모니터링 | `/system-management/server-monitoring` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/system-management/server-monitoring.md) |
| 서버·시스템·연동 서버 관측 | SB 운영관리 > 시스템 관리 > 서버 시간 관리 | 서버 시간 관리 · 조회 | `/system-management/server-time-management` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/system-management/server-time-management.md) |
| 시스템 메시지·발행·이메일 확인 | SB 운영관리 > 시스템 관리 > 시스템 SMS 모니터링 로그 | 시스템 SMS 모니터링 로그 · 모니터링 | `/system-management/sms-monitoring-log` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/system-management/sms-monitoring-log.md) |
| 서버·시스템·연동 서버 관측 | SB 운영관리 > 시스템 관리 > 빌서버 연결 서버 | 빌서버 연결 서버 · 조회 | `/system-management/build-server-connection` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/system-management/build-server-connection.md) |
| 업무·개선 요청·식별자·접속 기록 | SB 운영관리 > 시스템 관리 > 접속이력관리 | 접속이력관리 · 이력 조회 | `/system-management/access-history` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/system-management/access-history.md) |
| 업무·개선 요청·식별자·접속 기록 | SB 운영관리 > 시스템 관리 > 접속이력관리 | 접속이력관리 상세 · 상세 | `/system-management/access-history/:id` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/system-management/access-history__by-id.md) |
| 업무·개선 요청·식별자·접속 기록 | SB 운영관리 > 시스템 관리 > 업무 리스트 | 업무 리스트 · 조회 | `/system-management/work` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/system-management/work.md) |
| 업무·개선 요청·식별자·접속 기록 | SB 운영관리 > 시스템 관리 > 업무 리스트 등록 | 업무 리스트 등록 · 조회 | `/system-management/work/register` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/system-management/work__register.md) |
| 업무·개선 요청·식별자·접속 기록 | SB 운영관리 > 시스템 관리 > 업무 리스트 등록 | 업무 등록 · 등록 | `/system-management/work/register/new` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/system-management/work__register__new.md) |
| 업무·개선 요청·식별자·접속 기록 | SB 운영관리 > 시스템 관리 > 업무 리스트 등록 | 업무 리스트 등록 상세 · 상세 | `/system-management/work/register/:id` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/system-management/work__register__by-id.md) |
| 업무·개선 요청·식별자·접속 기록 | SB 운영관리 > 시스템 관리 > 웹링크 식별자 관리 | 웹링크 식별자 관리 · 조회 | `/system-management/weblink-identifier` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/system-management/weblink-identifier.md) |
| 업무·개선 요청·식별자·접속 기록 | SB 운영관리 > 시스템 관리 > 웹링크 식별자 관리 | 웹링크 식별자 등록 · 등록 | `/system-management/weblink-identifier/new` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/system-management/weblink-identifier__new.md) |
| 업무·개선 요청·식별자·접속 기록 | SB 운영관리 > 시스템 관리 > 웹링크 식별자 관리 | 웹링크 식별자 관리 상세 · 상세 | `/system-management/weblink-identifier/:id` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/system-management/weblink-identifier__by-id.md) |
| 업무·개선 요청·식별자·접속 기록 | SB 운영관리 > 시스템 관리 > 웹링크 식별자 관리 | 웹링크 식별자 수정 · 수정 | `/system-management/weblink-identifier/:id/edit` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/system-management/weblink-identifier__by-id__edit.md) |
| 운영자 계정·조직·권한 그룹 | SmartWork 관리 > 계정 관리 | 계정 관리 · 조회·관리 | `/settings/account-management` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/settings/account-management.md) |
| 운영자 계정·조직·권한 그룹 | SmartWork 관리 > 계정 관리 | 계정 관리 등록 · 등록 | `/settings/account-management/new` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/settings/account-management__new.md) |
| 운영자 계정·조직·권한 그룹 | SmartWork 관리 > 계정 관리 | 계정 관리 수정 · 수정 | `/settings/account-management/:id/edit` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/settings/account-management__by-id__edit.md) |
| 운영자 계정·조직·권한 그룹 | SmartWork 관리 > 조직 관리 | 조직 관리 · 조회·관리 | `/settings/organization-management` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/settings/organization-management.md) |
| 운영자 계정·조직·권한 그룹 | SmartWork 관리 > 권한 관리 | 권한 관리 · 조회·관리 | `/settings/permissions` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/settings/permissions.md) |
| 운영자 계정·조직·권한 그룹 | SmartWork 관리 > 권한 관리 | 권한 관리 등록 · 등록 | `/settings/permissions/new` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/settings/permissions__new.md) |
| 운영자 계정·조직·권한 그룹 | SmartWork 관리 > 권한 관리 | 권한 관리 상세 · 상세 | `/settings/permissions/:id` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/settings/permissions__by-id.md) |
| 운영 공지·인증 정책과 감사 로그 | SmartWork 관리 > 로그 관리 | 로그 관리 · 조회 | `/settings/log-management` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/settings/log-management.md) |
| 운영 공지·인증 정책과 감사 로그 | SmartWork 관리 > 공지 관리 | 공지 관리 · 조회·관리 | `/settings/notice-management` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/settings/notice-management.md) |
| 운영 공지·인증 정책과 감사 로그 | SmartWork 관리 > 로그인 관리 | 로그인 관리 · 조회·관리 | `/settings/login-management` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/settings/login-management.md) |
| 공지·FAQ·개별 문의·자료 | 고객지원 > 고객 게시판 관리 > 공지사항 | 공지사항 · 조회 | `/customer-support/notice` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/notice.md) |
| 공지·FAQ·개별 문의·자료 | 고객지원 > 고객 게시판 관리 > 공지사항 | 공지사항 등록 · 등록 | `/customer-support/notice/new` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/notice__new.md) |
| 공지·FAQ·개별 문의·자료 | 고객지원 > 고객 게시판 관리 > 공지사항 | 공지사항 삭제 · 상세 | `/customer-support/notice/:id` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/notice__by-id.md) |
| 공지·FAQ·개별 문의·자료 | 고객지원 > 고객 게시판 관리 > 공지사항 | 공지사항 수정 · 수정 | `/customer-support/notice/:id/edit` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/notice__by-id__edit.md) |
| 공지·FAQ·개별 문의·자료 | 고객지원 > 고객 게시판 관리 > FAQ | FAQ · 조회 | `/customer-support/faq` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/faq.md) |
| 공지·FAQ·개별 문의·자료 | 고객지원 > 고객 게시판 관리 > FAQ | FAQ 등록 · 등록 | `/customer-support/faq/new` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/faq__new.md) |
| 공지·FAQ·개별 문의·자료 | 고객지원 > 고객 게시판 관리 > FAQ | FAQ 삭제 · 상세 | `/customer-support/faq/:id` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/faq__by-id.md) |
| 공지·FAQ·개별 문의·자료 | 고객지원 > 고객 게시판 관리 > FAQ | FAQ 수정 · 수정 | `/customer-support/faq/:id/edit` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/faq__by-id__edit.md) |
| 공지·FAQ·개별 문의·자료 | 고객지원 > 고객 게시판 관리 > 1:1 문의 | 1:1 문의 · 조회 | `/customer-support/qna` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/qna.md) |
| 공지·FAQ·개별 문의·자료 | 고객지원 > 고객 게시판 관리 > 1:1 문의 | 1:1 문의 등록 · 등록 | `/customer-support/qna/new` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/qna__new.md) |
| 공지·FAQ·개별 문의·자료 | 고객지원 > 고객 게시판 관리 > 1:1 문의 | 1:1 문의 삭제 · 상세 | `/customer-support/qna/:id` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/qna__by-id.md) |
| 공지·FAQ·개별 문의·자료 | 고객지원 > 고객 게시판 관리 > 1:1 문의 | 1:1 문의 수정 · 수정 | `/customer-support/qna/:id/edit` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/qna__by-id__edit.md) |
| 공지·FAQ·개별 문의·자료 | 고객지원 > 고객 게시판 관리 > 1:1 문의 | 1:1 문의 답글 · 답글 | `/customer-support/qna/:id/reply` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/qna__by-id__reply.md) |
| 공지·FAQ·개별 문의·자료 | 고객지원 > 고객 게시판 관리 > 자료실 | 자료실 · 조회 | `/customer-support/pds` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/pds.md) |
| 공지·FAQ·개별 문의·자료 | 고객지원 > 고객 게시판 관리 > 자료실 | 자료실 등록 · 등록 | `/customer-support/pds/new` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/pds__new.md) |
| 공지·FAQ·개별 문의·자료 | 고객지원 > 고객 게시판 관리 > 자료실 | 자료실 삭제 · 상세 | `/customer-support/pds/:id` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/pds__by-id.md) |
| 공지·FAQ·개별 문의·자료 | 고객지원 > 고객 게시판 관리 > 자료실 | 자료실 수정 · 수정 | `/customer-support/pds/:id/edit` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/pds__by-id__edit.md) |
| 서비스 도입·제휴 문의와 제한 | 고객지원 > 고객 문의 관리 > 서비스 도입 문의 | 서비스 도입 문의 · 조회 | `/customer-support/service-inquiry` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/customer-support/service-inquiry.md) |
| 서비스 도입·제휴 문의와 제한 | 고객지원 > 고객 문의 관리 > 서비스 도입 문의 | 서비스 도입 문의 등록 · 등록 | `/customer-support/service-inquiry/new` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/customer-support/service-inquiry__new.md) |
| 서비스 도입·제휴 문의와 제한 | 고객지원 > 고객 문의 관리 > 서비스 도입 문의 | 서비스 도입 문의 상세 · 상세 | `/customer-support/service-inquiry/:id` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/customer-support/service-inquiry__by-id.md) |
| 서비스 도입·제휴 문의와 제한 | 고객지원 > 고객 문의 관리 > 제휴 문의 | 제휴 문의 · 조회 | `/customer-support/affiliation-inquiry` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/customer-support/affiliation-inquiry.md) |
| 서비스 도입·제휴 문의와 제한 | 고객지원 > 고객 문의 관리 > 제휴 문의 | 제휴 문의 상세 · 상세 | `/customer-support/affiliation-inquiry/:id` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/customer-support/affiliation-inquiry__by-id.md) |
| 서비스 도입·제휴 문의와 제한 | 고객지원 > 고객 문의 관리 > 블랙리스트 관리 | 블랙리스트 관리 · 조회·관리 | `/customer-support/blacklist` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/customer-support/blacklist.md) |
| 기술자료와 문의 방법 제공 | 고객지원 > 서비스 플랫폼 관리(자료실) > WEB 자료실 | WEB 자료실 · 조회 | `/customer-support/web-resources` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/web-resources.md) |
| 기술자료와 문의 방법 제공 | 고객지원 > 서비스 플랫폼 관리(자료실) > WEB 자료실 | WEB 자료실 등록 · 등록 | `/customer-support/web-resources/new` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/web-resources__new.md) |
| 기술자료와 문의 방법 제공 | 고객지원 > 서비스 플랫폼 관리(자료실) > WEB 자료실 | WEB 자료실 상세 · 상세 | `/customer-support/web-resources/:id` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/web-resources__by-id.md) |
| 기술자료와 문의 방법 제공 | 고객지원 > 서비스 플랫폼 관리(자료실) > WEB 자료실 | WEB 자료실 수정 · 수정 | `/customer-support/web-resources/:id/edit` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/web-resources__by-id__edit.md) |
| 기술자료와 문의 방법 제공 | 고객지원 > 서비스 플랫폼 관리(자료실) > SAP 자료실 | SAP 자료실 · 조회 | `/customer-support/sap-resources` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/sap-resources.md) |
| 기술자료와 문의 방법 제공 | 고객지원 > 서비스 플랫폼 관리(자료실) > SAP 자료실 | SAP 자료실 등록 · 등록 | `/customer-support/sap-resources/new` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/sap-resources__new.md) |
| 기술자료와 문의 방법 제공 | 고객지원 > 서비스 플랫폼 관리(자료실) > SAP 자료실 | SAP 자료실 상세 · 상세 | `/customer-support/sap-resources/:id` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/sap-resources__by-id.md) |
| 기술자료와 문의 방법 제공 | 고객지원 > 서비스 플랫폼 관리(자료실) > SAP 자료실 | SAP 자료실 수정 · 수정 | `/customer-support/sap-resources/:id/edit` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/sap-resources__by-id__edit.md) |
| 기술자료와 문의 방법 제공 | 고객지원 > 서비스 플랫폼 관리(자료실) > NSAP 자료실 | NSAP 자료실 · 조회 | `/customer-support/nsap-resources` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/nsap-resources.md) |
| 기술자료와 문의 방법 제공 | 고객지원 > 서비스 플랫폼 관리(자료실) > NSAP 자료실 | NSAP 자료실 등록 · 등록 | `/customer-support/nsap-resources/new` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/nsap-resources__new.md) |
| 기술자료와 문의 방법 제공 | 고객지원 > 서비스 플랫폼 관리(자료실) > NSAP 자료실 | NSAP 자료실 상세 · 상세 | `/customer-support/nsap-resources/:id` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/nsap-resources__by-id.md) |
| 기술자료와 문의 방법 제공 | 고객지원 > 서비스 플랫폼 관리(자료실) > NSAP 자료실 | NSAP 자료실 수정 · 수정 | `/customer-support/nsap-resources/:id/edit` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/nsap-resources__by-id__edit.md) |
| 기술자료와 문의 방법 제공 | 고객지원 > 서비스 플랫폼 관리(자료실) > WEB 문의 가이드 | WEB 문의 가이드 · 조회 | `/customer-support/web-inquiry-guide` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/web-inquiry-guide.md) |
| 기술자료와 문의 방법 제공 | 고객지원 > 서비스 플랫폼 관리(자료실) > WEB 문의 가이드 | WEB 문의 가이드 등록 · 등록 | `/customer-support/web-inquiry-guide/new` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/web-inquiry-guide__new.md) |
| 기술자료와 문의 방법 제공 | 고객지원 > 서비스 플랫폼 관리(자료실) > WEB 문의 가이드 | WEB 문의 가이드 상세 · 상세 | `/customer-support/web-inquiry-guide/:id` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/web-inquiry-guide__by-id.md) |
| 기술자료와 문의 방법 제공 | 고객지원 > 서비스 플랫폼 관리(자료실) > WEB 문의 가이드 | WEB 문의 가이드 수정 · 수정 | `/customer-support/web-inquiry-guide/:id/edit` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/web-inquiry-guide__by-id__edit.md) |
| 기술자료와 문의 방법 제공 | 고객지원 > 서비스 플랫폼 관리(자료실) > SAP 문의 가이드 | SAP 문의 가이드 · 조회 | `/customer-support/sap-inquiry-guide` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/sap-inquiry-guide.md) |
| 기술자료와 문의 방법 제공 | 고객지원 > 서비스 플랫폼 관리(자료실) > SAP 문의 가이드 | SAP 문의 가이드 등록 · 등록 | `/customer-support/sap-inquiry-guide/new` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/sap-inquiry-guide__new.md) |
| 기술자료와 문의 방법 제공 | 고객지원 > 서비스 플랫폼 관리(자료실) > SAP 문의 가이드 | SAP 문의 가이드 상세 · 상세 | `/customer-support/sap-inquiry-guide/:id` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/sap-inquiry-guide__by-id.md) |
| 기술자료와 문의 방법 제공 | 고객지원 > 서비스 플랫폼 관리(자료실) > SAP 문의 가이드 | SAP 문의 가이드 수정 · 수정 | `/customer-support/sap-inquiry-guide/:id/edit` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/sap-inquiry-guide__by-id__edit.md) |
| 기술자료와 문의 방법 제공 | 고객지원 > 서비스 플랫폼 관리(자료실) > NSAP 문의 가이드 | NSAP 문의 가이드 · 조회 | `/customer-support/nsap-inquiry-guide` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/nsap-inquiry-guide.md) |
| 기술자료와 문의 방법 제공 | 고객지원 > 서비스 플랫폼 관리(자료실) > NSAP 문의 가이드 | NSAP 문의 가이드 등록 · 등록 | `/customer-support/nsap-inquiry-guide/new` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/nsap-inquiry-guide__new.md) |
| 기술자료와 문의 방법 제공 | 고객지원 > 서비스 플랫폼 관리(자료실) > NSAP 문의 가이드 | NSAP 문의 가이드 상세 · 상세 | `/customer-support/nsap-inquiry-guide/:id` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/nsap-inquiry-guide__by-id.md) |
| 기술자료와 문의 방법 제공 | 고객지원 > 서비스 플랫폼 관리(자료실) > NSAP 문의 가이드 | NSAP 문의 가이드 수정 · 수정 | `/customer-support/nsap-inquiry-guide/:id/edit` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/nsap-inquiry-guide__by-id__edit.md) |
| 기술자료와 문의 방법 제공 | 고객지원 > 서비스 플랫폼 관리(자료실) > 연동업체 소스 관리 | 연동업체 소스 관리 · 조회 | `/customer-support/vendor-source-management` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/vendor-source-management.md) |
| 기술자료와 문의 방법 제공 | 고객지원 > 서비스 플랫폼 관리(자료실) > 연동업체 소스 관리 | 연동업체 소스 관리 등록 · 등록 | `/customer-support/vendor-source-management/new` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/vendor-source-management__new.md) |
| 기술자료와 문의 방법 제공 | 고객지원 > 서비스 플랫폼 관리(자료실) > 연동업체 소스 관리 | 연동업체 소스 관리 상세 · 상세 | `/customer-support/vendor-source-management/:id` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/vendor-source-management__by-id.md) |
| 기술자료와 문의 방법 제공 | 고객지원 > 서비스 플랫폼 관리(자료실) > 연동업체 소스 관리 | 연동업체 소스 관리 수정 · 수정 | `/customer-support/vendor-source-management/:id/edit` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/vendor-source-management__by-id__edit.md) |
| 쿠폰 혜택·상태·이력 | 고객지원 > 멤버십 쿠폰관리 > 쿠폰 조회 | 쿠폰 조회 · 조회 | `/customer-support/coupon` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/coupon.md) |
| 쿠폰 혜택·상태·이력 | 고객지원 > 멤버십 쿠폰관리 > 쿠폰 조회 | 쿠폰 조회 상세 · 상세 | `/customer-support/coupon/:couponNo` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/coupon__by-couponNo.md) |
| 쿠폰 혜택·상태·이력 | 고객지원 > 멤버십 쿠폰관리 > 쿠폰 이력 조회 | 쿠폰 이력 조회 · 이력 조회 | `/customer-support/coupon-history` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/customer-support/coupon-history.md) |
| 운영반영 요청 기록 | SB 운영관리 > 운영반영 관리 > 소스 관리 | 소스 관리 · 조회 | `/source-management/source-management` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/source-management/source-management.md) |
| 운영반영 요청 기록 | SB 운영관리 > 운영반영 관리 > 소스 관리 | 소스 반영 등록 · 등록 | `/source-management/source-management/new` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/source-management/source-management__new.md) |
| 운영반영 요청 기록 | SB 운영관리 > 운영반영 관리 > 소스 관리 | 소스 관리 상세 · 상세 | `/source-management/source-management/:id` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/source-management/source-management__by-id.md) |
| 운영반영 요청 기록 | SB 운영관리 > 운영반영 관리 > 소스 관리 | 소스 반영 수정 · 수정 | `/source-management/source-management/:id/edit` | WBS 담당 기준 | 검토 대기 | [기존 매뉴얼](../manuals/source-management/source-management__by-id__edit.md) |
| 직원 인증·내 계정·세션 | 내 계정 > 프로필 | 프로필 · 조회·관리 | `/my-account/profile` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/my-account/profile.md) |
| 직원 인증·내 계정·세션 | 내 계정 > 설정 | 설정 · 조회·관리 | `/my-account/settings` | 확정 필요 | 검토 대기 | [신규 매뉴얼](../manuals/my-account/settings.md) |

## 독립 업무 매뉴얼에서 제외한 경로

| 라우트 | 유형 | 사유·이동 대상 |
| --- | --- | --- |
| `/hub-service/bulk-integration-management` | 미구현 | 현재 ComingSoon 화면만 연결된다. |
| `/hub-service/new-integration-recovery/checklists` | 리다이렉트 | 차세대 복구솔루션으로 이동한다. [대상 매뉴얼](../manuals/hub-service/new-integration-recovery.md) |
| `/my-account` | 리다이렉트 | 내 계정 프로필이 기본 탭이다. [대상 매뉴얼](../manuals/my-account/profile.md) |
| `/settings/account-management/:id` | 리다이렉트 | 유효한 계정 번호는 수정 화면, 나머지는 계정 목록으로 이동한다. [대상 매뉴얼](../manuals/settings/account-management__by-id__edit.md) |
| `/*` | 공통 오류 처리 | 정의된 경로가 없을 때 표시하는 공통 404 화면이다. |

# 업무 도메인 지도

이 문서는 업무 영역을 찾기 위한 상위 지도다. 같은 영역의 페이지가 같은 일을 한다는 뜻이 아니다. 처음 보는 독자는 아래에서 담당 업무를 찾은 뒤 개별 페이지의 **1) 화면 기본 정보 → 도메인 이해**에서 사용 상황·실제 데이터·판단 결과·다음 업무를 확인한다. [페이지별 소스 대조표](page-domain-review.md)에서 134개 경로의 설명 근거와 탭·영역 구분을 확인할 수 있다. SB 고객관리·SB 서비스관리·SB 운영관리·서비스 현황·고객지원은 메뉴의 큰 분류이며, 아래 표는 실제 업무 대상과 목적을 중심으로 나눈 세부 영역이다.

대상은 기존 WBS 유지윤 담당 56개 메뉴·134개 독립 화면이다. 이 지도는 전체 SmartWork 기능 목록이나 신규 담당 선정 결과가 아니다. 도메인 설명은 코드·메뉴·기존 매뉴얼의 업무 규칙을 풀어쓴 것으로, 실제 저장·발송·배포 검증을 추가로 완료했다는 의미가 아니다.

| 세부 도메인 | 다루는 대상 | 독립 화면 | 문서 |
|---|---|---|---|
| [스마트빌 회사·회원 관리](#company) | 회사: 서비스를 이용하는 사업자 | 7 | [회사 정보 조회·관리](../manuals/company-management/company-info.md) |
| [스마트빌 가입·탈퇴 현황](#customer-status) | 회원: 이용 사용자 | 2 | [가입 현황 조회·관리](../manuals/smartbill-status/status.md) |
| [글로싸인 엔터프라이즈 고객·인증 관리](#glosign) | 회사: 글로싸인 조직 | 5 | [회원 정보 조회·관리](../manuals/glosign-enterprise/members.md) |
| [전자세금계산서·거래명세서 운영](#invoice) | 공급자: 거래 문서를 발행하는 쪽 | 6 | [세금계산서 조회 조회·관리](../manuals/tax-invoice/tax-invoice.md) |
| [채권잔액 확인 서비스](#bond) | 채권잔액 확인서: 거래 잔액 확인에 쓰는 문서 | 12 | [채권잔액 확인서 조회 조회·관리](../manuals/bond-service/bond-balance-inquiry.md) |
| [설치형 홈택스 세금계산서 수집](#hometax) | 수집: 외부 문서를 가져오는 작업 | 8 | [모니터링 조회·관리](../manuals/hometax-dti/monitoring.md) |
| [보나뱅크 서비스 운영](#bonabank) | 보나뱅크 회사·회원: 이 서비스 구분의 고객 정보 | 14 | [회사 정보 조회·관리](../manuals/bonabank/company.md) |
| [서비스 오류 접수·처리](#error) | 오류 접수 건: 실제 조사·처리할 개별 문제 | 7 | [전체 오류 조회/처리 조회·관리](../manuals/error-management/error-reports.md) |
| [운영반영 계획·소스 관리](#source) | 개발 항목: 반영할 변경 작업 | 4 | [소스 관리 조회·관리](../manuals/source-management/source-management.md) |
| [입금·예치금·환불 관리](#payment) | 입금: 접수된 납부 내역 | 13 | [입금 현황 조회 조회·관리](../manuals/payment/status.md) |
| [미납 업체의 이용 제한 예외](#unpaid) | 미납: 납부되지 않은 요금 상태 | 1 | [미납 예외업체 관리 조회·관리](../manuals/service-overview/unpaid-exception-manager.md) |
| [서비스 이용 통계](#statistics) | 이용 건수: 조건에 포함된 처리 문서 수 | 7 | [월별 이용 현황 (세금, 계약) 조회·관리](../manuals/statistics/monthly-usage.md) |
| [고객 게시판·문의 응대](#board) | 공지: 서비스 안내 | 17 | [공지사항 조회·관리](../manuals/customer-support/notice.md) |
| [멤버십 쿠폰 운영](#coupon) | 쿠폰: 업체에 제공된 혜택을 식별하는 단위 | 3 | [쿠폰 조회 조회·관리](../manuals/customer-support/coupon.md) |
| [연동 플랫폼 자료·문의 가이드](#platform) | WEB·SAP·NSAP: 현재 메뉴가 구분하는 연동 자료 영역 | 28 | [WEB 자료실 조회·관리](../manuals/customer-support/web-resources.md) |

<a id="company"></a>
## 스마트빌 회사·회원 관리

스마트빌을 이용하는 회사와 그 회사에 속한 회원의 가입 상태·서비스 설정을 관리하는 업무다. 고객 문의가 들어왔을 때 어느 회사·회원의 문제인지 식별하고, 회사 단위 설정과 회원 단위 권한을 나누어 확인한다.

- 주요 대상·용어: 회사: 서비스를 이용하는 사업자 / 회원: 회사에 소속된 사용자 / 사업자번호: 회사를 찾는 업무 식별값
- 업무 흐름: 회사 또는 업로드 결과 찾기 → 가입·소속·설정 확인 → 필요한 관리 작업 → 결과·이력 확인
- 업무 구분: 거래업체 파일의 가입 여부 확인과 회사·회원의 실제 신규 가입은 다른 작업이다. 회사 번호와 회원 번호를 서로 대신 사용하지 않는다.

- [회사 정보 조회·관리](../manuals/company-management/company-info.md) · `/company-management/company-info`
- [회사 정보 전체 회원 조회](../manuals/company-management/company-info__by-companyId__members.md) · `/company-management/company-info/:companyId/members`
- [회사 정보 회원 권한 조회](../manuals/company-management/company-info__by-companyKey__member-permissions.md) · `/company-management/company-info/:companyKey/member-permissions`
- [회사 정보 상세](../manuals/company-management/company-info__by-id.md) · `/company-management/company-info/:id`
- [회사 정보 변경 이력](../manuals/company-management/company-info__by-id__change-history.md) · `/company-management/company-info/:id/change-history`
- [스마트빌 가입조회 조회·관리](../manuals/company-management/registration-inquiry.md) · `/company-management/registration-inquiry`
- [스마트빌 가입조회 상세](../manuals/company-management/registration-inquiry__by-uploadId.md) · `/company-management/registration-inquiry/:uploadId`

<a id="customer-status"></a>
## 스마트빌 가입·탈퇴 현황

스마트빌 고객 규모와 변동을 회원·사업장 단위로 파악하는 업무다. 가입 또는 탈퇴가 발생한 기간의 실적과 누적 현황을 확인하며, 회사별 설정 변경보다는 현황 파악에 사용한다.

- 주요 대상·용어: 회원: 이용 사용자 / 사업장: 서비스를 사용하는 사업자 단위 / 조회 기간: 통계에 포함할 가입·탈퇴 시점
- 업무 흐름: 집계 대상·기간 선택 → 회원/사업장 구분 → 현황 조회 → 조건을 맞춰 비교·반출
- 업무 구분: 회원 수와 사업장 수는 서로 다른 집계 대상이다. 탈퇴 현황 조회는 탈퇴를 실행하는 기능이 아니다.

- [가입 현황 조회·관리](../manuals/smartbill-status/status.md) · `/smartbill-status/status`
- [탈퇴 현황 조회·관리](../manuals/smartbill-status/withdrawal-status.md) · `/smartbill-status/withdrawal-status`

<a id="glosign"></a>
## 글로싸인 엔터프라이즈 고객·인증 관리

글로싸인 엔터프라이즈의 회사·회원 현황과 계약 열람에 필요한 인증 문제를 관리하는 업무다. 회사에 속한 사용자를 확인하거나 비밀번호·열람 잠금 문제를 조사할 때 사용한다.

- 주요 대상·용어: 회사: 글로싸인 조직 / 회원: 조직 또는 개인 사용자 / 열람 인증 잠금: 계약을 열 때 인증 실패가 누적된 상태
- 업무 흐름: 회사·회원 또는 계약 찾기 → 소속·인증 상태 확인 → 허용된 초기화 작업 → 결과 확인
- 업무 구분: 스마트빌 회사정보와 글로싸인 조직정보는 조회 대상·식별자가 다르다. 비밀번호 초기화와 계약 열람 인증 잠금 해제도 서로 다른 처리다.

- [회원 정보 조회·관리](../manuals/glosign-enterprise/members.md) · `/glosign-enterprise/members`
- [회사 정보 조회·관리](../manuals/glosign-enterprise/companies.md) · `/glosign-enterprise/companies`
- [회사 정보 전체 회원 조회](../manuals/glosign-enterprise/companies__by-orgSeq.md) · `/glosign-enterprise/companies/:orgSeq`
- [비밀번호 초기화 비밀번호 초기화](../manuals/glosign-enterprise/status.md) · `/glosign-enterprise/status`
- [열람인증 초기화 조회·관리](../manuals/glosign-enterprise/personal-password-reset.md) · `/glosign-enterprise/personal-password-reset`

<a id="invoice"></a>
## 전자세금계산서·거래명세서 운영

회사 간 거래 문서인 전자세금계산서와 거래명세서의 발행 내용·처리 상태를 조사하는 업무다. 문서가 보이지 않거나 수신·메일·첨부 관련 문의가 있을 때 대상 문서와 작성일을 맞춰 확인한다.

- 주요 대상·용어: 공급자: 거래 문서를 발행하는 쪽 / 공급받는자: 거래 상대방 / 거래명세서: 거래 내역을 나타내는 문서로 세금계산서와 구분 / 작성일(wday): 상세 조회의 문서 기준일
- 업무 흐름: 조회 대상·기간 선택 → 문서 선택 → 본문·상태·연계 문서 확인 → 필요한 지원 작업
- 업무 구분: 현행 조회와 과거 조회는 메뉴·데이터 원천이 구분된다. 경로의 legacy는 과거 문서 조회를 뜻한다. 목록·상세·인감 이미지의 조회 성공 여부도 각각 확인한다.

- [세금계산서 조회 조회·관리](../manuals/tax-invoice/tax-invoice.md) · `/tax-invoice/tax-invoice`
- [세금계산서 조회 상세](../manuals/tax-invoice/tax-invoice__by-id.md) · `/tax-invoice/tax-invoice/:id`
- [세금계산서 조회 (단독) 거래명세서 상세](../manuals/tax-invoice/tax-invoice__statement__by-id.md) · `/tax-invoice/tax-invoice/statement/:id`
- [과거 세금계산서 조회 조회·관리](../manuals/tax-invoice/legacy-tax-invoice.md) · `/tax-invoice/legacy-tax-invoice`
- [과거 세금계산서 조회 상세](../manuals/tax-invoice/legacy-tax-invoice__by-id.md) · `/tax-invoice/legacy-tax-invoice/:id`
- [과거 세금계산서 조회 (단독) 거래명세서 상세](../manuals/tax-invoice/legacy-tax-invoice__statement__by-id.md) · `/tax-invoice/legacy-tax-invoice/statement/:id`

<a id="bond"></a>
## 채권잔액 확인 서비스

거래 상대방과 확인할 채권잔액 문서 및 이를 주고받는 연동 상태를 관리하는 업무다. 확인서 조회, 이용 담당자의 권한, 연동업체 설정, 송수신 장애를 같은 업무 흐름 안에서 조사한다.

- 주요 대상·용어: 채권잔액 확인서: 거래 잔액 확인에 쓰는 문서 / 연동업체: 시스템 연결 대상 업체 / 참조번호·conversation ID: 문서 또는 송수신 건을 추적하는 값
- 업무 흐름: 확인서·연동업체 찾기 → 담당 권한·송수신 상태 확인 → 로그·전문·장애 정보 조사 → 필요한 조치
- 업무 구분: 문서의 잔액 확인과 실제 입금·환불 처리는 다른 업무다. 송신 요청·접수·상대방 처리 결과를 한 상태로 간주하지 않는다.

- [채권잔액 확인서 조회 조회·관리](../manuals/bond-service/bond-balance-inquiry.md) · `/bond-service/bond-balance-inquiry`
- [채권잔액 확인서 조회 상세](../manuals/bond-service/bond-balance-inquiry__by-drcNo.md) · `/bond-service/bond-balance-inquiry/:drcNo`
- [담당자 권한 조회 조회·관리](../manuals/bond-service/drc-right.md) · `/bond-service/drc-right`
- [담당자 권한 조회 상세](../manuals/bond-service/drc-right__by-comNo.md) · `/bond-service/drc-right/:comNo`
- [연동업체 관리 조회·관리](../manuals/bond-service/drc-company-link.md) · `/bond-service/drc-company-link`
- [연동업체 관리 상세](../manuals/bond-service/drc-company-link__by-comNo.md) · `/bond-service/drc-company-link/:comNo`
- [연동업체 관리 등록](../manuals/bond-service/drc-company-link__new.md) · `/bond-service/drc-company-link/new`
- [연동 로그 조회 조회·관리](../manuals/bond-service/integration-log.md) · `/bond-service/integration-log`
- [연동업체 장애 관리 조회·관리](../manuals/bond-service/integration-partner-error.md) · `/bond-service/integration-partner-error`
- [연동업체 장애 관리 장애 등록·수정](../manuals/bond-service/integration-partner-error__detail.md) · `/bond-service/integration-partner-error/detail`
- [채권잔액 전송 관리 조회·관리](../manuals/bond-service/receivable-balance-transfer.md) · `/bond-service/receivable-balance-transfer`
- [채권잔액 전송 관리 상세](../manuals/bond-service/receivable-balance-transfer__by-conversationId.md) · `/bond-service/receivable-balance-transfer/:conversationId`

<a id="hometax"></a>
## 설치형 홈택스 세금계산서 수집

홈택스에서 세금계산서 데이터를 가져오는 설치형 수집 작업의 설정과 실행 상태를 관리하는 업무다. 업체별 인증키·인증서·실행 주기와 실패 내역을 확인해 수집이 중단된 원인을 찾는다.

- 주요 대상·용어: 수집: 외부 문서를 가져오는 작업 / 인증키(sbKey): 설치·연동 대상을 식별하는 키 / 인증서: 홈택스 인증에 사용하는 수단 / 이메일 파싱: 이메일 내용을 읽어 처리하는 별도 수집 경로
- 업무 흐름: 연동 대상·설정 확인 → 인증서 유효성 확인 → 실행 현황 확인 → 실패 로그 조사
- 업무 구분: 홈택스 수집과 국세청에 문서를 보내는 전송·신고는 방향과 목적이 다르다. 인증서 등록·만료와 개별 수집 실행 성공도 따로 확인한다.

- [모니터링 조회·관리](../manuals/hometax-dti/monitoring.md) · `/hometax-dti/monitoring`
- [인증키 관리 조회·관리](../manuals/hometax-dti/auth-key.md) · `/hometax-dti/auth-key`
- [인증키 관리 상세](../manuals/hometax-dti/auth-key__by-sbKey.md) · `/hometax-dti/auth-key/:sbKey`
- [오류 로그 조회 조회·관리](../manuals/hometax-dti/error-logs.md) · `/hometax-dti/error-logs`
- [인증서 등록 현황 조회 조회·관리](../manuals/hometax-dti/certificate-status.md) · `/hometax-dti/certificate-status`
- [인증서 만료일 관리 조회·관리](../manuals/hometax-dti/certificate-expiry.md) · `/hometax-dti/certificate-expiry`
- [인증서 로그인 실패 조회 조회·관리](../manuals/hometax-dti/login-failures.md) · `/hometax-dti/login-failures`
- [이메일파싱 모니터링 조회·관리](../manuals/hometax-dti/email-parsing.md) · `/hometax-dti/email-parsing`

<a id="bonabank"></a>
## 보나뱅크 서비스 운영

보나뱅크 구분으로 관리되는 회사·회원과 전자세금계산서 업무를 운영하는 영역이다. 고객 정보, 문서 현황, 국세청 신고 실패, 이용 통계와 공지를 함께 확인하되 현재 메뉴의 보나뱅크 범위를 유지한다.

- 주요 대상·용어: 보나뱅크 회사·회원: 이 서비스 구분의 고객 정보 / 신고 실패: 국세청 관련 처리에서 실패로 분류된 내역 / 공지: 서비스 안내 게시물
- 업무 흐름: 보나뱅크 고객 식별 → 회사·회원 또는 문서·통계 선택 → 상태·이력 확인 → 필요한 지원 작업
- 업무 구분: 스마트빌 전체 고객 목록과 보나뱅크 목록은 범위가 다를 수 있다. 세금계산서 목록의 상세 이동은 공통 세금계산서 화면으로 연결되는 현재 구현을 따른다.

- [회사 정보 조회·관리](../manuals/bonabank/company.md) · `/bonabank/company`
- [회사 정보 전체 회원 조회](../manuals/bonabank/company__by-companyId__members.md) · `/bonabank/company/:companyId/members`
- [회사 정보 상세](../manuals/bonabank/company__by-id.md) · `/bonabank/company/:id`
- [회사 정보 변경 이력](../manuals/bonabank/company__by-id__change-history.md) · `/bonabank/company/:id/change-history`
- [회원 정보 조회·관리](../manuals/bonabank/member.md) · `/bonabank/member`
- [회원 정보 상세](../manuals/bonabank/member__by-id.md) · `/bonabank/member/:id`
- [세금계산서 조회 조회·관리](../manuals/bonabank/tax-invoice.md) · `/bonabank/tax-invoice`
- [세금계산서 조회 상세](../manuals/bonabank/tax-invoice__by-dtiIdx.md) · `/bonabank/tax-invoice/:dtiIdx`
- [세금계산서 통계 조회·관리](../manuals/bonabank/tax-invoice-statistics.md) · `/bonabank/tax-invoice-statistics`
- [국세청 신고 실패 조회 조회·관리](../manuals/bonabank/nts-failures.md) · `/bonabank/nts-failures`
- [공지사항 관리 조회·관리](../manuals/bonabank/notices.md) · `/bonabank/notices`
- [공지사항 관리 상세](../manuals/bonabank/notices__by-id.md) · `/bonabank/notices/:id`
- [공지사항 관리 수정](../manuals/bonabank/notices__by-id__edit.md) · `/bonabank/notices/:id/edit`
- [공지사항 관리 등록](../manuals/bonabank/notices__new.md) · `/bonabank/notices/new`

<a id="error"></a>
## 서비스 오류 접수·처리

서비스 이용 중 발생한 문제를 접수하고 처리 경과를 남기는 업무다. 개별 오류 건의 문의 업체·증상·처리 상태와, 여러 오류에서 공통으로 사용하는 오류 코드 설명을 나누어 관리한다.

- 주요 대상·용어: 오류 접수 건: 실제 조사·처리할 개별 문제 / 처리내역: 해당 건에 남기는 대응 기록 / 오류 코드: 문제 유형과 설명을 식별하는 공통 코드
- 업무 흐름: 문의·증상 접수 → 오류 목록에서 대상 확인 → 원인·처리내역 기록 → 상태 확인
- 업무 구분: 오류 코드 정의를 바꾸는 일과 접수 건을 처리하는 일은 다르다. 처리내역 저장만으로 실제 서비스 장애가 해결되었다고 판단하지 않는다.

- [전체 오류 조회/처리 조회·관리](../manuals/error-management/error-reports.md) · `/error-management/error-reports`
- [전체 오류 조회/처리 상세](../manuals/error-management/error-reports__by-id.md) · `/error-management/error-reports/:id`
- [전체 오류 조회/처리 오류 처리내역 등록](../manuals/error-management/error-reports__by-id__process.md) · `/error-management/error-reports/:id/process`
- [오류 접수/등록 등록](../manuals/error-management/error-reports__new.md) · `/error-management/error-reports/new`
- [오류 코드 관리 조회·관리](../manuals/error-management/error-code-management.md) · `/error-management/error-code-management`
- [오류 코드 관리 상세](../manuals/error-management/error-code-management__by-errorCode.md) · `/error-management/error-code-management/:errorCode`
- [오류 코드 관리 등록](../manuals/error-management/error-code-management__new.md) · `/error-management/error-code-management/new`

<a id="source"></a>
## 운영반영 계획·소스 관리

개발 항목을 데모·운영 환경에 언제 반영할지 기록하고 완료 여부를 관리하는 업무다. 어떤 변경을 누가 준비하고 어떤 환경에 반영했는지 업무 기록을 추적할 때 사용한다.

- 주요 대상·용어: 개발 항목: 반영할 변경 작업 / 데모·운영 반영일: 환경별 계획·완료 시점 / 완료 상태: 화면에서 관리하는 업무 기록
- 업무 흐름: 개발 항목 등록 → 반영 계획 확인 → 상세·내용 보완 → 반영 후 업무 상태 기록
- 업무 구분: 이 화면의 소스 관리 기록은 Git 저장소의 코드·커밋 관리와 다르다. 완료 표시나 내용 저장만으로 서버 배포가 실행되었다고 보지 않는다.

- [소스 관리 조회·관리](../manuals/source-management/source-management.md) · `/source-management/source-management`
- [소스 관리 상세](../manuals/source-management/source-management__by-id.md) · `/source-management/source-management/:id`
- [소스 관리 수정](../manuals/source-management/source-management__by-id__edit.md) · `/source-management/source-management/:id/edit`
- [소스 관리 등록](../manuals/source-management/source-management__new.md) · `/source-management/source-management/new`

<a id="payment"></a>
## 입금·예치금·환불 관리

고객의 서비스 요금 입금과 미리 보유한 금액, 환불 신청을 관리하는 업무다. 입금 내역이 어느 업체·청구에 연결되는지, 예치금이 어떻게 늘거나 줄었는지, 환불 가능한 금액과 처리 상태가 무엇인지 확인한다.

- 주요 대상·용어: 입금: 접수된 납부 내역 / 예치금: 서비스 이용을 위해 보유·차감되는 금액 / 청구월: 요금을 청구한 월 / 환불 신청: 환불 대상·금액·계좌·처리 상태 기록
- 업무 흐름: 업체·기간·청구 찾기 → 입금·잔액·이력 확인 → 허용된 입금/예치금/환불 처리 → 상태·금액 재확인
- 업무 구분: 예치금 잔액·환불 가능 금액·환불 신청 금액은 같은 값이 아니다. 화면의 처리 완료와 실제 은행 송금 완료의 확인 범위를 구분한다.

- [입금 현황 조회 조회·관리](../manuals/payment/status.md) · `/payment/status`
- [입금 현황 조회 상세](../manuals/payment/status__by-id.md) · `/payment/status/:id`
- [예치금 관리 조회·관리](../manuals/payment/deposit.md) · `/payment/deposit`
- [예치금 관리 상세](../manuals/payment/deposit__by-id.md) · `/payment/deposit/:id`
- [일별 예치금 조회 조회·관리](../manuals/payment/daily-deposit-inquiry.md) · `/payment/daily-deposit-inquiry`
- [일별 예치금 조회 상세](../manuals/payment/daily-deposit-inquiry__by-id.md) · `/payment/daily-deposit-inquiry/:id`
- [벌크식계좌 입금 관리 조회·관리](../manuals/payment/bulk-account-deposit.md) · `/payment/bulk-account-deposit`
- [벌크식계좌 입금 관리 상세](../manuals/payment/bulk-account-deposit__by-id.md) · `/payment/bulk-account-deposit/:id`
- [무통장입금 취소내역 조회 조회·관리](../manuals/payment/bank-transfer-cancel.md) · `/payment/bank-transfer-cancel`
- [환불 관리 조회·관리](../manuals/payment/refund-management.md) · `/payment/refund-management`
- [환불 관리 상세](../manuals/payment/refund-management__by-refundNo.md) · `/payment/refund-management/:refundNo`
- [환불 관리 환불 가능 금액 조회](../manuals/payment/refund-management__inquiry.md) · `/payment/refund-management/inquiry`
- [환불 관리 등록](../manuals/payment/refund-management__new.md) · `/payment/refund-management/new`

<a id="unpaid"></a>
## 미납 업체의 이용 제한 예외

요금 미납에 따른 이용 제한에서 업체별로 예외를 적용할 기간과 상태를 관리하는 업무다. 고객 대응 중 일정 기간 서비스를 허용할 필요가 있을 때 해당 업체와 예외 기록을 확인한다.

- 주요 대상·용어: 미납: 납부되지 않은 요금 상태 / 예외업체: 제한 예외 적용 대상 / 예외 기간: 예외가 유효한 기간
- 업무 흐름: 업체 식별 → 미납·기존 예외 확인 → 기간·상태 관리 → 적용 결과 확인
- 업무 구분: 이용 제한 예외를 등록하는 것은 미납 금액을 납부·정산하거나 채무를 없애는 처리와 다르다.

- [미납 예외업체 관리 조회·관리](../manuals/service-overview/unpaid-exception-manager.md) · `/service-overview/unpaid-exception-manager`

<a id="statistics"></a>
## 서비스 이용 통계

전자세금계산서와 전자계약이 얼마나 사용되는지 기간·업체·문서 구분별로 파악하는 업무다. 월별 흐름을 보고 필요한 월의 일별 수치나 업체별 실적을 확인한다.

- 주요 대상·용어: 이용 건수: 조건에 포함된 처리 문서 수 / 이용 업체 수: 집계 대상 업체 수 / 매출·매입: 공급자·공급받는자 관점의 구분 / 집계월: 통계의 기준 월
- 업무 흐름: 집계 대상·기간 선택 → 월별·업체별 현황 확인 → 일별 내역 비교 → 필요 시 반출
- 업무 구분: 문서 건수와 업체 수, 매출과 매입은 서로 다른 지표다. 서로 다른 화면의 합계를 비교할 때 기간·상태·집계 대상과 단위를 맞춘다.

- [월별 이용 현황 (세금, 계약) 조회·관리](../manuals/statistics/monthly-usage.md) · `/statistics/monthly-usage`
- [월별 이용 현황 (세금, 계약) 전자계약 일별 현황](../manuals/statistics/monthly-usage__daily-electronic-contract.md) · `/statistics/monthly-usage/daily-electronic-contract`
- [월별 이용 현황 (세금, 계약) 세금계산서 일별 현황](../manuals/statistics/monthly-usage__daily-tax-invoice.md) · `/statistics/monthly-usage/daily-tax-invoice`
- [월별 세금계산서 이용 현황 (일반) 조회·관리](../manuals/statistics/monthly-tax-invoice-usage.md) · `/statistics/monthly-tax-invoice-usage`
- [월별 세금계산서 이용 현황 (일반) 일별 현황](../manuals/statistics/monthly-tax-invoice-usage__daily.md) · `/statistics/monthly-tax-invoice-usage/daily`
- [매출/매입 이용 현황 조회·관리](../manuals/statistics/sales-purchases-usage.md) · `/statistics/sales-purchases-usage`
- [세금계산서 일별 데이터 집계 조회·관리](../manuals/statistics/daily-tax-invoice-aggregate.md) · `/statistics/daily-tax-invoice-aggregate`

<a id="board"></a>
## 고객 게시판·문의 응대

스마트빌 고객에게 공지·자주 묻는 질문·자료를 제공하고 개별 문의에 답하는 업무다. 공개 안내 성격의 게시물과 고객별 문의·답글을 구분하여 내용을 관리한다.

- 주요 대상·용어: 공지: 서비스 안내 / FAQ: 자주 묻는 질문과 답변 / 1:1 문의: 개별 고객의 질문·답글 / 자료실: 설명과 첨부파일을 제공하는 게시판
- 업무 흐름: 게시판·문의 선택 → 목록 검색 → 내용 확인 또는 작성 → 필요 시 수정·답글 → 게시·응답 상태 확인
- 업무 구분: 공지·FAQ·자료실과 개인 문의는 공개 범위·업무 목적이 다르다. 상세 조회수 증가와 본문 변경을 구분하고 문의의 개인정보는 필요한 권한으로 확인한다.

- [공지사항 조회·관리](../manuals/customer-support/notice.md) · `/customer-support/notice`
- [공지사항 상세](../manuals/customer-support/notice__by-id.md) · `/customer-support/notice/:id`
- [공지사항 수정](../manuals/customer-support/notice__by-id__edit.md) · `/customer-support/notice/:id/edit`
- [공지사항 등록](../manuals/customer-support/notice__new.md) · `/customer-support/notice/new`
- [FAQ 조회·관리](../manuals/customer-support/faq.md) · `/customer-support/faq`
- [FAQ 상세](../manuals/customer-support/faq__by-id.md) · `/customer-support/faq/:id`
- [FAQ 수정](../manuals/customer-support/faq__by-id__edit.md) · `/customer-support/faq/:id/edit`
- [FAQ 등록](../manuals/customer-support/faq__new.md) · `/customer-support/faq/new`
- [1:1 문의 조회·관리](../manuals/customer-support/qna.md) · `/customer-support/qna`
- [1:1 문의 상세](../manuals/customer-support/qna__by-id.md) · `/customer-support/qna/:id`
- [1:1 문의 수정](../manuals/customer-support/qna__by-id__edit.md) · `/customer-support/qna/:id/edit`
- [1:1 문의 답글 등록](../manuals/customer-support/qna__by-id__reply.md) · `/customer-support/qna/:id/reply`
- [1:1 문의 등록](../manuals/customer-support/qna__new.md) · `/customer-support/qna/new`
- [자료실 조회·관리](../manuals/customer-support/pds.md) · `/customer-support/pds`
- [자료실 상세](../manuals/customer-support/pds__by-id.md) · `/customer-support/pds/:id`
- [자료실 수정](../manuals/customer-support/pds__by-id__edit.md) · `/customer-support/pds/:id/edit`
- [자료실 등록](../manuals/customer-support/pds__new.md) · `/customer-support/pds/new`

<a id="coupon"></a>
## 멤버십 쿠폰 운영

업체에 제공된 멤버십 쿠폰의 종류·유효성·발급 및 사용 이력을 확인하는 업무다. 고객이 보유 혜택이나 사용 결과를 문의할 때 해당 업체·쿠폰·기간을 맞춰 조사한다.

- 주요 대상·용어: 쿠폰: 업체에 제공된 혜택을 식별하는 단위 / 만료: 사용 가능한 기간이 종료된 상태 / 쿠폰 이력: 발급·사용 등 해당 쿠폰에 남은 기록
- 업무 흐름: 업체·쿠폰 식별 → 종류·상태·만료 확인 → 발급·사용 이력 비교
- 업무 구분: 쿠폰의 혜택·사용 이력과 현금성 예치금·입금·환불 내역은 다른 업무 대상이다. 이력 조회를 쿠폰 발급·사용 실행으로 해석하지 않는다.

- [쿠폰 조회 조회·관리](../manuals/customer-support/coupon.md) · `/customer-support/coupon`
- [쿠폰 조회 상세](../manuals/customer-support/coupon__by-couponNo.md) · `/customer-support/coupon/:couponNo`
- [쿠폰 이력 조회 조회·관리](../manuals/customer-support/coupon-history.md) · `/customer-support/coupon-history`

<a id="platform"></a>
## 연동 플랫폼 자료·문의 가이드

WEB·SAP·NSAP 등 서비스 연동 구분별로 자료와 문의 대응 가이드를 게시하는 업무다. 연동 담당자가 대상 플랫폼의 설명·첨부파일·댓글을 찾아 보고 필요한 게시물을 관리할 때 사용한다.

- 주요 대상·용어: WEB·SAP·NSAP: 현재 메뉴가 구분하는 연동 자료 영역 / 자료실: 설명·파일 게시 / 문의 가이드: 문의 대응 안내 / 연동업체 소스 관리: 관련 소스 자료 게시판
- 업무 흐름: 연동 구분·게시판 선택 → 게시물 검색 → 내용·첨부·댓글 확인 → 필요한 게시물 작성·수정
- 업무 구분: 같은 제목·파일명이어도 게시판 유형과 게시글 ID가 다르면 다른 자료다. 여기의 소스 게시글 관리와 운영반영 관리의 배포 계획 기록은 별개다.

- [WEB 자료실 조회·관리](../manuals/customer-support/web-resources.md) · `/customer-support/web-resources`
- [WEB 자료실 상세](../manuals/customer-support/web-resources__by-id.md) · `/customer-support/web-resources/:id`
- [WEB 자료실 수정](../manuals/customer-support/web-resources__by-id__edit.md) · `/customer-support/web-resources/:id/edit`
- [WEB 자료실 등록](../manuals/customer-support/web-resources__new.md) · `/customer-support/web-resources/new`
- [WEB 문의 가이드 조회·관리](../manuals/customer-support/web-inquiry-guide.md) · `/customer-support/web-inquiry-guide`
- [WEB 문의 가이드 상세](../manuals/customer-support/web-inquiry-guide__by-id.md) · `/customer-support/web-inquiry-guide/:id`
- [WEB 문의 가이드 수정](../manuals/customer-support/web-inquiry-guide__by-id__edit.md) · `/customer-support/web-inquiry-guide/:id/edit`
- [WEB 문의 가이드 등록](../manuals/customer-support/web-inquiry-guide__new.md) · `/customer-support/web-inquiry-guide/new`
- [SAP 자료실 조회·관리](../manuals/customer-support/sap-resources.md) · `/customer-support/sap-resources`
- [SAP 자료실 상세](../manuals/customer-support/sap-resources__by-id.md) · `/customer-support/sap-resources/:id`
- [SAP 자료실 수정](../manuals/customer-support/sap-resources__by-id__edit.md) · `/customer-support/sap-resources/:id/edit`
- [SAP 자료실 등록](../manuals/customer-support/sap-resources__new.md) · `/customer-support/sap-resources/new`
- [SAP 문의 가이드 조회·관리](../manuals/customer-support/sap-inquiry-guide.md) · `/customer-support/sap-inquiry-guide`
- [SAP 문의 가이드 상세](../manuals/customer-support/sap-inquiry-guide__by-id.md) · `/customer-support/sap-inquiry-guide/:id`
- [SAP 문의 가이드 수정](../manuals/customer-support/sap-inquiry-guide__by-id__edit.md) · `/customer-support/sap-inquiry-guide/:id/edit`
- [SAP 문의 가이드 등록](../manuals/customer-support/sap-inquiry-guide__new.md) · `/customer-support/sap-inquiry-guide/new`
- [NSAP 자료실 조회·관리](../manuals/customer-support/nsap-resources.md) · `/customer-support/nsap-resources`
- [NSAP 자료실 상세](../manuals/customer-support/nsap-resources__by-id.md) · `/customer-support/nsap-resources/:id`
- [NSAP 자료실 수정](../manuals/customer-support/nsap-resources__by-id__edit.md) · `/customer-support/nsap-resources/:id/edit`
- [NSAP 자료실 등록](../manuals/customer-support/nsap-resources__new.md) · `/customer-support/nsap-resources/new`
- [NSAP 문의 가이드 조회·관리](../manuals/customer-support/nsap-inquiry-guide.md) · `/customer-support/nsap-inquiry-guide`
- [NSAP 문의 가이드 상세](../manuals/customer-support/nsap-inquiry-guide__by-id.md) · `/customer-support/nsap-inquiry-guide/:id`
- [NSAP 문의 가이드 수정](../manuals/customer-support/nsap-inquiry-guide__by-id__edit.md) · `/customer-support/nsap-inquiry-guide/:id/edit`
- [NSAP 문의 가이드 등록](../manuals/customer-support/nsap-inquiry-guide__new.md) · `/customer-support/nsap-inquiry-guide/new`
- [연동업체 소스 관리 조회·관리](../manuals/customer-support/vendor-source-management.md) · `/customer-support/vendor-source-management`
- [연동업체 소스 관리 상세](../manuals/customer-support/vendor-source-management__by-id.md) · `/customer-support/vendor-source-management/:id`
- [연동업체 소스 관리 수정](../manuals/customer-support/vendor-source-management__by-id__edit.md) · `/customer-support/vendor-source-management/:id/edit`
- [연동업체 소스 관리 등록](../manuals/customer-support/vendor-source-management__new.md) · `/customer-support/vendor-source-management/new`

## 기준과 갱신

설명 보강일 2026-11-09, 소스 기준 `dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc`. 세부 기능·권한·부수 효과·DB 계약의 근거는 각 페이지 5·7번을 따른다. 도메인 설명을 바꿀 때 같은 영역의 페이지와 이 지도를 함께 갱신한다. [전체 조사 목록](../inventory/wbs-pages.md) · [실행 검증 범위](browser-verification.md).

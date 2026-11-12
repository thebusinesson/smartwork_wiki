# SmartWork 페이지별 매뉴얼 작성 대상

- 조사일: 2026-11-09 (한국 시간)
- 소스 기준: 현재 로컬 `main`, [dc216b313](https://github.com/thebusinesson/smartwork/commit/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc) (2026-11-06). 원격 최신 상태를 별도 fetch하지 않았음.
- 작성자 기준: `ryujiyoon <rjy927@businesson.co.kr>` (Git 설정 및 작성자 이력 대조).
- 작성자 이력 기간: 2026-02-24 ~ 2026-11-06. 현재 HEAD에서 도달 가능한 이력을 사용하며 병합 커밋은 작업 근거에서 제외.

## 집계

| 구분 | 메뉴 수 | 설명 |
|---|---:|---|
| A | 97 | 기능 개발·API 연동 또는 개별 동작 개선 근거 확인 |
| B | 113 | 검증·권한·검색 상태 유지·리팩터링 등 공통 개선 중심 |
| C | 6 | 해당 작성자의 페이지·전용 하위 구성요소 수정 근거 미확인 |
| 합계 | 216 | 사이드바 214개 + 권한 전용 메뉴 2개 |

작업 흔적이 확인되는 메뉴는 **210개**, 관련 URL은 **415개**다. 전체 등록 경로는 438개이며 리다이렉트 3개, 준비중 1개도 포함한다. 메뉴 없는 로그인·프로필 등의 공통 화면도 전체 경로 CSV에 포함했다.

## 분류와 사용 방법

1. A 메뉴부터 매뉴얼을 작성한다. 각 메뉴 아래의 목록·상세·등록·수정·이력·다운로드 화면은 `routes.csv`에서 메뉴ID로 묶어 확인한다.
2. B도 실제 작업 이력이 있는 메뉴다. 신규 개발 담당 화면만 문서화하려면 별도 범위 확인 후 포함한다. A/B는 최초 개발자 또는 단독 담당자를 뜻하지 않는다.
3. 분류는 커밋 제목과 변경 파일을 이용한 1차 판단이다. 페이지의 직접 이력과 같은 기능 폴더에서 재귀적으로 참조하는 API·훅·컴포넌트를 조사했다. 공용 유틸·타입 변경만으로 A로 분류하지 않았다. 같은 기능에서 공유하는 구성요소 수정도 포함되므로 대표 근거 파일과 커밋으로 재확인할 수 있다.
4. C는 작업하지 않았다는 단정이 아니다. 서버 파일만 수정한 커밋을 각 화면에 자동 연결하지 않았으며, 병합·다른 작성자 명의의 커밋·현재 HEAD 밖의 브랜치는 누락될 수 있다.
5. 아래 표의 경로 수는 해당 메뉴에 연결된 전체 등록 URL 수다. 개별 하위 경로의 작업 여부는 CSV에서 따로 구분한다. 작성 상태는 아직 모두 미작성이다.

## 메뉴 목록

각 항목의 근거 커밋은 대표 사례 1개다. 파일 경로와 전체 커밋 설명은 `menus.csv`, 화면별 근거는 `routes.csv`를 참조한다.

### A. 기능 개발·개별 개선 (97개)

#### SB 고객관리 > 스마트빌 회원·회사정보 관리

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M001 | 회원 정보 | `/member-management/member` | 3 | [e9096a1b2](https://github.com/thebusinesson/smartwork/commit/e9096a1b29ac4df295c4cf5324bccd222c2df50d) fix: 스마트빌 회원정보 관리 > 회원 정보 조회 진입 자동조회 방지 및 검색조건 필수화 |
| M004 | 회사 정보 | `/company-management/company-info` | 5 | [631252da8](https://github.com/thebusinesson/smartwork/commit/631252da89de9dc74a32dc2720177baa36d46449) feat/회사정보-조회 |
| M005 | 스마트빌 가입조회 | `/company-management/registration-inquiry` | 2 | [e7c9b2c76](https://github.com/thebusinesson/smartwork/commit/e7c9b2c767b3a0a1dd48a67c355ab97b4fd32e9d) feat/스마트빌-가입-조회 |

#### SB 고객관리 > 예외 관리

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M009 | [업체]예외 처리 정보 | `/exception-management/exception-vendor` | 3 | [81e6c7790](https://github.com/thebusinesson/smartwork/commit/81e6c779049c8460f85f6bbf21121fd95891db22) fix: 예외 서비스 전체 해제 저장 시 확인창을 삭제 문구로 표시, 목록 삭제 안내 반영 |
| M010 | [비회원]예외 처리 정보 | `/exception-management/exception-non-member` | 2 | [81e6c7790](https://github.com/thebusinesson/smartwork/commit/81e6c779049c8460f85f6bbf21121fd95891db22) fix: 예외 서비스 전체 해제 저장 시 확인창을 삭제 문구로 표시, 목록 삭제 안내 반영 |

#### SB 고객관리 > 스마트빌 이용 현황

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M012 | 가입 현황 | `/smartbill-status/status` | 1 | [1c7ad2453](https://github.com/thebusinesson/smartwork/commit/1c7ad2453a2177b173636469c50b08c22bd7fc4e) feat/스마트빌 이용 현황 > 가입 현황 조회 API 및 FE 연동 |
| M013 | 탈퇴 현황 | `/smartbill-status/withdrawal-status` | 1 | [e70e51259](https://github.com/thebusinesson/smartwork/commit/e70e51259211305551ff3cd2489a24de85447804) feat: 스마트빌 이용 현황 > 가입/탈퇴 현황 엑셀 다운로드 및 탈퇴 조회 API |

#### SB 고객관리 > 글로싸인 엔터프라이즈

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M014 | 회원 정보 | `/glosign-enterprise/members` | 1 | [1c23f6129](https://github.com/thebusinesson/smartwork/commit/1c23f61290358543a3256ef2ec0834ce61744d87) feat: 글로싸인 엔터프라이즈 > 회원 정보 구현                                             - BE: 회사/회원 목록 + 유저 목록… |
| M015 | 회사 정보 | `/glosign-enterprise/companies` | 2 | [1c23f6129](https://github.com/thebusinesson/smartwork/commit/1c23f61290358543a3256ef2ec0834ce61744d87) feat: 글로싸인 엔터프라이즈 > 회원 정보 구현                                             - BE: 회사/회원 목록 + 유저 목록… |
| M016 | 비밀번호 초기화 | `/glosign-enterprise/status` | 1 | [19ced5f00](https://github.com/thebusinesson/smartwork/commit/19ced5f00e0c6eac095da416edd8ffe5b83feb5a) fix: 글로싸인 엔터프라이즈 비밀번호 초기화 및 회원/회사 정보 화면 개선 |
| M017 | 열람인증 초기화 | `/glosign-enterprise/personal-password-reset` | 1 | [1c23f6129](https://github.com/thebusinesson/smartwork/commit/1c23f61290358543a3256ef2ec0834ce61744d87) feat: 글로싸인 엔터프라이즈 > 회원 정보 구현                                             - BE: 회사/회원 목록 + 유저 목록… |

#### SB 서비스관리 > 전자세금계산서

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M018 | 세금계산서 조회 | `/tax-invoice/tax-invoice` | 3 | [c70c176a5](https://github.com/thebusinesson/smartwork/commit/c70c176a5ad3041f169773fab86b81f7ce2f9e40) 세금계산서 페이지 api 연동 2 |
| M019 | 과거 세금계산서 조회 | `/tax-invoice/legacy-tax-invoice` | 3 | [c70c176a5](https://github.com/thebusinesson/smartwork/commit/c70c176a5ad3041f169773fab86b81f7ce2f9e40) 세금계산서 페이지 api 연동 2 |
| M020 | 수신자 변경 이력 조회 | `/tax-invoice/recipient-change-history` | 1 | [e4d4cff1a](https://github.com/thebusinesson/smartwork/commit/e4d4cff1a23fee0b28d44bc7524080fc83dfabfe) feat/세금계산서-조회 |
| M033 | 거래명세서 조회 | `/tax-invoice/transaction-statement` | 2 | [56362ddd3](https://github.com/thebusinesson/smartwork/commit/56362ddd3eb7ca17e561a17fe6c02b13d2006208) feat/단독-거래명세서-조회 |
| M034 | 지로세금계산서 조회 | `/tax-invoice/giro-tax-invoice` | 1 | [c70c176a5](https://github.com/thebusinesson/smartwork/commit/c70c176a5ad3041f169773fab86b81f7ce2f9e40) 세금계산서 페이지 api 연동 2 |

#### SB 서비스관리 > 세금계산서 운영/관리

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M045 | 대량서비스 모니터링 | `/tax-operations/bulk-service-monitoring` | 1 | [55e151f45](https://github.com/thebusinesson/smartwork/commit/55e151f453a2fd7a9c32d5ea80f7087d877d3eae) feat: 대량서비스 모니터링 발행 건수 요약 추가 |

#### SB 서비스관리 > 국세청 전송 관리

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M054 | 일자별 전송결과 | `/nts-transmission/transmission-results-by-date` | 1 | [590d2d299](https://github.com/thebusinesson/smartwork/commit/590d2d299b9992d53f9809c9726fe4cde11fe4a1) fix: 국세청전송 상세결과 참조번호 길어질 때 페이징 버튼 숨김 현상 수정 |
| M056 | 국세청 전송 설정 관리 | `/nts-transmission/transmission-settings` | 1 | [631252da8](https://github.com/thebusinesson/smartwork/commit/631252da89de9dc74a32dc2720177baa36d46449) feat/회사정보-조회 |

#### SB 서비스관리 > 전자계약

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M063 | 삼양사 사용내역 조회 | `/electronic-contract/samyang-usage-history` | 1 | [d5809daab](https://github.com/thebusinesson/smartwork/commit/d5809daabe0c6f5c07e6ca61f276f4a8bd7a2fa6) fix: 삼양사 사용내역 조회 빈 결과 문구를 해당월 기준으로 변경 |

#### SB 서비스관리 > 채권잔액 확인 서비스

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M072 | 채권잔액 확인서 조회 | `/bond-service/bond-balance-inquiry` | 2 | [45b6f7a1a](https://github.com/thebusinesson/smartwork/commit/45b6f7a1a5ac2858eca9f1b2a34278bb0592e994) feat: 채권잔액 확인 서비스 > 채권잔액 확인서 조회                                           - BE: 채권잔액 확인서 파일 다운로… |
| M073 | 담당자 권한 조회 | `/bond-service/drc-right` | 2 | [1b8c11da5](https://github.com/thebusinesson/smartwork/commit/1b8c11da5dea5e90e0a5d19514aec29b10b68919) feat/채권잔액 확인 서비스 > 담당자 권한 조회 API 및 FE 구현 |
| M074 | 연동업체 관리 | `/bond-service/drc-company-link` | 3 | [60a2fa713](https://github.com/thebusinesson/smartwork/commit/60a2fa7131c6fa50ab91ca5a0e82f453ccb6a76a) feat/채권잔액 확인 서비스 > 연동업체 관련 API 및 FE 구현 |
| M075 | 연동 로그 조회 | `/bond-service/integration-log` | 1 | [63da60931](https://github.com/thebusinesson/smartwork/commit/63da60931456aa6a8e750c9a149f83001dda6a97) - 채권잔액 확인 서비스 > 연동 로그 조회 API 및 FE 구현   - BE:참조번호/사업자번호+기간 2가지 모드 로그 검색 API 추가   - BE: 레거시 SP 직접… |
| M076 | 연동업체 장애 관리 | `/bond-service/integration-partner-error` | 2 | [e21bf7b88](https://github.com/thebusinesson/smartwork/commit/e21bf7b885cf9af546aae4bbaa5a43fed7da42f6) feat/채권잔액 확인 서비스 > 연동 업체 장애 관리 API 및 FE 구현 |
| M077 | 채권잔액 전송 관리 | `/bond-service/receivable-balance-transfer` | 2 | [ff56b1507](https://github.com/thebusinesson/smartwork/commit/ff56b15071f5546cb09b40d2ff0af4d625641bb6) feat/채권잔액 확인 서비스 > 채권잔액 전송 관리 API 및 FE 구현 - BE: 3 엔드포인트 추가 — /api/v1/bond-service/receivable-ba… |

#### SB 서비스관리 > 홈택스 DTI 수집

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M080 | 모니터링 | `/hometax-dti/monitoring` | 1 | [d26b721a2](https://github.com/thebusinesson/smartwork/commit/d26b721a22bddd9209b9c477d3afaf525509073b) feat/홈택스-DTI-수집 > 모니터링 BE/FE 신규 구현 |
| M081 | 인증키 관리 | `/hometax-dti/auth-key` | 2 | [f7c95e685](https://github.com/thebusinesson/smartwork/commit/f7c95e68552fc01746f20a3525b29a79ca7f99d1) feat/홈택스-DTI-수집 > 인증키 관리 BE/FE 신규 구현 |
| M082 | 오류 로그 조회 | `/hometax-dti/error-logs` | 1 | [84405966c](https://github.com/thebusinesson/smartwork/commit/84405966c787af4e468f899e458d54b75aba0316) feat/홈택스-DTI-수집 > 오류 로그 조회 BE/FE 신규 구현 |
| M083 | 인증서 등록 현황 조회 | `/hometax-dti/certificate-status` | 1 | [3c542995f](https://github.com/thebusinesson/smartwork/commit/3c542995f33b9465415ee833dcb5ccf5250035ee) feat/홈택스-DTI-수집 > 인증서 등록 현황 조회 BE/FE 신규 구현 + 오류 로그 조회 UI 개선 |
| M084 | 인증서 만료일 관리 | `/hometax-dti/certificate-expiry` | 1 | [48aa86373](https://github.com/thebusinesson/smartwork/commit/48aa8637327e5910f45ee66c00976f9a24cd89da) feat/홈택스-DTI-수집 > 인증서 만료일 관리 BE/FE 신규 구현 |
| M085 | 인증서 로그인 실패 조회 | `/hometax-dti/login-failures` | 1 | [d7e696c0c](https://github.com/thebusinesson/smartwork/commit/d7e696c0cc27dd57ee3a6c9b0d54c7941737ceda) feat/홈택스-DTI-수집 > 인증서 로그인 실패 조회 BE/FE 신규 구현 |
| M086 | 이메일파싱 모니터링 | `/hometax-dti/email-parsing` | 1 | [313db672f](https://github.com/thebusinesson/smartwork/commit/313db672f8d404acd7ee92df5980df2ed0a45760) feat/홈택스-DTI-수집 > 이메일파싱 모니터링 BE/FE 신규 구현 |

#### SB 서비스관리 > 오픈스크랩

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M090 | 매출/매입 조회 | `/openscrap/sales-purchases` | 2 | [345bbe1e0](https://github.com/thebusinesson/smartwork/commit/345bbe1e070afd114f2da4eb2a98e38a9ee6a3fb) feat: 오픈스크랩 매출/매입 조회 공급자·공급받는자에 '전체' 옵션 추가 및 승인번호 단독 조회 허용 |

#### SB 서비스관리 > 보나뱅크

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M092 | 회사 정보 | `/bonabank/company` | 4 | [631252da8](https://github.com/thebusinesson/smartwork/commit/631252da89de9dc74a32dc2720177baa36d46449) feat/회사정보-조회 |
| M093 | 회원 정보 | `/bonabank/member` | 2 | [9d37890de](https://github.com/thebusinesson/smartwork/commit/9d37890de7a86cf63574f33ca91d3d7cf6ff8be3) feat/보나뱅크 > 회원 정보 BE/FE 신규 구현 + 디테일 페이지 |
| M094 | 세금계산서 조회 | `/bonabank/tax-invoice` | 2 | [9266a6acc](https://github.com/thebusinesson/smartwork/commit/9266a6acc7acffec4337cdd3a4879699bd68a127) feat/보나뱅크 > 세금계산서 조회 BE/FE 신규 구현 + 상세 페이지 |
| M095 | 세금계산서 통계 | `/bonabank/tax-invoice-statistics` | 1 | [9cb07a9f6](https://github.com/thebusinesson/smartwork/commit/9cb07a9f6d0a6bc8165cd884766460d6bd043856) feat/보나뱅크 > 세금계산서 통계 BE/FE 신규 구현   - BE: 세금계산서 통계 도메인 신규 (taxstatistics)     - 4 endpoint (/mon… |
| M096 | 국세청 신고 실패 조회 | `/bonabank/nts-failures` | 1 | [24d978c98](https://github.com/thebusinesson/smartwork/commit/24d978c98ebfddde19bc4f04e296ce72bb2af58f) feat/보나뱅크 > 국세청 신고 실패 조회 BE/FE 신규 구현                                           - BE: 국세청 신고 실패 … |
| M097 | 공지사항 관리 | `/bonabank/notices` | 4 | [69d2baa78](https://github.com/thebusinesson/smartwork/commit/69d2baa7837bc24251c0e5f03dcfd22a97376438) feat/보나뱅크 > 공지사항 CRUD BE/FE 신규 구현 + 회원 탈퇴처리 노출 |

#### SB 운영관리 > 오류 관리

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M098 | 오류 접수/등록 | `/error-management/error-reports/new` | 1 | [449de62a0](https://github.com/thebusinesson/smartwork/commit/449de62a01ff6aa5cf5a35557d5d1fed37118f25) feat/오류-관리 브랜치 작업 요약 (오류 접수/등록, 전체 오류 조회/처리)   api/operations/error/   - 컨트롤러 5종     - ErrorRec… |
| M099 | 전체 오류 조회/처리 | `/error-management/error-reports` | 3 | [449de62a0](https://github.com/thebusinesson/smartwork/commit/449de62a01ff6aa5cf5a35557d5d1fed37118f25) feat/오류-관리 브랜치 작업 요약 (오류 접수/등록, 전체 오류 조회/처리)   api/operations/error/   - 컨트롤러 5종     - ErrorRec… |
| M100 | 오류 코드 관리 | `/error-management/error-code-management` | 3 | [786f1c5d3](https://github.com/thebusinesson/smartwork/commit/786f1c5d3141ea442506b19c3616d23e2a027095) feat/오류-관리 > 오류 코드 관리                                                        BE — 신규 모듈 전체 (unt… |

#### SB 운영관리 > 운영반영 관리

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M101 | 소스 관리 | `/source-management/source-management` | 4 | [4045cac79](https://github.com/thebusinesson/smartwork/commit/4045cac79f229e8a76f0c6b640fe3d84bb507602) feat/운영반영-관리 |

#### SB 운영관리 > 시스템 관리

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M104 | 시스템 SMS 모니터링 | `/system-management/sms-monitoring` | 1 | [4ff6961f2](https://github.com/thebusinesson/smartwork/commit/4ff6961f239fda529dff11b4d0b191a9f3487aa7) fix: 시스템 SMS 모니터링 active 체크박스 제한 해제 및 토글 시 정렬 고정 |
| M108 | 연동 서버 모니터링 | `/system-management/server-monitoring` | 1 | [f926d8a43](https://github.com/thebusinesson/smartwork/commit/f926d8a43a5c938d8e70cfb3f9aed80f0bdf56cb) feat: 연동 서버 모니터링 허브업체명 클릭 시 허브업체 서비스 점검 관리 상세로 이동 |
| M111 | 웹링크 식별자 관리 | `/system-management/weblink-identifier` | 4 | [9cda83026](https://github.com/thebusinesson/smartwork/commit/9cda83026aa4d20ca3b1d4ed64c65636956c40c5) feat: 웹링크 식별자 CONFIRM_KEY 자동생성을 사업자번호 기반 규칙으로 변경 |
| M113 | 서버 시간 관리 | `/system-management/server-time-management` | 1 | [638c59bc2](https://github.com/thebusinesson/smartwork/commit/638c59bc24827b1480c2e39b064e33ac4ec6f00c) feat: 서버 시간 관리 서버 간 시간 오차 행 붉은 배경 표시 |

#### 서비스 현황 > 요금관리

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M120 | 클로버 관리 | `/billing-management/clover-charge` | 3 | [6a241fd4e](https://github.com/thebusinesson/smartwork/commit/6a241fd4e117359685c3e3fd8fbdd87adfdb37bc) fix: 클로버 관리 조회 검색조건이 DB까지 전달되지 않던 문제 수정 |

#### 서비스 현황 > 입금관리

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M122 | 입금 현황 조회 | `/payment/status` | 2 | [9b7aeb05c](https://github.com/thebusinesson/smartwork/commit/9b7aeb05cffd685596795b08121422eb6d21119d) - 입금 현황 조회 API 개발 - 입금 현황 상세 조회 API 개발 - error code 정의 |
| M123 | 예치금 관리 | `/payment/deposit` | 2 | [6e8da3ee3](https://github.com/thebusinesson/smartwork/commit/6e8da3ee37148999a8e992f78de1339a47e29974) - 예치금 관리 상세조회 API 개발 - 입금 처리 API 개발 - 입금 취소 API 개발 - 소멸 처리 API 개발 |
| M124 | 일별 예치금 조회 | `/payment/daily-deposit-inquiry` | 2 | [6e8da3ee3](https://github.com/thebusinesson/smartwork/commit/6e8da3ee37148999a8e992f78de1339a47e29974) - 예치금 관리 상세조회 API 개발 - 입금 처리 API 개발 - 입금 취소 API 개발 - 소멸 처리 API 개발 |
| M125 | 벌크식계좌 입금 관리 | `/payment/bulk-account-deposit` | 2 | [3dba8b1c9](https://github.com/thebusinesson/smartwork/commit/3dba8b1c9c66c8d14182c8b8638b0036da1f85f3) 벌크식 계좌 입금 관리 목록 API 개발 |
| M130 | 본사 입금 등록 | `/payment/head-office-deposit-register` | 2 | [9fe5daa53](https://github.com/thebusinesson/smartwork/commit/9fe5daa53f22dc8e2fe2f962fd9674766b11cc97) fix: 첨부파일 필수 안내를 업로드 시도 후에만 빨간 오류로 표시 |
| M132 | (EB13/EB14) CMS 계좌 관리 | `/payment/cms-account` | 9 | [29d5a2ae5](https://github.com/thebusinesson/smartwork/commit/29d5a2ae5923c02319fbbe09e34de64b0a99e7a8) fix: CMS 상세 페이지 검색창 키 입력마다 API 호출되는 문제 수정 |
| M133 | (EB21/EB22) CMS 자동이체 관리 | `/payment/cms-withdrawal-request` | 9 | [29d5a2ae5](https://github.com/thebusinesson/smartwork/commit/29d5a2ae5923c02319fbbe09e34de64b0a99e7a8) fix: CMS 상세 페이지 검색창 키 입력마다 API 호출되는 문제 수정 |
| M136 | 무통장입금 취소내역 조회 | `/payment/bank-transfer-cancel` | 1 | [353b6c6be](https://github.com/thebusinesson/smartwork/commit/353b6c6bed71051a065733b8c8645dfe55177691) 무통장 입금 취소 내역 조회 API 개발 |
| M137 | 환불 관리 | `/payment/refund-management` | 4 | [7b0c6cca4](https://github.com/thebusinesson/smartwork/commit/7b0c6cca4500c77397deece305a22aa33e54e2eb) 환불 관리 조회 목록 API 개발 |

#### 서비스 현황 > 미납 예외업체 관리

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M139 | 미납 예외업체 관리 | `/service-overview/unpaid-exception-manager` | 1 | [ca92aad8a](https://github.com/thebusinesson/smartwork/commit/ca92aad8a6904e285710e637db6bf69ba07a5542) 미납 예외 업체 목록 API 개발 미납 예외 상세 API 개발 미납 예외 삭제 API 개발 미납 예외 수정 API 개발 |

#### 서비스 현황 > 통계 정보

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M141 | 월별 이용 현황 (세금, 계약) | `/statistics/monthly-usage` | 3 | [c6aff211a](https://github.com/thebusinesson/smartwork/commit/c6aff211ac4ba714c011390fc00eb720004f300a) feat/통계-정보 > 월별 이용 현황 (세금, 계약) |
| M142 | 월별 세금계산서 이용 현황 (일반) | `/statistics/monthly-tax-invoice-usage` | 2 | [714dc1540](https://github.com/thebusinesson/smartwork/commit/714dc1540d69b0c5d25c27fae859f55b32bbd12a) fix: 월별 세금계산서 이용 현황 다운로드 다이얼로그 닫힘·상세 타이틀 수정 |
| M143 | 매출/매입 이용 현황 | `/statistics/sales-purchases-usage` | 1 | [33182a250](https://github.com/thebusinesson/smartwork/commit/33182a2505b8782fd6b61323be17687d863b3ac9) feat/통계-정보 |
| M144 | 세금계산서 일별 데이터 집계 | `/statistics/daily-tax-invoice-aggregate` | 1 | [b43a4dbb6](https://github.com/thebusinesson/smartwork/commit/b43a4dbb62e6d7e2cdb8a7644a172f68209d00af) fix: 세금계산서 일별 데이터 집계 다운로드 다이얼로그 닫힘·목록 페이징 수정 |
| M152 | 보나뱅크 발행 현황 | `/statistics/bonabank-issue` | 1 | [763b005e2](https://github.com/thebusinesson/smartwork/commit/763b005e2ecd07e2defcbf26d74b643a32bcdaba) feat: 보나뱅크 발행 현황 발행월 기준 일별 발행건수 다운로드로 변경 |
| M153 | 허브업체 이용 현황 | `/statistics/hub-company-usage` | 2 | [c6e86dd09](https://github.com/thebusinesson/smartwork/commit/c6e86dd0903b59de67f0c88b68328c95c64b8069) fix: 허브업체 이용 현황 목록 정렬·기간 표기 및 상세 조회기간/정렬 수정 |
| M154 | 서비스별 매출액 조회 | `/statistics/service-sales` | 1 | [cbbefd3de](https://github.com/thebusinesson/smartwork/commit/cbbefd3de767ab83567fd06719e43a44eb82c17d) fix: 서비스별 매출액 합계행 추가 및 틸코블렛 조회월 기본값 세팅 |
| M157 | 현금영수증 틸코블렛 API 호출 현황 | `/statistics/cash-receipt-tilko-bullet-api-call` | 1 | [cbbefd3de](https://github.com/thebusinesson/smartwork/commit/cbbefd3de767ab83567fd06719e43a44eb82c17d) fix: 서비스별 매출액 합계행 추가 및 틸코블렛 조회월 기본값 세팅 |
| M159 | 매출채권 데이터 다운로드 | `/statistics/ar-data-download` | 1 | [c0867544c](https://github.com/thebusinesson/smartwork/commit/c0867544c0ca474495601bb2d72c602a4bb49211) fix: 매출채권 데이터 다운로드 팝업 타이틀 중복 표시 수정 |

#### 연동 서비스 관리 > 연동 서비스 관리

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M173 | 연동업체 문의 처리 | `/hub-service/inquiry-management` | 4 | [9c7e12391](https://github.com/thebusinesson/smartwork/commit/9c7e123913f9dca097fd1f91bcb4af4d80351944) feat: 연동업체 문의 처리 등록/수정/목록 기능 구현 및 정합화 |
| M174 | 허브업체 서비스 점검 관리 | `/hub-service/maintenance` | 2 | [6a193f993](https://github.com/thebusinesson/smartwork/commit/6a193f993a07b60f7ee48d0f39631834079f317c) feat: 허브업체 서비스 점검 관리 BE API 구현 및 FE 연동 |
| M175 | OpenAPI 로그 조회 | `/hub-service/openapi-log` | 2 | [d3cad41a5](https://github.com/thebusinesson/smartwork/commit/d3cad41a54cd351a63ebc3d153b6486199a36011) fix: 참조번호 검색 입력칸 너비 확대 |

#### 연동 서비스 관리 > 서비스 공지 메일관리

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M185 | 고객 이메일 발송 | `/hub-service/service-notice-email/customer-email-send` | 1 | [14dfaa49b](https://github.com/thebusinesson/smartwork/commit/14dfaa49bf6520290961662e1d937d1e15e25fde) feat: 허브 서비스 점검 상세 서버주소 표시·점검일자 직접입력 개선 (#PR) |
| M186 | 메일 발송 업체 관리 | `/hub-service/service-notice-email` | 3 | [fcf735980](https://github.com/thebusinesson/smartwork/commit/fcf735980ca3f89cdd8e92b68bf9bd2b80d0c6a0) feat: 서비스 공지 이메일 BE API 구현 (메일링 업체 CRUD·발송·이력) |
| M187 | 메일 발송 고객 정보 조회 | `/hub-service/service-notice-email/send-history` | 1 | [6a193f993](https://github.com/thebusinesson/smartwork/commit/6a193f993a07b60f7ee48d0f39631834079f317c) feat: 허브업체 서비스 점검 관리 BE API 구현 및 FE 연동 |

#### 광고/마케팅 운영 관리 > 광고배너 관리

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M188 | 광고배너 등록 및 조회 | `/banner/management` | 3 | [a39309d97](https://github.com/thebusinesson/smartwork/commit/a39309d97c61a62e38dcacf476636114a9c48cf7) feat: 광고배너 등록 및 조회 API 개발 및 화면 연동 |
| M189 | 키워드 배너등록 | `/banner/keyword` | 3 | [b5441e283](https://github.com/thebusinesson/smartwork/commit/b5441e2832610f6e472c8078e1cb98c67d41b069) feat: 키워드 배너등록 API 개발 및 화면 연동 |
| M190 | 키워드 모수 조회 | `/banner/keyword-volume` | 1 | [bc476fc73](https://github.com/thebusinesson/smartwork/commit/bc476fc73e692e846592231cb881039d278595aa) feat: 키워드 모수 조회 API 개발 및 화면 연동 |
| M191 | 신규 검색페이지별 검색어로그 | `/banner/search-term-log` | 1 | [c3aaf7d83](https://github.com/thebusinesson/smartwork/commit/c3aaf7d83c132b735e2daab8eea48f2ef0530b28) feat: 신규 검색페이지별 검색어로그 API 개발 및 화면 연동 |

#### 광고/마케팅 운영 관리 > 배너 통계정보

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M192 | 배너광고 효과 측정 | `/banner/effect-measurement` | 1 | [4443e78ec](https://github.com/thebusinesson/smartwork/commit/4443e78ec7963d13b8685839e36c53249216381a) fix: 배너광고 효과 측정 전 그룹 조회 및 광고배너 저장 구조 개선 |
| M193 | 배너광고 통계 | `/banner/daily-statistics` | 1 | [b86d1c713](https://github.com/thebusinesson/smartwork/commit/b86d1c71357c35e54daf86570502630668fbddbc) fix: 배너 통계 화면·다운로드의 배너 위치 코드값을 표시명으로 노출 |
| M194 | 키워드 배너 광고 통계 | `/banner/keyword-daily-statistics` | 2 | [2ce6502c8](https://github.com/thebusinesson/smartwork/commit/2ce6502c85765ec209055bc75b9493825aec07b5) feat: 키워드 배너 광고 통계 API 개발 및 화면 연동 |

#### 고객지원 > 고객 게시판 관리

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M195 | 공지사항 | `/customer-support/notice` | 4 | [68f3953a3](https://github.com/thebusinesson/smartwork/commit/68f3953a35aa5647faf08409444f268f0b0c0514) feat: 고객지원 > 공지사항 BE/FE 신규 구현 (SBAdmin 이관) |
| M196 | FAQ | `/customer-support/faq` | 4 | [b17b6e731](https://github.com/thebusinesson/smartwork/commit/b17b6e731bd6bfd3a9b67e626e371a67a743c7c2) feat: 고객지원 > FAQ BE/FE 신규 구현 (SBAdmin 이관) |
| M197 | 1:1 문의 | `/customer-support/qna` | 5 | [c076223dd](https://github.com/thebusinesson/smartwork/commit/c076223dd91eb0edcbca0fc88b4398d5744a3750) feat: 고객지원 > 1:1 문의 / 자료실 BE/FE 신규 구현 (SBAdmin 이관) |
| M198 | 자료실 | `/customer-support/pds` | 4 | [c076223dd](https://github.com/thebusinesson/smartwork/commit/c076223dd91eb0edcbca0fc88b4398d5744a3750) feat: 고객지원 > 1:1 문의 / 자료실 BE/FE 신규 구현 (SBAdmin 이관) |

#### 고객지원 > 고객 문의 관리

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M199 | 서비스 도입 문의 | `/customer-support/service-inquiry` | 3 | [7ea36c8ef](https://github.com/thebusinesson/smartwork/commit/7ea36c8ef07cff9829e1dd22c133959c463a575a) feat: 서비스 도입 문의 FE 연동 (신규 BE API 사용) |
| M200 | 제휴 문의 | `/customer-support/affiliation-inquiry` | 2 | [5dff4c4a2](https://github.com/thebusinesson/smartwork/commit/5dff4c4a25e11556a79986bce6f2e7984f7e3ff6) feat: 제휴 문의 API 연동 및 화면 구현 |
| M201 | 블랙리스트 관리 | `/customer-support/blacklist` | 1 | [e52f88691](https://github.com/thebusinesson/smartwork/commit/e52f886918b914556a31befaa07ce4b143bb9eb0) 고객지원 > 고객 문의 관리 > 블랙리스트 관리 |

#### 고객지원 > 멤버십 쿠폰관리

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M202 | 쿠폰 조회 | `/customer-support/coupon` | 2 | [9e7f4ccdf](https://github.com/thebusinesson/smartwork/commit/9e7f4ccdfa51a2679318811791de168b544b127b) feat: 고객지원 > 멤버십 쿠폰관리 > 쿠폰 조회 BE/FE 신규 구현 (SBAdmin 이관) |
| M203 | 쿠폰 이력 조회 | `/customer-support/coupon-history` | 1 | [1d36e0519](https://github.com/thebusinesson/smartwork/commit/1d36e0519c48df04e325dfb24763cfe80f81fe02) feat: 고객지원 > 멤버십 쿠폰관리 > 쿠폰 이력 조회 BE 신규 구현 (SBAdmin 이관) |

#### 고객지원 > 서비스 플랫폼 관리(자료실)

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M204 | WEB 자료실 | `/customer-support/web-resources` | 4 | [973d9e026](https://github.com/thebusinesson/smartwork/commit/973d9e026a99250221d989322e3f5fb390dd0b9d) feat: 고객지원 > 서비스 플랫폼 관리(자료실) > WEB 자료실 BE/FE 신규 구현 (SBAdmin 이관) |
| M205 | WEB 문의 가이드 | `/customer-support/web-inquiry-guide` | 4 | [973d9e026](https://github.com/thebusinesson/smartwork/commit/973d9e026a99250221d989322e3f5fb390dd0b9d) feat: 고객지원 > 서비스 플랫폼 관리(자료실) > WEB 자료실 BE/FE 신규 구현 (SBAdmin 이관) |
| M206 | SAP 자료실 | `/customer-support/sap-resources` | 4 | [973d9e026](https://github.com/thebusinesson/smartwork/commit/973d9e026a99250221d989322e3f5fb390dd0b9d) feat: 고객지원 > 서비스 플랫폼 관리(자료실) > WEB 자료실 BE/FE 신규 구현 (SBAdmin 이관) |
| M207 | SAP 문의 가이드 | `/customer-support/sap-inquiry-guide` | 4 | [973d9e026](https://github.com/thebusinesson/smartwork/commit/973d9e026a99250221d989322e3f5fb390dd0b9d) feat: 고객지원 > 서비스 플랫폼 관리(자료실) > WEB 자료실 BE/FE 신규 구현 (SBAdmin 이관) |
| M208 | NSAP 자료실 | `/customer-support/nsap-resources` | 4 | [973d9e026](https://github.com/thebusinesson/smartwork/commit/973d9e026a99250221d989322e3f5fb390dd0b9d) feat: 고객지원 > 서비스 플랫폼 관리(자료실) > WEB 자료실 BE/FE 신규 구현 (SBAdmin 이관) |
| M209 | NSAP 문의 가이드 | `/customer-support/nsap-inquiry-guide` | 4 | [973d9e026](https://github.com/thebusinesson/smartwork/commit/973d9e026a99250221d989322e3f5fb390dd0b9d) feat: 고객지원 > 서비스 플랫폼 관리(자료실) > WEB 자료실 BE/FE 신규 구현 (SBAdmin 이관) |
| M210 | 연동업체 소스 관리 | `/customer-support/vendor-source-management` | 4 | [973d9e026](https://github.com/thebusinesson/smartwork/commit/973d9e026a99250221d989322e3f5fb390dd0b9d) feat: 고객지원 > 서비스 플랫폼 관리(자료실) > WEB 자료실 BE/FE 신규 구현 (SBAdmin 이관) |

### B. 검증·공통 개선 중심 (113개)

#### SB 고객관리 > 스마트빌 회원·회사정보 관리

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M002 | 아이디/비밀번호 관리 | `/member-management/id-password` | 1 | [183d37ddd](https://github.com/thebusinesson/smartwork/commit/183d37ddd0167f5bc029ba5e69bb7ba59c9ce49b) refactor: 검색 필수값 검증을 전역 스키마로 전환 |
| M003 | 회원 이메일 다운로드 | `/member-management/email-download` | 2 | [8185c6108](https://github.com/thebusinesson/smartwork/commit/8185c6108ab47334a6bde322856e771ad0aafe8e) feat: 회원 이메일 다운로드 업체 조건 필수 검증 RHF+Zod 전환 (#927) |
| M006 | 휴폐업 조회 | `/company-management/suspended-closed-inquiry` | 1 | [571e3fac6](https://github.com/thebusinesson/smartwork/commit/571e3fac6c568a4674a6ce9947f32a3906c7099d) feat: 휴폐업 조회 과세유형·폐업일자 등록 RHF+Zod 전환, 오류 인라인 표시 (CUS-18) (#927) |
| M007 | 대량 회원가입 (권한 전용) | `/member-management/member/bulk-registration` | 1 | [36cf91070](https://github.com/thebusinesson/smartwork/commit/36cf9107031c303f954c1cbda5551753767647c9) refactor: customer·status·marketing·support/board 스키마 파일 제거(DSL 변환 후 인라인), useRhfForm·전역 프리셋 적용 |
| M008 | 회원 비밀번호 초기화 (권한 전용) | `/member-management/id-password/password-reset` | 1 | [e8da746f6](https://github.com/thebusinesson/smartwork/commit/e8da746f603341b11ee3c53ef0b41e82bd4d0295) feat: 메뉴 권한 기반 액션 버튼 게이팅 및 등록/수정 라우트 진입 차단 (#513) |

#### SB 고객관리 > 예외 관리

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M011 | SMS 수신거부 관리 | `/exception-management/sms-opt-out` | 1 | [e8da746f6](https://github.com/thebusinesson/smartwork/commit/e8da746f603341b11ee3c53ef0b41e82bd4d0295) feat: 메뉴 권한 기반 액션 버튼 게이팅 및 등록/수정 라우트 진입 차단 (#513) |

#### SB 서비스관리 > 전자세금계산서

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M021 | 내 거래처 조회 | `/tax-invoice/my-customers` | 1 | [4cdfd5fcd](https://github.com/thebusinesson/smartwork/commit/4cdfd5fcdef94066e789a79b1ea13174e7666432) fix: 중복 EmptyState 렌더링 제거 |
| M022 | 담당자 권한 조회 | `/tax-invoice/manager-permission` | 1 | [842470e34](https://github.com/thebusinesson/smartwork/commit/842470e34664f1f1da56d73864c699199ee08a34) feat: 전자세금계산서 남은 조회 화면 SearchFilter 기반 RHF+Zod 통일, 업체 조건 '전체' 외 입력 필수 |
| M023 | 부서 조회 | `/tax-invoice/departments` | 1 | [842470e34](https://github.com/thebusinesson/smartwork/commit/842470e34664f1f1da56d73864c699199ee08a34) feat: 전자세금계산서 남은 조회 화면 SearchFilter 기반 RHF+Zod 통일, 업체 조건 '전체' 외 입력 필수 |
| M024 | 지사(사업장) 조회 | `/tax-invoice/branches` | 1 | [842470e34](https://github.com/thebusinesson/smartwork/commit/842470e34664f1f1da56d73864c699199ee08a34) feat: 전자세금계산서 남은 조회 화면 SearchFilter 기반 RHF+Zod 통일, 업체 조건 '전체' 외 입력 필수 |
| M025 | 마감설정 조회 | `/tax-invoice/closing-settings` | 1 | [842470e34](https://github.com/thebusinesson/smartwork/commit/842470e34664f1f1da56d73864c699199ee08a34) feat: 전자세금계산서 남은 조회 화면 SearchFilter 기반 RHF+Zod 통일, 업체 조건 '전체' 외 입력 필수 |
| M026 | 매입 자동 승인 설정 조회 | `/tax-invoice/purchase-auto-approval-settings` | 1 | [458082db7](https://github.com/thebusinesson/smartwork/commit/458082db73af1dba170b79119aea5a3154861fb8) feat: 매입 자동 승인 설정 조회 체크박스 필수 검증 RHF+Zod 적용, 토스트 대신 인라인 오류 |
| M027 | 알림발송 서비스 설정 조회 | `/tax-invoice/notification-service-settings` | 1 | [842470e34](https://github.com/thebusinesson/smartwork/commit/842470e34664f1f1da56d73864c699199ee08a34) feat: 전자세금계산서 남은 조회 화면 SearchFilter 기반 RHF+Zod 통일, 업체 조건 '전체' 외 입력 필수 |
| M028 | 알림발송 서비스 이용내역 | `/tax-invoice/notification-service-history` | 1 | [842470e34](https://github.com/thebusinesson/smartwork/commit/842470e34664f1f1da56d73864c699199ee08a34) feat: 전자세금계산서 남은 조회 화면 SearchFilter 기반 RHF+Zod 통일, 업체 조건 '전체' 외 입력 필수 |
| M029 | 이벤트당첨(역매입대납) 업체 조회 | `/tax-invoice/event-winner-vendors` | 1 | [842470e34](https://github.com/thebusinesson/smartwork/commit/842470e34664f1f1da56d73864c699199ee08a34) feat: 전자세금계산서 남은 조회 화면 SearchFilter 기반 RHF+Zod 통일, 업체 조건 '전체' 외 입력 필수 |
| M030 | 다운로드 요청/처리 조회 | `/tax-invoice/download-requests` | 1 | [842470e34](https://github.com/thebusinesson/smartwork/commit/842470e34664f1f1da56d73864c699199ee08a34) feat: 전자세금계산서 남은 조회 화면 SearchFilter 기반 RHF+Zod 통일, 업체 조건 '전체' 외 입력 필수 |
| M031 | 비회원 수신 비밀번호 조회 | `/tax-invoice/guest-password` | 1 | [79eb408b7](https://github.com/thebusinesson/smartwork/commit/79eb408b7a40768f9e643779cab4c9fee9da99a7) feat: 목록 체크박스 일괄처리 권한 게이팅 + 연동오류 로그 행 클릭 이동 |
| M032 | 비회원 수신설정 조회 | `/tax-invoice/guest-reception-settings` | 1 | [842470e34](https://github.com/thebusinesson/smartwork/commit/842470e34664f1f1da56d73864c699199ee08a34) feat: 전자세금계산서 남은 조회 화면 SearchFilter 기반 RHF+Zod 통일, 업체 조건 '전체' 외 입력 필수 |
| M035 | 지로 원본 다운로드 | `/tax-invoice/giro-original-download` | 1 | [79eb408b7](https://github.com/thebusinesson/smartwork/commit/79eb408b7a40768f9e643779cab4c9fee9da99a7) feat: 목록 체크박스 일괄처리 권한 게이팅 + 연동오류 로그 행 클릭 이동 |
| M036 | 국세청 전송 현황 | `/tax-invoice/nts-transmission-status` | 1 | [7be44798a](https://github.com/thebusinesson/smartwork/commit/7be44798a50d1c164c1c53199a8ae05b6efe6471) fix: 국세청 전송 현황·개별 조회 SearchFilter 와 중복되는 필수값 토스트 제거 |
| M037 | 국세청 전송 개별 조회 | `/tax-invoice/nts-transmission` | 1 | [e8da746f6](https://github.com/thebusinesson/smartwork/commit/e8da746f603341b11ee3c53ef0b41e82bd4d0295) feat: 메뉴 권한 기반 액션 버튼 게이팅 및 등록/수정 라우트 진입 차단 (#513) |
| M038 | SMTP 전송결과 조회 | `/tax-invoice/smtp-transmission-results` | 1 | [842470e34](https://github.com/thebusinesson/smartwork/commit/842470e34664f1f1da56d73864c699199ee08a34) feat: 전자세금계산서 남은 조회 화면 SearchFilter 기반 RHF+Zod 통일, 업체 조건 '전체' 외 입력 필수 |

#### SB 서비스관리 > 세금계산서 운영/관리

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M039 | Error 발생 현황 | `/tax-operations/error-status` | 1 | [594f8ad76](https://github.com/thebusinesson/smartwork/commit/594f8ad7682892751db29fd0a0f654a297501667) feat: 세금계산서 운영/관리 검색 화면 RHF+Zod 통일, 참조번호별 로그 조회 참조번호 필수 검증 추가 |
| M040 | 참조번호별 로그 조회 | `/tax-operations/reference-log` | 2 | [594f8ad76](https://github.com/thebusinesson/smartwork/commit/594f8ad7682892751db29fd0a0f654a297501667) feat: 세금계산서 운영/관리 검색 화면 RHF+Zod 통일, 참조번호별 로그 조회 참조번호 필수 검증 추가 |
| M041 | 사업자별 로그 조회 | `/tax-operations/logs-by-business` | 1 | [594f8ad76](https://github.com/thebusinesson/smartwork/commit/594f8ad7682892751db29fd0a0f654a297501667) feat: 세금계산서 운영/관리 검색 화면 RHF+Zod 통일, 참조번호별 로그 조회 참조번호 필수 검증 추가 |
| M042 | 연동오류 로그조회 | `/tax-operations/integration-error-logs` | 1 | [79eb408b7](https://github.com/thebusinesson/smartwork/commit/79eb408b7a40768f9e643779cab4c9fee9da99a7) feat: 목록 체크박스 일괄처리 권한 게이팅 + 연동오류 로그 행 클릭 이동 |
| M043 | 상태불일치 조회 | `/tax-operations/status-mismatch` | 1 | [594f8ad76](https://github.com/thebusinesson/smartwork/commit/594f8ad7682892751db29fd0a0f654a297501667) feat: 세금계산서 운영/관리 검색 화면 RHF+Zod 통일, 참조번호별 로그 조회 참조번호 필수 검증 추가 |
| M044 | 상태불일치 처리 등록 | `/tax-operations/status-mismatch-register` | 1 | [79eb408b7](https://github.com/thebusinesson/smartwork/commit/79eb408b7a40768f9e643779cab4c9fee9da99a7) feat: 목록 체크박스 일괄처리 권한 게이팅 + 연동오류 로그 행 클릭 이동 |
| M046 | 국세청전송 마감일 관리 | `/nts-transmission/transmission-deadlines` | 1 | [e8da746f6](https://github.com/thebusinesson/smartwork/commit/e8da746f603341b11ee3c53ef0b41e82bd4d0295) feat: 메뉴 권한 기반 액션 버튼 게이팅 및 등록/수정 라우트 진입 차단 (#513) |
| M047 | 공휴일 관리 | `/tax-operations/holiday-management` | 1 | [79eb408b7](https://github.com/thebusinesson/smartwork/commit/79eb408b7a40768f9e643779cab4c9fee9da99a7) feat: 목록 체크박스 일괄처리 권한 게이팅 + 연동오류 로그 행 클릭 이동 |
| M048 | 합계표 마감일 관리 | `/tax-operations/summary-deadline-management` | 2 | [79eb408b7](https://github.com/thebusinesson/smartwork/commit/79eb408b7a40768f9e643779cab4c9fee9da99a7) feat: 목록 체크박스 일괄처리 권한 게이팅 + 연동오류 로그 행 클릭 이동 |
| M049 | 지연발행일 관리 | `/tax-operations/delayed-issuance-management` | 2 | [79eb408b7](https://github.com/thebusinesson/smartwork/commit/79eb408b7a40768f9e643779cab4c9fee9da99a7) feat: 목록 체크박스 일괄처리 권한 게이팅 + 연동오류 로그 행 클릭 이동 |
| M050 | 참조/승인번호 변경 | `/tax-operations/reference-approval-change` | 1 | [e8da746f6](https://github.com/thebusinesson/smartwork/commit/e8da746f603341b11ee3c53ef0b41e82bd4d0295) feat: 메뉴 권한 기반 액션 버튼 게이팅 및 등록/수정 라우트 진입 차단 (#513) |

#### SB 서비스관리 > 국세청 전송 관리

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M051 | 예약전송 모니터링 | `/nts-transmission/scheduled-transmission-monitoring` | 2 | [ac9452c4c](https://github.com/thebusinesson/smartwork/commit/ac9452c4c7e9baac8823e0b9f7c9db34d9934539) feat: 목록→상세 화면 전반에 검색조건·조회결과 유지 기능 확대 적용 |
| M052 | 전송 전 오류 조회 | `/nts-transmission/pre-transmission-errors` | 2 | [ac9452c4c](https://github.com/thebusinesson/smartwork/commit/ac9452c4c7e9baac8823e0b9f7c9db34d9934539) feat: 목록→상세 화면 전반에 검색조건·조회결과 유지 기능 확대 적용 |
| M053 | 처리결과 오류 조회 | `/nts-transmission/result-errors` | 2 | [ac9452c4c](https://github.com/thebusinesson/smartwork/commit/ac9452c4c7e9baac8823e0b9f7c9db34d9934539) feat: 목록→상세 화면 전반에 검색조건·조회결과 유지 기능 확대 적용 |
| M055 | 전송 거부업체 조회 | `/nts-transmission/rejected-vendors` | 1 | [541aa9f6d](https://github.com/thebusinesson/smartwork/commit/541aa9f6d313a0a01f8bd217625a7d01129abadf) feat: 국세청 전송 관리 기간 조회 화면 5곳 기간 필수 검증 RHF+Zod 적용, 오류 인라인 표시 |
| M057 | 국세청 수집 관리 조회 | `/nts-transmission/collection-management` | 1 | [1c5bcc84a](https://github.com/thebusinesson/smartwork/commit/1c5bcc84a31367e84427da944f8cf456ebffad8b) feat: 국세청 수집 관리 조회 사업자번호 검증 RHF+Zod 통일, 토스트 제거 |

#### SB 서비스관리 > 전자계약

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M058 | 전자계약 조회 | `/electronic-contract/electronic-contract-inquiry` | 2 | [2cadedb3f](https://github.com/thebusinesson/smartwork/commit/2cadedb3f612444b7db20a21ea377a27d4810ed8) feat: 전자계약 검색 화면 8곳 RHF+Zod 통일, 업체 조건 '전체' 외 입력 필수·참조번호/사용월 필수 검증 |
| M059 | 담당자 권한 조회 | `/electronic-contract/manager-access-info` | 1 | [7380f1ca0](https://github.com/thebusinesson/smartwork/commit/7380f1ca02f500018e8ee06dcb0f2ff3525fb759) feat: 전자계약 담당자 권한·용량 조회 업체 조건 검증 RHF+Zod 적용, 2자 미만 검색어 오류 인라인 표시 |
| M060 | 전자계약 용량 조회 | `/electronic-contract/electronic-contract-capacity` | 2 | [7380f1ca0](https://github.com/thebusinesson/smartwork/commit/7380f1ca02f500018e8ee06dcb0f2ff3525fb759) feat: 전자계약 담당자 권한·용량 조회 업체 조건 검증 RHF+Zod 적용, 2자 미만 검색어 오류 인라인 표시 |
| M061 | 다운로드 조회 | `/electronic-contract/download-history` | 1 | [2cadedb3f](https://github.com/thebusinesson/smartwork/commit/2cadedb3f612444b7db20a21ea377a27d4810ed8) feat: 전자계약 검색 화면 8곳 RHF+Zod 통일, 업체 조건 '전체' 외 입력 필수·참조번호/사용월 필수 검증 |
| M062 | 단방향 이용 고객 조회 | `/electronic-contract/one-way-user` | 3 | [e8da746f6](https://github.com/thebusinesson/smartwork/commit/e8da746f603341b11ee3c53ef0b41e82bd4d0295) feat: 메뉴 권한 기반 액션 버튼 게이팅 및 등록/수정 라우트 진입 차단 (#513) |
| M064 | 연동업체 관리 | `/electronic-contract/linked-vendor-manage` | 3 | [e8da746f6](https://github.com/thebusinesson/smartwork/commit/e8da746f603341b11ee3c53ef0b41e82bd4d0295) feat: 메뉴 권한 기반 액션 버튼 게이팅 및 등록/수정 라우트 진입 차단 (#513) |
| M065 | 참조번호별 로그 조회 | `/electronic-contract/reference-log` | 1 | [2cadedb3f](https://github.com/thebusinesson/smartwork/commit/2cadedb3f612444b7db20a21ea377a27d4810ed8) feat: 전자계약 검색 화면 8곳 RHF+Zod 통일, 업체 조건 '전체' 외 입력 필수·참조번호/사용월 필수 검증 |
| M066 | 연동업체 장애관리 | `/electronic-contract/linked-vendor-failure` | 2 | [e8da746f6](https://github.com/thebusinesson/smartwork/commit/e8da746f603341b11ee3c53ef0b41e82bd4d0295) feat: 메뉴 권한 기반 액션 버튼 게이팅 및 등록/수정 라우트 진입 차단 (#513) |
| M067 | 스마트빌 인증서 관리 | `/electronic-contract/smartbill-certificate` | 3 | [79eb408b7](https://github.com/thebusinesson/smartwork/commit/79eb408b7a40768f9e643779cab4c9fee9da99a7) feat: 목록 체크박스 일괄처리 권한 게이팅 + 연동오류 로그 행 클릭 이동 |
| M068 | 전자계약 오류 조회 | `/electronic-contract/error-inquiry` | 2 | [e8da746f6](https://github.com/thebusinesson/smartwork/commit/e8da746f603341b11ee3c53ef0b41e82bd4d0295) feat: 메뉴 권한 기반 액션 버튼 게이팅 및 등록/수정 라우트 진입 차단 (#513) |

#### SB 서비스관리 > 구매확인서

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M069 | 구매확인서 조회 | `/purchase-confirmation/purchase-confirmation` | 2 | [ac9452c4c](https://github.com/thebusinesson/smartwork/commit/ac9452c4c7e9baac8823e0b9f7c9db34d9934539) feat: 목록→상세 화면 전반에 검색조건·조회결과 유지 기능 확대 적용 |
| M070 | 송신거래 약정키 등록 | `/purchase-confirmation/transmission-agreement-key` | 3 | [79eb408b7](https://github.com/thebusinesson/smartwork/commit/79eb408b7a40768f9e643779cab4c9fee9da99a7) feat: 목록 체크박스 일괄처리 권한 게이팅 + 연동오류 로그 행 클릭 이동 |
| M071 | 식별자 정보 등록 | `/purchase-confirmation/identifier-key` | 3 | [79eb408b7](https://github.com/thebusinesson/smartwork/commit/79eb408b7a40768f9e643779cab4c9fee9da99a7) feat: 목록 체크박스 일괄처리 권한 게이팅 + 연동오류 로그 행 클릭 이동 |

#### SB 서비스관리 > SCM

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M078 | 카페 조회 | `/smartbill-scm/cafe` | 2 | [ac9452c4c](https://github.com/thebusinesson/smartwork/commit/ac9452c4c7e9baac8823e0b9f7c9db34d9934539) feat: 목록→상세 화면 전반에 검색조건·조회결과 유지 기능 확대 적용 |
| M079 | SCM 조회 | `/smartbill-scm/scm` | 4 | [e8da746f6](https://github.com/thebusinesson/smartwork/commit/e8da746f603341b11ee3c53ef0b41e82bd4d0295) feat: 메뉴 권한 기반 액션 버튼 게이팅 및 등록/수정 라우트 진입 차단 (#513) |

#### SB 서비스관리 > 오픈스크랩

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M088 | 모니터링 | `/openscrap/monitoring` | 2 | [ac9452c4c](https://github.com/thebusinesson/smartwork/commit/ac9452c4c7e9baac8823e0b9f7c9db34d9934539) feat: 목록→상세 화면 전반에 검색조건·조회결과 유지 기능 확대 적용 |
| M089 | 업체 관리 | `/openscrap/vendors` | 2 | [e8da746f6](https://github.com/thebusinesson/smartwork/commit/e8da746f603341b11ee3c53ef0b41e82bd4d0295) feat: 메뉴 권한 기반 액션 버튼 게이팅 및 등록/수정 라우트 진입 차단 (#513) |
| M091 | 오류 로그 조회 | `/openscrap/error-logs` | 1 | [e25494a6b](https://github.com/thebusinesson/smartwork/commit/e25494a6bd2e920b768075ff45de4d60e9583b4c) feat: 오픈스크랩 모니터링·업체·매출매입·오류 로그 조회 검색 검증 RHF+Zod 적용, 기본 일자를 초기화 시점에 재계산 |

#### SB 운영관리 > 시스템 관리

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M102 | 서버 용량 관리 | `/system-management/server-capacity` | 2 | [c73b2abad](https://github.com/thebusinesson/smartwork/commit/c73b2abadacd53da5dc6b2025a2d02e26e934cb7) feat: 시스템 관리 일자·기간 검색 조회 일자 필수 검증 RHF+Zod 적용, 오류 인라인 표시 |
| M103 | 시스템 모니터링 | `/system-management/system-monitoring` | 1 | [c73b2abad](https://github.com/thebusinesson/smartwork/commit/c73b2abadacd53da5dc6b2025a2d02e26e934cb7) feat: 시스템 관리 일자·기간 검색 조회 일자 필수 검증 RHF+Zod 적용, 오류 인라인 표시 |
| M107 | 이메일 전송 모니터링 | `/system-management/email-monitoring` | 2 | [c73b2abad](https://github.com/thebusinesson/smartwork/commit/c73b2abadacd53da5dc6b2025a2d02e26e934cb7) feat: 시스템 관리 일자·기간 검색 조회 일자 필수 검증 RHF+Zod 적용, 오류 인라인 표시 |
| M109 | 업무 리스트 | `/system-management/work` | 1 | [c73b2abad](https://github.com/thebusinesson/smartwork/commit/c73b2abadacd53da5dc6b2025a2d02e26e934cb7) feat: 시스템 관리 일자·기간 검색 조회 일자 필수 검증 RHF+Zod 적용, 오류 인라인 표시 |
| M110 | 업무 리스트 등록 | `/system-management/work/register` | 3 | [e8da746f6](https://github.com/thebusinesson/smartwork/commit/e8da746f603341b11ee3c53ef0b41e82bd4d0295) feat: 메뉴 권한 기반 액션 버튼 게이팅 및 등록/수정 라우트 진입 차단 (#513) |
| M112 | 업무개선 및 요청리스트 | `/system-management/request-improve` | 4 | [e8da746f6](https://github.com/thebusinesson/smartwork/commit/e8da746f603341b11ee3c53ef0b41e82bd4d0295) feat: 메뉴 권한 기반 액션 버튼 게이팅 및 등록/수정 라우트 진입 차단 (#513) |
| M114 | 빌서버 연결 서버 | `/system-management/build-server-connection` | 1 | [c73b2abad](https://github.com/thebusinesson/smartwork/commit/c73b2abadacd53da5dc6b2025a2d02e26e934cb7) feat: 시스템 관리 일자·기간 검색 조회 일자 필수 검증 RHF+Zod 적용, 오류 인라인 표시 |
| M115 | 접속이력관리 | `/system-management/access-history` | 2 | [ac9452c4c](https://github.com/thebusinesson/smartwork/commit/ac9452c4c7e9baac8823e0b9f7c9db34d9934539) feat: 목록→상세 화면 전반에 검색조건·조회결과 유지 기능 확대 적용 |

#### 서비스 현황 > 요금관리

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M116 | 일별 이용료 발행 | `/billing-management/daily-usage-fee-billing` | 1 | [79eb408b7](https://github.com/thebusinesson/smartwork/commit/79eb408b7a40768f9e643779cab4c9fee9da99a7) feat: 목록 체크박스 일괄처리 권한 게이팅 + 연동오류 로그 행 클릭 이동 |
| M117 | 결제 방식별 일일 정산 | `/billing-management/daily-settlement-by-payment` | 1 | [4cdfd5fcd](https://github.com/thebusinesson/smartwork/commit/4cdfd5fcdef94066e789a79b1ea13174e7666432) fix: 중복 EmptyState 렌더링 제거 |
| M118 | 영수 대량 발행 | `/billing-management/bulk-receipt-issue` | 1 | [82f74d3f9](https://github.com/thebusinesson/smartwork/commit/82f74d3f9dac7bfc107c3cab7c2706bbca09d083) feat: 영수 대량 발행·오류 로그 조회 검색 검증 RHF+Zod 적용, 작성일자 필수 오류 인라인 표시 |
| M119 | 영수 대량 발행 오류 로그 조회 | `/billing-management/bulk-receipt-issue-logs` | 1 | [82f74d3f9](https://github.com/thebusinesson/smartwork/commit/82f74d3f9dac7bfc107c3cab7c2706bbca09d083) feat: 영수 대량 발행·오류 로그 조회 검색 검증 RHF+Zod 적용, 작성일자 필수 오류 인라인 표시 |
| M121 | KT 대납 리스트 | `/billing-management/kt-proxy-payment-list` | 1 | [d15919756](https://github.com/thebusinesson/smartwork/commit/d159197562db037b218816343070e8c8e2270e70) feat: KT 대납 리스트·일별 이용료 발행·결제 방식별 일일 정산 검색 검증 RHF+Zod 적용, 오류 인라인 표시 |

#### 서비스 현황 > 입금관리

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M126 | 본사 입금 관리 | `/payment/head-office-deposit` | 2 | [79eb408b7](https://github.com/thebusinesson/smartwork/commit/79eb408b7a40768f9e643779cab4c9fee9da99a7) feat: 목록 체크박스 일괄처리 권한 게이팅 + 연동오류 로그 행 클릭 이동 |
| M127 | 단발성 입금 관리 | `/payment/os-iv-deposit` | 1 | [fa415b230](https://github.com/thebusinesson/smartwork/commit/fa415b23073fb5784b13085182df14ea5e78d0f6) feat: 청구/입금 행 단위 상태 처리를 실행(EXECUTE) 권한으로 전환 |
| M128 | 단발성 매출·입금 등록 | `/payment/manual-transactions` | 4 | [30118f01d](https://github.com/thebusinesson/smartwork/commit/30118f01d2c5fd9d20d67d1f1a5d15378655ed80) feat: 목록 페이지 일괄선택에 "전체/페이지" 선택 범위 구분 추가 |
| M129 | 단발성 거래처 관리 | `/payment/manual-clients` | 4 | [ac9f86fcc](https://github.com/thebusinesson/smartwork/commit/ac9f86fccfbe29eb5e6feb24a4ad0aecd1299436) feat: 단발성 매출·입금·거래처 목록 검색과 등록·수정·복사작성 검증 RHF+Zod 적용, 오류 인라인 표시 |
| M131 | (EB11) CMS 통합 변경내역 반영 | `/payment/cms-integration` | 2 | [e8da746f6](https://github.com/thebusinesson/smartwork/commit/e8da746f603341b11ee3c53ef0b41e82bd4d0295) feat: 메뉴 권한 기반 액션 버튼 게이팅 및 등록/수정 라우트 진입 차단 (#513) |
| M134 | 업체별 CMS 계좌 현황 | `/payment/cms-account-status` | 1 | [c2c3a3e91](https://github.com/thebusinesson/smartwork/commit/c2c3a3e91896b91fd6054fd654194d3f319d8e6c) feat: CMS 계좌·자동이체 검색, 신청 생성, EB11 파일 등록, 결과 파일 업로드 검증 RHF+Zod 적용, 오류 인라인 표시 |
| M135 | 신용카드 자동결제 승인요청 | `/payment/credit-card-auto-payment` | 2 | [854f6e42d](https://github.com/thebusinesson/smartwork/commit/854f6e42d3b640980bdab2c0cb2d31d6ca30a338) fix: 실행 권한 전환 검증에서 발견한 불일치 5건 수정 |
| M138 | 출금신청 예외처리 관리 | `/payment/withdrawal-exception` | 4 | [e8da746f6](https://github.com/thebusinesson/smartwork/commit/e8da746f603341b11ee3c53ef0b41e82bd4d0295) feat: 메뉴 권한 기반 액션 버튼 게이팅 및 등록/수정 라우트 진입 차단 (#513) |

#### 서비스 현황 > 채권 관리

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M140 | 매출 채권 현황 다운로드 | `/ar-management/account-receivable-status-download` | 6 | [79eb408b7](https://github.com/thebusinesson/smartwork/commit/79eb408b7a40768f9e643779cab4c9fee9da99a7) feat: 목록 체크박스 일괄처리 권한 게이팅 + 연동오류 로그 행 클릭 이동 |

#### 서비스 현황 > 통계 정보

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M145 | 세금계산서 매출 분석 다운로드 | `/statistics/dti-sales-analysis` | 1 | [abbee1c8b](https://github.com/thebusinesson/smartwork/commit/abbee1c8bd3db3e7216aee3bd8cee81ac7a3781a) feat: 통계 정보 월·연도 단일 필수 다운로드 화면 검증 RHF+Zod 적용, 오류 인라인 표시 |
| M146 | 웹→연동 인식 사업장 발행현황 | `/statistics/web-link-issue` | 1 | [abbee1c8b](https://github.com/thebusinesson/smartwork/commit/abbee1c8bd3db3e7216aee3bd8cee81ac7a3781a) feat: 통계 정보 월·연도 단일 필수 다운로드 화면 검증 RHF+Zod 적용, 오류 인라인 표시 |
| M147 | 월별 고객·매출 통합 현황 | `/statistics/monthly-customer-sales` | 1 | [abbee1c8b](https://github.com/thebusinesson/smartwork/commit/abbee1c8bd3db3e7216aee3bd8cee81ac7a3781a) feat: 통계 정보 월·연도 단일 필수 다운로드 화면 검증 RHF+Zod 적용, 오류 인라인 표시 |
| M148 | 월별 웹·연동 고객 현황 | `/statistics/monthly-web-link-customer` | 1 | [abbee1c8b](https://github.com/thebusinesson/smartwork/commit/abbee1c8bd3db3e7216aee3bd8cee81ac7a3781a) feat: 통계 정보 월·연도 단일 필수 다운로드 화면 검증 RHF+Zod 적용, 오류 인라인 표시 |
| M149 | 전자계약 서비스 월간 지표 | `/statistics/dct-monthly-metrics` | 1 | [abbee1c8b](https://github.com/thebusinesson/smartwork/commit/abbee1c8bd3db3e7216aee3bd8cee81ac7a3781a) feat: 통계 정보 월·연도 단일 필수 다운로드 화면 검증 RHF+Zod 적용, 오류 인라인 표시 |
| M150 | 청구 월별 웹·연동 고객 사용 데이터 | `/statistics/billing-monthly-web-link-usage` | 1 | [abbee1c8b](https://github.com/thebusinesson/smartwork/commit/abbee1c8bd3db3e7216aee3bd8cee81ac7a3781a) feat: 통계 정보 월·연도 단일 필수 다운로드 화면 검증 RHF+Zod 적용, 오류 인라인 표시 |
| M151 | 신규 연동 고객 등록 현황 | `/statistics/new-link-registration` | 1 | [abbee1c8b](https://github.com/thebusinesson/smartwork/commit/abbee1c8bd3db3e7216aee3bd8cee81ac7a3781a) feat: 통계 정보 월·연도 단일 필수 다운로드 화면 검증 RHF+Zod 적용, 오류 인라인 표시 |
| M155 | OpenAPI 사용현황 | `/statistics/open-api-usage` | 1 | [583149fd7](https://github.com/thebusinesson/smartwork/commit/583149fd78df3a83b6c9236e92de2eba93e26829) feat: 통계 정보 조회 화면 검색 검증 RHF+Zod 적용, 업체 조건·조회기간 필수 오류 인라인 표시 |
| M156 | WORKPLACE 월별 OAPI 사용량 집계 | `/statistics/workplace-monthly-oapi-usage` | 1 | [583149fd7](https://github.com/thebusinesson/smartwork/commit/583149fd78df3a83b6c9236e92de2eba93e26829) feat: 통계 정보 조회 화면 검색 검증 RHF+Zod 적용, 업체 조건·조회기간 필수 오류 인라인 표시 |
| M158 | 매출 데이터 다운로드 | `/statistics/sales-data-download` | 1 | [38c2d8f2a](https://github.com/thebusinesson/smartwork/commit/38c2d8f2abd5c2450bac6c1f892ac8bf4d7489f0) feat: 매출 채권·매출 데이터 다운로드 섹션별 검증 RHF+Zod 적용, 오류 인라인 표시 |
| M160 | 휴폐업 업체 요약 | `/statistics/suspended-closed-company-summary` | 1 | [583149fd7](https://github.com/thebusinesson/smartwork/commit/583149fd78df3a83b6c9236e92de2eba93e26829) feat: 통계 정보 조회 화면 검색 검증 RHF+Zod 적용, 업체 조건·조회기간 필수 오류 인라인 표시 |
| M161 | 휴폐업 업체 리스트 | `/statistics/suspended-closed-company` | 1 | [583149fd7](https://github.com/thebusinesson/smartwork/commit/583149fd78df3a83b6c9236e92de2eba93e26829) feat: 통계 정보 조회 화면 검색 검증 RHF+Zod 적용, 업체 조건·조회기간 필수 오류 인라인 표시 |

#### 연동 협업 관리 > 연동 협업 관리

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M162 | 영업 관리 | `/hub-collab/sales-management` | 4 | [e8da746f6](https://github.com/thebusinesson/smartwork/commit/e8da746f603341b11ee3c53ef0b41e82bd4d0295) feat: 메뉴 권한 기반 액션 버튼 게이팅 및 등록/수정 라우트 진입 차단 (#513) |
| M163 | 프로젝트 완료 관리 | `/hub-collab/project-completion` | 1 | [79eb408b7](https://github.com/thebusinesson/smartwork/commit/79eb408b7a40768f9e643779cab4c9fee9da99a7) feat: 목록 체크박스 일괄처리 권한 게이팅 + 연동오류 로그 행 클릭 이동 |
| M164 | System Key 관리 | `/hub-collab/system-key-management` | 4 | [e8da746f6](https://github.com/thebusinesson/smartwork/commit/e8da746f603341b11ee3c53ef0b41e82bd4d0295) feat: 메뉴 권한 기반 액션 버튼 게이팅 및 등록/수정 라우트 진입 차단 (#513) |
| M165 | 벌크계좌 관리 | `/hub-collab/bulk-account-management` | 3 | [79eb408b7](https://github.com/thebusinesson/smartwork/commit/79eb408b7a40768f9e643779cab4c9fee9da99a7) feat: 목록 체크박스 일괄처리 권한 게이팅 + 연동오류 로그 행 클릭 이동 |

#### 연동/허브 업체 관리 > 연동/허브 업체 관리

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M166 | 허브업체 관리 | `/hub-vendor/hub-vendor-management` | 5 | [e8da746f6](https://github.com/thebusinesson/smartwork/commit/e8da746f603341b11ee3c53ef0b41e82bd4d0295) feat: 메뉴 권한 기반 액션 버튼 게이팅 및 등록/수정 라우트 진입 차단 (#513) |
| M167 | 연동플랫폼 통합관리 | `/hub-vendor/platform-management` | 3 | [e8da746f6](https://github.com/thebusinesson/smartwork/commit/e8da746f603341b11ee3c53ef0b41e82bd4d0295) feat: 메뉴 권한 기반 액션 버튼 게이팅 및 등록/수정 라우트 진입 차단 (#513) |
| M168 | [구연동]연동업체 관리 | `/hub-vendor/vendor-management` | 6 | [e8da746f6](https://github.com/thebusinesson/smartwork/commit/e8da746f603341b11ee3c53ef0b41e82bd4d0295) feat: 메뉴 권한 기반 액션 버튼 게이팅 및 등록/수정 라우트 진입 차단 (#513) |
| M169 | [차세대]연동업체 관리 | `/hub-vendor/nextgen-vendor-management` | 4 | [e8da746f6](https://github.com/thebusinesson/smartwork/commit/e8da746f603341b11ee3c53ef0b41e82bd4d0295) feat: 메뉴 권한 기반 액션 버튼 게이팅 및 등록/수정 라우트 진입 차단 (#513) |
| M170 | 첨부파일 연동업체관리 | `/hub-vendor/attachment-vendor-management` | 3 | [e8da746f6](https://github.com/thebusinesson/smartwork/commit/e8da746f603341b11ee3c53ef0b41e82bd4d0295) feat: 메뉴 권한 기반 액션 버튼 게이팅 및 등록/수정 라우트 진입 차단 (#513) |
| M171 | OpenAPI 허브 관리 | `/hub-vendor/openapi-hub-management` | 3 | [e8da746f6](https://github.com/thebusinesson/smartwork/commit/e8da746f603341b11ee3c53ef0b41e82bd4d0295) feat: 메뉴 권한 기반 액션 버튼 게이팅 및 등록/수정 라우트 진입 차단 (#513) |
| M172 | 조직도/비회원 연동 사용 조회 | `/hub-vendor/orgchart-guest-integration` | 1 | [416749b7f](https://github.com/thebusinesson/smartwork/commit/416749b7fd9f794fbfa4b150d5449e046ad66f5c) feat: 허브업체·연동업체·플랫폼·OpenAPI 허브·조직도 목록 검색과 허브업체 등록·수정 검증 RHF+Zod 적용, 업체 조건 필수 오류 인라인 표시 |

#### 연동 서비스 관리 > 연동 서비스 관리

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M176 | OpenAPI 인증토큰 관리 | `/hub-service/openapi-auth-token` | 1 | [88c719141](https://github.com/thebusinesson/smartwork/commit/88c71914150549d633c83e67f26320aed5762f29) feat: 허브업체 서비스 점검·OpenAPI 로그·인증토큰 목록 검색 검증 RHF+Zod 적용, 오류 인라인 표시 |
| M177 | 인증서 OID 관리 | `/hub-service/certificate-oid` | 3 | [e8da746f6](https://github.com/thebusinesson/smartwork/commit/e8da746f603341b11ee3c53ef0b41e82bd4d0295) feat: 메뉴 권한 기반 액션 버튼 게이팅 및 등록/수정 라우트 진입 차단 (#513) |
| M178 | 연동업체 라우팅 일괄 변경 | `/hub-service/vendor-routing-bulk-change` | 1 | [b1b6fd480](https://github.com/thebusinesson/smartwork/commit/b1b6fd48033870134044c6fd5e133695950cb8d4) feat: 라우팅 일괄 변경과 구연동 라우팅 예외 등록 검증 RHF+Zod 적용, 오류 인라인 표시 |
| M179 | [구연동] 라우팅 예외 관리 | `/hub-service/routing-exception` | 1 | [79eb408b7](https://github.com/thebusinesson/smartwork/commit/79eb408b7a40768f9e643779cab4c9fee9da99a7) feat: 목록 체크박스 일괄처리 권한 게이팅 + 연동오류 로그 행 클릭 이동 |
| M180 | 자동이체 예외 설정 | `/hub-service/auto-transfer-exception` | 3 | [e8da746f6](https://github.com/thebusinesson/smartwork/commit/e8da746f603341b11ee3c53ef0b41e82bd4d0295) feat: 메뉴 권한 기반 액션 버튼 게이팅 및 등록/수정 라우트 진입 차단 (#513) |
| M181 | [구연동] 복구솔루션 | `/hub-service/status-change-recovery` | 1 | [e8da746f6](https://github.com/thebusinesson/smartwork/commit/e8da746f603341b11ee3c53ef0b41e82bd4d0295) feat: 메뉴 권한 기반 액션 버튼 게이팅 및 등록/수정 라우트 진입 차단 (#513) |
| M183 | [차세대] 발행전문 조회 | `/hub-service/nextgen-issuance-inquiry` | 1 | [d77e8bd82](https://github.com/thebusinesson/smartwork/commit/d77e8bd828a41babb573a1f153c588026b34a3ca) feat: 차세대 발행전문 조회와 구연동 복구 검색 검증 RHF+Zod 적용, 오류 인라인 표시 |

#### SW 설정

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M211 | 권한 관리 | `/settings/permissions` | 3 | [79eb408b7](https://github.com/thebusinesson/smartwork/commit/79eb408b7a40768f9e643779cab4c9fee9da99a7) feat: 목록 체크박스 일괄처리 권한 게이팅 + 연동오류 로그 행 클릭 이동 |
| M212 | 계정 관리 | `/settings/account-management` | 4 | [e8da746f6](https://github.com/thebusinesson/smartwork/commit/e8da746f603341b11ee3c53ef0b41e82bd4d0295) feat: 메뉴 권한 기반 액션 버튼 게이팅 및 등록/수정 라우트 진입 차단 (#513) |
| M213 | 조직 관리 | `/settings/organization-management` | 1 | [fd36e4006](https://github.com/thebusinesson/smartwork/commit/fd36e4006f0914229f2b10311b87f2a69dc7f1d0) fix: 조회 권한 계정에 노출되던 액션 UI 게이팅 보완 (#NNN) |
| M214 | 로그 관리 | `/settings/log-management` | 1 | [ec8dba713](https://github.com/thebusinesson/smartwork/commit/ec8dba7132bfe9bbfbc98c6b21880a6ce3033d56) refactor: 공용 컴포넌트·검색 필드 검증을 전역 스키마로 전환 |
| M215 | 공지 관리 | `/settings/notice-management` | 1 | [f616e99af](https://github.com/thebusinesson/smartwork/commit/f616e99afb97c0e3b633179a10356bc03caa3cd8) refactor: 설정 영역 공지 관리 검증 RHF Zod 전환 |

### C. 작업 근거 미확인 (6개)

#### SB 서비스관리 > 홈택스 DTI 수집

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M087 | Wetax 납부대상 관리 | `/hometax-dti/wetax-payment-targets` | 2 | — 근거 미확인 |

#### SB 운영관리 > 시스템 관리

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M105 | 시스템 SMS 모니터링 로그 | `/system-management/sms-monitoring-log` | 1 | — 근거 미확인 |
| M106 | 발행 관리 | `/system-management/issue-management` | 1 | — 근거 미확인 |

#### 연동 서비스 관리 > 연동 서비스 관리

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M182 | [차세대] 복구솔루션 | `/hub-service/new-integration-recovery` | 2 | — 근거 미확인 |
| M184 | 대량연동 관리 | `/hub-service/bulk-integration-management` | 1 | — 근거 미확인 |

#### SW 설정

| ID | 메뉴명 | 메뉴 URL | 등록 경로 수 | 대표 작업 근거 |
|---|---|---|---:|---|
| M216 | 로그인 관리 | `/settings/login-management` | 1 | — 근거 미확인 |

## 메뉴 외 공통 화면

| 화면 | URL | 작업 이력 |
|---|---|---|
| 로그인 | `/` | [57cb92a33](https://github.com/thebusinesson/smartwork/commit/57cb92a33d91ebbfae182aeb094a5d65ce94f966) 검증·공통 개선 |
| 비밀번호 변경 | `/change-password` | [368d06386](https://github.com/thebusinesson/smartwork/commit/368d063865dd7dc35d558320c8bc709c2c5b03d7) 검증·공통 개선 |
| 최초 계정 설정 | `/initial-account-setup` | [4aed0b8c7](https://github.com/thebusinesson/smartwork/commit/4aed0b8c797e47f83ab5da28e481b70d961dd4fb) 검증·공통 개선 |
| 비밀번호 찾기 | `/forgot-password` | [368d06386](https://github.com/thebusinesson/smartwork/commit/368d063865dd7dc35d558320c8bc709c2c5b03d7) 검증·공통 개선 |
| 대시보드 | `/dashboard` | — 직접 수정 이력 미확인 |
| 조직도 | `/organization-chart` | [a38ad7ce5](https://github.com/thebusinesson/smartwork/commit/a38ad7ce53f956ee291bdc13bd714fcbf53448a6) 검증·공통 개선 |
| 404 안내 | `/*` | — 직접 수정 이력 미확인 |
| 내 계정 기본 경로 | `/my-account` | — 직접 수정 이력 미확인 |
| 내 프로필 | `/my-account/profile` | [368d06386](https://github.com/thebusinesson/smartwork/commit/368d063865dd7dc35d558320c8bc709c2c5b03d7) 검증·공통 개선 |
| 내 계정 설정 | `/my-account/settings` | [b569fb20f](https://github.com/thebusinesson/smartwork/commit/b569fb20f727bdeb066a5f75eca129b8746847cf) 검증·공통 개선 |

## 매뉴얼 작성 때 함께 확인할 화면

- **(단독) 거래명세서**: `menuConfig.ts`의 제목 보정에 `/tax-invoice/tax-invoice/:id?document=transaction-statement`가 있다. 쿼리값에 따른 화면 분기는 별도의 메뉴/URL 패턴 수로 중복 집계하지 않았다.
- 팝업·탭·다운로드 사유 입력·파일 업로드 등은 상위 메뉴 매뉴얼 안에서 다룬다. 이번 목록은 경로 중심이므로 각 화면의 모든 팝업과 탭을 별도 문서 단위로 펼치지는 않았다.
- 모바일앱 관련 4개 기능(앱푸시 발송 관리, 모바일 이미지 배너 관리, 모바일 이미지 배너 일자별 통계, 모바일 컨텐츠 배너 관리)은 작업 이력이 있으나 현재 라우트 등록이 제거되어 있다. `unregistered-pages.md`에 별도 기록했다.
- `대량연동 관리`는 현재 `ComingSoonPage` 연결이다. 일반 사용 매뉴얼 작성 대상으로 확정하지 않는다.

## 조사 근거

- [메뉴 구성](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/menuConfig.ts)
- [최상위 경로](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/index.tsx)
- [기능별 경로](https://github.com/thebusinesson/smartwork/tree/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains)
- Git 전체 작성자 목록, 작성자별 커밋, 화면 및 기능 전용 파일의 변경·이름 변경 이력. 백엔드 API 개발 커밋도 주요 구현 사례와 대조했다.

## 확인 범위의 한계

실제 로그인·브라우저 화면·개발 DB·API 실행은 확인하지 않았다. 이 문서는 현재 코드와 Git 이력으로 만든 매뉴얼 목차 후보이며 실제 화면 동작과 배포 여부의 검증 결과는 아니다.

# [광고 효과와 통계] 키워드 배너광고 상세 통계 다운로드 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

키워드 배너광고 상세 통계 다운로드에서 **키워드 배너 광고 통계 — 키워드별 CSV 다운로드** 결과를 확인한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 광고 효과와 통계 |
| 언제 사용하는가 | 키워드 배너 광고 통계 — 키워드별 상세, 키워드 배너 광고 통계 — 키워드별 CSV 다운로드 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 일자, 키워드명, 배너 위치, 노출, 클릭, 조회기간 |
| 업무 흐름 | 키워드 배너 광고 통계 — 키워드별 상세, 키워드 배너 광고 통계 — 키워드별 CSV 다운로드 |
| 이 페이지의 역할 | 상세 · 키워드 배너 광고 통계 — 키워드별 CSV 다운로드 |
| 판단 결과·다음 업무 | [키워드 배너 광고 통계](keyword-daily-statistics.md) |
| 다른 화면과의 구분 | 광고/마케팅 운영 관리 > 배너 통계정보 > 키워드 배너 광고 통계에서 사용하는 상세 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 키워드 배너광고 상세 통계 다운로드에서 **키워드 배너 광고 통계 — 키워드별 CSV 다운로드** 결과를 확인한다. |
| 메뉴·화면 경로 | 광고/마케팅 운영 관리 > 배너 통계정보 > 키워드 배너 광고 통계 · `/banner/keyword-daily-statistics/:id` · 경로 변수 `id` |
| 화면 유형·담당 | 상세 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [키워드 배너 광고 통계](keyword-daily-statistics.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/banner/keyword-daily-statistics` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `id` |
| 키워드 배너 광고 통계 — 키워드별 상세 | `/banner/keyword-daily-statistics` `VIEW` | `startDate: String` · `endDate: String` · `companyName: String` · `keywordName: String?` · `bannerPosition: String?` · `page: Int` · `size: Int` |
| 키워드 배너 광고 통계 — 키워드별 CSV 다운로드 | `/banner/keyword-daily-statistics` `EXCEL_DOWNLOAD` | `startDate: String` · `endDate: String` · `companyName: String` · `keywordName: String?` · `bannerPosition: String?` |

코드에서 확인한 버튼·작업명은 **검색**, **취소**, **다운로드**, **키워드 배너광고 상세 통계 다운로드**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [키워드 배너 광고 통계](keyword-daily-statistics.md)에서 대상 또는 작업을 선택한다. `/banner/keyword-daily-statistics/:id`에서 이전 화면이 전달한 `id`와 현재 대상을 확인한다.
2. **조회기간**, **캠페인명** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색**, **다운로드**, **키워드 배너광고 상세 통계 다운로드** 중 해당 버튼을 선택한다.
3. **키워드 배너 광고 통계 — 키워드별 CSV 다운로드** 처리 결과를 확인하고 받은 파일의 대상과 적용 조건을 대조한다.
4. 후속 조회나 목록 복귀가 필요하면 [키워드 배너 광고 통계](keyword-daily-statistics.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `id` |
| 일자 | 출력 | 조회 응답 기준 | 화면 필드 `date` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/KeywordBannerDailyStatisticsDetailPage.tsx#L311) |
| 키워드명 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | API 요청 `keywordName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/KeywordBannerDailyStatisticsDetailPage.tsx#L314) |
| 배너 위치 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | API 요청 `bannerPosition` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/KeywordBannerDailyStatisticsDetailPage.tsx#L325) |
| 노출 | 출력 | 조회 응답 기준 | 화면 필드 `impressions` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/KeywordBannerDailyStatisticsDetailPage.tsx#L334) |
| 클릭 | 출력 | 조회 응답 기준 | 화면 필드 `clicks` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/KeywordBannerDailyStatisticsDetailPage.tsx#L335) |
| 조회기간 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/KeywordBannerDailyStatisticsDetailPage.tsx#L40) |
| 캠페인명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/KeywordBannerDailyStatisticsDetailPage.tsx#L55) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 키워드 배너 광고 통계 — 키워드별 상세 | `GET /api/v1/banner/keyword-daily-statistics/detail` · `/banner/keyword-daily-statistics` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/marketing/banner/keyworddailystatistics/KeywordBannerStatController.kt#L96) | `startDate: String` · `endDate: String` · `companyName: String` · `keywordName: String?` · `bannerPosition: String?` · `page: Int` · `size: Int` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `currentPage`, `size` | `SmartBill3.dbo.upAdm_Select_KeywordBanner_Stats_Detail_XLSDOWN` |
| 키워드 배너 광고 통계 — 키워드별 CSV 다운로드 | `GET /api/v1/banner/keyword-daily-statistics/detail/download` · `/banner/keyword-daily-statistics` `EXCEL_DOWNLOAD` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/marketing/banner/keyworddailystatistics/KeywordBannerStatController.kt#L112) | `startDate: String` · `endDate: String` · `companyName: String` · `keywordName: String?` · `bannerPosition: String?` → 파일 또는 오류 응답 | `SmartBill3.dbo.upAdm_Select_KeywordBanner_Stats_Detail_XLSDOWN` |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `SmartBill3.dbo.upAdm_Select_KeywordBanner_Stats_Detail_XLSDOWN` | @FROM_DATE varchar(10), @TO_DATE varchar(10), @COMNAME varchar(100), @BnrLocation varchar(20), @AD_KEYWORD varchar(50) | 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/marketing/banner/keyworddailystatistics/repository/KeywordBannerStatMapper.kt#L63) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-eb08bc46efc9fba4) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 일자, 키워드명, 배너 위치, 노출, 클릭, 조회기간 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 광고/마케팅 운영 관리 > 배너 통계정보 > 키워드 배너 광고 통계의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 배너광고명을 선택해주세요. | 일자, 키워드명, 배너 위치, 노출, 클릭, 조회기간 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 데이터를 불러오는 중 오류가 발생했습니다. | 일자, 키워드명, 배너 위치, 노출, 클릭, 조회기간 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 검색 후 다시 시도해 주세요. | 일자, 키워드명, 배너 위치, 노출, 클릭, 조회기간 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 다운로드할 데이터가 없습니다. | 일자, 키워드명, 배너 위치, 노출, 클릭, 조회기간 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/BannerRoutes.tsx#L28) · [KeywordBannerDailyStatisticsDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/KeywordBannerDailyStatisticsDetailPage.tsx#L89) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/api/keywordBannerDailyStatisticsApi.ts#L84) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/api/keywordBannerDailyStatisticsApi.ts#L97) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 1개 중 개발 메타데이터 확인 1개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-8809bd0e11cd91b4) | Demo 메타데이터 1/1개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

# [배너·키워드의 등록과 노출] 신규 검색페이지별 검색어로그 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

신규 검색페이지별 검색어로그에서 **검색어로그 목록** 결과를 확인한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 배너·키워드의 등록과 노출 |
| 언제 사용하는가 | 검색어로그 목록, 검색어로그 CSV 다운로드 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 검색 일자, 검색어, 조회기간 |
| 업무 흐름 | 검색어로그 목록, 검색어로그 CSV 다운로드 |
| 이 페이지의 역할 | 조회 · 검색어로그 목록 |
| 판단 결과·다음 업무 | 현재 화면에서 결과를 확인한다. |
| 다른 화면과의 구분 | 같은 경로에서 열리는 조회·팝업은 이 문서에서 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 신규 검색페이지별 검색어로그에서 **검색어로그 목록** 결과를 확인한다. |
| 메뉴·화면 경로 | 광고/마케팅 운영 관리 > 광고배너 관리 > 신규 검색페이지별 검색어로그 · `/banner/search-term-log` |
| 화면 유형·담당 | 조회 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | 현재 화면에서 결과를 확인한다. |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/banner/search-term-log` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 검색어로그 목록 | `/banner/search-term-log` `VIEW` | `startDate: String` · `endDate: String` · `page: Int` · `size: Int` |
| 검색어로그 CSV 다운로드 | `/banner/search-term-log` `EXCEL_DOWNLOAD` | `startDate: String` · `endDate: String` |

코드에서 확인한 버튼·작업명은 **검색**, **다운로드**, **검색페이지별 검색어로그 다운로드**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **광고/마케팅 운영 관리 > 광고배너 관리 > 신규 검색페이지별 검색어로그**를 연다. `/banner/search-term-log`를 연다.
2. **검색어**, **조회기간** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색**, **다운로드**, **검색페이지별 검색어로그 다운로드** 중 해당 버튼을 선택한다.
3. **검색어로그 목록** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 검색 일자 | 출력 | 조회 응답 기준 | 화면 필드 `searchDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/SearchTermLogPage.tsx#L204) |
| 검색어 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `searchTerm` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/SearchTermLogPage.tsx#L212) |
| 조회기간 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/SearchTermLogPage.tsx#L32) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 검색어로그 목록 | `GET /api/v1/banner/search-term-log` · `/banner/search-term-log` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/marketing/banner/searchtermlog/SearchTermLogController.kt#L49) | `startDate: String` · `endDate: String` · `page: Int` · `size: Int` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `currentPage`, `size` | `SmartBill3.dbo.upAdm_Select_KEYWORDAD_TXT_LOG` · 코드 연계 트랜잭션 |
| 검색어로그 CSV 다운로드 | `GET /api/v1/banner/search-term-log/download` · `/banner/search-term-log` `EXCEL_DOWNLOAD` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/marketing/banner/searchtermlog/SearchTermLogController.kt#L65) | `startDate: String` · `endDate: String` → 파일 또는 오류 응답 | `SmartBill3.dbo.upAdm_Select_KEYWORDAD_TXT_LOG_List_XLSDOWN` |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `SmartBill3.dbo.upAdm_Select_KEYWORDAD_TXT_LOG` | @PAGE int, @TOP int, @FromDate varchar(10), @ToDate varchar(10) | 정의 참조 `SmartBill3.dbo.MYSEARCH_KEYWORD_LOG` · 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/marketing/banner/searchtermlog/repository/SearchTermLogMapper.kt#L34) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3e1854b446d30691) |
| `SmartBill3.dbo.upAdm_Select_KEYWORDAD_TXT_LOG_List_XLSDOWN` | @FromDate varchar(10), @ToDate varchar(10) | 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/marketing/banner/searchtermlog/repository/SearchTermLogMapper.kt#L44) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b34833efdfc63910) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 검색 일자, 검색어, 조회기간 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 광고/마케팅 운영 관리 > 광고배너 관리 > 신규 검색페이지별 검색어로그의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 데이터를 불러오는데 실패했습니다. | 검색 일자, 검색어, 조회기간 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 검색 후 다시 시도해 주세요. | 검색 일자, 검색어, 조회기간 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 다운로드할 데이터가 없습니다. | 검색 일자, 검색어, 조회기간 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 다운로드 중 오류가 발생했습니다. | 검색 일자, 검색어, 조회기간 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/BannerRoutes.tsx#L23) · [SearchTermLogPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/SearchTermLogPage.tsx#L44) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/api/bannerSearchTermLogApi.ts#L29) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/api/bannerSearchTermLogApi.ts#L46) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 2개 중 개발 메타데이터 확인 2개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-83f885b2d9ae12fe) | Demo 메타데이터 2/2개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

# [배너·키워드의 등록과 노출] 키워드 배너등록 상세 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

키워드 배너등록 상세에서 **키워드 배너 단건 상세** 결과를 확인한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 배너·키워드의 등록과 노출 |
| 언제 사용하는가 | 키워드 배너 단건 상세, 키워드 배너 등록 이미지 보기, 키워드 배너 중복 안내, 키워드 배너 수정 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 캠페인명, 배너 사용기간, 배너 위치, 모든 영역, 세금계산서 조회, 세금계산서 작성 |
| 업무 흐름 | 키워드 배너 단건 상세, 키워드 배너 등록 이미지 보기, 키워드 배너 중복 안내, 키워드 배너 수정 |
| 이 페이지의 역할 | 상세 · 키워드 배너 단건 상세 |
| 판단 결과·다음 업무 | [키워드 배너등록](keyword.md) |
| 다른 화면과의 구분 | 광고/마케팅 운영 관리 > 광고배너 관리 > 키워드 배너등록에서 사용하는 상세 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 확인 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/KeywordBannerDetailPage.tsx#L315) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 키워드 배너등록 상세에서 **키워드 배너 단건 상세** 결과를 확인한다. |
| 메뉴·화면 경로 | 광고/마케팅 운영 관리 > 광고배너 관리 > 키워드 배너등록 · `/banner/keyword/:id` · 경로 변수 `id` |
| 화면 유형·담당 | 상세 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [키워드 배너등록](keyword.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/banner/keyword` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `id` |
| 키워드 배너 단건 상세 | `/banner/keyword` `VIEW` | `excelFileIdx: Long` |
| 키워드 배너 등록 이미지 보기 | `/banner/keyword` `VIEW` | `excelFileIdx: Long` |
| 키워드 배너 중복 안내 | `/banner/keyword` `PROCESS` | `KeywordBannerSaveRequest` `companyName`, `bannerTitle`, `bannerContent`, `bannerPosition`, `bannerLink`, `startDate`, `endDate`, `startTime`, `endTime`, `viewYn`, `bnrTarget` · `keywordFile: MultipartFile?` · `excludeExcelFileIdx: Long` · 서버 필수 `companyName`, `bannerPosition` |
| 키워드 배너 수정 | `/banner/keyword` `PROCESS` | `excelFileIdx: Long` · `KeywordBannerSaveRequest` `companyName`, `bannerTitle`, `bannerContent`, `bannerPosition`, `bannerLink`, `startDate`, `endDate`, `startTime`, `endTime`, `viewYn`, `bnrTarget` · `imageFile: MultipartFile?` · `keywordFile: MultipartFile?` · 서버 필수 `companyName`, `bannerPosition` |

코드에서 확인한 버튼·작업명은 **찾아보기**, **등록 이미지 보기**, **등록 이미지 조회**, **등록 이미지**, **취소**, **수정**, **확인**, **계속 등록**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [키워드 배너등록](keyword.md)에서 대상 또는 작업을 선택한다. `/banner/keyword/:id`에서 이전 화면이 전달한 `id`와 현재 대상을 확인한다.
2. **캠페인명**, **배너 사용기간**, **배너 위치**, **모든 영역**, **세금계산서 조회**, **세금계산서 작성**, **거래처 선택** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **등록 이미지 보기**, **등록 이미지 조회**, **등록 이미지**, **확인**, **계속 등록** 중 해당 버튼을 선택한다.
3. **키워드 배너 단건 상세** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [키워드 배너등록](keyword.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `id` |
| 캠페인명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/KeywordBannerDetailPage.tsx#L114) |
| 배너 사용기간 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/KeywordBannerDetailPage.tsx#L127) |
| 배너 위치 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/KeywordBannerDetailPage.tsx#L144) |
| 모든 영역 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `KEYWORD_BANNER_ALL` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/utils/bannerConstants.ts#L29) |
| 세금계산서 조회 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `KEYWORD_BANNER_PREV` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/utils/bannerConstants.ts#L30) |
| 세금계산서 작성 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `KEYWORD_BANNER_MAKE` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/utils/bannerConstants.ts#L31) |
| 거래처 선택 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `KEYWORD_BN_CLIENT` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/utils/bannerConstants.ts#L32) |
| 발행안내 팝업 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `KEYWORD_BN_BFPOP` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/utils/bannerConstants.ts#L33) |
| 처리결과 팝업 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `KEYWORD_BN_ISSPOP` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/utils/bannerConstants.ts#L34) |
| 마이페이지 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `KEYWORD_BN_MYPAGE` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/utils/bannerConstants.ts#L35) |
| 신규검색페이지 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `KEYWORD_BN_SEARCH` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/utils/bannerConstants.ts#L36) |
| 이미지 업로드 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/KeywordBannerDetailPage.tsx#L158) |
| 배너 이동경로 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/KeywordBannerDetailPage.tsx#L189) |
| 키워드배너 제목 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/KeywordBannerDetailPage.tsx#L203) |
| 키워드배너 내용 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/KeywordBannerDetailPage.tsx#L217) |
| 키워드 목록 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/KeywordBannerDetailPage.tsx#L232) |
| 사용 여부 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/KeywordBannerDetailPage.tsx#L262) |
| 미사용 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/KeywordBannerDetailPage.tsx#L266) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 키워드 배너 단건 상세 | `GET /api/v1/keyword-banners/{excelFileIdx}` · `/banner/keyword` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/marketing/banner/keyword/KeywordBannerController.kt#L131) | `excelFileIdx: Long` → `success`, `data`, `error`, `id`, `companyName`, `bannerTitle`, `bannerContent`, `bannerPosition`, `startDate`, `endDate`, `startTime`, `endTime` | `SmartBill3.dbo.upAdm_Select_KeywordBanner_Detail`, `smartwork.dbo.banner_attachment_meta`, `smartwork.dbo.usp_keyword_banner_meta_select` |
| 키워드 배너 등록 이미지 보기 | `GET /api/v1/keyword-banners/{excelFileIdx}/image` · `/banner/keyword` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/marketing/banner/keyword/KeywordBannerController.kt#L87) | `excelFileIdx: Long` → 파일 또는 오류 응답 | `SmartBill3.dbo.upAdm_Select_KeywordBanner_Detail`, `smartwork.dbo.banner_attachment_meta`, `smartwork.dbo.usp_keyword_banner_meta_select` |
| 키워드 배너 중복 안내 | `POST /api/v1/keyword-banners/overlaps` · `/banner/keyword` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/marketing/banner/keyword/KeywordBannerController.kt#L76) | `KeywordBannerSaveRequest` `companyName`, `bannerTitle`, `bannerContent`, `bannerPosition`, `bannerLink`, `startDate`, `endDate`, `startTime`, `endTime`, `viewYn`, `bnrTarget` · `keywordFile: MultipartFile?` · `excludeExcelFileIdx: Long` · 서버 필수 `companyName`, `bannerPosition` → `success`, `data`, `error`, `id`, `companyName`, `bannerTitle`, `bannerPosition`, `startDate`, `endDate`, `matchedKeywords` | `SmartBill3.dbo.MAIL_BANNER`, `SmartBill3.dbo.AD_KEYWORD_INFO`, `SmartBill3.dbo.upAdm_Select_KeywordBanner_Detail`, `smartwork.dbo.banner_attachment_meta`, `smartwork.dbo.usp_keyword_banner_meta_select` |
| 키워드 배너 수정 | `PUT /api/v1/keyword-banners/{excelFileIdx}` · `/banner/keyword` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/marketing/banner/keyword/KeywordBannerController.kt#L169) | `excelFileIdx: Long` · `KeywordBannerSaveRequest` `companyName`, `bannerTitle`, `bannerContent`, `bannerPosition`, `bannerLink`, `startDate`, `endDate`, `startTime`, `endTime`, `viewYn`, `bnrTarget` · `imageFile: MultipartFile?` · `keywordFile: MultipartFile?` · 서버 필수 `companyName`, `bannerPosition` → `success`, `data`, `error` | `SmartBill3.dbo.upAdm_Select_KeywordBanner_Detail`, `smartwork.dbo.banner_attachment_meta`, `smartwork.dbo.usp_keyword_banner_meta_select`, `smartwork.dbo.usp_keyword_banner_next_excel_idx`, `SmartBill3.dbo.upAdm_Save_KeywordBannerInfo` 외 1개 · 정의에서 확인한 쓰기 `SmartBill3.dbo.MAIL_BANNER`, `SmartBill3.dbo.AD_KEYWORD_INFO` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `SmartBill3.dbo.upAdm_Select_KeywordBanner_Detail` | @FILE_IDX int | 정의 참조 `SmartBill3.dbo.AD_KEYWORD_INFO`, `SmartBill3.dbo.MAIL_BANNER` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/marketing/banner/keyword/repository/KeywordBannerMapper.kt#L106) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-a93d5c95fcf95359) |
| `smartwork.dbo.banner_attachment_meta` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/marketing/banner/repository/BannerAttachmentMetaMapper.kt#L59) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-9aa6a116404463ee) |
| `smartwork.dbo.usp_keyword_banner_meta_select` | @EXCEL_FILE_IDX int | 정의 참조 `SmartBill3.dbo.AD_KEYWORD_INFO`, `SmartBill3.dbo.MAIL_BANNER` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/marketing/banner/keyword/repository/KeywordBannerMapper.kt#L130) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-17270d138ce13819) |
| `SmartBill3.dbo.MAIL_BANNER` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/marketing/banner/keyword/repository/KeywordBannerMapper.kt#L53) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-0128c875a75053cc) |
| `SmartBill3.dbo.AD_KEYWORD_INFO` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL JOIN | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/marketing/banner/keyword/repository/KeywordBannerMapper.kt#L53) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-426852db413b2dfd) |
| `smartwork.dbo.usp_keyword_banner_next_excel_idx` | 컬럼·결과 계약은 매퍼 참조 | 정의 참조 `SmartBill3.dbo.AD_KEYWORD_INFO` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/marketing/banner/keyword/repository/KeywordBannerMapper.kt#L116) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b6cf5cb6c34aa94f) |
| `SmartBill3.dbo.upAdm_Save_KeywordBannerInfo` | @MODE varchar(5), @FILE_IDX int, @BNR_COMNAME varchar(40), @BNR_START_DATE varchar(30), @BNR_END_DATE varchar(30), @BNR_IMAGE varchar(300), @BNR_URL varchar(300), @BNR_LOCATION varchar(20), @ADMIN_ID varchar(100), @AD_KEYWORD varchar(50), @AD_TITLE varchar(50), @AD_CONTENT varchar(110), @EXCEL_FILE_NAME varchar(100), @FILE_UPLOAD_YN varchar(1), @NEW_FILE_IDX int | 정의 참조 `SmartBill3.dbo.AD_KEYWORD_INFO`, `SmartBill3.dbo.ADMIN_INFO`, `SmartBill3.dbo.MAIL_BANNER` · 정적 쓰기 `SmartBill3.dbo.MAIL_BANNER`, `SmartBill3.dbo.AD_KEYWORD_INFO` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/marketing/banner/keyword/repository/KeywordBannerMapper.kt#L145) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-e0847e52bc4e2a0e) |
| `smartwork.dbo.usp_keyword_banner_meta_update` | @EXCEL_FILE_IDX int, @VIEW_YN varchar(1), @BNR_TARGET varchar(10) | 정의 참조 `SmartBill3.dbo.AD_KEYWORD_INFO`, `SmartBill3.dbo.MAIL_BANNER` · 쓰기 구문 존재 · 대상 별칭 또는 하위 정의 확인 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/marketing/banner/keyword/repository/KeywordBannerMapper.kt#L153) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-9040c267c9e4bddc) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 캠페인명, 배너 사용기간, 배너 위치, 모든 영역, 세금계산서 조회, 세금계산서 작성 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 광고/마케팅 운영 관리 > 광고배너 관리 > 키워드 배너등록의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/BannerRoutes.tsx#L22) · [KeywordBannerDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/KeywordBannerDetailPage.tsx#L33) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/api/keywordBannerApi.ts#L175) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/api/keywordBannerApi.ts#L140) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/api/keywordBannerApi.ts#L136) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/api/keywordBannerApi.ts#L193) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 8개 중 개발 메타데이터 확인 8개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-5d68863ca7b25a86) | Demo 메타데이터 8/8개 확인 · Dev와 계약 차이 1개 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

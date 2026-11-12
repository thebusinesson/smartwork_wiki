# [배너·키워드의 등록과 노출] 광고배너 등록 및 조회 상세 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

광고배너 등록 및 조회 상세에서 **배너 단건 상세** 결과를 확인한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 배너·키워드의 등록과 노출 |
| 언제 사용하는가 | 배너 단건 상세, 비회원 미리보기 메인 배너 목록, 배너 수정 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 캠페인명, 배너 사용기간, 전체, 배너 그룹, 배너 위치, 배너 사이즈 |
| 업무 흐름 | 배너 단건 상세, 비회원 미리보기 메인 배너 목록, 배너 수정 |
| 이 페이지의 역할 | 상세 · 배너 단건 상세 |
| 판단 결과·다음 업무 | [광고배너 등록 및 조회](management.md) |
| 다른 화면과의 구분 | 광고/마케팅 운영 관리 > 광고배너 관리 > 광고배너 등록 및 조회에서 사용하는 상세 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 저장 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/components/PreviewMainSelectionDialog.tsx#L146) |
| 확인 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/BannerDetailPage.tsx#L192) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 광고배너 등록 및 조회 상세에서 **배너 단건 상세** 결과를 확인한다. |
| 메뉴·화면 경로 | 광고/마케팅 운영 관리 > 광고배너 관리 > 광고배너 등록 및 조회 · `/banner/management/:id` · 경로 변수 `id` |
| 화면 유형·담당 | 상세 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [광고배너 등록 및 조회](management.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/banner/management` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `id` |
| 배너 단건 상세 | `/banner/management` `VIEW` | `id: Long` · `gubun: String` |
| 비회원 미리보기 메인 배너 목록 | `/banner/management` `VIEW` | 추가 입력은 Controller 서명 참조 |
| 배너 수정 | `/banner/management` `PROCESS` | `id: Long` · `gubun: String` · `BannerSaveRequest` `bannerGroup`, `bannerName`, `bannerPosition`, `linkUrl`, `startDate`, `endDate`, `startTime`, `endTime`, `sizeW`, `sizeH`, `nMemIdx`, `retargetScript`, `viewYn`, `svcGubun` · `file: MultipartFile?` · `mobileFile: MultipartFile?` · 서버 필수 `bannerGroup`, `bannerName` |

코드에서 확인한 버튼·작업명은 **메일배너 위치 확인**, **파일 제거**, **찾아보기**, **등록 이미지 보기**, **버튼1**, **버튼2**, **선택 제거**, **저장**, **등록 이미지 조회**, **등록 이미지**, **취소**, **배너 수정 취소**, **수정**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [광고배너 등록 및 조회](management.md)에서 대상 또는 작업을 선택한다. `/banner/management/:id`에서 이전 화면이 전달한 `id`와 현재 대상을 확인한다.
2. **캠페인명**, **배너 사용기간**, **전체**, **배너 그룹**, **배너 위치**, **배너 사이즈**, **이미지 업로드 [웹]** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **메일배너 위치 확인**, **등록 이미지 보기**, **저장**, **등록 이미지 조회**, **등록 이미지** 중 해당 버튼을 선택한다.
3. **배너 단건 상세** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [광고배너 등록 및 조회](management.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `id` |
| 캠페인명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/components/BasicInfoSection.tsx#L18) |
| 캠페인명을 입력하세요 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/components/BasicInfoSection.tsx#L21) |
| 배너 사용기간 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/components/BasicInfoSection.tsx#L27) |
| 전체 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `all` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/components/BannerSettingsSection.tsx#L27) |
| 배너 그룹 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/components/BannerSettingsSection.tsx#L62) |
| 배너 그룹을 선택하세요 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/components/BannerSettingsSection.tsx#L65) |
| 배너 위치 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/components/BannerSettingsSection.tsx#L72) |
| 배너 위치를 선택하세요 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/components/BannerSettingsSection.tsx#L85) |
| 섹션 선택 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/components/BannerSettingsSection.tsx#L123) |
| 배너위치 선택 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/components/BannerSettingsSection.tsx#L178) |
| 배너 사이즈 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/components/BannerSettingsSection.tsx#L200) |
| 선택된 파일 없음 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/components/BannerImageUploadRow.tsx#L51) |
| 이미지 업로드 [웹] | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/components/MainBannerMediaSection.tsx#L85) |
| 이미지 업로드 [모바일] | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/components/MainBannerMediaSection.tsx#L101) |
| 내용1 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/components/MainBannerMediaSection.tsx#L117) |
| 내용2 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/components/MainBannerMediaSection.tsx#L118) |
| 내용3 [강조] | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/components/MainBannerMediaSection.tsx#L119) |
| 버튼 노출 텍스트 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/components/MainBannerMediaSection.tsx#L60) |
| 이미지 업로드 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/components/RecommendServiceSection.tsx#L46) |
| 타이틀 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/components/RecommendServiceSection.tsx#L62) |
| 내용2 [강조] | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/components/RecommendServiceSection.tsx#L76) |
| 배너 이동경로 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/components/RecommendServiceSection.tsx#L85) |
| 비회원 미리보기 메인 선택 | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/components/ImageInfoSection.tsx#L140) |
| 기간 | 출력 | 조회 응답 기준 | 화면 필드 `period` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/components/PreviewMainSelectionDialog.tsx#L121) |
| 이미지명 | 출력 | 조회 응답 기준 | API 응답 `imageName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/components/PreviewMainSelectionDialog.tsx#L129) |
| 사용 여부 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/components/UsageSettingsSection.tsx#L15) |
| 리타겟팅 스크립트 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/components/RetargetingSection.tsx#L14) |
| 리타겟팅 사용 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/components/RetargetingSection.tsx#L22) |
| 리타겟팅 스크립트를 입력하세요 | 입력 | 화면 상태·입력 조건에 따라 표시 | 입력란 안내 문구 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/components/RetargetingSection.tsx#L25) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 배너 단건 상세 | `GET /api/v1/banners/{id}` · `/banner/management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/marketing/banner/BannerController.kt#L130) | `id: Long` · `gubun: String` → `success`, `data`, `error`, `id`, `gubun`, `bannerGroup`, `bannerName`, `bannerPosition`, `imagePath`, `imageOriginalName`, `linkUrl`, `sizeW` | `smartwork.dbo.usp_main_banner_select`, `smartwork.dbo.banner_attachment_meta`, `smartwork.dbo.upAdmSB_View_AdverBanner` |
| 비회원 미리보기 메인 배너 목록 | `GET /api/v1/banners/nmem-previews` · `/banner/management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/marketing/banner/BannerController.kt#L99) | 추가 입력은 Controller 서명 참조 → `success`, `data`, `error`, `id`, `bannerName`, `startDate`, `endDate`, `imageName` | `SmartBill3.dbo.upAdmSB_Lst_nMemMailBanner` |
| 배너 수정 | `PUT /api/v1/banners/{id}` · `/banner/management` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/marketing/banner/BannerController.kt#L165) | `id: Long` · `gubun: String` · `BannerSaveRequest` `bannerGroup`, `bannerName`, `bannerPosition`, `linkUrl`, `startDate`, `endDate`, `startTime`, `endTime`, `sizeW`, `sizeH`, `nMemIdx`, `retargetScript`, `viewYn`, `svcGubun` · `file: MultipartFile?` · `mobileFile: MultipartFile?` · 서버 필수 `bannerGroup`, `bannerName` → `success`, `data`, `error` | `smartwork.dbo.usp_adver_banner_save`, `smartwork.dbo.usp_main_banner_select`, `smartwork.dbo.banner_attachment_meta`, `smartwork.dbo.upAdmSB_View_AdverBanner`, `SB_COMMON.dbo.BANNER_AD_INFO` 외 3개 · 정의에서 확인한 쓰기 `SB_COMMON.dbo.BANNER_AD_INFO`, `SmartBill3.dbo.MAIL_BANNER_HISTORY`, `SmartBill3.dbo.MAIL_BANNER`, `smartwork.dbo.main_banner` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.usp_main_banner_select` | @IDX int | 정의 참조 `smartwork.dbo.main_banner` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/marketing/banner/repository/MainBannerMapper.kt#L68) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3cf585b785996588) |
| `smartwork.dbo.banner_attachment_meta` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/marketing/banner/repository/BannerAttachmentMetaMapper.kt#L59) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-9aa6a116404463ee) |
| `smartwork.dbo.upAdmSB_View_AdverBanner` | @bnrIdx int, @gubun varchar(1) | 정의 참조 `SmartBill3.dbo.ADVERTISEMENT_INFO`, `SB_COMMON.dbo.BANNER_AD_INFO`, `SmartBill3.dbo.MAIL_BANNER` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/marketing/banner/repository/AdverBannerMapper.kt#L94) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-1517b497ecd27df9) |
| `SmartBill3.dbo.upAdmSB_Lst_nMemMailBanner` | 컬럼·결과 계약은 매퍼 참조 | 동적 SQL 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/marketing/banner/repository/AdverBannerMapper.kt#L176) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-07dc0a4d1b98b888) |
| `smartwork.dbo.usp_adver_banner_save` | @IDX int, @BANNER_GROUP varchar(20), @ADMIN_ID varchar(100), @BANNER_NAME varchar(40), @BANNER_POSITION varchar(20), @IMG_PATH varchar(300), @IMG_EXTENSION varchar(5), @SIZE_W int, @SIZE_H int, @LINK_URL varchar(300), @START_DATE datetime, @END_DATE datetime, @VIEW_YN char(1), @BNR_TARGET varchar(20), @N_MEM_IDX int = NULL, @RETARGET_SCRIPT varchar(max) = NULL, @SVC_GUBUN varchar(10) = NULL, @SORT_ORDER int = NULL, @MOBILE_IMAGE_PATH nvarchar(300) = NULL, @CONTENT1 nvarchar(max) = NULL, @CONTENT2 nvarchar(max) = NULL, @CONTENT3 nvarchar(max) = NULL, @BUTTON1_TEXT nvarchar(100) = NULL, @BUTTON1_URL nvarchar(300) = NULL, @BUTTON2_YN char(1) = NULL, @BUTTON2_TEXT nvarchar(100) = NULL, @BUTTON2_URL nvarchar(300) = NULL, @RECOMMEND_TITLE nvarchar(200) = NULL, @RECOMMEND_CONTENT1 nvarchar(max) = NULL, @RECOMMEND_CONTENT2 nvarchar(max) = NULL, @SECTION varchar(10) = NULL, @QUADRANT varchar(10) = NULL, @CATEGORY nvarchar(100) = NULL, @TITLE nvarchar(200) = NULL, @GUBUN varchar(3) = NULL, @RESULT_IDX int OUT | 정의 참조 `SmartBill3.dbo.ADMIN_INFO`, `SB_COMMON.dbo.BANNER_AD_INFO`, `SmartBill3.dbo.MAIL_BANNER`, `SmartBill3.dbo.MAIL_BANNER_HISTORY`, `smartwork.dbo.main_banner` · 정적 쓰기 `SB_COMMON.dbo.BANNER_AD_INFO`, `SmartBill3.dbo.MAIL_BANNER_HISTORY`, `SmartBill3.dbo.MAIL_BANNER`, `smartwork.dbo.main_banner` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/marketing/banner/repository/AdverBannerMapper.kt#L212) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-b31e7d79761a7ba5) |
| `SB_COMMON.dbo.BANNER_AD_INFO` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/marketing/banner/repository/AdverBannerMapper.kt#L132) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-e744138452adb0d1) |
| `SmartBill3.dbo.MAIL_BANNER` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/marketing/banner/repository/AdverBannerMapper.kt#L146) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-0128c875a75053cc) |
| `smartwork.dbo.main_banner` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/marketing/banner/repository/AdverBannerMapper.kt#L159) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-7139aaf03e41b1e5) |
| `smartwork.dbo.usp_banner_viewyn_update` | @GUBUN varchar(3), @IDX int, @VIEW_YN varchar(1) | 정의 참조 `SB_COMMON.dbo.BANNER_AD_INFO`, `SmartBill3.dbo.MAIL_BANNER`, `smartwork.dbo.main_banner` · 정적 쓰기 `SB_COMMON.dbo.BANNER_AD_INFO`, `SmartBill3.dbo.MAIL_BANNER`, `smartwork.dbo.main_banner` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/marketing/banner/repository/AdverBannerMapper.kt#L189) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-820276dccbb6fce7) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 캠페인명, 배너 사용기간, 전체, 배너 그룹, 배너 위치, 배너 사이즈 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 광고/마케팅 운영 관리 > 광고배너 관리 > 광고배너 등록 및 조회의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 배너 데이터를 불러오는데 실패했습니다. | 캠페인명, 배너 사용기간, 전체, 배너 그룹, 배너 위치, 배너 사이즈 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |
| 배너 ID가 없습니다. | 캠페인명, 배너 사용기간, 전체, 배너 그룹, 배너 위치, 배너 사이즈 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/BannerRoutes.tsx#L19) · [BannerDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/BannerDetailPage.tsx#L27) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/api/bannerApi.ts#L211) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/api/bannerApi.ts#L257) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/api/bannerApi.ts#L234) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 9개 중 개발 메타데이터 확인 9개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-9d2d60af281c86b9) | Demo 메타데이터 9/9개 확인 · Dev와 계약 차이 2개 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

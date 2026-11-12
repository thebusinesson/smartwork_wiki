# [배너·키워드의 등록과 노출] 광고배너 등록 및 조회 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

광고배너 등록 및 조회에서 **배너 목록 (검색 + 페이징)** 결과를 확인한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 배너·키워드의 등록과 노출 |
| 언제 사용하는가 | 배너 목록 (검색 + 페이징), 배너 사용여부(VIEW_YN) 토글 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 전체, 일자, 캠페인명, 배너 그룹, 등록일, 기간 |
| 업무 흐름 | 배너 목록 (검색 + 페이징), 배너 사용여부(VIEW_YN) 토글 |
| 이 페이지의 역할 | 조회·관리 · 배너 목록 (검색 + 페이징) |
| 판단 결과·다음 업무 | [등록 취소](management__new.md) · [광고배너 등록 및 조회 상세](management__by-id.md) |
| 다른 화면과의 구분 | 이 경로에서 볼 수 있는 조건·결과를 기준으로 사용한다. 독립 경로의 상세·등록은 관련 화면에 연결한다. |

### 화면 구역과 확인창

| 실제 구역명 | 사용하는 상황 | 해당 구역의 데이터 | 판단·후속 업무 |
| --- | --- | --- | --- |
| 확인 | 작업 직전 | 실행 여부와 작업 대상을 확인한다. | [구현](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/BannerManagementPage.tsx#L418) |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 광고배너 등록 및 조회에서 **배너 목록 (검색 + 페이징)** 결과를 확인한다. |
| 메뉴·화면 경로 | 광고/마케팅 운영 관리 > 광고배너 관리 > 광고배너 등록 및 조회 · `/banner/management` |
| 화면 유형·담당 | 조회·관리 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [등록 취소](management__new.md) · [광고배너 등록 및 조회 상세](management__by-id.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/banner/management` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | SmartWork 계정 |
| 배너 목록 (검색 + 페이징) | `/banner/management` `VIEW` | `BannerSearchRequest` `dateType`, `startDate`, `endDate`, `companyName`, `bannerGroup`, `bannerPosition`, `page`, `size` |
| 배너 사용여부(VIEW_YN) 토글 | `/banner/management` `PROCESS` | `id: Long` · `gubun: String` · `BannerViewYnRequest` `viewYn`, `conflictToken` · 서버 필수 `viewYn` |

코드에서 확인한 버튼·작업명은 **복사**, **검색**, **메일배너 위치 확인**, **등록**, **취소**, **기존 배너 Off 후 적용**, **확인**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. **광고/마케팅 운영 관리 > 광고배너 관리 > 광고배너 등록 및 조회**를 연다. `/banner/management`를 연다.
2. **전체**, **일자**, **캠페인명**, **배너 그룹**, **이미지명**, **이미지 연결 링크** 중 필요한 조건과 값을 확인한다. 할 작업에 맞춰 **검색**, **메일배너 위치 확인**, **등록**, **기존 배너 Off 후 적용**, **확인** 중 해당 버튼을 선택한다.
3. **배너 목록 (검색 + 페이징)** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
4. 후속 조회나 목록 복귀가 필요하면 [등록 취소](management__new.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 전체 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `all` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/BannerManagementPage.tsx#L134) |
| 일자 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/BannerManagementPage.tsx#L94) |
| 캠페인명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/BannerManagementPage.tsx#L105) |
| 배너 그룹 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/BannerManagementPage.tsx#L114) |
| 등록일 | 출력 | 조회 응답 기준 | 화면 필드 `registrationDate` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/BannerManagementPage.tsx#L260) |
| 기간 | 출력 | 조회 응답 기준 | 화면 필드 `period` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/BannerManagementPage.tsx#L270) |
| 배너 위치 | 출력 | 조회 응답 기준 | 화면 필드 `exposurePosition` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/BannerManagementPage.tsx#L273) |
| 이미지명 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `imageName` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/BannerManagementPage.tsx#L281) |
| 이미지 연결 링크 | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면 필드 `imageLink` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/BannerManagementPage.tsx#L290) |
| 사용여부 | 출력 | 조회 응답 기준 | 화면 필드 `useYn` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/BannerManagementPage.tsx#L316) |
| 복사 | 출력 | 조회 응답 기준 | 화면 필드 `copy` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/BannerManagementPage.tsx#L342) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 배너 목록 (검색 + 페이징) | `GET /api/v1/banners` · `/banner/management` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/marketing/banner/BannerController.kt#L76) | `BannerSearchRequest` `dateType`, `startDate`, `endDate`, `companyName`, `bannerGroup`, `bannerPosition`, `page`, `size` → `success`, `data`, `error`, `content`, `totalElements`, `totalPages`, `page`, `size` | `smartwork.dbo.usp_main_banner_list_select`, `smartwork.dbo.usp_adver_banner_list_select` · 코드 연계 트랜잭션 |
| 배너 사용여부(VIEW_YN) 토글 | `PATCH /api/v1/banners/{id}/view-yn` · `/banner/management` `PROCESS` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/marketing/banner/BannerController.kt#L191) | `id: Long` · `gubun: String` · `BannerViewYnRequest` `viewYn`, `conflictToken` · 서버 필수 `viewYn` → `success`, `data`, `error` | `SB_COMMON.dbo.BANNER_AD_INFO`, `SmartBill3.dbo.MAIL_BANNER`, `smartwork.dbo.main_banner`, `smartwork.dbo.usp_banner_viewyn_update`, `smartwork.dbo.usp_main_banner_select` 외 2개 · 정의에서 확인한 쓰기 `SB_COMMON.dbo.BANNER_AD_INFO`, `SmartBill3.dbo.MAIL_BANNER`, `smartwork.dbo.main_banner` · 코드 연계 트랜잭션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `smartwork.dbo.usp_main_banner_list_select` | @POSITION varchar(10) = NULL | 정의 참조 `smartwork.dbo.main_banner` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/marketing/banner/repository/MainBannerMapper.kt#L63) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-5d555699c968c06b) |
| `smartwork.dbo.usp_adver_banner_list_select` | @PAGE int, @PAGE_SIZE int, @BANNER_NAME varchar(100), @BNR_GROUP varchar(20), @BNR_LOCATION varchar(20), @DATE_TYPE varchar(10), @FROM_DATE varchar(10), @TO_DATE varchar(10) | 정의 참조 `SmartBill3.dbo.ADVERTISEMENT_INFO`, `SB_COMMON.dbo.BANNER_AD_INFO`, `SmartBill3.dbo.MAIL_BANNER` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/marketing/banner/repository/AdverBannerMapper.kt#L64) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-e9241e6d0878f629) |
| `SB_COMMON.dbo.BANNER_AD_INFO` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/marketing/banner/repository/AdverBannerMapper.kt#L113) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-e744138452adb0d1) |
| `SmartBill3.dbo.MAIL_BANNER` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/marketing/banner/repository/AdverBannerMapper.kt#L113) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-0128c875a75053cc) |
| `smartwork.dbo.main_banner` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/marketing/banner/repository/AdverBannerMapper.kt#L113) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-7139aaf03e41b1e5) |
| `smartwork.dbo.usp_banner_viewyn_update` | @GUBUN varchar(3), @IDX int, @VIEW_YN varchar(1) | 정의 참조 `SB_COMMON.dbo.BANNER_AD_INFO`, `SmartBill3.dbo.MAIL_BANNER`, `smartwork.dbo.main_banner` · 정적 쓰기 `SB_COMMON.dbo.BANNER_AD_INFO`, `SmartBill3.dbo.MAIL_BANNER`, `smartwork.dbo.main_banner` · RETURN 문 포함 | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/marketing/banner/repository/AdverBannerMapper.kt#L189) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-820276dccbb6fce7) |
| `smartwork.dbo.usp_main_banner_select` | @IDX int | 정의 참조 `smartwork.dbo.main_banner` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/marketing/banner/repository/MainBannerMapper.kt#L68) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-3cf585b785996588) |
| `smartwork.dbo.banner_attachment_meta` | 컬럼·결과 계약은 매퍼 참조 | 매퍼 SQL FROM | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/marketing/banner/repository/BannerAttachmentMetaMapper.kt#L59) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-9aa6a116404463ee) |
| `smartwork.dbo.upAdmSB_View_AdverBanner` | @bnrIdx int, @gubun varchar(1) | 정의 참조 `SmartBill3.dbo.ADVERTISEMENT_INFO`, `SB_COMMON.dbo.BANNER_AD_INFO`, `SmartBill3.dbo.MAIL_BANNER` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/marketing/banner/repository/AdverBannerMapper.kt#L94) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-1517b497ecd27df9) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 전체, 일자, 캠페인명, 배너 그룹, 등록일, 기간 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 광고/마케팅 운영 관리 > 광고배너 관리 > 광고배너 등록 및 조회의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 변경 요청의 결과가 불명확함 | 대상 식별자, 요청 시각, 응답과 처리 이력 | 대상 상태를 다시 조회한다. 실제 변경을 확인하기 전 동일 요청을 반복하지 않는다. |
| 데이터를 불러오는데 실패했습니다. | 전체, 일자, 캠페인명, 배너 그룹, 등록일, 기간 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/BannerRoutes.tsx#L17) · [BannerManagementPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/BannerManagementPage.tsx#L68) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/api/bannerApi.ts#L194) · [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/marketing/banner/api/bannerApi.ts#L248) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 9개 중 개발 메타데이터 확인 9개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-492469a0fba8139b) | Demo 메타데이터 9/9개 확인 · Dev와 계약 차이 2개 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

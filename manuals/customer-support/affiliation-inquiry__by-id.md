# [서비스 도입·제휴 문의와 제한] 제휴 문의 상세 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

제휴 문의 상세에서 **제휴 문의 상세** 결과를 확인한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 서비스 도입·제휴 문의와 제한 |
| 언제 사용하는가 | 제휴 문의 상세 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 제휴 문의 상세 |
| 업무 흐름 | 제휴 문의 상세 |
| 이 페이지의 역할 | 상세 · 제휴 문의 상세 |
| 판단 결과·다음 업무 | [제휴 문의](affiliation-inquiry.md) |
| 다른 화면과의 구분 | 고객지원 > 고객 문의 관리 > 제휴 문의에서 사용하는 상세 경로다. 입력·결과는 이 경로에 전달된 대상과 해당 작업을 기준으로 확인한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 제휴 문의 상세에서 **제휴 문의 상세** 결과를 확인한다. |
| 메뉴·화면 경로 | 고객지원 > 고객 문의 관리 > 제휴 문의 · `/customer-support/affiliation-inquiry/:id` · 경로 변수 `id` |
| 화면 유형·담당 | 상세 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [제휴 문의](affiliation-inquiry.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/customer-support/affiliation-inquiry` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `id` |
| 제휴 문의 상세 | `/customer-support/affiliation-inquiry` `VIEW` | `id: Long` |

코드에서 확인한 버튼·작업명은 **목록**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. [제휴 문의](affiliation-inquiry.md)에서 대상 또는 작업을 선택한다. `/customer-support/affiliation-inquiry/:id`에서 이전 화면이 전달한 `id`와 현재 대상을 확인한다.
2. **제휴 문의 상세** 결과에서 대상과 상태를 확인한다. 세부 이력이나 처리 화면으로 이동할 때 같은 식별자를 유지한다.
3. 후속 조회나 목록 복귀가 필요하면 [제휴 문의](affiliation-inquiry.md)에서 후속 절차를 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `id` |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 제휴 문의 상세 | `GET /api/v1/customer-support/affiliation-inquiries/{id}` · `/customer-support/affiliation-inquiry` `VIEW` · [Controller](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/api/support/customersupport/affiliationinquiry/AffiliationInquiryController.kt#L143) | `id: Long` → `success`, `data`, `error`, `id`, `registeredAt`, `affiliationTypeCode`, `affiliationTypeLabel`, `title`, `companyName`, `managerName`, `phone`, `mobile` | `office.dbo.upSW_PARTASK_DETAIL` |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| `office.dbo.upSW_PARTASK_DETAIL` | @IDX int | 정의 참조 `SB_COMMON.dbo.SB_Part_Ask` | [Mapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/customersupport/affiliationinquiry/repository/AffiliationInquiryMapper.kt#L105) · [2026-11-11 개발 SQL Server 메타데이터](../../references/all-pages-database.md#object-4278ab58e77ef457) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 제휴 문의 상세 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |
| 메뉴가 보이지 않거나 작업이 거부됨 | 고객지원 > 고객 문의 관리 > 제휴 문의의 접근 권한과 위 작업별 액션 | 권한 담당에게 메뉴 경로와 필요한 작업을 전달한다. |
| 상세 정보를 불러오는데 실패했습니다. | 제휴 문의 상세 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/CustomerSupportRoutes.tsx#L115) · [AffiliationInquiryDetailPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/customersupport/AffiliationInquiryDetailPage.tsx#L27) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [프런트엔드 요청](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/support/customersupport/api/affiliationInquiryApi.ts#L53) | 코드 확인 · API 표의 Controller 기준 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 직접 경로 객체 1개 중 개발 메타데이터 확인 1개 · 2026-11-11 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-9e2a54ce51b3db0e) | Demo 메타데이터 1/1개 확인 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

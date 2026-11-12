# [시스템 키·벌크계좌·업체 연결 설정] [구연동]연동업체 관리 체크리스트 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

연동업체의 오픈체크 항목을 살펴보는 화면이다. 현재 경로에서 업체와 조건을 표시하며, 체크리스트 조회·다운로드는 구현 준비 상태다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 시스템 키·벌크계좌·업체 연결 설정 |
| 언제 사용하는가 | 화면 표시 및 이동 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 업체명, 영업 상품과 업체조건 |
| 업무 흐름 | 연동업체명과 영업 상품을 이전 화면에서 받아 표시한다. 업체조건을 바꿀 수 있으며, 현재 코드에서는 조회 데이터가 비어 있고 다운로드 버튼은 구현 예정 메시지를 표시한다. |
| 이 페이지의 역할 | 체크리스트 · [구연동]연동업체 관리 체크리스트 |
| 판단 결과·다음 업무 | [[구연동]연동업체 관리](vendor-management.md) |
| 다른 화면과의 구분 | 연동업체명과 영업 상품을 이전 화면에서 받아 표시한다. 업체조건을 바꿀 수 있으며, 현재 코드에서는 조회 데이터가 비어 있고 다운로드 버튼은 구현 예정 메시지를 표시한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 연동업체의 오픈체크 항목을 살펴보는 화면이다. 현재 경로에서 업체와 조건을 표시하며, 체크리스트 조회·다운로드는 구현 준비 상태다. |
| 메뉴·화면 경로 | 연동/허브 업체 관리 > 연동/허브 업체 관리 > [구연동]연동업체 관리 · `/hub-vendor/vendor-management/:id/checklist` · 경로 변수 `id` |
| 화면 유형·담당 | 체크리스트 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | [[구연동]연동업체 관리](vendor-management.md) |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/hub-vendor/vendor-management` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | `id` |

코드에서 확인한 버튼·작업명은 **다운로드**, **목록**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. 연동업체명과 영업 상품을 이전 화면에서 받아 표시한다. 업체조건을 바꿀 수 있으며, 현재 코드에서는 조회 데이터가 비어 있고 다운로드 버튼은 구현 예정 메시지를 표시한다.
2. 조회·다운로드가 준비 중이다. 이 화면의 표시만으로 업체의 실제 체크 완료나 데이터 유무를 판단할 수 없다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 경로 식별자 | 입력·경로 | 이전 화면이 전달한 대상 값 | `id` |
| 연동업체명: | 화면 항목 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/vendorManagement/pages/VendorChecklistPage.tsx#L68) |
| 업체조건: | 입력 또는 선택 | 화면 상태·입력 조건에 따라 표시 | 화면에서 확인하는 항목 · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/vendorManagement/pages/VendorChecklistPage.tsx#L78) |
| 사업자번호 | 출력 | 조회 응답 기준 | 화면 필드 `businessNumber-h` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/hubVendor/components/ChecklistTable.tsx#L44) |
| 업체명 | 출력 | 조회 응답 기준 | 화면 필드 `companyName-h` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/hubVendor/components/ChecklistTable.tsx#L45) |
| 가입일 | 출력 | 조회 응답 기준 | 화면 필드 `joinDate-h` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/hubVendor/components/ChecklistTable.tsx#L46) |
| 자동승인 | 출력 | 조회 응답 기준 | 화면 필드 `autoApproval-group` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/hubVendor/components/ChecklistTable.tsx#L60) |
| SMS 자동발송 | 출력 | 조회 응답 기준 | 화면 필드 `smsAuto-group` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/hubVendor/components/ChecklistTable.tsx#L74) |
| 정매입 | 출력 | 조회 응답 기준 | 화면 필드 `issueCmtYn-h` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/hubVendor/components/ChecklistTable.tsx#L77) |
| 역매입 | 출력 | 조회 응답 기준 | 화면 필드 `rissueCmtYn-h` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/hubVendor/components/ChecklistTable.tsx#L78) |
| 개인매출 | 출력 | 조회 응답 기준 | 화면 필드 `pissueCmtYn-h` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/hubVendor/components/ChecklistTable.tsx#L79) |
| 정매출 | 출력 | 조회 응답 기준 | 화면 필드 `dtiSms-h` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/hubVendor/components/ChecklistTable.tsx#L80) |
| 위수탁 | 출력 | 조회 응답 기준 | 화면 필드 `bdtiSms-h` · [표시·입력 소스](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/hubVendor/components/ChecklistTable.tsx#L82) |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 화면 표시·이동 | 해당 없음 · SmartWork 화면 자체의 업무 API 호출 없음 | 화면 진입 → 연동업체명과 영업 상품을 이전 화면에서 받아 표시한다. 업체조건을 바꿀 수 있으며, 현재 코드에서는 조회 데이터가 비어 있고 다운로드 버튼은 구현 예정 메시지를 표시한다. | 이전 화면이 전달한 업체명·영업 상품 및 현재 화면 상태 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| 해당 없음 | 직접 DB 호출 없음 | 이전 화면이 전달한 업체명·영업 상품 및 현재 화면 상태 | [VendorChecklistPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/vendorManagement/pages/VendorChecklistPage.tsx#L30) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 비거나 기능을 사용할 수 없음 | 이전 화면이 전달한 업체명·영업 상품 및 현재 화면 상태 | 조회·다운로드가 준비 중이다. 이 화면의 표시만으로 업체의 실제 체크 완료나 데이터 유무를 판단할 수 없다. |
| 다운로드 기능은 추후 구현 예정입니다. | 업체명, 영업 상품과 업체조건 | 조건을 확인한다. 계속 발생하면 요청 시각과 마스킹한 식별자를 운영 담당에게 전달한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/IntegrationRoutes.tsx#L106) · [VendorChecklistPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/vendorManagement/pages/VendorChecklistPage.tsx#L30) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [VendorChecklistPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubcollab/vendorManagement/pages/VendorChecklistPage.tsx#L30) | 화면 소스 확인 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 화면 직접 DB 호출 해당 없음 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-82f6884c2367b5b3) | 해당 없음 · 체크리스트 조회·다운로드가 준비 중이며 직접 DB 호출 없음 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

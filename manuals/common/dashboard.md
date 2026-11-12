# [직원 인증·내 계정·세션] 대시보드 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

로그인 직후 업무 메뉴로 이동하는 기본 화면이다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 직원 인증·내 계정·세션 |
| 언제 사용하는가 | 화면 표시 및 이동 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | 사이드바와 로그인 사용자 |
| 업무 흐름 | 로그인 뒤 기본 진입 화면으로 이동한다. 대시보드 화면의 본문은 현재 별도 업무 API를 호출하지 않는다. |
| 이 페이지의 역할 | 대시보드 · 대시보드 |
| 판단 결과·다음 업무 | 현재 화면에서 결과를 확인한다. |
| 다른 화면과의 구분 | 로그인 뒤 기본 진입 화면으로 이동한다. 대시보드 화면의 본문은 현재 별도 업무 API를 호출하지 않는다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 로그인 직후 업무 메뉴로 이동하는 기본 화면이다. |
| 메뉴·화면 경로 | SmartWork 공통 > 대시보드 · `/dashboard` |
| 화면 유형·담당 | 대시보드 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | 현재 화면에서 결과를 확인한다. |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | 로그인이 필요한 공통 화면이다. 루트 라우트에서 메뉴 권한 검사 예외로 구성한다. | 접속 환경과 대상 |

## 3) 화면 사용 절차

1. 로그인 뒤 기본 진입 화면으로 이동한다. 대시보드 화면의 본문은 현재 별도 업무 API를 호출하지 않는다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 화면 상태 | 출력 | 접속 환경에 따라 표시 | 로그인 뒤 기본 진입 화면으로 이동한다. 대시보드 화면의 본문은 현재 별도 업무 API를 호출하지 않는다. |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 화면 표시·이동 | 해당 없음 · SmartWork 화면 자체의 업무 API 호출 없음 | 화면 진입 → 로그인 뒤 기본 진입 화면으로 이동한다. 대시보드 화면의 본문은 현재 별도 업무 API를 호출하지 않는다. | SmartWork 앱 셸 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| 해당 없음 | 직접 DB 호출 없음 | SmartWork 앱 셸 | [DashboardPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/shared/dashboard/DashboardPage.tsx#L3) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 없거나 대상이 다름 | 사이드바와 로그인 사용자 | 현재 경로와 조회 대상, 적용한 조건을 확인하고 다시 조회한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/index.tsx) · [DashboardPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/shared/dashboard/DashboardPage.tsx#L3) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [DashboardPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/shared/dashboard/DashboardPage.tsx#L3) | 화면 소스 확인 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 화면 직접 DB 호출 해당 없음 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-89347bb23a645278) | 해당 없음 · 대시보드 본문의 직접 업무 DB 호출 없음 · 2026-11-11 |
| 화면 재현 | [로컬 Playwright 표본](../../evidence/browser/all-pages-sample-2026-11-11.json) | 로그인 후 화면 진입 확인 · 2026-11-11 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

# [연동 문의·점검·라우팅·복구] [차세대] 복구솔루션 관리자 매뉴얼

## 1) 화면 기본 정보

### 도메인 이해

차세대 복구솔루션의 비교 화면으로 진입한다. 현재 접속 환경에 따라 내장 화면이나 접속 안내를 표시한다.

| 구분 | 설명 |
| --- | --- |
| 업무 영역 | 연동 문의·점검·라우팅·복구 |
| 언제 사용하는가 | 화면 표시 및 이동 업무가 필요할 때 사용한다. |
| 주요 대상·데이터 | Demo 또는 운영 접속 환경 |
| 업무 흐름 | 현재 출처가 Demo 또는 운영 복구솔루션과 같으면 내장 화면을 연다. 다른 환경에서는 안내와 접속 선택지를 표시한다. |
| 이 페이지의 역할 | 연계 진입 · [차세대] 복구솔루션 |
| 판단 결과·다음 업무 | 현재 화면에서 결과를 확인한다. |
| 다른 화면과의 구분 | 현재 출처가 Demo 또는 운영 복구솔루션과 같으면 내장 화면을 연다. 다른 환경에서는 안내와 접속 선택지를 표시한다. |

### 화면 정보

| 항목 | 작성 내용 |
| --- | --- |
| 업무 도메인·목적 | 차세대 복구솔루션의 비교 화면으로 진입한다. 현재 접속 환경에 따라 내장 화면이나 접속 안내를 표시한다. |
| 메뉴·화면 경로 | 연동 서비스 관리 > 연동 서비스 관리 > [차세대] 복구솔루션 · `/hub-service/new-integration-recovery` · 호환 진입 `/hub-service/new-integration-recovery/checklists` |
| 화면 유형·담당 | 연계 진입 · 업무·기술 담당은 해당 메뉴 운영 범위에서 확인 |
| 관련 화면 | 현재 화면에서 결과를 확인한다. |

## 2) 사용 권한과 사전 준비

| 기능·버튼 | 메뉴 권한·추가 조건 | 준비할 데이터 |
| --- | --- | --- |
| 화면 진입 | `/hub-service/new-integration-recovery` 메뉴 접근을 확인한다. 아래 API 권한은 작업별 서버 검사 기준이다. | 접속 환경과 대상 |

코드에서 확인한 버튼·작업명은 **접속**이다. 작업과 대상 상태에 따라 표시가 달라질 수 있다.

## 3) 화면 사용 절차

1. 현재 출처가 Demo 또는 운영 복구솔루션과 같으면 내장 화면을 연다. 다른 환경에서는 안내와 접속 선택지를 표시한다.
2. 지원되는 접속 환경과 내장 화면 상태를 확인한다. 실제 비교·변경의 결과는 차세대 복구솔루션 담당이 확인한다.

## 4) 입력·표시 데이터

| 화면 항목 | 구분·필수 | 형식·기본값·제약 | 의미·API 필드·원천 |
| --- | --- | --- | --- |
| 화면 상태 | 출력 | 접속 환경에 따라 표시 | 현재 출처가 Demo 또는 운영 복구솔루션과 같으면 내장 화면을 연다. 다른 환경에서는 안내와 접속 선택지를 표시한다. |

## 5) API·DB·연계

| 작업 | API·권한 | 입력 → 결과 | 데이터 원천·변경 영향 |
| --- | --- | --- | --- |
| 화면 표시·이동 | 해당 없음 · SmartWork 화면 자체의 업무 API 호출 없음 | 화면 진입 → 현재 출처가 Demo 또는 운영 복구솔루션과 같으면 내장 화면을 연다. 다른 환경에서는 안내와 접속 선택지를 표시한다. | 외부 차세대 복구솔루션 |

| DB 객체 또는 저장소 | 입력·출력 계약 | 읽기·쓰기 대상 및 규칙 | 확인 근거 |
| --- | --- | --- | --- |
| 해당 없음 | 직접 DB 호출 없음 | 외부 차세대 복구솔루션 | [NewIntegrationRecoveryProxyPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/NewIntegrationRecoveryProxyPage.tsx#L9) |

## 6) 예외 상황과 운영 확인

| 상황 | 확인할 항목 | 관리자 대응·문의에 필요한 정보 |
| --- | --- | --- |
| 결과가 비거나 기능을 사용할 수 없음 | 외부 차세대 복구솔루션 | 지원되는 접속 환경과 내장 화면 상태를 확인한다. 실제 비교·변경의 결과는 차세대 복구솔루션 담당이 확인한다. |

## 7) 검증·출처

| 검증 항목 | 근거·환경 | 상태·확인일 |
| --- | --- | --- |
| 대상 선정 | [전체 화면 인벤토리](../../inventory/all-pages.md) | 현재 등록 업무 라우트 2026-11-11 |
| 메뉴·화면·라우트 | [라우트 선언](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/IntegrationRoutes.tsx#L160) · [NewIntegrationRecoveryProxyPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/NewIntegrationRecoveryProxyPage.tsx#L9) | 코드 확인 2026-11-11 · dc216b313 |
| 권한·API·업무 규칙 | [NewIntegrationRecoveryProxyPage.tsx](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/feature/integration/hubservice/NewIntegrationRecoveryProxyPage.tsx#L9) | 화면 소스 확인 2026-11-11 |
| DB 정의·파일·외부 연계 | [개발 DB 정의와 조회 범위](../../references/all-pages-database.md) | 화면 직접 DB 호출 해당 없음 |
| Demo DB 대조 | [페이지별 Demo 대조](../../references/all-pages-demo.md#page-86eb30dc677b28ae) | 해당 없음 · 외부 차세대 복구 화면 진입. 이 페이지의 직접 DB 호출 없음. 외부 시스템 저장소는 확인 범위 밖 · 2026-11-11 |
| 화면 재현 | 실제 검증 계정과 데이터가 있는 환경 | 신규 브라우저 실행 미확인 · 해당 메뉴 운영 담당 확인 |
| 배포 환경·DB 실행 | 배포 권한·업무 저장·외부 처리 | 미확인 · 해당 환경의 운영·기술 담당 확인 |

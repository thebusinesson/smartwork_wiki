# SmartWork 초기세팅

처음 참여한 개발자가 저장소를 받고 프런트엔드·백엔드를 실행한 뒤 로그인·기본 조회를 확인하기 위한 가이드다. 예시 셸은 Ubuntu 22.04 또는 WSL의 Bash 기준이며, Windows IDE에서도 같은 버전·환경변수·프로필을 적용한다. 명령은 **smartwork 저장소**에서 실행하고, 매뉴얼 저장소인 smartwork_wiki에서는 실행하지 않는다.

## 읽는 순서

| 순서 | 문서 | 완료 기준 |
|---|---|---|
| 1 | [개발 도구와 저장소](01-개발도구와-저장소.md) | Git 접근, Node.js 22·Yarn Classic·Java 17·Wrapper 확인 |
| 2 | [DB·연계·파일 준비](04-DB-연계-파일.md) | 개발 DB 접근과 외부 연계·저장소의 사용 범위 확인 |
| 3 | [백엔드 설정과 실행](03-백엔드.md) | local 프로필·인증 설정을 정하고 API 기동 |
| 4 | [프런트엔드 설정과 실행](02-프론트엔드.md) | 의존성 설치·환경변수·개발 서버 확인 |
| 5 | [검증과 문제 해결](05-검증과-문제해결.md) | 로그인·권한·조회와 필요한 검사 결과 확인 |

## 시스템 이해

SmartWork는 스마트빌 관련 업무를 내부 관리자가 운영하는 시스템이다. 브라우저의 React 화면이 Spring Boot API를 호출하고, MyBatis가 SQL Server 저장 프로시저를 통해 업무 데이터를 조회·변경한다. 업무별 의미는 [도메인 지도](../references/domain-overview.md), 화면별 사용법은 [매뉴얼 목차](../inventory/wbs-pages.md)를 참고한다.

```text
Browser → React frontend → /api/v1 → Spring Boot backend
                                        ↓
                                  MyBatis → SQL Server Stored Procedure
                                        ↓
                               기능별 파일 저장소·메일/외부 연계
```

## 기술 스택

아래는 루트 README의 배지와 기준 파일을 대조한 버전이다. Node·Java·Yarn·Git을 준비하면 React·Kotlin·Vite 등 프로젝트 의존성은 Yarn 또는 Gradle이 받는다. 프레임워크를 각각 전역 설치할 필요는 없다.

| 영역 | 기술 | 기준 버전·설명 | 원본 |
|---|---|---|---|
| Frontend 실행 | Node.js | 22 계열; 배포 workflow 기준 | [workflow](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/.github/workflows/deploy-frontend-demo.yml) |
| 패키지 관리 | Yarn | Classic 1.x; yarn.lock 권위, patch 버전은 별도 고정되어 있지 않음 | [README](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/README.md), [lockfile](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/yarn.lock) |
| UI | React / TypeScript | 19.2.3 / 5.9.3 | [lockfile](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/yarn.lock) |
| 개발·빌드 / 테스트 | Vite / Vitest | 7.3.1 / 3.2.4 | [lockfile](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/yarn.lock) |
| 상태 관리 | Zustand | 5.0.10 | [lockfile](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/yarn.lock) |
| 스타일·컴포넌트 | Tailwind CSS / shadcn/ui | 직접 의존 Tailwind 4.1.18, shadcn CLI 3.7.0. shadcn 컴포넌트는 프로젝트 소스로 관리 | [package.json](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/package.json), [lockfile](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/yarn.lock) |
| Backend 실행 | Java | 17 toolchain | [Gradle 설정](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/build.gradle.kts) |
| 언어 / 프레임워크 | Kotlin / Spring Boot | 1.9.25 / 3.3.5 | [Gradle 설정](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/build.gradle.kts) |
| 빌드 | Gradle | Wrapper 8.10.2 | [Wrapper](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/gradle/wrapper/gradle-wrapper.properties) |
| 업무 DB | Microsoft SQL Server / MyBatis | 저장 프로시저 중심. DB 서버 버전은 이 저장소에서 단일 값으로 고정하지 않음 | [Backend README](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/README.md), [SQL 문서 규칙](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/docs/sql/README.md) |

lockfile에는 직접·간접 의존성의 여러 버전이 함께 있을 수 있다. 예를 들어 Tailwind 4.0.16 엔트리도 있으나 직접 의존 selector `tailwindcss@^4.1.17`의 해결 버전은 4.1.18이다. package.json 범위나 첫 검색 결과만으로 배지 버전을 바꾸지 않는다.

## 한눈에 보기

| 영역 | 주요 기술 | 상세 원본 |
|---|---|---|
| Frontend | Node.js 22, React 19, TypeScript, Vite | [frontend/README.md](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/README.md) |
| Backend | Java 17, Kotlin, Spring Boot 3.3.5, MyBatis | [backend/README.md](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/README.md) |
| Database | Microsoft SQL Server, Stored Procedure | [backend/docs/sql/README.md](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/docs/sql/README.md) |

## 시작 전 알아둘 설정

- `local`은 내 PC에서 앱을 실행하는 프로필이며 DB가 격리된다는 의미가 아니다. 기본 연결은 공유 개발 SQL Server다.
- 현재 local에는 `security.permit-all-api=true`, `spring.jpa.hibernate.ddl-auto=update`가 있다. 실제 로그인·권한 검증과 초기 조회용 실행에서는 [백엔드 가이드](03-백엔드.md)의 덮어쓰기를 사용한다.
- 메일 브로커에는 소비자가 연결되어 있고 PG·재전송 등 별도 외부 연계가 있다. 앱이 localhost에서 실행된다는 사실만으로 테스트 발송·금액 처리가 격리되지는 않는다.
- 비밀번호·토큰·실제 고객값을 문서·예제·스크린샷·Git에 기록하지 않는다. 접속값은 승인된 전달·주입 방식을 사용한다.

## 원본 README에서 보완한 내용

| 항목 | 이 가이드에서 적용한 기준 |
|---|---|
| 패키지 매니저 | 루트/Frontend README·workflow의 Yarn 기준. 배포 가이드 일부의 pnpm 예시는 사용하지 않음 |
| build와 테스트 | Backend README에는 build가 테스트 포함이라고 되어 있지만 실제 Test 태스크는 test 명시 때만 실행되므로 `./gradlew test`를 별도 수행 |
| 환경 준비 | `.env.example`, 프로필·인증·DB·메일·파일·포트·검증 순서 추가 |
| Docker | docker-compose.dev.yml은 개발 서버용 앱 구성. 로컬 전용 DB까지 만드는 완전한 격리 환경으로 설명하지 않음 |

원본 설정이 바뀌면 이 폴더와 연결된 페이지를 함께 갱신한다. 환경별 값은 문서에 복제하지 않고 소스·배포 설정을 원본으로 유지한다.

작성·소스 확인일: 2026-11-09 · SmartWork 코드 기준 `dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc`. 명령·설정은 저장소 소스와 대조했으며 새 PC에서 전체 설치·DB·메일 연계 실행을 재현한 결과는 아니다.

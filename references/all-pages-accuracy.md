# 전체 페이지 매뉴얼 정확성·일관성 점검

2026-11-11 기준 SmartWork <code>dc216b313</code>와 <code>docs/page-work-inventory</code> 작업본을 대조했다. [전체 페이지 목차](../inventory/all-pages.md)

## 전체 문서 대조

| 검증 항목 | 범위와 결과 |
|---|---|
| 대상과 양식 | 업무 라우트 433개와 매뉴얼 433개가 대응한다. 모든 문서에서 공통 7개 항목과 각 표의 열·순서, 문서 및 소스 링크를 검사했다. |
| API와 권한 | 매뉴얼의 API 행 1,216개를 현재 Controller의 HTTP 메서드·경로에 연결했다. 그중 정적 권한 선언이 있는 1,097개 행의 액션을 대조했고 차이 0건을 확인했다. 요청별 프로그램 권한과 실제 역할의 허용·거부는 환경 확인 대상이다. |
| 화면별 역할 | 공용 폼을 사용하는 등록·수정·답글의 경로와 코드 분기를 대조했다. 등록 모드가 쓰지 않는 수정·삭제, 수정 모드가 쓰지 않는 신규 등록 등을 정리했다. |
| DB | 페이지별 Demo 링크, 객체 대조, 미확인 객체 표기를 검사했다. 추가된 원문 조회에 필요한 객체는 개발·Demo에서 읽기 전용으로 확인했다. [Demo DB 대조](all-pages-demo.md) |

## 확인 후 보완한 내용

[112개 화면별 수정 목록](all-pages-accuracy-changes.md)

- 공용 폼과 훅에서 다른 모드의 API가 함께 들어간 문서 38개에서 비활성 API 행 70개를 정리했다. 예를 들어 권한 그룹 등록은 신규 그룹을 생성하며, 권한 그룹 상세는 같은 주소에서 수정 모드로 전환한다. [권한 그룹 등록](../manuals/settings/permissions__new.md) · [권한 그룹 상세](../manuals/settings/permissions__by-id.md)
- 공통 마스킹 컴포넌트의 실제 서버 호출을 대조해 48개 문서에 원문 조회 API 51개와 <code>UNMASK</code> 권한, 관련 근거를 추가했다. [권한 관리 목록](../manuals/settings/permissions.md)
- 33개 문서에서 입력란 이름을 버튼 목록에서 제외했고, 10개 문서의 설정 메뉴 상위 명칭을 실제 표시인 **SmartWork 관리**로 맞췄다. 중복을 합쳐 총 112개 문서의 내용을 보완했다.

## 브라우저 표본과 남은 검증

| 화면 | 실제 확인 범위 |
|---|---|
| [/settings/permissions/new](../manuals/settings/permissions__new.md) | 등록 화면 진입 및 표시 확인 · 권한 그룹 생성 진입 버튼, 등록 · 2026-11-11 |
| [/bonabank/notices/new](../manuals/bonabank/notices__new.md) | 등록 화면 진입 및 표시 확인 · 작성 진입 버튼, 제목, 저장 · 2026-11-11 |
| [/payment/manual-transactions/new](../manuals/payment/manual-transactions__new.md) | 등록 경로 진입 확인 · 2026-11-11 |

등록 화면 표본은 진입과 관찰한 항목만 기록했다. 저장·삭제·발송·금액 처리와 역할별 접근, 그 밖의 페이지별 화면 동작은 해당 환경에서 추가 검증이 필요하다. [이번 Playwright 근거](../evidence/browser/all-pages-accuracy-2026-11-11.json) · [기존 전체 페이지 표본](../evidence/browser/all-pages-sample-2026-11-11.json)

프로젝트 완료 화면의 연동 요청과 청구 등록은 프런트엔드에 호출 선언이 있으며, 현재 소스에서 대응 Controller가 확인되지 않았다. 문서에서 기술 담당 확인 항목으로 유지했다. [프로젝트 완료 관리](../manuals/hub-collab/project-completion.md)

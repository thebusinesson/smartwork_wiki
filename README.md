# SmartWork 관리자 매뉴얼

SmartWork에 등록된 업무 화면 433개의 페이지별 관리자 매뉴얼을 제공한다.

**[전체 페이지 매뉴얼 목차](inventory/all-pages.md)** · [WBS 담당 화면 134개](inventory/wbs-pages.md)

처음 읽는 경우 [업무 도메인 지도](references/domain-overview.md)에서 업무 영역을 찾고, 개발 환경을 준비하려면 [초기세팅 가이드](초기세팅/README.md)부터 시작한다.

- 기존 WBS 조사 범위는 태스크 105개, 업무 메뉴 범위 56개(코드상 사이드바 진입점 57개), 독립 화면 경로 134개.
- 문서 형식: 화면 기본 정보(도메인 이해·이 페이지의 역할 포함) → 권한·준비 → 사용 절차 → 입력·표시 데이터 → API·DB·연계 → 예외 대응 → 검증·출처.
- 현재 상태: 코드·개발 DB 정의 조사와 로컬 브라우저 대조 반영, 업무·미재현 범위 검토 대기. 실제 실행 검증 범위는 아래 문서를 확인한다.

## 목록과 작성 기준

- [선정 WBS 태스크 CSV](inventory/wbs-tasks.csv)
- [페이지 조사 목록 CSV](inventory/wbs-pages.csv)
- [제외 경로와 사유 CSV](inventory/excluded-routes.csv)
- [공통 작성 기준](MANUAL_GUIDE.md)
- [페이지별 복사용 양식](templates/page-manual.md)

- [페이지 누락·도메인 설명 일관성 검증](references/coverage-domain-audit.md)
- [페이지별 업무 설명·화면 소스 대조](references/page-domain-review.md)
- [Playwright 브라우저 검증 결과·경로별 증적](references/browser-verification.md)

## 기술 근거

- [API 계약과 호출 경로](references/api-contracts.md)
- [개발 DB 객체 계약](references/database-contracts.md)
- [전체 화면 매뉴얼의 개발 DB 근거](references/all-pages-database.md)
- [전체 화면 매뉴얼의 Demo DB 대조](references/all-pages-demo.md)
- [검증 범위·미확인 항목·후속 확인 담당](references/verification.md)

확인일: 2026-11-09. 코드 기준: `dc216b313`. 브랜치: `codex/wbs-yujiyoon-manuals`.

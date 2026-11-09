# SmartWork 관리자 매뉴얼

제공받은 **WBS 탭의 작업자 `유지윤`**을 기준으로 작성한 페이지별 관리자 매뉴얼이다.

**[전체 매뉴얼 목차 및 조사 상태](inventory/wbs-pages.md)**

처음 읽는 경우 [업무 도메인 지도](references/domain-overview.md)에서 업무 영역을 찾고, 개발 환경을 준비하려면 [초기세팅 가이드](초기세팅/README.md)부터 시작한다.

- 대상: WBS 태스크 105개, 현재 메뉴 56개, 독립 화면 경로 134개.
- 문서 형식: 화면 기본 정보(도메인 이해·이 페이지의 역할 포함) → 권한·준비 → 사용 절차 → 입력·표시 데이터 → API·DB·연계 → 예외 대응 → 검증·출처.
- 현재 상태: 코드·개발 DB 정의 조사와 로컬 브라우저 대조 반영, 업무·미재현 범위 검토 대기. 실제 실행 검증 범위는 아래 문서를 확인한다.

## 목록과 작성 기준

- [선정 WBS 태스크 CSV](inventory/wbs-tasks.csv)
- [페이지 조사 목록 CSV](inventory/wbs-pages.csv)
- [제외 경로와 사유 CSV](inventory/excluded-routes.csv)
- [공통 작성 기준](MANUAL_GUIDE.md)
- [페이지별 복사용 양식](templates/page-manual.md)

- [Playwright 브라우저 검증 결과·경로별 증적](references/browser-verification.md)

## 기술 근거

- [API 계약과 호출 경로](references/api-contracts.md)
- [개발 DB 객체 계약](references/database-contracts.md)
- [검증 범위·미확인 항목·후속 확인 담당](references/verification.md)

확인일: 2026-11-09. 코드 기준: `dc216b313`. 브랜치: `codex/wbs-yujiyoon-manuals`.

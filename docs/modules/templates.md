# Templates Module

## 책임

- 새 프로젝트에 복사할 문서 초안 제공
- 최소 지시와 상세 문서 분리 원칙 반영
- 템플릿과 실제 예시의 역할 경계 유지

## 먼저 읽을 파일

- `templates/AGENTS.md`
- `templates/CLAUDE.md`
- `templates/ARCHITECTURE.md`
- `templates/module.md`
- `templates/verification.md`
- `templates/bootstrap_prompt.md`

## 수정 시 주의

- 템플릿을 추가하거나 삭제하면 `README.md`와 `SETUP_STEPS.md`의 목록을 함께 갱신한다.
- `AGENTS.md`에는 공통 최소 규칙만 남긴다.
- 특정 도구 전용 메모는 선택 파일로 취급한다.
- 채워진 예시는 `docs/examples/`에 두고 템플릿 본문을 불필요하게 늘리지 않는다.

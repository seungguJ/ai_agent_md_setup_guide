# Claude Handoff Module

## 책임

- Claude CLI 자동 위임 실행
- prompt, response, meta 로그 저장
- 연결 확인 절차 제공

## 먼저 읽을 파일

- `docs/agent_runtime.md`
- `scripts/claude_handoff.sh`
- `docs/handoffs/connectivity-check.md`

## 진입점

- `scripts/claude_handoff.sh --task-file docs/handoffs/connectivity-check.md`

## 수정 시 주의

- 스크립트 인자 변경 시 runtime 문서와 README 예시를 같이 갱신한다.
- 로그 저장 위치가 바뀌면 `.gitignore`와 검증 기준도 같이 바꿔야 한다.

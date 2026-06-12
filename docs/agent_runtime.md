# agent_runtime.md

## 목적

이 문서는 이 저장소에서 `scripts/claude_handoff.sh`를 실제로 실행할 때의 기준을 정의한다.

## 구성 요소

- 역할 정의: `AGENTS.md`, `CLAUDE.md`
- 입력 템플릿: `docs/template.md`
- 실행 스크립트: `scripts/claude_handoff.sh`
- 실행 로그: `.claude/handoffs/`

## 사전 조건

- `claude` CLI 설치
- `claude auth login` 완료
- 루트에 `CLAUDE.md` 존재
- `docs/handoffs/*.md` task file 존재

## 표준 호출 흐름

1. 관리자 Agent가 task file을 준비한다.
2. `scripts/claude_handoff.sh --task-file <path>`를 실행한다.
3. prompt, response, meta 파일 생성 여부를 확인한다.
4. response 파일 내용이 task 요구사항을 만족하는지 확인한다.
5. 결과를 setup 문서에 반영한다.

## 확인 결과 기록 규칙

- 성공 시 생성 파일 경로를 남긴다.
- 실패 시 종료 코드와 stderr 핵심 문구를 남긴다.
- 문서와 실제 동작 차이가 있으면 문서를 수정한다.

## 현재 저장소에서 확인된 동작

- 검증 일시: 2026-06-12
- 실행 명령: `bash scripts/claude_handoff.sh --task-file docs/handoffs/connectivity-check.md --label live-connectivity-check --timeout-seconds 180`
- 결과: 종료 코드 `0`
- 생성 파일:
  - `.claude/handoffs/20260612-225638-live-connectivity-check.prompt.md`
  - `.claude/handoffs/20260612-225638-live-connectivity-check.response.md`
  - `.claude/handoffs/20260612-225638-live-connectivity-check.meta.txt`

주의:

- response 파일은 Claude 응답 본문만 저장한다.
- 저장 경로 요약 문구는 콘솔 출력에만 나타난다.

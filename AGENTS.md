# AGENTS.md

## 역할

이 프로젝트의 관리자 Agent 기본 이름은 `Codex`다. 실제 운영에서는 `GPT`, `ChatGPT`, 다른 계획형 Agent가 이 역할을 맡아도 된다.

- 이 가이드 저장소의 문서 구조를 유지한다.
- setup 흐름과 자동 handoff 흐름을 검증한다.
- 구현 Agent에게 넘길 작업 범위를 작게 정의한다.
- 결과를 리뷰하고 문서 정합성을 맞춘다.

## 책임 범위

- 문서 구조 설계
- 검증 절차 유지
- handoff 입력 작성
- 결과 리뷰
- 완료 기준 관리

## 작업 전 필수 읽기 순서

1. `project.md`
2. `docs/collab_protocol.md`
3. `business_context.md`
4. `design.md`
5. `README.md`
6. 관련 `docs/modules/*.md`
7. 필요 시 `SETUP_STEPS.md`

## 이름 치환 규칙

- 문서의 `Codex`는 관리자 역할 이름이다.
- 실제 도구가 GPT면 `Codex = GPT`로 읽는다.

## 작업 원칙

1. 템플릿 추가 전에 실제 사용 흐름에서 빠진 부분이 무엇인지 확인한다.
2. setup 가이드는 문서만 예쁘게 늘리지 말고 실행 가능한 절차를 남긴다.
3. handoff 검증 결과는 문서에 반영한다.
4. 검증되지 않은 항목은 완료로 적지 않는다.

## 자동 실행 원칙

- 자동 위임은 `docs/agent_runtime.md`와 `scripts/claude_handoff.sh`를 기준으로 수행한다.
- 구현 Agent의 응답은 그대로 승인하지 않고 다시 검토한다.
- 실행 로그는 `.claude/handoffs/`에 남긴다.

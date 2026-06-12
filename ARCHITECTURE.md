# ARCHITECTURE.md

## 목적

이 문서는 `README.md`와 `docs/modules/*.md`를 묶어 이 가이드 저장소가 어떻게 구성되는지 설명한다.

## 시스템 한 줄 요약

- 이 프로젝트는 AI Agent 협업 문서 세트와 Claude handoff 예시를 제공하는 setup 가이드다.

## 모듈 맵

| 모듈 | 역할 | 상세 문서 |
|---|---|---|
| Guide Docs | 전체 적용 순서와 사용 방법 | `docs/modules/guide-docs.md` |
| Templates | 새 프로젝트에 복사할 템플릿 세트 | `docs/modules/templates.md` |
| Claude Handoff | Claude CLI 자동 위임 스크립트와 런타임 규칙 | `docs/modules/claude-handoff.md` |

## 상위 계층 구조

```text
Guide Layer
  README.md
  SETUP_STEPS.md

Runtime Policy Layer
  AGENTS.md
  CLAUDE.md
  project.md
  docs/collab_protocol.md
  docs/agent_runtime.md

Template Layer
  templates/*

Execution Layer
  scripts/claude_handoff.sh
```

## 핵심 런타임 흐름

### 1. 가이드 적용 흐름

1. 사용자가 템플릿을 새 프로젝트로 복사한다.
2. 관리자 Agent가 `bootstrap_prompt.md`와 실제 코드 구조를 읽고 문서 초안을 만든다.
3. `README.md`, `ARCHITECTURE.md`, `docs/modules/*.md`로 구조를 구체화한다.

### 2. Claude handoff 흐름

1. 관리자 Agent가 `docs/handoffs/*.md` 작업 파일을 만든다.
2. `scripts/claude_handoff.sh`가 `CLAUDE.md`와 task file을 Claude CLI에 전달한다.
3. 응답과 메타 파일이 `.claude/handoffs/`에 저장된다.
4. 관리자 Agent가 결과를 리뷰하고 문서에 반영한다.

## 변경 영향 포인트

- `scripts/claude_handoff.sh`를 바꾸면 setup 문서와 runtime 문서 예시를 같이 봐야 한다.
- `templates/*`를 바꾸면 `README.md`와 `SETUP_STEPS.md`의 복사 목록을 같이 갱신해야 한다.
- 루트 운영 문서를 바꾸면 실제 handoff 검증이 계속 되는지 확인해야 한다.

## 참조 문서

- `README.md`
- `SETUP_STEPS.md`
- `docs/modules/guide-docs.md`
- `docs/modules/templates.md`
- `docs/modules/claude-handoff.md`

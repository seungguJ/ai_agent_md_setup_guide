# AI Agent MD Setup Guide

이 저장소는 AI 에이전트용 프로젝트 문서를 한 파일에 몰아넣지 않고, 최소 지시와 상세 문서를 분리해 운영하는 방법을 정리한 가이드다.

핵심 원칙은 세 가지다.

- `AGENTS.md`에는 에이전트가 반드시 지켜야 할 최소 규칙만 둔다.
- 사람이 읽는 설명은 `README.md`, `ARCHITECTURE.md`, `docs/*.md`로 분리한다.
- 현재 작업 지시는 `project.md`, `docs/template.md`, `tasks/*` 같은 작업 문서에 따로 둔다.

긴 컨텍스트 파일 하나로 모든 것을 해결하려 하지 않고, 필요한 문서만 읽게 구조를 나누는 것이 목표다.

## Research Basis

이 저장소의 문서 원칙은 아래 자료를 직접 참고해 정리했다.

- 2026-01-23, *On the Impact of AGENTS.md Files on the Efficiency of AI Coding Agents*: AGENTS.md가 있는 경우 실행 시간과 출력 토큰이 각각 감소하는 경향을 보고했다. 이 저장소는 이를 근거로 `AGENTS.md` 자체는 유지하되, 짧고 기능적인 규칙만 남긴다. https://arxiv.org/abs/2601.20404
- 2025-11-17, *Agent READMEs: An Empirical Study of Context Files for Agentic Coding*: 실제 저장소의 컨텍스트 파일이 빌드/실행, 구현 세부, 아키텍처에 집중되고 보안/성능 같은 비기능 요구는 적게 다뤄진다고 보고했다. 이 저장소는 기능 중심 문서 구조를 기본으로 두되, 비기능 기준이 필요하면 별도 문서에 명시하도록 유도한다. https://arxiv.org/abs/2511.12884
- 2026-02-12, *Evaluating AGENTS.md: Are Repository-Level Context Files Helpful for Coding Agents?*: 불필요한 요구가 많은 컨텍스트 파일은 성공률을 낮추고 비용을 높일 수 있으므로 최소 요구사항 중심으로 작성해야 한다고 결론냈다. 이 저장소가 `AGENTS.md`를 최소 규칙 문서로 제한하는 가장 직접적인 근거다. https://arxiv.org/abs/2602.11988
- 2025-09-29, Anthropic, *Effective context engineering for AI agents*: 컨텍스트는 유한 자원이며, 장기 작업에서는 compaction과 structured note-taking이 중요하다고 설명한다. 이 저장소의 `tasks/*`, 아카이브 규칙, 문서 분리 원칙은 이 방향을 따른다. https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents

요약하면, 이 저장소는 "컨텍스트 파일을 없애는 것"이 아니라 "최소 고신호 문서만 남기고 나머지는 역할별로 분리하는 것"을 목표로 한다.

## 추천 구조

```text
.
├── README.md
├── AGENTS.md
├── CLAUDE.md
├── project.md
├── business_context.md
├── design.md
├── ARCHITECTURE.md
├── docs/
│   ├── collab_protocol.md
│   ├── examples/
│   ├── template.md
│   └── modules/
├── tasks/
│   ├── TODO.md
│   ├── PROMPT.md
│   └── CHANGELOG_NOTES.md
└── templates/
```

`CLAUDE.md`는 선택 사항이다. 특정 도구가 자체 프로젝트 메모 파일을 읽는 경우에만 둔다. `AGENTS.md`와 역할을 나누기 위한 필수 파일은 아니다.

## 파일 역할

- `README.md`: 프로젝트 개요, 실행법, 문서 인덱스
- `AGENTS.md`: 에이전트 공통 최소 규칙
- `CLAUDE.md`: Claude Code 같은 특정 도구용 선택 메모
- `project.md`: 현재 작업 상태와 최근 결정
- `business_context.md`: 제품 목적, 사용자, 우선순위
- `design.md`: 결과물 판단 기준
- `ARCHITECTURE.md`: 구조, 모듈, 변경 영향 포인트
- `docs/collab_protocol.md`: 작업 상태 관리와 문서 갱신 규칙
- `docs/template.md`: 작업 등록과 작업 지시 템플릿
- `docs/modules/*.md`: 기능 또는 문서 묶음별 상세 설명
- `tasks/*`: 이번 작업에만 필요한 작업 목록과 프롬프트
- `docs/examples/*`: 실제로 채워진 예시 문서

## 단일 읽기 순서

읽기 순서는 `docs/collab_protocol.md`만 기준으로 유지한다. 다른 문서에는 같은 순서를 복제하지 않는다.

## 적용 순서

1. `templates/`에서 기본 문서를 복사한다.
2. `README.md`에 프로젝트 개요와 문서 인덱스를 채운다.
3. `AGENTS.md`에는 최소 규칙만 남긴다.
4. `project.md`에 현재 작업과 상태 규칙을 적는다.
5. `business_context.md`, `design.md`, `ARCHITECTURE.md`를 실제 프로젝트 기준으로 채운다.
6. `docs/modules/*.md`에 핵심 기능별 수정 진입점을 정리한다.
7. 작업이 생기면 `project.md`와 `docs/template.md` 형식으로 범위를 분리해 기록한다.

## 문서 크기 정책

이 기준은 연구의 정량 임계값이 아니라, 최소 고신호 컨텍스트를 유지하라는 연구 결과를 바탕으로 이 저장소에 맞게 정한 운영 규칙이다.

- `AGENTS.md`: 50줄 안팎 유지
- 인덱스성 문서: 150줄 안팎을 넘기면 분리 검토
- 한 문서에 목적이 2개 이상 섞이면 분리
- 예시와 기록은 템플릿 본문에 누적하지 않고 `docs/examples/` 또는 `tasks/*`로 이동

## context rot 대응

- 끝난 작업은 계속 `project.md`에 쌓아두지 않고 필요 시 [tasks/CHANGELOG_NOTES.md](tasks/CHANGELOG_NOTES.md)로 이동한다.
- `tasks/PROMPT.md`는 현재 작업용으로만 유지한다.
- 오래된 예시는 `docs/examples/`에 모으고, 템플릿은 항상 최소형만 유지한다.

## 실제 예시

- 예시 개요: [docs/examples/README.md](docs/examples/README.md)
- 샘플 모듈 문서: [docs/examples/sample-module.md](docs/examples/sample-module.md)
- 샘플 작업 문서: [docs/examples/sample-task.md](docs/examples/sample-task.md)
- 샘플 상태판: [docs/examples/sample-project.md](docs/examples/sample-project.md)

## 템플릿 복사 위치

| 이 저장소 파일 | 새 프로젝트 위치 |
|---|---|
| `templates/AGENTS.md` | `AGENTS.md` |
| `templates/CLAUDE.md` | `CLAUDE.md` |
| `templates/project.md` | `project.md` |
| `templates/ARCHITECTURE.md` | `ARCHITECTURE.md` |
| `templates/business_context.md` | `business_context.md` |
| `templates/design.md` | `design.md` |
| `templates/docs_collab_protocol.md` | `docs/collab_protocol.md` |
| `templates/docs_template.md` | `docs/template.md` |
| `templates/module.md` | `docs/modules/<module-name>.md` |
| `templates/tasks_TODO.md` | `tasks/TODO.md` |
| `templates/tasks_PROMPT.md` | `tasks/PROMPT.md` |
| `templates/tasks_CHANGELOG_NOTES.md` | `tasks/CHANGELOG_NOTES.md` |
| `templates/bootstrap_prompt.md` | `bootstrap_prompt.md` |

## 문서 설계 기준

- `AGENTS.md`는 짧게 유지한다.
- 상세 설명은 `docs/`와 개별 문서로 보낸다.
- 작업 지시는 현재 작업만 다룬다.
- 역할 이름에 의존하지 않는다. 하나의 에이전트가 독립적으로 작업해도 구조가 성립해야 한다.
- 검증하지 않은 자동화나 운영 흐름은 문서에 적지 않는다.

## 검증 기준

- 새 에이전트가 `AGENTS.md`와 `README.md`만 읽고 문서 구조를 이해할 수 있어야 한다.
- 현재 작업 상태는 `project.md`만 보면 파악 가능해야 한다.
- `ARCHITECTURE.md`와 `docs/modules/*.md`만으로 수정 진입점을 좁힐 수 있어야 한다.
- 작업 문서는 목적, 변경 대상, 금지 사항, 검증 방법, 완료 조건을 포함해야 한다.
- 역할 분리 없이도 문서 세트가 독립적으로 동작해야 한다.

## 주의사항

- `AGENTS.md`에 아키텍처 설명까지 몰아넣지 않는다.
- 특정 도구 전용 파일이 있더라도 공통 규칙은 `AGENTS.md` 기준으로 유지한다.
- 기존 사용자 변경이 있는 파일은 추측으로 덮어쓰지 않는다.

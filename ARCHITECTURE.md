# ARCHITECTURE.md

## 목적

이 문서는 `README.md`와 `docs/modules/*.md`를 묶어 이 가이드 저장소의 구조를 설명한다.

## 시스템 한 줄 요약

- 이 프로젝트는 AI 에이전트용 문서 구조를 최소 지시, 사람용 설명, 작업별 상세 문서로 분리하는 setup 가이드다.

## 모듈 맵

| 모듈 | 역할 | 상세 문서 |
|---|---|---|
| Guide Docs | 전체 적용 순서와 사용 방법 | `docs/modules/guide-docs.md` |
| Templates | 새 프로젝트에 복사할 템플릿 세트 | `docs/modules/templates.md` |

## 상위 계층 구조

```text
Guide Layer
  README.md
  SETUP_STEPS.md

Policy Layer
  AGENTS.md
  project.md
  docs/collab_protocol.md

Context Layer
  business_context.md
  design.md
  ARCHITECTURE.md
  docs/modules/*

Template Layer
  templates/*
```

## 핵심 흐름

### 1. 가이드 적용 흐름

1. 사용자가 템플릿을 새 프로젝트로 복사한다.
2. 에이전트가 `AGENTS.md`와 `README.md`를 기준으로 구조를 파악한다.
3. `business_context.md`, `design.md`, `ARCHITECTURE.md`, `docs/modules/*.md`를 실제 프로젝트 기준으로 채운다.
4. `project.md`와 작업 문서를 사용해 현재 작업 범위를 관리한다.

### 2. 문서 운영 흐름

1. 새 작업을 `project.md`에 등록한다.
2. 작업 상세는 `docs/template.md` 형식이나 `tasks/*` 문서로 분리한다.
3. 구조 변경 시 `README.md`, `ARCHITECTURE.md`, 템플릿을 함께 갱신한다.
4. 검증이 끝난 뒤에만 상태를 `done`으로 바꾼다.

## 변경 영향 포인트

- `templates/*`를 바꾸면 `README.md`와 `SETUP_STEPS.md`의 복사 목록을 같이 갱신해야 한다.
- 공통 규칙을 바꾸면 `AGENTS.md`와 `docs/collab_protocol.md`를 같이 봐야 한다.
- 문서 역할이 바뀌면 `docs/modules/*.md` 설명도 함께 수정해야 한다.

## 참조 문서

- `README.md`
- `SETUP_STEPS.md`
- `docs/modules/guide-docs.md`
- `docs/modules/templates.md`

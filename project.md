# project.md

## 목적

이 문서는 `ai_agent_md_setup_guide`의 작업 현황판이다.

## 시작 전 참고 순서

- 읽기 순서는 `docs/collab_protocol.md`를 기준으로 본다.
- 이 문서는 현재 작업 상태와 최근 결정만 관리한다.

## 상태 규칙

- `todo`: 시작 전
- `in_progress`: 진행 중
- `review`: 구현 완료, 검토 대기
- `blocked`: 외부 확인 필요
- `done`: 검증과 문서 반영까지 완료

## 현재 작업 현황

| ID | 작업명 | 담당 | 상태 | 산출물 | 비고 |
|---|---|---|---|---|---|
| P-001 | setup guide 골격 정리 | Codex | done | 템플릿, README, setup 문서 | 초기 문서화 |
| P-002 | 최소 지시 중심 구조 보강 | Codex | done | README, 템플릿 보강 | 문서 분리 원칙 반영 |
| P-003 | 독립 운영 구조 전환 | Codex | done | 루트 운영 문서, 템플릿 정리 | 역할 분리 제거 |
| P-004 | 연구 근거 및 예시 보강 | Codex | done | README, 운영 규칙, 예시 문서 | 평가 반영 |
| P-005 | harness engineering 적용 | Claude | done | `docs/modules/harness-engineering.md`, `templates/verification.md`, `verification.md`, README/ARCHITECTURE/AGENTS/collab_protocol/SETUP_STEPS/bootstrap_prompt 갱신 | 검증 루프(feedback)와 무한 루프 방지 조건 추가 |

## 최근 결정

- 이 저장소는 역할 분리형 운영보다 독립 실행 가능한 문서 구조를 우선한다.
- `AGENTS.md`는 최소 규칙만 담고, 상세 설명은 별도 문서로 분리한다.
- `CLAUDE.md`는 선택적 도구 메모로만 취급한다.
- 읽기 순서는 `docs/collab_protocol.md`를 단일 기준으로 유지한다.
- 이 저장소는 harness 중 문서(feedforward) 레이어만 다루고, 검증 루프(feedback)는 `verification.md`로 분리해 정책만 정의한다. 도구 권한·observability는 범위 밖이다.
- `verification.md`에는 무한 루프 방지 조건(최대 반복 횟수, 무진전 감지, 멈춤 시 보고)을 반드시 포함한다.

## 꼭 체크해야 할 목록

- 역할 분리 전제를 문서에서 제거한다.
- 템플릿 목록과 실제 `templates/` 구성이 일치해야 한다.
- 삭제된 운영 방식을 완료 기준에 남기지 않는다.
- 오래된 완료 작업은 필요 시 `tasks/CHANGELOG_NOTES.md`로 이동한다.

## 다음 작업 작성 규칙

- 작업 목적
- 시작 조건
- 완료 조건
- 관련 문서
- 관련 파일

## 완료 정의

- 실제 문서 구조 반영
- 관련 템플릿 갱신
- 상호 참조 정리

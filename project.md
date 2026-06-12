# project.md

## 목적

이 문서는 `ai_agent_md_setup_guide`의 작업 현황판이다.

- 현재 진행 작업
- 담당자
- 상태
- 최근 결정
- 다음 액션

## 시작 전 참고 순서

1. `project.md`
2. `docs/collab_protocol.md`
3. 역할 문서 (`AGENTS.md` 또는 `CLAUDE.md`)
4. `business_context.md`
5. `design.md`
6. `README.md`
7. 관련 `docs/modules/*.md`
8. 필요 시 `SETUP_STEPS.md`

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
| P-002 | GPT 관리자 치환 규칙 추가 | Codex | done | README, SETUP_STEPS, 템플릿 보강 | GPT bootstrap 포함 |
| P-003 | 실제 Claude handoff 검증과 setup 보정 | Codex | review | 루트 운영 문서, handoff 로그, 검증 반영 문서 | 2026-06-12 live connectivity check 성공 |

## 최근 결정

- 이 저장소 자체도 템플릿 모음이 아니라 실행 검증 가능한 예시 프로젝트처럼 유지한다.
- 관리자 역할 이름은 `Codex`로 두되 GPT가 그대로 대체 가능해야 한다.
- Claude handoff 검증은 템플릿만이 아니라 루트 운영 문서를 기준으로 실행한다.

## 꼭 체크해야 할 목록

- handoff 검증 결과가 실제 로그 파일로 남아야 한다.
- 문서상 예시와 실제 스크립트 동작이 어긋나면 문서를 먼저 고친다.
- `.claude/` 로그는 Git 추적 대상에 올리지 않는다.

## 다음 작업 작성 규칙

- 작업 목적
- 시작 조건
- 완료 조건
- 관련 문서
- 관련 파일

## 완료 정의

- 실제 검증 수행
- 결과 반영
- 관련 문서 갱신

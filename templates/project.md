# project.md

## 목적

이 문서는 여러 AI Agent가 함께 사용하는 작업 현황판이다.

- 현재 진행 작업
- 담당자
- 상태
- 최근 결정 사항
- 다음 액션

## 시작 전 참고 순서

1. `project.md`
2. `docs/collab_protocol.md`
3. 본인 역할 문서 (`AGENTS.md` 또는 `CLAUDE.md`)
4. `business_context.md`
5. `design.md`
6. `README.md`
7. 관련 `docs/modules/*.md`

## 상태 규칙

- `todo`: 시작 전
- `in_progress`: 진행 중
- `review`: 구현 완료, 검토 대기
- `blocked`: 외부 확인 필요
- `done`: 검증과 문서 반영까지 완료

## 현재 작업 현황

| ID | 작업명 | 담당 | 상태 | 산출물 | 비고 |
|---|---|---|---|---|---|
| P-001 | 협업 문서 체계 수립 | Codex | todo | Agent 문서, 협업 문서 | 초기 설정 |

## 최근 결정

- Codex는 관리자 역할, Claude는 실무자 역할로 분리한다.
- 진행 상태 공유의 단일 기준 문서는 `project.md`다.
- 협업 프로토콜은 `docs/collab_protocol.md`에서 관리한다.
- 자동 위임은 문서만으로 활성화하지 않고 `docs/agent_runtime.md`와 `scripts/claude_handoff.sh`를 함께 유지한다.

## 꼭 체크해야 할 목록

- 프로젝트별 핵심 제약을 여기에 적는다.
- 보안, 개인정보, 성능, 비용, 운영 리스크를 우선 적는다.
- Agent가 작업 전 반드시 확인해야 하는 금지 사항을 적는다.

## 다음 작업 작성 규칙

새 작업을 추가할 때 아래 항목을 같이 기록한다.

- 작업 목적
- 시작 조건
- 완료 조건
- 관련 문서
- 관련 코드 파일

## 완료 정의

- 요구사항 반영 완료
- 기본 검증 완료
- 리스크 기록 완료
- 필요한 문서 갱신 완료

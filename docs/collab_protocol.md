# collab_protocol.md

## 목적

이 문서는 이 저장소에서 관리자 Agent와 Claude가 어떻게 협업하는지 정의한다.

## 공통 문서 맵

- `project.md`: 현재 작업 상태
- `AGENTS.md`: 관리자 역할 규칙
- `CLAUDE.md`: 구현 역할 규칙
- `README.md`: 전체 인덱스
- `ARCHITECTURE.md`: 구조와 흐름
- `docs/template.md`: 작업 지시와 보고 형식
- `docs/agent_runtime.md`: 실제 handoff 실행 규칙

## 공통 작업 순서

1. `project.md`
2. `docs/collab_protocol.md`
3. 역할 문서
4. `business_context.md`
5. `design.md`
6. `README.md`
7. 관련 `docs/modules/*.md`

## 역할 분리

### Codex

- 작업 정의
- 범위 통제
- 리뷰

### Claude

- 구현
- 검증
- 결과 보고

## 인계 및 승인

1. Codex가 작업 파일을 작성한다.
2. Claude가 작업을 수행하거나 연결 확인 응답을 반환한다.
3. Codex가 로그와 응답을 확인한다.
4. 검증 결과를 문서에 반영한다.

## 충돌 방지 규칙

- 템플릿 변경 시 루트 가이드 문서와 함께 검토한다.
- 자동화 검증 결과가 바뀌면 runtime 문서를 먼저 갱신한다.

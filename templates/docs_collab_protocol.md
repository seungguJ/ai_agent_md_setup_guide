# collab_protocol.md

## 목적

이 문서는 작업 상태를 관리하고 문서 충돌을 줄이기 위한 공통 운영 규칙을 정의한다.

## 공통 문서 맵

- `project.md`
- `AGENTS.md`
- `README.md`
- `business_context.md`
- `design.md`
- `verification.md`
- `ARCHITECTURE.md`
- `docs/template.md`
- `docs/modules/*.md`

## 공통 작업 순서

1. `project.md`
2. `docs/collab_protocol.md`
3. `AGENTS.md`
4. `business_context.md`
5. `design.md`
6. `verification.md`
7. `README.md`
8. 관련 `docs/modules/*.md`
9. 필요 시 `ARCHITECTURE.md`
10. 실제 파일

이 순서는 단일 기준이다. 다른 문서에는 반복해서 적지 않는다.

## 작업 운영 규칙

- 모든 작업은 `project.md`에 등록한다.
- 시작 전에 상태를 `in_progress`로 바꾼다.
- 검증과 문서 반영까지 끝나야 `done`으로 바꾼다.
- 새 작업 시작 전 파일 충돌 여부를 확인한다.

## 문서 분리 규칙

- `AGENTS.md`는 짧게 유지한다.
- 구조 설명은 `README.md`와 `ARCHITECTURE.md`로 분리한다.
- 현재 작업 상세는 `docs/template.md` 형식이나 `tasks/*` 문서에 둔다.
- 특정 도구 메모는 선택 파일로 분리하되 공통 규칙을 중복하지 않는다.

## 크기와 보관 규칙

- `AGENTS.md`는 50줄 안팎으로 유지한다.
- 인덱스 문서는 150줄 안팎을 넘기면 분리 검토한다.
- 완료된 작업 메모는 `tasks/CHANGELOG_NOTES.md`로 이동한다.
- 예시는 템플릿이 아니라 `docs/examples/`에 둔다.

## 충돌 방지 규칙

- 같은 파일을 동시에 크게 수정하지 않는다.
- 구조 변경 전 `project.md`에 기록한다.
- 문서 기준이 바뀌면 인덱스와 템플릿도 같이 갱신한다.

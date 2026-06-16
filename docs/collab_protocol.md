# collab_protocol.md

## 목적

이 문서는 이 저장소에서 작업 상태를 관리하고 문서 충돌을 줄이기 위한 공통 운영 규칙을 정의한다.

## 공통 문서 맵

- `project.md`: 현재 작업 현황, 상태, 최근 결정
- `AGENTS.md`: 모든 에이전트가 따라야 할 최소 규칙
- `README.md`: 전체 구조 인덱스
- `business_context.md`: 제품 목적과 범위
- `design.md`: 결과물 판단 기준
- `verification.md`: 검증/피드백 루프 정책
- `ARCHITECTURE.md`: 상위 구조와 변경 영향 포인트
- `docs/template.md`: 작업 등록과 작업 지시 템플릿
- `docs/modules/*.md`: 기능 또는 문서 묶음별 상세 설명

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

이 순서는 이 저장소의 단일 기준이다. 다른 문서에는 같은 내용을 반복해서 적지 않고 이 문서를 참조한다.

## 작업 운영 규칙

- 모든 작업은 `project.md`에 등록한다.
- 각 작업은 담당, 상태, 산출물, 비고를 가진다.
- 시작 전에 `todo`를 `in_progress`로 바꾼다.
- 구현 완료 후 검토가 필요하면 `review`로 바꾼다.
- 검증과 문서 반영까지 끝나야 `done`으로 바꾼다.
- 새 작업 시작 전 기존 작업과 파일 충돌 여부를 확인한다.

## 문서 분리 규칙

- `AGENTS.md`에는 최소 규칙만 둔다.
- 구조 설명은 `README.md`와 `ARCHITECTURE.md`로 보낸다.
- 현재 작업 지시는 `docs/template.md` 형식이나 `tasks/*` 문서에 둔다.
- 특정 도구 메모는 `CLAUDE.md` 같은 선택 파일로 분리할 수 있지만, 공통 규칙을 중복하지 않는다.

## 크기와 토큰 예산 규칙

- `AGENTS.md`는 50줄 안팎의 최소 규칙 문서로 유지한다.
- `README.md`는 인덱스와 운영 원칙 중심으로 유지하고, 상세 설명은 링크로 보낸다.
- 한 문서가 약 150줄을 넘거나 목적이 2개 이상 섞이면 분리 후보로 본다.
- 예시, 변경 이력, 장문 작업 메모는 본문에 누적하지 않고 `docs/examples/` 또는 `tasks/*`로 이동한다.

이 기준은 연구에서 직접 제시된 숫자가 아니라, 최소 고신호 컨텍스트를 유지하라는 최근 연구와 실무 가이드를 바탕으로 이 저장소에 맞게 정한 운영 규칙이다.

## context rot 대응 규칙

- `project.md`의 `done` 작업 중 30일 이상 지난 항목은 필요 시 `tasks/CHANGELOG_NOTES.md`나 별도 기록 문서로 옮긴다.
- `tasks/PROMPT.md`는 현재 작업만 유지하고, 끝난 작업 지시는 새 파일로 대체하거나 기록 문서로 이동한다.
- `docs/modules/*.md`는 실제 수정 진입점만 남기고 장문 회의 메모는 넣지 않는다.
- 오래된 예시는 템플릿 대체본처럼 보이지 않게 `docs/examples/` 아래에 분리한다.

## 충돌 방지 규칙

- 같은 파일을 동시에 크게 수정하지 않는다.
- 구조 변경 전에는 먼저 `project.md`에 기록한다.
- 문서 기준이 바뀌면 인덱스 문서와 템플릿을 같이 갱신한다.
- 로컬 설정, 도구별 개인 메모, 빌드 산출물은 기본적으로 Git 추적 대상에 포함하지 않는다.

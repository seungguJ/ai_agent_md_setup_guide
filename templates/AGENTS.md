# AGENTS.md

## 역할

이 문서는 이 프로젝트에서 작업하는 모든 AI 에이전트가 따라야 하는 공통 최소 규칙이다.

## 작업 원칙

1. 이 파일은 짧게 유지한다.
2. 구조 설명은 `README.md`와 `ARCHITECTURE.md`로 분리한다.
3. 현재 작업 지시는 `project.md` 또는 `tasks/*` 문서에 둔다.
4. 검증하지 않은 내용은 완료로 적지 않는다.
5. 구조가 바뀌면 템플릿과 인덱스도 같이 갱신한다.
6. 읽기 순서는 `docs/collab_protocol.md`를 단일 기준으로 사용한다.
7. 같은 실수가 반복되면 지시문 추가보다 `verification.md`의 검증 장치(테스트/린트/권한 축소)로 옮긴다.
8. 같은 시도를 반복해도 진전이 없으면(같은 에러, 같은 diff, 상태가 왔다갔다 함) 멈추고 막힌 지점을 보고한다. 무한 루프 방지 기준은 `verification.md`를 따른다.

## 크기 기준

- 이 파일은 가능하면 50줄 안팎을 유지한다.
- 한 문서가 약 150줄을 넘거나 목적이 섞이면 분리한다.

## 참조 문서

- `README.md`
- `project.md`
- `docs/collab_protocol.md`
- `docs/template.md`
- `verification.md`

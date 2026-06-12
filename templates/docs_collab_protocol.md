# collab_protocol.md

## 목적

여러 AI Agent가 같은 프로젝트를 다룰 때 충돌을 줄이고, 작업 인계와 리뷰를 일관되게 하기 위한 협업 규약이다.

이 문서에서 `Codex`는 관리자 역할 이름이다. 실제 운영에서는 GPT가 이 역할을 맡아도 된다.

## 공통 문서 맵

- `project.md`: 현재 작업 현황, 담당자, 상태, 최근 결정
- `AGENTS.md`: Codex 역할, 계획, 리뷰, 점검 방식
- `CLAUDE.md`: Claude 역할, 구현, 보고 방식
- `business_context.md`: 제품 목적, 우선순위, 기능 범위
- `design.md`: 화면 및 결과물 판단 기준
- `README.md`: 프로젝트 구조 인덱스
- `docs/modules/*.md`: 기능별 상세 문서
- `ARCHITECTURE.md`: 상위 설계 참고 문서
- `docs/template.md`: 작업 등록, 지시, 보고 템플릿

## 공통 작업 순서

1. `project.md`
2. `docs/collab_protocol.md`
3. 역할 문서 (`AGENTS.md` 또는 `CLAUDE.md`)
4. `business_context.md`
5. `design.md`
6. `README.md`
7. 관련 `docs/modules/*.md`
8. 필요 시 `ARCHITECTURE.md`
9. 실제 코드

## Level 1: 작업 운영

- 모든 작업은 `project.md`에 등록한다.
- 각 작업은 담당자, 상태, 산출물, 비고를 가진다.
- 시작 전에 `todo`에서 `in_progress`로 바꾼다.
- 구현 완료 후 `review`로 바꾸고 리뷰 요청을 남긴다.
- 검증과 문서 반영까지 끝나야 `done`으로 바꾼다.
- 새 작업 시작 전 기존 작업과 파일 충돌 여부를 확인한다.

## Level 2: 역할 분리

### Codex

- 요구사항 해석
- 작업 분해
- 우선순위 설정
- 리뷰
- 문서 정합성 관리

### Claude

- 기능 구현
- 코드 수정
- 테스트
- 버그 수정
- 결과 보고

관리자 Agent 이름만 다를 뿐 역할은 동일하다.

- GPT를 쓰면 `Codex = GPT`
- 다른 계획형 Agent를 쓰면 `Codex = 해당 Agent`

## Level 3: 인계 및 승인

1. Codex가 작업을 정의한다.
2. Claude가 구현 범위와 가정을 확인한다.
3. Claude가 구현 후 결과를 보고한다.
4. Codex가 리뷰하고 보완 요청 또는 승인한다.
5. 완료 시 `project.md`와 관련 문서를 갱신한다.

## Level 4: 실행 런타임

- 역할 정의만으로 자동 실행이 활성화되지는 않는다.
- 자동 호출은 `docs/agent_runtime.md`와 `scripts/claude_handoff.sh`를 기준으로 수행한다.
- Codex는 Claude 호출 전에 작업 지시 템플릿을 채운다.
- Claude 호출 결과는 `.claude/handoffs/`에 저장한다.
- 자동 호출 후에도 승인 권한은 Codex에 남는다.

## 충돌 방지 규칙

- 같은 파일을 동시에 크게 수정하지 않는다.
- 구조 변경 전에는 먼저 `project.md`에 기록한다.
- 문서 기준이 바뀌면 역할 문서와 컨텍스트 문서를 같이 갱신한다.
- 로컬 설정, Agent 로그, 빌드 산출물, 개인 계정 정보는 Git 추적 대상에 포함하지 않는다.

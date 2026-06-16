# Setup Steps

이 문서는 새 프로젝트에 AI 에이전트용 문서 체계를 세팅하는 절차다.

## 1. 기본 문서 만들기

프로젝트 루트에 아래 파일을 둔다.

```text
README.md
AGENTS.md
project.md
business_context.md
design.md
verification.md
ARCHITECTURE.md
docs/collab_protocol.md
docs/template.md
docs/modules/
tasks/
```

필요하면 아래 파일을 추가한다.

```text
CLAUDE.md
tasks/TODO.md
tasks/PROMPT.md
tasks/CHANGELOG_NOTES.md
```

## 2. 문서 역할 나누기

- `AGENTS.md`: 모든 에이전트가 지켜야 할 최소 규칙
- `README.md`: 사람과 에이전트가 함께 보는 인덱스
- `project.md`: 현재 작업 상태판
- `verification.md`: 검증/피드백 루프 정책
- `ARCHITECTURE.md`: 구조와 변경 영향 포인트
- `docs/modules/*.md`: 기능별 상세 설명
- `tasks/*`: 이번 작업에만 필요한 작업 문서

핵심은 한 문서에 모든 설명을 몰아넣지 않는 것이다.

## 3. 읽기 순서 고정하기

읽기 순서는 `docs/collab_protocol.md` 한 곳에만 적는다. 다른 문서에는 복제하지 말고 참조만 남긴다.

```text
1. project.md
2. docs/collab_protocol.md
3. AGENTS.md
4. business_context.md
5. design.md
6. verification.md
7. README.md
8. 관련 docs/modules/*.md
9. 필요 시 ARCHITECTURE.md
10. 실제 코드
```

## 4. project.md를 단일 상태판으로 만들기

`project.md`에는 아래 항목을 둔다.

- 목적
- 시작 전 참고 순서
- 상태 규칙
- 현재 작업 현황 표
- 최근 결정
- 꼭 체크해야 할 목록
- 다음 작업 작성 규칙
- 완료 정의

상태값은 단순하게 유지한다.

```text
todo
in_progress
review
blocked
done
```

## 5. 구조 문서 만들기

`ARCHITECTURE.md`와 `docs/modules/*.md`를 같이 만든다.

- `ARCHITECTURE.md`: 시스템 한 줄 요약, 모듈 맵, 상위 계층 구조, 핵심 흐름, 변경 영향 포인트
- `docs/modules/*.md`: 책임, 먼저 읽을 파일, 진입점, 수정 시 주의

이 두 문서가 있어야 에이전트가 구조를 매번 다시 추측하지 않는다.

## 6. 검증 루프 정의하기

문서(`AGENTS.md`, `docs/modules/*.md`)는 실수를 막는 feedforward 장치다. 그것만으로 부족한 부분은 feedback 장치, 즉 검증 루프로 보완한다.

`verification.md`에 아래를 정의한다.

- computational 체크: 테스트, 린트, 타입 체크처럼 빠르고 결정적인 확인
- inferential 체크: 코드 리뷰, LLM-as-judge처럼 느리지만 의미를 보는 확인
- 게이팅 시점: 통합 전에 끝낼 체크와 통합 후에만 돌릴 체크 구분
- 같은 실수가 반복되면 지시문을 늘리는 대신 린트 규칙, 테스트, 권한 축소 같은 실행 가능한 장치로 옮긴다는 규칙

개념은 `docs/modules/harness-engineering.md`를 참고한다.

## 7. 작업 지시 템플릿 고정하기

작업 문서에는 최소한 아래 항목을 포함한다.

```md
### 작업명

### 목적

### 변경 대상 파일

### 구현 요구사항

### 금지 사항

### 검증 방법

### 완료 조건

### 보고 형식
```

작업 지시는 파일 단위로 구체화한다. "전체 개선" 같은 넓은 표현은 피한다.

## 8. 문서 크기 기준 정하기

아래 기준은 저장소 운영 규칙으로 먼저 두는 것이 안전하다.

- `AGENTS.md`: 50줄 안팎
- 인덱스 문서: 150줄 안팎을 넘기면 분리 검토
- 한 문서에 목적이 2개 이상 섞이면 분리
- 완료된 작업 메모는 `tasks/CHANGELOG_NOTES.md`로 이동

## 9. 실제 예시 함께 두기

템플릿만 두지 말고 최소 1개의 채워진 예시를 같이 둔다.

- 예시 모듈 문서 1개
- 예시 작업 문서 1개
- 예시 상태판 또는 작업 기록 1개

## 10. 선택적 도구 메모 다루기

`CLAUDE.md` 같은 파일은 특정 도구가 자체적으로 읽는 경우에만 둔다.

- 공통 규칙은 `AGENTS.md`에 둔다.
- 도구별 명령어나 사용 팁만 선택 파일에 둔다.
- 역할 분리 문서처럼 운영하지 않는다.

## 11. Git 제외 규칙 정리하기

로컬 설정과 개인 메모는 기본적으로 Git에 올리지 않는다.

권장 제외 항목:

```gitignore
.claude/
.codex/
.env
local.properties
build/
dist/
node_modules/
```

## 12. 완료 기준

새 프로젝트 세팅이 끝났다고 보려면 아래를 만족해야 한다.

- `README.md`에 문서 인덱스가 있다.
- `AGENTS.md`가 짧고 명확하다.
- `ARCHITECTURE.md`에 모듈 맵과 핵심 흐름이 있다.
- `docs/modules/*.md`가 실제 핵심 기능 수를 반영한다.
- `project.md`에 현재 작업과 최근 결정이 있다.
- 작업 템플릿이 목적, 변경 대상, 검증 기준을 분리한다.
- `verification.md`에 computational/inferential 체크와 게이팅 시점이 구분되어 있다.

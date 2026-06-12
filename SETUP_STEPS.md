# Setup Steps

이 문서는 새 프로젝트에 AI Agent 문서 체계와 Codex-Claude 연결 흐름을 구축하는 절차다.

이 문서에서 `Codex`는 관리자 역할 이름이다. 실제로는 `GPT`, `ChatGPT`, `Claude Code` 등 문서 정리와 리뷰를 맡는 Agent로 바꿔도 된다.

## 1. 기본 문서 만들기

프로젝트 루트에 아래 파일을 둔다.

```text
AGENTS.md
CLAUDE.md
project.md
business_context.md
design.md
README.md
ARCHITECTURE.md
docs/collab_protocol.md
docs/template.md
docs/modules/
docs/handoffs/
```

처음부터 모든 문서를 길게 쓰지 않는다. 최소한 아래 정보만 채운다.

- 현재 프로젝트가 무엇인지
- 누가 어떤 역할을 맡는지
- 작업 상태를 어디에 기록하는지
- 작업 시작 전에 어떤 순서로 문서를 읽는지
- 완료 기준과 검증 기준이 무엇인지

## 2. 역할 나누기

참조 프로젝트의 핵심 역할 분리는 다음과 같다.

- Codex: 관리자, 작업 분해, 범위 통제, 리뷰, 문서 정합성 관리
- Claude: 실무자, 코드 구현, 테스트, 버그 수정, 결과 보고

다른 Agent를 쓰더라도 같은 원칙을 유지한다.

- 한 Agent가 작업을 정의한다.
- 다른 Agent가 구현한다.
- 정의한 Agent가 결과를 리뷰한다.
- 승인 전에는 자동 구현 결과를 그대로 완료 처리하지 않는다.

실무 권장 매핑:

- `GPT` 또는 `ChatGPT`: 관리자 역할
- `Claude`: 구현 역할
- 둘 다 가능하면 문서상 이름은 그대로 두고 역할만 치환한다.

## 3. 읽기 순서 고정하기

모든 Agent 문서에 공통 읽기 순서를 적는다.

```text
1. project.md
2. docs/collab_protocol.md
3. 본인 역할 문서
4. business_context.md
5. design.md
6. README.md
7. 관련 docs/modules/*.md
8. 필요 시 ARCHITECTURE.md
9. 실제 코드
```

이 순서의 목적은 작업 상태, 협업 규칙, 제품 목적, 코드 구조를 확인한 뒤 수정하게 만드는 것이다.

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

## 4-1. ARCHITECTURE.md와 모듈 문서를 같이 만든다

`project.md`가 현재 상태판이라면, `ARCHITECTURE.md`와 `docs/modules/*.md`는 수정 진입점 지도 역할을 한다.

- `ARCHITECTURE.md`: 시스템 한 줄 요약, 모듈 맵, 상위 계층 구조, 핵심 런타임 흐름, 변경 영향 포인트
- `docs/modules/*.md`: 기능별 책임, 먼저 읽을 파일, 진입점, 수정 시 주의

이 두 문서가 빠지면 GPT는 구조를 매번 새로 추측하게 된다.

## 5. 작업 지시 템플릿 고정하기

Claude 또는 구현 Agent에게 넘기는 작업에는 최소한 아래 항목을 포함한다.

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

작업 지시는 파일 단위로 구체화한다. "전체 개선" 같은 넓은 표현은 피하고, 변경 대상과 검증 방법을 먼저 좁힌다.

## 5-1. GPT bootstrap prompt를 같이 둔다

새 프로젝트를 처음 세팅할 때는 `bootstrap_prompt.md`를 프로젝트 루트에 두고 GPT에게 함께 제공한다.

목적:

- 템플릿만 복사한 뒤 비어 있는 문서를 실제 프로젝트 맥락으로 채우게 한다.
- `README.md`, `ARCHITECTURE.md`, `docs/modules/*.md`를 프로젝트 코드 기준으로 작성하게 만든다.
- 첫 `project.md` 작업 항목까지 등록하게 만든다.

## 6. 자동 연결 스크립트 붙이기

자동 연결을 쓰려면 아래 조건이 필요하다.

- `claude` CLI 설치
- CLI 인증 완료
- 프로젝트 루트에 `CLAUDE.md` 존재
- `docs/handoffs/*.md` 작업 지시 파일 존재
- `scripts/claude_handoff.sh` 실행 가능

실행 예시:

```bash
scripts/claude_handoff.sh --task-file docs/handoffs/connectivity-check.md
scripts/claude_handoff.sh --task-file docs/handoffs/p001-example.md --label p001
scripts/claude_handoff.sh --task-file docs/handoffs/p001-example.md --timeout-seconds 900
```

## 7. 연결 확인 작업 만들기

첫 handoff는 코드 수정 없는 연결 확인으로 시작한다.

```md
### 작업명

Claude 연결 확인

### 목적

Codex에서 handoff 스크립트를 통해 Claude CLI와 통신 가능한지 확인한다.

### 변경 대상 파일

- 없음

### 구현 요구사항

- 코드 수정 없이 짧은 한국어 응답만 반환한다.
- 응답에는 `연결 확인 완료` 문구를 포함한다.

### 금지 사항

- 프로젝트 파일 수정 금지

### 검증 방법

- 스크립트가 성공 종료될 것
- `.claude/handoffs/`에 prompt, response, meta 파일이 생성될 것

### 완료 조건

- Claude 응답을 수신하고 저장 경로를 확인한다.

### 보고 형식

- 수정 파일
- 주요 변경 내용
- 검증 내용
- 남은 리스크
```

실제 확인 포인트:

- 성공 시 response 파일에는 Claude 응답 본문만 남는다.
- `Saved prompt to ...`, `Saved response to ...`, `Saved metadata to ...`는 콘솔 출력이므로 response 파일에서 찾지 않는다.
- 검증 스크립트나 수동 확인 시에는 `meta.txt`의 경로 정보와 response 본문을 분리해 확인한다.

## 8. 첫 실제 작업 운영하기

첫 실제 작업은 아래 조건을 만족하는 작은 작업이 좋다.

- 변경 파일 1~3개
- 테스트 또는 정적 검증 가능
- 되돌리기 쉬운 변경
- 문서와 코드의 연결을 확인할 수 있는 작업

완료 후 Codex는 Claude 보고를 그대로 받아들이지 말고 아래를 확인한다.

- 요구사항 반영 여부
- 회귀 가능성
- 검증 결과
- 문서 갱신 필요 여부
- 사용자 기존 변경 충돌 여부

## 9. Git 제외 규칙 정리하기

자동 Agent 로그와 로컬 정보는 기본적으로 Git에 올리지 않는다.

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

프로젝트 성격에 따라 빌드 산출물, 모델 파일, 개인 설정 파일을 추가한다.

## 10. 완료 기준

새 프로젝트 세팅이 끝났다고 보려면 아래를 만족해야 한다.

- `README.md`에 요구사항별 진입 문서와 핵심 파일 표가 있다.
- `ARCHITECTURE.md`에 모듈 맵과 핵심 흐름이 있다.
- `docs/modules/*.md`가 실제 핵심 기능 수를 반영한다.
- `project.md`에 현재 작업과 최근 결정이 있다.
- `AGENTS.md`를 읽은 GPT가 관리자 역할을 바로 수행할 수 있다.
- Claude 자동 인계를 쓸 경우 `docs/agent_runtime.md`와 `scripts/claude_handoff.sh`가 함께 존재한다.
- 연결 확인 handoff가 실제로 `0` 종료 코드와 `.claude/handoffs/*.prompt.md`, `*.response.md`, `*.meta.txt` 생성을 보여준다.

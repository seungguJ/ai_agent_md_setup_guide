# AI Agent MD Setup Guide

이 폴더는 다른 프로젝트에 AI Agent용 Markdown 문서와 자동 인계 구조를 구축하기 위한 가이드다.

이 가이드에서 `Codex`는 관리자 역할 이름이다. 실제 운영에서는 `GPT`, `ChatGPT`, `Claude Code`, 다른 계획형 Agent로 치환해도 된다. 중요한 것은 제품 맥락과 작업 범위를 정리하는 관리자 역할과, 구현과 검증을 수행하는 실무자 역할을 분리하는 점이다.

## 목표

- 프로젝트 안에서 AI Agent의 역할과 책임을 명확히 나눈다.
- 작업 상태, 제품 맥락, 설계 맥락, 모듈 문서를 분리해 관리한다.
- Codex가 작업을 정의하고 Claude가 구현하는 인계 흐름을 문서와 스크립트로 연결한다.
- 자동 호출 결과를 로그로 남겨 추적 가능하게 만든다.

## 핵심 구조

권장 구조는 아래와 같다.

```text
.
├── AGENTS.md
├── CLAUDE.md
├── project.md
├── business_context.md
├── design.md
├── README.md
├── ARCHITECTURE.md
├── docs/
│   ├── agent_runtime.md
│   ├── collab_protocol.md
│   ├── template.md
│   ├── handoffs/
│   └── modules/
└── scripts/
    └── claude_handoff.sh
```

핵심은 역할 문서만 두는 것이 아니라, `project.md`를 현재 상태의 기준점으로 삼고 `docs/collab_protocol.md`, `docs/template.md`, `docs/agent_runtime.md`, `scripts/claude_handoff.sh`를 통해 실제 작업 인계까지 연결하는 것이다.

## 권장 파일 세트

최소 구성:

- `AGENTS.md`: Codex 또는 관리자 Agent의 역할, 읽기 순서, 리뷰 기준
- `CLAUDE.md`: Claude 또는 구현 Agent의 역할, 구현 원칙, 보고 형식
- `project.md`: 작업 현황판, 상태 규칙, 최근 결정
- `docs/collab_protocol.md`: 여러 Agent가 같은 프로젝트를 다룰 때의 협업 규칙
- `docs/template.md`: 작업 등록, 작업 지시, 보고, 리뷰 템플릿

자동 연결까지 필요한 구성:

- `docs/agent_runtime.md`: 자동 호출 규칙, 입력/출력 계약, 로그 정책
- `scripts/claude_handoff.sh`: Claude CLI 호출 스크립트
- `docs/handoffs/*.md`: Claude에게 넘길 작업 지시 파일
- `.claude/handoffs/`: 실행된 prompt, response, meta 로그 저장 위치

프로젝트 이해도를 높이는 구성:

- `business_context.md`: 제품 목적, 사용자, 우선순위, 범위 밖 항목
- `design.md`: UI/UX 또는 결과물 판단 기준
- `README.md`: 프로젝트 구조 인덱스와 요구사항별 진입점
- `ARCHITECTURE.md`: 큰 설계와 데이터/모듈 흐름
- `docs/modules/*.md`: 기능 또는 모듈별 상세 문서
- `bootstrap_prompt.md`: GPT 같은 관리자 Agent에게 첫 세팅을 맡길 때 쓰는 시작 프롬프트

## Agent 연결 방식

권장 흐름은 아래와 같다.

1. 사용자가 Codex에게 요구사항을 전달한다.
2. Codex가 `project.md`와 관련 문서를 읽고 작업 범위를 좁힌다.
3. Codex가 `docs/handoffs/<task>.md`에 작업 지시를 작성한다.
4. Codex가 `scripts/claude_handoff.sh --task-file docs/handoffs/<task>.md`를 실행한다.
5. 스크립트가 `CLAUDE.md`를 system prompt에 붙이고 작업 지시를 Claude CLI에 전달한다.
6. Claude가 구현 또는 검토 결과를 보고한다.
7. 스크립트가 `.claude/handoffs/`에 prompt, response, meta 파일을 저장한다.
8. Codex가 Claude 결과를 리뷰하고 승인, 보완 요청, 직접 수정 중 하나를 결정한다.
9. 완료 시 `project.md`와 관련 문서를 갱신한다.

## 적용 순서

1. 새 프로젝트 루트에 `templates/`의 파일들을 복사한다.
2. 프로젝트명, 기술 스택, 제품 목적, 모듈명을 실제 프로젝트에 맞게 바꾼다.
3. `README.md`에는 전체 구조와 요구사항별 진입 문서를 적는다.
4. `project.md`에는 현재 작업과 최근 결정을 등록한다.
5. `ARCHITECTURE.md`에 상위 계층, 데이터 흐름, 변경 영향 포인트를 적는다.
6. `docs/modules/`에는 기능별 문서를 하나씩 추가한다.
7. GPT를 관리자 역할로 쓸 경우 `bootstrap_prompt.md`를 초기 프롬프트로 사용해 프로젝트 문서 초안을 생성한다.
8. 자동 연결이 필요하면 `scripts/claude_handoff.sh`를 복사하고 실행 권한을 준다.
9. `claude` CLI 인증 후 연결 확인 handoff를 실행한다.
10. 첫 실제 작업은 작은 파일 범위로 제한해 검증한다.

## 템플릿 복사 위치

| 이 폴더의 파일 | 새 프로젝트 위치 |
|---|---|
| `templates/AGENTS.md` | `AGENTS.md` |
| `templates/CLAUDE.md` | `CLAUDE.md` |
| `templates/project.md` | `project.md` |
| `templates/ARCHITECTURE.md` | `ARCHITECTURE.md` |
| `templates/business_context.md` | `business_context.md` |
| `templates/design.md` | `design.md` |
| `templates/docs_collab_protocol.md` | `docs/collab_protocol.md` |
| `templates/docs_template.md` | `docs/template.md` |
| `templates/docs_agent_runtime.md` | `docs/agent_runtime.md` |
| `templates/module.md` | `docs/modules/<module-name>.md` |
| `templates/handoff_connectivity_check.md` | `docs/handoffs/connectivity-check.md` |
| `templates/bootstrap_prompt.md` | `bootstrap_prompt.md` |
| `scripts/claude_handoff.sh` | `scripts/claude_handoff.sh` |

## GPT로 바로 세팅할 때

새 프로젝트에 아래 파일을 먼저 복사한다.

- `AGENTS.md`
- `CLAUDE.md`
- `project.md`
- `ARCHITECTURE.md`
- `business_context.md`
- `design.md`
- `docs/collab_protocol.md`
- `docs/template.md`
- `docs/agent_runtime.md`
- `docs/modules/<module-name>.md`
- `bootstrap_prompt.md`

그다음 GPT에게 최소한 아래 입력을 함께 준다.

- 현재 프로젝트 루트 경로
- 기술 스택
- 제품 목적 한 줄
- 핵심 기능 3~7개
- 제외할 범위
- 이미 있는 코드 또는 폴더 구조

이 정보와 `bootstrap_prompt.md`만 있으면 GPT가 문서 초안, 모듈 분리, 첫 `project.md` 작업 등록까지 한 번에 만들 수 있게 구성하는 것이 목표다.

## 검증된 Claude handoff 예시

이 저장소에서는 2026-06-12에 아래 실제 실행으로 Claude 연결 확인을 검증했다.

```bash
bash scripts/claude_handoff.sh --task-file docs/handoffs/connectivity-check.md --label live-connectivity-check --timeout-seconds 180
```

검증 결과:

- 종료 코드 `0`
- `.claude/handoffs/20260612-225638-live-connectivity-check.prompt.md` 생성
- `.claude/handoffs/20260612-225638-live-connectivity-check.response.md` 생성
- `.claude/handoffs/20260612-225638-live-connectivity-check.meta.txt` 생성
- response 파일에 `연결 확인 완료` 포함

실동작 주의:

- response 파일에는 Claude 응답 본문만 저장된다.
- `Saved prompt to ...` 같은 저장 경로 안내는 스크립트 콘솔 출력에만 나타난다.
- 따라서 자동 검증은 response 파일 내용과 파일 존재 여부를 나눠서 확인하는 편이 안전하다.

## 검증 기준

- 새 Agent가 작업 시작 전에 읽어야 할 문서 순서를 알 수 있어야 한다.
- 현재 작업 상태는 `project.md`만 보면 판단 가능해야 한다.
- `ARCHITECTURE.md`와 `docs/modules/*.md`만 읽어도 어디를 먼저 수정해야 할지 좁힐 수 있어야 한다.
- Claude에게 넘기는 작업 지시는 목적, 변경 파일, 금지 사항, 검증 방법, 완료 조건을 포함해야 한다.
- 자동 호출을 쓰는 경우 `.claude/handoffs/`에 실행 로그가 남아야 한다.
- 완료 처리는 구현, 검증, 문서 반영 근거가 있을 때만 해야 한다.

## 주의사항

- 역할 문서만 만들었다고 Agent가 자동 연결되는 것은 아니다.
- 자동 연결은 CLI, 인증, 실행 스크립트, 로그 저장 정책이 함께 있어야 한다.
- 한 번에 넓은 범위를 Claude에게 넘기면 리뷰 비용과 충돌 위험이 커진다.
- `.claude/`, `.codex/`, 로컬 설정, 인증 정보, 빌드 산출물은 Git 추적 대상에서 제외하는 것이 안전하다.
- 기존 사용자 변경이 있는 파일은 자동 구현 전에 충돌 가능성을 먼저 확인한다.

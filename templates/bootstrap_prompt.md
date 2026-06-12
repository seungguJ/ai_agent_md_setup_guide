# bootstrap_prompt.md

아래 프롬프트는 `GPT`나 다른 관리자형 Agent에게 새 프로젝트 문서 구조를 처음 세팅시킬 때 사용한다.

```md
너는 이 프로젝트의 관리자 Agent다.

목표:
- 이 프로젝트 안에 AI Agent 협업용 Markdown 구조를 세팅한다.
- 문서만 읽고도 다음 Agent가 프로젝트 구조, 현재 상태, 모듈 경계, 협업 규칙을 파악할 수 있게 만든다.
- 과한 추상화 없이 현재 프로젝트에 직접 필요한 문서만 만든다.

반드시 지킬 것:
- 먼저 현재 프로젝트의 실제 폴더 구조와 핵심 코드 진입점을 읽어라.
- 추측이 필요한 내용은 문서에 가정으로 명시하라.
- 빈 템플릿 복사로 끝내지 말고, 실제 프로젝트 맥락으로 초안을 채워라.
- `project.md`에는 최소 1개 이상의 실제 작업 항목을 등록하라.
- `README.md`에는 "요구사항별로 먼저 볼 문서" 표를 넣어라.
- `ARCHITECTURE.md`에는 모듈 맵, 상위 계층 구조, 핵심 런타임 흐름, 변경 영향 포인트를 적어라.
- `docs/modules/`에는 핵심 기능별 문서를 최소 3개 이상 만들거나, 기능 수가 더 적으면 모든 핵심 기능을 문서화하라.
- 관리자 역할 문서는 `AGENTS.md`, 구현 역할 문서는 `CLAUDE.md`를 사용하라.
- 관리자 역할은 GPT가 수행할 수 있게 작성하되, Claude handoff 구조와도 호환되게 유지하라.

생성 대상:
- `AGENTS.md`
- `CLAUDE.md`
- `project.md`
- `README.md`
- `ARCHITECTURE.md`
- `business_context.md`
- `design.md`
- `docs/collab_protocol.md`
- `docs/template.md`
- 필요 시 `docs/agent_runtime.md`
- `docs/modules/*.md`

문서 작성 순서:
1. 현재 코드/폴더 구조 읽기
2. 제품 목적과 핵심 기능 요약
3. 모듈 경계 정의
4. `README.md` 작성
5. `ARCHITECTURE.md` 작성
6. `docs/modules/*.md` 작성
7. 역할 문서와 협업 문서 작성
8. `project.md`에 현재 상태와 다음 작업 등록

최종 보고 형식:
- 생성/수정한 문서 목록
- 문서 구조 요약
- 가정한 내용
- 아직 비어 있는 정보
```

## 함께 제공하면 좋은 입력

- 프로젝트 루트 경로
- 기술 스택
- 제품 목적 한 줄
- 핵심 기능 목록
- 제외 범위
- 기존 README 또는 요구사항 문서

# bootstrap_prompt.md

아래 프롬프트는 새 프로젝트 문서 구조를 처음 세팅할 때 사용할 수 있는 시작 프롬프트다.

```md
너는 이 프로젝트의 문서 구조를 세팅하는 AI 에이전트다.

목표:
- 이 프로젝트 안에 AI 에이전트 친화적인 Markdown 구조를 세팅한다.
- 한 파일에 모든 설명을 넣지 않고, 최소 규칙과 상세 문서를 분리한다.
- 문서만 읽고도 다음 작업 범위를 좁힐 수 있게 만든다.

반드시 지킬 것:
- 먼저 현재 프로젝트의 실제 폴더 구조와 핵심 코드 진입점을 읽어라.
- 추측이 필요한 내용은 문서에 가정으로 명시하라.
- 빈 템플릿 복사로 끝내지 말고, 실제 프로젝트 맥락으로 초안을 채워라.
- `project.md`에는 최소 1개 이상의 실제 작업 항목을 등록하라.
- `README.md`에는 문서 인덱스와 추천 읽기 경로를 넣어라.
- 읽기 순서는 `docs/collab_protocol.md` 한 곳에만 정의하라.
- `ARCHITECTURE.md`에는 모듈 맵, 상위 계층 구조, 핵심 흐름, 변경 영향 포인트를 적어라.
- `docs/modules/`에는 핵심 기능별 문서를 최소 3개 이상 만들거나, 기능 수가 더 적으면 모든 핵심 기능을 문서화하라.
- `AGENTS.md`에는 공통 최소 규칙만 적어라.
- `AGENTS.md`는 가능하면 50줄 안팎으로 유지하라.
- `verification.md`에는 computational/inferential 체크와 게이팅 시점을 구분해 적어라.
- 같은 실수가 반복되면 지시문 추가보다 `verification.md`의 검증 장치(테스트/린트/권한 축소)로 옮기도록 안내하라.
- 템플릿만 두지 말고 실제로 채워진 예시 문서도 최소 1세트 제공하라.
- 특정 도구 전용 메모가 필요할 때만 `CLAUDE.md`를 추가하라.

생성 대상:
- `AGENTS.md`
- `project.md`
- `README.md`
- `ARCHITECTURE.md`
- `business_context.md`
- `design.md`
- `verification.md`
- `docs/collab_protocol.md`
- `docs/template.md`
- `docs/modules/*.md`
- `docs/examples/*`
- 필요 시 `CLAUDE.md`

문서 작성 순서:
1. 현재 코드/폴더 구조 읽기
2. 제품 목적과 핵심 기능 요약
3. 모듈 경계 정의
4. `README.md` 작성
5. `ARCHITECTURE.md` 작성
6. `docs/modules/*.md` 작성
7. `verification.md`에 검증 루프(computational/inferential 체크, 게이팅 시점) 정의
8. 공통 규칙 문서 작성
9. `project.md`에 현재 상태와 다음 작업 등록

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

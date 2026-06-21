# Harness Engineering Module

## 책임

- "harness engineering" 개념을 이 저장소의 문서 구조에 연결
- 이 가이드가 다루는 영역(문서·컨텍스트)과 다루지 않는 영역(도구 권한, observability)을 구분
- 반복되는 에이전트 실수를 문서가 아니라 검증 장치로 옮기는 기준 제공

## 핵심 개념

- Harness = 모델을 둘러싼 모든 장치(컨텍스트/메모리, 도구, 검증 루프, 권한, observability). 모델 자체보다 harness 품질이 결과를 더 많이 결정한다.
- Guides(feedforward): 실수가 나기 전에 막는 장치. 이 저장소의 `AGENTS.md`, `CLAUDE.md`, `docs/modules/*.md`가 여기 속한다.
- Sensors(feedback): 결과가 나온 뒤 확인하고 고치게 하는 장치. 테스트·린트처럼 빠르고 결정적인 computational 체크와, 코드 리뷰·LLM-as-judge처럼 느리지만 의미를 보는 inferential 체크로 나뉜다.
- 같은 실수가 반복되면 지시문을 더 적기보다, 그 실수를 다시 못 하게 막는 실행 가능한 장치(린트 규칙, 테스트, 권한 축소)로 옮긴다. 이 저장소는 이 판단을 `verification.md`에 기록하도록 안내한다.
- Loop(반복 종료 조건): 에이전트의 작업 루프 자체에도 멈춤 조건이 있어야 한다. 같은 에러·같은 diff·같은 실패가 반복되는데도 멈추지 않으면 harness가 아니라 무한 루프가 된다. 이 저장소는 이 조건을 `verification.md`의 "무한 루프 방지" 절에 둔다.

## 이 저장소가 다루는 레이어 / 다루지 않는 레이어

| Harness 레이어 | 이 저장소의 대응 문서 | 비고 |
|---|---|---|
| Context / Memory (feedforward) | `AGENTS.md`, `CLAUDE.md`, `project.md`, `docs/modules/*.md` | 이 가이드가 다루는 핵심 영역 |
| 검증 루프 (feedback, computational/inferential) | `verification.md` | 정책만 정의하고, 실제 실행은 각 프로젝트의 테스트/린트/CI에 위임 |
| Agent Loop / 반복 종료 조건 (feedback) | `verification.md`의 "무한 루프 방지" | 최대 반복 횟수, 무진전 감지, 멈춤 시 보고 방식을 정의 |
| 도구·권한 범위 (guardrails) | 다루지 않음 | Claude Code `settings.json`, MCP 권한 설정 등 도구별 설정에서 다룬다 |
| Skills / 재사용 워크플로 (guides) | 다루지 않음 | SKILL.md·slash command 묶음. 도구별로 별도 설치·등록해야 동작한다. 아래 "범위 밖 참고" 참조 |
| Observability | 다루지 않음 | 로깅/트레이싱은 런타임별 설정에서 다룬다 |

## 범위 밖 참고: Skills와 공급망 검증

아래는 다른 harness 레이어에 속하고 모두 **별도 설치·등록이 필요한 도구/스킬**이다. 이 저장소(문서 구조)에 코드로 통합하지 않고, 어떤 레이어인지만 매핑한다.

- 재사용 워크플로(Skills): SKILL.md 형식의 워크플로와 slash command 묶음. 도구마다 별도 등록이 필요하다(예: Claude Code는 플러그인 마켓플레이스 등록, Gemini CLI는 skills install). 이 저장소의 문서 규칙은 이런 스킬을 만들 때의 작성 원칙으로 재사용할 수 있다. 참고: https://github.com/addyosmani/agent-skills
- 스킬 공급망 보안(guardrails): 외부 스킬은 프롬프트 인젝션·데이터 유출 같은 패턴을 포함할 수 있어, 설치 전 점검이 필요하다. 참고: NVIDIA SkillSpector — https://github.com/NVIDIA/SkillSpector
- 코드베이스 지식 그래프(observability/context tooling): 저장소를 그래프로 만들어 질의하는 별도 도구. 설치 후 slash command로 호출한다. 참고: safishamsi/graphify — https://github.com/safishamsi/graphify

## 먼저 읽을 파일

- `README.md`의 "Harness Engineering 관점" 절
- `verification.md`

## 진입점

- 새 프로젝트에 검증 루프나 권한 정책을 명시해야 할 때
- "문서만 늘었는데 같은 실수가 반복된다"는 신호가 보여 feedback 장치로 옮길지 판단할 때
- 에이전트가 같은 수정을 반복하거나 진전 없이 도는 신호가 보일 때

## 수정 시 주의

- 이 문서는 개념 설명과 레이어 매핑만 유지한다. 특정 CI 문법이나 도구별 설정 방법은 적지 않는다.
- 레이어 매핑이 바뀌면 `README.md`의 "Harness Engineering 관점" 절도 같이 갱신한다.

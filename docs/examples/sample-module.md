# Sample Module Document

## 책임

- 사용자 인증 화면과 로그인 요청 흐름 관리
- 세션 복구와 로그아웃 진입점 제공
- 권한 정책 자체의 정의는 담당하지 않음

## 먼저 읽을 파일

- `frontend/src/features/auth/LoginPage.tsx`
- `frontend/src/features/auth/useAuthSession.ts`
- `backend/src/auth/auth_service.py`

## 이 모듈이 가진 상태

- 현재 로그인 사용자
- 액세스 토큰 만료 상태
- 로그인 실패 메시지

## 진입점

- 사용자 진입점: `/login`
- API 진입점: `POST /api/login`
- 백그라운드 진입점: 앱 시작 시 세션 복구

## 요구사항별로 볼 위치

| 요구사항 | 볼 파일/함수 |
|---|---|
| 로그인 버튼 UX 수정 | `LoginPage.tsx` |
| 세션 복구 실패 처리 | `useAuthSession.ts` |
| 비밀번호 검증 규칙 수정 | `auth_service.py` |

## 수정 시 주의

- 로그인 성공 후 리다이렉트 경로와 권한 체크 로직을 같이 확인한다.
- 에러 메시지를 바꾸면 프론트와 백엔드 응답 형식이 함께 맞는지 본다.
- 세션 관련 변경은 만료, 재로그인, 로그아웃까지 한 흐름으로 검증한다.

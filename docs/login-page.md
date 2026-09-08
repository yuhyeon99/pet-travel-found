# Login Page (/auth/login)

- 위치: `src/pages/AuthPage/Login/index.jsx`; 공통 폼 래퍼 `AuthForm` 사용.
- 입력 필드: 이메일, 비밀번호. `useState`로 관리.
- 제출 동작: `login` 서비스 호출 → 성공 시 알림 후 `/`로 이동, 실패 시 오류 메시지 알림.
- 인증 저장: `authService.login`이 로컬스토리지 사용자 목록과 해시된 비밀번호를 검증하고 세션 스토리지에 로그인 상태/유저 정보 저장.
- 링크: 하단 링크로 회원가입 이동(`/auth/register`).
- 주의사항: 네이티브 `alert` 사용; UX 개선 시 토스트/폼 검증 추가 고려.

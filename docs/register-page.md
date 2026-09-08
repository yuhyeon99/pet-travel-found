# Register Page (/auth/register)

- 위치: `src/pages/AuthPage/Register/index.jsx`; `AuthForm` 래퍼 재사용.
- 입력 필드: 이름, 이메일, 비밀번호. `useState`로 관리.
- 제출 동작: `setUser` 서비스 호출 → 성공 시 알림 후 `/auth/login`으로 리다이렉트, 실패 시 오류 메시지 알림.
- 저장 로직: `authService.setUser`가 비밀번호를 SHA-256으로 해싱 후 로컬스토리지 `user` 배열에 저장, 중복 이메일 검사 포함.
- 링크: 하단 링크로 로그인 이동(`/auth/login`).
- 주의사항: 서버 없이 로컬스토리지에 사용자 정보 저장하므로 프로덕션 보안 요구에는 미흡; 추후 API 연동 필요.

# Auth Page (/auth)

- 위치: `src/pages/AuthPage/index.jsx` (레이아웃), 자식 경로 `/auth/login`, `/auth/register`는 Outlet으로 렌더.
- 목적: 로그인/회원가입 화면을 공통 컨테이너로 감싸 중앙 정렬 및 스타일 일관성 확보.
- 데이터 흐름: 자체 상태 없음, 자식 폼에서 전달받은 `onSubmit` 처리만 수행.
- 주요 컴포넌트: `Outlet`, 스타일 `AuthPage.module.css`.
- 네비게이션: 상위 라우트 `/auth` 진입 시 기본으로 로그인(`index` -> `/auth/login`).

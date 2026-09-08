# Booking Page (/booking)

- 위치: `src/pages/BookingPage/index.jsx`.
- 접근 제어: 마운트 시 `isAuthenticated()` 확인, 비로그인 시 알림 후 `/auth/login`으로 이동.
- 입력: 체크인/체크아웃 날짜, 인원(1~10). `verifyCheckIn/verifyCheckOut/verifyHeadCount`로 유효성 검사 및 경고.
- 전달 데이터: `useLocation().state`에서 받은 `name`, `address`를 표시; 상세에서 전달되지 않으면 `undefined` 가능.
- 주요 동작: `결제하기` 클릭 시 필수 날짜 체크 → `/payment`로 `name`, `address`, `checkIn`, `checkOut`, `headCount`, `price:"120000"`를 state로 전달.
- UI: 좌측 예약 폼 + CTA, 우측 장식 이미지. 가격·숙박비 계산은 Payment 페이지에서 수행.
- 주의사항: 현재 가격 하드코딩, 날짜 비교 시 `new Date()` 사용으로 오늘 이전 선택 차단.

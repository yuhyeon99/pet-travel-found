# Payment Page (/payment)

- 위치: `src/pages/PaymentPage/index.jsx`.
- 접근 제어: 마운트 시 `isAuthenticated()` 검사, 미로그인 시 알림 후 `/auth/login` 이동.
- 진입 데이터: `/booking`에서 state로 전달된 `name`, `address`, `checkIn`, `checkOut`, `headCount`, `price`를 사용.
- 금액 계산: `stayDuration = (checkOut - checkIn)` 일수, `totalPrice = price * stayDuration`(문자→Number 변환 후 locale string). 1박 요금도 `price`에서 표시.
- 결제 폼: 카드번호(숫자 그룹핑), 유효기간(MM/YY 포맷), CVV(최대 3자리), 카드 소유자명. 입력 포맷팅 로직 포함.
- 결제 처리: `handlePayment`가 `setPayment` 호출 → 민감 정보는 SHA-256 해싱 후 로컬스토리지 `payment` 배열에 저장, 세션의 사용자 이름/이메일을 함께 기록.
- 후속 동작: 성공/실패 알림 후 `/my`로 이동.
- 의존성: `Button`, `getImage`, `payService`, 스타일 `PaymentPage.module.css`.

# Detail Page (/detail)

- 위치: `src/pages/DetailPage/index.jsx`.
- 진입 데이터: `/list` → `PlaceItem`에서 `navigate`로 전달한 state(thumbnail, name, score, address, shortIntro, options, price). 전달 누락 시 기본값으로 안전 처리.
- 주요 UI: 좌측 썸네일+기본 정보(주소, 평점, 설명), 우측 예약 패널(가격/1박 + `예약하기` 버튼), 하단 편의시설 아이콘 리스트.
- 동작: `예약하기` 클릭 시 `navigate('/booking', { state: safeState })`로 예약 화면에 동일 payload 전달.
- 이미지: 전달된 thumbnail 없으면 `/src/assets/images/no-photo.png`를 사용(추후 실제 이미지 URL로 대체 예정).
- 의존성: `Icon`, `Button`, `getImage`, 스타일 `DetailPage.module.css`.

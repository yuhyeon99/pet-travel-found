# Main Page (/)

- 위치: `src/pages/MainPage/index.jsx`
- 목적: 랜딩 페이지로 브랜드 소개 및 주요 가치 제시, 검색 리스트로 이동하는 진입점 제공.
- 주요 섹션: 히어로(카피+CTA 두 개), 소개 영역(`#info`), 특징 4가지 카드.
- 상호작용: `지금 시작하기` 버튼은 `location.href = "/list"`; `더 알아보기`는 페이지 내 `#info` 앵커로 스크롤.
- 데이터/상태: 로컬 상태 및 외부 데이터 없음. 정적 텍스트·이미지(`getImage`)와 `Icon` 컴포넌트 사용.
- 의존성: `Button`, `Icon`, `getImage`, 스타일 `MainPage.module.css`.
- 주의사항: 버튼 이동이 `location.href` 기반이라 SPA 내비게이션 효과를 원하면 `useNavigate`로 교체 검토.

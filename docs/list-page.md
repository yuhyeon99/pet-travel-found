# List Page (/list)

- 위치: `src/pages/ListPage/index.jsx`.
- 역할: 검색 필터 UI와 결과 목록을 보여줌.
- 초기 상태: `useLocation().state`에서 `searchKeyword`, `searchLocation`을 받아 기본값 "펜션"/빈 문자열을 전달.
- 주요 컴포넌트
  - `Search`: 카테고리 텍스트 입력, 지역 드롭다운(전체/제주/포항/평창/부산). `navigate('/list', { state })`로 동일 경로 재요청.
  - `PlaceList`: `getPlaceList` 서비스로 공공데이터 API 호출 후 결과를 리스트로 렌더. 실패 시 콘솔 로그 후 빈 배열.
  - `PlaceItem`: 썸네일·이름·주소·옵션 등 표시, 위시리스트 토글(로컬 상태), `상세보기` 클릭 시 `/detail`로 state 전달.
- 데이터 의존성: 환경변수 `VITE_PET_PLACE_API_KEY`, `VITE_PET_PLACE_API_URL` 필요. 미설정 시 예외 발생.
- 기타: 가격/평점은 현재 하드코딩(120,000원, 4.8). 주소에서 도시명 추출해 카드 상단 위치로 사용.

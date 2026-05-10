
## 🚀 주요 기능 및 세부 구현 (Key Features & Implementation)

### 1. 사용자 인증 및 보안 (Authentication)
- **JWT 기반 로그인**: 사용자가 아이디와 비밀번호를 입력하면 백엔드(`http://localhost:8080/login`)와 통신하여 인증을 수행합니다.
- **토큰 관리**: 응답 헤더로 전달받은 Access Token에서 `Bearer ` 접두사를 제거한 후, 보안을 고려해 쿠키(Cookie)에 `secure` 옵션과 함께 저장합니다.
- **사용자 경험(UX)**: 로그인 통신 중에는 `ShapeLoading` 컴포넌트를 통해 로딩 상태를 시각적으로 제공하여 대기 시간을 자연스럽게 처리합니다. 성공적으로 로그인하면 세계 지도(`/map`) 페이지로 자동 리다이렉트됩니다.

### 2. 인터랙티브 세계 지도 (Interactive World Map)
- **지도 시각화**: `@amcharts/amcharts4` 라이브러리와 `worldLow` 지리 데이터를 활용하여 밀러(Miller) 도법 기반의 3D 세계 지도를 렌더링합니다.
- **인터랙션 및 애니메이션**: 
  - 국가(Polygon)에 마우스를 올리면 색상이 변하는 호버(Hover) 액션과 툴팁이 제공됩니다.
  - 특정 국가 클릭 시 해당 오브젝트로 부드럽게 줌인(Zoom-in)되며, 시각적 하이라이트 처리가 적용됩니다.
- **국가별 라우팅**: 국가 클릭 후 1.5초의 딜레이 애니메이션 이후, 선택된 국가 이름을 소문자로 변환해 쿼리 파라미터(`?nation=...`)로 담아 메인 대시보드(`/main`)로 이동합니다.

### 3. 커뮤니티 시스템 (Community Board)
- **데이터 연동**: `Fetch API`를 사용하여 백엔드(`http://localhost:8080/api/community/allcommunity`)로부터 게시글 목록을 불러옵니다.
- **데이터 처리**: 받아온 원본 데이터를 클라이언트에서 필요한 형태(작성일자 포맷팅, 필드명 매핑 등)로 가공하여 렌더링합니다. 목록은 최신순으로 정렬(Reverse)되어 표시됩니다.
- **페이지네이션(Pagination)**: `react-js-pagination` 라이브러리를 활용하여 한 페이지당 5개의 게시글만 보이도록 효율적으로 클라이언트 사이드 페이징을 구현했습니다.
- **게시글 이동**: 리스트에서 특정 게시물의 제목을 클릭하면, `React Router`의 `state`를 통해 해당 게시물의 상세 데이터 객체를 함께 전달하며 상세 페이지(`/boarddetail`)로 이동합니다.

## 🛠 기술 스택 (Tech Stack)

### Frontend Core
- **React**: v18.3.1
- **React Router DOM**: v7.0.2 (페이지 라우팅 및 상태 전달)

### Data Visualization & Map
- **amCharts 4** (`@amcharts/amcharts4`, `@amcharts/amcharts4-geodata`)

### State Management & Communication
- **Axios** (로그인 API 통신) & **Fetch API** (게시판 데이터 연동)
- **React Hooks** (`useState`, `useEffect`)

### UI Components & Styling
- **CSS Modules / Styled Components**
- **Pagination**: `react-js-pagination`
- **Loading & Animations**: Custom UI (`ShapeLoading.js`), `GSAP`

## 파일 구조 
```
T100_front/
├── public/
│   ├── fonts/
│   │   └── PPEditorialOld-UltraboldItalic.otf
│   ├── LOGO.png
│   ├── favicon.ico
│   ├── happy.jpg
│   ├── index.html
│   ├── logo192.png
│   ├── logo512.png
│   ├── manifest.json
│   ├── map.png
│   ├── robots.txt
│   ├── t1001.jpg
│   ├── t1002.jpg
│   ├── t1003.jpg
│   ├── teabag_img.png
│   └── tft.jpg
├── src/
│   ├── Board/
│   │   ├── Board.css
│   │   ├── Board.js
│   │   ├── BoardDetail.css
│   │   ├── BoardDetail.js
│   │   ├── BoardUpdate.css
│   │   ├── BoardUpdate.js
│   │   ├── BoardWrite.css
│   │   ├── BoardWrite.js
│   │   ├── Editor.css
│   │   ├── Editor.js
│   │   ├── Updator.css
│   │   └── Updator.js
│   ├── Ad.js
│   ├── App.css
│   ├── App.js
│   ├── App.test.js
│   ├── CountryDetails.js
│   ├── Loading.css
│   ├── Loading.js
│   ├── Login.js
│   ├── Main.css
│   ├── Main.js
│   ├── Modal.css
│   ├── Modal.js
│   ├── MyInfo.css
│   ├── MyInfo.js
│   ├── MyPage.css
│   ├── MyPage.js
│   ├── MyPageFunction.css
│   ├── MyPageFunction.js
│   ├── Nav.css
│   ├── Navi.js
│   ├── Pageswap.css
│   ├── Pageswap.js
│   ├── ReportContainer.js
│   ├── ShapeLoading.js
│   ├── Sign.css
│   ├── Sign.js
│   ├── Start.js
│   ├── Style.js
│   ├── WorldMap.js
│   ├── index.css
│   ├── index.js
│   ├── logo.svg
│   ├── reportWebVitals.js
│   ├── settings.css
│   └── setupTests.js
├── .gitignore
├── README.md
├── package-lock.json
├── package.json
└── yarn.lock
```

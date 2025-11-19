<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8" />
  <title>칵테일 파인더 – 와이어프레임</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <style>
    :root {
      --app-width: 390px;
      --padding-x: 20px;
      --space-4: 4px;
      --space-8: 8px;
      --space-12: 12px;
      --space-16: 16px;
      --space-24: 24px;
      --space-32: 32px;
      --border-radius-card: 12px;
      --color-bg: #f5f5f7;
      --color-surface: #ffffff;
      --color-border: #dedede;
      --color-text-main: #111111;
      --color-text-sub: #666666;
      --color-text-muted: #9b9b9b;
      --color-accent: #111111;
      --color-accent-soft: #f2f2f7;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI",
        sans-serif;
      background: #000;
      display: flex;
      justify-content: center;
      padding: var(--space-16);
    }

    .app {
      width: 100%;
      max-width: var(--app-width);
      height: 100vh;
      background: var(--color-bg);
      border-radius: 32px;
      overflow: hidden;
      display: flex;
      flex-direction: column;
      box-shadow: 0 10px 30px rgba(0, 0, 0, 0.25);
    }

    .app-header-spacer {
      height: 16px;
    }

    .app-main {
      flex: 1;
      overflow-y: auto;
      padding: 0 var(--padding-x) var(--space-24);
    }

    .screen {
      display: none;
    }
    .screen--active {
      display: block;
    }

    .section {
      margin-bottom: var(--space-24);
    }

    .section-title {
      font-size: 18px;
      font-weight: 600;
      color: var(--color-text-main);
      margin-bottom: var(--space-12);
    }

    .section-subtitle {
      font-size: 13px;
      color: var(--color-text-muted);
      margin-bottom: var(--space-16);
    }

    /* 검색바 공통 */
    .search-bar {
      margin-bottom: var(--space-24);
    }

    .search-input {
      width: 100%;
      padding: var(--space-12) var(--space-16);
      border-radius: 999px;
      border: 1px solid var(--color-border);
      font-size: 14px;
      outline: none;
      background: var(--color-surface);
      cursor: pointer;
    }

    .search-input::placeholder {
      color: var(--color-text-muted);
    }

    /* 홈 – 빠른 취향 설정 */
    .preference-row {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: var(--space-16);
      margin-bottom: var(--space-12);
    }

    .preference-label-group {
      flex: 1;
    }

    .preference-label {
      font-size: 13px;
      font-weight: 500;
      margin-bottom: var(--space-8);
      color: var(--color-text-main);
    }

    .preference-range {
      width: 100%;
    }

    .preference-level {
      font-size: 12px;
      color: var(--color-text-muted);
      min-width: 56px;
      text-align: right;
    }

    /* 카드 리스트 공통 */
    .card-list {
      display: flex;
      flex-direction: column;
      gap: var(--space-12);
    }

    .cocktail-card,
    .category-card,
    .log-card {
      background: var(--color-surface);
      border-radius: var(--border-radius-card);
      padding: var(--space-16) var(--space-16);
      border: 1px solid var(--color-border);
      cursor: pointer;
      transition: background 0.15s ease, transform 0.1s ease;
    }

    .cocktail-card:hover,
    .category-card:hover,
    .log-card:hover {
      background: #f0f0f2;
    }

    .cocktail-card:active,
    .category-card:active,
    .log-card:active {
      transform: scale(0.98);
    }

    .cocktail-name {
      font-size: 16px;
      font-weight: 600;
      margin-bottom: var(--space-4);
      color: var(--color-text-main);
    }

    .cocktail-base {
      font-size: 12px;
      color: var(--color-text-muted);
      margin-bottom: var(--space-8);
    }

    .cocktail-summary {
      font-size: 13px;
      color: var(--color-text-sub);
      margin-bottom: var(--space-12);
    }

    .cocktail-meta-row {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: var(--space-16);
    }

    .meta-label {
      font-size: 12px;
      color: var(--color-text-muted);
    }

    /* 카테고리 카드 */
    .category-title {
      font-size: 15px;
      font-weight: 600;
      margin-bottom: var(--space-4);
      color: var(--color-text-main);
    }

    .category-desc {
      font-size: 13px;
      color: var(--color-text-sub);
    }

    /* 상단 라인 헤더 (카테고리 화면) */
    .top-bar {
      display: flex;
      align-items: center;
      gap: var(--space-8);
      margin: var(--space-16) 0 var(--space-16);
    }

    .top-bar-back {
      width: 28px;
      height: 28px;
      border-radius: 999px;
      border: 1px solid var(--color-border);
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 14px;
      cursor: pointer;
      background: var(--color-surface);
    }

    .top-bar-title {
      font-size: 17px;
      font-weight: 600;
      color: var(--color-text-main);
    }

    /* 바텀 네비게이션 */
    .app-nav {
      height: 84px;
      background: var(--color-surface);
      border-top: 1px solid var(--color-border);
      display: flex;
      align-items: center;
      justify-content: space-around;
    }

    .nav-item {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 4px;
      font-size: 11px;
      color: var(--color-text-muted);
      cursor: pointer;
    }

    .nav-item--active {
      color: var(--color-text-main);
    }

    .nav-icon {
      width: 26px;
      height: 26px;
      border-radius: 8px;
      border: 1.5px solid var(--color-text-main);
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 14px;
    }

    .nav-item--inactive .nav-icon {
      border-color: var(--color-text-muted);
    }

    .nav-item--record .nav-icon {
      border-radius: 50%;
    }

    .nav-item--prefs .nav-icon {
      border-style: dashed;
    }

    .mt-8 { margin-top: var(--space-8); }
    .mt-16 { margin-top: var(--space-16); }
    .mt-24 { margin-top: var(--space-24); }

    /* ===== 기록 화면 폼 ===== */
    .record-form {
      display: flex;
      flex-direction: column;
      gap: var(--space-16);
      background: var(--color-surface);
      padding: var(--space-16);
      border-radius: var(--border-radius-card);
      border: 1px solid var(--color-border);
    }

    .form-field {
      display: flex;
      flex-direction: column;
      gap: var(--space-8);
    }

    .form-label {
      font-size: 13px;
      font-weight: 500;
      color: var(--color-text-main);
    }

    .form-input,
    .form-select,
    .form-file {
      padding: var(--space-8) var(--space-12);
      border-radius: 8px;
      border: 1px solid var(--color-border);
      font-size: 13px;
      outline: none;
      background: #fff;
    }

    .form-range-row {
      display: flex;
      align-items: center;
      gap: var(--space-12);
    }

    .form-range {
      flex: 1;
    }

    .range-value {
      font-size: 12px;
      color: var(--color-text-sub);
      min-width: 60px;
      text-align: right;
    }

    .btn-primary {
      margin-top: var(--space-8);
      padding: var(--space-12);
      border-radius: 999px;
      border: none;
      background: var(--color-accent);
      color: #fff;
      font-size: 14px;
      font-weight: 600;
      cursor: pointer;
      text-align: center;
    }

    .btn-primary:active {
      transform: scale(0.98);
    }

    .helper-text {
      font-size: 11px;
      color: var(--color-text-muted);
    }

    /* ===== 취향 화면 (기록 리스트) ===== */
    .log-card {
      cursor: default;
    }

    .log-content {
      display: flex;
      gap: var(--space-12);
      align-items: flex-start;
    }

    .log-thumb {
      width: 64px;
      height: 64px;
      border-radius: 12px;
      background: var(--color-accent-soft);
      object-fit: cover;
      flex-shrink: 0;
    }

    .log-info {
      flex: 1;
      display: flex;
      flex-direction: column;
      gap: var(--space-4);
    }

    .log-name {
      font-size: 15px;
      font-weight: 600;
      color: var(--color-text-main);
    }

    .log-date {
      font-size: 12px;
      color: var(--color-text-muted);
    }

    .log-meta-row {
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: var(--space-8);
    }

    .log-rating {
      font-size: 12px;
      color: var(--color-text-sub);
    }

    .log-taste {
      font-size: 12px;
      color: var(--color-text-muted);
    }

    .empty-state {
      font-size: 13px;
      color: var(--color-text-muted);
      padding: var(--space-16);
      background: var(--color-accent-soft);
      border-radius: 12px;
      text-align: center;
    }
  </style>
</head>
<body>
  <div class="app">
    <div class="app-header-spacer"></div>

    <main class="app-main">
      <!-- ===== 홈 화면 ===== -->
      <div class="screen screen--active" id="screen-home">
        <!-- 검색 (탭하면 스타일별 검색 화면으로 이동) -->
        <section class="section search-bar">
          <input
            class="search-input"
            type="search"
            id="home-search-input"
            placeholder="칵테일 검색 (탭해서 스타일 별로 보기)..."
            readonly
          />
        </section>

        <!-- 빠른 취향 설정 -->
        <section class="section">
          <h2 class="section-title">빠른 취향 설정</h2>

          <div class="preference-row">
            <div class="preference-label-group">
              <div class="preference-label">당도</div>
              <input class="preference-range" type="range" min="1" max="5" value="3" />
            </div>
            <div class="preference-level">보통</div>
          </div>

          <div class="preference-row">
            <div class="preference-label-group">
              <div class="preference-label">산미</div>
              <input class="preference-range" type="range" min="1" max="5" value="3" />
            </div>
            <div class="preference-level">보통</div>
          </div>

          <div class="preference-row">
            <div class="preference-label-group">
              <div class="preference-label">향 강도</div>
              <input class="preference-range" type="range" min="1" max="5" value="4" />
            </div>
            <div class="preference-level">보통</div>
          </div>

          <div class="preference-row">
            <div class="preference-label-group">
              <div class="preference-label">도수</div>
              <input class="preference-range" type="range" min="1" max="5" value="2" />
            </div>
            <div class="preference-level">낮음</div>
          </div>
        </section>

        <!-- 추천 칵테일 -->
        <section class="section">
          <h2 class="section-title">추천 칵테일</h2>

          <div class="card-list">
            <!-- Classic 예시: Gin Fizz -->
            <article class="cocktail-card" data-name="Gin Fizz">
              <div class="cocktail-name">Gin Fizz</div>
              <div class="cocktail-base">진 (Classic)</div>
              <p class="cocktail-summary">
                레몬 주스와 탄산수로 상큼하고 청량한 클래식 진 칵테일입니다.
              </p>
              <div class="cocktail-meta-row">
                <span class="meta-label">특징</span>
                <span class="meta-label">상큼 · 가벼움</span>
              </div>
            </article>

            <!-- Contemporary 예시: Mojito -->
            <article class="cocktail-card" data-name="Mojito">
              <div class="cocktail-name">Mojito</div>
              <div class="cocktail-base">럼 (Contemporary)</div>
              <p class="cocktail-summary">
                민트와 라임이 어우러진, 상큼하고 청량한 대표 모던 칵테일입니다.
              </p>
              <div class="cocktail-meta-row">
                <span class="meta-label">특징</span>
                <span class="meta-label">민트 · 라임 · 청량</span>
              </div>
            </article>

            <!-- New Era 예시: New York Sour -->
            <article class="cocktail-card" data-name="New York Sour">
              <div class="cocktail-name">New York Sour</div>
              <div class="cocktail-base">위스키 (New Era)</div>
              <p class="cocktail-summary">
                위스키 사워 위에 레드 와인을 띄운, 비주얼과 밸런스가 뛰어난 뉴 에라 스타일입니다.
              </p>
              <div class="cocktail-meta-row">
                <span class="meta-label">특징</span>
                <span class="meta-label">상큼 · 레드 와인 플로트</span>
              </div>
            </article>
          </div>
        </section>
      </div>

      <!-- ===== 검색 화면 (스타일별: Classic / Contemporary / New Era) ===== -->
      <div class="screen" id="screen-search">
        <section class="section search-bar">
          <input
            class="search-input"
            type="search"
            placeholder="칵테일 이름, 재료로 검색..."
          />
        </section>

        <section class="section">
          <h2 class="section-title">스타일별 칵테일</h2>
          <p class="section-subtitle">Classic / Contemporary / New Era 스타일로 나누어 둘러보세요.</p>

          <div class="card-list">
            <article class="category-card" data-category="classic">
              <div class="category-title">Classic</div>
              <div class="category-desc">
                전통적인 레시피와 역사 속에서 검증된 클래식 칵테일들입니다.
              </div>
            </article>

            <article class="category-card" data-category="contemporary">
              <div class="category-title">Contemporary</div>
              <div class="category-desc">
                비교적 최근 세대에 널리 사랑받는 컨템포러리 스타일 칵테일들입니다.
              </div>
            </article>

            <article class="category-card" data-category="newEra">
              <div class="category-title">New Era</div>
              <div class="category-desc">
                클래식을 재해석한 뉴 에라 스타일의 칵테일들입니다.
              </div>
            </article>
          </div>
        </section>
      </div>

      <!-- ===== 카테고리 상세 화면 ===== -->
      <div class="screen" id="screen-category">
        <div class="top-bar">
          <div class="top-bar-back" id="btn-category-back">←</div>
          <div class="top-bar-title" id="category-title">Classic 칵테일</div>
        </div>

        <section class="section">
          <p class="section-subtitle" id="category-desc">
            전통적인 레시피와 오랜 역사 속에서 사랑받아 온 칵테일들입니다.
          </p>

          <div class="card-list" id="category-list">
            <!-- JS에서 카테고리별 칵테일을 채워 넣습니다 -->
          </div>
        </section>
      </div>

      <!-- ===== 기록 화면 ===== -->
      <div class="screen" id="screen-record">
        <section class="section">
          <h2 class="section-title">칵테일 기록하기</h2>
          <p class="section-subtitle">
            오늘 마신 칵테일의 정보를 기록해두고, 나중에 취향을 다시 볼 수 있어요.
          </p>

          <form class="record-form" id="record-form">
            <div class="form-field">
              <label class="form-label" for="log-name">칵테일 이름</label>
              <input id="log-name" class="form-input" type="text" placeholder="예: New York Sour" required />
            </div>

            <div class="form-field">
              <label class="form-label" for="log-place">장소</label>
              <input id="log-place" class="form-input" type="text" placeholder="예: 홍대 XX바, 집에서" />
            </div>

            <div class="form-field">
              <label class="form-label" for="log-taste">맛 평가 (4단계)</label>
              <select id="log-taste" class="form-select">
                <option value="별로였음">1단계 · 별로였음</option>
                <option value="그저 그럼">2단계 · 그저 그럼</option>
                <option value="괜찮았음" selected>3단계 · 괜찮았음</option>
                <option value="완전 취향">4단계 · 완전 취향</option>
              </select>
              <span class="helper-text">느낌에 가장 가까운 단계를 선택하세요.</span>
            </div>

            <div class="form-field">
              <label class="form-label" for="log-rating">별점 (0.5 단위, 5점 만점)</label>
              <div class="form-range-row">
                <input id="log-rating" class="form-range" type="range" min="0" max="10" step="1" value="8" />
                <div class="range-value" id="log-rating-display">4.0 / 5.0</div>
              </div>
              <span class="helper-text">슬라이더를 움직이면 0.5점 단위로 조정됩니다.</span>
            </div>

            <div class="form-field">
              <label class="form-label" for="log-photo">사진</label>
              <input id="log-photo" class="form-file" type="file" accept="image/*" />
              <span class="helper-text">칵테일이나 바 분위기 사진을 선택해 보관할 수 있어요. (선택)</span>
            </div>

            <button type="submit" class="btn-primary">기록 추가하기</button>
          </form>
        </section>
      </div>

      <!-- ===== 취향(기록 목록) 화면 ===== -->
      <div class="screen" id="screen-prefs">
        <section class="section">
          <h2 class="section-title">나의 칵테일 기록</h2>
          <p class="section-subtitle">
            지금까지 기록한 칵테일들을 모아서 볼 수 있어요.
          </p>

          <div id="log-list" class="card-list">
            <!-- 기록이 없을 때 -->
          </div>
        </section>
      </div>
    </main>

    <!-- 바텀 네비게이션 (홈 / 기록 / 취향) -->
    <nav class="app-nav">
      <div class="nav-item nav-item--active" data-tab="home">
        <div class="nav-icon">⌂</div>
        <span>홈</span>
      </div>
      <div class="nav-item nav-item--inactive nav-item--record" data-tab="record">
        <div class="nav-icon">✚</div>
        <span>기록</span>
      </div>
      <div class="nav-item nav-item--inactive nav-item--prefs" data-tab="prefs">
        <div class="nav-icon">♥</div>
        <span>취향</span>
      </div>
    </nav>
  </div>

  <script>
    // ===== 화면 관리 =====
    const screens = {
      home: document.getElementById('screen-home'),
      search: document.getElementById('screen-search'),
      category: document.getElementById('screen-category'),
      record: document.getElementById('screen-record'),
      prefs: document.getElementById('screen-prefs'),
    };

    const navItems = document.querySelectorAll('.nav-item');

    function setActiveScreen(name) {
      Object.values(screens).forEach(scr => scr.classList.remove('screen--active'));
      if (screens[name]) screens[name].classList.add('screen--active');
    }

    function setActiveTab(tabName) {
      navItems.forEach(item => {
        item.classList.remove('nav-item--active');
        item.classList.add('nav-item--inactive');
        if (item.dataset.tab === tabName) {
          item.classList.add('nav-item--active');
          item.classList.remove('nav-item--inactive');
        }
      });
    }

    navItems.forEach(item => {
      item.addEventListener('click', () => {
        const tab = item.dataset.tab;

        if (tab === 'home') {
          setActiveScreen('home');
          setActiveTab('home');
        } else if (tab === 'record') {
          setActiveScreen('record');
          setActiveTab('record');
        } else if (tab === 'prefs') {
          setActiveScreen('prefs');
          setActiveTab('prefs');
          renderLogs();
        }
      });
    });

    // 홈 상단 검색 탭 → 스타일별 검색 화면으로 이동
    const homeSearchInput = document.getElementById('home-search-input');
    homeSearchInput.addEventListener('click', () => {
      setActiveScreen('search');
      // 탭은 그대로 홈 유지 (검색은 홈 안의 확장 화면 느낌)
    });

    // ===== 카테고리 데이터 (Classic / Contemporary / New Era) =====
    const categoryData = {
      classic: {
        title: 'Classic 칵테일',
        desc: '전통적인 레시피와 역사 속에서 검증된 클래식 칵테일들입니다.',
        cocktails: [
          {
            name: 'Gin Fizz',
            base: '진',
            summary: '레몬 주스, 설탕 시럽, 탄산수로 만드는 상큼하고 청량한 진 칵테일입니다.'
          },
          {
            name: 'Casino',
            base: '진',
            summary: '마라스키노와 오렌지 비터, 레몬 주스로 드라이하면서 은은한 체리 향이 나는 클래식 진 칵테일입니다.'
          },
          {
            name: 'Rusty Nail',
            base: '스카치 위스키',
            summary: '드람뷰이와 스카치를 섞어 달콤함과 스모키함을 동시에 느낄 수 있는 묵직한 칵테일입니다.'
          },
          {
            name: 'Stinger',
            base: '코냑',
            summary: '화이트 크렘드멍트와 코냑이 어우러져 시원한 민트 향과 부드러움을 주는 칵테일입니다.'
          },
          {
            name: 'Paradise',
            base: '진',
            summary: '살구 브랜디와 오렌지 주스가 들어가 과일 향이 풍부하고 부드럽게 마실 수 있는 클래식 칵테일입니다.'
          },
        ],
      },
      contemporary: {
        title: 'Contemporary 칵테일',
        desc: '비교적 최근 세대에 널리 사랑받는 컨템포러리 스타일 칵테일들입니다.',
        cocktails: [
          {
            name: 'Mojito',
            base: '럼',
            summary: '라임, 민트, 설탕, 탄산수를 사용해 상큼하고 청량한 느낌을 주는 대표적인 컨템포러리 칵테일입니다.'
          },
          {
            name: 'Mimosa',
            base: '스파클링 와인',
            summary: '오렌지 주스와 스파클링 와인을 섞어 가볍고 달콤하게 즐길 수 있는 브런치 칵테일입니다.'
          },
          {
            name: 'Sex on the Beach',
            base: '보드카',
            summary: '크랜베리 주스와 피치 리큐르, 오렌지 주스가 들어가 달콤하고 과일맛이 강한 칵테일입니다.'
          },
          {
            name: 'Cosmopolitan',
            base: '보드카',
            summary: '크랜베리 주스와 라임, 트리플섹이 들어간 드라이하면서도 새콤한 핑크 컬러의 대표 칵테일입니다.'
          },
          {
            name: 'Piña Colada',
            base: '럼',
            summary: '코코넛 크림과 파인애플 주스로 만든 부드럽고 달콤한 트로피컬 디저트 칵테일입니다.'
          },
        ],
      },
      newEra: {
        title: 'New Era 칵테일',
        desc: '클래식을 재해석한 레시피와 현대 바 문화 속에서 재조명된 뉴 에라 스타일 칵테일들입니다.',
        cocktails: [
          {
            name: 'New York Sour',
            base: '위스키',
            summary: '위스키 사워 위에 레드 와인을 띄워 상큼함과 깊은 풍미를 동시에 느낄 수 있는 칵테일입니다.'
          },
          {
            name: 'Bee’s Knees',
            base: '진',
            summary: '꿀 시럽과 레몬 주스를 사용해 꿀의 달콤함과 산미가 조화로운 상큼한 진 칵테일입니다.'
          },
          {
            name: 'Jungle Bird',
            base: '다크 럼',
            summary: '캄파리, 파인애플 주스, 라임이 들어가 달콤함과 쌉싸름함, 열대 과일 향이 모두 느껴지는 티키 스타일 칵테일입니다.'
          },
          {
            name: 'Paloma',
            base: '데킬라',
            summary: '자몽 주스와 라임, 탄산수를 사용해 멕시코에서 특히 사랑받는 상큼하고 가벼운 칵테일입니다.'
          },
          {
            name: 'Canchanchara',
            base: '럼',
            summary: '꿀과 라임, 탄산수로 만드는 쿠바 전통 스타일 칵테일로, 상큼하면서도 부드러운 맛이 특징입니다.'
          },
        ],
      },
    };

    const categoryTitleEl = document.getElementById('category-title');
    const categoryDescEl = document.getElementById('category-desc');
    const categoryListEl = document.getElementById('category-list');
    const btnCategoryBack = document.getElementById('btn-category-back');

    // 카테고리 카드 클릭 시 카테고리 화면으로 전환
    document.querySelectorAll('.category-card').forEach(card => {
      card.addEventListener('click', () => {
        const category = card.dataset.category;
        const data = categoryData[category];

        if (!data) return;

        categoryTitleEl.textContent = data.title;
        categoryDescEl.textContent = data.desc;

        categoryListEl.innerHTML = '';
        data.cocktails.forEach(c => {
          const article = document.createElement('article');
          article.className = 'cocktail-card';
          article.innerHTML = `
            <div class="cocktail-name">${c.name}</div>
            <div class="cocktail-base">${c.base}</div>
            <p class="cocktail-summary">${c.summary}</p>
          `;
          categoryListEl.appendChild(article);
        });

        setActiveScreen('category');
      });
    });

    // 카테고리 화면 뒤로가기 → 다시 검색 화면으로
    btnCategoryBack.addEventListener('click', () => {
      setActiveScreen('search');
    });

    // ===== 기록 데이터 관리 =====
    const logs = []; // 메모리 상에만 저장 (새로고침시 초기화)

    const recordForm = document.getElementById('record-form');
    const logRatingInput = document.getElementById('log-rating');
    const logRatingDisplay = document.getElementById('log-rating-display');

    function updateRatingDisplay() {
      const value = parseInt(logRatingInput.value, 10);
      const score = (value / 2).toFixed(1); // 0~10 → 0~5 (0.5 단위)
      logRatingDisplay.textContent = `${score} / 5.0`;
    }

    logRatingInput.addEventListener('input', updateRatingDisplay);
    updateRatingDisplay();

    recordForm.addEventListener('submit', (e) => {
      e.preventDefault();

      const name = document.getElementById('log-name').value.trim();
      const place = document.getElementById('log-place').value.trim();
      const taste = document.getElementById('log-taste').value;
      const ratingRaw = parseInt(logRatingInput.value, 10);
      const rating = ratingRaw / 2;
      const photoInput = document.getElementById('log-photo');
      const file = photoInput.files[0];

      if (!name) {
        alert('칵테일 이름을 입력해주세요.');
        return;
      }

      let imageUrl = null;
      if (file) {
        imageUrl = URL.createObjectURL(file);
      }

      const date = new Date().toLocaleDateString('ko-KR');

      logs.push({
        name,
        place,
        taste,
        rating,
        imageUrl,
        date,
      });

      // 폼 초기화
      recordForm.reset();
      logRatingInput.value = 8;
      updateRatingDisplay();

      alert('기록이 추가되었습니다. 취향 탭에서 확인할 수 있어요.');
    });

    const logListEl = document.getElementById('log-list');

    function renderLogs() {
      logListEl.innerHTML = '';

      if (logs.length === 0) {
        const empty = document.createElement('div');
        empty.className = 'empty-state';
        empty.textContent = '아직 기록된 칵테일이 없습니다. 하단의 [기록] 탭에서 첫 기록을 추가해 보세요.';
        logListEl.appendChild(empty);
        return;
      }

      logs.slice().reverse().forEach((log) => {
        const card = document.createElement('article');
        card.className = 'log-card';
        const ratingText = `${log.rating.toFixed(1)} / 5.0`;

        card.innerHTML = `
          <div class="log-content">
            <div>
              ${
                log.imageUrl
                  ? `<img class="log-thumb" src="${log.imageUrl}" alt="${log.name}">`
                  : `<div class="log-thumb"></div>`
              }
            </div>
            <div class="log-info">
              <div class="log-name">${log.name}</div>
              <div class="log-date">${log.date}${log.place ? ` · ${log.place}` : ''}</div>
              <div class="log-meta-row">
                <div class="log-rating">⭐ ${ratingText}</div>
                <div class="log-taste">${log.taste}</div>
              </div>
            </div>
          </div>
        `;
        logListEl.appendChild(card);
      });
    }
  </script>
</body>
</html>

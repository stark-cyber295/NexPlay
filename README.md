# NexPlay 
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="theme-color" content="#080b14">
  <title>NexPlay | Browser Arcade</title>
  <style>
    :root {
      --bg: #080b14;
      --panel: #111827;
      --panel2: #151e30;
      --blue: #48a8ff;
      --purple: #a56bff;
      --text: #f4f7ff;
      --muted: #98a6bf;
      --border: #253149;
    }

    * { box-sizing: border-box; }

    body {
      margin: 0;
      color: var(--text);
      background:
        radial-gradient(ellipse at 50% -20%, #17325b 0, transparent 50%),
        var(--bg);
      font-family: Inter, system-ui, -apple-system, Segoe UI, sans-serif;
      min-height: 100vh;
    }

    button, input { font: inherit; }

    button, a { -webkit-tap-highlight-color: transparent; }

    a { color: inherit; text-decoration: none; }

    .topbar {
      position: sticky;
      top: 0;
      z-index: 10;
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 16px;
      padding: 15px 5%;
      background: rgba(8, 11, 20, .88);
      backdrop-filter: blur(14px);
      border-bottom: 1px solid var(--border);
    }

    .logo {
      font-size: 25px;
      font-weight: 900;
      letter-spacing: -1px;
    }

    .logo span { color: var(--blue); }

    .top-actions {
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .status-pill {
      color: #a9e9c5;
      background: #153326;
      border: 1px solid #24563e;
      border-radius: 30px;
      padding: 7px 11px;
      font-size: 12px;
    }

    .hero {
      text-align: center;
      padding: 46px 18px 30px;
    }

    .eyebrow {
      color: var(--blue);
      text-transform: uppercase;
      letter-spacing: 3px;
      font-weight: 800;
      font-size: 12px;
    }

    h1 {
      font-size: clamp(38px, 7vw, 68px);
      line-height: 1.05;
      letter-spacing: -3px;
      margin: 14px 0;
    }

    h1 span {
      background: linear-gradient(90deg, var(--blue), var(--purple));
      -webkit-background-clip: text;
      background-clip: text;
      color: transparent;
    }

    .hero p {
      color: var(--muted);
      max-width: 580px;
      margin: 0 auto;
      line-height: 1.7;
    }

    .wrap {
      width: min(1200px, 92%);
      margin: 0 auto;
    }

    .player-section { margin: 18px auto 42px; }

    .section-heading {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 12px;
      margin-bottom: 14px;
    }

    h2 {
      font-size: 23px;
      margin: 0;
      letter-spacing: -.6px;
    }

    .small-text {
      color: var(--muted);
      font-size: 12px;
    }

    .player-shell {
      overflow: hidden;
      background: #03050a;
      border: 1px solid #293c5b;
      border-radius: 18px;
      box-shadow: 0 0 45px #236cc21c;
    }

    .player-bar {
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 12px;
      padding: 12px 15px;
      background: var(--panel);
      border-bottom: 1px solid var(--border);
    }

    .playing-name {
      display: flex;
      align-items: center;
      gap: 10px;
      min-width: 0;
      font-weight: 750;
    }

    .playing-name span:last-child {
      overflow: hidden;
      text-overflow: ellipsis;
      white-space: nowrap;
    }

    .player-buttons {
      display: flex;
      gap: 8px;
      flex-wrap: wrap;
    }

    .btn {
      display: inline-flex;
      align-items: center;
      justify-content: center;
      gap: 7px;
      padding: 10px 13px;
      border: 1px solid var(--border);
      border-radius: 10px;
      color: var(--text);
      background: #1a2539;
      cursor: pointer;
      font-size: 13px;
      font-weight: 700;
      transition: .18s ease;
    }

    .btn:hover {
      transform: translateY(-1px);
      border-color: var(--blue);
    }

    .btn-primary {
      color: #06101d;
      background: var(--blue);
      border-color: var(--blue);
    }

    .btn-primary:hover { background: #82c5ff; }

    .player-stage {
      position: relative;
      width: 100%;
      aspect-ratio: 16 / 9;
      min-height: 280px;
      background:
        radial-gradient(ellipse at center, #132542 0, #070b13 70%);
    }

    #gameFrame {
      display: none;
      width: 100%;
      height: 100%;
      min-height: 280px;
      position: absolute;
      inset: 0;
      border: 0;
      background: #fff;
    }

    .placeholder {
      position: absolute;
      inset: 0;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      text-align: center;
      padding: 24px;
    }

    .big-icon {
      font-size: clamp(45px, 8vw, 75px);
      margin-bottom: 12px;
      filter: drop-shadow(0 0 20px #48a8ff44);
    }

    .placeholder h3 {
      font-size: 24px;
      margin: 0 0 8px;
    }

    .placeholder p {
      max-width: 460px;
      color: var(--muted);
      font-size: 14px;
      line-height: 1.6;
      margin: 0 0 17px;
    }

    .player-note {
      padding: 12px 15px;
      color: var(--muted);
      background: #0c1220;
      border-top: 1px solid var(--border);
      font-size: 12px;
      line-height: 1.6;
    }

    .library { padding-bottom: 55px; }

    .tools {
      display: flex;
      gap: 12px;
      margin: 18px 0;
      flex-wrap: wrap;
    }

    .search-box {
      flex: 1 1 230px;
      min-width: 0;
      position: relative;
    }

    .search-box input {
      width: 100%;
      padding: 14px 15px 14px 42px;
      color: var(--text);
      background: var(--panel);
      border: 1px solid var(--border);
      border-radius: 12px;
      outline: none;
    }

    .search-box input:focus {
      border-color: var(--blue);
      box-shadow: 0 0 0 3px #48a8ff19;
    }

    .search-icon {
      position: absolute;
      top: 12px;
      left: 14px;
      color: var(--muted);
    }

    .filters {
      display: flex;
      flex-wrap: wrap;
      gap: 8px;
      margin-bottom: 20px;
    }

    .filter {
      padding: 9px 13px;
      border: 1px solid var(--border);
      border-radius: 30px;
      color: var(--muted);
      background: var(--panel);
      cursor: pointer;
      font-size: 13px;
    }

    .filter.active, .filter:hover {
      color: white;
      background: #173459;
      border-color: var(--blue);
    }

    .game-grid {
      display: grid;
      grid-template-columns: repeat(4, minmax(0, 1fr));
      gap: 15px;
    }

    .game-card {
      min-width: 0;
      padding: 15px;
      border: 1px solid var(--border);
      border-radius: 15px;
      background: linear-gradient(150deg, #141e30, #0d1320);
      transition: .2s ease;
    }

    .game-card:hover {
      transform: translateY(-3px);
      border-color: #416a9f;
      box-shadow: 0 12px 30px #0003;
    }

    .game-top {
      display: flex;
      align-items: flex-start;
      justify-content: space-between;
      gap: 10px;
    }

    .game-icon {
      width: 54px;
      height: 54px;
      display: grid;
      place-items: center;
      border-radius: 13px;
      font-size: 29px;
      background: linear-gradient(135deg, #1d3b60, #292147);
      border: 1px solid #354768;
    }

    .favorite {
      padding: 3px;
      color: #8190a9;
      border: 0;
      background: transparent;
      font-size: 23px;
      cursor: pointer;
    }

    .favorite.selected { color: #ffd166; }

    .game-card h3 {
      margin: 13px 0 5px;
      font-size: 16px;
    }

    .game-card p {
      height: 34px;
      margin: 0 0 13px;
      color: var(--muted);
      font-size: 12px;
      line-height: 1.4;
    }

    .game-actions {
      display: flex;
      gap: 7px;
    }

    .game-actions .btn {
      flex: 1;
      padding: 9px 6px;
      font-size: 12px;
    }

    .empty {
      grid-column: 1 / -1;
      padding: 40px;
      color: var(--muted);
      text-align: center;
      border: 1px dashed var(--border);
      border-radius: 14px;
    }

    footer {
      border-top: 1px solid var(--border);
      padding: 23px 5%;
      color: var(--muted);
      text-align: center;
      font-size: 12px;
      line-height: 1.8;
    }

    @media (max-width: 900px) {
      .game-grid { grid-template-columns: repeat(3, minmax(0, 1fr)); }
    }

    @media (max-width: 620px) {
      .game-grid { grid-template-columns: repeat(2, minmax(0, 1fr)); }
      .topbar { padding: 12px 4%; }
      .logo { font-size: 22px; }
      .status-pill { display: none; }
      .hero { padding-top: 35px; }
      h1 { letter-spacing: -1.5px; }
      .player-bar { align-items: flex-start; flex-direction: column; }
      .player-stage { aspect-ratio: 4 / 3; min-height: 300px; }
      #gameFrame { min-height: 300px; }
    }

    @media (max-width: 370px) {
      .game-grid { grid-template-columns: 1fr; }
    }
  </style>
</head>
<body>
  <header class="topbar">
    <a class="logo" href="#">Nex<span>Play</span></a>
    <div class="top-actions">
      <span class="status-pill">● Browser Arcade</span>
      <a class="btn" href="#games">🎮 Games</a>
    </div>
  </header>

  <section class="hero">
    <div class="eyebrow">Your next game is here</div>
    <h1>Play More. <span>Explore More.</span></h1>
    <p>Find your next favorite game. Search the library, save favorites, and try games in the built-in player.</p>
  </section>

  <main class="wrap">
    <section class="player-section" id="player">
      <div class="section-heading">
        <h2>🎯 Game Player</h2>
        <span class="small-text">Choose a game below to get started</span>
      </div>

      <div class="player-shell">
        <div class="player-bar">
          <div class="playing-name">
            <span id="currentIcon">🎮</span>
            <span id="currentTitle">Ready to play?</span>
          </div>
          <div class="player-buttons">
            <button class="btn" id="reloadBtn" type="button">↻ Reload</button>
            <a class="btn btn-primary" id="openGame" href="https://poki.com/" target="_blank" rel="noopener noreferrer">Open Game ↗</a>
          </div>
        </div>

        <div class="player-stage">
          <iframe
            id="gameFrame"
            title="NexPlay game player"
            allow="fullscreen; autoplay; gamepad; clipboard-read; clipboard-write"
            allowfullscreen
            referrerpolicy="strict-origin-when-cross-origin">
          </iframe>

          <div class="placeholder" id="placeholder">
            <div class="big-icon" id="placeholderIcon">🕹️</div>
            <h3 id="placeholderTitle">Pick your first game</h3>
            <p id="placeholderText">Choose any game card below. If a game doesn't appear here, use the Open Game button to play on its original website.</p>
            <a href="#games" class="btn btn-primary">Browse Games ↓</a>
          </div>
        </div>

        <div class="player-note" id="playerStatus" aria-live="polite">
          Ready. Some game websites block embedded players; those games may need to open in a new tab.
        </div>
      </div>
    </section>

    <section class="library" id="games">
      <div class="section-heading">
        <h2>🕹️ Game Library</h2>
        <span class="small-text" id="gameCount"></span>
      </div>

      <div class="tools">
        <div class="search-box">
          <span class="search-icon">⌕</span>
          <input id="searchInput" type="search" placeholder="Search games..." autocomplete="off" aria-label="Search games">
        </div>
        <button class="btn" id="favoritesToggle" type="button">☆ Favorites</button>
      </div>

      <div class="filters" id="filters">
        <button class="filter active" data-category="All">All Games</button>
        <button class="filter" data-category="Racing">🏎️ Racing</button>
        <button class="filter" data-category="Sports">🏀 Sports</button>
        <button class="filter" data-category="Arcade">👾 Arcade</button>
        <button class="filter" data-category="Puzzle">🧩 Puzzle</button>
        <button class="filter" data-category="Strategy">🧠 Strategy</button>
        <button class="filter" data-category="Music">🎵 Music</button>
      </div>

      <div class="game-grid" id="gameGrid"></div>
    </section>
  </main>

  <footer>
    <strong>NexPlay</strong> — Your browser arcade.<br>
    Games are hosted by their respective websites. NexPlay is an independent game portal and is not affiliated with those sites.
  </footer>

  <script>
    const games = [
      {
        name: "Escape Road 3",
        icon: "🚘",
        category: "Racing",
        description: "Escape, dodge traffic, and keep moving.",
        url: "https://poki.com/"
      },
      {
        name: "Slope",
        icon: "🟢",
        category: "Arcade",
        description: "Guide a ball down a fast 3D course.",
        url: "https://slopegame.io/"
      },
      {
        name: "Retro Bowl",
        icon: "🏈",
        category: "Sports",
        description: "Manage your team and play football.",
        url: "https://poki.com/en/g/retro-bowl"
      },
      {
        name: "Cookie Clicker",
        icon: "🍪",
        category: "Strategy",
        description: "Click cookies and build your bakery.",
        url: "https://orteil.dashnet.org/cookieclicker/"
      },
      {
        name: "BitLife",
        icon: "📱",
        category: "Strategy",
        description: "Make choices in a life simulator.",
        url: "https://bitlifeonline.com/"
      },
      {
        name: "Minecraft Classic",
        icon: "🧱",
        category: "Arcade",
        description: "Build with blocks in the classic version.",
        url: "https://classic.minecraft.net/"
      },
      {
        name: "Geometry Dash",
        icon: "🔷",
        category: "Music",
        description: "Jump and dodge to the rhythm.",
        url: "https://www.crazygames.com/"
      },
      {
        name: "Baseball Bros",
        icon: "⚾",
        category: "Sports",
        description: "Swing for the fences in arcade baseball.",
        url: "https://baseballbros.io/"
      },
      {
        name: "Basket Bros",
        icon: "🏀",
        category: "Sports",
        description: "Play quick basketball matches.",
        url: "https://basketbros.io/"
      },
      {
        name: "Football Bros",
        icon: "🏈",
        category: "Sports",
        description: "Take on opponents in arcade football.",
        url: "https://footballbros.io/"
      },
      {
        name: "Moto X3M",
        icon: "🏍️",
        category: "Racing",
        description: "Race a bike across obstacle courses.",
        url: "https://poki.com/en/moto-x3m"
      },
      {
        name: "2048",
        icon: "🔢",
        category: "Puzzle",
        description: "Combine tiles to reach 2048.",
        url: "https://play2048.co/"
      },
      {
        name: "Wordle",
        icon: "🟩",
        category: "Puzzle",
        description: "Guess the daily five-letter word.",
        url: "https://www.nytimes.com/games/wordle/index.html"
      },
      {
        name: "Agar.io",
        icon: "🔵",
        category: "Arcade",
        description: "Grow your cell and avoid bigger cells.",
        url: "https://agar.io/"
      },
      {
        name: "Slither.io",
        icon: "🐍",
        category: "Arcade",
        description: "Grow your snake and collect glowing dots.",
        url: "https://slither.io/"
      },
      {
        name: "Tetris",
        icon: "🟪",
        category: "Puzzle",
        description: "Fit falling blocks into complete lines.",
        url: "https://tetris.com/play-tetris"
      },
      {
        name: "Chess",
        icon: "♟️",
        category: "Strategy",
        description: "Practice your moves on a chessboard.",
        url: "https://www.chess.com/play"
      },
      {
        name: "Little Alchemy 2",
        icon: "🧪",
        category: "Puzzle",
        description: "Combine elements to discover new things.",
        url: "https://littlealchemy2.com/"
      },
      {
        name: "Vex 3",
        icon: "🏃",
        category: "Arcade",
        description: "Run, jump, and solve platform challenges.",
        url: "https://www.crazygames.com/"
      },
      {
        name: "Space Waves",
        icon: "🌊",
        category: "Arcade",
        description: "Steer through waves of obstacles.",
        url: "https://www.crazygames.com/"
      },
      {
        name: "Smash Karts",
        icon: "🏎️",
        category: "Racing",
        description: "Race and battle in kart arenas.",
        url: "https://smashkarts.io/"
      },
      {
        name: "Paper.io 2",
        icon: "🟨",
        category: "Arcade",
        description: "Expand your territory and protect it.",
        url: "https://paper-io.com/"
      },
      {
        name: "Flappy Bird",
        icon: "🐤",
        category: "Arcade",
        description: "Fly through obstacles with careful taps.",
        url: "https://flappybird.io/"
      },
      {
        name: "Drift Boss",
        icon: "🚗",
        category: "Racing",
        description: "Time your turns on a winding track.",
        url: "https://poki.com/en/drift-boss"
      },
      {
        name: "Eggy Car",
        icon: "🥚",
        category: "Racing",
        description: "Drive carefully and keep your egg safe.",
        url: "https://poki.com/en/eggy-car"
      },
      {
        name: "Friday Night Funkin'",
        icon: "🎤",
        category: "Music",
        description: "Hit the notes in a rhythm battle.",
        url: "https://www.newgrounds.com/portal/view/770371"
      }
    ];

    const grid = document.getElementById("gameGrid");
    const searchInput = document.getElementById("searchInput");
    const gameCount = document.getElementById("gameCount");
    const favoritesToggle = document.getElementById("favoritesToggle");
    const frame = document.getElementById("gameFrame");
    const placeholder = document.getElementById("placeholder");
    const currentTitle = document.getElementById("currentTitle");
    const currentIcon = document.getElementById("currentIcon");
    const openGame = document.getElementById("openGame");
    const playerStatus = document.getElementById("playerStatus");

    let activeCategory = "All";
    let showFavoritesOnly = false;
    let currentGame = null;
    let favorites = [];

    try {
      favorites = JSON.parse(localStorage.getItem("nexplay-favorites") || "[]");
      if (!Array.isArray(favorites)) favorites = [];
    } catch {
      favorites = [];
    }

    function saveFavorites() {
      try {
        localStorage.setItem("nexplay-favorites", JSON.stringify(favorites));
      } catch {
        // Favorites still work until this page is refreshed.
      }
    }

    function escapeHTML(value) {
      return String(value).replace(/[&<>"']/g, char => ({
        "&": "&amp;",
        "<": "&lt;",
        ">": "&gt;",
        '"': "&quot;",
        "'": "&#39;"
      })[char]);
    }

    function renderGames() {
      const search = searchInput.value.trim().toLowerCase();

      const filtered = games.filter(game => {
        const matchesSearch =
          game.name.toLowerCase().includes(search) ||
          game.category.toLowerCase().includes(search) ||
          game.description.toLowerCase().includes(search);

        const matchesCategory =
          activeCategory === "All" || game.category === activeCategory;

        const matchesFavorite =
          !showFavoritesOnly || favorites.includes(game.name);

        return matchesSearch && matchesCategory && matchesFavorite;
      });

      gameCount.textContent = `${filtered.length} games`;
      grid.innerHTML = "";

      if (!filtered.length) {
        grid.innerHTML = '<div class="empty">No games found. Try another search or category.</div>';
        return;
      }

      filtered.forEach(game => {
        const isFavorite = favorites.includes(game.name);
        const card = document.createElement("article");
        card.className = "game-card";

        card.innerHTML = `
          <div class="game-top">
            <div class="game-icon">${game.icon}</div>
            <button
              class="favorite ${isFavorite ? "selected" : ""}"
              type="button"
              aria-label="${isFavorite ? "Remove from" : "Add to"} favorites"
              title="${isFavorite ? "Remove favorite" : "Add favorite"}"
            >${isFavorite ? "★" : "☆"}</button>
          </div>
          <h3>${escapeHTML(game.name)}</h3>
          <p>${escapeHTML(game.description)}</p>
          <div class="game-actions">
            <button class="btn btn-primary play-button" type="button">▶ Play Here</button>
            <a
              class="btn"
              href="${escapeHTML(game.url)}"
              target="_blank"
              rel="noopener noreferrer"
            >↗ Open</a>
          </div>
        `;

        card.querySelector(".play-button").addEventListener("click", () => {
          loadGame(game);
        });

        card.querySelector(".favorite").addEventListener("click", () => {
          if (favorites.includes(game.name)) {
            favorites = favorites.filter(name => name !== game.name);
          } else {
            favorites.push(game.name);
          }
          saveFavorites();
          renderGames();
        });

        grid.appendChild(card);
      });
    }

    function loadGame(game) {
      currentGame = game;

      currentTitle.textContent = game.name;
      currentIcon.textContent = game.icon;
      openGame.href = game.url;

      placeholder.style.display = "none";
      frame.style.display = "block";

      // Reset the iframe when reloading the same game.
      frame.src = "about:blank";
      frame.src = game.url;

      playerStatus.textContent =
        `Loading ${game.name}. If the player stays blank or shows an error, this site may block embedding. Click "Open Game" to play on the original website.`;

      document.getElementById("player").scrollIntoView({
        behavior: "smooth",
        block: "start"
      });
    }

    document.getElementById("reloadBtn").addEventListener("click", () => {
      if (currentGame) {
        loadGame(currentGame);
      } else {
        playerStatus.textContent = "Choose a game from the library first.";
      }
    });

    searchInput.addEventListener("input", renderGames);

    document.querySelectorAll(".filter").forEach(button => {
      button.addEventListener("click", () => {
        activeCategory = button.dataset.category;

        document.querySelectorAll(".filter").forEach(item => {
          item.classList.toggle("active", item === button);
        });

        renderGames();
      });
    });

    favoritesToggle.addEventListener("click", () => {
      showFavoritesOnly = !showFavoritesOnly;
      favoritesToggle.textContent = showFavoritesOnly
        ? "★ Show All Games"
        : "☆ Favorites";
      favoritesToggle.classList.toggle("btn-primary", showFavoritesOnly);
      renderGames();
    });

    renderGames();
  </script>
</body>
</html>


# NexPlay 

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <meta name="theme-color" content="#080b14">
  <title>NexPlay | Browser Arcade</title>

  <style>
    :root {
      --bg: #080b14;
      --panel: #111827;
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
      background: radial-gradient(ellipse at 50% -20%, #17325b, transparent 55%), var(--bg);
      font-family: system-ui, sans-serif;
    }

    button, input { font: inherit; }
    a { color: inherit; text-decoration: none; }

    .topbar {
      position: sticky;
      top: 0;
      z-index: 5;
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 15px 5%;
      background: #080b14ed;
      border-bottom: 1px solid var(--border);
      backdrop-filter: blur(12px);
    }

    .logo { font-size: 25px; font-weight: 900; }
    .logo span, .accent { color: var(--blue); }

    .wrap { width: min(1200px, 92%); margin: auto; }

    .hero { text-align: center; padding: 45px 15px 30px; }

    .eyebrow {
      color: var(--blue);
      text-transform: uppercase;
      letter-spacing: 3px;
      font-size: 12px;
      font-weight: 800;
    }

    h1 {
      margin: 12px 0;
      font-size: clamp(38px, 7vw, 66px);
      line-height: 1.1;
      letter-spacing: -2px;
    }

    h1 span {
      background: linear-gradient(90deg, var(--blue), var(--purple));
      color: transparent;
      background-clip: text;
    }

    .hero p { color: var(--muted); line-height: 1.7; }

    .section-heading {
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 12px;
      margin-bottom: 14px;
    }

    h2 { margin: 0; font-size: 23px; }

    .muted { color: var(--muted); font-size: 12px; }

    .player-shell {
      overflow: hidden;
      background: #03050a;
      border: 1px solid #293c5b;
      border-radius: 16px;
      margin-bottom: 42px;
    }

    .player-bar {
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 12px;
      flex-wrap: wrap;
      padding: 12px 15px;
      background: var(--panel);
      border-bottom: 1px solid var(--border);
    }

    .playing-name { font-weight: 800; }

    .player-buttons, .game-actions, .tools, .filters {
      display: flex;
      gap: 8px;
      flex-wrap: wrap;
    }

    .btn {
      display: inline-flex;
      align-items: center;
      justify-content: center;
      padding: 10px 13px;
      border: 1px solid var(--border);
      border-radius: 9px;
      color: var(--text);
      background: #1a2539;
      font-size: 13px;
      font-weight: 750;
      cursor: pointer;
    }

    .btn:hover { border-color: var(--blue); }

    .btn-primary {
      color: #06101d;
      background: var(--blue);
      border-color: var(--blue);
    }

    .player-stage {
      position: relative;
      aspect-ratio: 16 / 9;
      min-height: 280px;
      background: radial-gradient(ellipse, #132542, #070b13);
    }

    #gameFrame {
      display: none;
      position: absolute;
      inset: 0;
      width: 100%;
      height: 100%;
      min-height: 280px;
      border: 0;
      background: white;
    }

    .placeholder {
      position: absolute;
      inset: 0;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      padding: 22px;
      text-align: center;
    }

    .big-icon { font-size: 65px; margin-bottom: 10px; }
    .placeholder h3 { margin: 0 0 8px; font-size: 23px; }
    .placeholder p { max-width: 480px; color: var(--muted); line-height: 1.6; }

    .player-note {
      padding: 12px 15px;
      color: var(--muted);
      background: #0c1220;
      border-top: 1px solid var(--border);
      font-size: 12px;
      line-height: 1.6;
    }

    .library { padding-bottom: 50px; }

    .tools { margin: 18px 0; }

    .search-box { flex: 1 1 220px; }

    .search-box input {
      width: 100%;
      padding: 13px;
      color: var(--text);
      background: var(--panel);
      border: 1px solid var(--border);
      border-radius: 10px;
      outline: none;
    }

    .search-box input:focus { border-color: var(--blue); }

    .filters { margin-bottom: 20px; }

    .filter {
      padding: 9px 13px;
      color: var(--muted);
      background: var(--panel);
      border: 1px solid var(--border);
      border-radius: 25px;
      cursor: pointer;
      font-size: 13px;
    }

    .filter.active {
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
      background: linear-gradient(150deg, #141e30, #0d1320);
      border: 1px solid var(--border);
      border-radius: 14px;
    }

    .game-card:hover {
      border-color: #416a9f;
      transform: translateY(-2px);
    }

    .game-top {
      display: flex;
      align-items: center;
      justify-content: space-between;
    }

    .game-icon {
      display: grid;
      place-items: center;
      width: 52px;
      height: 52px;
      font-size: 28px;
      border-radius: 12px;
      background: linear-gradient(135deg, #1d3b60, #292147);
    }

    .favorite {
      color: #8190a9;
      background: transparent;
      border: 0;
      font-size: 24px;
      cursor: pointer;
    }

    .favorite.selected { color: #ffd166; }

    .game-card h3 { margin: 13px 0 5px; font-size: 16px; }

    .game-card p {
      min-height: 34px;
      margin: 0 0 13px;
      color: var(--muted);
      font-size: 12px;
      line-height: 1.5;
    }

    .game-actions { display: flex; }
    .game-actions .btn { flex: 1; padding: 9px 5px; font-size: 12px; }

    .empty {
      grid-column: 1 / -1;
      padding: 35px;
      text-align: center;
      color: var(--muted);
      border: 1px dashed var(--border);
      border-radius: 12px;
    }

    footer {
      padding: 24px 5%;
      color: var(--muted);
      text-align: center;
      border-top: 1px solid var(--border);
      font-size: 12px;
      line-height: 1.8;
    }

    @media (max-width: 900px) {
      .game-grid { grid-template-columns: repeat(3, minmax(0, 1fr)); }
    }

    @media (max-width: 620px) {
      .game-grid { grid-template-columns: repeat(2, minmax(0, 1fr)); }
      .player-stage { aspect-ratio: 4 / 3; min-height: 300px; }
      #gameFrame { min-height: 300px; }
      .topbar { padding: 12px 4%; }
    }

    @media (max-width: 370px) {
      .game-grid { grid-template-columns: 1fr; }
    }
  </style>
</head>

<body>
  <header class="topbar">
    <a class="logo" href="#">Nex<span>Play</span></a>
    <a class="btn" href="#games">🎮 Games</a>
  </header>

  <section class="hero">
    <div class="eyebrow">Your next game is here</div>
    <h1>Play More. <span>Explore More.</span></h1>
    <p>Find your next favorite game, search the library, and save your favorites.</p>
  </section>

  <main class="wrap">
    <section id="player">
      <div class="section-heading">
        <h2>🎯 Game Player</h2>
        <span class="muted">Select a game below</span>
      </div>

      <div class="player-shell">
        <div class="player-bar">
          <div class="playing-name">
            <span id="currentIcon">🎮</span>
            <span id="currentTitle">Ready to play?</span>
          </div>
          <div class="player-buttons">
            <button class="btn" id="reloadBtn" type="button">↻ Reload</button>
            <a class="btn btn-primary" id="openGame"
               href="https://escaperoad-3.com/"
               target="_blank" rel="noopener noreferrer">Open Game ↗</a>
          </div>
        </div>

        <div class="player-stage">
          <iframe id="gameFrame"
            title="NexPlay game player"
            allow="fullscreen; autoplay; gamepad; clipboard-read; clipboard-write"
            allowfullscreen
            referrerpolicy="strict-origin-when-cross-origin"></iframe>

          <div class="placeholder" id="placeholder">
            <div class="big-icon">🕹️</div>
            <h3>Pick your first game</h3>
            <p>Choose a game below. If it doesn't load here, click Open Game to play on its own website.</p>
            <a class="btn btn-primary" href="#games">Browse Games ↓</a>
          </div>
        </div>

        <div class="player-note" id="playerStatus" aria-live="polite">
          Ready! Some game websites do not allow embedded play.
        </div>
      </div>
    </section>

    <section class="library" id="games">
      <div class="section-heading">
        <h2>🕹️ Game Library</h2>
        <span class="muted" id="gameCount"></span>
      </div>

      <div class="tools">
        <div class="search-box">
          <input id="searchInput" type="search"
            placeholder="🔎 Search games..." aria-label="Search games">
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
    Games are provided by their respective websites. NexPlay is an independent portal.
  </footer>

  <script>
    const games = [
      {
        name: "Escape Road 3",
        icon: "🚘",
        category: "Racing",
        description: "Escape the police in a driving chase.",
        url: "https://escaperoad-3.com/"
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
        url: "https://cookieclicker.com/"
      },
      {
        name: "BitLife",
        icon: "📱",
        category: "Strategy",
        description: "Life simulator website.",
        url: "https://bitlifeonline.com/"
      },
      {
        name: "Minecraft Classic",
        icon: "🧱",
        category: "Arcade",
        description: "Build with blocks in classic Minecraft.",
        url: "https://classic.minecraft.net/"
      },
      {
        name: "Geometry Dash",
        icon: "🔷",
        category: "Music",
        description: "A browser rhythm-platformer inspired by Geometry Dash.",
        url: "https://www.crazygames.com/game/geometry-dash-online"
      },
      {
        name: "Baseball Bros",
        icon: "⚾",
        category: "Sports",
        description: "Play arcade-style baseball.",
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
        url: "https://fb.dunkbros.com/"
      },
      {
        name: "Moto X3M",
        icon: "🏍️",
        category: "Racing",
        description: "Race a bike through obstacle courses.",
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
        description: "Grow your snake and collect dots.",
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
        description: "Play chess online.",
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
        description: "Run, jump, climb, and dodge obstacles.",
        url: "https://vex-3.com/vex-3"
      },
      {
        name: "Space Waves",
        icon: "🌊",
        category: "Arcade",
        description: "Steer through a course full of obstacles.",
        url: "https://geometrydash3d.com/space-waves"
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
      } catch {}
    }

    function escapeHTML(value) {
      return String(value).replace(/[&<>"']/g, character => ({
        "&": "&amp;",
        "<": "&lt;",
        ">": "&gt;",
        '"': "&quot;",
        "'": "&#39;"
      })[character]);
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
        grid.innerHTML = '<div class="empty">No games found. Try another search.</div>';
        return;
      }

      filtered.forEach(game => {
        const isFavorite = favorites.includes(game.name);
        const card = document.createElement("article");
        card.className = "game-card";

        card.innerHTML = `
          <div class="game-top">
            <div class="game-icon">${game.icon}</div>
            <button class="favorite ${isFavorite ? "selected" : ""}"
              type="button" aria-label="Toggle favorite"
              title="Toggle favorite">${isFavorite ? "★" : "☆"}</button>
          </div>
          <h3>${escapeHTML(game.name)}</h3>
          <p>${escapeHTML(game.description)}</p>
          <div class="game-actions">
            <button class="btn btn-primary play-button" type="button">▶ Play Here</button>
            <a class="btn" href="${escapeHTML(game.url)}"
              target="_blank" rel="noopener noreferrer">↗ Open</a>
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

      frame.src = "about:blank";
      frame.src = game.url;

      playerStatus.textContent =
        `Loading ${game.name}. If it stays blank, click "Open Game" to play on the game's own website.`;

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
      renderGames();
    });

    renderGames();
  </script>
</body>
</html>

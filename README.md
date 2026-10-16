# NexPlay 
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>GameHub | Play Games</title>
  <meta name="description" content="A fun, searchable collection of browser games.">
  <style>
    :root {
      --blue: #3978f6;
      --blue-dark: #245bd0;
      --bg: #f5f7fb;
      --card: #ffffff;
      --text: #20283a;
      --muted: #697386;
      --border: #e2e7f0;
    }

    * { box-sizing: border-box; }

    body {
      margin: 0;
      background: var(--bg);
      color: var(--text);
      font-family: Arial, Helvetica, sans-serif;
    }

    header {
      padding: 28px 20px 22px;
      background: white;
      border-bottom: 1px solid var(--border);
    }

    .header-inner, main, footer {
      max-width: 1100px;
      margin: auto;
    }

    .brand {
      font-size: 29px;
      font-weight: 800;
      letter-spacing: -1px;
    }

    .brand span { color: var(--blue); }

    .subtitle {
      margin: 8px 0 20px;
      color: var(--muted);
    }

    .search-row {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
    }

    input, select {
      min-width: 0;
      padding: 12px 14px;
      border: 1px solid var(--border);
      border-radius: 10px;
      background: white;
      color: var(--text);
      font-size: 15px;
    }

    #search { flex: 1; min-width: 190px; }

    button {
      border: 0;
      border-radius: 10px;
      padding: 11px 14px;
      background: var(--blue);
      color: white;
      font-weight: 700;
      cursor: pointer;
    }

    button:hover { background: var(--blue-dark); }

    main { padding: 24px 20px 40px; }

    .toolbar {
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-wrap: wrap;
      gap: 12px;
      margin-bottom: 18px;
    }

    h2 { margin: 0; font-size: 21px; }

    #count {
      color: var(--muted);
      font-size: 14px;
      margin-top: 5px;
    }

    .filters {
      display: flex;
      gap: 8px;
      flex-wrap: wrap;
      margin: 18px 0 22px;
    }

    .filter {
      background: white;
      color: var(--text);
      border: 1px solid var(--border);
      border-radius: 22px;
      padding: 9px 14px;
    }

    .filter.active {
      background: var(--blue);
      color: white;
      border-color: var(--blue);
    }

    .grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
      gap: 16px;
    }

    .game {
      display: flex;
      flex-direction: column;
      min-height: 220px;
      padding: 18px;
      background: var(--card);
      border: 1px solid var(--border);
      border-radius: 16px;
      transition: transform .15s, box-shadow .15s;
    }

    .game:hover {
      transform: translateY(-3px);
      box-shadow: 0 8px 24px #1e315010;
    }

    .game-top {
      display: flex;
      justify-content: space-between;
      align-items: flex-start;
    }

    .game-icon {
      display: grid;
      place-items: center;
      width: 56px;
      height: 56px;
      border-radius: 14px;
      background: #edf3ff;
      font-size: 31px;
    }

    .favorite {
      background: transparent;
      color: #a0a8b8;
      font-size: 23px;
      padding: 2px 5px;
    }

    .favorite:hover { background: transparent; color: #e8a317; }
    .favorite.saved { color: #e8a317; }

    .game h3 { margin: 15px 0 7px; font-size: 18px; }

    .game p {
      margin: 0 0 16px;
      color: var(--muted);
      font-size: 14px;
      line-height: 1.45;
    }

    .game-bottom {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 8px;
      margin-top: auto;
    }

    .category {
      color: var(--muted);
      font-size: 12px;
      background: #f1f3f8;
      padding: 6px 9px;
      border-radius: 20px;
    }

    .play {
      text-decoration: none;
      background: var(--blue);
      color: white;
      padding: 9px 13px;
      border-radius: 9px;
      font-size: 13px;
      font-weight: 700;
    }

    .play:hover { background: var(--blue-dark); }

    .empty {
      grid-column: 1 / -1;
      text-align: center;
      background: white;
      border: 1px solid var(--border);
      padding: 40px 20px;
      border-radius: 14px;
      color: var(--muted);
    }

    footer {
      padding: 0 20px 28px;
      text-align: center;
      color: var(--muted);
      font-size: 13px;
    }

    @media (max-width: 500px) {
      .brand { font-size: 25px; }
      .grid { grid-template-columns: 1fr; }
      .toolbar { align-items: flex-start; }
    }
  </style>
</head>
<body>
  <header>
    <div class="header-inner">
      <div class="brand">🎮 Game<span>Hub</span></div>
      <p class="subtitle">Find a game. Click play. Have fun!</p>
      <div class="search-row">
        <input id="search" type="search" placeholder="Search games..." aria-label="Search games">
        <select id="sort" aria-label="Sort games">
          <option value="popular">Featured order</option>
          <option value="az">Name: A–Z</option>
          <option value="za">Name: Z–A</option>
        </select>
        <button id="favoritesOnly" type="button" aria-pressed="false">⭐ Favorites</button>
      </div>
    </div>
  </header>

  <main>
    <div class="toolbar">
      <div>
        <h2>Explore Games</h2>
        <div id="count" aria-live="polite"></div>
      </div>
    </div>

    <div class="filters" id="filters"></div>
    <section class="grid" id="games" aria-label="Game list"></section>
  </main>

  <footer>
    GameHub is a fan-made directory of links to browser games.
    Games are hosted by their respective websites.
  </footer>

  <script>
    const games = [
      {
        name: "Escape Road 3",
        category: "Racing",
        icon: "🚗",
        description: "Drive, dodge, and escape in a wild chase.",
        url: "https://poki.com/"
      },
      {
        name: "Cookie Clicker",
        category: "Idle",
        icon: "🍪",
        description: "Bake cookies and build your cookie empire.",
        url: "https://orteil.dashnet.org/cookieclicker/"
      },
      {
        name: "BitLife",
        category: "Simulation",
        icon: "🌟",
        description: "Make choices and explore a life simulator.",
        url: "https://bitlifeonline.com/"
      },
      {
        name: "Minecraft Classic",
        category: "Building",
        icon: "🧱",
        description: "Build with blocks in a classic Minecraft version.",
        url: "https://classic.minecraft.net/"
      },
      {
        name: "Geometry Dash",
        category: "Arcade",
        icon: "🟪",
        description: "Jump and dodge obstacles to the beat.",
        url: "https://www.crazygames.com/"
      },
      {
        name: "Retro Bowl",
        category: "Sports",
        icon: "🏈",
        description: "Build your team and chase the championship.",
        url: "https://poki.com/en/g/retro-bowl"
      },
      {
        name: "Slope",
        category: "Arcade",
        icon: "🟢",
        description: "Guide a rolling ball down a 3D track.",
        url: "https://slopegame.io/"
      },
      {
        name: "Baseball Bros",
        category: "Sports",
        icon: "⚾",
        description: "Play fast-paced baseball matches.",
        url: "https://baseballbros.io/"
      },
      {
        name: "Basket Bros",
        category: "Sports",
        icon: "🏀",
        description: "Shoot hoops and compete in basketball.",
        url: "https://basketbros.io/"
      },
      {
        name: "Football Bros",
        category: "Sports",
        icon: "🏈",
        description: "Play quick arcade-style football matches.",
        url: "https://footballbros.io/"
      },
      {
        name: "Moto X3M",
        category: "Racing",
        icon: "🏍️",
        description: "Race through challenging motorcycle tracks.",
        url: "https://poki.com/en/moto-x3m"
      },
      {
        name: "2048",
        category: "Puzzle",
        icon: "🔢",
        description: "Combine number tiles to reach 2048.",
        url: "https://play2048.co/"
      },
      {
        name: "Wordle",
        category: "Puzzle",
        icon: "🔤",
        description: "Guess the hidden five-letter word.",
        url: "https://www.nytimes.com/games/wordle/index.html"
      },
      {
        name: "Agar.io",
        category: "Multiplayer",
        icon: "🔵",
        description: "Grow your cell and compete with other players.",
        url: "https://agar.io/"
      },
      {
        name: "Slither.io",
        category: "Multiplayer",
        icon: "🐍",
        description: "Grow your snake and avoid other snakes.",
        url: "https://slither.io/"
      },
      {
        name: "Tetris",
        category: "Puzzle",
        icon: "🧩",
        description: "Fit falling blocks together.",
        url: "https://tetris.com/play-tetris"
      },
      {
        name: "Chess",
        category: "Strategy",
        icon: "♟️",
        description: "Play chess and practice your strategy.",
        url: "https://www.chess.com/play"
      },
      {
        name: "Little Alchemy 2",
        category: "Puzzle",
        icon: "🧪",
        description: "Combine elements to discover new items.",
        url: "https://littlealchemy2.com/"
      },
      {
        name: "Moto X3M Pool Party",
        category: "Racing",
        icon: "🌊",
        description: "Try more motorcycle stunt challenges.",
        url: "https://poki.com/"
      },
      {
        name: "Vex 3",
        category: "Platformer",
        icon: "🏃",
        description: "Run, jump, and avoid tricky obstacles.",
        url: "https://www.coolmathgames.com/"
      },
      {
        name: "Slice Master",
        category: "Arcade",
        icon: "🔪",
        description: "Slice objects in a quick arcade challenge.",
        url: "https://www.coolmathgames.com/"
      },
      {
        name: "Space Waves",
        category: "Arcade",
        icon: "🚀",
        description: "Steer through a wave-filled obstacle course.",
        url: "https://spacewaves.io/"
      },
      {
        name: "Smash Karts",
        category: "Multiplayer",
        icon: "🏎️",
        description: "Race and battle in kart arenas.",
        url: "https://smashkarts.io/"
      },
      {
        name: "Paper.io 2",
        category: "Multiplayer",
        icon: "🖍️",
        description: "Claim territory while protecting your trail.",
        url: "https://paper-io.com/"
      },
      {
        name: "Flappy Bird",
        category: "Arcade",
        icon: "🐤",
        description: "Navigate a bird through narrow gaps.",
        url: "https://flappybird.io/"
      },
      {
        name: "Stack",
        category: "Arcade",
        icon: "🟦",
        description: "Stack blocks as accurately as you can.",
        url: "https://www.crazygames.com/"
      },
      {
        name: "Drift Boss",
        category: "Racing",
        icon: "🚙",
        description: "Drift around corners and stay on the track.",
        url: "https://www.crazygames.com/"
      },
      {
        name: "Eggy Car",
        category: "Racing",
        icon: "🥚",
        description: "Drive carefully and keep your egg safe.",
        url: "https://www.crazygames.com/"
      },
      {
        name: "Friday Night Funkin'",
        category: "Music",
        icon: "🎤",
        description: "Play a rhythm game to the beat.",
        url: "https://www.newgrounds.com/"
      },
      {
        name: "Basketball Bros",
        category: "Sports",
        icon: "🏀",
        description: "Jump into quick basketball matches.",
        url: "https://basketbros.io/"
      }
    ];

    const gameContainer = document.getElementById("games");
    const searchInput = document.getElementById("search");
    const sortSelect = document.getElementById("sort");
    const filtersContainer = document.getElementById("filters");
    const count = document.getElementById("count");
    const favoritesButton = document.getElementById("favoritesOnly");

    let activeCategory = "All";
    let favoritesOnly = false;
    let favorites = [];

    try {
      favorites = JSON.parse(localStorage.getItem("gamehub-favorites") || "[]");
      if (!Array.isArray(favorites)) favorites = [];
    } catch {
      favorites = [];
    }

    const categories = [
      "All",
      ...new Set(games.map(game => game.category))
    ];

    function saveFavorites() {
      try {
        localStorage.setItem("gamehub-favorites", JSON.stringify(favorites));
      } catch {
        // The site still works if browser storage is unavailable.
      }
    }

    function buildFilters() {
      filtersContainer.innerHTML = "";

      categories.forEach(category => {
        const button = document.createElement("button");
        button.type = "button";
        button.className = "filter" +
          (activeCategory === category ? " active" : "");
        button.textContent = category;
        button.setAttribute("aria-pressed", activeCategory === category);

        button.addEventListener("click", () => {
          activeCategory = category;
          buildFilters();
          renderGames();
        });

        filtersContainer.appendChild(button);
      });
    }

    function renderGames() {
      const query = searchInput.value.trim().toLowerCase();

      let filtered = games.filter(game => {
        const matchesSearch = (
          game.name + " " + game.category + " " + game.description
        ).toLowerCase().includes(query);

        const matchesCategory =
          activeCategory === "All" || game.category === activeCategory;

        const matchesFavorite =
          !favoritesOnly || favorites.includes(game.name);

        return matchesSearch && matchesCategory && matchesFavorite;
      });

      if (sortSelect.value === "az") {
        filtered.sort((a, b) => a.name.localeCompare(b.name));
      } else if (sortSelect.value === "za") {
        filtered.sort((a, b) => b.name.localeCompare(a.name));
      }

      count.textContent =
        `${filtered.length} game${filtered.length === 1 ? "" : "s"} found`;

      gameContainer.innerHTML = "";

      if (filtered.length === 0) {
        const empty = document.createElement("div");
        empty.className = "empty";
        empty.textContent = "No games found. Try another search or category.";
        gameContainer.appendChild(empty);
        return;
      }

      filtered.forEach(game => {
        const isFavorite = favorites.includes(game.name);
        const card = document.createElement("article");
        card.className = "game";

        const top = document.createElement("div");
        top.className = "game-top";

        const icon = document.createElement("div");
        icon.className = "game-icon";
        icon.textContent = game.icon;
        icon.setAttribute("aria-hidden", "true");

        const favorite = document.createElement("button");
        favorite.className = "favorite" + (isFavorite ? " saved" : "");
        favorite.type = "button";
        favorite.textContent = isFavorite ? "★" : "☆";
        favorite.setAttribute(
          "aria-label",
          isFavorite ? "Remove from favorites" : "Add to favorites"
        );
        favorite.setAttribute("aria-pressed", isFavorite);

        favorite.addEventListener("click", () => {
          if (favorites.includes(game.name)) {
            favorites = favorites.filter(name => name !== game.name);
          } else {
            favorites.push(game.name);
          }
          saveFavorites();
          renderGames();
        });

        top.append(icon, favorite);

        const title = document.createElement("h3");
        title.textContent = game.name;

        const description = document.createElement("p");
        description.textContent = game.description;

        const bottom = document.createElement("div");
        bottom.className = "game-bottom";

        const category = document.createElement("span");
        category.className = "category";
        category.textContent = game.category;

        const play = document.createElement("a");
        play.className = "play";
        play.textContent = "Play game ↗";
        play.href = game.url;
        play.target = "_blank";
        play.rel = "noopener noreferrer";

        bottom.append(category, play);
        card.append(top, title, description, bottom);
        gameContainer.appendChild(card);
      });
    }

    searchInput.addEventListener("input", renderGames);
    sortSelect.addEventListener("change", renderGames);

    favoritesButton.addEventListener("click", () => {
      favoritesOnly = !favoritesOnly;
      favoritesButton.setAttribute("aria-pressed", favoritesOnly);
      favoritesButton.textContent = favoritesOnly
        ? "⭐ Show all games"
        : "⭐ Favorites";
      renderGames();
    });

    buildFilters();
    renderGames();
  </script>
</body>
</html>


<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>FERARUM</title>

  <style>
    body {
      margin: 0;
      background: #100e14;
      color: #f1eaf5;
      font-family: Georgia, serif;
      line-height: 1.6;
    }

    header {
      background: #1d1624;
      text-align: center;
      padding: 35px 15px;
      border-bottom: 1px solid #64466f;
    }

    h1 {
      margin: 0;
      letter-spacing: 3px;
      font-size: clamp(28px, 5vw, 44px);
    }

    header p {
      color: #c7b2d0;
    }

    nav {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 10px;
      padding: 15px;
      background: #19131e;
    }

    nav a {
      color: #f1e4f7;
      text-decoration: none;
      padding: 7px 13px;
      border: 1px solid #60466a;
      border-radius: 8px;
    }

    nav a:hover {
      background: #50355c;
    }

    main {
      max-width: 850px;
      margin: auto;
      padding: 24px 16px;
    }

    section {
      background: #1b1721;
      border: 1px solid #45334e;
      border-radius: 12px;
      padding: 22px;
      margin-bottom: 20px;
    }

    h2 {
      color: #ddb8ed;
    }

    .news-date {
      color: #bfa5cc;
      font-size: 14px;
    }

    button {
      cursor: pointer;
      color: white;
      background: #70477e;
      border: 0;
      border-radius: 8px;
      padding: 10px 16px;
      font: inherit;
    }

    button:hover {
      background: #8c5c9d;
    }

    input {
      background: #100e14;
      color: white;
      border: 1px solid #80628b;
      border-radius: 8px;
      padding: 10px;
      width: 100px;
      font: inherit;
    }

    footer {
      text-align: center;
      padding: 25px;
      color: #a99aaa;
    }
  </style>
</head>

<body>
  <header>
    <h1>ТЁМНЫЙ АРХИВ</h1>
    <p>Новости, тайны и маленькие игры</p>
  </header>

  <nav>
    <a href="#home">Главная</a>
    <a href="#news">Новости</a>
    <a href="#games">Игры</a>
    <a href="#about">О проекте</a>
  </nav>

  <main>
    <section id="home">
      <h2>Добро пожаловать</h2>
      <p>
        Это мой собственный сайт.
        Здесь будут новости, интерактивы и игры.
      </p>
      <button id="welcomeButton">Открыть сообщение</button>
      <p id="welcomeMessage"></p>
    </section>

    <section id="news">
      <h2>Новости</h2>

      <article>
        <p class="news-date">28 октября 2026</p>
        <h3>Архив открыт!</h3>
        <p>На сайте появилась первая запись.
        Скоро здесь будут новые разделы.</p>
      </article>

      <article>
        <p class="news-date">27 октября 2026</p>
        <h3>Начало проекта</h3>
        <p>Началась работа над дизайном и играми.</p>
      </article>
    </section>

    <section id="games">
      <h2>Игра: угадай число</h2>
      <p>Я загадал число от 1 до 10. Попробуй угадать!</p>

      <input id="guessInput" type="number"
        min="1" max="10" placeholder="1–10">

      <button id="guessButton">Проверить</button>
      <p id="gameMessage" aria-live="polite"></p>
      <p>Очки: <span id="score">0</span></p>
      <button id="resetButton">Новая игра</button>
    </section>

    <section id="about">
      <h2>О проекте</h2>
      <p>
        Здесь можно рассказать историю проекта,
        представить команду и добавить контакты.
      </p>
    </section>
  </main>

  <footer>
    © 2026 — Тёмный архив
  </footer>

  <script>
    // Интерактивное приветствие
    const welcomeButton = document.querySelector("#welcomeButton");
    const welcomeMessage = document.querySelector("#welcomeMessage");

    welcomeButton.addEventListener("click", function () {
      welcomeMessage.textContent =
        "Добро пожаловать! Исследуй сайт и попробуй игру.";
    });

    // Мини-игра
    const guessInput = document.querySelector("#guessInput");
    const guessButton = document.querySelector("#guessButton");
    const gameMessage = document.querySelector("#gameMessage");
    const scoreDisplay = document.querySelector("#score");
    const resetButton = document.querySelector("#resetButton");

    let secretNumber = randomNumber();
    let score = 0;
    let finished = false;

    function randomNumber() {
      return Math.floor(Math.random() * 10) + 1;
    }

    guessButton.addEventListener("click", function () {
      if (finished) {
        gameMessage.textContent =
          "Начни новую игру, чтобы попробовать снова.";
        return;
      }

      const guess = Number(guessInput.value);

      if (!guessInput.value || guess < 1 ||
          guess > 10 || !Number.isInteger(guess)) {
        gameMessage.textContent =
          "Введи целое число от 1 до 10.";
        return;
      }

      if (guess === secretNumber) {
        score += 1;
        scoreDisplay.textContent = score;
        gameMessage.textContent =
          "Верно! Ты угадал число!";
        finished = true;
      } else if (guess < secretNumber) {
        gameMessage.textContent = "Моё число больше!";
      } else {
        gameMessage.textContent = "Моё число меньше!";
      }
    });

    resetButton.addEventListener("click", function () {
      secretNumber = randomNumber();
      finished = false;
      guessInput.value = "";
      gameMessage.textContent = "Новое число загадано!";
    });
  </script>
</body>
</html>

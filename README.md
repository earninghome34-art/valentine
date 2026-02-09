<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Be My Valentine 💖</title>

  <style>
    :root {
      --bg: #ffd6e7;
      --primary: #ff5c8a;
      --secondary: #ff8fb1;
      --text: #7a003c;
      --white: #ffffff;
    }

    * {
      box-sizing: border-box;
      font-family: "Segoe UI", system-ui, sans-serif;
    }

    body {
      margin: 0;
      min-height: 100vh;
      background: linear-gradient(135deg, #ffe1ec, var(--bg));
      display: flex;
      align-items: center;
      justify-content: center;
      overflow: hidden;
    }

    .container {
      text-align: center;
      padding: 2rem;
    }

    h1 {
      color: var(--text);
      font-size: clamp(1.8rem, 5vw, 2.6rem);
      margin-bottom: 2rem;
    }

    .buttons {
      display: flex;
      gap: 1.5rem;
      justify-content: center;
      flex-wrap: wrap;
    }

    button {
      padding: 0.9rem 2rem;
      font-size: 1.1rem;
      border-radius: 999px;
      border: none;
      cursor: pointer;
      transition: transform 0.2s ease, box-shadow 0.2s ease;
      box-shadow: 0 10px 25px rgba(0,0,0,0.15);
    }

    button:active {
      transform: scale(0.95);
    }

    #yesBtn {
      background: var(--primary);
      color: var(--white);
    }

    #yesBtn:hover {
      background: var(--secondary);
    }

    #noBtn {
      background: #fff;
      color: var(--text);
      position: fixed;
      z-index: 1000;
    }

    /* SUCCESS PAGE */
    .success {
      display: none;
      text-align: center;
      animation: fadeIn 0.8s ease forwards;
    }

    .success h1 {
      margin-bottom: 1rem;
    }

    .hearts {
      position: fixed;
      inset: 0;
      pointer-events: none;
      overflow: hidden;
    }

    .heart {
      position: absolute;
      font-size: 1.2rem;
      animation: floatUp 4s linear infinite;
      opacity: 0.8;
    }

    @keyframes floatUp {
      from {
        transform: translateY(100vh) scale(1);
        opacity: 1;
      }
      to {
        transform: translateY(-10vh) scale(1.4);
        opacity: 0;
      }
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }
  </style>
</head>

<body>

  <!-- MAIN PAGE -->
  <div class="container" id="main">
    <h1 id="heading">Ankita will you be my Valentine? ❤️</h1>

    <div class="buttons">
      <button id="yesBtn">Yes 💖</button>
      <button id="noBtn">No 💔</button>
    </div>
  </div>

  <!-- SUCCESS PAGE -->
  <div class="container success" id="success">
    <h1>Yay! You just made me the happiest person 💕</h1>
    <p>Happy Valentine’s Day ❤️</p>
  </div>

  <div class="hearts" id="hearts"></div>

  <script>
    const noBtn = document.getElementById("noBtn");
    const yesBtn = document.getElementById("yesBtn");
    const main = document.getElementById("main");
    const success = document.getElementById("success");
    const hearts = document.getElementById("hearts");

    function moveNoButton() {
      const btnRect = noBtn.getBoundingClientRect();
      const padding = 10;

      const maxX = window.innerWidth - btnRect.width - padding;
      const maxY = window.innerHeight - btnRect.height - padding;

      const x = Math.random() * maxX;
      const y = Math.random() * maxY;

      noBtn.style.left = `${x}px`;
      noBtn.style.top = `${y}px`;
    }

    // Desktop hover
    noBtn.addEventListener("mouseenter", moveNoButton);

    // Mobile tap
    noBtn.addEventListener("touchstart", (e) => {
      e.preventDefault();
      moveNoButton();
    });

    // Click safety
    noBtn.addEventListener("click", (e) => {
      e.preventDefault();
      moveNoButton();
    });

    // Initial random placement
    moveNoButton();

    yesBtn.addEventListener("click", () => {
      main.style.display = "none";
      success.style.display = "block";
      startHearts();
    });

    function startHearts() {
      setInterval(() => {
        const heart = document.createElement("div");
        heart.className = "heart";
        heart.textContent = "❤️";
        heart.style.left = Math.random() * 100 + "vw";
        heart.style.animationDuration = 3 + Math.random() * 2 + "s";
        hearts.appendChild(heart);

        setTimeout(() => heart.remove(), 5000);
      }, 250);
    }
  </script>

</body>
</html>

# ilon-oyini.html
[ilon-oyini (2).html](https://github.com/user-attachments/files/30628111/ilon-oyini.2.html)
<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>Ilon O'yini</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      -webkit-tap-highlight-color: transparent;
    }
    body {
      background: linear-gradient(135deg, #0f2027, #203a43, #2c5364);
      min-height: 100vh;
      min-height: 100dvh;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      font-family: 'Segoe UI', system-ui, sans-serif;
      color: #fff;
      overflow: hidden;
      user-select: none;
      -webkit-user-select: none;
      touch-action: manipulation;
      padding: 10px 0;
    }
    h1 {
      font-size: 1.8rem;
      margin-bottom: 8px;
      text-shadow: 0 2px 8px rgba(0,0,0,0.4);
      letter-spacing: 1px;
    }
    .score-board {
      display: flex;
      gap: 24px;
      margin-bottom: 12px;
      font-size: 1.15rem;
      font-weight: 600;
    }
    .score-board span {
      background: rgba(255,255,255,0.12);
      padding: 6px 16px;
      border-radius: 20px;
      backdrop-filter: blur(4px);
    }
    #gameCanvas {
      background: #111;
      border-radius: 12px;
      box-shadow: 0 10px 40px rgba(0,0,0,0.5), 0 0 0 3px rgba(255,255,255,0.08);
      max-width: 95vw;
      max-height: 55vh;
      width: 100%;
      height: auto;
      touch-action: none;
    }
    .controls {
      margin-top: 12px;
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 8px;
      width: 100%;
      max-width: 320px;
      padding: 0 10px;
    }
    .btn {
      background: linear-gradient(145deg, #00c853, #00a844);
      border: none;
      color: white;
      font-size: 1.05rem;
      font-weight: 600;
      padding: 12px 32px;
      border-radius: 30px;
      cursor: pointer;
      box-shadow: 0 4px 15px rgba(0,200,83,0.35);
      transition: transform 0.15s, box-shadow 0.15s;
    }
    .btn:active {
      transform: scale(0.96);
    }
    .btn.secondary {
      background: linear-gradient(145deg, #ff6b6b, #ee5253);
      box-shadow: 0 4px 15px rgba(238,82,83,0.35);
    }
    .dpad {
      display: grid;
      grid-template-columns: 70px 70px 70px;
      grid-template-rows: 70px 70px 70px;
      gap: 8px;
      margin-top: 6px;
    }
    .dpad button {
      width: 70px;
      height: 70px;
      border: none;
      border-radius: 16px;
      background: rgba(255,255,255,0.18);
      color: white;
      font-size: 1.8rem;
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: center;
      transition: background 0.1s;
      -webkit-user-select: none;
      user-select: none;
      touch-action: manipulation;
    }
    .dpad button:active {
      background: rgba(255,255,255,0.35);
      transform: scale(0.95);
    }
    .up { grid-column: 2; grid-row: 1; }
    .left { grid-column: 1; grid-row: 2; }
    .right { grid-column: 3; grid-row: 2; }
    .down { grid-column: 2; grid-row: 3; }
    .hint {
      margin-top: 8px;
      font-size: 0.8rem;
      opacity: 0.7;
      text-align: center;
    }

    /* Telefon uchun maxsus */
    @media (max-width: 500px) {
      h1 {
        font-size: 1.4rem;
        margin-bottom: 6px;
      }
      .score-board {
        gap: 12px;
        font-size: 1rem;
        margin-bottom: 8px;
      }
      .score-board span {
        padding: 5px 12px;
      }
      #gameCanvas {
        max-height: 50vh;
      }
      .dpad {
        grid-template-columns: 76px 76px 76px;
        grid-template-rows: 76px 76px 76px;
        gap: 10px;
      }
      .dpad button {
        width: 76px;
        height: 76px;
        font-size: 2rem;
        border-radius: 18px;
      }
    }
    .overlay {
      position: absolute;
      inset: 0;
      background: rgba(0,0,0,0.75);
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      border-radius: 12px;
      z-index: 10;
    }
    .overlay h2 {
      font-size: 2rem;
      margin-bottom: 8px;
    }
    .overlay p {
      margin-bottom: 20px;
      font-size: 1.1rem;
      opacity: 0.9;
    }
    .hidden { display: none !important; }
  </style>
</head>
<body>
  <h1>🐍 Ilon O'yini</h1>
  <div class="score-board">
    <span>Ball: <strong id="score">0</strong></span>
    <span>Eng yaxshi: <strong id="highScore">0</strong></span>
  </div>

  <div style="position: relative;">
    <canvas id="gameCanvas" width="400" height="400"></canvas>
    <div id="startOverlay" class="overlay hidden">
      <h2>Ilon O'yini</h2>
      <p>Boshlash uchun tugmani bosing</p>
      <button class="btn" id="startBtn">Boshlash</button>
    </div>
    <div id="gameOverOverlay" class="overlay hidden">
      <h2>O'yin tugadi!</h2>
      <p>Ballingiz: <strong id="finalScore">0</strong></p>
      <button class="btn" id="restartBtn">Qayta o'ynash</button>
    </div>
  </div>

  <div class="controls">
    <div class="dpad">
      <button class="up" data-dir="up">▲</button>
      <button class="left" data-dir="left">◀</button>
      <button class="right" data-dir="right">▶</button>
      <button class="down" data-dir="down">▼</button>
    </div>
    <p class="hint">Klaviatura: ← → ↑ ↓ yoki WASD</p>
  </div>

  <script>
    const canvas = document.getElementById('gameCanvas');
    const ctx = canvas.getContext('2d');
    const scoreEl = document.getElementById('score');
    const highScoreEl = document.getElementById('highScore');
    const finalScoreEl = document.getElementById('finalScore');
    const startOverlay = document.getElementById('startOverlay');
    const gameOverOverlay = document.getElementById('gameOverOverlay');
    const startBtn = document.getElementById('startBtn');
    const restartBtn = document.getElementById('restartBtn');

    const GRID = 20;
    const COLS = canvas.width / GRID;
    const ROWS = canvas.height / GRID;

    let snake, direction, nextDirection, food, score, highScore, gameLoop, speed, isRunning;

    try {
      highScore = parseInt(localStorage.getItem('snakeHighScore') || '0');
    } catch (e) {
      highScore = 0;
    }
    highScoreEl.textContent = highScore;

    function init() {
      snake = [{ x: 10, y: 10 }];
      direction = { x: 1, y: 0 };
      nextDirection = { x: 1, y: 0 };
      score = 0;
      speed = 200;
      isRunning = false;
      scoreEl.textContent = '0';
      placeFood();
      draw();
    }

    function placeFood() {
      let valid = false;
      while (!valid) {
        food = {
          x: Math.floor(Math.random() * COLS),
          y: Math.floor(Math.random() * ROWS)
        };
        valid = !snake.some(s => s.x === food.x && s.y === food.y);
      }
    }

    function draw() {
      // Fon
      ctx.fillStyle = '#0d1117';
      ctx.fillRect(0, 0, canvas.width, canvas.height);

      // To'r (yengil)
      ctx.strokeStyle = 'rgba(255,255,255,0.03)';
      ctx.lineWidth = 1;
      for (let i = 0; i <= COLS; i++) {
        ctx.beginPath();
        ctx.moveTo(i * GRID, 0);
        ctx.lineTo(i * GRID, canvas.height);
        ctx.stroke();
      }
      for (let i = 0; i <= ROWS; i++) {
        ctx.beginPath();
        ctx.moveTo(0, i * GRID);
        ctx.lineTo(canvas.width, i * GRID);
        ctx.stroke();
      }

      // Oziq
      ctx.fillStyle = '#ff4757';
      ctx.shadowColor = '#ff4757';
      ctx.shadowBlur = 12;
      roundRect(food.x * GRID + 2, food.y * GRID + 2, GRID - 4, GRID - 4, 6);
      ctx.shadowBlur = 0;

      // Ilon
      snake.forEach((seg, i) => {
        const t = i / snake.length;
        const r = Math.floor(50 + t * 30);
        const g = Math.floor(200 - t * 80);
        const b = Math.floor(80 + t * 40);
        ctx.fillStyle = `rgb(${r},${g},${b})`;
        if (i === 0) {
          ctx.shadowColor = '#2ed573';
          ctx.shadowBlur = 10;
        }
        roundRect(seg.x * GRID + 1, seg.y * GRID + 1, GRID - 2, GRID - 2, 5);
        ctx.shadowBlur = 0;

        // Ko'zlar (bosh)
        if (i === 0) {
          ctx.fillStyle = '#fff';
          const eyeSize = 3;
          if (direction.x === 1) {
            ctx.beginPath(); ctx.arc(seg.x * GRID + 14, seg.y * GRID + 6, eyeSize, 0, Math.PI * 2); ctx.fill();
            ctx.beginPath(); ctx.arc(seg.x * GRID + 14, seg.y * GRID + 14, eyeSize, 0, Math.PI * 2); ctx.fill();
          } else if (direction.x === -1) {
            ctx.beginPath(); ctx.arc(seg.x * GRID + 6, seg.y * GRID + 6, eyeSize, 0, Math.PI * 2); ctx.fill();
            ctx.beginPath(); ctx.arc(seg.x * GRID + 6, seg.y * GRID + 14, eyeSize, 0, Math.PI * 2); ctx.fill();
          } else if (direction.y === -1) {
            ctx.beginPath(); ctx.arc(seg.x * GRID + 6, seg.y * GRID + 6, eyeSize, 0, Math.PI * 2); ctx.fill();
            ctx.beginPath(); ctx.arc(seg.x * GRID + 14, seg.y * GRID + 6, eyeSize, 0, Math.PI * 2); ctx.fill();
          } else {
            ctx.beginPath(); ctx.arc(seg.x * GRID + 6, seg.y * GRID + 14, eyeSize, 0, Math.PI * 2); ctx.fill();
            ctx.beginPath(); ctx.arc(seg.x * GRID + 14, seg.y * GRID + 14, eyeSize, 0, Math.PI * 2); ctx.fill();
          }
        }
      });
    }

    function roundRect(x, y, w, h, r) {
      ctx.beginPath();
      ctx.moveTo(x + r, y);
      ctx.arcTo(x + w, y, x + w, y + h, r);
      ctx.arcTo(x + w, y + h, x, y + h, r);
      ctx.arcTo(x, y + h, x, y, r);
      ctx.arcTo(x, y, x + w, y, r);
      ctx.closePath();
      ctx.fill();
    }

    function update() {
      direction = { ...nextDirection };
      const head = {
        x: snake[0].x + direction.x,
        y: snake[0].y + direction.y
      };

      // Devor bilan to'qnashuv
      if (head.x < 0 || head.x >= COLS || head.y < 0 || head.y >= ROWS) {
        gameOver();
        return;
      }

      // O'ziga urilish
      if (snake.some(s => s.x === head.x && s.y === head.y)) {
        gameOver();
        return;
      }

      snake.unshift(head);

      if (head.x === food.x && head.y === food.y) {
        score += 10;
        scoreEl.textContent = score;
        if (score > highScore) {
          highScore = score;
          highScoreEl.textContent = highScore;
          try {
            localStorage.setItem('snakeHighScore', highScore);
          } catch (e) {}
        }
        // Tezlikni sekin oshirish
        if (speed > 80) {
          speed -= 2;
          clearInterval(gameLoop);
          gameLoop = setInterval(update, speed);
        }
        placeFood();
      } else {
        snake.pop();
      }

      draw();
    }

    function gameOver() {
      isRunning = false;
      clearInterval(gameLoop);
      finalScoreEl.textContent = score;
      gameOverOverlay.classList.remove('hidden');
    }

    function startGame() {
      init();
      startOverlay.classList.add('hidden');
      gameOverOverlay.classList.add('hidden');
      isRunning = true;
      gameLoop = setInterval(update, speed);
    }

    function setDirection(dir) {
      if (!isRunning) return;
      const opposites = {
        up: 'down', down: 'up', left: 'right', right: 'left'
      };
      const current = direction.x === 1 ? 'right' : direction.x === -1 ? 'left' : direction.y === -1 ? 'up' : 'down';
      if (opposites[dir] === current) return;

      if (dir === 'up') nextDirection = { x: 0, y: -1 };
      if (dir === 'down') nextDirection = { x: 0, y: 1 };
      if (dir === 'left') nextDirection = { x: -1, y: 0 };
      if (dir === 'right') nextDirection = { x: 1, y: 0 };
    }

    // Klaviatura
    document.addEventListener('keydown', e => {
      const key = e.key.toLowerCase();
      if (['arrowup', 'w'].includes(key)) { e.preventDefault(); setDirection('up'); }
      if (['arrowdown', 's'].includes(key)) { e.preventDefault(); setDirection('down'); }
      if (['arrowleft', 'a'].includes(key)) { e.preventDefault(); setDirection('left'); }
      if (['arrowright', 'd'].includes(key)) { e.preventDefault(); setDirection('right'); }
      if (key === ' ' || key === 'enter') {
        if (!isRunning) startGame();
      }
    });

    // D-pad
    document.querySelectorAll('.dpad button').forEach(btn => {
      btn.addEventListener('click', () => setDirection(btn.dataset.dir));
      btn.addEventListener('touchstart', e => {
        e.preventDefault();
        setDirection(btn.dataset.dir);
      });
    });

    startBtn.addEventListener('click', startGame);
    restartBtn.addEventListener('click', startGame);

    // Sahifa ochilganda darhol o'yinni boshlash
    startGame();
  </script>
</body>
</html>

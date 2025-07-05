# Habibjane
<html lang="ru">
<head>
  <meta charset="UTF-8" />
  <title>MINES 1WIN STYLE ⭐️ + число бомб</title>
  <style>
    body {
      background: #111;
      color: #fff;
      font-family: Arial, sans-serif;
      text-align: center;
      padding: 20px;
    }
    h2 {
      margin-top: 10px;
    }
    .controls {
      margin: 20px;
    }
    button {
      background: #000;
      border: 2px solid #555;
      border-radius: 8px;
      color: #00bfff;
      font-size: 16px;
      padding: 10px 20px;
      margin: 0 10px;
      cursor: pointer;
      transition: background-color 0.3s ease, box-shadow 0.3s ease;
    }
    button:disabled {
      opacity: 0.4;
      cursor: default;
    }
    button:hover:not(:disabled) {
      background-color: #111;
      box-shadow: 0 0 10px #00bfff;
    }
    .grid {
      display: grid;
      grid-template-columns: repeat(5, 60px);
      grid-gap: 10px;
      justify-content: center;
      margin-top: 20px;
      border: 3px solid #222;
      border-radius: 12px;
      padding: 10px;
      background: #0a0a0a;
      position: relative;
    }
    .cell {
      width: 60px;
      height: 60px;
      background: #000;
      border: 2px solid #444;
      border-radius: 10px;
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: center;
      transition: box-shadow 0.5s ease, transform 0.3s ease;
      font-size: 26px;
    }
    .cell.opened {
      box-shadow: 0 0 8px rgba(0, 191, 255, 0.2);
      transform: scale(1.05);
    }
    .star {
      color: #00bfff;
      text-shadow: 0 0 6px #00bfff, 0 0 12px #00bfff, 0 0 18px #00bfff;
      opacity: 0;
      animation: fadeIn 0.6s ease forwards;
    }
    @keyframes fadeIn {
      from { opacity: 0; transform: scale(0.7); }
      to { opacity: 1; transform: scale(1); }
    }
    .input-container {
      position: absolute;
      bottom: -70px;
      left: 50%;
      transform: translateX(-50%);
      background: #000;
      border: 2px solid #444;
      border-radius: 10px;
      padding: 5px 10px;
      display: flex;
      align-items: center;
      gap: 15px;
      color: #00bfff;
      font-weight: bold;
      user-select: none;
      box-shadow: 0 0 6px #00bfff;
      font-size: 16px;
    }
    .input-container label {
      margin-right: 5px;
    }
    .input-container input {
      width: 50px;
      padding: 5px;
      font-size: 18px;
      border-radius: 6px;
      border: 1px solid #00bfff;
      background: #111;
      color: #00bfff;
      text-align: center;
      outline: none;
      transition: border-color 0.3s ease;
    }
    .input-container input:focus {
      border-color: #1e90ff;
      box-shadow: 0 0 5px #1e90ff;
    }
  </style>
</head>
<body>

  <h2>🧨 MINES - 1WIN Style ⭐️ + число бомб</h2>

  <div class="controls">
    <button id="signalBtn">Получить сигнал</button>
    <button id="startBtn" disabled>Старт</button>
  </div>

  <div class="grid" id="grid"></div>

  <div class="input-container" title="Выберите количество сигнала и число бомб (только для учета)">
    <label for="mineCount">Сигнал:</label>
    <input type="number" id="mineCount" min="1" max="10" value="4" />
    <label for="bombCount">Бомбы:</label>
    <input type="number" id="bombCount" min="0" max="10" value="0" />
  </div>

<script>
  const signalBtn = document.getElementById('signalBtn');
  const startBtn = document.getElementById('startBtn');
  const grid = document.getElementById('grid');
  const mineCountInput = document.getElementById('mineCount');
  const bombCountInput = document.getElementById('bombCount');

  let cells = [];

  // Создаем 25 ячеек
  for (let i = 0; i < 25; i++) {
    const cell = document.createElement('div');
    cell.className = 'cell';
    grid.appendChild(cell);
    cells.push(cell);
  }

  function getMineCount() {
    let val = parseInt(mineCountInput.value);
    if (isNaN(val) || val < 1) return 1;
    if (val > 10) return 10;
    return val;
  }

  function getBombCount() {
    let val = parseInt(bombCountInput.value);
    if (isNaN(val) || val < 0) return 0;
    if (val > 10) return 10;
    return val;
  }

  signalBtn.onclick = () => {
    signalBtn.disabled = true;
    startBtn.disabled = false;

    // Закрываем все ячейки
    cells.forEach(cell => {
      cell.innerHTML = '';
      cell.classList.remove('opened');
    });
  };

  startBtn.onclick = () => {
    startBtn.disabled = true;

    const minesCount = getMineCount();
    const bombsCount = getBombCount();

    const available = cells.filter(cell => !cell.classList.contains('opened'));
    const shuffled = available.sort(() => 0.5 - Math.random());
    const totalToOpen = minesCount; // Только мины визуально открываются

    const selectedMines = shuffled.slice(0, minesCount);

    selectedMines.forEach((cell, index) => {
      setTimeout(() => {
        const star = document.createElement('span');
        star.className = 'star';
        star.innerText = '⭐️';
        cell.appendChild(star);
        cell.classList.add('opened');
      }, index * 900);
    });

    setTimeout(() => {
      signalBtn.disabled = false;
    }, minesCount * 900 + 500);
  };
</script>

</body>
</html>

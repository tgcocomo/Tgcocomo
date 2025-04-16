<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Calculator</title>
  <style>
    body {
      background: #121212;
      color: #fff;
      font-family: 'Arial', sans-serif;
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 50px;
    }

    h1 {
      background: linear-gradient(90deg, #ff4b2b, #ff416c, #3b82f6, #10b981);
      -webkit-background-clip: text;
      color: transparent;
      font-size: 32px;
      margin-bottom: 20px;
    }

    .calculator {
      background: #1e1e1e;
      padding: 20px;
      border-radius: 15px;
      box-shadow: 0 0 15px #00f7ff;
    }

    .display {
      background: #000;
      color: #0f0;
      font-size: 24px;
      padding: 10px;
      border-radius: 5px;
      margin-bottom: 15px;
      text-align: right;
    }

    .buttons {
      display: grid;
      grid-template-columns: repeat(4, 60px);
      gap: 10px;
    }

    button {
      padding: 15px;
      font-size: 18px;
      border: none;
      border-radius: 8px;
      background: linear-gradient(145deg, #3a3a3a, #222);
      color: #fff;
      cursor: pointer;
      transition: all 0.2s ease;
    }

    button:hover {
      background: #0ff;
      color: #000;
    }

    .equal {
      background: #00f7ff;
      color: #000;
    }
  </style>
</head>
<body>

  <h1>Developed by Hamza Mughal</h1>

  <div class="calculator">
    <div class="display" id="display">0</div>
    <div class="buttons">
      <button onclick="clearDisplay()">C</button>
      <button onclick="append('%')">%</button>
      <button onclick="append('/')">/</button>
      <button onclick="append('*')">*</button>

      <button onclick="append('7')">7</button>
      <button onclick="append('8')">8</button>
      <button onclick="append('9')">9</button>
      <button onclick="append('-')">-</button>

      <button onclick="append('4')">4</button>
      <button onclick="append('5')">5</button>
      <button onclick="append('6')">6</button>
      <button onclick="append('+')">+</button>

      <button onclick="append('1')">1</button>
      <button onclick="append('2')">2</button>
      <button onclick="append('3')">3</button>
      <button onclick="calculate()" class="equal">=</button>

      <button onclick="append('0')" style="grid-column: span 2;">0</button>
      <button onclick="append('.')">.</button>
    </div>
  </div>

  <script>
    let display = document.getElementById('display');

    function append(value) {
      if (display.innerText === '0') {
        display.innerText = value;
      } else {
        display.innerText += value;
      }
    }

    function clearDisplay() {
      display.innerText = '0';
    }

    function calculate() {
      try {
        display.innerText = eval(display.innerText);
      } catch {
        display.innerText = 'Error';
      }
    }
  </script>

</body>
</html>

<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>calculator</title>
  <style>
    :root {
      --primary-bg: #000;
      --accent-color: #00bfff; /* Changed from neon green to neon blue */
      --secondary-bg: #111;
      --hover-bg: rgba(0, 191, 255, 0.2);
      --text-color: #fff;
      --btn-shadow: 0 0 10px rgba(0, 191, 255, 0.5);
      --btn-active-shadow: 0 0 5px rgba(0, 191, 255, 0.8);
    }

    body {
      margin: 0;
      padding: 20px;
      background: linear-gradient(135deg, var(--primary-bg) 0%, #221122 100%);
      color: var(--text-color);
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      min-height: 100vh;
      position: relative;
      animation: fadeIn 1s ease-in;
    }

    @keyframes fadeIn {
      from {
        opacity: 0;
      }
      to {
        opacity: 1;
      }
    }

    body::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: radial-gradient(
        circle at 50% 50%,
        rgba(0, 191, 255, 0.05) 0%,
        transparent 70%
      );
      pointer-events: none;
      z-index: -1;
    }

    .title {
      font-size: 2.5rem;
      margin-bottom: 20px;
      text-align: center;
      color: var(--accent-color);
      text-shadow: 0 0 20px var(--accent-color);
      font-weight: 300;
      font-family: 'Arial', sans-serif;
    }

    .calculator {
      background: rgba(17, 17, 17, 0.9);
      backdrop-filter: blur(15px);
      border: 1px solid var(--accent-color);
      border-radius: 15px;
      padding: 20px;
      box-shadow: 0 10px 40px rgba(0, 191, 255, 0.2),
        inset 0 0 20px rgba(0, 191, 255, 0.1);
      width: 100%;
      max-width: 350px;
      transition: box-shadow 0.3s ease;
    }

    .calculator:hover {
      box-shadow: 0 15px 50px rgba(0, 191, 255, 0.3),
        inset 0 0 25px rgba(0, 191, 255, 0.15);
    }

    .display {
      background: rgba(0, 0, 0, 0.8);
      border: 1px solid var(--accent-color);
      border-radius: 10px;
      padding: 15px;
      margin-bottom: 20px;
      font-size: 1.8rem;
      text-align: right;
      word-wrap: break-word;
      color: var(--accent-color);
      font-family: 'Courier New', monospace;
      box-shadow: inset 0 0 10px rgba(0, 191, 255, 0.3);
      height: 60px;
      overflow: hidden;
    }

    .buttons {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 10px;
    }

    .btn {
      background: transparent;
      border: 2px solid var(--accent-color);
      border-radius: 50%;
      width: 70px;
      height: 70px;
      display: flex;
      align-items: center;
      justify-content: center;
      cursor: pointer;
      transition: all 0.2s ease-in-out;
      font-size: 1.5rem;
      color: var(--accent-color);
      font-weight: bold;
      position: relative;
      overflow: hidden;
    }

    .btn::before {
      content: '';
      position: absolute;
      top: 50%;
      left: 50%;
      width: 0;
      height: 0;
      background: var(--accent-color);
      border-radius: 50%;
      transform: translate(-50%, -50%);
      transition: width 0.3s, height 0.3s;
      z-index: -1;
    }

    .btn:hover::before {
      width: 100%;
      height: 100%;
    }

    .btn:hover {
      box-shadow: var(--btn-shadow);
      color: var(--primary-bg);
      transform: scale(1.05);
    }

    .btn:active {
      transform: scale(0.95);
      box-shadow: var(--btn-active-shadow);
    }

    .btn.clear {
      background: rgba(255, 0, 0, 0.3);
      border-color: #ff0000;
      color: #fff;
    }

    .btn.clear:hover {
      box-shadow: 0 0 10px rgba(255, 0, 0, 0.5);
      background: #ff0000;
      color: #fff;
    }

    .btn.equals {
      background: var(--accent-color);
      color: var(--primary-bg);
    }

    .btn.equals:hover {
      box-shadow: var(--btn-shadow);
      background: var(--accent-color);
      color: var(--primary-bg);
    }

    @media (max-width: 600px) {
      .title {
        font-size: 2rem;
      }
      .display {
        font-size: 1.5rem;
        height: 50px;
      }
      .btn {
        width: 55px;
        height: 55px;
        font-size: 1.2rem;
      }
      .calculator {
        padding: 15px;
        max-width: 280px;
      }
    }
  </style>
</head>
<body>
  <h1 class="title">Calculator</h1>
  <div class="calculator">
    <div class="display" id="display">0</div>
    <div class="buttons">
      <button class="btn clear" id="clear">C</button>
      <button class="btn operator" id="percent">%</button>
      <button class="btn operator" id="divide">/</button>
      <button class="btn operator" id="multiply">*</button>
      <button class="btn number" id="seven">7</button>
      <button class="btn number" id="eight">8</button>
      <button class="btn number" id="nine">9</button>
      <button class="btn operator" id="subtract">-</button>
      <button class="btn number" id="four">4</button>
      <button class="btn number" id="five">5</button>
      <button class="btn number" id="six">6</button>
      <button class="btn operator" id="add">+</button>
      <button class="btn number" id="one">1</button>
      <button class="btn number" id="two">2</button>
      <button class="btn number" id="three">3</button>
      <button class="btn number zero" id="zero">0</button>
      <button class="btn number" id="decimal">.</button>
      <button class="btn equals" id="equals">=</button>
    </div>
  </div>

  <script>
    let display = document.getElementById('display');
    let expression = '';

    document.querySelectorAll('.btn').forEach(btn => {
      btn.addEventListener('click', function () {
        const value = this.textContent;

        if (this.id === 'clear') {
          expression = '';
          display.textContent = '0';
        } else if (this.id === 'equals') {
          try {
            // Replace % with /100 for percentage calculation
            let exp = expression.replace(/%/g, '/100');
            expression = eval(exp).toString();
            display.textContent = expression;
          } catch (e) {
            display.textContent = 'Error';
            expression = '';
          }
        } else if (this.classList.contains('number') || this.classList.contains('operator')) {
          // Prevent multiple decimals in a number segment
          if (value === '.') {
            // Split expression by operators to get last number segment
            const parts = expression.split(/[\+\-\*\/%]/);
            const last = parts[parts.length - 1];
            if (last.includes('.')) return;
          }
          expression += value;
          display.textContent = expression;
        }
      });
    });
  </script>
</body>
</html>

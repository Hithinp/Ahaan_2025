---
layout: post
title:  Calculator
permalink: /calculator/
toc: true
---


<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Calculator</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
    body {
      font-family: Arial, sans-serif;
      background-color: #f4f4f4;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }
    .calculator {
      background-color: #333;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 0 20px rgba(0, 0, 0, 0.2);
    }
    .display {
      background-color: #222;
      color: #fff;
      font-size: 2em;
      text-align: right;
      padding: 10px;
      margin-bottom: 10px;
      border-radius: 5px;
    }
    .keys {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 10px;
    }
    button {
      background-color: #444;
      color: #fff;
      border: none;
      padding: 20px;
      font-size: 1.5em;
      border-radius: 5px;
      cursor: pointer;
      transition: background-color 0.3s;
    }
    button:hover {
      background-color: #555;
    }
    button.clear {
      grid-column: span 2;
      background-color: #d9534f;
    }
    button.equals {
      background-color: #5cb85c;
      grid-column: span 2;
    }
  </style>
</head>
<body>

  <div class="calculator">
    <div class="display" id="display">0</div>
    <div class="keys">
      <button class="clear">C</button>
      <button>/</button>
      <button>*</button>
      <button>7</button>
      <button>8</button>
      <button>9</button>
      <button>-</button>
      <button>4</button>
      <button>5</button>
      <button>6</button>
      <button>+</button>
      <button>1</button>
      <button>2</button>
      <button>3</button>
      <button class="equals">=</button>
      <button>0</button>
      <button>.</button>
    </div>
  </div>

  <script>
    const display = document.getElementById('display');
    const buttons = document.querySelectorAll('button');
    let currentInput = '';
    let operator = '';
    let firstValue = '';
    let secondValue = '';
    
    buttons.forEach(button => {
      button.addEventListener('click', () => {
        const value = button.textContent;

        if (value === 'C') {
          clearDisplay();
        } else if (value === '=') {
          calculateResult();
        } else if (value === '+' || value === '-' || value === '*' || value === '/') {
          setOperator(value);
        } else {
          appendNumber(value);
        }
      });
    });

    function clearDisplay() {
      currentInput = '';
      firstValue = '';
      secondValue = '';
      operator = '';
      display.textContent = '0';
    }

    function appendNumber(number) {
      if (currentInput === '' && number === '.') {
        currentInput = '0.';
      } else if (number === '.' && currentInput.includes('.')) {
        return; // Prevent multiple decimals
      } else {
        currentInput += number;
      }
      display.textContent = currentInput;
    }

    function setOperator(op) {
      if (currentInput === '') return; // Prevent setting operator without a number
      if (operator !== '') calculateResult(); // If there's already an operator, calculate first
      firstValue = currentInput;
      operator = op;
      currentInput = '';
    }

    function calculateResult() {
      if (firstValue === '' || operator === '' || currentInput === '') return;

      secondValue = currentInput;
      let result;
      switch (operator) {
        case '+':
          result = parseFloat(firstValue) + parseFloat(secondValue);
          break;
        case '-':
          result = parseFloat(firstValue) - parseFloat(secondValue);
          break;
        case '*':
          result = parseFloat(firstValue) * parseFloat(secondValue);
          break;
        case '/':
          result = parseFloat(firstValue) / parseFloat(secondValue);
          break;
      }

      display.textContent = result;
      currentInput = result.toString();
      operator = '';
      firstValue = '';
      secondValue = '';
    }
  </script>

</body>
</html>

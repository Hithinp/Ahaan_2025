---
layout: post
title: Snake Game
permalink: /snake/
toc: true
---


<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Snake Game</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
    body {
      font-family: Arial, sans-serif;
      background-color: #0f0f0f;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }
    canvas {
      background-color: #1b1b1b;
      display: block;
      margin: 0 auto;
      border: 10px solid #444;
      border-radius: 10px;
      box-shadow: 0 0 15px rgba(0, 0, 0, 0.5);
    }
    .game-container {
      text-align: center;
      color: #fff;
    }
    h1 {
      margin-bottom: 20px;
      font-size: 2.5em;
      letter-spacing: 3px;
      color: #4caf50;
    }
    .score {
      font-size: 1.8em;
      margin-bottom: 10px;
      color: #00d1ff;
    }
    .game-over {
      color: red;
      font-size: 2.5em;
      display: none;
      margin-top: 20px;
      font-weight: bold;
    }
    button {
      padding: 10px 30px;
      font-size: 1.2em;
      cursor: pointer;
      margin-top: 20px;
      background-color: #4caf50;
      color: white;
      border: none;
      border-radius: 5px;
      box-shadow: 0 3px 8px rgba(0, 0, 0, 0.2);
      transition: background-color 0.3s;
    }
    button:hover {
      background-color: #45a049;
    }
  </style>
</head>
<body>
  <div class="game-container">
    <h1>Snake Game</h1>
    <canvas id="gameCanvas" width="500" height="500"></canvas>
    <div class="score">Score: <span id="score">0</span></div>
    <div id="gameOver" class="game-over">Game Over!</div>
    <button id="startButton">Start Game</button>
  </div>

  <script>
    const canvas = document.getElementById('gameCanvas');
    const ctx = canvas.getContext('2d');
    const scoreDisplay = document.getElementById('score');
    const gameOverDisplay = document.getElementById('gameOver');
    const startButton = document.getElementById('startButton');

    const gridSize = 25;
    const canvasSize = 500;
    let snake = [
      { x: gridSize * 4, y: gridSize * 5 },
      { x: gridSize * 3, y: gridSize * 5 },
      { x: gridSize * 2, y: gridSize * 5 },
      { x: gridSize, y: gridSize * 5 },
      { x: 0, y: gridSize * 5 }
    ];
    let direction = { x: gridSize, y: 0 };
    let food = { x: gridSize * 10, y: gridSize * 10 };
    let score = 0;
    let gameLoop;
    let gameSpeed = 150; // Initial speed, slightly faster than before

    // Draw the game grid, snake, and food
    function draw() {
      ctx.clearRect(0, 0, canvasSize, canvasSize);

      // Draw the snake
      snake.forEach((segment, index) => {
        ctx.fillStyle = index === 0 ? '#00d1ff' : '#4caf50'; // Head is blue, body is green
        ctx.fillRect(segment.x, segment.y, gridSize, gridSize);
      });

      // Draw the food
      ctx.fillStyle = '#ff1a1a';
      ctx.fillRect(food.x, food.y, gridSize, gridSize);
    }

    // Move the snake based on direction
    function moveSnake() {
      const head = { x: snake[0].x + direction.x, y: snake[0].y + direction.y };

      snake.unshift(head);

      if (head.x === food.x && head.y === food.y) {
        // Snake eats food
        score += 10;
        scoreDisplay.textContent = score;
        placeFood();
        increaseSpeed();
      } else {
        // Remove the tail segment unless eating food
        snake.pop();
      }
    }

    // Place food at random position on grid
    function placeFood() {
      food.x = Math.floor(Math.random() * (canvasSize / gridSize)) * gridSize;
      food.y = Math.floor(Math.random() * (canvasSize / gridSize)) * gridSize;

      // Ensure food doesn't spawn on the snake
      if (snake.some(segment => segment.x === food.x && segment.y === food.y)) {
        placeFood();
      }
    }

    // Increase game speed after eating food
    function increaseSpeed() {
      if (gameSpeed > 80) {
        gameSpeed -= 5; // Speed increases gradually
        clearInterval(gameLoop);
        gameLoop = setInterval(main, gameSpeed);
      }
    }

    // Check for collisions with walls or itself
    function checkCollision() {
      const head = snake[0];

      // Wall collision
      if (head.x < 0 || head.x >= canvasSize || head.y < 0 || head.y >= canvasSize) {
        return true;
      }

      // Self collision
      for (let i = 1; i < snake.length; i++) {
        if (snake[i].x === head.x && snake[i].y === head.y) {
          return true;
        }
      }

      return false;
    }

    // Main game function
    function main() {
      moveSnake();
      if (checkCollision()) {
        gameOver();
        return;
      }
      draw();
    }

    // Game over state
    function gameOver() {
      clearInterval(gameLoop);
      gameOverDisplay.style.display = 'block';
      startButton.textContent = 'Restart Game';
      startButton.style.display = 'block';
    }

    // Handle direction change based on keyboard input
    function changeDirection(event) {
      const key = event.keyCode;
      const UP = 38, DOWN = 40, LEFT = 37, RIGHT = 39;

      if (key === UP && direction.y === 0) {
        direction = { x: 0, y: -gridSize };
      } else if (key === DOWN && direction.y === 0) {
        direction = { x: 0, y: gridSize };
      } else if (key === LEFT && direction.x === 0) {
        direction = { x: -gridSize, y: 0 };
      } else if (key === RIGHT && direction.x === 0) {
        direction = { x: gridSize, y: 0 };
      }
    }

    // Start/restart the game
    function startGame() {
      snake = [
        { x: gridSize * 4, y: gridSize * 5 },
        { x: gridSize * 3, y: gridSize * 5 },
        { x: gridSize * 2, y: gridSize * 5 },
        { x: gridSize, y: gridSize * 5 },
        { x: 0, y: gridSize * 5 }
      ];
      direction = { x: gridSize, y: 0 };
      score = 0;
      scoreDisplay.textContent = score;
      gameOverDisplay.style.display = 'none';
      gameSpeed = 150; // Reset speed
      placeFood();
      clearInterval(gameLoop);
      gameLoop = setInterval(main, gameSpeed);
    }

    // Event listeners
    document.addEventListener('keydown', changeDirection);
    startButton.addEventListener('click', startGame);
  </script>
</body>
</html>

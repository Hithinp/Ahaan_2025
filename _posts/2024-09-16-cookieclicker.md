---
layout: post
title: Cookie Clicker 
permalink: /cookie-clicker/
toc: true

---




<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Cookie Clicker Game</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      background-color: #f5f5f5;
    }

    #game {
      padding: 20px;
      max-width: 600px;
      margin: 0 auto;
    }

    #cookie-container {
      margin-top: 30px;
    }

    /* Create a circle for the cookie */
    #cookie {
      width: 200px;
      height: 200px;
      background-color: #D2691E; /* Cookie color */
      border-radius: 50%;
      position: relative;
      margin: 0 auto;
      cursor: pointer;
      transition: transform 0.1s;
    }

    /* Chocolate chips */
    .chip {
      width: 20px;
      height: 20px;
      background-color: #3E2723; /* Dark chocolate color */
      border-radius: 50%;
      position: absolute;
    }

    /* Position chocolate chips randomly */
    .chip:nth-child(1) {
      top: 30px;
      left: 50px;
    }

    .chip:nth-child(2) {
      top: 50px;
      right: 40px;
    }

    .chip:nth-child(3) {
      top: 120px;
      left: 60px;
    }

    .chip:nth-child(4) {
      top: 140px;
      right: 50px;
    }

    .chip:nth-child(5) {
      top: 90px;
      left: 90px;
    }

    /* Cookie click effect */
    #cookie:active {
      transform: scale(0.95);
    }

    #cookieCount {
      font-size: 24px;
      font-weight: bold;
    }

    #upgrades {
      margin-top: 20px;
    }

    button {
      padding: 10px 20px;
      font-size: 18px;
      margin: 10px;
      cursor: pointer;
      background-color: #4CAF50;
      color: white;
      border: none;
      border-radius: 5px;
    }

    button:disabled {
      background-color: #ccc;
      cursor: not-allowed;
    }
  </style>
</head>
<body>
  <div id="game">
    <h1>Cookie Clicker</h1>
    <div id="cookie-container">
      <!-- CSS styled cookie -->
      <div id="cookie">
        <div class="chip"></div>
        <div class="chip"></div>
        <div class="chip"></div>
        <div class="chip"></div>
        <div class="chip"></div>
      </div>
      <p>Cookies: <span id="cookieCount">0</span></p>
    </div>
    <div id="upgrades">
      <button id="buyAutoClicker">Buy Auto Clicker (10 Cookies)</button>
      <button id="buyMultiplier">Buy Multiplier (20 Cookies)</button>
    </div>
  </div>

  <script>
    // Variables to keep track of cookies and upgrades
    let cookies = 0;
    let cookiesPerClick = 1;
    let autoClickerPrice = 10;
    let multiplierPrice = 20;
    let autoClickerActive = false;

    // DOM elements
    const cookieCountElement = document.getElementById('cookieCount');
    const cookieElement = document.getElementById('cookie');
    const buyAutoClickerButton = document.getElementById('buyAutoClicker');
    const buyMultiplierButton = document.getElementById('buyMultiplier');

    // Function to update the cookie count
    function updateCookieCount() {
      cookieCountElement.innerText = cookies;
    }

    // Function to handle clicking on the cookie
    cookieElement.addEventListener('click', () => {
      cookies += cookiesPerClick;
      updateCookieCount();
    });

    // Function to handle buying the auto clicker
    buyAutoClickerButton.addEventListener('click', () => {
      if (cookies >= autoClickerPrice) {
        cookies -= autoClickerPrice;
        updateCookieCount();
        buyAutoClickerButton.disabled = true; // Disable the button after purchase
        autoClickerActive = true;

        // Automatically add cookies every second
        setInterval(() => {
          if (autoClickerActive) {
            cookies += cookiesPerClick;
            updateCookieCount();
          }
        }, 1000);
      }
    });

    // Function to handle buying the multiplier
    buyMultiplierButton.addEventListener('click', () => {
      if (cookies >= multiplierPrice) {
        cookies -= multiplierPrice;
        cookiesPerClick *= 2; // Double the cookies per click
        updateCookieCount();
        buyMultiplierButton.disabled = true; // Disable the button after purchase
      }
    });
  </script>
</body>
</html>

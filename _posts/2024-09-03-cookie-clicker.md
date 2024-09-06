---
layout: post
title: The Famous Cookie Clicker Game! (Pair Showcase)
permalink: /cookie-clicker/
toc: true
---

<html>
<head>
<style>
p {
  color: orange;
  font-family: courier;
  font-size: 160%;
}
</style>
</head>
<body>

<p1>We love to play Cookie Clicker in my free time, so why not make my own version off cookie clicker. It may be simple but it is a wonderful way to pass time.</p1>
<p2>Created by Rutvik Chavda and Ahaan Vaidyanathan</p2>

</body>
</html>

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cookie Clicker</title>
    <style>
        #cookie {
            width: 100px;
            height: 100px;
            background-color: brown;
            border-radius: 50%;
            cursor: pointer;
            display: block;
            margin: 20px auto;
        }
        #store button {
            margin: 5px;
        }
    </style>
</head>
<body>
    <h1>Cookie Clicker</h1>
    <div id="cookie"></div>
    <p>Cookies: <span id="cookieCount">0</span></p>

    <h2>Store</h2>
    <div id="store">
        <button onclick="buyUpgrade()">Buy Upgrade (10 cookies)</button>
        <p>Cookies per click: <span id="cookiesPerClick">1</span></p>
    </div>

    <script>
        let cookieCount = 0;
        let cookiesPerClick = 1;

        document.getElementById('cookie').addEventListener('click', function() {
            cookieCount += cookiesPerClick;
            document.getElementById('cookieCount').textContent = cookieCount;
        });

        function buyUpgrade() {
            if (cookieCount >= 10) {
                cookieCount -= 10;
                cookiesPerClick += 1;
                document.getElementById('cookieCount').textContent = cookieCount;
                document.getElementById('cookiesPerClick').textContent = cookiesPerClick;
            } else {
                alert('Not enough cookies!');
            }
        }
    </script>
</body>
</html>



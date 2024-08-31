---
layout: page
title: About
permalink: /about/
---

<html>
<body>


<p style="font-size:100%; color: MediumSeaGreen; font: italic bold 20px Arial, sans-serif;"> Hello my name is Ahaan and I am a 10th grader aka Sophmore. I lived in San Diego all my life, and was born downtown. I love to play  video games on my Nintendo Switch and my favorite foods are Chicken and Pizza. My goals after high school is to work in video game devlopment 
either as a programmer or designer. I am excited to dive deeper into computer science in order to achieve my goals.</p>

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


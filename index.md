---
layout: base
title: Student Home 
description: Home Page
image: /images/mario_animation.png
hide: true
---


---
<html>
<head>
<body>



<!-- Liquid:  statements -->

<!--- Concatenation of site URL to frontmatter image  --->
{% assign sprite_file = site.baseurl | append: page.image %}
<!--- Has is a list variable containing mario metadata for sprite --->
{% assign hash = site.data.mario_metadata %}  
<!--- Size width/height of Sprit images --->
{% assign pixels = 256 %}

<!--- HTML for page contains <p> tag named "Mario" and class properties for a "sprite"  -->

<p id="mario" class="sprite"></p>
  
<!--- Embedded Cascading Style Sheet (CSS) rules, 
        define how HTML elements look 
--->
<style>

  /*CSS style rules for the id and class of the sprite...
  */
  .sprite {
    height: {{pixels}}px;
    width: {{pixels}}px;
    background-image: url('{{sprite_file}}');
    background-repeat: no-repeat;
  }

  /*background position of sprite element
  */
  #mario {
    background-position: calc({{animations[0].col}} * {{pixels}} * -1px) calc({{animations[0].row}} * {{pixels}}* -1px);
  }
</style>

<!--- Embedded executable code--->
<script>
  ////////// convert YML hash to javascript key:value objects /////////

  var mario_metadata = {}; //key, value object
  {% for key in hash %}  
  
  var key = "{{key | first}}"  //key
  var values = {} //values object
  values["row"] = {{key.row}}
  values["col"] = {{key.col}}
  values["frames"] = {{key.frames}}
  mario_metadata[key] = values; //key with values added

  {% endfor %}

  ////////// game object for player /////////

  class Mario {
    constructor(meta_data) {
      this.tID = null;  //capture setInterval() task ID
      this.positionX = 0;  // current position of sprite in X direction
      this.currentSpeed = 0;
      this.marioElement = document.getElementById("mario"); //HTML element of sprite
      this.pixels = {{pixels}}; //pixel offset of images in the sprite, set by liquid constant
      this.interval = 100; //animation time interval
      this.obj = meta_data;
      this.marioElement.style.position = "absolute";
    }

    animate(obj, speed) {
      let frame = 0;
      const row = obj.row * this.pixels;
      this.currentSpeed = speed;

      this.tID = setInterval(() => {
        const col = (frame + obj.col) * this.pixels;
        this.marioElement.style.backgroundPosition = `-${col}px -${row}px`;
        this.marioElement.style.left = `${this.positionX}px`;

        this.positionX += speed;
        frame = (frame + 1) % obj.frames;

        const viewportWidth = window.innerWidth;
        if (this.positionX > viewportWidth - this.pixels) {
          document.documentElement.scrollLeft = this.positionX - viewportWidth + this.pixels;
        }
      }, this.interval);
    }

    startWalking() {
      this.stopAnimate();
      this.animate(this.obj["Walk"], 3);
    }

    startRunning() {
      this.stopAnimate();
      this.animate(this.obj["Run1"], 6);
    }

    startPuffing() {
      this.stopAnimate();
      this.animate(this.obj["Puff"], 0);
    }

    startCheering() {
      this.stopAnimate();
      this.animate(this.obj["Cheer"], 0);
    }

    startFlipping() {
      this.stopAnimate();
      this.animate(this.obj["Flip"], 0);
    }

    startResting() {
      this.stopAnimate();
      this.animate(this.obj["Rest"], 0);
    }

    stopAnimate() {
      clearInterval(this.tID);
    }
  }

  const mario = new Mario(mario_metadata);

  ////////// event control /////////

  window.addEventListener("keydown", (event) => {
    if (event.key === "ArrowRight") {
      event.preventDefault();
      if (event.repeat) {
        mario.startCheering();
      } else {
        if (mario.currentSpeed === 0) {
          mario.startWalking();
        } else if (mario.currentSpeed === 3) {
          mario.startRunning();
        }
      }
    } else if (event.key === "ArrowLeft") {
      event.preventDefault();
      if (event.repeat) {
        mario.stopAnimate();
      } else {
        mario.startPuffing();
      }
    }
  });

  //touch events that enable animations
  window.addEventListener("touchstart", (event) => {
    event.preventDefault(); // prevent default browser action
    if (event.touches[0].clientX > window.innerWidth / 2) {
      // move right
      if (currentSpeed === 0) { // if at rest, go to walking
        mario.startWalking();
      } else if (currentSpeed === 3) { // if walking, go to running
        mario.startRunning();
      }
    } else {
      // move left
      mario.startPuffing();
    }
  });

  //stop animation on window blur
  window.addEventListener("blur", () => {
    mario.stopAnimate();
  });

  //start animation on window focus
  window.addEventListener("focus", () => {
     mario.startFlipping();
  });

  //start animation on page load or page refresh
  document.addEventListener("DOMContentLoaded", () => {
    // adjust sprite size for high pixel density devices
    const scale = window.devicePixelRatio;
    const sprite = document.querySelector(".sprite");
    sprite.style.transform = `scale(${0.2 * scale})`;
    mario.startResting();
  });

</script>
<table>
    <tr>
        <td><img src="{{site.baseurl}}/images/flag.jpeg" height="60" title="Home" alt=""></td>
        <td><a href="{{site.baseurl}}/india-culture/">Timeless India</a></td>
        <td><a href="{{site.baseurl}}/fitness/">Fitness Blog</a></td>
        <td><a href="{{site.baseurl}}/san-diego/">Discover San Diego</a></td>
        <td><a href="{{site.baseurl}}/snake/">Snake Game</a></td>
        <td><a href="{{site.baseurl}}/jupyter/">Jupyter Notebooks</a></td>
        
        
    </tr>
</table>
<h1 style="font-size:300%; color: Red; font: bold 50px Arial, sans-serif;"> Ahaan Vaidyanathan GitHub Page </h1>
----
<div>
<p1 style="font-size:70%; color: purple; font: bold 21px Open Sans;"> Welcome to my GitHub page for AP Computer Science Principals  &#128513;</p1>

<!-- Adding an image using the <img> tag -->
<img src="{{site.baseurl}}/images/Alaska.JPG" height="160">






<div>

<html>
<head>
<body>
----




---
<div>
    <!-- notice how tags can be put INSIDE eachother -->
    <p style="color: Brown; font: bold 14px Open Sans;"> Click here to view College Board </p>
    <a href="https://apstudents.collegeboard.org/" class="button-link">AP College Board</a>

<style>
.button-link {
    display: inline-block;
    padding: 12px 24px;
    font-size: 16px;
    font-weight: bold;
    text-align: center;
    text-decoration: none;
    color: #fff;
    background-color: #4CAF50;
    border: none;
    border-radius: 8px;
    box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
    transition: background-color 0.3s ease, box-shadow 0.3s ease;
}

.button-link:hover {
    background-color: #45a049;
    box-shadow: 0px 6px 8px rgba(0, 0, 0, 0.2);
}

.button-link:active {
    background-color: #3e8e41;
    box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
    transform: translateY(2px);
}
</style>
     
</div>
---
<!-- third information -->
<div>
    <!-- notice how tags can be put INSIDE eachother -->
    <p style=" color: Brown; font: bold 14px Open Sans;"> Click here to learn how to code! </p>
      <a href="https://www.w3schools.com/" class="button-link">W3schools</a>

<style>
.button-link {
    display: inline-block;
    padding: 12px 24px;
    font-size: 16px;
    font-weight: bold;
    text-align: center;
    text-decoration: none;
    color: #fff;
    background-color: #4CAF50;
    border: none;
    border-radius: 8px;
    box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
    transition: background-color 0.3s ease, box-shadow 0.3s ease;
}

.button-link:hover {
    background-color: #45a049;
    box-shadow: 0px 6px 8px rgba(0, 0, 0, 0.2);
}

.button-link:active {
    background-color: #3e8e41;
    box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
    transform: translateY(2px);
}
</style>
</div>
---
---
<!-- second information -->
<div>
    <!-- notice how tags can be put INSIDE eachother -->
    <p style=" color: Brown; font: bold 14px Open Sans;"> Click here to view Del Norte Website! </p>
      <a href="https://delnorte.powayusd.com/" class="button-link">Del Norte Website</a>

<style>
.button-link {
    display: inline-block;
    padding: 12px 24px;
    font-size: 16px;
    font-weight: bold;
    text-align: center;
    text-decoration: none;
    color: #fff;
    background-color: #4CAF50;
    border: none;
    border-radius: 8px;
    box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
    transition: background-color 0.3s ease, box-shadow 0.3s ease;
}

.button-link:hover {
    background-color: #45a049;
    box-shadow: 0px 6px 8px rgba(0, 0, 0, 0.2);
}

.button-link:active {
    background-color: #3e8e41;
    box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
    transform: translateY(2px);

}

</style>
     
</div>
---

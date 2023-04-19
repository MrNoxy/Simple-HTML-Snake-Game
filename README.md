# Simple-HTML-Snake-Game
> Source Code + Demo Website for a Simple HTML ugly looking (worse then Discord Light Mode) Snake Game made by me (Noxy#6969)
> If you want to check this out before using my code you should have a look to the [Demo Version](https://demo-snake.glitch.me/) made by me!
> Also please star this post!


> ***Note: This crappy code was made using Chat GPT. I was bored and decided to make a fun little snake game!***


# Here is the Source Code

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>Snake Game</title>
    <style>
      canvas {
        border: 1px solid black;
        background-color: white;
      }
      button {
        margin-top: 20px;
        padding: 10px;
        font-size: 16px;
        background-color: #4CAF50;
        color: white;
        border: none;
        cursor: pointer;
      }
    </style>
  </head>
  <body>
    <canvas id="canvas" width="400" height="400"></canvas>
    <div id="scoreLabel">Score: 0</div>
    <div id="lastScoreLabel"></div>
    <button id="restartButton" style="display: none;">Press R to restart the game</button>
    <br>
    <p>Thank you for playing this little game I  made! [Made by Noxy#6969] <br>
    You can use the <a href="https://github.com/MrNoxy/Simple-HTML-Snake-Game/tree/main">Source Code</a> if you want to improve this game or make ur own version
    </p>
    
    
    <script>
      // Initialize variables
      let canvas = document.getElementById("canvas");
      let ctx = canvas.getContext("2d");
      let snake = [{x: 10, y: 10}];
      let food = {x: 0, y: 0};
      let direction = "right";
      let score = 0;
      let lastScore = 0;
      let game;
      
      // Draw the snake
      function drawSnake() {
        for (let i = 0; i < snake.length; i++) {
          ctx.fillStyle = "#000000";
          ctx.fillRect(snake[i].x * 10, snake[i].y * 10, 10, 10);
        }
      }
      
      // Draw the food
      function drawFood() {
        ctx.fillStyle = "#FF0000";
        ctx.fillRect(food.x * 10, food.y * 10, 10, 10);
      }
      
      // Generate a random number
      function getRandomNumber(min, max) {
        return Math.floor(Math.random() * (max - min + 1)) + min;
      }
      
      // Check for collision with food
      function checkFoodCollision() {
        if (snake[0].x === food.x && snake[0].y === food.y) {
          snake.push({x: 0, y: 0});
          score++;
          generateFood();
        }
      }
      
      // Check for collision with walls or body
      function checkCollision() {
        if (snake[0].x < 0 || snake[0].x >= canvas.width / 10 ||
            snake[0].y < 0 || snake[0].y >= canvas.height / 10) {
          endGame();
        }
        for (let i = 1; i < snake.length; i++) {
          if (snake[0].x === snake[i].x && snake[0].y === snake[i].y) {
            endGame();
          }
        }
      }
      
      // End the game
      function endGame() {
        clearInterval(game);
        lastScore = score;
        score = 0;
        direction = "right";
        snake = [{x: 10, y: 10}];
        document.getElementById("scoreLabel").innerHTML = "Score: " + score;
        document.getElementById("lastScoreLabel").innerHTML = "Last Score: " + lastScore;
        document.getElementById("restartButton").style.display = "block";
      }
      
      // Generate food at a random location
      function generateFood() {
        food.x = getRandomNumber(0, canvas.width / 10 - 1);
        food.y = getRandomNumber(0, canvas.height / 10 - 1);
      }
      // Handle keyboard input
      document.addEventListener("keydown", function(event) {
        if (event.key === "ArrowLeft" && direction !== "right") {
          direction = "left";
        } else if (event.key === "ArrowUp" && direction !== "down") {
          direction = "up";
        } else if (event.key === "ArrowRight" && direction !== "left") {
          direction = "right";
        } else if (event.key === "ArrowDown" && direction !== "up") {
          direction = "down";
        } else if (event.key === "r") {
          restart();
        }
      });
      
      // Restart the game
      function restart() {
        document.getElementById("restartButton").style.display = "none";
        startGame();
      }
      
      // Start the game loop
      function startGame() {
        game = setInterval(function() {
          // Clear the canvas
          ctx.clearRect(0, 0, canvas.width, canvas.height);
          
          // Move the snake
          for (let i = snake.length - 1; i > 0; i--) {
            snake[i].x = snake[i - 1].x;
            snake[i].y = snake[i - 1].y;
          }
          if (direction === "left") {
            snake[0].x--;
          } else if (direction === "up") {
            snake[0].y--;
          } else if (direction === "right") {
            snake[0].x++;
          } else if (direction === "down") {
            snake[0].y++;
          }
          
          // Draw the snake and food
          drawSnake();
          drawFood();
          
          // Check for collision with food or walls/body
          checkFoodCollision();
          checkCollision();
          
          // Update the score
          document.getElementById("scoreLabel").innerHTML = "Score: " + score;
        }, 150);
        
        // Generate the first food
        generateFood();
      }
      
      // Start the game
      startGame();
    </script>
  </body>
</html>

```

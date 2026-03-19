# Snake-game
Snake 
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Snake Game</title>

<style .controls {
    margin-top: 20px;
    text-align: center;
}

.controls button {
    font-size: 20px;
    padding: 10px 15px;
    margin: 5px;
    border: none;
    border-radius: 8px;
    background: #00ff99;
}>
body {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background: #111;
    color: white;
    font-family: Arial;
    flex-direction: column;
}

h1 {
    margin-bottom: 10px;
}

canvas {
    background: black;
    border: 2px solid #00ff99;
}

.score {
    margin: 10px;
}
</style>
</head>

<body>

<h1>Snake Game 🐍</h1>
<div class="score">Score: <span id="score">0</span></div>
<canvas id="game" width="300" height="300"></canvas>

<script>
const canvas = document.getElementById("game");
const ctx = canvas.getContext("2d");

let box = 15;
let snake = [{x: 150, y: 150}];
let food = {
    x: Math.floor(Math.random()*20)*box,
    y: Math.floor(Math.random()*20)*box
};
let dx = box;
let dy = 0;
let score = 0;

document.addEventListener("keydown", changeDirection);

function changeDirection(event) {
    if (event.key === "ArrowUp" && dy === 0) {
        dx = 0; dy = -box;
    } else if (event.key === "ArrowDown" && dy === 0) {
        dx = 0; dy = box;
    } else if (event.key === "ArrowLeft" && dx === 0) {
        dx = -box; dy = 0;
    } else if (event.key === "ArrowRight" && dx === 0) {
        dx = box; dy = 0;
    }
}

function drawGame() {
    ctx.fillStyle = "black";
    ctx.fillRect(0, 0, 300, 300);

    // Draw snake
    for (let i = 0; i < snake.length; i++) {
        ctx.fillStyle = "#00ff99";
        ctx.fillRect(snake[i].x, snake[i].y, box, box);
    }

    // Draw food
    ctx.fillStyle = "red";
    ctx.fillRect(food.x, food.y, box, box);

    let headX = snake[0].x + dx;
    let headY = snake[0].y + dy;

    // Eat food
    if (headX === food.x && headY === food.y) {
        score++;
        document.getElementById("score").innerText = score;
        food = {
            x: Math.floor(Math.random()*20)*box,
            y: Math.floor(Math.random()*20)*box
        };
    } else {
        snake.pop();
    }

    let newHead = {x: headX, y: headY};

    // Game over conditions
    if (
        headX < 0 || headY < 0 ||
        headX >= 300 || headY >= 300 ||
        collision(newHead, snake)
    ) {
        alert("Game Over! Score: " + score);
        document.location.reload();
    }

    snake.unshift(newHead);
}

function collision(head, array) {
    for (let i = 0; i < array.length; i++) {
        if (head.x === array[i].x && head.y === array[i].y) {
            return true;
        }
    }
    return false;
}

setInterval(drawGame, 120);
</script function setDirection(dir) {
    if (dir === "UP" && dy === 0) {
        dx = 0; dy = -box;
    } else if (dir === "DOWN" && dy === 0) {
        dx = 0; dy = box;
    } else if (dir === "LEFT" && dx === 0) {
        dx = -box; dy = 0;
    } else if (dir === "RIGHT" && dx === 0) {
        dx = box; dy = 0;
    }
}>

</body>
</html>

<div class="controls">
    <button onclick="setDirection('UP')">⬆️</button><br>
    <button onclick="setDirection('LEFT')">⬅️</button>
    <button onclick="setDirection('DOWN')">⬇️</button>
    <button onclick="setDirection('RIGHT')">➡️</button>
</div>

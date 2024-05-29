---
layout: default
title: Student Blog
permalink: /gameoflife
---

<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Conway's Game of Life</title>
<link rel="stylesheet" href="helloworld.css">
<body>
<canvas id="gameCanvas"></canvas>
<div id="controls">
    <button onclick="start()">Start</button>
    <button onclick="stop()">Stop</button>
    <button onclick="clearGrid()">Clear</button>
    <div>
        <label for="speedRange">Speed:</label>
        <input type="range" id="speedRange" min="10" max="1000" value="900" oninput="adjustSpeed(this.value)">
    </div>
</div>
<script>
const canvas = document.getElementById('gameCanvas');
const ctx = canvas.getContext('2d');
// Size of the grid
const gridSize = 50;
const cellSize = 10; // Size of each cell in pixels
let speed = 100; // Milliseconds per frame
canvas.width = gridSize * cellSize;
canvas.height = gridSize * cellSize;
let grid = Array.from({ length: gridSize }, () => Array.from({ length: gridSize }, () => 0));
let intervalId = null;
// Function to update the grid
function updateGrid() {
    const newGrid = Array.from({ length: gridSize }, () => Array.from({ length: gridSize }, () => 0));
    for (let i = 0; i < gridSize; i++) {
        for (let j = 0; j < gridSize; j++) {
            const neighbors = countNeighbors(i, j);
            if (grid[i][j] === 1) {
                if (neighbors < 2 || neighbors > 3) {
                    newGrid[i][j] = 0;
                } else {
                    newGrid[i][j] = 1;
                }
            } else {
                if (neighbors === 3) {
                    newGrid[i][j] = 1;
                }
            }
        }
    }
    grid = newGrid;
}
// Function to count the number of live neighbors
function countNeighbors(x, y) {
    let count = 0;
    for (let i = -1; i <= 1; i++) {
        for (let j = -1; j <= 1; j++) {
            if (i === 0 && j === 0) continue;
            const nx = x + i;
            const ny = y + j;
            if (nx >= 0 && nx < gridSize && ny >= 0 && ny < gridSize && grid[nx][ny] === 1) {
                count++;
            }
        }
    }
    return count;
}
// Function to draw the grid
function drawGrid() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    for (let i = 0; i < gridSize; i++) {
        for (let j = 0; j < gridSize; j++) {
            if (grid[i][j] === 1) {
                ctx.fillStyle = 'black';
            } else {
                ctx.fillStyle = 'white';
            }
            ctx.fillRect(j * cellSize, i * cellSize, cellSize, cellSize);
        }
    }
    drawGridLines();
}

function drawGridLines() {
    ctx.strokeStyle = '#ccc';
    for (let i = 0; i <= gridSize; i++) {
        ctx.beginPath();
        ctx.moveTo(0, i * cellSize);
        ctx.lineTo(canvas.width, i * cellSize);
        ctx.stroke();
        ctx.beginPath();
        ctx.moveTo(i * cellSize, 0);
        ctx.lineTo(i * cellSize, canvas.height);
        ctx.stroke();
    }
}
// Mouse event listeners for toggling cells
canvas.addEventListener('mousedown', function(event) {
    const x = Math.floor(event.offsetY / cellSize);
    const y = Math.floor(event.offsetX / cellSize);
    grid[x][y] = 1 - grid[x][y]; // Toggle cell state
    drawGrid();
});
// Start the simulation
function start() {
    const url = "http://brawlstarsapibackend.stu.nighthawkcodingsociety.com/api/users";
    const body = {
        uid: localStorage.getItem('uid'),
        timesplayed: '1'
    };
    const authoptions = {
        method: 'PUT',
        mode: 'cors',
        cache: 'default',
        credentials: 'include',
        body: JSON.stringify(body),
        headers: {
            'Content-Type': 'application/json',
        }
    };
    fetch(url, authoptions)
    console.log('added one');
    console.log(body);
    intervalId = setInterval(function() {
        updateGrid();
        drawGrid();
    }, speed);
}

// Stop the simulation
function stop() {
    clearInterval(intervalId);
}

// Clear the grid
function clearGrid() {
    clearInterval(intervalId);
    grid = Array.from({ length: gridSize }, () => Array.from({ length: gridSize }, () => 0));
    drawGrid();
}

// Adjust the speed of the simulation
function adjustSpeed(newSpeed) {
    speed = 1010 - newSpeed; // Invert the scale
    if (intervalId) {
        clearInterval(intervalId);
        start();
    }
}


</script>


<a href='{{site.baseurl}}/leaderboard'>Leaderboard</a>

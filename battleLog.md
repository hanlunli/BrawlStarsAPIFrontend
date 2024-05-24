<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Conway's Game of Life</title>
<style>
    canvas {
        border: 1px solid black;
    }
</style>
</head>
<body>
<canvas id="gameCanvas"></canvas>
<br>
<button onclick="start()">Start</button>
<button onclick="stop()">Stop</button>
<button onclick="clearGrid()">Clear</button>
<script>
const canvas = document.getElementById('gameCanvas');
const ctx = canvas.getContext('2d');

// Size of the grid
const gridSize = 50;
const cellSize = 10; // Size of each cell in pixels
const speed = 100; // Milliseconds per frame

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
                ctx.fillRect(j * cellSize, i * cellSize, cellSize, cellSize);
            }
        }
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
</script>
</body>
</html>

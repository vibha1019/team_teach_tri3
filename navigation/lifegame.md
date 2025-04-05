---
layout: default
title: Life Game
search_exclude: true
permalink: /life/
---
# Conway's Game of Life

<div class="controls">
    <button onclick="start()" id="start-btn">Start</button>
    <button onclick="step()">Step</button>
    <button onclick="randomInit(50)">Random</button>
    <button onclick="clearGrid()">Clear</button>
</div>
<div id="grid-container"></div>

<style>
body {
    background-color: #121212; /* 深色背景 */
    color: #e0e0e0; /* 浅色文字 */
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 20px;
}
h1 {
    color: #bb86fc; /* 紫色标题 */
    text-align: center;
    margin-bottom: 20px;
}
#grid-container {
    display: grid;
    gap: 1px;
    background-color: #333;
    padding: 1px;
    margin: 20px auto;
    max-width: fit-content;
}
.cell {
    background-color: #1e1e1e;
    width: 15px;
    height: 15px;
    transition: background-color 0.1s;
}
.cell.alive {
    background-color: #bb86fc;
}
.controls {
    margin: 20px 0;
    text-align: center;
}
button {
    padding: 8px 16px;
    margin: 0 5px;
    background-color: #333;
    color: #fff;
    border: 1px solid #bb86fc;
    border-radius: 4px;
    cursor: pointer;
    transition: all 0.2s;
}
button:hover {
    background-color: #bb86fc;
    color: #000;
}
</style>

<script>
// 游戏配置
const GRID_SIZE = 40;
const CELL_SIZE = 15;
let paused = false;
let intervalId = null;

// 初始化网格
const grid = Array(GRID_SIZE).fill().map(() => Array(GRID_SIZE).fill(0));
const container = document.getElementById('grid-container');

// 设置网格样式
container.style.gridTemplateColumns = `repeat(${GRID_SIZE}, ${CELL_SIZE}px)`;

// 创建单元格
for (let i = 0; i < GRID_SIZE * GRID_SIZE; i++) {
    const cell = document.createElement('div');
    cell.className = 'cell';
    cell.id = `cell-${i}`;
    cell.addEventListener('click', () => toggleCell(i));
    cell.addEventListener('mouseover', (e) => {
        if (e.buttons === 1) toggleCell(i);
    });
    container.appendChild(cell);
}

// 切换细胞状态
function toggleCell(index) {
    const row = Math.floor(index / GRID_SIZE);
    const col = index % GRID_SIZE;
    grid[row][col] = grid[row][col] ? 0 : 1;
    updateGrid();
}

// 更新网格显示
function updateGrid() {
    for (let i = 0; i < GRID_SIZE * GRID_SIZE; i++) {
        const row = Math.floor(i / GRID_SIZE);
        const col = i % GRID_SIZE;
        const cell = document.getElementById(`cell-${i}`);
        cell.classList.toggle('alive', grid[row][col] === 1);
    }
}

// 计算邻居数量
function countNeighbors(row, col) {
    let count = 0;
    for (let r = -1; r <= 1; r++) {
        for (let c = -1; c <= 1; c++) {
            if (r === 0 && c === 0) continue;
            const newRow = row + r;
            const newCol = col + c;
            if (newRow >= 0 && newRow < GRID_SIZE && newCol >= 0 && newCol < GRID_SIZE) {
                count += grid[newRow][newCol];
            }
        }
    }
    return count;
}

// 单步执行
function step() {
    const newGrid = Array(GRID_SIZE).fill().map(() => Array(GRID_SIZE).fill(0));
    
    for (let row = 0; row < GRID_SIZE; row++) {
        for (let col = 0; col < GRID_SIZE; col++) {
            const neighbors = countNeighbors(row, col);
            if (grid[row][col] === 1) {
                newGrid[row][col] = (neighbors === 2 || neighbors === 3) ? 1 : 0;
            } else {
                newGrid[row][col] = neighbors === 3 ? 1 : 0;
            }
        }
    }
    
    for (let row = 0; row < GRID_SIZE; row++) {
        for (let col = 0; col < GRID_SIZE; col++) {
            grid[row][col] = newGrid[row][col];
        }
    }
    
    updateGrid();
}

// 开始/暂停游戏
function start() {
    const btn = document.getElementById('start-btn');
    if (intervalId) {
        clearInterval(intervalId);
        intervalId = null;
        btn.textContent = 'Start';
    } else {
        intervalId = setInterval(step, 100);
        btn.textContent = 'Pause';
    }
}

// 随机初始化
function randomInit(count) {
    for (let row = 0; row < GRID_SIZE; row++) {
        for (let col = 0; col < GRID_SIZE; col++) {
            grid[row][col] = 0;
        }
    }
    updateGrid();
    
    for (let i = 0; i < count; i++) {
        const row = Math.floor(Math.random() * GRID_SIZE);
        const col = Math.floor(Math.random() * GRID_SIZE);
        grid[row][col] = 1;
    }
    updateGrid();
}

// 清空网格
function clearGrid() {
    for (let row = 0; row < GRID_SIZE; row++) {
        for (let col = 0; col < GRID_SIZE; col++) {
            grid[row][col] = 0;
        }
    }
    updateGrid();
}

// 初始渲染
updateGrid();
</script>

### Extra Credit: Try the game twice to see how density affects evolution!
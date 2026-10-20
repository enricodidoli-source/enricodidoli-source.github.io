---
layout: single
title: "Maze Algorithms"
permalink: /_projects/maze_algorithms/
author_profile: true
---

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>Maze Game</title>
  <style>
    body {
      font-family: sans-serif;
      display: flex;
      flex-direction: column;
      align-items: center;
      background: #f0f2f5;
      margin: 0;
      padding: 15px;
      box-sizing: border-box;
    }
    h1 {
      margin-top: 5px;
      margin-bottom: 15px;
      text-align: center;
      color: #222;
    }
    .settings {
      margin-bottom: 15px;
      padding: 15px;
      background: white;
      border-radius: 8px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.1);
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 12px;
      width: 100%;
      max-width: 500px;
      box-sizing: border-box;
    }
    .settings-group {
      display: flex;
      align-items: center;
      gap: 5px;
    }
    .settings select, .settings button {
      padding: 8px;
      font-size: 16px;
      border-radius: 4px;
      border: 1px solid #ccc;
    }
    .settings button {
      background: #007bff;
      color: white;
      border: none;
      cursor: pointer;
      font-weight: bold;
      transition: background 0.2s;
      flex-grow: 1;
    }
    .settings button:hover { background: #0056b3; }
    .stats-container, .legend-container {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 15px;
      background: white;
      padding: 15px;
      border-radius: 8px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.1);
      width: 100%;
      max-width: 500px;
      box-sizing: border-box;
    }
    .stats-container {
      margin-bottom: 15px;
    }
    .stat-box {
      font-size: 14px;
      font-weight: bold;
      text-align: center;
      color: #333;
      flex: 1 1 40%;
    }
    .stat-box span {
      display: block;
      font-size: 20px;
      color: #007bff;
    }
    #maze-img {
      width: 100%;
      height: auto;
      max-width: 420px;
      border: 2px solid #333;
      border-radius: 8px;
      background: white;
      box-shadow: 0 4px 10px rgba(0,0,0,0.15);
    }
    .controls {
      margin-top: 15px;
      margin-bottom: 15px;
      display: grid;
      grid-template-columns: 70px 70px 70px;
      grid-gap: 10px;
      justify-content: center;
    }
    button.move-btn {
      padding: 16px;
      font-size: 22px;
      cursor: pointer;
      border: 1px solid #888;
      border-radius: 8px;
      background: #fff;
      transition: background 0.1s;
      touch-action: manipulation;
    }
    button.move-btn:active { background: #ddd; }
    .btn-up    { grid-column: 2; }
    .btn-left  { grid-column: 1; grid-row: 2; }
    .btn-down  { grid-column: 2; grid-row: 2; }
    .btn-right { grid-column: 3; grid-row: 2; }
    .legend-item {
      display: flex;
      align-items: center;
      gap: 6px;
      font-size: 13px;
      color: #333;
      font-weight: bold;
    }
    .color-box {
      width: 16px;
      height: 16px;
      border-radius: 3px;
      border: 1px solid #aaa;
    }
  </style>
</head>
<body>

  <h1>Maze Game</h1>

  <div class="settings">
    <div class="settings-group">
      <label for="algo-select">Algorithm:</label>
      <select id="algo-select">
        <option value="Recursive_Backtracking">Recursive Backtracking (DFS)</option>
        <option value="Prim">Prim</option>
        <option value="Eller">Eller</option>
        <option value="Aldous_Broder">Aldous-Broder</option>
        <option value="Wilson">Wilson</option>
      </select>
    </div>
    <div class="settings-group">
      <label for="size-select">Size:</label>
      <select id="size-select">
        <option value="2">2x2</option>
        <option value="3">3x3</option>
        <option value="4">4x4</option>
        <option value="5" selected>5x5</option>
        <option value="6">6x6</option>
        <option value="7">7x7</option>
        <option value="8">8x8</option>
        <option value="9">9x9</option>
        <option value="10">10x10</option>
      </select>
    </div>
    <button onclick="startNewMaze()">Generate</button>
  </div>

  <div class="stats-container">
    <div class="stat-box">Moves <span id="moves-count">0</span></div>
    <div class="stat-box">Corridors <span id="corridors-count">0</span></div>
    <div class="stat-box">Intersections <span id="intersections-count">0</span></div>
    <div class="stat-box">Dead Ends <span id="deadends-count">0</span></div>
  </div>

  <img id="maze-img" src="" alt="Loading maze...">

  <div class="controls">
    <button class="move-btn btn-up" onclick="sendMove('up')">▲</button>
    <button class="move-btn btn-left" onclick="sendMove('left')">◀</button>
    <button class="move-btn btn-down" onclick="sendMove('down')">▼</button>
    <button class="move-btn btn-right" onclick="sendMove('right')">▶</button>
  </div>

  <div class="legend-container">
    <div class="legend-item"><div class="color-box" style="background: red;"></div>Generation Root</div>
    <div class="legend-item"><div class="color-box" style="background: pink;"></div>Maze Entry</div>
    <div class="legend-item"><div class="color-box" style="background: blue;"></div>Character</div>
    <div class="legend-item"><div class="color-box" style="background: yellow;"></div>Maze Exit</div>
    <div class="legend-item"><div class="color-box" style="background: green;"></div>Victory Character</div>
  </div>

<script>
    function updateStats(data) {
      document.getElementById('moves-count').textContent = data.moves;
      document.getElementById('corridors-count').textContent = data.corridors;
      document.getElementById('intersections-count').textContent = data.intersections;
      document.getElementById('deadends-count').textContent = data.dead_ends;
    }

    function startNewMaze() {
      const algo = document.getElementById('algo-select').value;
      const size = document.getElementById('size-select').value;

      fetch(`/get_maze?algo=${algo}&size=${size}`)
        .then(res => res.json())
        .then(data => {
          document.getElementById('maze-img').src = data.image;
          updateStats(data);
        })
        .catch(err => console.error("API Error:", err));
    }

    startNewMaze();

    let isWaitingForServer = false;

    function sendMove(dir) {
      if (isWaitingForServer) return;
      
      isWaitingForServer = true; 

      fetch('/move', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ direction: dir })
      })
      .then(res => res.json())
      .then(data => {
        if (!data.error) { 
          document.getElementById('maze-img').src = data.image;
          updateStats(data);
          
          if (data.won) {
            setTimeout(() => alert('Congratulations! You beat the maze!'), 100);
          }
        }
      })
      .catch(err => console.error("API Error:", err))
      .finally(() => {
        isWaitingForServer = false; // Riapre il lucchetto alla fine
      });
    }

    window.addEventListener('keydown', (e) => {
      const keys = {
        'ArrowUp': 'up', 'KeyW': 'up',
        'ArrowDown': 'down', 'KeyS': 'down',
        'ArrowLeft': 'left', 'KeyA': 'left',
        'ArrowRight': 'right', 'KeyD': 'right'
      };
      
      if (['ArrowUp', 'ArrowDown', 'ArrowLeft', 'ArrowRight'].includes(e.code)) {
        e.preventDefault(); 
      }

      if (keys[e.code]) {
        sendMove(keys[e.code]);
      }
    });
  </script>
</body>
</html>

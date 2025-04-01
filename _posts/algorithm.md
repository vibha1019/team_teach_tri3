<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Treasure Hunt Game</title>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; }
        #game-board { display: grid; grid-template-columns: repeat(5, 50px); gap: 5px; margin: 20px auto; width: max-content; }
        .cell { width: 50px; height: 50px; border: 1px solid #000; display: flex; align-items: center; justify-content: center; }
        .player { background-color: blue; color: white; }
        .treasure { background-color: gold; }
        .trap { background-color: red; }
    </style>
</head>
<body>
    <h1>Treasure Hunt Game</h1>
    <p>Use W (up), A (left), S (down), D (right) keys to move.</p>
    <div id="game-board"></div>
    <p id="message"></p>
    <script>
        const size = 5;
        let player = [0, 0];
        let treasure = [Math.floor(Math.random() * size), Math.floor(Math.random() * size)];
        let trap = [Math.floor(Math.random() * size), Math.floor(Math.random() * size)];
        while (trap[0] === treasure[0] && trap[1] === treasure[1]) {
            trap = [Math.floor(Math.random() * size), Math.floor(Math.random() * size)];
        }
        
        function renderBoard() {
            const board = document.getElementById("game-board");
            board.innerHTML = "";
            for (let i = 0; i < size; i++) {
                for (let j = 0; j < size; j++) {
                    const cell = document.createElement("div");
                    cell.classList.add("cell");
                    if (player[0] === i && player[1] === j) cell.classList.add("player");
                    board.appendChild(cell);
                }
            }
        }
        
        function movePlayer(event) {
            const key = event.key.toUpperCase();
            let newPlayer = [...player];
            if (key === 'W' && player[0] > 0) newPlayer[0]--;
            if (key === 'S' && player[0] < size - 1) newPlayer[0]++;
            if (key === 'A' && player[1] > 0) newPlayer[1]--;
            if (key === 'D' && player[1] < size - 1) newPlayer[1]++;
            
            player = newPlayer;
            checkGameState();
            renderBoard();
        }
        
        function checkGameState() {
            const message = document.getElementById("message");
            if (player[0] === trap[0] && player[1] === trap[1]) {
                message.textContent = "Oh no! You stepped on a trap. Game Over!";
                document.removeEventListener("keydown", movePlayer);
            } else if (player[0] === treasure[0] && player[1] === treasure[1]) {
                message.textContent = "Congratulations! You found the treasure!";
                document.removeEventListener("keydown", movePlayer);
            } else {
                let distance = Math.abs(player[0] - treasure[0]) + Math.abs(player[1] - treasure[1]);
                message.textContent = `You feel like the treasure is ${distance} steps away.`;
            }
        }
        
        document.addEventListener("keydown", movePlayer);
        renderBoard();
    </script>
</body>
</html>

//css
body {
    font-family: Arial, sans-serif;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background: linear-gradient(to right, #ffffff, #000000);
    margin: 0;
}

.container {
    text-align: center;
}

#gameBoard {
    display: grid;
    grid-template-columns: repeat(3, 100px);
    grid-gap: 5px;
    margin: 20px auto;
}

.cell {
    width: 100px;
    height: 100px;
    background-color: #f0f0f0;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 2em;
    cursor: pointer;
}

#status {
    margin: 20px;
    font-size: 1.5em;
}

button {
    padding: 10px 20px;
    font-size: 1em;
    cursor: pointer;
}
//js
let currentPlayer = "X";
let gameBoard = ["", "", "", "", "", "", "", "", ""];
let gameActive = true;

const winningConditions = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6]
];

function makeMove(index) {
    if (gameBoard[index] === "" && gameActive) {
        gameBoard[index] = currentPlayer;
        document.getElementById(`cell${index}`).innerText = currentPlayer;
        checkResult();
        currentPlayer = currentPlayer === "X" ? "O" : "X";
    }
}

function checkResult() {
    let roundWon = false;
    for (let i = 0; i < winningConditions.length; i++) {
        const winCondition = winningConditions[i];
        let a = gameBoard[winCondition[0]];
        let b = gameBoard[winCondition[1]];
        let c = gameBoard[winCondition[2]];
        if (a === "" || b === "" || c === "") {
            continue;
        }
        if (a === b && b === c) {
            roundWon = true;
            break;
        }
    }

    if (roundWon) {
        document.getElementById("status").innerText = `Player ${currentPlayer} wins!`;
        gameActive = false;
        return;
    }

    let roundDraw = !gameBoard.includes("");
    if (roundDraw) {
        document.getElementById("status").innerText = "Draw!";
        gameActive = false;
        return;
    }
}

function restartGame() {
    currentPlayer = "X";
    gameBoard = ["", "", "", "", "", "", "", "", ""];
    gameActive = true;
    document.getElementById("status").innerText = "";
    document.querySelectorAll(".cell").forEach(cell => cell.innerText = "");
}
//HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tic-Tac-Toe</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="container">
        <h1>Tic-Tac-Toe</h1>
        <div id="gameBoard">
            <div class="cell" id="cell0" onclick="makeMove(0)"></div>
            <div class="cell" id="cell1" onclick="makeMove(1)"></div>
            <div class="cell" id="cell2" onclick="makeMove(2)"></div>
            <div class="cell" id="cell3" onclick="makeMove(3)"></div>
            <div class="cell" id="cell4" onclick="makeMove(4)"></div>
            <div class="cell" id="cell5" onclick="makeMove(5)"></div>
            <div class="cell" id="cell6" onclick="makeMove(6)"></div>
            <div class="cell" id="cell7" onclick="makeMove(7)"></div>
            <div class="cell" id="cell8" onclick="makeMove(8)"></div>
        </div>
        <div id="status"></div>
        <button onclick="restartGame()">Restart</button>
    </div>
    <script src="script.js"></script>
</body>
</html>

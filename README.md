# PRODIGY_AD_04
TIC TAC TOE

index.html

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Tic Tac Toe</title>
  <link rel="stylesheet" href="style.css" />
</head>
<body>
  <h1>Tic Tac Toe</h1>

  <div class="game-board" id="gameBoard">
    <div class="cell" data-index="0"></div>
    <div class="cell" data-index="1"></div>
    <div class="cell" data-index="2"></div>
    <div class="cell" data-index="3"></div>
    <div class="cell" data-index="4"></div>
    <div class="cell" data-index="5"></div>
    <div class="cell" data-index="6"></div>
    <div class="cell" data-index="7"></div>
    <div class="cell" data-index="8"></div>
  </div>

  <div id="message"></div>
  <button id="restartBtn">Restart</button>

  <script src="script.js"></script>
</body>
</html>

style.css

body {
  font-family: Arial, sans-serif;
  background: #F3E9DC;
  text-align: center;
  margin-top: 50px;
}

h1 {
  color: #743014;
}

.game-board {
  display: grid;
  grid-template-columns: repeat(3, 100px);
  gap: 10px;
  justify-content: center;
  margin: 30px auto;
}

.cell {
  width: 100px;
  height: 100px;
  border-radius: 45px;
  background-color: #FFEDAB;
  border: 2px solid #90acbc;
  font-size: 2.5rem;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
}

.cell.X {
  color: #FC703C;
}

.cell.O {
  color: #087167;
}

#message {
  font-size: 1.5rem;
  margin: 20px;
  color: #222;
}

#restartBtn {
  padding: 10px 20px;
  font-size: 1rem;
  background-color: #75070C;
  color: #FFEDAB;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

script.js

const cells = document.querySelectorAll('.cell');
const message = document.getElementById('message');
const restartBtn = document.getElementById('restartBtn');

let currentPlayer = 'X';
let gameActive = true;
let board = Array(9).fill("");

const winningCombinations = [
  [0, 1, 2], [3, 4, 5], [6, 7, 8], // Rows
  [0, 3, 6], [1, 4, 7], [2, 5, 8], // Columns
  [0, 4, 8], [2, 4, 6]             // Diagonals
];

function handleClick(e) {
  const index = e.target.getAttribute('data-index');

  if (board[index] !== "" || !gameActive) return;

  board[index] = currentPlayer;
  e.target.textContent = currentPlayer;
  e.target.classList.add(currentPlayer);

  if (checkWin()) {
    message.textContent = `Player ${currentPlayer} wins!`;
    gameActive = false;
  } else if (board.every(cell => cell !== "")) {
    message.textContent = "It's a draw!";
    gameActive = false;
  } else {
    currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
  }
}

function checkWin() {
  return winningCombinations.some(combo => {
    return combo.every(index => board[index] === currentPlayer);
  });
}

function restartGame() {
  board = Array(9).fill("");
  currentPlayer = 'X';
  gameActive = true;
  message.textContent = "";

  cells.forEach(cell => {
    cell.textContent = "";
    cell.classList.remove('X', 'O');
  });
}

cells.forEach(cell => cell.addEventListener('click', handleClick));
restartBtn.addEventListener('click', restartGame);

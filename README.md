# game
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Tic Tac Toe</title>
  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      background: linear-gradient(135deg, #74ebd5, #ACB6E5);
      font-family: 'Segoe UI', sans-serif;
    }

    .container {
      text-align: center;
    }

    h1 {
      font-size: 3em;
      margin-bottom: 30px;
      color: #fff;
      text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
    }

    .board {
      display: grid;
      grid-template-columns: repeat(3, 100px);
      grid-template-rows: repeat(3, 100px);
      gap: 10px;
      margin: 0 auto;
    }

    .cell {
      background: rgba(255, 255, 255, 0.9);
      border-radius: 10px;
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 3rem;
      color: #333;
      cursor: pointer;
      transition: all 0.3s ease;
      user-select: none;
      box-shadow: 0 5px 10px rgba(0,0,0,0.2);
    }

    .cell:hover {
      transform: scale(1.1);
      background: #ffffff;
    }

    .cell.X {
      color: #ff3b30;
    }

    .cell.O {
      color: #007aff;
    }

    .winning-message {
      position: fixed;
      top: 0;
      left: 0;
      height: 100%;
      width: 100%;
      background: rgba(0,0,0,0.6);
      display: flex;
      justify-content: center;
      align-items: center;
      opacity: 0;
      pointer-events: none;
      transition: opacity 0.3s ease;
    }

    .winning-message.show {
      opacity: 1;
      pointer-events: all;
    }

    .message-box {
      background: #fff;
      padding: 30px 50px;
      border-radius: 10px;
      text-align: center;
      box-shadow: 0 5px 15px rgba(0,0,0,0.3);
    }

    .message-box p {
      font-size: 2em;
      margin-bottom: 20px;
      color: #333;
    }

    .message-box button {
      padding: 10px 25px;
      font-size: 1.2em;
      background: linear-gradient(45deg, #74ebd5, #ACB6E5);
      border: none;
      color: #fff;
      border-radius: 5px;
      cursor: pointer;
      transition: transform 0.2s ease;
    }

    .message-box button:hover {
      transform: scale(1.1);
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Tic Tac Toe</h1>
    <div class="board" id="board">
      <div class="cell" data-cell></div>
      <div class="cell" data-cell></div>
      <div class="cell" data-cell></div>
      <div class="cell" data-cell></div>
      <div class="cell" data-cell></div>
      <div class="cell" data-cell></div>
      <div class="cell" data-cell></div>
      <div class="cell" data-cell></div>
      <div class="cell" data-cell></div>
    </div>
  </div>

  <div class="winning-message" id="winningMessage">
    <div class="message-box">
      <p id="messageText"></p>
      <button id="restartButton">Play Again</button>
    </div>
  </div>

  <script>
    const cells = document.querySelectorAll('[data-cell]');
    const board = document.getElementById('board');
    const winningMessage = document.getElementById('winningMessage');
    const messageText = document.getElementById('messageText');
    const restartButton = document.getElementById('restartButton');

    const WINNING_COMBINATIONS = [
      [0, 1, 2],
      [3, 4, 5],
      [6, 7, 8],
      [0, 3, 6],
      [1, 4, 7],
      [2, 5, 8],
      [0, 4, 8],
      [2, 4, 6]
    ];

    let isCircleTurn;

    startGame();

    restartButton.addEventListener('click', startGame);

    function startGame() {
      isCircleTurn = false;
      cells.forEach(cell => {
        cell.classList.remove('X');
        cell.classList.remove('O');
        cell.textContent = '';
        cell.removeEventListener('click', handleClick);
        cell.addEventListener('click', handleClick, { once: true });
      });
      winningMessage.classList.remove('show');
    }

    function handleClick(e) {
      const cell = e.target;
      const currentClass = isCircleTurn ? 'O' : 'X';
      placeMark(cell, currentClass);

      if (checkWin(currentClass)) {
        endGame(false, currentClass);
      } else if (isDraw()) {
        endGame(true);
      } else {
        isCircleTurn = !isCircleTurn;
      }
    }

    function placeMark(cell, currentClass) {
      cell.classList.add(currentClass);
      cell.textContent = currentClass;
    }

    function checkWin(currentClass) {
      return WINNING_COMBINATIONS.some(combination => {
        return combination.every(index => {
          return cells[index].classList.contains(currentClass);
        });
      });
    }

    function isDraw() {
      return [...cells].every(cell => {
        return cell.classList.contains('X') || cell.classList.contains('O');
      });
    }

    function endGame(draw, winner) {
      if (draw) {
        messageText.textContent = "It's a Draw!";
      } else {
        messageText.textContent = `${winner} Wins!`;
      }
      winningMessage.classList.add('show');
    }
  </script>
</body>
</html>

                            LUDO DICE   
<!DOCTYPE html>
<html>
<head>
  <title>Roll Dice</title>
  <style>
    .dice {
      width: 100px;
      height: 100px;
      margin-top: 20px;
      border: 4px solid #000;
      border-radius: 15px;
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      grid-template-rows: repeat(3, 1fr);
      gap: 5px;
      padding: 10px;
    }
    .dot {
      width: 20px;
      height: 20px;
      background-color: black;
      border-radius: 50%;
      justify-self: center;
      align-self: center;
    }
    button {
      padding: 10px 20px;
      font-size: 18px;
      margin-top: 20px;
    }
  </style>
</head>
<body>

<h2>🎲 Roll the Dice</h2>
<button onclick="rollDice()">Roll Dice</button>

<div id="dice" class="dice"></div>

<script>
  function rollDice() {
    const diceContainer = document.getElementById("dice");
    diceContainer.innerHTML = "";

    const number = Math.floor(Math.random() * 6) + 1;

    const dotMap = {
      1: [4],
      2: [0, 8],
      3: [0, 4, 8],
      4: [0, 2, 6, 8],
      5: [0, 2, 4, 6, 8],
      6: [0, 2, 3, 5, 6, 8]
    };

    for (let i = 0; i < 9; i++) {
      const cell = document.createElement("div");
      if (dotMap[number].includes(i)) {
        cell.className = "dot";
      }
      diceContainer.appendChild(cell);
    }

    alert("You rolled a " + number + "!");
  }
</script>

</body>
</html>


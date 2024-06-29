/**
 * Declaring the initial constants for the game setup stage 
 */
const GRID_SIZE = 10;
const TREASURE_VALUES = [5, 6, 7, 8];
const DIRECTIONS = ['a', 'd', 'w', 's'];

/**
 * Setiing up the Game state
 */  
let grid = [];
let treasureHunterPosition = null;
let setupStageEnded = false;
let playStageEnded = false;
let roundsCompleted = 0;
let treasuresRemaining = [0, 0, 0, 0];
let userScore = 0;

/* Initializing the 10x10 grid setup for the game as required for the setup and play stage 
 * The code for the following function is done by taking reference from 
 * sencha (https://www.sencha.com/blog/how-to-create-professional-design-with-javascript-grid/):
 * How to setup a 10x10 professional grid in javascript 
 */ 
function initializeGrid() {
  const gridElement = document.getElementById('grid');
  for (let i = 0; i < GRID_SIZE; i++) {
    grid[i] = [];
    for (let j = 0; j < GRID_SIZE; j++) {
      const cell = document.createElement('div');
      cell.className = 'cell';
      cell.dataset.row = i;
      cell.dataset.col = j;
      cell.textContent = '';
      grid[i][j] = cell;
      gridElement.appendChild(cell);
    }
  }
}

/* Function to handle the cell clicking during setup stage of the game as required 
 * The code for the following function is done by taking reference from 
 * medium (https://medium.com/@imPradhyumn/tic-tac-toe-using-javascript-48b079bcd015):
 * How to handle cell clicks while drafting the setup stage for any game 
 * Also made use of ChatGPT: How to setup and handle cell clicks while drafting setup stage for a game 
 * OpenAI, Chat GPT 2024 Version. 
 */ 
function handleCellClick(event) {
  if (playStageEnded) {
    alert('Game is in the end stage. You cannot make changes to the grid.');
    return;
  }

  const row = parseInt(event.target.dataset.row);
  const col = parseInt(event.target.dataset.col);

  if (!setupStageEnded) {
    const input = prompt('Enter "h" for Hunter, "o" for Obstacle, or number (5-8) for Treasure:');
    if (input === 'h') {
      if (treasureHunterPosition) {
        alert('Treasure hunter already placed. You cannot place another one.');
      } else {
        placeTreasureHunter(row, col);
      }
    } else if (input === 'o') {
      placeObstacle(row, col);
    } else if (parseInt(input) >= 5 && parseInt(input) <= 8) {
      placeTreasure(row, col, parseInt(input));
    } else {
      alert('Invalid input!');
    }
  }
}

/**
 * Defining a Function to Handle key pressing stage during play stage setup for the game 
 */  
function handleKeyPress(event) {
  if (setupStageEnded && !playStageEnded) {
    const key = event.key.toLowerCase();
    if (DIRECTIONS.includes(key)) {
      moveTreasureHunter(key);
    } else {
      alert('Invalid input!');
    }
  }
}

/**
 *  Defining a Function for placement of treasure during setup stage of the game 
 */ 
function placeTreasure(row, col, value) {
  if (grid[row][col].textContent !== '') {
    alert('Cell already occupied. You cannot change the object placed on this cell.');
    return;
  }
  grid[row][col].textContent = value;
  treasuresRemaining[value - 5]++;
}

/**
 * Defining a Function for placement of an obstacle during setup stage of the game 
 */ 
function placeObstacle(row, col) {
  if (grid[row][col].textContent !== '') {
    alert('Cell already occupied. You cannot change the object placed on this cell.');
    return;
  }
  grid[row][col].textContent = 'O';
}

/** 
 * Defining a function for placement of treasure hunter during setup stage of the game 
 */ 
function placeTreasureHunter(row, col) {
  if (treasureHunterPosition) {
    alert('Treasure hunter already placed. You cannot place another one.');
    return;
  }
  treasureHunterPosition = [row, col];
  grid[row][col].textContent = 'H';
}

/* The above code snippets from handling key pressing stage to defining a function for placement of treasure hunter
 * I have used references from mdn web docs for basic comprehension of drafting these codes.
 * mdn web docs (https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide): 
*/ 

/* Function to move the treasure hunter left, right, up and down during play stage of the game 
 * The code for this function was drafted by taking reference from stackoverflow 
 * stackoverflow (https://stackoverflow.com/questions/56660003/i-am-trying-to-move-my-character-with-the-arrow-keys-but-it-doesnt-move):
 * Trying to code for making the game player to move in directions using certain keys 
 */ 
function moveTreasureHunter(direction) {
  const [row, col] = treasureHunterPosition;
  let newRow = row;
  let newCol = col;

  if (direction === 'a') {
    newCol--;
  } else if (direction === 'd') {
    newCol++;
  } else if (direction === 'w') {
    newRow--;
  } else if (direction === 's') {
    newRow++;
  }

  if (!isValidMove(newRow, newCol)) {
    alert('Invalid move!');
    return;
  }

  const targetCell = grid[newRow][newCol];
  const targetContent = targetCell.textContent;

  if (targetContent === 'O') {
    alert('Cannot move onto an obstacle!');
    return;
  }

  if (targetContent !== '') {
    // Collecting the treasure while playing the game 
    const treasureValue = parseInt(targetContent);
    userScore += treasureValue;
    treasuresRemaining[treasureValue - 5]--;
    
    // Removing the treasure while playing the game 
    targetCell.textContent = '';
    
    // Placing an obstacle on an empty cell randomly after hunter collects any one treasure 
    placeRandomObstacle();
    endRound();
  } else {
    
    // Moving to empty cell during the game play stage 
    grid[row][col].textContent = '';
    treasureHunterPosition = [newRow, newCol];
    targetCell.textContent = 'H';
    endRound();
  }
}

/**
 * Checking if each and every move is valid and follows the rules of the game 
 */ 
function isValidMove(row, col) {
  return row >= 0 && row < GRID_SIZE && col >= 0 && col < GRID_SIZE;
}

/**
 * Finishes the rounds in the playstage of the game 
 */ 
function endRound() {
  roundsCompleted++;
  updateStatus();
  if (treasuresRemaining.every(count => count === 0)) {
    endPlayStage();
  }
}

/** 
 * Finishes the setup stage of the game 
 */  
function endSetupStage() {
  if (!treasureHunterPosition) {
    alert('You must place the treasure hunter before ending the setup stage.');
    return;
  }
  setupStageEnded = true;
  document.getElementById('endSetupButton').style.display = 'none';
  updateStatus();
}

/**
 * Ending the game by finishing the playstage 
 * Computes the performance index once the game is ended 
 */ 
function endPlayStage() {
  playStageEnded = true;
  computePerformanceIndex();
}

/** 
 * Computing the performance index of the game and finishing the game  
 */ 
function computePerformanceIndex() {
  const performanceIndex = roundsCompleted > 0 ? (userScore / roundsCompleted).toFixed(2) : 0;
  alert(`Performance Index: ${performanceIndex}`);
}

/** 
 * Updating the status information for the game as the hunter proceeds 
 */ 
function updateStatus() {
  let status = `Rounds Completed: ${roundsCompleted}<br>`;
  for (let i = 0; i < TREASURE_VALUES.length; i++) {
    status += `Treasures Remaining (${TREASURE_VALUES[i]}): ${treasuresRemaining[i]}<br>`;
  }
  status += `User Score: ${userScore}`;
  document.getElementById('status').innerHTML = status;
}

/** 
 * Placing an obstacle on a random empty cell after the hunter collects the first treasure 
 */ 
function placeRandomObstacle() {
  let row, col;
  do {
    row = Math.floor(Math.random() * GRID_SIZE);
    col = Math.floor(Math.random() * GRID_SIZE);
  } while (grid[row][col].textContent !== '');
  grid[row][col].textContent = 'O'; 
}

// Initializing the grid for the game 
initializeGrid();

// Adding event listener for the end setup stage game button 
document.getElementById('endSetupButton').addEventListener('click', endSetupStage);

// Adding event listener for the key press during play stage of the game 
document.addEventListener('keypress', handleKeyPress);

// Adding event listener for the cell click during setup stage of the game 
const cells = document.querySelectorAll('.cell');
cells.forEach(cell => {
  cell.addEventListener('click', handleCellClick);
});

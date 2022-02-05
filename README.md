# Javascript Math Sprint Game

## Radio Buttons section and Functionality
```javascript
// Get Elements

// Pages
const gamePage = document.getElementById("game-page");
const scorePage = document.getElementById("score-page");
const splashPage = document.getElementById("splash-page");
const countdownPage = document.getElementById("countdown-page");

// Splash Page
const startForm = document.getElementById("start-form");
const radioContainers = document.querySelectorAll(".radio-container");
const radioInputs = document.querySelectorAll("input");
const bestScores = document.querySelectorAll(".best-score-value");

// Countdown Page
const countdown = document.querySelector(".countdown");

// Game Page
const itemContainer = document.querySelector(".item-container");

// Score Page
const finalTimeEl = document.querySelector(".final-time");
const baseTimeEl = document.querySelector(".base-time");
const penaltyTimeEl = document.querySelector(".penalty-time");
const playAgainBtn = document.querySelector(".play-again");

// Equations
let questionAmount = 0;
let equationsArray = [];

// Game Page
let firstNumber = 0;
let secondNumber = 0;
let equtionObject = {};
const wrongFormat = [];
```

## Countdown Page
```javascript
// Start the Countdown, displays... 3,2,1 , Go!
function countdownStart() {
  countdown.textContent = "3";
  setTimeout(() => {
    countdown.textContent = "2";
  }, 1000);
  setTimeout(() => {
    countdown.textContent = "1";
  }, 2000);
  setTimeout(() => {
    countdown.textContent = "GO!";
  }, 3000);
}

// Navigate from Splash Page to Countdown Page
function showCountDown() {
  countdownPage.hidden = false;
  splashPage.hidden = true;
  countdownStart();
  console.log(
    "showing the countdown page and countdownStart function ",
    countdownPage
  );
}
// Form that decides amount of questions
function selectQuestionAmount(e) {
  e.preventDefault();
  questionAmount = getRadioValue();
  console.log("question amount", questionAmount);
  if (questionAmount) {
    showCountDown();
  }
  console.log("select question amount", questionAmount);
}
```

## Generate Random Equation
```javascript
// Create Correct/Incorrect Random Equations
function createEquations() {
  // Randomly choose how many correct equations there should be
  const correctEquations = getRandomInt(questionAmount);
  console.log("correct equations:", correctEquations);

  // Set amount of wrong equations
  const wrongEquations = questionAmount - correctEquations;
  console.log("wrong equations:", wrongEquations);

  // Loop through, multiply random numbers up to 9, push to array
  for (let i = 0; i < correctEquations; i++) {
    firstNumber = getRandomInt(9);
    secondNumber = getRandomInt(9);
    const equationValue = firstNumber * secondNumber;
    const equation = `${firstNumber} x ${secondNumber} = ${equationValue}`;
    equationObject = { value: equation, evaluated: "true" };
    equationsArray.push(equationObject);
  }

  // Loop through, mess with the equation results, push to array
  for (let i = 0; i < wrongEquations; i++) {
    firstNumber = getRandomInt(9);
    secondNumber = getRandomInt(9);
    const equationValue = firstNumber * secondNumber;
    wrongFormat[0] = `${firstNumber} X ${secondNumber + 1} = ${equationValue}`;
    wrongFormat[1] = `${firstNumber} X ${secondNumber} = ${equationValue - 1}`;
    wrongFormat[2] = `${firstNumber + 1} X ${secondNumber} = ${equationValue}`;
    const formatChoice = getRandomInt(3);
    const equation = wrongFormat[formatChoice];
    equationObject = { value: equation, evaluated: "false" };
    equationsArray.push(equationObject);
  }
  console.log("equations array:", equationsArray);
}
```
## Display Game Page
```javascript
// Displays Game Page
function showGamePage() {
  gamePage.hidden = false;
  countdownPage.hidden = true;
}
```
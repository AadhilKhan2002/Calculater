<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculator</title>
    <link rel="stylesheet" href="C-1.css">
    <style>
body{
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background-color: #f0f0f0;
}
p{
    text-align: center;
    font-size: 40px;
    color: limegreen;
}
.calculator {
    border-radius: 5px;
    box-shadow: 0px 0px 20px 0px rgba(0, 0, 0, 0.2);
    padding: 20px;
    background-color: #fff;
}
.calculator-screen {
    width: 90%;
    height: 90px;
    border: none;
    background-color: #252525;
    color: #fff;
    text-align: right;
    padding-right: 20px;
    padding-left: 10px;
    font-size: 1.5em;
    border-radius: 5px;
    margin-bottom: 10px;
}
.calculator-keys button {
    height: 60px;
    width: 22%;
    margin: 3px;
    background-color: #e0e0e0;
    border: none;
    border-radius: 5px;
    font-size: 1.2em;
    transition: background-color 0.2s;
}
.calculator-keys button:hover {
    background-color: #d4d4d4;
}
.operator {
    background-color: #ff9500;
    color: #fff;
}
.operator:hover {
    background-color: #e48900;
}
.equal-sign {
    height: 100%;
    background-color: #ff9500;
    color: #fff;
}
.equal-sign:hover {
    background-color: #e48900;
}
.all-clear {
    background-color: #ff3b30;
    color: #fff;
}
.all-clear:hover {
    background-color: #e02e24;
}

    </style>
</head>
<body>
    <div class="calculator">
        <p>Basic Calculater</p>
        <input type="text" class="calculator-screen" value="" disabled />
        <div class="calculator-keys">
            <button type="button" class="operator" value="+">+</button>
            <button type="button" class="operator" value="-">-</button>
            <button type="button" class="operator" value="*">&times;</button>
            <button type="button" class="operator" value="/">&divide;</button>

  <button type="button" value="7">7</button>
  <button type="button" value="8">8</button>
  <button type="button" value="9">9</button>

  <button type="button" value="4">4</button>
  <button type="button" value="5">5</button>
  <button type="button" value="6">6</button>

  <button type="button" value="1">1</button>
  <button type="button" value="2">2</button>
  <button type="button" value="3">3</button>

  <button type="button" value="0">0</button>
  <button type="button" class="decimal" value=".">.</button>
  <button type="button" class="all-clear" value="all-clear">AC</button>

  <button type="button" class="equal-sign" value="=">=</button>
 </div>
</div>
    <script src="C-1.js">
    document.addEventListener('DOMContentLoaded', () => {
    const calculator = {
        displayValue: '0',
        firstOperand: null,
        waitingForSecondOperand: false,
        operator: null,
    };
    function inputDigit(digit) {
        const { displayValue, waitingForSecondOperand } = calculator;
if (waitingForSecondOperand === true) {
            calculator.displayValue = digit;
            calculator.waitingForSecondOperand = false;
        } else {
            calculator.displayValue = displayValue === '0' ? digit : displayValue + digit;
        }
    }
function inputDecimal(dot) {
        if (calculator.waitingForSecondOperand === true) return;
if (!calculator.displayValue.includes(dot)) {
            calculator.displayValue += dot;
        }
    }
 function handleOperator(nextOperator) {
        const { firstOperand, displayValue, operator } = calculator;
        const inputValue = parseFloat(displayValue);
if (operator && calculator.waitingForSecondOperand) {
            calculator.operator = nextOperator;
            return;
        }
 if (firstOperand == null && !isNaN(inputValue)) {
            calculator.firstOperand = inputValue;
        } else if (operator) {
            const result = performCalculation[operator](firstOperand, inputValue);
 calculator.displayValue = String(result);
            calculator.firstOperand = result;
        }
 calculator.waitingForSecondOperand = true;
        calculator.operator = nextOperator;
    }
const performCalculation = {
        '/': (firstOperand, secondOperand) => firstOperand / secondOperand,
        '*': (firstOperand, secondOperand) => firstOperand * secondOperand,
        '+': (firstOperand, secondOperand) => firstOperand + secondOperand,
        '-': (firstOperand, secondOperand) => firstOperand - secondOperand,
        '=': (firstOperand, secondOperand) => secondOperand,
    };
 function resetCalculator() {
        calculator.displayValue = '0';
        calculator.firstOperand = null;
        calculator.waitingForSecondOperand = false;
        calculator.operator = null;
    }
function updateDisplay() {
        const display = document.querySelector('.calculator-screen');
        display.value = calculator.displayValue;
    }
updateDisplay();
 const keys = document.querySelector('.calculator-keys');
    keys.addEventListener('click', (event) => {
        const { target } = event;
        const { value } = target;
if (!target.matches('button')) {
            return;
        }
switch (value) {
            case '+':
            case '-':
            case '*':
            case '/':
            case '=':
                handleOperator(value);
                break;
            case '.':
                inputDecimal(value);
                break;
            case 'all-clear':
                resetCalculator();
                break;
            default:
                if (Number.isInteger(parseFloat(value))) {
                    inputDigit(value);
                }
        }

   updateDisplay();
    });
});

    </script>
</body>
</html>

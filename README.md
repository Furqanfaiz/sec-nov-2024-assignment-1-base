<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Basic Calculator</title>
    <style>
        .calculator {
            width: 300px;
            margin: 50px auto;
            padding: 20px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        .display {
            width: 100%;
            margin-bottom: 10px;
            padding: 10px;
            font-size: 18px;
        }
        .buttons {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 5px;
        }
        button {
            padding: 10px;
            font-size: 16px;
            cursor: pointer;
        }
    </style>
</head>
<body>
<div class="calculator">
    <input type="text" class="display" id="display" readonly>
    <div class="buttons">
        <button onclick="appendNumber('7')">7</button>
        <button onclick="appendNumber('8')">8</button>
        <button onclick="appendNumber('9')">9</button>
        <button onclick="setOperation('+')">+</button>

        <button onclick="appendNumber('4')">4</button>
        <button onclick="appendNumber('5')">5</button>
        <button onclick="appendNumber('6')">6</button>
        <button onclick="setOperation('-')">-</button>

        <button onclick="appendNumber('1')">1</button>
        <button onclick="appendNumber('2')">2</button>
        <button onclick="appendNumber('3')">3</button>
        <button onclick="setOperation('*')">×</button>

        <button onclick="appendNumber('0')">0</button>
        <button onclick="appendNumber('.')">.</button>
        <button onclick="calculate()">=</button>
        <button onclick="setOperation('/')">/</button>

        <button onclick="setOperation('^')">^</button>
        <button onclick="setOperation('%')">%</button>
        <button onclick="clearDisplay()">C</button>
        <button onclick="deleteLast()">←</button>
    </div>
</div>

<script>
    let firstNumber = '';
    let currentOperation = '';
    let newNumber = true;
    const display = document.getElementById('display');

    function appendNumber(num) {
        if (newNumber) {
            display.value = '';
            newNumber = false;
        }
        // Prevent multiple decimal points
        if (num === '.' && display.value.includes('.')) return;
        display.value += num;
    }

    function setOperation(op) {
        firstNumber = display.value;
        currentOperation = op;
        newNumber = true;
    }

    function clearDisplay() {
        display.value = '';
        firstNumber = '';
        currentOperation = '';
        newNumber = true;
    }

    function deleteLast() {
        display.value = display.value.slice(0, -1);
    }

    function calculate() {
        if (!currentOperation || !firstNumber) return;

        const num1 = parseFloat(firstNumber);
        const num2 = parseFloat(display.value);
        let result;

        switch (currentOperation) {
            case '+':
                result = num1 + num2;
                break;
            case '-':
                result = num1 - num2;
                break;
            case '*':
                result = num1 * num2;
                break;
            case '/':
                if (num2 === 0) {
                    display.value = 'Error: Division by zero';
                    return;
                }
                result = num1 / num2;
                break;
            case '^':
                result = Math.pow(num1, num2);
                break;
            case '%':
                result = num1 % num2;
                break;
        }

        // Handle decimal precision
        result = parseFloat(result.toFixed(8));
        display.value = result;
        firstNumber = result.toString();
        newNumber = true;
    }
</script>
</body>
</html>

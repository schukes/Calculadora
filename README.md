<!DOCTYPE html>
<html>
<head>
  <title>Calculadora</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #222;
      color: #fff;
    }

    .calculator {
      max-width: 300px;
      margin: 0 auto;
      background-color: #333;
      padding: 10px;
      border-radius: 5px;
      box-shadow: 0 0 5px rgba(0, 0, 0, 0.3);
    }

    #input {
      width: 100%;
      padding: 5px;
      margin-bottom: 10px;
      font-size: 18px;
      background-color: #444;
      color: #fff;
      border: none;
      border-radius: 5px;
    }

    .buttons {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      grid-gap: 5px;
    }

    button {
      padding: 10px;
      font-size: 18px;
      background-color: #555;
      color: #fff;
      border: none;
      cursor: pointer;
    }

    .tooltip {
      position: relative;
      display: inline-block;
    }

    .tooltip:hover #tooltipText {
      visibility: visible;
      opacity: 1;
    }

    .tooltip #tooltipText {
      visibility: hidden;
      background-color: #333;
      color: #fff;
      text-align: center;
      border-radius: 6px;
      padding: 5px;
      position: absolute;
      z-index: 1;
      bottom: 125%;
      left: 50%;
      transform: translateX(-50%);
      opacity: 0;
      transition: opacity 0.3s;
    }

    .print-button {
      display: block;
      margin: 10px auto;
      padding: 10px;
      font-size: 16px;
      background-color: #555;
      color: #fff;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }

    .ticket {
      padding: 10px;
      margin-top: 10px;
      background-color: #444;
      border: 1px solid #777;
      border-radius: 5px;
    }

    .ticket p {
      margin: 0;
      white-space: pre;
    }
  </style>
</head>
<body>
  <div class="calculator">
    <input type="text" id="input" disabled>
    <div class="buttons">
      <button onclick="appendNumber(7)" data-tooltip="Insere o número 7">7</button>
      <button onclick="appendNumber(8)" data-tooltip="Insere o número 8">8</button>
      <button onclick="appendNumber(9)" data-tooltip="Insere o número 9">9</button>
      <button onclick="appendOperator('+')" data-tooltip="Adição">+</button>
      <button onclick="appendNumber(4)" data-tooltip="Insere o número 4">4</button>
      <button onclick="appendNumber(5)" data-tooltip="Insere o número 5">5</button>
      <button onclick="appendNumber(6)" data-tooltip="Insere o número 6">6</button>
      <button onclick="appendOperator('-')" data-tooltip="Subtração">-</button>
      <button onclick="appendNumber(1)" data-tooltip="Insere o número 1">1</button>
      <button onclick="appendNumber(2)" data-tooltip="Insere o número 2">2</button>
      <button onclick="appendNumber(3)" data-tooltip="Insere o número 3">3</button>
      <button onclick="appendOperator('*')" data-tooltip="Multiplicação">*</button>
      <button onclick="appendNumber(0)" data-tooltip="Insere o número 0">0</button>
      <button onclick="appendOperator('.')">.</button>
      <button onclick="calculate()" data-tooltip="Calcula o resultado">=</button>
      <button onclick="appendOperator('/')" data-tooltip="Divisão">/</button>
      <button onclick="clearInput()" data-tooltip="Limpa o campo">C</button>
      <button onclick="memoryClear()" data-tooltip="Limpa a memória">MC</button>
      <button onclick="memoryRecall()" data-tooltip="Recupera o valor armazenado na memória e insere no campo de entrada">MR</button>
      <button onclick="memoryAdd()" data-tooltip="Adiciona o valor atual no campo de entrada à memória">M+</button>
      <button onclick="memorySubtract()" data-tooltip="Subtrai o valor atual no campo de entrada da memória">M-</button>
      <button onclick="memoryStore()" data-tooltip="Armazena o valor atual no campo de entrada na memória">MS</button>
      <button onclick="calculatePercentage()" data-tooltip="Calcula a porcentagem do valor atual no campo de entrada">%</button>
      <button onclick="clearEntry()" data-tooltip="Limpa a entrada atual no campo de entrada">CE</button>
      <button onclick="calculateInverse()" data-tooltip="Calcula o inverso do valor atual no campo de entrada">1/x</button>
      <button onclick="calculateSquare()" data-tooltip="Calcula o quadrado do valor atual no campo de entrada">x²</button>
      <button onclick="calculateSquareRoot()" data-tooltip="Calcula a raiz quadrada do valor atual no campo de entrada">√</button>
      <button onclick="changeSign()" data-tooltip="Inverte o sinal do valor atual no campo de entrada">+/-</button>
    </div>
    <div class="tooltip">
      <span id="tooltipText"></span>
    </div>
    <button onclick="printTicket()" class="print-button">Imprimir</button>
    <div id="ticket" class="ticket"></div>
  </div>

  <script>
    let inputField = document.getElementById("input");
    let ticketDiv = document.getElementById("ticket");
    let calculationHistory = [];
    let memory = 0;

    function appendNumber(number) {
      inputField.value += number;
    }

    function appendOperator(operator) {
      inputField.value += operator;
    }

    function calculate() {
      try {
        const expression = inputField.value;
        result = eval(expression);
        const operation = expression + "=" + result;
        calculationHistory.push(operation);
        clearInput();
        displayCalculationHistory();
      } catch (error) {
        inputField.value = "Erro";
      }
    }

    function clearInput() {
      inputField.value = "";
    }

    function displayCalculationHistory() {
      let ticketContent = "<p>Histórico de cálculos:</p>";
      for (let i = 0; i < calculationHistory.length; i++) {
        ticketContent += "<p>" + calculationHistory[i] + "</p>";
      }
      ticketDiv.innerHTML = ticketContent;
    }

    function printTicket() {
      displayCalculationHistory();
      window.print();
    }

    // Funções adicionadas:

    function memoryClear() {
      memory = 0;
    }

    function memoryRecall() {
      inputField.value = memory;
    }

    function memoryAdd() {
      const currentValue = parseFloat(inputField.value);
      memory += currentValue;
    }

    function memorySubtract() {
      const currentValue = parseFloat(inputField.value);
      memory -= currentValue;
    }

    function memoryStore() {
      memory = parseFloat(inputField.value);
    }

    function calculatePercentage() {
      const currentValue = parseFloat(inputField.value);
      const percentage = currentValue / 100;
      inputField.value = percentage;
    }

    function clearEntry() {
      inputField.value = "";
    }

    function calculateInverse() {
      const currentValue = parseFloat(inputField.value);
      const inverse = 1 / currentValue;
      inputField.value = inverse;
    }

    function calculateSquare() {
      const currentValue = parseFloat(inputField.value);
      const square = currentValue * currentValue;
      inputField.value = square;
    }

    function calculateSquareRoot() {
      const currentValue = parseFloat(inputField.value);
      const squareRoot = Math.sqrt(currentValue);
      inputField.value = squareRoot;
    }

    function changeSign() {
      const currentValue = parseFloat(inputField.value);
      const invertedSign = -currentValue;
      inputField.value = invertedSign;
    }
  </script>
</body>
</html>

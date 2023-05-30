<!DOCTYPE html>
<html>
<head>
  <title>Calculadora</title>
  <style>
    body {
      background-color: #212121;
      color: #ffffff;
      font-family: Arial, sans-serif;
      padding: 10px;
      margin: 0;
    }

    h1 {
      text-align: center;
    }

    .calculator {
      max-width: 400px;
      margin: 0 auto;
      background-color: #333333;
      border-radius: 10px;
      padding: 20px;
    }

    #resultado {
      width: 100%;
      height: 40px;
      font-size: 24px;
      padding: 5px;
      margin-bottom: 10px;
      background-color: #555555;
      border: none;
      color: #ffffff;
      text-align: right;
    }

    .button-grid {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      grid-gap: 10px;
    }

    button {
      width: 100%;
      height: 40px;
      font-size: 18px;
      background-color: #666666;
      border: none;
      color: #ffffff;
      cursor: pointer;
    }

    button:hover {
      background-color: #999999;
    }

    #historico {
      margin-top: 20px;
      background-color: #212121;
      padding: 10px;
      border-radius: 10px;
    }

    .ticket {
      background-color: #333333;
      padding: 10px;
      margin-bottom: 10px;
      border-radius: 5px;
    }

    .ticket p {
      margin: 0;
      font-size: 16px;
    }

    .ticket .expressao {
      font-size: 18px;
      font-weight: bold;
      margin-bottom: 5px;
    }

    .ticket .resultado {
      font-size: 24px;
      font-weight: bold;
    }

    .ticket hr {
      border: none;
      border-top: 1px dashed #ffffff;
      margin: 10px 0;
    }

    .btn-limpar {
      width: 100%;
      height: 40px;
      font-size: 18px;
      background-color: #bf360c;
      border: none;
      color: #ffffff;
      cursor: pointer;
      margin-top: 10px;
    }

    @media (max-width: 480px) {
      .calculator {
        max-width: 300px;
      }
    }
  </style>
</head>
<body>
  <h1>Calculadora</h1>
  <div class="calculator">
    <input type="text" id="resultado" readonly>
    <div class="button-grid">
      <button onclick="adicionarNumero('7')">7</button>
      <button onclick="adicionarNumero('8')">8</button>
      <button onclick="adicionarNumero('9')">9</button>
      <button onclick="adicionarOperador('+')">+</button>
      <button onclick="adicionarNumero('4')">4</button>
      <button onclick="adicionarNumero('5')">5</button>
      <button onclick="adicionarNumero('6')">6</button>
      <button onclick="adicionarOperador('-')">-</button>
      <button onclick="adicionarNumero('1')">1</button>
      <button onclick="adicionarNumero('2')">2</button>
      <button onclick="adicionarNumero('3')">3</button>
      <button onclick="adicionarOperador('*')">*</button>
      <button onclick="adicionarNumero('0')">0</button>
      <button onclick="adicionarDecimal('.')">.</button>
      <button onclick="calcular()">=</button>
      <button onclick="adicionarOperador('/')">/</button>
    </div>
    <button class="btn-limpar" onclick="limpar()">Limpar</button>
  </div>

  <div id="historico"></div>

  <script>
    var numeroAtual = '';
    var operadorAtual = '';
    var resultado = 0;
    var historico = [];

    function adicionarNumero(numero) {
      numeroAtual += numero;
      resultado = parseFloat(numeroAtual);
      document.getElementById('resultado').value = numeroAtual;
    }

    function adicionarOperador(operador) {
      if (numeroAtual !== '') {
        calcular();
      }
      operadorAtual = operador;
      numeroAtual = '';
    }

    function adicionarDecimal(decimal) {
      if (numeroAtual === '') {
        numeroAtual = '0';
      }
      if (numeroAtual.indexOf(decimal) === -1) {
        numeroAtual += decimal;
      }
      document.getElementById('resultado').value = numeroAtual;
    }

    function calcular() {
      var valorAtual = parseFloat(numeroAtual);
      var total;

      switch (operadorAtual) {
        case '+':
          total = resultado + valorAtual;
          break;
        case '-':
          total = resultado - valorAtual;
          break;
        case '*':
          total = resultado * valorAtual;
          break;
        case '/':
          total = resultado / valorAtual;
          break;
        default:
          return;
      }

      historico.push({ expressao: resultado + ' ' + operadorAtual + ' ' + numeroAtual, resultado: total });
      numeroAtual = '';
      operadorAtual = '';
      resultado = total;

      document.getElementById('resultado').value = total;

      exibirHistorico();
    }

    function limpar() {
      numeroAtual = '';
      operadorAtual = '';
      resultado = 0;
      document.getElementById('resultado').value = '';
      historico = [];
      exibirHistorico();
    }

    function exibirHistorico() {
      var historicoDiv = document.getElementById('historico');
      historicoDiv.innerHTML = '';

      for (var i = 0; i < historico.length; i++) {
        var ticket = document.createElement('div');
        ticket.classList.add('ticket');

        var expressao = document.createElement('p');
        expressao.classList.add('expressao');
        expressao.textContent = historico[i].expressao;

        var resultado = document.createElement('p');
        resultado.classList.add('resultado');
        resultado.textContent = historico[i].resultado;

        var linha = document.createElement('hr');

        ticket.appendChild(expressao);
        ticket.appendChild(resultado);
        ticket.appendChild(linha);

        historicoDiv.appendChild(ticket);
      }
    }

    // Captura eventos do teclado
    document.onkeydown = function(event) {
      var key = event.key;
      if (key >= '0' && key <= '9') {
        adicionarNumero(key);
      } else if (key === '.') {
        adicionarDecimal(key);
      } else if (key === '+' || key === '-' || key === '*' || key === '/') {
        adicionarOperador(key);
      } else if (key === 'Enter' || key === '=') {
        calcular();
      }
    };
  </script>
</body>
</html>

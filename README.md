# <!DOCTYPE html>
<html>
<head>
  <title>Calculadora</title>
  <style>
    body {
      background-color: #212121;
      color: #ffffff;
      font-family: Arial, sans-serif;
    }

    h1 {
      text-align: center;
    }

    #resultado {
      width: 100%;
      height: 40px;
      font-size: 24px;
      padding: 5px;
      margin-bottom: 10px;
      background-color: #333333;
      border: none;
      color: #ffffff;
    }

    table {
      width: 300px;
      margin: 0 auto;
      margin-bottom: 10px;
    }

    table td {
      text-align: center;
      padding: 10px;
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
      background-color: #212121;
      padding: 10px;
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
  </style>
</head>
<body>
  <h1>Calculadora</h1>
  <input type="text" id="resultado" readonly>
  <br>
  <table>
    <tr>
      <td><button onclick="adicionarNumero('7')">7</button></td>
      <td><button onclick="adicionarNumero('8')">8</button></td>
      <td><button onclick="adicionarNumero('9')">9</button></td>
      <td><button onclick="adicionarOperador('+')">+</button></td>
    </tr>
    <tr>
      <td><button onclick="adicionarNumero('4')">4</button></td>
      <td><button onclick="adicionarNumero('5')">5</button></td>
      <td><button onclick="adicionarNumero('6')">6</button></td>
      <td><button onclick="adicionarOperador('-')">-</button></td>
    </tr>
    <tr>
      <td><button onclick="adicionarNumero('1')">1</button></td>
      <td><button onclick="adicionarNumero('2')">2</button></td>
      <td><button onclick="adicionarNumero('3')">3</button></td>
      <td><button onclick="adicionarOperador('*')">*</button></td>
    </tr>
    <tr>
      <td><button onclick="adicionarNumero('0')">0</button></td>
      <td><button onclick="adicionarDecimal('.')">.</button></td>
      <td><button onclick="calcular()">=</button></td>
      <td><button onclick="adicionarOperador('/')">/</button></td>
    </tr>
  </table>

  <br>
  <button onclick="imprimir()">Imprimir</button>

  <div id="historico"></div>

  <script>
    var numeroAtual = '';
    var operadorAtual = '';
    var resultado;
    var historico = [];

    function adicionarNumero(numero) {
      numeroAtual += numero;
      resultado = document.getElementById('resultado');
      resultado.value = numeroAtual;
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
      resultado = document.getElementById('resultado');
      resultado.value = numeroAtual;
    }

    function calcular() {
      var valorAnterior = parseFloat(resultado.value);
      var valorAtual = parseFloat(numeroAtual);
      var total;

      switch (operadorAtual) {
        case '+':
          total = valorAnterior + valorAtual;
          break;
        case '-':
          total = valorAnterior - valorAtual;
          break;
        case '*':
          total = valorAnterior * valorAtual;
          break;
        case '/':
          total = valorAnterior / valorAtual;
          break;
        default:
          return;
      }

      historico.push({ expressao: resultado.value + ' ' + operadorAtual + ' ' + numeroAtual, resultado: total });
      numeroAtual = '';
      operadorAtual = '';
      resultado = document.getElementById('resultado');
      resultado.value = total;

      exibirHistorico();
    }

    function limpar() {
      numeroAtual = '';
      operadorAtual = '';
      resultado = document.getElementById('resultado');
      resultado.value = '';
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

    function imprimir() {
      var printContents = document.getElementById('historico').innerHTML;
      var originalContents = document.body.innerHTML;
      document.body.innerHTML = printContents;
      window.print();
      document.body.innerHTML = originalContents;
      exibirHistorico();
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

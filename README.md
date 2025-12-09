# 💻 Calculadora Web Simples

Uma calculadora básica e científica desenvolvida usando HTML, CSS (com Grid) e JavaScript puro.

## 🌟 Funcionalidades

Esta calculadora oferece funções aritméticas básicas, operações de memória (M+, MR, etc.) e funções científicas essenciais.

* **Operações Básicas:** Adição (+), Subtração (-), Multiplicação (*), Divisão (/).
* **Controle:** Limpar tudo (C), Limpar Entrada (CE), Alterar Sinal (+/-).
* **Memória:** Limpar (MC), Recuperar (MR), Adicionar (M+), Subtrair (M-), Armazenar (MS).
* **Funções Científicas:** Raiz Quadrada (√), Quadrado (x²), Inverso (1/x), Porcentagem (%).
* **Histórico:** Registro de operações no "Ticket" e função de impressão.
* **Usabilidade:** Suporte completo para **entrada via teclado**.

## 🚀 Como Usar

1.  **Clone o repositório:**
    ```bash
    git clone [LINK-DO-SEU-REPOSITORIO]
    ```
2.  **Abra o arquivo:** Navegue até o diretório e abra o arquivo `index.html` no seu navegador preferido.

## ⌨️ Comandos do Teclado

| Tecla | Ação |
| :---: | :--- |
| `0-9`, `.`, `+`, `-`, `*`, `/` | Inserir número ou operador |
| `Enter` ou `=` | Calcular resultado |
| `Delete` | Limpar a entrada atual (`CE`) |
| `Escape` | Limpar tudo (`C`) |

## ⚠️ Nota de Segurança

O cálculo da expressão utiliza a função JavaScript nativa **`eval()`**. Embora seja eficiente para esta calculadora simples, o uso de `eval()` é geralmente desaconselhado para entradas de usuário não confiáveis devido a potenciais vulnerabilidades de segurança (injeção de código).

* **Referência:** [MDN Web Docs - `eval()`](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/eval)

## 🛠️ Tecnologias

* **HTML5**
* **CSS3** (Flexbox/Grid para Layout)
* **JavaScript** (Puro)

## 🧑‍💻 Contribuição

Contribuições são bem-vindas! Se você encontrar um bug ou quiser adicionar um recurso, sinta-se à vontade para abrir uma *Issue* ou enviar um *Pull Request*.

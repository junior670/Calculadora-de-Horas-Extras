<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8">
  <title>Calculadora de Horas Extras Neon</title>
  <style>
    body {
      background-color: #0f0f0f;
      font-family: 'Segoe UI', sans-serif;
      color: #fff;
      text-align: center;
      padding: 40px;
    }

    h1 {
      color: #00ffff;
      text-shadow: 0 0 10px #00ffff, 0 0 20px #00ffff;
    }

    .container {
      background-color: #1a1a1a;
      padding: 30px;
      border-radius: 15px;
      box-shadow: 0 0 20px #00ffff55;
      max-width: 500px;
      margin: 0 auto;
    }

    input {
      width: 90%;
      padding: 10px;
      margin: 10px 0;
      border: none;
      border-radius: 5px;
      background-color: #111;
      color: #00ffff;
      font-size: 16px;
      box-shadow: inset 0 0 10px #00ffff55;
    }

    button {
      background: #00ffff;
      color: #000;
      padding: 12px 20px;
      border: none;
      font-weight: bold;
      border-radius: 8px;
      cursor: pointer;
      margin: 10px 5px 0;
      box-shadow: 0 0 10px #00ffff, 0 0 20px #00ffff;
      transition: transform 0.2s ease, box-shadow 0.3s ease;
    }

    button:hover {
      transform: scale(1.05);
      box-shadow: 0 0 20px #00ffff, 0 0 30px #00ffff;
    }

    .resultado {
      margin-top: 30px;
      background-color: #111;
      padding: 20px;
      border-radius: 10px;
      box-shadow: inset 0 0 15px #00ffff44;
      font-size: 16px;
      white-space: pre-line;
    }

    .social {
      margin-top: 50px;
    }

    .social a {
      color: #00ffcc;
      margin: 0 10px;
      text-decoration: none;
      font-size: 20px;
      text-shadow: 0 0 5px #00ffcc, 0 0 10px #00ffcc;
      transition: color 0.3s, transform 0.3s;
    }

    .social a:hover {
      color: #ffffff;
      transform: scale(1.1);
    }
  </style>
</head>
<body>
  <h1>Calculadora de Horas Extras</h1>
  <div class="container">
    <input type="number" step="0.01" id="valorHora" placeholder="Valor da hora (R$)">
    <input type="number" id="horasNormais" placeholder="Horas normais trabalhadas (Ex: 220)">
    <input type="number" id="horas50" placeholder="Horas extras 50%">
    <input type="number" id="horas60" placeholder="Horas extras 60%">
    <input type="number" id="horas70" placeholder="Horas extras 70%">
    <input type="number" id="horas100" placeholder="Horas extras 100%">
    <input type="number" id="horas110" placeholder="Horas extras 110%">

    <button onclick="calcular()">Calcular</button>
    <button onclick="limparCampos()">Limpar</button>
    <button onclick="baixarResultado()">Baixar Resultado</button>

    <div id="resultado" class="resultado"></div>
  </div>


  <div class="social">
    <p>✨ Me siga nas redes sociais:</p>
    <a href="https://www.linkedin.com/in/junior-santos-9b930b211" target="_blank" style="color: #0ff; text-decoration: none;">LinkedIn</a> |
      <a href="https://github.com/junior670" target="_blank" style="color: #0ff; text-decoration: none;">GitHub</a> |
      <a href="https://www.instagram.com/junior670" target="_blank" style="color: #0ff; text-decoration: none;">Instagram</a> |
      <a href="https://www.dio.me/users/diegojr09" target="_blank" style="color: #0ff; text-decoration: none;">Perfil Público.Dio</a> |
      <a href="https://www.dio.me/" target="_blank" style="color: #0ff; text-decoration: none;">Dio.me</a> |
      <a href="https://www.youtube.com/watch?v=jVxxKYlSDNk" target="_blank" style="color: #0ff; text-decoration: none;">YouTube</a> |
  </div>




  <script>
    let resultadoTexto = "";

    function calcular() {
      const valorHora = parseFloat(document.getElementById("valorHora").value);
      const horasNormais = parseFloat(document.getElementById("horasNormais").value);
      const horas50 = parseFloat(document.getElementById("horas50").value) || 0;
      const horas60 = parseFloat(document.getElementById("horas60").value) || 0;
      const horas70 = parseFloat(document.getElementById("horas70").value) || 0;
      const horas100 = parseFloat(document.getElementById("horas100").value) || 0;
      const horas110 = parseFloat(document.getElementById("horas110").value) || 0;

      if (isNaN(valorHora) || isNaN(horasNormais)) {
        document.getElementById("resultado").textContent = "Preencha o valor da hora e as horas normais.";
        return;
      }

      const salarioFixo = valorHora * horasNormais;
      const extra50 = horas50 * valorHora * 1.5;
      const extra60 = horas60 * valorHora * 1.6;
      const extra70 = horas70 * valorHora * 1.7;
      const extra100 = horas100 * valorHora * 2.0;
      const extra110 = horas110 * valorHora * 2.1;

      const totalExtras = extra50 + extra60 + extra70 + extra100 + extra110;
      const salarioBruto = salarioFixo + totalExtras;
      const vale = salarioFixo * 0.40;
      const descontoINSS = salarioBruto * 0.08;
      const salarioLiquido = salarioBruto - descontoINSS;

      resultadoTexto =
        `💰 Salário Fixo (mensal): R$ ${salarioFixo.toFixed(2)}\n\n` +
        `⏱️ Horas Extras:\n` +
        `- 50%: R$ ${extra50.toFixed(2)}\n` +
        `- 60%: R$ ${extra60.toFixed(2)}\n` +
        `- 70%: R$ ${extra70.toFixed(2)}\n` +
        `- 100%: R$ ${extra100.toFixed(2)}\n` +
        `- 110%: R$ ${extra110.toFixed(2)}\n\n` +
        `🔧 Total Horas Extras: R$ ${totalExtras.toFixed(2)}\n\n` +
        `📊 Salário Bruto: R$ ${salarioBruto.toFixed(2)}\n` +
        `💳 Vale (40% do fixo): R$ ${vale.toFixed(2)}\n\n` +
        `📉 Desconto INSS (8%): R$ ${descontoINSS.toFixed(2)}\n` +
        `✅ Salário Líquido: R$ ${salarioLiquido.toFixed(2)}`;

      document.getElementById("resultado").textContent = resultadoTexto;
    }

    function limparCampos() {
      const ids = ["valorHora", "horasNormais", "horas50", "horas60", "horas70", "horas100", "horas110"];
      ids.forEach(id => document.getElementById(id).value = "");
      document.getElementById("resultado").textContent = "";
      resultadoTexto = "";
    }

    function baixarResultado() {
      if (!resultadoTexto) {
        alert("Calcule primeiro antes de baixar o resultado!");
        return;
      }
      const blob = new Blob([resultadoTexto], { type: 'text/plain' });
      const link = document.createElement('a');
      link.href = URL.createObjectURL(blob);
      link.download = "resultado_calculo.txt";
      link.click();
    }
  </script>
</body>
</html>


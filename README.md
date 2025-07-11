<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Cadastro</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f4f4f4;
      padding: 30px;
    }
    .form-container {
      background: white;
      padding: 25px;
      max-width: 400px;
      margin: auto;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
      text-align: center;
    }
    h2 {
      margin-bottom: 10px;
    }
    input, button {
      width: 100%;
      padding: 10px;
      margin-top: 10px;
      border-radius: 5px;
      border: 1px solid #ccc;
      font-size: 16px;
    }
    button {
      background: #4CAF50;
      color: white;
      border: none;
      cursor: pointer;
    }
    .hidden {
      display: none;
    }
    .spinner {
      border: 5px solid #f3f3f3;
      border-top: 5px solid #4CAF50;
      border-radius: 50%;
      width: 50px;
      height: 50px;
      animation: spin 1s linear infinite;
      margin: 20px auto;
    }
    @keyframes spin {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }
  </style>
</head>
<body>

  <div class="form-container">
    <div id="cadastroDiv">
      <h2>Crie sua Conta</h2>
      <p>Preencha os campos abaixo:</p>
      <form id="cadastro">
        <input type="text" name="nome" placeholder="Seu nome" required>
        <input type="email" name="email" placeholder="Seu e-mail" required>
        <input type="text" name="whatsapp" placeholder="Seu WhatsApp" required>
        <input type="password" name="senha" placeholder="Crie uma senha" required>
        <input type="password" name="confirmaSenha" placeholder="Confirme a senha" required>
        <button type="submit">Cadastrar</button>
      </form>
    </div>

    <div id="loading" class="hidden">
      <p>Enviando dados...</p>
      <div class="spinner"></div>
    </div>

    <div id="sucesso" class="hidden">
      <h2>Cadastro Concluído!</h2>
      <p>Obrigado! Seus dados foram recebidos com sucesso.</p>
      <p><strong>Um de nossos atendentes irá entrar em contato.</strong></p>
    </div>
  </div>

  <script>
    document.getElementById('cadastro').addEventListener('submit', function(e) {
      e.preventDefault();
      const form = this;
      const senha = form.senha.value;
      const confirma = form.confirmaSenha.value;

      if (senha !== confirma) {
        alert('As senhas não coincidem!');
        return;
      }

      document.getElementById('cadastroDiv').classList.add('hidden');
      document.getElementById('loading').classList.remove('hidden');

      const formData = new FormData(form);
      formData.append('_captcha', 'false');
      formData.append('_subject', 'Novo Cadastro');

      fetch('https://formsubmit.co/natanaelverissimo34@gmail.com', {
        method: 'POST',
        body: formData
      }).then(() => {
        setTimeout(() => {
          document.getElementById('loading').classList.add('hidden');
          document.getElementById('sucesso').classList.remove('hidden');
        }, 2000); // Aguarda 2 segundos de "carregamento"
      });
    });
  </script>

</body>
</html>

<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Lendário Plataforma Games</title>
  <style>
    body {
      margin: 0;
      font-family: 'Comic Sans MS', sans-serif;
      background-color: #2E0854; /* Roxo escuro */
      color: #fff;
    }

    header {
      background-color: #6A0DAD;
      padding: 20px;
      text-align: center;
      font-size: 2em;
      font-weight: bold;
      border-bottom: 5px solid #FFD700;
    }

    .container {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
      gap: 20px;
      padding: 20px;
    }

    .card {
      background-color: #7B1FA2;
      border-radius: 15px;
      padding: 15px;
      text-align: center;
      transition: transform 0.3s;
      cursor: pointer;
    }

    .card:hover {
      transform: scale(1.05);
      background-color: #9C27B0;
    }

    .card img {
      width: 100%;
      border-radius: 10px;
    }

    .card h3 {
      margin-top: 10px;
      font-size: 1.2em;
      color: #FFD700;
    }

    .card p {
      font-size: 0.9em;
      margin: 10px 0;
    }

    .btn {
      background-color: #FFD700;
      color: #4B0082;
      padding: 8px 12px;
      border-radius: 8px;
      text-decoration: none;
      font-weight: bold;
      display: inline-block;
      margin-top: 10px;
    }

    .btn:hover {
      background-color: #FFA500;
    }

    footer {
      background-color: #6A0DAD;
      text-align: center;
      padding: 15px;
      font-size: 0.9em;
      border-top: 5px solid #FFD700;
    }
  </style>
</head>
<body>
  <header>
    🎮 Lendário Plataforma Games
  </header>

  <!-- Música de fundo -->
  <audio autoplay loop>
    <source src="https://media.vocaroo.com/mp3/1iOle3gRKpTl" type="audio/mpeg">
    Seu navegador não suporta áudio.
  </audio>

  <div class="container">
    <!-- Jogo 1 -->
    <div class="card">
      <img src="https://via.placeholder.com/250x150.png?text=Lendario+Voo+Simulador" alt="Lendário Voo Simulador">
      <h3>Lendário Voo Simulador</h3>
      <p>Teste suas habilidades de voo nesse simulador incrível!</p>
      <a href="https://luancraft39.github.io/Lend-rio-Voo-Simulador/" class="btn" target="_blank">Jogar</a>
    </div>

    <!-- Jogo 2 -->
    <div class="card">
      <img src="https://via.placeholder.com/250x150.png?text=Lendario+Parkour+Adventure" alt="Lendário Parkour Adventure">
      <h3>Lendário Parkour Adventure</h3>
      <p>Supere obstáculos e viva uma aventura radical de parkour!</p>
      <a href="https://luancraft39.github.io/Lend-rio-Parkour-Adventure/" class="btn" target="_blank">Jogar</a>
    </div>

    <!-- Jogo 3 -->
    <div class="card">
      <img src="https://via.placeholder.com/250x150.png?text=Lendario+Click+Simulador" alt="Lendário Click Simulador">
      <h3>Lendário Click Simulador</h3>
      <p>Mostre sua velocidade de cliques e alcance recordes!</p>
      <a href="https://luancraft39.github.io/Lend-rio-Click-Simulador/" class="btn" target="_blank">Jogar</a>
    </div>

    <!-- Jogo 4 - Novo -->
    <div class="card">
      <img src="https://via.placeholder.com/250x150.png?text=Lendario+Beat+Clash" alt="Lendário Beat Clash">
      <h3>Lendário Beat Clash</h3>
      <p>Entre no ritmo e enfrente batalhas musicais épicas!</p>
      <a href="https://luancraft39.github.io/LEND-RIO-BEAT-CLASH-X" class="btn" target="_blank">Jogar</a>
    </div>
  </div>

  <footer>© 2025 - 2026 Lendário Studio Community — todos os direitos reservados.</footer>
</body>
</html>

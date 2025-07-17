<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Noite de Jogos Criativos - Jogar Online</title>
  <style>
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: #fff8f0;
      margin: 0; padding: 0;
      color: #333;
      max-width: 900px;
      margin-left: auto;
      margin-right: auto;
      padding: 15px;
    }
    h1, h2 {
      color: #963cbd;
      text-align: center;
    }
    section {
      background: #faf5ff;
      border: 2px dashed #963cbd;
      border-radius: 12px;
      margin-bottom: 30px;
      padding: 15px 20px;
    }
    button {
      background: #963cbd;
      color: white;
      border: none;
      padding: 10px 18px;
      border-radius: 8px;
      cursor: pointer;
      font-size: 1rem;
      margin-top: 10px;
      transition: background-color 0.3s ease;
    }
    button:hover:not(:disabled) {
      background: #b173f2;
    }
    button:disabled {
      background: #ccc;
      cursor: not-allowed;
    }
    label {
      display: block;
      margin-top: 10px;
    }
    input[type="text"], textarea, select {
      width: 100%;
      padding: 8px;
      margin-top: 4px;
      border: 1px solid #ccc;
      border-radius: 6px;
      font-size: 1rem;
      resize: vertical;
    }
    ul {
      list-style: none;
      padding-left: 0;
    }
    ul li {
      background: #eee;
      margin: 5px 0;
      padding: 8px;
      border-radius: 6px;
    }
    .timer {
      font-weight: bold;
      font-size: 1.3rem;
      margin-top: 10px;
      color: #963cbd;
      text-align: center;
    }
    .flex-row {
      display: flex;
      gap: 15px;
      flex-wrap: wrap;
      justify-content: center;
    }
    .flex-col {
      display: flex;
      flex-direction: column;
    }
    .point-list {
      margin-top: 10px;
    }
    .notice {
      background: #fff2cc;
      border-left: 5px solid #f39c12;
      padding: 10px;
      margin-top: 10px;
      border-radius: 6px;
    }
    .hidden {
      display: none;
    }
    .phrase-list {
      max-height: 200px;
      overflow-y: auto;
      background: #fff;
      border: 1px solid #ccc;
      padding: 10px;
      border-radius: 6px;
      margin-top: 10px;
      white-space: pre-line;
    }
  </style>
</head>
<body>

  <h1>🎲 Noite de Jogos Criativos</h1>

  <!-- 1. Mímica Temática -->
  <section id="mimica">
    <h2>🪩 1. Mímica Temática</h2>
    <p><strong>Instruções:</strong> Clique em "Sortear palavra" para receber uma palavra para representar. Você tem 1 minuto para fazer a mímica enquanto seu grupo tenta adivinhar.</p>
    
    <label for="temaMimica">Escolha um tema:</label>
    <select id="temaMimica" aria-label="Escolha um tema para a mímica">
      <option value="biblicos">Personagens bíblicos ou santos</option>
      <option value="profissoes">Profissões</option>
      <option value="filmes">Filmes ou séries</option>
      <option value="emocoes">Emoções</option>
      <option value="objetos">Objetos do cotidiano</option>
    </select>
    <button id="sortearPalavraBtn">Sortear palavra</button>
    <p><strong>Palavra sorteada:</strong> <span id="palavraSorteada">---</span></p>

    <div class="timer" id="timerMimica" aria-live="polite">Tempo: 01:00</div>
    <button id="iniciarTimerBtn" disabled>Iniciar tempo</button>

    <p class="notice">Dica: Use uma caixinha ou chapéu para sortear na vida real, este site ajuda a organizar e controlar o tempo!</p>
  </section>

  <!-- 2. Quem eu sou? -->
  <section id="quemEuSou">
    <h2>🎭 2. Quem eu sou?</h2>
    <p><strong>Instruções:</strong> Cada jogador escreve o nome de uma pessoa famosa ou personagem e cola "virtualmente" na testa do amigo da direita. Ele deve fazer perguntas de “sim” ou “não” para descobrir quem é.</p>
    
    <label for="nomePersonagem">Digite o nome para colar na testa:</label>
    <input type="text" id="nomePersonagem" placeholder="Nome de pessoa famosa ou personagem" aria-label="Nome para colar na testa" />
    <button id="colocarNaTestaBtn">Colocar na testa</button>

    <p><strong>Nome na testa:</strong> <span id="nomeNaTestaDisplay" aria-live="polite">---</span></p>

    <label for="perguntaSimNao">Faça uma pergunta (responda sim/não):</label>
    <input type="text" id="perguntaSimNao" placeholder="Ex: Sou vivo?" aria-label="Pergunta sim ou não" />
    <button id="fazerPerguntaBtn" disabled>Enviar pergunta</button>

    <div id="respostaSimNaoContainer" class="hidden" role="region" aria-live="polite" aria-label="Escolha a resposta sim ou não">
      <p><strong>Resposta:</strong></p>
      <button class="respostaBtn" data-resp="sim">Sim</button>
      <button class="respostaBtn" data-resp="nao">Não</button>
    </div>

    <p id="perguntasRestantes" aria-live="polite">Perguntas restantes nesta rodada: 3</p>
  </section>

  <!-- 3. Improviso de Palavras -->
  <section id="improviso">
    <h2>🧠 3. Improviso de Palavras</h2>
    <p><strong>Instruções:</strong> Clique em "Sortear palavras" para receber 3 a 5 palavras aleatórias. Você tem 1 minuto para inventar uma história usando todas.</p>

    <button id="sortearPalavrasImprovisoBtn">Sortear palavras</button>
    <p><strong>Palavras sorteadas:</strong></p>
    <ul id="palavrasImprovisoList" aria-live="polite"></ul>

    <div class="timer" id="timerImproviso" aria-live="polite">Tempo: 01:00</div>
    <button id="iniciarTimerImprovisoBtn" disabled>Iniciar tempo</button>
  </section>

  <!-- 4. História Coletiva -->
  <section id="historiaColetiva">
    <h2>📚 4. História Coletiva</h2>
    <p><strong>Instruções:</strong> Cada pessoa adiciona uma frase para construir a história. A história vai aparecendo na lista abaixo.</p>

    <label for="fraseHistoria">Digite uma frase para continuar a história:</label>
    <textarea id="fraseHistoria" rows="2" placeholder="Digite sua frase aqui..." aria-label="Frase para continuar a história"></textarea>
    <button id="adicionarFraseBtn">Adicionar frase</button>

    <div class="phrase-list" id="listaHistoria" aria-live="polite" aria-label="História coletiva"></div>
    <button id="resetarHistoriaBtn" style="margin-top:10px; background:#f44336;">Reiniciar história</button>
  </section>

<script>
  // --- Dados para os jogos ---

  const palavras = {
    biblicos: [
      "Moisés", "Noé", "Jesus", "Maria", "Pedro", "Paulo", "Davi", "Elias",
      "Abraão", "Sansão", "Isaías", "João Batista"
    ],
    profissoes: [
      "Médico", "Professor", "Bombeiro", "Policial", "Advogado",
      "Arquiteto", "Cozinheiro", "Jornalista", "Motorista"
    ],
    filmes: [
      "Harry Potter", "Star Wars", "Vingadores", "Frozen", "Matrix",
      "Titanic", "O Rei Leão", "Jurassic Park"
    ],
    emocoes: [
      "Alegria", "Raiva", "Tristeza", "Medo", "Surpresa", "Nojo", "Esperança"
    ],
    objetos: [
      "Chave", "Celular", "Relógio", "Livro", "Garfo", "Copo", "Caneta"
    ]
  };

  // --- Mímica Temática ---
  const sortearPalavraBtn = document.getElementById('sortearPalavraBtn');
  const palavraSorteadaEl = document.getElementById('palavraSorteada');
  const temaMimicaSelect = document.getElementById('temaMimica');
  const iniciarTimerBtn = document.getElementById('iniciarTimerBtn');
  const timerMimicaEl = document.getElementById('timerMimica');
  let timerMimicaId = null;
  let timerMimicaSegundos = 60;

  function sortearPalavra() {
    const tema = temaMimicaSelect.value;
    const lista = palavras[tema];
    const palavra = lista[Math.floor(Math.random() * lista.length)];
    palavraSorteadaEl.textContent = palavra;
    iniciarTimerBtn.disabled = false;
    resetTimerMimica();
  }

  function resetTimerMimica() {
    timerMimicaSegundos = 60;
    timerMimicaEl.textContent = "Tempo: 01:00";
    clearInterval(timerMimicaId);
  }

  function iniciarTimerMimica() {
    iniciarTimerBtn.disabled = true;
    timerMimicaId = setInterval(() => {
      timerMimicaSegundos--;
      const min = String(Math.floor(timerMimicaSegundos / 60)).padStart(2, '0');
      const seg = String(timerMimicaSegundos % 60).padStart(2, '0');
      timerMimicaEl.textContent = `Tempo: ${min}:${seg}`;
      if(timerMimicaSegundos <= 0) {
        clearInterval(timerMimicaId);
        alert("Tempo esgotado!");
        iniciarTimerBtn.disabled = false;
      }
    }, 1000);
  }

  sortearPalavraBtn.addEventListener('click', sortearPalavra);
  iniciarTimerBtn.addEventListener('click', iniciarTimerMimica);

  // --- Quem eu sou? ---
  const nomePersonagemInput = document.getElementById('nomePersonagem');
  const colocarNaTestaBtn = document.getElementById('colocarNaTestaBtn');
  const nomeNaTestaDisplay = document.getElementById('nomeNaTestaDisplay');
  const perguntaSimNaoInput = document.getElementById('perguntaSimNao');
  const fazerPerguntaBtn = document.getElementById('fazerPerguntaBtn');
  const respostaSimNaoContainer = document.getElementById('respostaSimNaoContainer');
  const respostasBtn = document.querySelectorAll('.respostaBtn');
  const perguntasRestantesEl = document.getElementById('perguntasRestantes');
  let perguntasRestantes = 3;
  let perguntaAtual = '';

  colocarNaTestaBtn.addEventListener('click', () => {
    const nome = nomePersonagemInput.value.trim();
    if(nome === '') {
      alert('Digite um nome válido.');
      return;
    }
    nomeNaTestaDisplay.textContent = nome;
    nomePersonagemInput.value = '';
    perguntasRestantes = 3;
    perguntasRestantesEl.textContent = `Perguntas restantes nesta rodada: ${perguntasRestantes}`;
    fazerPerguntaBtn.disabled = false;
    perguntaSimNaoInput.value = '';
    respostaSimNaoContainer.classList.add('hidden');
  });

  fazerPerguntaBtn.addEventListener('click', () => {
    const pergunta = perguntaSimNaoInput.value.trim();
    if(pergunta === '') {
      alert('Digite uma pergunta.');
      return;
    }
    perguntaAtual = pergunta;
    respostaSimNaoContainer.classList.remove('hidden');
    fazerPerguntaBtn.disabled = true;
  });

  respostasBtn.forEach(btn => {
    btn.addEventListener('click', () => {
      const resp = btn.dataset.resp;
      alert(`Pergunta: "${perguntaAtual}"\nResposta: ${resp.toUpperCase()}`);
      perguntasRestantes--;
      perguntasRestantesEl.textContent = `Perguntas restantes nesta rodada: ${perguntasRestantes}`;
      fazerPerguntaBtn.disabled = perguntasRestantes <= 0;
      respostaSimNaoContainer.classList.add('hidden');
      perguntaSimNaoInput.value = '';
      if(perguntasRestantes <= 0) {
        alert('Acabaram as perguntas desta rodada! Troquem de jogador.');
      }
    });
  });

  // --- Improviso de Palavras ---
  const sortearPalavrasImprovisoBtn = document.getElementById('sortearPalavrasImprovisoBtn');
  const palavrasImprovisoList = document.getElementById('palavrasImprovisoList');
  const iniciarTimerImprovisoBtn = document.getElementById('iniciarTimerImprovisoBtn');
  const timerImprovisoEl = document.getElementById('timerImproviso');
  let timerImprovisoId = null;
  let timerImprovisoSegundos = 60;

  const listaPalavrasImproviso = [
    "sol", "bicicleta", "padre", "sorvete", "deserto", "amizade", "miragem", "tempestade",
    "livro", "passagem", "estrela", "rio", "vento", "paz", "música", "milagre", "amigo"
  ];

  function sortearPalavrasImproviso() {
    palavrasImprovisoList.innerHTML = '';
    // Sorteia entre 3 e 5 palavras únicas
    const count = Math.floor(Math.random() * 3) + 3;
    let selecionadas = [];
    while(selecionadas.length < count) {
      const p = listaPalavrasImproviso[Math.floor(Math.random() * listaPalavrasImproviso.length)];
      if(!selecionadas.includes(p)) selecionadas.push(p);
    }
    selecionadas.forEach(palavra => {
      const li = document.createElement('li');
      li.textContent = palavra;
      palavrasImprovisoList.appendChild(li);
    });
    iniciarTimerImprovisoBtn.disabled = false;
    resetTimerImproviso();
  }

  function resetTimerImproviso() {
    timerImprovisoSegundos = 60;
    timerImprovisoEl.textContent = "Tempo: 01:00";
    clearInterval(timerImprovisoId);
  }

  function iniciarTimerImproviso() {
    iniciarTimerImprovisoBtn.disabled = true;
    timerImprovisoId = setInterval(() => {
      timerImprovisoSegundos--;
      const min = String(Math.floor(timerImprovisoSegundos / 60)).padStart(2, '0');
      const seg = String(timerImprovisoSegundos % 60).padStart(2, '0');
      timerImprovisoEl.textContent = `Tempo: ${min}:${seg}`;
      if(timerImprovisoSegundos <= 0) {
        clearInterval(timerImprovisoId);
        alert("Tempo esgotado!");
        iniciarTimerImprovisoBtn.disabled = false;
      }
    }, 1000);
  }

  sortearPalavrasImprovisoBtn.addEventListener('click', sortearPalavrasImproviso);
  iniciarTimerImprovisoBtn.addEventListener('click', iniciarTimerImproviso);

  // --- História Coletiva ---
  const fraseHistoriaInput = document.getElementById('fraseHistoria');
  const adicionarFraseBtn = document.getElementById('adicionarFraseBtn');
  const listaHistoriaEl = document.getElementById('listaHistoria');
  const resetarHistoriaBtn = document.getElementById('resetarHistoriaBtn');

  let historia = [];

  function atualizarHistoria() {
    listaHistoriaEl.innerHTML = '';
    historia.forEach((frase, i) => {
      const p = document.createElement('p');
      p.textContent = `${i + 1}. ${frase}`;
      listaHistoriaEl.appendChild(p);
    });
  }

  adicionarFraseBtn.addEventListener('click', () => {
    const texto = fraseHistoriaInput.value.trim();
    if(texto === '') {
      alert('Digite uma frase para continuar a história.');
      return;
    }
    historia.push(texto);
    fraseHistoriaInput.value = '';
    atualizarHistoria();
  });

  resetarHistoriaBtn.addEventListener('click', () => {
    if(confirm('Quer reiniciar a história? Isso apagará tudo.')) {
      historia = [];
      atualizarHistoria();
    }
  });

</script>

</body>
</html>

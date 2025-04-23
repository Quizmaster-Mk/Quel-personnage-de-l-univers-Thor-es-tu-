<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Quel personnage de Thor es-tu ?</title>
  <style>
    body {
      font-family: 'Courier New', monospace;
      background-color: #000; /* Noir Asgardien */
      color: #d4af37; /* Or */
      margin: 0;
      padding: 20px;
      text-align: center;
    }

    h1 {
      color: #d4af37; /* Or */
      font-size: 40px;
      margin-bottom: 20px;
    }

    img.logo {
      max-width: 200px;
      margin-bottom: 20px;
    }

    .question {
      margin: 20px 0;
      background-color: #1c1c1c; /* Noir profond */
      padding: 20px;
      border-radius: 10px;
      border: 1px solid #c0c0c0; /* Argenté */
    }

    .options button {
      background-color: #d4af37;
      color: #000;
      padding: 10px 20px;
      border: none;
      margin: 5px;
      font-size: 18px;
      cursor: pointer;
      border-radius: 5px;
      transition: all 0.3s ease;
    }

    .options button:hover {
      background-color: #c0c0c0; /* Argent */
      color: #000;
      transform: scale(1.1);
    }

    .result {
      background-color: #1c1c1c;
      padding: 20px;
      border-radius: 10px;
      margin-top: 20px;
      display: none;
      border: 1px solid #c0c0c0;
    }

    .score {
      font-size: 18px;
      margin-top: 10px;
      color: #fff;
    }
  </style>
</head>
<body>
  <img class="logo" src="https://zupimages.net/up/25/17/tzze.jpg" alt="Logo Thor">
  <h1>Quel personnage de Thor es-tu ?</h1>

  <div id="quiz-container">
    <div class="question" id="question-container">
      <h2 id="question-text"></h2>
      <div class="options" id="options-container"></div>
    </div>
  </div>

  <div class="result" id="result-container">
    <h2>Tu es...</h2>
    <p id="result-text"></p>
    <p class="score">Ton résultat est basé sur tes choix !</p>
    <button onclick="startQuiz()">Rejouer</button>
  </div>

  <script>
    const questions = [
      { question: "Quelle est ta plus grande force ?", options: ["La loyauté", "La ruse", "La puissance", "La sagesse"], result: [0, 1, 2, 3] },
      { question: "Ton arme préférée ?", options: ["Un marteau magique", "Une lance redoutable", "Des illusions", "La science Asgardienne"], result: [0, 1, 2, 3] },
      { question: "Quel est ton plus grand défaut ?", options: ["L’arrogance", "La jalousie", "La colère", "L’obstination"], result: [2, 1, 0, 3] },
      { question: "Où préfères-tu vivre ?", options: ["Asgard", "Midgard (la Terre)", "Jotunheim", "N’importe où tant qu’il y a des combats"], result: [0, 3, 1, 2] },
      { question: "Quel est ton plus grand ennemi ?", options: ["Moi-même", "Mon frère", "Les mortels", "Le destin"], result: [1, 0, 2, 3] }
    ];

    const characters = [
      { name: "Thor", description: "Le dieu du tonnerre ! Fort, courageux, parfois un peu impulsif, mais toujours prêt à défendre les neuf royaumes." },
      { name: "Loki", description: "Le dieu de la malice. Rusé, charmeur, parfois dangereux… mais impossible à ignorer." },
      { name: "Odin", description: "Le sage souverain d’Asgard. Puissant, réfléchi, et gardien des plus grands secrets de l’univers." },
      { name: "Heimdall", description: "Le gardien du Bifröst. Toujours vigilant, noble et prêt à tout pour protéger Asgard." },
      { name: "Hela", description: "La déesse de la mort. Puissante, impitoyable, et déterminée à réclamer ce qui lui revient." },
      { name: "Valkyrie", description: "Guerrière intrépide d’Asgard. Rebelle mais loyale, elle combat pour un avenir meilleur." }
    ];

    let currentQuestion = 0;
    let userAnswers = [];

    function startQuiz() {
      currentQuestion = 0;
      userAnswers = [];
      document.getElementById('result-container').style.display = 'none';
      document.getElementById('quiz-container').style.display = 'block';
      showQuestion();
    }

    function showQuestion() {
      const question = questions[currentQuestion];
      document.getElementById('question-text').innerText = question.question;

      const optionsContainer = document.getElementById('options-container');
      optionsContainer.innerHTML = '';

      question.options.forEach((option, index) => {
        const button = document.createElement('button');
        button.innerText = option;
        button.onclick = () => {
          userAnswers.push(question.result[index]);
          currentQuestion++;
          if (currentQuestion < questions.length) {
            showQuestion();
          } else {
            showResult();
          }
        };
        optionsContainer.appendChild(button);
      });
    }

    function showResult() {
      const resultIndex = userAnswers.reduce((a, b) => a + b, 0) % characters.length;
      const result = characters[resultIndex];
      document.getElementById('result-text').innerText = `${result.name} - ${result.description}`;
      document.getElementById('quiz-container').style.display = 'none';
      document.getElementById('result-container').style.display = 'block';
    }

    startQuiz();
  </script>
</body>
</html>

<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Quiz Interativo: Você está no controle... ou a tela está?</title>
<style>
body {
    font-family: Arial, sans-serif;
    background: #f5f6fa;
    margin: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
}
.quiz-container {
    background: #fff;
    padding: 20px;
    border-radius: 15px;
    width: 90%;
    max-width: 600px;
    box-shadow: 0 4px 8px rgba(0,0,0,0.2);
}
h1 {
    text-align: center;
    color: #2c3e50;
}
.question {
    font-size: 18px;
    margin-bottom: 15px;
}
.option {
    background: #ecf0f1;
    padding: 10px;
    margin: 8px 0;
    border-radius: 8px;
    cursor: pointer;
    transition: 0.3s;
}
.option:hover {
    background: #dcdde1;
}
.correct {
    background-color: #2ecc71 !important;
    color: #fff;
}
.wrong {
    background-color: #e74c3c !important;
    color: #fff;
}
button {
    background: #3498db;
    color: white;
    border: none;
    padding: 10px 15px;
    font-size: 16px;
    border-radius: 8px;
    cursor: pointer;
    margin-top: 10px;
    display: none;
}
button:hover {
    background: #2980b9;
}
.result {
    text-align: center;
    font-size: 20px;
    font-weight: bold;
}
</style>
</head>
<body>

<div class="quiz-container">
    <h1>Quiz Interativo: Você está no controle... ou a tela está?</h1>
    <div id="quiz"></div>
    <button id="next-btn">Próxima</button>
</div>

<script>
const quizData = [
    { question: "O que é considerado empregado em telas?", options: ["Usar o celular para trabalhar","O uso excessivo de dispositivos que afetam a saúde física, mental ou os relacionamentos pessoais","Assistir televisão por mais de uma hora por dia","Usar redes sociais sociais"], answer: 1 },
    { question: "Qual das seguintes opções NÃO é um sinal de alerta de dependência em telas?", options: ["Dificuldade de ficar longe do celular","Ansiedade ao não estar online","Usar o celular antes de dormir","Uso prolongado sem perceber o tempo passar"], answer: 2 },
    { question: "Qual é um dos efeitos do uso exagerado de redes sociais como Instagram e TikTok?", options: ["Aumento da autoestima","Melhoria da concentração","Perda de tempo produtiva","Mais interação social"], answer: 2 },
    { question: "Qual destas é uma dica para usar telas com equilíbrio?", options: ["Usar o celular na cama antes de dormir","Evitar conversas pessoais com amigos","Priorizar atividades ao ar livre","Passar o máximo de tempo possível nas redes sociais"], answer: 2 },
    { question: "Qual a mensagem principal do 'Lembre-se' no final do texto?", options: ["As telas foram feitas para controlar a vida das pessoas","A saúde mental não é tão importante quanto o uso das telas","As telas foram feitas para facilitar a vida, não para controlá-la, e a saúde mental importante","Não é necessário procurar ajuda se sentir que perdeu o controle"], answer: 2 },
    { question: "Qual é uma consequência do uso excessivo de telas antes de dormir?", options: ["Melhora do sono","Mais energia ao acordar","Dificuldade para dormir e insônia","Aumento da concentração"], answer: 2 },
    { question: "Uma forma de reduzir o tempo em redes sociais é:", options: ["Desligar notificações","Ficar online o tempo todo","Seguir perfis aleatórios","Usar o celular na cama"], answer: 0 },
    { question: "O que é saudável fazer durante o tempo de lazer?", options: ["Ficar exclusivamente nas redes sociais","Priorizar atividades físicas ou hobbies offline","Evitar qualquer contato com amigos","Usar telas antes de dormir"], answer: 1 },
    { question: "Como identificar se uma pessoa está usando telas de forma equilibrada?", options: ["Ela se sente ansiosa ao desligar o celular","Ela consegue equilibrar tempo online e offline","Ela nunca se exercita","Ela usa redes sociais 24h por dia"], answer: 1 },
    { question: "Por que é importante controlar o uso de telas?", options: ["Para melhorar a saúde mental, física e relacionamentos","Para se tornar dependente das redes sociais","Para perder tempo produtivo","Para evitar dormir"], answer: 0 }
];

let currentQuestion = 0;
let score = 0;

const quiz = document.getElementById("quiz");
const nextBtn = document.getElementById("next-btn");

function loadQuestion() {
    const q = quizData[currentQuestion];
    quiz.innerHTML = `<div class="question">${q.question}</div>` +
        q.options.map((opt, i) => `<div class="option" onclick="selectOption(this, ${i})">${opt}</div>`).join("");
    nextBtn.style.display = "none";
}

function selectOption(element, selected) {
    const correct = quizData[currentQuestion].answer;
    if(selected === correct){
        element.classList.add('correct');
        score++;
    } else {
        element.classList.add('wrong');
        // Marcar a correta
        document.querySelectorAll('.option')[correct].classList.add('correct');
    }
    // Desabilitar todas as opções
    document.querySelectorAll('.option').forEach(opt => opt.style.pointerEvents = 'none');
    nextBtn.style.display = "block";
}

nextBtn.addEventListener('click', () => {
    currentQuestion++;
    if(currentQuestion < quizData.length){
        loadQuestion();
    } else {
        quiz.innerHTML = `<div class="result">Você acertou ${score} de ${quizData.length} perguntas!</div>`;
        nextBtn.style.display = "none";
    }
});

loadQuestion();
</script>

</body>
</html>

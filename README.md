<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ferramenta de Estudo Interativa</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f5f5f5;
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
            padding: 20px;
        }
        .input-group, .card {
            background-color: #fff;
            border: 2px solid #4CAF50;
            border-radius: 8px;
            width: 300px;
            padding: 20px;
            box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1);
            text-align: center;
            margin-bottom: 15px;
        }
        .input-group input, .input-group textarea {
            width: 100%;
            padding: 10px;
            margin-top: 10px;
            font-size: 16px;
        }
        .btn {
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 4px;
            padding: 10px 20px;
            font-size: 16px;
            cursor: pointer;
            margin-top: 10px;
        }
        .btn:hover {
            background-color: #45a049;
        }
        .card .question, .card .answer {
            color: #333;
            font-size: 18px;
            margin: 15px 0;
        }
    </style>
</head>
<body>

<div class="input-group">
    <label for="question">Digite sua pergunta:</label>
    <input type="text" id="question" placeholder="Ex: Qual é a capital da França?">
    <label for="answer">Digite sua resposta:</label>
    <textarea id="answer" rows="3" placeholder="Ex: Paris"></textarea>
    <button class="btn" onclick="addCard()">Adicionar Pergunta</button>
</div>

<div id="card-container"></div>

<button class="btn" onclick="downloadCards()">Baixar Conteúdo</button>

<script>
    function addCard() {
        const question = document.getElementById('question').value;
        const answer = document.getElementById('answer').value;
        
        if (question && answer) {
            const cardContainer = document.getElementById('card-container');
            
            const card = document.createElement('div');
            card.className = 'card';
            
            const questionElement = document.createElement('div');
            questionElement.className = 'question';
            questionElement.innerText = question;
            
            const answerElement = document.createElement('div');
            answerElement.className = 'answer';
            answerElement.innerText = answer;
            answerElement.style.display = 'none';
            
            const toggleButton = document.createElement('button');
            toggleButton.className = 'btn';
            toggleButton.innerText = 'Mostrar Resposta';
            toggleButton.onclick = function() {
                if (answerElement.style.display === 'none') {
                    answerElement.style.display = 'block';
                    toggleButton.innerText = 'Ocultar Resposta';
                } else {
                    answerElement.style.display = 'none';
                    toggleButton.innerText = 'Mostrar Resposta';
                }
            };
            
            card.appendChild(questionElement);
            card.appendChild(answerElement);
            card.appendChild(toggleButton);
            cardContainer.appendChild(card);

            document.getElementById('question').value = '';
            document.getElementById('answer').value = '';
        } else {
            alert('Por favor, preencha tanto a pergunta quanto a resposta.');
        }
    }

    function downloadCards() {
        const cards = document.querySelectorAll('.card');
        let content = '';
        
        cards.forEach((card, index) => {
            const question = card.querySelector('.question').innerText;
            const answer = card.querySelector('.answer').innerText;
            content += Pergunta ${index + 1}: ${question}\nResposta: ${answer}\n\n;
        });
        
        const blob = new Blob([content], { type: 'text/plain' });
        const link = document.createElement('a');
        link.href = URL.createObjectURL(blob);
        link.download = 'cartoes_de_estudo.txt';
        link.click();
    }
</script>

</body>
</html>

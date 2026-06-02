# robkanovaleksei-boop.github.io<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <title>TikTok удаляет детей без апелляции!</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            background: linear-gradient(135deg, #ff0050, #00f2ea);
            color: white;
            text-align: center;
        }
        .container {
            background: rgba(0,0,0,0.8);
            padding: 30px;
            border-radius: 20px;
            margin-top: 50px;
        }
        input, textarea {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            border-radius: 10px;
            border: none;
        }
        button {
            background: #ff0050;
            color: white;
            padding: 15px 30px;
            border: none;
            border-radius: 10px;
            font-size: 18px;
            cursor: pointer;
        }
        button:hover { background: #ff3366; }
        #counter {
            font-size: 48px;
            font-weight: bold;
            color: #00f2ea;
        }
        .complaint {
            background: rgba(255,255,255,0.1);
            padding: 10px;
            margin: 10px 0;
            border-radius: 10px;
            text-align: left;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>😡 TikTok удалил мой аккаунт без апелляции!</h1>
        <h2>Они игнорируют детей! Требуем справедливости!</h2>
        
        <div>
            <h3>Подписей под жалобой:</h3>
            <div id="counter">0</div>
        </div>

        <form id="complaintForm">
            <input type="text" id="name" placeholder="Ваше имя (можно анонимно)" required>
            <input type="number" id="age" placeholder="Ваш возраст" required>
            <textarea id="story" placeholder="Расскажите, как TikTok удалил ваш аккаунт..." rows="4"></textarea>
            <button type="submit">✊ Подписать жалобу!</button>
        </form>

        <div id="complaints"></div>
    </div>

    <script>
        // Загружаем подписи из localStorage
        let signatures = JSON.parse(localStorage.getItem('tiktokComplaints') || '[]');
        updateCounter();

        document.getElementById('complaintForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const complaint = {
                name: document.getElementById('name').value || 'Аноним',
                age: document.getElementById('age').value,
                story: document.getElementById('story').value,
                date: new Date().toLocaleString()
            };
            
            signatures.push(complaint);
            localStorage.setItem('tiktokComplaints', JSON.stringify(signatures));
            
            updateCounter();
            displayComplaints();
            this.reset();
            
            alert('✅ Спасибо! Ваша жалоба добавлена!');
        });

        function updateCounter() {
            document.getElementById('counter').textContent = signatures.length;
        }

        function displayComplaints() {
            const container = document.getElementById('complaints');
            container.innerHTML = signatures.map(c => 
                `<div class="complaint">
                    <strong>${c.name}</strong> (${c.age} лет)<br>
                    <small>${c.date}</small><br>
                    ${c.story}
                </div>`
            ).join('');
        }

        displayComplaints();
    </script>
</body>
</html>

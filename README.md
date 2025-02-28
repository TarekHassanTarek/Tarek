<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <title>تمساح جائع!</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background: #87CEEB;
            text-align: center;
        }
        
        .container {
            margin: 50px auto;
            max-width: 800px;
            padding: 20px;
        }
        
        .emoji {
            font-size: 100px;
            margin: 20px;
        }
        
        button {
            padding: 15px 30px;
            font-size: 20px;
            background: #4CAF50;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            margin: 10px;
        }
        
        button:hover {
            background: #45a049;
        }
        
        #message {
            font-size: 24px;
            color: #333;
            margin: 20px;
            min-height: 30px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>التمساح الجائع 🐊</h1>
        <div class="emoji" id="croc">🐊</div>
        <div class="emoji" id="fish">🐟</div>
        <div id="message"></div>
        <button onclick="croc.eat()">أكل السمكة!</button>
        <button onclick="resetGame()">إعادة اللعبة</button>
    </div>

    <script>
        class Fish {
            constructor() {
                this.alive = true;
            }

            isAlive() {
                return this.alive;
            }

            beEaten() {
                this.alive = false;
            }
        }

        class Crocodile {
            constructor() {
                this.fish = new Fish();
                this.updateUI();
            }

            eat() {
                const fishElement = document.getElementById('fish');
                const messageElement = document.getElementById('message');

                if (this.fish.isAlive()) {
                    this.fish.beEaten();
                    fishElement.style.opacity = '0.3';
                    messageElement.innerHTML = '🐊 التمساح أكل السمكة! 🐟💔';
                    sessionStorage.setItem('fishState', 'eaten');
                } else {
                    messageElement.innerHTML = '⚠️ لا توجد سمكة حية!';
                }
            }

            updateUI() {
                const fishState = sessionStorage.getItem('fishState');
                if (fishState === 'eaten') {
                    this.fish.beEaten();
                    document.getElementById('fish').style.opacity = '0.3';
                }
            }
        }

        const croc = new Crocodile();

        function resetGame() {
            sessionStorage.removeItem('fishState');
            croc.fish = new Fish();
            document.getElementById('fish').style.opacity = '1';
            document.getElementById('message').innerHTML = '';
        }

        // التحقق من الحالة عند تحميل الصفحة
        window.onload = () => croc.updateUI();
    </script>
</body>
</html>

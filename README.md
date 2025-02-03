<!DOCTYPE html>
<html>
<head>
    <title>Organixia: Zap Acne!</title>
    <style>
        body {
            margin: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background: #ffe6f2; /* Light pink background */
        }
        #game-container {
            width: 300px;
            height: 500px;
            position: relative;
            background: url('https://raw.githubusercontent.com/YOUR-GITHUB-USERNAME/REPO-NAME/main/skincare-bg.jpg');
            background-size: cover;
            border-radius: 15px;
            overflow: hidden;
        }
        .acne {
            width: 50px;
            height: 50px;
            position: absolute;
            cursor: pointer;
            background: url('https://raw.githubusercontent.com/YOUR-GITHUB-USERNAME/REPO-NAME/main/acne-icon.png');
            background-size: cover;
            animation: float 2s infinite;
        }
        #score, #timer {
            color: white;
            font-size: 20px;
            font-family: Arial;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
            padding: 10px;
        }
        #score { position: absolute; top: 10px; left: 10px; }
        #timer { position: absolute; top: 10px; right: 10px; }
        @keyframes float {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
        }
    </style>
</head>
<body>
    <div id="game-container">
        <div id="score">Score: 0</div>
        <div id="timer">Time: 30</div>
    </div>

    <script>
        let score = 0;
        let timeLeft = 30;
        const targetScore = 15; // Score needed to win

        // Create acne elements
        function createAcne() {
            const acne = document.createElement('div');
            acne.className = 'acne';
            acne.style.left = Math.random() * 250 + 'px'; // Random X position
            acne.style.top = Math.random() * 450 + 'px'; // Random Y position
            
            acne.onclick = () => {
                score++;
                document.getElementById('score').textContent = `Score: ${score}`;
                acne.remove();
                if (score >= targetScore) showDiscount();
            };

            document.getElementById('game-container').appendChild(acne);
        }

        // Timer countdown
        const timer = setInterval(() => {
            timeLeft--;
            document.getElementById('timer').textContent = `Time: ${timeLeft}`;
            if (timeLeft <= 0) endGame();
        }, 1000);

        // Spawn new acne every 0.8 seconds
        setInterval(createAcne, 800);

        // Win condition
        function showDiscount() {
            clearInterval(timer);
            document.getElementById('game-container').innerHTML = `
                <div style="text-align:center; padding-top:200px; color:white;">
                    <h2>🎉 You Won!</h2>
                    <p>Use code: <strong>GLOW20</strong></p>
                    <p>20% OFF Organixia Acne Care Kit</p>
                    <button style="padding:10px 20px; background:#ff69b4; border:none; color:white; border-radius:5px; cursor:pointer;" 
                            onclick="window.location.href='https://organixia.com'">
                        CLAIM NOW
                    </button>
                </div>
            `;
        }

        // Lose condition
        function endGame() {
            document.getElementById('game-container').innerHTML = `
                <div style="text-align:center; padding-top:200px; color:white;">
                    <h2>Time's Up! 😢</h2>
                    <p>Try again to unlock your discount!</p>
                </div>
            `;
        }
    </script>
</body>
</html>

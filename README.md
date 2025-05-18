# Rock-paper-scissorss
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ultimate Rock Paper Scissors</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;700&family=Press+Start+2P&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #4361ee;
            --secondary: #f72585;
            --accent: #4cc9f0;
            --dark: #2b2d42;
            --light: #f8f9fa;
            --success: #38b000;
            --danger: #d00000;
            --warning: #ffaa00;
            --neutral: #adb5bd;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Poppins', sans-serif;
            background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 20px;
            color: var(--dark);
        }

        .game-container {
            background: rgba(255, 255, 255, 0.9);
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.15);
            padding: 30px;
            width: 100%;
            max-width: 600px;
            text-align: center;
            backdrop-filter: blur(5px);
            border: 1px solid rgba(255, 255, 255, 0.3);
            transition: all 0.3s ease;
        }

        h1 {
            font-family: 'Press Start 2P', cursive;
            font-size: 2rem;
            margin-bottom: 15px;
            background: linear-gradient(to right, var(--primary), var(--secondary));
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
        }

        .game-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }

        .score-display {
            display: flex;
            gap: 20px;
            font-size: 1.2rem;
        }

        .score {
            padding: 8px 15px;
            border-radius: 10px;
            font-weight: 600;
        }

        .player-score {
            background-color: rgba(67, 97, 238, 0.1);
            color: var(--primary);
        }

        .computer-score {
            background-color: rgba(247, 37, 133, 0.1);
            color: var(--secondary);
        }

        .game-area {
            margin: 25px 0;
        }

        .choices {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin: 30px 0;
        }

        .choice-btn {
            background: white;
            border: none;
            border-radius: 50%;
            width: 90px;
            height: 90px;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: all 0.3s ease;
            font-size: 2.5rem;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            position: relative;
            overflow: hidden;
        }

        .choice-btn::after {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            border-radius: 50%;
            opacity: 0;
            transition: opacity 0.3s ease;
        }

        .choice-btn:hover::after {
            opacity: 0.1;
        }

        .choice-btn:hover {
            transform: translateY(-5px) scale(1.05);
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.15);
        }

        .choice-btn:active {
            transform: translateY(0) scale(0.98);
        }

        #rock {
            background-color: rgba(255, 0, 0, 0.1);
        }
        #rock::after {
            background: var(--danger);
        }

        #paper {
            background-color: rgba(0, 0, 255, 0.1);
        }
        #paper::after {
            background: var(--primary);
        }

        #scissors {
            background-color: rgba(0, 255, 0, 0.1);
        }
        #scissors::after {
            background: var(--success);
        }

        .result-display {
            min-height: 100px;
            display: flex;
            flex-direction: column;
            justify-content: center;
            margin: 20px 0;
        }

        #result-text {
            font-size: 1.5rem;
            font-weight: 700;
            margin-bottom: 10px;
        }

        #round-info {
            color: var(--dark);
            opacity: 0.8;
            font-size: 1.1rem;
        }

        .moves-display {
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 30px;
            margin: 30px 0;
            font-size: 3rem;
        }

        .vs {
            font-family: 'Press Start 2P', cursive;
            font-size: 1rem;
            color: var(--neutral);
        }

        .action-buttons {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin-top: 20px;
        }

        .btn {
            padding: 12px 25px;
            border-radius: 50px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            border: none;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 15px rgba(0, 0, 0, 0.15);
        }

        .btn:active {
            transform: translateY(0);
        }

        .reset-btn {
            background-color: var(--dark);
            color: white;
        }

        .new-game-btn {
            background-color: var(--primary);
            color: white;
        }

        .win {
            color: var(--success);
        }

        .lose {
            color: var(--danger);
        }

        .draw {
            color: var(--warning);
        }

        .confetti {
            position: fixed;
            width: 10px;
            height: 10px;
            background-color: var(--accent);
            opacity: 0;
            animation: confetti-fall 5s ease-in-out forwards;
        }

        @keyframes confetti-fall {
            0% {
                transform: translateY(-100vh) rotate(0deg);
                opacity: 1;
            }
            100% {
                transform: translateY(100vh) rotate(360deg);
                opacity: 0;
            }
        }

        @media (max-width: 600px) {
            h1 {
                font-size: 1.5rem;
            }
            .choice-btn {
                width: 70px;
                height: 70px;
                font-size: 2rem;
            }
            .moves-display {
                font-size: 2.5rem;
                gap: 20px;
            }
        }
    </style>
</head>
<body>
    <div class="game-container">
        <h1>ROCK PAPER SCISSORS</h1>
        
        <div class="game-header">
            <div class="score-display">
                <div class="score player-score">YOU: <span id="player-score">0</span></div>
                <div class="score computer-score">CPU: <span id="computer-score">0</span></div>
            </div>
        </div>
        
        <div class="game-area">
            <div class="result-display">
                <div id="result-text">Choose your weapon!</div>
                <div id="round-info">First to score 5 points wins the game</div>
            </div>
            
            <div class="moves-display">
                <div id="player-move">❔</div>
                <div class="vs">VS</div>
                <div id="computer-move">❔</div>
            </div>
            
            <div class="choices">
                <button id="rock" class="choice-btn" title="Rock" aria-label="Rock">✊</button>
                <button id="paper" class="choice-btn" title="Paper" aria-label="Paper">✋</button>
                <button id="scissors" class="choice-btn" title="Scissors" aria-label="Scissors">✌️</button>
            </div>
        </div>
        
        <div class="action-buttons">
            <button id="reset-btn" class="btn reset-btn">Reset Score</button>
            <button id="new-game-btn" class="btn new-game-btn">New Game</button>
        </div>
    </div>

    <script>
        const buttons = document.querySelectorAll('.choice-btn');
        const playerScoreEl = document.getElementById('player-score');
        const computerScoreEl = document.getElementById('computer-score');
        const resultTextEl = document.getElementById('result-text');
        const roundInfoEl = document.getElementById('round-info');
        const playerMoveEl = document.getElementById('player-move');
        const computerMoveEl = document.getElementById('computer-move');
        const resetBtn = document.getElementById('reset-btn');
        const newGameBtn = document.getElementById('new-game-btn');
        const gameContainer = document.querySelector('.game-container');
        
        let playerScore = 0;
        let computerScore = 0;
        let roundCount = 0;
        let gameOver = false;
        
        const emojis = {
            rock: '✊',
            paper: '✋',
            scissors: '✌️',
            default: '❔'
        };
        
        const sounds = {
            win: new Audio('https://assets.mixkit.co/sfx/preview/mixkit-winning-chimes-2015.mp3'),
            lose: new Audio('https://assets.mixkit.co/sfx/preview/mixkit-retro-arcade-lose-2027.mp3'),
            draw: new Audio('https://assets.mixkit.co/sfx/preview/mixkit-neutral-game-notification-951.mp3'),
            click: new Audio('https://assets.mixkit.co/sfx/preview/mixkit-electronic-click-1118.mp3')
        };
        
        initGame();
        
        buttons.forEach(button => {
            button.addEventListener('click', () => handleChoice(button.id));
        });
        
        resetBtn.addEventListener('click', resetScore);
        newGameBtn.addEventListener('click', initGame);
        
        function initGame() {
            playerScore = 0;
            computerScore = 0;
            roundCount = 0;
            gameOver = false;
            
            updateScoreDisplay();
            playerMoveEl.textContent = emojis.default;
            computerMoveEl.textContent = emojis.default;
            
            resultTextEl.textContent = 'Choose your weapon!';
            resultTextEl.className = '';
            roundInfoEl.textContent = 'First to score 5 points wins the game';
            
            gameContainer.style.transform = 'scale(1)';
            enableChoiceButtons();
        }
        
        function handleChoice(playerChoice) {
            if (gameOver) return;
            
            playSound('click');
            roundCount++;
            
            const computerChoice = getComputerChoice();
            const winner = determineWinner(playerChoice, computerChoice);
            
            updateMovesDisplay(playerChoice, computerChoice);
            updateScore(winner);
            displayResult(playerChoice, computerChoice, winner);
            checkGameStatus();
            
            gameContainer.style.transform = 'scale(0.98)';
            setTimeout(() => {
                gameContainer.style.transform = 'scale(1)';
            }, 100);
        }
        
        function getComputerChoice() {
            const choices = ['rock', 'paper', 'scissors'];
            return choices[Math.floor(Math.random() * 3)];
        }
        
        function determineWinner(player, computer) {
            if (player === computer) return 'draw';
            
            const winConditions = {
                rock: 'scissors',
                paper: 'rock',
                scissors: 'paper'
            };
            
            return winConditions[player] === computer ? 'player' : 'computer';
        }
        
        function updateMovesDisplay(player, computer) {
            playerMoveEl.textContent = emojis[player];
            computerMoveEl.textContent = emojis[computer];
            
            playerMoveEl.classList.add('animate-move');
            computerMoveEl.classList.add('animate-move');
            
            setTimeout(() => {
                playerMoveEl.classList.remove('animate-move');
                computerMoveEl.classList.remove('animate-move');
            }, 500);
        }
        
        function updateScore(winner) {
            if (winner === 'player') playerScore++;
            if (winner === 'computer') computerScore++;
            
            updateScoreDisplay();
        }
        
        function updateScoreDisplay() {
            playerScoreEl.textContent = playerScore;
            computerScoreEl.textContent = computerScore;
        }
        
        function displayResult(player, computer, winner) {
            const playerChoice = capitalize(player);
            const computerChoice = capitalize(computer);
            
            if (winner === 'draw') {
                resultTextEl.textContent = "It's a Draw!";
                resultTextEl.className = 'draw';
                roundInfoEl.textContent = `Both chose ${playerChoice}`;
                playSound('draw');
            } else if (winner === 'player') {
                resultTextEl.textContent = "You Win!";
                resultTextEl.className = 'win';
                roundInfoEl.textContent = `${playerChoice} beats ${computerChoice}`;
                playSound('win');
            } else {
                resultTextEl.textContent = "You Lose!";
                resultTextEl.className = 'lose';
                roundInfoEl.textContent = `${computerChoice} beats ${playerChoice}`;
                playSound('lose');
            }
        }
        
        function checkGameStatus() {
            if (playerScore >= 5 || computerScore >= 5) {
                gameOver = true;
                disableChoiceButtons();
                
                if (playerScore >= 5) {
                    resultTextEl.textContent = "🎉 You Won the Game!";
                    roundInfoEl.textContent = `Final Score: ${playerScore}-${computerScore}`;
                    createConfetti();
                } else {
                    resultTextEl.textContent = "💻 Computer Won!";
                    roundInfoEl.textContent = `Final Score: ${playerScore}-${computerScore}`;
                }
            }
        }
        
        function resetScore() {
            playerScore = 0;
            computerScore = 0;
            updateScoreDisplay();
            
            if (gameOver) {
                resultTextEl.textContent = 'Choose your weapon!';
                resultTextEl.className = '';
                roundInfoEl.textContent = 'First to score 5 points wins the game';
                gameOver = false;
                enableChoiceButtons();
            }
            
            playSound('click');
        }
        
        function disableChoiceButtons() {
            buttons.forEach(button => {
                button.disabled = true;
                button.style.opacity = '0.6';
                button.style.cursor = 'not-allowed';
            });
        }
        
        function enableChoiceButtons() {
            buttons.forEach(button => {
                button.disabled = false;
                button.style.opacity = '1';
                button.style.cursor = 'pointer';
            });
        }
        
        function playSound(type) {
            if (sounds[type]) {
                sounds[type].currentTime = 0;
                sounds[type].play().catch(e => console.log("Audio play failed:", e));
            }
        }
        
        function createConfetti() {
            for (let i = 0; i < 100; i++) {
                const confetti = document.createElement('div');
                confetti.className = 'confetti';
                confetti.style.left = `${Math.random() * 100}vw`;
                confetti.style.backgroundColor = getRandomColor();
                confetti.style.animationDuration = `${Math.random() * 3 + 2}s`;
                confetti.style.animationDelay = `${Math.random() * 0.5}s`;
                document.body.appendChild(confetti);
                
                setTimeout(() => {
                    confetti.remove();
                }, 5000);
            }
        }
        
        function getRandomColor() {
            const colors = ['#4361ee', '#f72585', '#4cc9f0', '#7209b7', '#3a0ca3'];
            return colors[Math.floor(Math.random() * colors.length)];
        }
        
        function capitalize(str) {
            return str.charAt(0).toUpperCase() + str.slice(1);
        }
    </script>
</body>
</html>

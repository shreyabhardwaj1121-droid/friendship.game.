<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Friendship Button Game</title>
    <style>
        body {
            font-family: 'Comic Sans MS', cursive, sans-serif;
            margin: 0;
            padding: 0;
            background: linear-gradient(135deg, #ffeaa7, #fab1a0, #a29bfe, #fd79a8);
            background-size: 400% 400%;
            animation: gradientShift 10s ease infinite;
            overflow: hidden;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            position: relative;
        }

        @keyframes gradientShift {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        .doodle {
            position: absolute;
            font-size: 2rem;
            animation: float 6s ease-in-out infinite;
            opacity: 0.7;
        }

        .doodle:nth-child(odd) { animation-delay: -2s; }
        .doodle:nth-child(even) { animation-delay: -4s; }

        @keyframes float {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-20px); }
        }

        .heart { color: #ff7675; }
        .star { color: #fdcb6e; }
        .sparkle { color: #a29bfe; }
        .smiley { color: #fd79a8; }
        .cloud { color: #74b9ff; }
        .arrow { color: #00b894; }
        .sticker { color: #e17055; }

        .game-container {
            background: rgba(255, 255, 255, 0.9);
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            text-align: center;
            max-width: 500px;
            position: relative;
            z-index: 1;
        }

        h1 {
            color: #2d3436;
            font-size: 2.5rem;
            margin-bottom: 20px;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
        }

        .buttons {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
            margin-bottom: 20px;
        }

        button {
            background: linear-gradient(45deg, #ffeaa7, #fab1a0);
            border: none;
            border-radius: 15px;
            padding: 15px 20px;
            font-size: 1.2rem;
            font-weight: bold;
            color: #2d3436;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            position: relative;
            overflow: hidden;
        }

        button::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.4), transparent);
            transition: left 0.5s;
        }

        button:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
            background: linear-gradient(45deg, #fab1a0, #ffeaa7);
        }

        button:hover::before {
            left: 100%;
        }

        button:active {
            transform: translateY(0);
        }

        #message {
            font-size: 1.5rem;
            color: #2d3436;
            margin-top: 20px;
            min-height: 50px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <!-- Floating Doodle Elements -->
    <div class="doodle heart" style="top: 10%; left: 10%;">♥</div>
    <div class="doodle star" style="top: 20%; right: 15%;">★</div>
    <div class="doodle sparkle" style="bottom: 30%; left: 20%;">✨</div>
    <div class="doodle smiley" style="top: 40%; right: 10%;">☺</div>
    <div class="doodle cloud" style="bottom: 20%; left: 30%;">☁</div>
    <div class="doodle arrow" style="top: 60%; right: 20%;">➤</div>
    <div class="doodle sticker" style="bottom: 10%; right: 30%;">🏷</div>
    <div class="doodle heart" style="top: 70%; left: 15%;">♥</div>
    <div class="doodle star" style="bottom: 40%; right: 5%;">★</div>
    <div class="doodle sparkle" style="top: 30%; left: 40%;">✨</div>

    <div class="game-container">
        <h1>🌟 Friendship Button Game! 🌟</h1>
        <p>Click the buttons to see what our friendship really is... or is it? 😉</p>
        <div class="buttons">
            <button id="best-friends">Best Friends</button>
            <button id="just-friends">Just Friends</button>
            <button id="enemies">Enemies</button>
            <button id="idk">I Don’t Know</button>
        </div>
        <div id="message">What do you think we are? Click to find out! 🎉</div>
    </div>

    <script>
        const buttons = document.querySelectorAll('button');
        const message = document.getElementById('message');
        const clickCounts = {
            'best-friends': 0,
            'just-friends': 0,
            'enemies': 0,
            'idk': 0
        };

        const messages = {
            1: [
                "Try again, buddy! 😏",
                "Nope, keep clicking! 🤔",
                "Not quite yet! 😉",
                "Hmm, maybe not... 😜"
            ],
            2: [
                "Are you sure? Friendship is tricky! 😂",
                "Playful rejection: We're not there yet! 😅",
                "Confusion overload! What are we? 🤨",
                "Just friends? Or frenemies? 😈"
            ],
            3: [
                "Doubt creeps in... Is this real? 🤯",
                "Suspense! One more click? 😲",
                "Funny doubt: Besties or just vibes? 😂",
                "I don't know either! Keep guessing! 🤪"
            ]
        };

        buttons.forEach(button => {
            button.addEventListener('click', () => {
                const id = button.id;
                clickCounts[id]++;
                const cycle = (clickCounts[id] - 1) % 3 + 1; // Cycles 1, 2, 3, 1, 2, 3...
                const msgIndex = Math.floor(Math.random() * messages[cycle].length);
                message.textContent = messages[cycle][msgIndex];
            });
        });
    </script>
</body>
</html>

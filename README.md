# friendship.game.
a fun interactive friendship button game made using html css and javascript...
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Friendship Button Game</title>

<style>
    * {
        box-sizing: border-box;
    }

    body {
        margin: 0;
        padding: 0;
        height: 100vh;
        font-family: 'Comic Sans MS', cursive;
        background: linear-gradient(-45deg, #ff9a9e, #fad0c4, #a1c4fd, #c2e9fb);
        background-size: 400% 400%;
        animation: bgMove 10s ease infinite;
        display: flex;
        justify-content: center;
        align-items: center;
        overflow: hidden;
    }

    @keyframes bgMove {
        0% { background-position: 0% 50%; }
        50% { background-position: 100% 50%; }
        100% { background-position: 0% 50%; }
    }

    .game-box {
        background: linear-gradient(135deg, #ffffff, #f3f9ff);
        border-radius: 30px;
        padding: 35px;
        width: 340px;
        text-align: center;
        box-shadow: 0 25px 50px rgba(0,0,0,0.25);
        position: relative;
        animation: pop 1s ease;
    }

    @keyframes pop {
        from { transform: scale(0.8); opacity: 0; }
        to { transform: scale(1); opacity: 1; }
    }

    h1 {
        margin: 0;
        font-size: 28px;
        background: linear-gradient(90deg, #ff6a00, #ee0979, #00c6ff);
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
    }

    p {
        margin-top: 10px;
        font-size: 16px;
        color: #444;
    }

    .message {
        margin: 25px 0;
        font-size: 19px;
        min-height: 45px;
        font-weight: bold;
        color: #222;
        transition: 0.3s;
    }

    .buttons {
        display: flex;
        justify-content: space-around;
        margin-top: 20px;
    }

    button {
        border: none;
        padding: 14px 26px;
        font-size: 16px;
        border-radius: 40px;
        cursor: pointer;
        font-weight: bold;
        transition: 0.3s;
    }

    #yesBtn {
        background: linear-gradient(135deg, #00f2fe, #4facfe);
        color: #fff;
        box-shadow: 0 0 15px #4facfe;
    }

    #noBtn {
        background: linear-gradient(135deg, #ff0844, #ffb199);
        color: #fff;
        box-shadow: 0 0 15px #ff0844;
    }

    button:hover {
        transform: scale(1.15) rotate(-2deg);
    }

    /* doodles */
    .doodle {
        position: absolute;
        font-size: 45px;
        animation: float 4s ease-in-out infinite;
        opacity: 0.7;
    }

    @keyframes float {
        0%, 100% { transform: translateY(0); }
        50% { transform: translateY(-12px); }
    }

    .d1 { top: -20px; left: -20px; }
    .d2 { bottom: -20px; right: -20px; }
    .d3 { top: -25px; right: 30px; }
    .d4 { bottom: -25px; left: 30px; }
</style>
</head>

<body>

<div class="game-box">
    <div class="doodle d1">🌈</div>
    <div class="doodle d2">✨</div>
    <div class="doodle d3">🎨</div>
    <div class="doodle d4">🤝</div>

    <h1>Friendship Test 😎</h1>
    <p>No love, only bestie energy 💥</p>

    <div class="message" id="msg">
        Choose wisely 👀
    </div>

    <div class="buttons">
        <button id="yesBtn">YES</button>
        <button id="noBtn">NO</button>
    </div>
</div>

<script>
    let noClicks = 0;
    let yesClicks = 0;

    const noMessages = [
        "Try again 😏",
        "Better luck next time 😌",
        "I'm not convinced 🤨",
        "Nope ❌",
        "Try again 🙃",
        "Do it again 😈"
    ];

    const yesMessages = [
        "Ohhh really? 👀",
        "Oh no 😳",
        "Haha caught you 😎 Friendship confirmed!"
    ];

    const msgBox = document.getElementById("msg");

    document.getElementById("noBtn").addEventListener("click", () => {
        msgBox.innerText = noMessages[noClicks % noMessages.length];
        noClicks++;
    });

    document.getElementById("yesBtn").addEventListener("click", () => {
        if (yesClicks < yesMessages.length) {
            msgBox.innerText = yesMessages[yesClicks];
            yesClicks++;
        } else {
            msgBox.innerText = "Game over 😜 Reload to play again!";
        }
    });
</script>

</body>
</html>

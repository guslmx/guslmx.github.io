<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <meta name="format-detection" content="telephone=no, date=no, email=no, address=no">
    <title>Carte 21 - Machine</title>
    <style>
        body {
            font-family: "Arial Black", "Segoe UI", Roboto, sans-serif;
            background-color: #1a1a1a;
            margin: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
            height: 100vh;
            color: white;
            user-select: none;
        }

        .banner {
            width: 100%;
            background-color: #4CAF50;
            color: white;
            text-align: center;
            font-size: 28px;
            font-weight: 900;
            padding: 10px 0;
            box-shadow: 0 4px 10px rgba(0,0,0,0.6);
            border-bottom: 4px solid #fff;
            position: fixed;
            top: 0;
            left: 0;
            z-index: 10;
        }

        .cercle-21 {
            display: inline-block;
            border: 3px solid white;
            border-radius: 50%;
            width: 45px;
            height: 45px;
            line-height: 45px;
            text-align: center;
        }

        .container {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            flex-grow: 1;
            margin-top: 70px;
            width: 100%;
        }

        .digicode {
            background: linear-gradient(135deg, #e6e6e6 0%, #b3b3b3 50%, #808080 100%);
            padding: 25px;
            border-radius: 15px;
            border: 3px solid #555;
            box-shadow: inset 0 0 15px rgba(255,255,255,0.7), 0 15px 30px rgba(0,0,0,0.8);
            width: 280px;
        }

        .screen {
            background-color: #0a1f0a;
            color: #39ff14;
            font-family: 'Courier New', Courier, monospace;
            font-size: 40px;
            text-align: center;
            border-radius: 8px;
            margin-bottom: 20px;
            letter-spacing: 10px;
            border: 3px solid #000;
            box-shadow: inset 0 0 15px rgba(0,0,0,0.9);
            height: 60px;
            display: flex;
            align-items: center;
            justify-content: center;
            overflow: hidden;
        }

        .keypad {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 15px;
        }

        .key {
            background: linear-gradient(to bottom, #f9f9f9, #c4c4c4);
            border: 2px solid #777;
            border-radius: 10px;
            font-size: 28px;
            font-weight: bold;
            color: #222;
            padding: 15px 0;
            cursor: pointer;
            box-shadow: 0 6px 0 #666, 0 10px 15px rgba(0,0,0,0.3);
            transition: all 0.1s;
        }

        .key:active {
            transform: translateY(6px);
            box-shadow: 0 0 0 #666, 0 4px 5px rgba(0,0,0,0.3);
        }

        .key.clear { color: #d32f2f; }
        .key.enter { color: #388e3c; }

        .result-view {
            display: none;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            text-align: center;
            padding: 20px;
            width: 90%;
        }

        .result-view h2 {
            font-size: 32px;
            margin-bottom: 10px;
            white-space: nowrap;
        }

        .result-view p {
            font-size: 22px;
            font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
            font-weight: normal;
            margin-top: 0;
        }

        .carte-cercle {
            background: linear-gradient(135deg, #a0a0a0, #707070);
            color: white;
            font-size: 55px;
            font-weight: 900;
            width: 120px;
            height: 120px;
            line-height: 120px;
            border-radius: 50%;
            border: 4px solid #ddd;
            box-shadow: 0 10px 20px rgba(0,0,0,0.5);
            margin-top: 20px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.4);
        }

        .penalty-icon {
            margin-bottom: 10px;
            animation: pulse 1s infinite alternate;
        }

        @keyframes pulse {
            from { transform: scale(1); }
            to { transform: scale(1.1); }
        }

        .retry-btn {
            background-color: #333;
            color: white;
            border: 2px solid #666;
            padding: 12px 25px;
            font-size: 18px;
            font-weight: bold;
            border-radius: 8px;
            margin-top: 30px;
            cursor: pointer;
        }
        .retry-btn:active { background-color: #111; }
    </style>
</head>
<body>
    <div class="banner">
        <span class="cercle-21">21</span>
    </div>

    <div id="digicode-view" class="container">
        <div class="digicode">
            <div class="screen" id="screen">----</div>
            <div class="keypad">
                <button class="key" onclick="press('1')">1</button>
                <button class="key" onclick="press('2')">2</button>
                <button class="key" onclick="press('3')">3</button>
                <button class="key" onclick="press('4')">4</button>
                <button class="key" onclick="press('5')">5</button>
                <button class="key" onclick="press('6')">6</button>
                <button class="key" onclick="press('7')">7</button>
                <button class="key" onclick="press('8')">8</button>
                <button class="key" onclick="press('9')">9</button>
                <button class="key clear" onclick="clearCode()">C</button>
                <button class="key" onclick="press('0')">0</button>
                <button class="key enter" onclick="checkCode()">OK</button>
            </div>
        </div>
    </div>

    <div id="success-view" class="container result-view">
        <h2 style="color: #4CAF50;">Code bon.</h2>
        <p>Prenez la carte</p>
        <div class="carte-cercle">48</div>
    </div>

    <div id="error-view" class="container result-view">
        <div class="penalty-icon">
            <svg viewBox="0 0 100 100" width="100" height="100">
                <circle cx="50" cy="50" r="45" fill="#c0392b" stroke="#e74c3c" stroke-width="4"/>
                <line x1="30" y1="30" x2="70" y2="70" stroke="white" stroke-width="12" stroke-linecap="round"/>
                <line x1="70" y1="30" x2="30" y2="70" stroke="white" stroke-width="12" stroke-linecap="round"/>
            </svg>
        </div>
        <h2 style="color: #e74c3c;">Code faux.</h2>
        <p>Appuyez une fois sur le<br>bouton pénalité.</p>
        <button class="retry-btn" onclick="resetDigicode()">Retour au digicode</button>
    </div>

    <script>
        const secretCode = "7239";
        let currentCode = "";
        const screenEl = document.getElementById("screen");

        function updateScreen() {
            let display = currentCode.padEnd(4, "-");
            screenEl.innerText = display;
        }

        function press(num) {
            if (currentCode.length < 4) {
                currentCode += num;
                updateScreen();
            }
        }

        function clearCode() {
            currentCode = "";
            updateScreen();
        }

        function checkCode() {
            if (currentCode.length !== 4) return;
            document.getElementById('digicode-view').style.display = 'none';
            if (currentCode === secretCode) {
                document.getElementById('success-view').style.display = 'flex';
            } else {
                document.getElementById('error-view').style.display = 'flex';
            }
        }

        function resetDigicode() {
            currentCode = "";
            updateScreen();
            document.getElementById('error-view').style.display = 'none';
            document.getElementById('digicode-view').style.display = 'flex';
        }
    </script>
</body>
</html>

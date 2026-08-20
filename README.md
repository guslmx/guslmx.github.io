# guslmx.github.io


<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Accès Sécurisé</title>
    <style>
        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
            background-color: #f0f2f5;
            color: #333;
        }
        .container {
            background: white;
            padding: 2rem;
            border-radius: 12px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.1);
            text-align: center;
            max-width: 85%;
            width: 320px;
        }
        input[type="password"] {
            width: 100%;
            padding: 12px;
            margin: 15px 0;
            border: 1px solid #ccc;
            border-radius: 6px;
            font-size: 20px;
            box-sizing: border-box;
            text-align: center;
            letter-spacing: 4px;
        }
        button {
            background-color: #000;
            color: white;
            border: none;
            padding: 12px 20px;
            border-radius: 6px;
            font-size: 16px;
            cursor: pointer;
            width: 100%;
            font-weight: bold;
        }
        button:active { background-color: #333; }
        #error-msg {
            color: #d93025;
            font-size: 14px;
            display: none;
            margin-top: 10px;
        }
        #hidden-content {
            display: none; /* Caché par défaut */
        }
        .success-icon {
            font-size: 48px;
            margin-bottom: 10px;
        }
    </style>
</head>
<body>

    <!-- ÉCRAN DE VERROUILLAGE -->
    <div id="login-screen" class="container">
        <h2>Zone Protégée</h2>
        <p>Veuillez entrer le code PIN</p>
        <!-- L'utilisateur tape le code ici -->
        <input type="password" id="pin-input" placeholder="••••" maxlength="4">
        <button onclick="checkPIN()">Déverrouiller</button>
        <p id="error-msg">Code incorrect, réessayez.</p>
    </div>

    <!-- CONTENU CACHÉ (s'affiche uniquement si le code est bon) -->
    <div id="hidden-content" class="container">
        <div class="success-icon">🔓</div>
        <h2>Accès Autorisé</h2>
        <p>Félicitations, tu as débloqué le contenu !</p>
        <p>tu peux passer à la suite</p>
    </div>

    <script>
        function checkPIN() {
            // DÉFINIS TON CODE ICI (actuellement 1234)
            const codeSecret = "1234"; 
            const pinSaisi = document.getElementById("pin-input").value;

            if (pinSaisi === codeSecret) {
                // Si le code est bon : on cache le cadenas, on montre le secret
                document.getElementById("login-screen").style.display = "none";
                document.getElementById("hidden-content").style.display = "block";
            } else {
                // Si le code est faux : on affiche l'erreur et on vide le champ
                document.getElementById("error-msg").style.display = "block";
                document.getElementById("pin-input").value = ""; 
            }
        }
    </script>

</body>
</html>

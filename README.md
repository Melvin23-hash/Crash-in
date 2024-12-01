
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Crash Game</title>
    <style>
        .container { text-align: center; margin-top: 50px; }
        .multiplier { font-size: 50px; }
        .bet-button { margin-top: 20px; }
    </style>
</head>
<body>
    <div class="container">
        <div class="multiplier" id="multiplier">1.00</div>
        <button class="bet-button" id="betButton">Place Bet</button>
        <div id="gameStatus"></div>
    </div>

    <script>
        let currentMultiplier = 1.00;
        let gameRunning = false;
        let crashMultiplier = Math.random() * (2.5 - 1) + 1; // Random crash point between 1x and 2.5x
        let betPlaced = false;

        // Update multiplier
        function updateMultiplier() {
            if (gameRunning) {
                currentMultiplier += 0.01; // Increase the multiplier slowly
                document.getElementById('multiplier').innerText = currentMultiplier.toFixed(2);
                if (currentMultiplier >= crashMultiplier) {
                    endGame("Crash! You lost!");
                } else {
                    setTimeout(updateMultiplier, 100); // Update every 100 ms
                }
            }
        }

        // Start the game
        document.getElementById('betButton').addEventListener('click', function() {
            if (betPlaced) {
                endGame("You already placed a bet.");
                return;
            }
            betPlaced = true;
            gameRunning = true;
            currentMultiplier = 1.00;
            crashMultiplier = Math.random() * (2.5 - 1) + 1;
            document.getElementById('gameStatus').innerText = "Game Started! Wait for the crash...";
            updateMultiplier();
        });

        // End the game
        function endGame(message) {
            gameRunning = false;
            document.getElementById('gameStatus').innerText = message;
            betPlaced = false;
        }
    </script>
</body>
</html>

 

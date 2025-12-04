<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Word Guessing Game</title>

    <style>
        body {
            font-family: "Segoe UI", Arial, sans-serif;
            background: linear-gradient(135deg, #c9d6ff, #e2e2e2);
            display: flex;
            justify-content: center;
            align-items: flex-start;
            padding-top: 40px;
        }

        .game-container {
            background: #ffffff;
            padding: 30px;
            border-radius: 14px;
            width: 380px;
            text-align: center;
            box-shadow: 0 4px 18px rgba(0,0,0,0.15);
            animation: fadeIn 0.4s ease-out;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        h1 {
            margin-bottom: 10px;
            color: #333;
        }

        #hint {
            margin-bottom: 15px;
            font-size: 14px;
            color: #555;
            font-style: italic;
        }

        .word {
            font-size: 28px;
            letter-spacing: 8px;
            margin: 20px 0;
            font-weight: bold;
        }

        input {
            padding: 10px;
            width: 140px;
            margin-bottom: 10px;
            text-align: center;
            border: 1px solid #666;
            border-radius: 6px;
            font-size: 16px;
        }

        button {
            padding: 10px 22px;
            cursor: pointer;
            border: none;
            background: #4b7bec;
            color: #fff;
            border-radius: 6px;
            margin-left: 5px;
            font-size: 15px;
        }

        button:hover {
            background: #3867d6;
        }

        .info {
            margin-top: 12px;
            color: #333;
            font-size: 15px;
        }

        .letters {
            font-weight: bold;
            color: #555;
        }
    </style>
</head>
<body>

    <div class="game-container">
        <h1>Word Guessing Game</h1>

        <p id="hint"></p>
        <div id="wordDisplay" class="word"></div>

        <input type="text" id="letterInput" maxlength="1" placeholder="Type a letter…">
        <button onclick="guessLetter()">Guess</button>

        <p class="info">Wrong Attempts: <span id="wrongCount">0</span></p>
        <p class="info">Your Guesses: <span id="guessedLetters" class="letters"></span></p>
    </div>

    <script>
        const words = [
            { word: "apple", hint: "A fruit you’ve probably eaten this week" },
            { word: "planet", hint: "You're standing on one right now" },
            { word: "javascript", hint: "The language running this game" },
            { word: "river", hint: "A natural water flow" }
        ];

        let selected = words[Math.floor(Math.random() * words.length)];
        let word = selected.word.toLowerCase();
        let guessed = [];
        let wrong = 0;

        document.getElementById("hint").textContent = "Hint: " + selected.hint;

        function updateDisplay() {
            let display = "";
            for (let letter of word) {
                display += guessed.includes(letter) ? letter + " " : "_ ";
            }
            document.getElementById("wordDisplay").textContent = display;
        }

        updateDisplay();

        function guessLetter() {
            let input = document.getElementById("letterInput").value.toLowerCase();

            if (!input.match(/^[a-z]$/)) {
                alert("Enter a valid alphabet letter.");
                return;
            }

            if (guessed.includes(input)) {
                alert("You've already tried that letter. Pick a new one.");
            } else if (word.includes(input)) {
                guessed.push(input);
            } else {
                wrong++;
                document.getElementById("wrongCount").textContent = wrong;
            }

            document.getElementById("guessedLetters").textContent = guessed.join(", ");
            document.getElementById("letterInput").value = "";
            updateDisplay();

            if ([...word].every(l => guessed.includes(l))) {
                setTimeout(() => {
                    alert("Nice! You figured it out 🎉\nThe word was: " + word);
                }, 200);
            }
        }
    </script>

</body>
</html>

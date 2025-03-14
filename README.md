# mission-1-stoichiometry
Mission Objective: Determine the ideal fuel-to-air ratio for complete combustion in Proton’s engines to maximize energy output and minimize emissions.
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Interactive Chemistry Game - Fuel Optimization</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #0a0a0a;
            color: white;
        }
        .game-container {
            margin: 50px auto;
            width: 80%;
            background: rgba(255, 255, 255, 0.1);
            padding: 20px;
            border-radius: 10px;
        }
        .drag-container {
            display: flex;
            justify-content: center;
            gap: 20px;
        }
        .drop-zone {
            width: 150px;
            height: 150px;
            border: 2px dashed white;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.3s ease;
        }
        .draggable {
            width: 100px;
            height: 100px;
            background-color: lightblue;
            text-align: center;
            line-height: 100px;
            cursor: grab;
            border-radius: 10px;
        }
        .drop-zone.correct {
            border: 3px solid green;
            background-color: rgba(0, 255, 0, 0.2);
        }
        .drop-zone.incorrect {
            border: 3px solid red;
            background-color: rgba(255, 0, 0, 0.2);
        }
    </style>
</head>
<body>
    <h1>Interactive Chemistry Game - Fuel Optimization</h1>
    <h2>Mission: Balance the Combustion Equation</h2>
    <p>Drag and drop the correct number of O₂ molecules to balance the equation.</p>
    
    <div class="game-container">
        <h3>Balanced Equation: C₈H₁₈ + ? O₂ → CO₂ + H₂O</h3>
        <div class="drag-container">
            <div class="draggable" draggable="true" id="o2">O₂</div>
        </div>
        <div class="drop-zone" id="dropZone">Drop O₂ Here</div>
    </div>
    
    <p id="result"></p>

    <audio id="correctSound" src="https://www.fesliyanstudios.com/play-mp3/4383"></audio>
    <audio id="errorSound" src="https://www.fesliyanstudios.com/play-mp3/4386"></audio>

    <script>
        let correctDrops = 0;
        const correctSound = document.getElementById("correctSound");
        const errorSound = document.getElementById("errorSound");

        document.getElementById("o2").addEventListener("dragstart", function (event) {
            event.dataTransfer.setData("text", event.target.id);
        });

        document.getElementById("dropZone").addEventListener("dragover", function (event) {
            event.preventDefault();
        });

        document.getElementById("dropZone").addEventListener("drop", function (event) {
            event.preventDefault();
            let data = event.dataTransfer.getData("text");
            if (data === "o2") {
                correctDrops++;
                if (correctDrops === 12) {
                    document.getElementById("result").innerText = "🎉 Mission Accomplished! The equation is balanced!";
                    this.classList.add("correct");
                    correctSound.play();
                } else {
                    document.getElementById("result").innerText = `You've dropped ${correctDrops} O₂ molecules. Keep going!`;
                    this.classList.add("correct");
                    correctSound.play();
                }
            } else {
                this.classList.add("incorrect");
                errorSound.play();
            }
            setTimeout(() => this.classList.remove("correct", "incorrect"), 500);
        });
    </script>
</body>
</html>

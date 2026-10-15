# www.quiz.com
<!DOCTYPE html>
<html lang="nl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pokémon Quiz Mania</title>
    <style>
        /* Pokémon Thema Styling */
        * { box-sizing: border-box; margin: 0; padding: 0; }
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background-color: #1c1c1f; color: #ffffff; line-height: 1.6; }
        
        /* Navigatiebalk */
        header { background-color: #111; padding: 20px; border-bottom: 4px solid #ffcb05; }
        nav { display: flex; justify-content: space-between; align-items: center; max-width: 1000px; margin: 0 auto; }
        .logo { font-size: 26px; font-weight: bold; color: #ffcb05; text-decoration: none; text-shadow: 2px 2px #3b4cca; }
        .logo span { color: #ff1f1f; }
        .nav-links a { color: #fff; text-decoration: none; margin-left: 20px; font-weight: bold; transition: color 0.3s; }
        .nav-links a:hover { color: #ffcb05; }

        /* Welkomstsectie */
        .hero { max-width: 800px; margin: 50px auto; padding: 20px; text-align: center; }
        .hero h1 { font-size: 42px; margin-bottom: 15px; color: #fff; text-shadow: 2px 2px #111; }
        .hero h1 span { color: #ffcb05; }
        .hero p { font-size: 18px; color: #ccc; margin-bottom: 30px; }

        /* Quiz Hub Layout */
        .quiz-container { max-width: 1000px; margin: 0 auto; padding: 20px; display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 25px; }
        .quiz-card { background-color: #2a2a2e; padding: 25px; border-radius: 12px; border: 2px solid #3b4cca; text-align: center; transition: transform 0.3s; }
        .quiz-card:hover { transform: translateY(-5px); border-color: #ffcb05; }
        .quiz-card h2 { color: #ffcb05; margin-bottom: 12px; font-size: 22px; }
        .quiz-card p { color: #ddd; margin-bottom: 20px; font-size: 15px; }
        
        /* Knoppen */
        .play-btn { background-color: #ff1f1f; color: white; border: none; padding: 10px 25px; font-size: 16px; font-weight: bold; border-radius: 25px; cursor: pointer; transition: background 0.2s; width: 100%; }
        .play-btn:hover { background-color: #cc1818; }

        /* Interactieve Mini-Quiz Box */
        .interactive-box { max-width: 600px; margin: 40px auto; background-color: #222; border: 3px dashed #ffcb05; padding: 30px; border-radius: 15px; text-align: center; }
        .interactive-box h3 { color: #ffcb05; margin-bottom: 15px; }
        .options { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-top: 20px; }
        .option-btn { background-color: #333; color: white; border: 2px solid #555; padding: 12px; border-radius: 8px; cursor: pointer; font-weight: bold; }
        .option-btn:hover { background-color: #3b4cca; border-color: #ffcb05; }
        #feedback { margin-top: 15px; font-weight: bold; font-size: 18px; }

        footer { text-align: center; padding: 30px; color: #777; font-size: 14px; margin-top: 60px; background-color: #111; border-top: 2px solid #222; }
    </style>
</head>
<body>

    <header>
        <nav>
            <a href="#" class="logo">Poke<span>Quiz</span></a>
            <div class="nav-links">
                <a href="#">Home</a>
                <a href="#">Alle Quizzen</a>
                <a href="#">Topscores</a>
            </div>
        </nav>
    </header>

    <section class="hero">
        <h1>Welkom bij <span>Pokémon Quiz Mania</span>!</h1>
        <p>Ben jij een échte Pokémon Meester? Test je legendarische kennis met onze wekelijkse nieuwe Pokémon-quizzen. Geen gedoe, puur Pokémon!</p>
    </section>

    <!-- Interactieve Demo Quiz -->
    <div class="interactive-box">
        <h3>Dagelijkse Snel-Quiz: Wie is deze Pokémon?</h3>
        <p><em>"Het heeft een bliksemflits-vormige staart en laadt elektriciteit op in zijn rode wangen."</em></p>
        <div class="options">
            <button class="option-btn" onclick="checkAntwoord(false)">Charmander</button>
            <button class="option-btn" onclick="checkAntwoord(true)">Pikachu</button>
            <button class="option-btn" onclick="checkAntwoord(false)">Eevee</button>
            <button class="option-btn" onclick="checkAntwoord(false)">Squirtle</button>
        </div>
        <div id="feedback"></div>
    </div>

    <!-- Lijst met andere Pokémon Quizzen -->
    <h2 style="text-align: center; margin-top: 40px; color: #fff;">Kies een Categorie</h2>
    <main class="quiz-container">
        <div class="quiz-card">
            <h2>Gen 1 Kennis</h2>
            <p>Weet jij alles over de allereerste 151 Pokémon uit Kanto? Test het nu!</p>
            <button class="play-btn" onclick="startQuiz('Gen 1')">Start Quiz</button>
        </div>
        <div class="quiz-card">
            <h2>Raad de Evolutie</h2>
            <p>Welke steen heeft Eevee nodig? Welk level evolueert deze Pokémon? Pittige vragen!</p>
            <button class="play-btn" onclick="startQuiz('Evolutie')">Start Quiz</button>
        </div>
        <div class="quiz-card">
            <h2>Legendary & Mythical</h2>
            <p>Hoe goed ken jij Mewtwo, Arceus en de andere zeldzame legenden?</p>
            <button class="play-btn" onclick="startQuiz('Legendary')">Start Quiz</button>
        </div>
    </main>

    <footer>
        <p>&copy; 2026 Pokémon Quiz Mania - Gemaakt voor échte fans.</p>
    </footer>

    <script>
        // Logica voor de dagelijkse mini-quiz
        function checkAntwoord(isCorrect) {
            const feedbackDiv = document.getElementById('feedback');
            if (isCorrect) {
                feedbackDiv.innerHTML = "🎉 Correct! Het is Pikachu!";
                feedbackDiv.style.color = "#00ff88";
            } else {
                feedbackDiv.innerHTML = "❌ Helaas, probeer het nog eens!";
                feedbackDiv.style.color = "#ff1f1f";
            }
        }

        // Logica voor de grote quizzen (placeholder)
        function startQuiz(naam) {
            alert("De " + naam + " Quiz wordt geladen... Maak je klaar!");
        }
    </script>

</body>
</html>

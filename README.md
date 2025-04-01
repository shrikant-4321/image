<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Level Up Quiz Game</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #6e8efb, #a777e3);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 15px;
            color: #333;
        }
        .quiz-container {
            background-color: white;
            width: 100%;
            max-width: 500px;
            padding: 25px;
            border-radius: 15px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.2);
            position: relative;
            overflow: hidden;
        }
        .header {
            display: flex;
            justify-content: space-between;
            margin-bottom: 20px;
            align-items: center;
        }
        .level-display {
            background-color: #4CAF50;
            color: white;
            padding: 8px 15px;
            border-radius: 20px;
            font-weight: bold;
            font-size: 14px;
        }
        .score-display {
            background-color: #2196F3;
            color: white;
            padding: 8px 15px;
            border-radius: 20px;
            font-weight: bold;
            font-size: 14px;
        }
        .question {
            font-size: 20px;
            margin-bottom: 25px;
            font-weight: 600;
            line-height: 1.4;
        }
        .options {
            display: grid;
            grid-template-columns: 1fr;
            gap: 12px;
            margin-bottom: 25px;
        }
        .option {
            padding: 15px;
            background-color: #f5f5f5;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s;
            font-size: 16px;
            border: 2px solid transparent;
        }
        .option:hover {
            background-color: #e0e0e0;
            transform: translateY(-2px);
        }
        .selected {
            border-color: #4CAF50;
            background-color: #e8f5e9;
        }
        .correct {
            background-color: #4CAF50;
            color: white;
            border-color: #4CAF50;
        }
        .incorrect {
            background-color: #f44336;
            color: white;
            border-color: #f44336;
        }
        .feedback {
            margin-bottom: 20px;
            padding: 12px;
            border-radius: 8px;
            text-align: center;
            font-weight: bold;
            display: none;
        }
        .correct-feedback {
            background-color: #e8f5e9;
            color: #2e7d32;
            display: block;
        }
        .incorrect-feedback {
            background-color: #ffebee;
            color: #c62828;
            display: block;
        }
        .next-btn {
            width: 100%;
            padding: 15px;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 10px;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        .next-btn:hover {
            background-color: #3e8e41;
        }
        .next-btn:disabled {
            background-color: #cccccc;
            cursor: not-allowed;
        }
        .progress-container {
            width: 100%;
            background-color: #e0e0e0;
            border-radius: 10px;
            margin-bottom: 20px;
            height: 10px;
        }
        .progress-bar {
            height: 100%;
            border-radius: 10px;
            background: linear-gradient(90deg, #4CAF50, #8BC34A);
            width: 0%;
            transition: width 0.5s ease;
        }
        .game-complete {
            text-align: center;
            padding: 20px;
        }
        .game-complete h2 {
            color: #4CAF50;
            margin-bottom: 15px;
        }
        .game-complete p {
            margin-bottom: 10px;
            font-size: 18px;
        }
        .restart-btn {
            margin-top: 20px;
            padding: 12px 25px;
            background-color: #2196F3;
            color: white;
            border: none;
            border-radius: 30px;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s;
        }
        .restart-btn:hover {
            background-color: #0b7dda;
            transform: scale(1.05);
        }
        .creator {
            margin-top: 30px;
            text-align: center;
            font-style: italic;
            color: #777;
        }
        .ad-container {
            margin: 20px 0;
            padding: 15px;
            background-color: #f0f0f0;
            border-radius: 8px;
            text-align: center;
            border: 1px dashed #ccc;
        }
        .ad-label {
            font-size: 12px;
            color: #666;
            margin-bottom: 5px;
        }
        @media (max-width: 400px) {
            .question {
                font-size: 18px;
            }
            .option {
                padding: 12px;
                font-size: 15px;
            }
        }
    </style>
</head>
<body>
    <div class="quiz-container">
        <div class="header">
            <div class="level-display">Level: <span id="level">1</span>/30</div>
            <div class="score-display">Score: <span id="score">0</span></div>
        </div>
        
        <div class="progress-container">
            <div class="progress-bar" id="progress"></div>
        </div>
        
        <div id="quiz-content">
            <div class="question" id="question">Loading question...</div>
            <div class="options" id="options">
                <!-- Options will be added by JavaScript -->
            </div>
            <div class="feedback" id="feedback"></div>
            <button class="next-btn" id="next-btn" disabled>Next</button>
            
            <!-- Banner Ad Placeholder -->
            <div class="ad-container">
                <div class="ad-label">Advertisement</div>
                <div id="banner-ad">Banner Ad (ca-app-pub-3535001234721478/4391331254)</div>
            </div>
        </div>
        
        <div id="game-complete" class="game-complete" style="display: none;">
            <h2>Congratulations!</h2>
            <p>You've completed all 30 levels!</p>
            <p>Your final score: <span id="final-score">0</span>/30</p>
            <button class="restart-btn" id="restart-btn">Play Again</button>
            
            <!-- Native Ad Placeholder -->
            <div class="ad-container" style="margin-top: 30px;">
                <div class="ad-label">Advertisement</div>
                <div id="native-ad">Native Ad (ca-app-pub-3535001234721478/6385572226)</div>
            </div>
            
            <div class="creator">Game created by Shrikant Sahani</div>
        </div>
    </div>

    <!-- Interstitial Ad Modal -->
    <div id="interstitial-ad" style="display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background-color: rgba(0,0,0,0.8); z-index: 1000; color: white; padding: 20px; text-align: center;">
        <h2>Advertisement</h2>
        <p>Interstitial Ad (ca-app-pub-3535001234721478/3098598758)</p>
        <p>The game will continue after this ad</p>
        <button id="close-interstitial" style="padding: 10px 20px; background-color: #4CAF50; color: white; border: none; border-radius: 5px; margin-top: 20px; cursor: pointer;">Close Ad</button>
    </div>

    <!-- Rewarded Ad Modal -->
    <div id="rewarded-ad" style="display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background-color: rgba(0,0,0,0.8); z-index: 1000; color: white; padding: 20px; text-align: center;">
        <h2>Rewarded Video</h2>
        <p>Rewarded Ad (ca-app-pub-3535001234721478/3347479372)</p>
        <p>Watch a video to continue playing from current level</p>
        <button id="watch-rewarded" style="padding: 10px 20px; background-color: #4CAF50; color: white; border: none; border-radius: 5px; margin: 10px; cursor: pointer;">Watch Video</button>
        <button id="skip-rewarded" style="padding: 10px 20px; background-color: #f44336; color: white; border: none; border-radius: 5px; margin: 10px; cursor: pointer;">Skip</button>
    </div>

    <script>
        // Quiz questions (30 questions)
        const quizQuestions = [
            {
                question: "What is the capital of India?",
                options: ["Mumbai", "Delhi", "Kolkata", "Chennai"],
                answer: 1
            },
            {
                question: "Which planet is known as the Red Planet?",
                options: ["Venus", "Mars", "Jupiter", "Saturn"],
                answer: 1
            },
            {
                question: "What is the largest mammal?",
                options: ["Elephant", "Blue Whale", "Giraffe", "Hippopotamus"],
                answer: 1
            },
            {
                question: "Which language runs in a web browser?",
                options: ["Java", "C", "Python", "JavaScript"],
                answer: 3
            },
            {
                question: "What year was JavaScript launched?",
                options: ["1996", "1995", "1994", "1997"],
                answer: 1
            },
            {
                question: "Which country is home to the kangaroo?",
                options: ["South Africa", "Brazil", "Australia", "Canada"],
                answer: 2
            },
            {
                question: "What is the largest ocean on Earth?",
                options: ["Atlantic", "Indian", "Arctic", "Pacific"],
                answer: 3
            },
            {
                question: "Which element has the chemical symbol 'O'?",
                options: ["Gold", "Oxygen", "Osmium", "Oganesson"],
                answer: 1
            },
            {
                question: "Who painted the Mona Lisa?",
                options: ["Vincent van Gogh", "Pablo Picasso", "Leonardo da Vinci", "Michelangelo"],
                answer: 2
            },
            {
                question: "What is the currency of Japan?",
                options: ["Won", "Yen", "Ringgit", "Baht"],
                answer: 1
            },
            {
                question: "Which planet is closest to the Sun?",
                options: ["Venus", "Mars", "Mercury", "Earth"],
                answer: 2
            },
            {
                question: "What is the tallest mountain in the world?",
                options: ["K2", "Mount Everest", "Kangchenjunga", "Lhotse"],
                answer: 1
            },
            {
                question: "Which animal is known as the 'King of the Jungle'?",
                options: ["Tiger", "Elephant", "Lion", "Gorilla"],
                answer: 2
            },
            {
                question: "What is the largest continent by area?",
                options: ["Africa", "North America", "Asia", "Europe"],
                answer: 2
            },
            {
                question: "Which country is the largest by area?",
                options: ["China", "USA", "Canada", "Russia"],
                answer: 3
            },
            {
                question: "What is the hardest natural substance on Earth?",
                options: ["Gold", "Iron", "Diamond", "Platinum"],
                answer: 2
            },
            {
                question: "Which planet has the most moons?",
                options: ["Jupiter", "Saturn", "Neptune", "Uranus"],
                answer: 1
            },
            {
                question: "What is the capital of Canada?",
                options: ["Toronto", "Vancouver", "Ottawa", "Montreal"],
                answer: 2
            },
            {
                question: "Which country invented tea?",
                options: ["India", "China", "Japan", "England"],
                answer: 1
            },
            {
                question: "What is the largest desert in the world?",
                options: ["Sahara", "Arabian", "Gobi", "Antarctic"],
                answer: 3
            },
            {
                question: "Which country is known as the Land of the Rising Sun?",
                options: ["China", "Thailand", "Japan", "South Korea"],
                answer: 2
            },
            {
                question: "What is the fastest land animal?",
                options: ["Lion", "Cheetah", "Pronghorn Antelope", "Quarter Horse"],
                answer: 1
            },
            {
                question: "Which country has the most pyramids?",
                options: ["Egypt", "Mexico", "Sudan", "Peru"],
                answer: 2
            },
            {
                question: "What is the national flower of India?",
                options: ["Rose", "Lotus", "Jasmine", "Sunflower"],
                answer: 1
            },
            {
                question: "Which planet has rings around it?",
                options: ["Jupiter", "Saturn", "Uranus", "All of these"],
                answer: 3
            },
            {
                question: "What is the largest bone in the human body?",
                options: ["Femur", "Tibia", "Humerus", "Pelvis"],
                answer: 0
            },
            {
                question: "Which country is the largest producer of coffee?",
                options: ["Colombia", "Vietnam", "Brazil", "Ethiopia"],
                answer: 2
            },
            {
                question: "What is the smallest country in the world?",
                options: ["Monaco", "Nauru", "Vatican City", "San Marino"],
                answer: 2
            },
            {
                question: "Which gas is most abundant in Earth's atmosphere?",
                options: ["Oxygen", "Carbon Dioxide", "Nitrogen", "Argon"],
                answer: 2
            },
            {
                question: "How many continents are there on Earth?",
                options: ["5", "6", "7", "8"],
                answer: 2
            }
        ];

        // DOM elements
        const questionElement = document.getElementById('question');
        const optionsElement = document.getElementById('options');
        const nextButton = document.getElementById('next-btn');
        const feedbackElement = document.getElementById('feedback');
        const levelElement = document.getElementById('level');
        const scoreElement = document.getElementById('score');
        const progressBar = document.getElementById('progress');
        const quizContent = document.getElementById('quiz-content');
        const gameComplete = document.getElementById('game-complete');
        const finalScoreElement = document.getElementById('final-score');
        const restartButton = document.getElementById('restart-btn');
        const interstitialAd = document.getElementById('interstitial-ad');
        const closeInterstitial = document.getElementById('close-interstitial');
        const rewardedAd = document.getElementById('rewarded-ad');
        const watchRewarded = document.getElementById('watch-rewarded');
        const skipRewarded = document.getElementById('skip-rewarded');

        // Quiz variables
        let currentQuestionIndex = 0;
        let score = 0;
        let selectedOption = null;
        let answeredCorrectly = false;
        let gameState = {}; // To save state for rewarded ad

        // Initialize quiz
        function startQuiz() {
            currentQuestionIndex = 0;
            score = 0;
            updateScore();
            showQuestion();
            quizContent.style.display = 'block';
            gameComplete.style.display = 'none';
            
            // Show app open ad (mock implementation)
            console.log("Showing App Open Ad: ca-app-pub-3535001234721478/4220108730");
        }

        // Display current question
        function showQuestion() {
            const question = quizQuestions[currentQuestionIndex];
            questionElement.textContent = question.question;
            optionsElement.innerHTML = '';
            
            question.options.forEach((option, index) => {
                const optionElement = document.createElement('div');
                optionElement.textContent = option;
                optionElement.classList.add('option');
                optionElement.addEventListener('click', () => selectOption(index));
                optionsElement.appendChild(optionElement);
            });
            
            levelElement.textContent = currentQuestionIndex + 1;
            nextButton.disabled = true;
            feedbackElement.style.display = 'none';
            feedbackElement.className = 'feedback';
            answeredCorrectly = false;
            selectedOption = null;
            
            // Update progress bar
            const progress = ((currentQuestionIndex) / quizQuestions.length) * 100;
            progressBar.style.width = `${progress}%`;
            
            // Show banner ad every 5 questions (mock implementation)
            if (currentQuestionIndex > 0 && currentQuestionIndex % 5 === 0) {
                console.log("Showing Banner Ad: ca-app-pub-3535001234721478/4391331254");
            }
        }

        // Select an option
        function selectOption(index) {
            if (answeredCorrectly) return;
            
            const options = document.querySelectorAll('.option');
            
            // Remove selected class from all options
            options.forEach(option => {
                option.classList.remove('selected');
            });
            
            // Add selected class to clicked option
            options[index].classList.add('selected');
            selectedOption = index;
            nextButton.disabled = false;
        }

        // Check answer and show feedback
        function checkAnswer() {
            const question = quizQuestions[currentQuestionIndex];
            const options = document.querySelectorAll('.option');
            
            // Disable all options
            options.forEach(option => {
                option.style.cursor = 'default';
                option.onclick = null;
            });
            
            // Check if answer is correct
            if (selectedOption === question.answer) {
                options[question.answer].classList.add('correct');
                feedbackElement.textContent = "Correct! Well done!";
                feedbackElement.className = 'feedback correct-feedback';
                score++;
                answeredCorrectly = true;
                updateScore();
                
                // Show interstitial ad every 3 correct answers (mock implementation)
                if (score > 0 && score % 3 === 0) {
                    showInterstitialAd();
                }
            } else {
                options[selectedOption].classList.add('incorrect');
                options[question.answer].classList.add('correct');
                feedbackElement.textContent = `Incorrect! The correct answer is: ${question.options[question.answer]}`;
                feedbackElement.className = 'feedback incorrect-feedback';
                
                // Offer rewarded ad to continue
                showRewardedAd();
            }
            
            feedbackElement.style.display = 'block';
            
            // Change button text if it's the last question
            if (currentQuestionIndex === quizQuestions.length - 1) {
                nextButton.textContent = "Finish";
            } else {
                nextButton.textContent = "Next";
            }
        }

        // Move to next question or show final score
        function nextQuestion() {
            if (!answeredCorrectly && selectedOption !== null) {
                checkAnswer();
                return;
            }
            
            // Move to next question if answer was correct
            if (answeredCorrectly) {
                currentQuestionIndex++;
                
                // If all questions completed, show final screen
                if (currentQuestionIndex >= quizQuestions.length) {
                    showFinalScreen();
                    return;
                }
                
                showQuestion();
            }
        }

        // Show final screen
        function showFinalScreen() {
            quizContent.style.display = 'none';
            gameComplete.style.display = 'block';
            finalScoreElement.textContent = score;
            
            // Show native ad on completion (mock implementation)
            console.log("Showing Native Ad: ca-app-pub-3535001234721478/6385572226");
        }

        // Show interstitial ad
        function showInterstitialAd() {
            console.log("Showing Interstitial Ad: ca-app-pub-3535001234721478/3098598758");
            interstitialAd.style.display = 'block';
        }

        // Show rewarded ad
        function showRewardedAd() {
            // Save current game state
            gameState = {
                currentQuestionIndex: currentQuestionIndex,
                score: score
            };
            
            console.log("Showing Rewarded Interstitial Ad: ca-app-pub-3535001234721478/6764712726");
            rewardedAd.style.display = 'block';
        }

        // Update score display
        function updateScore() {
            scoreElement.textContent = score;
        }

        // Event listeners
        nextButton.addEventListener('click', nextQuestion);
        restartButton.addEventListener('click', startQuiz);
        
        // Ad event listeners
        closeInterstitial.addEventListener('click', () => {
            interstitialAd.style.display = 'none';
        });
        
        watchRewarded.addEventListener('click', () => {
            console.log("User watched rewarded ad - continuing game");
            rewardedAd.style.display = 'none';
            
            // Restore game state
            currentQuestionIndex = gameState.currentQuestionIndex;
            score = gameState.score;
            updateScore();
            showQuestion();
        });
        
        skipRewarded.addEventListener('click', () => {
            console.log("User skipped rewarded ad - restarting game");
            rewardedAd.style.display = 'none';
            startQuiz();
        });

        // Start the quiz when page loads
        startQuiz();
    </script>
</body>
</html>

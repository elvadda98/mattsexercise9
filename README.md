<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vocabulary Game: Italian-Inspired English Vocabulary</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #009688 0%, #4CAF50 100%);
            min-height: 100vh;
            padding: 20px;
            color: #2c3e50;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .container {
            max-width: 1000px;
            width: 100%;
            background: white;
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.2);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #00796b, #009688);
            color: white;
            padding: 30px;
            text-align: center;
            position: relative;
        }

        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            position: relative;
            z-index: 1;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
        }

        .header p {
            font-size: 1.2em;
            opacity: 0.9;
            position: relative;
            z-index: 1;
        }

        .nav-buttons {
            display: flex;
            justify-content: center;
            gap: 10px;
            padding: 20px;
            background: #f8f9fa;
            flex-wrap: wrap;
        }

        .nav-btn {
            padding: 12px 24px;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
        }

        .nav-btn.active {
            background: linear-gradient(135deg, #00796b, #009688);
            color: white;
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(0, 121, 107, 0.4);
        }

        .nav-btn:not(.active) {
            background: white;
            color: #666;
        }

        .nav-btn:hover:not(.active) {
            background: #e9ecef;
            transform: translateY(-1px);
        }

        .game-section {
            display: none;
            padding: 30px;
            min-height: 400px;
        }

        .game-section.active {
            display: block;
            animation: fadeIn 0.5s ease-in;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .word-bank {
            background: linear-gradient(135deg, #e0f2f1, #e8f5e9);
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 25px;
            border: 2px solid #009688;
            box-shadow: 0 4px 15px rgba(0, 150, 136, 0.2);
        }

        .word-bank h3 {
            color: #00796b;
            margin-bottom: 15px;
            text-align: center;
            font-size: 1.4em;
        }

        .word-options {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            justify-content: center;
        }

        .word-option {
            background: linear-gradient(135deg, #009688, #00796b);
            color: white;
            padding: 10px 18px;
            border-radius: 20px;
            font-weight: bold;
            font-size: 16px;
            box-shadow: 0 3px 10px rgba(0, 150, 136, 0.3);
            transition: all 0.3s ease;
            cursor: default;
        }

        .word-option:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0, 150, 136, 0.4);
        }

        .question {
            background: #f8f9fa;
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 20px;
            border-left: 5px solid #009688;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
        }

        .question h3 {
            color: #00796b;
            margin-bottom: 15px;
            font-size: 1.3em;
        }

        .fill-blank {
            background: #fff;
            border: 2px solid #ddd;
            border-radius: 8px;
            padding: 8px 12px;
            font-size: 16px;
            margin: 0 5px;
            min-width: 120px;
            transition: border-color 0.3s ease;
        }

        .fill-blank.correct {
            border-color: #FF9800;
            background: #FFF3E0;
        }

        .fill-blank.incorrect {
            border-color: #F44336;
            background: #FFEBEE;
        }

        .fill-blank-pron {
            background: #fff;
            border: 2px solid #ddd;
            border-radius: 8px;
            padding: 8px 12px;
            font-size: 16px;
            margin: 0 5px;
            min-width: 120px;
            display: inline-block;
        }

        .fill-blank-pron.correct {
            border-color: #FF9800;
            background: #FFF3E0;
        }

        .fill-blank-pron.incorrect {
            border-color: #F44336;
            background: #FFEBEE;
        }

        .options {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-top: 15px;
        }

        .matching-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-top: 20px;
        }

        .match-column h4 {
            text-align: center;
            margin-bottom: 15px;
            color: #00796b;
            font-size: 1.2em;
        }

        .match-item {
            padding: 15px;
            margin: 8px 0;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .match-item:hover {
            border-color: #009688;
            transform: translateY(-1px);
            box-shadow: 0 4px 15px rgba(0, 150, 136, 0.2);
        }

        .match-item.selected {
            background: #e0f2f1;
            border-color: #009688;
        }

        .match-item.matched {
            background: #FF9800;
            color: white;
            border-color: #FF9800;
            cursor: default;
        }

        .check-btn {
            background: linear-gradient(135deg, #009688, #00796b);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            margin: 20px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0, 150, 136, 0.3);
        }

        .check-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(0, 150, 136, 0.4);
        }

        .reset-btn {
            background: linear-gradient(135deg, #F44336, #D32F2F);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            margin: 10px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(244, 67, 54, 0.3);
        }

        .reset-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(244, 67, 54, 0.4);
        }

        .feedback {
            margin-top: 15px;
            padding: 15px;
            border-radius: 10px;
            font-weight: bold;
            text-align: center;
            animation: slideIn 0.3s ease;
        }

        @keyframes slideIn {
            from { transform: translateX(-20px); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        .feedback.correct {
            background: #E8F5E9;
            color: #2E7D32;
            border: 1px solid #C8E6C9;
        }

        .feedback.incorrect {
            background: #FFEBEE;
            color: #C62828;
            border: 1px solid #FFCDD2;
        }

        .score {
            position: fixed;
            top: 20px;
            right: 20px;
            background: linear-gradient(135deg, #009688, #00796b);
            color: white;
            padding: 15px 20px;
            border-radius: 25px;
            font-weight: bold;
            box-shadow: 0 4px 15px rgba(0, 150, 136, 0.3);
            z-index: 1000;
        }

        .icon {
            font-size: 24px;
            margin-right: 10px;
            vertical-align: middle;
        }

        /* Vocabulary List Styles */
        .vocabulary-list {
            padding: 20px;
        }

        .vocabulary-item {
            margin-bottom: 25px;
            padding: 20px;
            border-radius: 10px;
            background: #f8f9fa;
            box-shadow: 0 4px 10px rgba(0,0,0,0.05);
        }

        .vocabulary-item h3 {
            color: #00796b;
            margin-bottom: 10px;
            font-size: 1.4em;
            border-bottom: 2px solid #009688;
            padding-bottom: 8px;
        }

        .vocabulary-item p {
            margin-bottom: 8px;
            line-height: 1.6;
        }

        .example {
            font-style: italic;
            color: #555;
            padding-left: 15px;
            border-left: 3px solid #009688;
            margin-top: 10px;
        }

        .italian-word {
            background-color: #FFF3E0;
            padding: 5px 10px;
            border-radius: 5px;
            font-weight: bold;
            color: #EF6C00;
            display: inline-block;
            margin-top: 5px;
        }

        .audio-btn {
            margin-top: 10px;
            padding: 8px 16px;
            border-radius: 20px;
            border: none;
            cursor: pointer;
            background: linear-gradient(135deg, #FF9800, #F57C00);
            color: white;
            font-weight: bold;
            font-size: 14px;
            box-shadow: 0 3px 10px rgba(255, 152, 0, 0.4);
            display: inline-flex;
            align-items: center;
            gap: 6px;
        }

        .audio-btn:hover {
            transform: translateY(-1px);
            box-shadow: 0 5px 15px rgba(255, 152, 0, 0.5);
        }

        .pron-btn-mic {
            padding: 6px 12px;
            border-radius: 18px;
            border: none;
            cursor: pointer;
            background: linear-gradient(135deg, #009688, #00796b);
            color: white;
            font-weight: bold;
            font-size: 14px;
            display: inline-flex;
            align-items: center;
            gap: 6px;
            margin-left: 5px;
        }

        .pron-btn-mic:hover {
            transform: translateY(-1px);
            box-shadow: 0 4px 12px rgba(0, 150, 136, 0.4);
        }

        @media (max-width: 768px) {
            .matching-container {
                grid-template-columns: 1fr;
                gap: 20px;
            }
            
            .nav-buttons {
                flex-direction: column;
                align-items: center;
            }
            
            .nav-btn {
                width: 220px;
            }
            
            .score {
                position: static;
                margin: 20px auto;
                display: block;
                width: fit-content;
            }
        }
    </style>
</head>
<body>
    <div class="score">Score: <span id="score">0</span>/18</div>
    
    <div class="container">
        <div class="header">
            <h1><i class="fas fa-book icon"></i> Vocabulary Game: Italian-Inspired English Vocabulary</h1>
            <p>Learn English equivalents of common Italian words and phrases!</p>
        </div>

        <div class="nav-buttons">
            <button class="nav-btn active" onclick="showSection('vocabulary', event)">Vocabulary List</button>
            <button class="nav-btn" onclick="showSection('fill-gaps', event)">Fill in the Gaps</button>
            <button class="nav-btn" onclick="showSection('matching', event)">Match Definitions</button>
            <button class="nav-btn" onclick="showSection('fill-gaps-pron', event)">Fill in the Gaps (Pronunciation)</button>
        </div>

        <!-- Vocabulary List Section -->
        <div id="vocabulary" class="game-section active">
            <h2 style="text-align: center; margin-bottom: 20px; color: #00796b;">Vocabulary Words and Meanings</h2>
            
            <div class="vocabulary-list">
                <div class="vocabulary-item">
                    <h3>how come (come mai)</h3>
                    <p><strong>Definition:</strong> Informal way to ask "why?" or "for what reason?"</p>
                    <p class="italian-word">Italian: come mai</p>
                    <button class="audio-btn" data-word="come mai" onclick="speakItalian(this.dataset.word)">
                        <i class="fas fa-volume-up"></i> Ascolta in italiano
                    </button>
                    <p><strong>Usage:</strong> Casual question expressing surprise or curiosity about something.</p>
                    <p class="example"><strong>Example:</strong> "How come you didn't come to the party last night?"</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>a little (un po')</h3>
                    <p><strong>Definition:</strong> A small amount; somewhat; slightly.</p>
                    <p class="italian-word">Italian: un po'</p>
                    <button class="audio-btn" data-word="un po'" onclick="speakItalian(this.dataset.word)">
                        <i class="fas fa-volume-up"></i> Ascolta in italiano
                    </button>
                    <p><strong>Usage:</strong> Used to indicate a small quantity or degree.</p>
                    <p class="example"><strong>Example:</strong> "Can I have a little sugar in my coffee, please?"</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>wake up (svegliare)</h3>
                    <p><strong>Definition:</strong> To stop sleeping; to become conscious after sleep.</p>
                    <p class="italian-word">Italian: svegliare</p>
                    <button class="audio-btn" data-word="svegliare" onclick="speakItalian(this.dataset.word)">
                        <i class="fas fa-volume-up"></i> Ascolta in italiano
                    </button>
                    <p><strong>Usage:</strong> Refers to the action of ending sleep, either for oneself or someone else.</p>
                    <p class="example"><strong>Example:</strong> "I usually wake up at 7 AM on weekdays."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>New Year's Day (capodanno)</h3>
                    <p><strong>Definition:</strong> January 1st, the first day of the year.</p>
                    <p class="italian-word">Italian: capodanno</p>
                    <button class="audio-btn" data-word="capodanno" onclick="speakItalian(this.dataset.word)">
                        <i class="fas fa-volume-up"></i> Ascolta in italiano
                    </button>
                    <p><strong>Usage:</strong> The holiday celebrating the beginning of the new year.</p>
                    <p class="example"><strong>Example:</strong> "We always have a big family dinner on New Year's Day."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>puppy (cucciolo)</h3>
                    <p><strong>Definition:</strong> A young dog, especially one less than a year old.</p>
                    <p class="italian-word">Italian: cucciolo</p>
                    <button class="audio-btn" data-word="cucciolo" onclick="speakItalian(this.dataset.word)">
                        <i class="fas fa-volume-up"></i> Ascolta in italiano
                    </button>
                    <p><strong>Usage:</strong> Can also refer to young animals of other species, but most commonly dogs.</p>
                    <p class="example"><strong>Example:</strong> "Their new puppy is so cute and playful!"</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>holiday/vacation (vacanza)</h3>
                    <p><strong>Definition:</strong> A period of time devoted to pleasure, rest, or relaxation away from work.</p>
                    <p class="italian-word">Italian: vacanza</p>
                    <button class="audio-btn" data-word="vacanza" onclick="speakItalian(this.dataset.word)">
                        <i class="fas fa-volume-up"></i> Ascolta in italiano
                    </button>
                    <p><strong>Usage:</strong> British English uses "holiday," American English uses "vacation."</p>
                    <p class="example"><strong>Example:</strong> "We're going on holiday to Spain next month."</p>
                </div>
            </div>
        </div>

        <!-- Fill in the Gaps Section (Writing) -->
        <div id="fill-gaps" class="game-section">
            <div class="word-bank">
                <h3><i class="fas fa-list-ul icon"></i> Word Bank - Choose from these words:</h3>
                <div class="word-options">
                    <span class="word-option">how come</span>
                    <span class="word-option">a little</span>
                    <span class="word-option">wake up</span>
                    <span class="word-option">New Year's Day</span>
                    <span class="word-option">puppy</span>
                    <span class="word-option">holiday</span>
                </div>
            </div>

            <div id="fill-gaps-container">
                <!-- Sentences will be dynamically inserted here -->
            </div>

            <button class="check-btn" onclick="checkFillBlanks()">Check Answers</button>
            <button class="reset-btn" onclick="resetFillBlanks()">Reset Answers</button>
        </div>

        <!-- Matching Section -->
        <div id="matching" class="game-section">
            <h2 style="text-align: center; margin-bottom: 20px; color: #00796b;">Match the words with their definitions</h2>
            <div class="matching-container">
                <div class="match-column">
                    <h4>Vocabulary Words</h4>
                    <div class="match-item" data-word="how come" onclick="selectMatch(this)">how come</div>
                    <div class="match-item" data-word="a little" onclick="selectMatch(this)">a little</div>
                    <div class="match-item" data-word="wake up" onclick="selectMatch(this)">wake up</div>
                    <div class="match-item" data-word="New Year's Day" onclick="selectMatch(this)">New Year's Day</div>
                    <div class="match-item" data-word="puppy" onclick="selectMatch(this)">puppy</div>
                    <div class="match-item" data-word="holiday" onclick="selectMatch(this)">holiday</div>
                </div>
                <div class="match-column">
                    <h4>Definitions</h4>
                    <div id="meanings-container">
                        <!-- Meanings will be dynamically inserted here -->
                    </div>
                </div>
            </div>
            <div class="feedback" id="matching-feedback" style="display: none;"></div>
            <button class="check-btn" onclick="checkMatching()">Check Matching</button>
            <button class="reset-btn" onclick="resetMatching()">Reset Matching</button>
        </div>

        <!-- NEW: Fill in the Gaps (Pronunciation) Section -->
        <div id="fill-gaps-pron" class="game-section">
            <div class="word-bank">
                <h3><i class="fas fa-microphone icon"></i> Pronunciation Gaps – Use these words:</h3>
                <div class="word-options">
                    <span class="word-option">how come</span>
                    <span class="word-option">a little</span>
                    <span class="word-option">wake up</span>
                    <span class="word-option">New Year's Day</span>
                    <span class="word-option">puppy</span>
                    <span class="word-option">holiday</span>
                </div>
                <p style="margin-top: 10px; text-align:center;">
                    🎤 Say the correct word to fill each gap. You don't type, you speak!
                </p>
            </div>

            <div id="pron-gaps-container">
                <!-- Pronunciation sentences will be inserted here -->
            </div>

            <button class="reset-btn" onclick="resetPronunciation()">Reset Pronunciation Exercise</button>
        </div>
    </div>

    <script>
        let score = 0;
        let selectedWord = null;
        let selectedMeaning = null;
        let matchedPairs = [];
        
        // Track correct answers for each section
        let fillBlanksCorrect = 0;
        let matchingCorrect = 0;
        let pronFillCorrect = 0;
        let pronCorrectFlags = [];

        // Text-to-speech for Italian
        function speakItalian(text) {
            const utterance = new SpeechSynthesisUtterance(text);
            utterance.lang = "it-IT";
            speechSynthesis.speak(utterance);
        }

        // Speech recognition for pronunciation gaps
        let recognition;
        if ("webkitSpeechRecognition" in window) {
            recognition = new webkitSpeechRecognition();
        } else if ("SpeechRecognition" in window) {
            recognition = new SpeechRecognition();
        }
        if (recognition) {
            recognition.lang = "en-US";
            recognition.interimResults = false;
            recognition.maxAlternatives = 1;
        }

        // Definitions for the matching game
        const definitions = [
            { meaning: "how come", text: "Informal way to ask 'why?' or 'for what reason?'" },
            { meaning: "a little", text: "A small amount; somewhat; slightly" },
            { meaning: "wake up", text: "To stop sleeping; to become conscious after sleep" },
            { meaning: "New Year's Day", text: "January 1st, the first day of the year" },
            { meaning: "puppy", text: "A young dog, especially one less than a year old" },
            { meaning: "holiday", text: "A period of time for pleasure, rest, or relaxation" }
        ];

        // Sentences for the fill-in-the-blanks (writing) game
        const sentences = [
            { text: "<input type='text' class='fill-blank' data-answer='How come' placeholder='answer'> you didn't come to the party last night?", answer: "How come" },
            { text: "Can I have <input type='text' class='fill-blank' data-answer='a little' placeholder='answer'> sugar in my coffee, please?", answer: "a little" },
            { text: "I usually <input type='text' class='fill-blank' data-answer='wake up' placeholder='answer'> at 7 AM on weekdays.", answer: "wake up" },
            { text: "We always have a big family dinner on <input type='text' class='fill-blank' data-answer='New Year's Day' placeholder='answer'>.", answer: "New Year's Day" },
            { text: "Their new <input type='text' class='fill-blank' data-answer='puppy' placeholder='answer'> is so cute and playful!", answer: "puppy" },
            { text: "We're going on <input type='text' class='fill-blank' data-answer='holiday' placeholder='answer'> to Spain next month.", answer: "holiday" },
            { text: "<input type='text' class='fill-blank' data-answer='How come' placeholder='answer'> she left the meeting early without saying goodbye?", answer: "How come" },
            { text: "I speak <input type='text' class='fill-blank' data-answer='a little' placeholder='answer'> French, but I'm not fluent.", answer: "a little" },
            { text: "Please <input type='text' class='fill-blank' data-answer='wake up' placeholder='answer'> early tomorrow for our flight.", answer: "wake up" },
            { text: "Many people make resolutions on <input type='text' class='fill-blank' data-answer='New Year's Day' placeholder='answer'>.", answer: "New Year's Day" },
            { text: "The <input type='text' class='fill-blank' data-answer='puppy' placeholder='answer'> chewed my favorite shoes!", answer: "puppy" },
            { text: "I need a <input type='text' class='fill-blank' data-answer='holiday' placeholder='answer'> after working so hard this year.", answer: "holiday" }
        ];

        // Sentences for the pronunciation fill-in-the-gaps game (different contexts)
        const pronSentences = [
            {
                before: "___ you're so tired today? You went to bed early!",
                answer: "How come"
            },
            {
                before: "I'm feeling ___ hungry, so I might eat a snack later.",
                answer: "a little"
            },
            {
                before: "On Saturdays I don't ___ until ten o'clock in the morning.",
                answer: "wake up"
            },
            {
                before: "On ___ we usually watch the parade and fireworks together.",
                answer: "New Year's Day"
            },
            {
                before: "The children were very happy when they got a new ___.",
                answer: "puppy"
            },
            {
                before: "Next year we want to take a ___ in the mountains.",
                answer: "holiday"
            }
        ];

        // Function to normalize user answers / transcripts
        function normalizeUserAnswer(answer) {
            const userAnswer = answer.toLowerCase().trim();

            if (userAnswer === "new year's day" || userAnswer === "new years day" || userAnswer === "new year day") {
                return "new year's day";
            }
            if (userAnswer === "a little" || userAnswer === "alittle") {
                return "a little";
            }
            if (userAnswer === "how come" || userAnswer === "howcome") {
                return "how come";
            }
            if (userAnswer === "wake up" || userAnswer === "wakeup") {
                return "wake up";
            }
            if (userAnswer === "holiday" || userAnswer === "vacation") {
                return "holiday";
            }
            return userAnswer;
        }

        // Function to shuffle array (Fisher-Yates algorithm)
        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
            return array;
        }

        // Initialize the fill-in-the-blanks game with shuffled sentences
        function initFillBlanks() {
            const container = document.getElementById('fill-gaps-container');
            container.innerHTML = '';
            
            // Shuffle the sentences and take 6 (one for each word)
            const shuffledSentences = shuffleArray([...sentences]).slice(0, 6);
            
            // Create and append the sentence elements
            shuffledSentences.forEach((sentence, index) => {
                const div = document.createElement('div');
                div.className = 'question';
                div.innerHTML = `
                    <h3>Fill in the blank ${index + 1}:</h3>
                    <p>${sentence.text}</p>
                    <div class="feedback" id="feedback-${index + 1}" style="display: none;"></div>
                `;
                container.appendChild(div);
            });
        }

        // Initialize the matching game with shuffled definitions
        function initMatchingGame() {
            const meaningsContainer = document.getElementById('meanings-container');
            meaningsContainer.innerHTML = '';
            
            // Shuffle the definitions
            const shuffledDefinitions = shuffleArray([...definitions]);
            
            // Create and append the definition elements
            shuffledDefinitions.forEach(def => {
                const div = document.createElement('div');
                div.className = 'match-item';
                div.setAttribute('data-meaning', def.meaning);
                div.onclick = function() { selectMatch(this); };
                div.textContent = def.text;
                meaningsContainer.appendChild(div);
            });
        }

        // Initialize pronunciation fill-in-the-gaps
        function initPronunciationBlanks() {
            const container = document.getElementById('pron-gaps-container');
            container.innerHTML = '';
            pronCorrectFlags = pronSentences.map(() => false);
            pronFillCorrect = 0;
            updateScore();

            pronSentences.forEach((sentence, index) => {
                const div = document.createElement('div');
                div.className = 'question';
                div.innerHTML = `
                    <h3>Pronunciation blank ${index + 1}:</h3>
                    <p>
                        ${sentence.before.replace("___", `<span id="pron-blank-${index}" class="fill-blank-pron">______</span>`)}
                        <button class="pron-btn-mic" onclick="recordPronunciation(${index})">
                            <i class="fas fa-microphone"></i> Speak
                        </button>
                    </p>
                    <div class="feedback" id="pron-feedback-${index}" style="display: none;"></div>
                `;
                container.appendChild(div);
            });
        }

        function showSection(sectionId, evt) {
            // Hide all sections
            document.querySelectorAll('.game-section').forEach(section => {
                section.classList.remove('active');
            });
            
            // Remove active class from all buttons
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            
            // Show selected section
            document.getElementById(sectionId).classList.add('active');
            
            // Add active class to clicked button
            if (evt && evt.target) {
                evt.target.classList.add('active');
            }
            
            // If showing fill-in-the-blanks section, reinitialize with shuffled sentences
            if (sectionId === 'fill-gaps') {
                initFillBlanks();
                // Reset written fill-in-the-gaps score
                fillBlanksCorrect = 0;
            }
            
            // If showing matching section, reinitialize with shuffled definitions
            if (sectionId === 'matching') {
                initMatchingGame();
                document.querySelectorAll('.match-item').forEach(item => {
                    item.classList.remove('selected', 'matched');
                });
                selectedWord = null;
                selectedMeaning = null;
                matchedPairs = [];
                matchingCorrect = 0;
                document.getElementById('matching-feedback').style.display = 'none';
            }

            // If showing pronunciation fill-in-the-gaps, (re)initialize
            if (sectionId === 'fill-gaps-pron') {
                initPronunciationBlanks();
            }
            
            // Update score display
            updateScore();
        }

        function checkFillBlanks() {
            const blanks = document.querySelectorAll('.fill-blank');
            let correctCount = 0;
            
            blanks.forEach((blank, index) => {
                const userAnswerRaw = blank.value;
                const userAnswerNormalized = normalizeUserAnswer(userAnswerRaw);
                const correctAnswer = blank.dataset.answer.toLowerCase();
                const correctNormalized = correctAnswer.toLowerCase();

                if (userAnswerNormalized === correctNormalized) {
                    blank.classList.remove('incorrect');
                    blank.classList.add('correct');
                    correctCount++;
                } else {
                    blank.classList.remove('correct');
                    blank.classList.add('incorrect');
                }
                
                // Show feedback for each question
                const feedback = document.getElementById(`feedback-${index+1}`);
                if (userAnswerNormalized === correctNormalized) {
                    feedback.textContent = '✅ Correct!';

                    feedback.className = 'feedback correct';
                } else {
                    feedback.textContent = `❌ Incorrect. The correct answer is: "${blank.dataset.answer}"`;
                    feedback.className = 'feedback incorrect';
                }
                feedback.style.display = 'block';
            });
            
            fillBlanksCorrect = correctCount;
            updateScore();
        }

        function resetFillBlanks() {
            const blanks = document.querySelectorAll('.fill-blank');
            blanks.forEach(blank => {
                blank.value = '';
                blank.classList.remove('correct', 'incorrect');
            });
            
            const feedbacks = document.querySelectorAll('#fill-gaps .feedback');
            feedbacks.forEach(feedback => {
                feedback.style.display = 'none';
            });
            
            fillBlanksCorrect = 0;
            updateScore();
        }

        function selectMatch(element) {
            if (element.classList.contains('matched')) return;
            
            if (element.dataset.word) {
                // Word selected
                if (selectedWord) selectedWord.classList.remove('selected');
                selectedWord = element;
                element.classList.add('selected');
            } else {
                // Meaning selected
                if (selectedMeaning) selectedMeaning.classList.remove('selected');
                selectedMeaning = element;
                element.classList.add('selected');
            }
            
            // Check if we have both word and meaning selected
            if (selectedWord && selectedMeaning) {
                checkMatch();
            }
        }

        function checkMatch() {
            const feedback = document.getElementById('matching-feedback');
            
            if (selectedWord.dataset.word === selectedMeaning.dataset.meaning) {
                // Correct match
                selectedWord.classList.remove('selected');
                selectedWord.classList.add('matched');
                selectedMeaning.classList.remove('selected');
                selectedMeaning.classList.add('matched');
                
                matchedPairs.push(selectedWord.dataset.word);
                
                feedback.textContent = '✅ Correct match!';
                feedback.className = 'feedback correct';
                
                // Check if all matches are complete
                if (matchedPairs.length === definitions.length) {
                    feedback.textContent = '🎉 Congratulations! You matched all terms correctly!';
                }
            } else {
                // Incorrect match
                feedback.textContent = '❌ Incorrect match. Try again.';
                feedback.className = 'feedback incorrect';
            }
            
            feedback.style.display = 'block';
            selectedWord = null;
            selectedMeaning = null;
            
            matchingCorrect = matchedPairs.length;
            updateScore();
        }

        function checkMatching() {
            const allMatches = document.querySelectorAll('.match-item[data-word]');
            let allCorrect = true;
            
            allMatches.forEach(item => {
                if (!item.classList.contains('matched')) {
                    allCorrect = false;
                }
            });
            
            const feedback = document.getElementById('matching-feedback');
            if (allCorrect) {
                feedback.textContent = '🎉 Excellent! All matches are correct!';
                feedback.className = 'feedback correct';
            } else {
                const unmatchedCount = definitions.length - matchedPairs.length;
                feedback.textContent = `You have ${unmatchedCount} unmatched pair${unmatchedCount !== 1 ? 's' : ''}. Keep trying!`;
                feedback.className = 'feedback incorrect';
            }
            feedback.style.display = 'block';
        }

        function resetMatching() {
            document.querySelectorAll('.match-item').forEach(item => {
                item.classList.remove('selected', 'matched');
            });
            
            initMatchingGame();
            
            selectedWord = null;
            selectedMeaning = null;
            matchedPairs = [];
            
            document.getElementById('matching-feedback').style.display = 'none';
            
            matchingCorrect = 0;
            updateScore();
        }

        // Pronunciation-based fill-in-the-gaps
        function recordPronunciation(index) {
            const expected = pronSentences[index].answer.toLowerCase();
            const blankEl = document.getElementById(`pron-blank-${index}`);
            const feedback = document.getElementById(`pron-feedback-${index}`);

            if (!recognition) {
                alert("Speech recognition is not supported in this browser.");
                return;
            }

            feedback.textContent = "Listening...";
            feedback.className = "";
            feedback.style.display = "block";

            recognition.start();

            recognition.onresult = function(event) {
                const transcriptRaw = event.results[0][0].transcript;
                const transcriptNorm = normalizeUserAnswer(transcriptRaw);
                const expectedNorm = expected.toLowerCase();

                if (transcriptNorm === expectedNorm) {
                    blankEl.textContent = pronSentences[index].answer;
                    blankEl.classList.remove('incorrect');
                    blankEl.classList.add('correct');

                    feedback.textContent = `✅ Correct! You said "${transcriptRaw}".`;
                    feedback.className = "feedback correct";

                    if (!pronCorrectFlags[index]) {
                        pronCorrectFlags[index] = true;
                        pronFillCorrect++;
                        updateScore();
                    }
                } else {
                    blankEl.classList.remove('correct');
                    blankEl.classList.add('incorrect');
                    feedback.textContent = `❌ Incorrect. You said "${transcriptRaw}". Try again.`;
                    feedback.className = "feedback incorrect";
                    feedback.style.display = "block";
                }
            };

            recognition.onerror = function() {
                feedback.textContent = "Error during recognition. Please try again.";
                feedback.className = "feedback incorrect";
                feedback.style.display = "block";
            };
        }

        function resetPronunciation() {
            initPronunciationBlanks();
        }

        function updateScore() {
            // Total score from all sections:
            // 6 fill-blanks (writing) + 6 matching + 6 pronunciation = 18 max
            score = fillBlanksCorrect + matchingCorrect + pronFillCorrect;
            document.getElementById('score').textContent = score;
        }
        
        // Initialize the page
        window.onload = function() {
            initFillBlanks();
            initMatchingGame();
            initPronunciationBlanks();
        }
    </script>
</body>
</html>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Where Should You Relocate?</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #f4f7f6;
            color: #333;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            text-align: center;
            padding: 20px;
        }
        #quiz-container {
            background: white;
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 10px 20px rgba(0,0,0,0.1);
            max-width: 500px;
            width: 100%;
        }
        h1 { font-size: 22px; margin-bottom: 20px; color: #2c3e50; }
        .btn {
            background-color: #3498db;
            color: white;
            border: none;
            padding: 15px;
            margin: 10px 0;
            width: 100%;
            border-radius: 8px;
            font-size: 16px;
            cursor: pointer;
            transition: 0.3s;
        }
        .btn:hover { background-color: #2980b9; }
        .result-box {
            font-size: 20px;
            font-weight: bold;
            color: #27ae60;
            margin-top: 20px;
        }
        .desc { font-size: 16px; font-weight: normal; color: #555; margin-top: 10px; }
    </style>
</head>
<body>

<div id="quiz-container">
    <h1 id="question">Welcome to the Global Mobility Test!</h1>
    <div id="answers">
        <button class="btn" onclick="startQuiz()">Start the Quiz</button>
    </div>
</div>

<script>
    const questions = [
        {
            question: "Q1: Pick your ideal work environment.",
            answers: {
                A: "A busy skyscraper office, 3 monitors, and lots of coffee.",
                B: "A cozy office that feels like home, with familiar people.",
                C: "A futuristic smart office with robots and high-tech gadgets.",
                D: "A pet-friendly IT hub with green plants and a cat on your desk."
            }
        },
        {
            question: "Q2: How do you spend your lunch break?",
            answers: {
                A: "Eating a quick sandwich at my desk while answering emails.",
                B: "Enjoying a warm, traditional meal with colleagues.",
                C: "Getting my food delivered by a drone or a smart app.",
                D: "Chilling at an IT cafe, drinking iced coffee, and petting a dog."
            }
        },
        {
            question: "Q3: What is your main career goal right now?",
            answers: {
                A: "Climbing the career ladder fast, even if I have to overwork.",
                B: "Working in a comfortable, native culture where everything is clear.",
                C: "Developing top-secret technologies and working with AI.",
                D: "Coding cool IT projects while living in a relaxed place."
            }
        }
    ];

    const results = {
        A: { country: "THE USA 🇺🇸 (The Hustler)", desc: "Fast pace, big goals, and a lot of overtime!" },
        B: { country: "UKRAINE 🇺🇦 (The Homebody)", desc: "Comfort, familiar culture, and warm relationships." },
        C: { country: "CHINA 🇨🇳 (The Tech Genius)", desc: "Futuristic innovations, AI, and smart gadgets." },
        D: { country: "VIETNAM 🇻🇳 (The IT & Pet Lover)", desc: "Coding, warm weather, and furry friends everywhere!" }
    };

    let currentQuestion = 0;
    let scores = { A: 0, B: 0, C: 0, D: 0 };

    function startQuiz() {
        currentQuestion = 0;
        scores = { A: 0, B: 0, C: 0, D: 0 };
        showQuestion();
    }

    function showQuestion() {
        if (currentQuestion >= questions.length) {
            showResult();
            return;
        }
        
        let q = questions[currentQuestion];
        document.getElementById("question").innerText = q.question;
        
        let answersHtml = "";
        for (let key in q.answers) {
            answersHtml += `<button class="btn" onclick="selectAnswer('${key}')">${q.answers[key]}</button>`;
        }
        document.getElementById("answers").innerHTML = answersHtml;
    }

    function selectAnswer(choice) {
        scores[choice]++;
        currentQuestion++;
        showQuestion();
    }

    function showResult() {
        let maxScore = 0;
        let finalChoice = "A";

        for (let key in scores) {
            if (scores[key] > maxScore) {
                maxScore = scores[key];
                finalChoice = key;
            }
        }

        let res = results[finalChoice];
        document.getElementById("question").innerText = "Your Perfect Destination is:";
        document.getElementById("answers").innerHTML = `
            <div class="result-box">${res.country}</div>
            <div class="desc">${res.desc}</div>
            <button class="btn" style="margin-top: 30px; background-color: #95a5a6;" onclick="startQuiz()">Take Test Again</button>
        `;
    }
</script>

</body>
</html>

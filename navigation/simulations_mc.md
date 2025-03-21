---
layout: default
title: Simulations MCQs
search_exclude: true
permalink: /mc/
---

# Simulations & Games MCQs

<style>
.answer {
    display: none;
    color: green;
    font-weight: bold;
}
.choice {
    display: block;
    padding: 10px;
    margin: 5px 0;
    border-radius: 5px;
    cursor: pointer;
    border: 2px solid transparent;
}
.correct {
    background-color: #d4edda; /* Light green */
    border-color: #28a745; /* Green */
    color: black;
}
.incorrect {
    background-color: #f8d7da; /* Light red */
    border-color: #dc3545; /* Red */
    color: black;
}
button {
    margin-top: 10px;
    padding: 8px 12px;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}
button:hover {
    background-color: #0056b3;
}
</style>

<div id="quiz">
    <div class="question">
        <p><b>1. Which of the following is an advantage of using a simulation instead of real-world experimentation?</b></p>
        <div class="choice" onclick="checkAnswer(this, false)">A) Simulations always provide perfectly accurate results.</div>
        <div class="choice" onclick="checkAnswer(this, true)">B) Simulations are faster and safer than real-world testing.</div>
        <div class="choice" onclick="checkAnswer(this, false)">C) Simulations do not require any computing power.</div>
        <div class="choice" onclick="checkAnswer(this, false)">D) Simulations replace the need for real-world experiments entirely.</div>
    </div>

    <div class="question">
        <p><b>2. A game developer is creating a simulation of planetary motion. What is a major limitation?</b></p>
        <div class="choice" onclick="checkAnswer(this, false)">A) It cannot be used to model any physical behavior.</div>
        <div class="choice" onclick="checkAnswer(this, true)">B) It may not account for all real-world variables such as minor gravitational interactions.</div>
        <div class="choice" onclick="checkAnswer(this, false)">C) It requires no computation time.</div>
        <div class="choice" onclick="checkAnswer(this, false)">D) It does not need to use physics-based algorithms.</div>
    </div>

    <div class="question">
        <p><b>3. What is an essential component of a disease spread simulation?</b></p>
        <div class="choice" onclick="checkAnswer(this, false)">A) The exact number of infected individuals at the end.</div>
        <div class="choice" onclick="checkAnswer(this, true)">B) A random number generator to create unpredictable interactions.</div>
        <div class="choice" onclick="checkAnswer(this, false)">C) The names of infected individuals.</div>
        <div class="choice" onclick="checkAnswer(this, false)">D) A completely accurate representation of human biology.</div>
    </div>

    <h2>Random Algorithms MCQs</h2>

    <div class="question">
        <p><b>4. A fair six-sided die is rolled twice. What is the probability that both rolls result in the same number?</b></p>
        <div class="choice" onclick="checkAnswer(this, true)">A) 1/6</div>
        <div class="choice" onclick="checkAnswer(this, false)">B) 1/12</div>
        <div class="choice" onclick="checkAnswer(this, false)">C) 1/36</div>
        <div class="choice" onclick="checkAnswer(this, false)">D) 1/3</div>
    </div>

    <div class="question">
        <p><b>5. A random number generator outputs a number between 1 and 100. What is the likelihood of generating a number greater than 75?</b></p>
        <div class="choice" onclick="checkAnswer(this, true)">A) 25%</div>
        <div class="choice" onclick="checkAnswer(this, false)">B) 50%</div>
        <div class="choice" onclick="checkAnswer(this, false)">C) 75%</div>
        <div class="choice" onclick="checkAnswer(this, false)">D) 10%</div>
    </div>

    <div class="question">
        <p><b>6. In a guessing game (1 to 50), what is the best strategy to minimize guesses?</b></p>
        <div class="choice" onclick="checkAnswer(this, false)">A) Guess randomly each time.</div>
        <div class="choice" onclick="checkAnswer(this, false)">B) Start at 1 and increment by 1.</div>
        <div class="choice" onclick="checkAnswer(this, true)">C) Use binary search: guess the middle and eliminate half.</div>
        <div class="choice" onclick="checkAnswer(this, false)">D) Always guess 25.</div>
    </div>

    <button onclick="showScore()">Submit Quiz</button>
    <h2 id="score" style="display: none;">Your Score: 0/6</h2>
</div>

<script>
let score = 0;
let answeredQuestions = new Set();

function checkAnswer(element, isCorrect) {
    if (answeredQuestions.has(element.parentNode)) {
        return; // Prevent changing answers
    }
    answeredQuestions.add(element.parentNode);
    
    if (isCorrect) {
        element.classList.add("correct");
        score++;
    } else {
        element.classList.add("incorrect");
    }
}

function showScore() {
    document.getElementById("score").innerHTML = "Your Score: " + score + "/6";
    document.getElementById("score").style.display = "block";
}
</script>

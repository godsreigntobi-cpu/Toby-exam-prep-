# Toby's-exam-prep-
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>UI Post-UTME Practice CBT</title>

<style>
body{
    font-family: Arial, sans-serif;
    background: #f2f2f2;
    margin: 0;
    padding-bottom: 40px;
}

.header{
    background: #003366;
    color: white;
    padding: 15px 30px;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.container{
    width: 90%;
    max-width: 800px;
    margin: 30px auto;
    background: white;
    padding: 25px;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0,0,0,.2);
}

.subject-badge {
    background: #e0e6ed;
    color: #003366;
    padding: 5px 12px;
    border-radius: 15px;
    font-weight: bold;
    display: inline-block;
    margin-bottom: 10px;
}

button{
    padding: 10px 20px;
    background: #003366;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-size: 16px;
    margin-right: 10px;
}

button:hover {
    background: #002244;
}

button.submit-btn {
    background: #28a745;
}

button.submit-btn:hover {
    background: #218838;
}

.option{
    margin: 12px 0;
    padding: 8px;
    border-radius: 5px;
    background: #f9f9f9;
    border: 1px solid #ddd;
    cursor: pointer;
}

.option:hover {
    background: #edf2f7;
}

.option input {
    margin-right: 10px;
}

.nav-buttons {
    margin-top: 25px;
}

#results {
    display: none;
}

.score-card {
    background: #e8f4f8;
    padding: 15px;
    border-radius: 8px;
    margin-top: 15px;
}
</style>

</head>

<body>

<div class="header">
    <h2>UI Post-UTME CBT Practice</h2>
    <h2 id="timer">90:00</h2>
</div>

<div class="container" id="quiz-container">
    <div class="subject-badge" id="subject"></div>
    <h3 id="question"></h3>

    <div id="options"></div>

    <div class="nav-buttons">
        <button onclick="previousQuestion()">Previous</button>
        <button onclick="nextQuestion()">Next</button>
        <button class="submit-btn" onclick="submitExam()">Submit</button>
    </div>
</div>

<div class="container" id="results">
    <h2>Test Completed!</h2>
    <p>Here is your performance summary:</p>
    <div class="score-card" id="score-details"></div>
    <br>
    <button onclick="location.reload()">Retake Exam</button>
</div>

<script>

let currentQuestion = 0;
let userAnswers = {};

const questions = [

//==================== MATHEMATICS ====================
{
    subject: "MATHEMATICS",
    question: "Simplify: (2^3 × 2^4) ÷ 2^5",
    options: ["2", "4", "8", "16"],
    answer: 1
},
{
    subject: "MATHEMATICS",
    question: "Solve for x in log2(x^2 - 1) = 3.",
    options: ["±2", "±3", "±4", "±9"],
    answer: 1
},
{
    subject: "MATHEMATICS",
    question: "Find the derivative dy/dx of y = 3x^3 - 5x^2 + 7x - 4 at x = 2.",
    options: ["19", "21", "23", "27"],
    answer: 2
},
{
    subject: "MATHEMATICS",
    question: "Evaluate ∫ (3x^2 + 2x + 1) dx.",
    options: ["x^3 + x^2 + x + C", "3x^3 + 2x^2 + x + C", "6x + 2 + C", "x^3 + 2x^2 + C"],
    answer: 0
},
{
    subject: "MATHEMATICS",
    question: "The 3rd term of an AP is 10 and the 7th term is 22. Find the 1st term.",
    options: ["2", "4", "6", "8"],
    answer: 1
},
{
    subject: "MATHEMATICS",
    question: "Calculate the standard deviation of the set of numbers: 2, 4, 6, 8, 10.",
    options: ["2.83", "4.00", "5.66", "8.00"],
    answer: 0
},
{
    subject: "MATHEMATICS",
    question: "In how many ways can a committee of 3 people be selected from a group of 7?",
    options: ["21", "35", "210", "5040"],
    answer: 1
},
{
    subject: "MATHEMATICS",
    question: "If sin θ = 3/5 where θ is an acute angle, find tan θ.",
    options: ["3/4", "4/5", "4/3", "5/3"],
    answer: 0
},
{
    subject: "MATHEMATICS",
    question: "Find the gradient of the straight line joining points A(2, 3) and B(6, 11).",
    options: ["1/2", "2", "3", "4"],
    answer: 1
},
{
    subject: "MATHEMATICS",
    question: "Solve the simultaneous equations: 2x + y = 7 and x - y = 2.",
    options: ["x = 3, y = 1", "x = 1, y = 3", "x = 4, y = -1", "x = 2, y = 3"],
    answer: 0
},

//==================== ENGLISH LANGUAGE ====================
{
    subject: "ENGLISH LANGUAGE",
    question: "Choose the correct option: Neither the manager nor the employees _____ satisfied with the decision.",
    options: ["was", "is", "were", "has been"],
    answer: 2
},
{
    subject: "ENGLISH LANGUAGE",
    question: "Select the correctly spelt word.",
    options: ["Accomodation", "Accommodation", "Acomodation", "Acommodation"],
    answer: 1
},
{
    subject: "ENGLISH LANGUAGE",
    question: "Choose the option OPPOSITE in meaning to the underlined word: His FRUGAL habits enabled him to invest.",
    options: ["Economical", "Extravagant", "Prudent", "Parsimonious"],
    answer: 1
},
{
    subject: "ENGLISH LANGUAGE",
    question: "Choose the option NEAREST in meaning to the underlined word: The witness gave a TACITURN response.",
    options: ["Loquacious", "Reserved", "Verbose", "Bold"],
    answer: 1
},
{
    subject: "ENGLISH LANGUAGE",
    question: "Complete the sentence: If I _____ you, I would accept the job offer immediately.",
    options: ["am", "was", "were", "have been"],
    answer: 2
},
{
    subject: "ENGLISH LANGUAGE",
    question: "Select the correct question tag: She hardly ever comes late, _____?",
    options: ["does she?", "doesn't she?", "is she?", "isn't she?"],
    answer: 0
},
{
    subject: "ENGLISH LANGUAGE",
    question: "Choose the word with the same vowel sound as 'beat':",
    options: ["bit", "key", "bet", "light"],
    answer: 1
},
{
    subject: "ENGLISH LANGUAGE",
    question: "Fill in the blank: The suspect was charged _____ armed robbery.",
    options: ["for", "with", "of", "about"],
    answer: 1
},
{
    subject: "ENGLISH LANGUAGE",
    question: "Identify the figure of speech: 'The stars danced playfully in the moonlit sky.'",
    options: ["Metaphor", "Simile", "Personification", "Hyperbole"],
    answer: 2
},
{
    subject: "ENGLISH LANGUAGE",
    question: "Choose the correct idiom meaning: To 'kick the bucket' means to...",
    options: ["Start a fight", "Die", "Clean a room", "Surrender"],
    answer: 1
},

//==================== ECONOMICS ====================
{
    subject: "ECONOMICS",
    question: "When price elasticity of demand is greater than 1, demand is said to be:",
    options: ["Perfectly inelastic", "Inelastic", "Unitary elastic", "Elastic"],
    answer: 3
},
{
    subject: "ECONOMICS",
    question: "If Qd = 100 - 4P, calculate the quantity demanded when Price = ₦10.",
    options: ["40", "60", "80", "100"],
    answer: 1
},
{
    subject: "ECONOMICS",
    question: "The difference between Gross National Product (GNP) and Gross Domestic Product (GDP) is:",
    options: ["Depreciation", "Net Factor Income from Abroad", "Indirect Taxes", "Subsidies"],
    answer: 1
},
{
    subject: "ECONOMICS",
    question: "A market situation where there is only a single buyer is called a:",
    options: ["Monopoly", "Monopsony", "Oligopoly", "Duopoly"],
    answer: 1
},
{
    subject: "ECONOMICS",
    question: "Inflation caused by an increase in total expenditures not matched by equal growth in output is:",
    options: ["Cost-push inflation", "Demand-pull inflation", "Hyperinflation", "Structural inflation"],
    answer: 1
},
{
    subject: "ECONOMICS",
    question: "Which of the following is a direct tax?",
    options: ["Excise duty", "Value Added Tax (VAT)", "Personal Income Tax", "Customs duty"],
    answer: 2
},
{
    subject: "ECONOMICS",
    question: "According to the Law of Diminishing Marginal Utility, as consumption of a good increases:",
    options: ["Total utility decreases", "Marginal utility decreases", "Marginal utility increases", "Total utility stays constant"],
    answer: 1
},
{
    subject: "ECONOMICS",
    question: "Malthusian population theory states that population grows geometrically while food supply grows:",
    options: ["Exponentially", "Arithmetically", "Geometrically", "Logarithmically"],
    answer: 1
},
{
    subject: "ECONOMICS",
    question: "The central bank controls credit expansion using all the following EXCEPT:",
    options: ["Open Market Operations", "Reserve Requirements", "Bank Rate", "Income Tax Rate"],
    answer: 3
},
{
    subject: "ECONOMICS",
    question: "Opportunity cost is best defined as the:",
    options: ["Monetary cost of a good", "Next best alternative foregone", "Total expenditure incurred", "Variable cost of production"],
    answer: 1
},

//==================== FINANCIAL ACCOUNTING ====================
{
    subject: "FINANCIAL ACCOUNTING",
    question: "The fundamental accounting equation is:",
    options: ["Assets = Liabilities + Capital", "Capital = Assets + Liabilities", "Assets = Capital - Liabilities", "Liabilities = Assets + Capital"],
    answer: 0
},
{
    subject: "FINANCIAL ACCOUNTING",
    question: "Given: Opening Capital ₦50,000, Additional Capital ₦15,000, Profit ₦20,000, Drawings ₦10,000. Calculate Closing Capital.",
    options: ["₦65,000", "₦75,000", "₦85,000", "₦95,000"],
    answer: 1
},
{
    subject: "FINANCIAL ACCOUNTING",
    question: "Which error causes an imbalance in the Trial Balance?",
    options: ["Error of Omission", "Error of Principle", "Single Entry Error", "Error of Commission"],
    answer: 2
},
{
    subject: "FINANCIAL ACCOUNTING",
    question: "A bank reconciliation statement is prepared by the:",
    options: ["Central Bank", "Auditor", "Account Holder/Business", "Commercial Bank"],
    answer: 2
},
{
    subject: "FINANCIAL ACCOUNTING",
    question: "Which of the following is classified as a Current Asset?",
    options: ["Premises", "Machinery", "Stock/Inventory", "Debentures"],
    answer: 2
},
{
    subject: "FINANCIAL ACCOUNTING",
    question: "The document issued by a seller to a buyer when goods are returned is called a:",
    options: ["Debit Note", "Credit Note", "Invoice", "Receipt"],
    answer: 1
},
{
    subject: "FINANCIAL ACCOUNTING",
    question: "Depreciation calculated using a fixed percentage on the reducing balance each year is the:",
    options: ["Straight Line Method", "Reducing Balance Method", "Sum-of-Years-Digits Method", "Revaluation Method"],
    answer: 1
},
{
    subject: "FINANCIAL ACCOUNTING",
    question: "The excess of current assets over current liabilities is called:",
    options: ["Working Capital", "Capital Employed", "Authorized Capital", "Reserve Capital"],
    answer: 0
},
{
    subject: "FINANCIAL ACCOUNTING",
    question: "In a partnership, interest on capital is credited to the partners':",
    options: ["Profit and Loss Account", "Current Account", "Appropriation Account", "Trading Account"],
    answer: 1
},
{
    subject: "FINANCIAL ACCOUNTING",
    question: "Goodwill is classified as a(n):",
    options: ["Current Asset", "Tangible Fixed Asset", "Intangible Asset", "Fictitious Asset"],
    answer: 2
}

];

function loadQuestion(){
    const q = questions[currentQuestion];
    document.getElementById("subject").innerHTML = q.subject;
    document.getElementById("question").innerHTML = (currentQuestion + 1) + ". " + q.question;

    let html = "";
    q.options.forEach((option, index) => {
        const checked = userAnswers[currentQuestion] === index ? "checked" : "";
        html += `
        <div class="option" onclick="selectOption(${index})">
            <input type="radio" name="option" id="opt_${index}" value="${index}" ${checked}>
            <label for="opt_${index}">${option}</label>
        </div>
        `;
    });

    document.getElementById("options").innerHTML = html;
}

function selectOption(index) {
    userAnswers[currentQuestion] = index;
    const radio = document.getElementById(`opt_${index}`);
    if(radio) radio.checked = true;
}

function nextQuestion(){
    if(currentQuestion < questions.length - 1){
        currentQuestion++;
        loadQuestion();
    }
}

function previousQuestion(){
    if(currentQuestion > 0){
        currentQuestion--;
        loadQuestion();
    }
}

function submitExam() {
    if (confirm("Are you sure you want to submit your exam?")) {
        calculateResults();
    }
}

function calculateResults() {
    let score = 0;
    let subjectScores = {};

    questions.forEach((q, index) => {
        if (!subjectScores[q.subject]) {
            subjectScores[q.subject] = { correct: 0, total: 0 };
        }
        subjectScores[q.subject].total++;

        if (userAnswers[index] === q.answer) {
            score++;
            subjectScores[q.subject].correct++;
        }
    });

    document.getElementById("quiz-container").style.display = "none";
    document.getElementById("results").style.display = "block";

    let detailsHtml = `<h3>Total Score: ${score} / ${questions.length} (${((score/questions.length)*100).toFixed(1)}%)</h3><hr>`;
    
    for (let subj in subjectScores) {
        detailsHtml += `<p><strong>${subj}:</strong> ${subjectScores[subj].correct} / ${subjectScores[subj].total}</p>`;
    }

    document.getElementById("score-details").innerHTML = detailsHtml;
}

loadQuestion();

//================ TIMER ===================
let time = 90 * 60;

const timerInterval = setInterval(() => {
    let mins = Math.floor(time / 60);
    let secs = time % 60;

    document.getElementById("timer").innerHTML = `${mins}:${secs < 10 ? "0" : ""}${secs}`;

    if (time > 0) {
        time--;
    } else {
        clearInterval(timerInterval);
        alert("Time is up! Your answers are being submitted automatically.");
        calculateResults();
    }
}, 1000);

</script>

</body>
</html>

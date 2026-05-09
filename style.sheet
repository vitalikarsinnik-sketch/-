document.addEventListener('DOMContentLoaded', () => {

    const questions = [
    {
        question: "Що таке операційна система?",
        answers: ["Пристрій для друку", "Програма для керування комп’ютером", "Комп’ютерна гра", "Тип монітора"],
        correct: 1
    },
    {
        question: "Для чого потрібен процесор?",
        answers: ["Для збереження файлів", "Для обробки інформації", "Для друку", "Для інтернету"],
        correct: 1
    },
    {
        question: "Який пристрій використовується для введення тексту?",
        answers: ["Монітор", "Принтер", "Клавіатура", "Колонки"],
        correct: 2
    },
    {
        question: "Що таке браузер?",
        answers: ["Програма для перегляду сайтів", "Антивірус", "Редактор фото", "Гра"],
        correct: 0
    },
    {
        question: "Для чого потрібна оперативна пам’ять?",
        answers: ["Для друку", "Для тимчасового зберігання даних", "Для охолодження", "Для звуку"],
        correct: 1
    },
    {
        question: "Який пристрій друкує документи?",
        answers: ["Сканер", "Миша", "Принтер", "Монітор"],
        correct: 2
    },
    {
        question: "Що таке комп’ютерний вірус?",
        answers: ["Корисна програма", "Шкідлива програма", "Тип браузера", "Файл"],
        correct: 1
    },
    {
        question: "Для чого потрібен антивірус?",
        answers: ["Для ігор", "Для створення фото", "Для захисту комп’ютера", "Для музики"],
        correct: 2
    },
    {
        question: "Що таке Wi-Fi?",
        answers: ["Тип процесора", "Бездротовий інтернет", "Клавіатура", "Монітор"],
        correct: 1
    },
    {
        question: "Який пристрій є пристроєм введення?",
        answers: ["Принтер", "Монітор", "Миша", "Проектор"],
        correct: 2
    }
];
    const startScreen = document.querySelector('#start-screen');
    const quizScreen = document.querySelector('#quiz-screen');
    const resultScreen = document.querySelector('#result-screen');
    const startBtn = document.querySelector('#start-btn');
    const restartBtn = document.querySelector('#restart-btn');
    const resultText = document.querySelector('#result-text');
    const questionText = document.querySelector('#question-text');
    const answersContainer = document.querySelector('#answers-container');
    const timerDisplay = document.querySelector('#timer');
    const themeToggle = document.querySelector('#theme-toggle');

    let questionIndex = 0;
    let score = 0;
    let timer = 15;
    let interval;

    // ============ ПЕРЕМИКАННЯ ТЕМИ ============
    // Перевіряємо збережену тему
    if (localStorage.getItem('theme') === 'dark') {
        document.body.classList.add('dark-theme');
        themeToggle.textContent = '☀️'; // Сонце для темної теми (щоб переключити на світлу)
    } else {
        themeToggle.textContent = '🌙'; // Місяць для світлої теми (щоб переключити на темну)
    }

    // Обробник кліку на кнопку теми
    themeToggle.addEventListener('click', () => {
        document.body.classList.toggle('dark-theme');
        
        if (document.body.classList.contains('dark-theme')) {
            localStorage.setItem('theme', 'dark');
            themeToggle.textContent = '☀️'; // Показуємо сонце (можна переключити на світлу)
        } else {
            localStorage.setItem('theme', 'light');
            themeToggle.textContent = '🌙'; // Показуємо місяць (можна переключити на темну)
        }
    });

    function showQuestion(question) {
        clearInterval(interval);
        startTimer();

        answersContainer.innerHTML = '';
        questionText.innerText = question.question;

        question.answers.forEach((answer, i) => {
            const button = document.createElement('button');
            button.innerText = answer;
            button.classList.add('answer-btn');
            button.addEventListener('click', () => checkAnswer(button, i));
            answersContainer.appendChild(button);
        });
    }

    function nextQuestion() {
        questionIndex++;
        if (questionIndex < questions.length) {
            showQuestion(questions[questionIndex]);
        } else {
            showResult();
        }
    }

    function checkAnswer(button, i) {
        const correctAnswer = questions[questionIndex].correct;
        
        // Показуємо правильну відповідь зеленим
        const allButtons = document.querySelectorAll('.answer-btn');
        allButtons.forEach((btn, index) => {
            btn.disabled = true;
            if (index === correctAnswer) {
                btn.classList.add('correct');
            }
        });
        
        // Якщо натиснута кнопка неправильна - показуємо червоним
        if (i !== correctAnswer) {
            button.classList.add('wrong');
        } else {
            score++;
        }

        setTimeout(nextQuestion, 1000);
    }

    function showResult() {
        clearInterval(interval);
        const accuracy = Math.round((score / questions.length) * 100);
        resultText.innerText = `Твій результат: ${score}/${questions.length} (${accuracy}%)`;

        quizScreen.classList.add('hide');
        resultScreen.classList.remove('hide');

        const finalScore = document.querySelector('#final-score');
        finalScore.innerText = score;
    }

    function startGame() {
        startScreen.classList.add('hide');
        resultScreen.classList.add('hide');
        quizScreen.classList.remove('hide');

        questionIndex = 0;
        score = 0;

        showQuestion(questions[questionIndex]);
    }

    function startTimer() {
        timer = 15;
        timerDisplay.innerText = `Час: ${timer}`;

        interval = setInterval(() => {
            timer--;
            timerDisplay.innerText = `Час: ${timer}`;

            if (timer <= 0) {
                clearInterval(interval);
                // Якщо час вийшов - показуємо правильну відповідь
                const allButtons = document.querySelectorAll('.answer-btn');
                const correctAnswer = questions[questionIndex].correct;
                allButtons.forEach((btn, index) => {
                    btn.disabled = true;
                    if (index === correctAnswer) {
                        btn.classList.add('correct');
                    }
                });
                setTimeout(nextQuestion, 1000);
            }
        }, 1000);
    }

    startBtn.addEventListener('click', startGame);

    restartBtn.addEventListener('click', () => {
        startGame();
        resultScreen.classList.add('hide');
    });

});

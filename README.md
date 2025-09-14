<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>QuizMaster - Create & Take Quizzes</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap');
        body { font-family: 'Inter', sans-serif; }
        .quiz-card { transition: all 0.3s ease; }
        .quiz-card:hover { transform: translateY(-4px); }
        .fade-in { animation: fadeIn 0.5s ease-in; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
        .slide-in { animation: slideIn 0.3s ease-out; }
        @keyframes slideIn { from { transform: translateX(-100%); } to { transform: translateX(0); } }
    </style>
</head>
<body class="bg-gradient-to-br from-blue-50 to-indigo-100 min-h-screen">
    <!-- Navigation -->
    <nav class="bg-white shadow-lg sticky top-0 z-50">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between items-center h-16">
                <div class="flex items-center">
                    <div class="text-2xl font-bold text-indigo-600">🧠 QuizMaster</div>
                </div>
                <div class="flex items-center space-x-4">
                    <button id="loginBtn" class="text-gray-700 hover:text-indigo-600 px-3 py-2 rounded-md text-sm font-medium">Login</button>
                    <button id="registerBtn" class="bg-indigo-600 hover:bg-indigo-700 text-white px-4 py-2 rounded-md text-sm font-medium">Register</button>
                    <div id="userMenu" class="hidden flex items-center space-x-4">
                        <span id="welcomeUser" class="text-gray-700 font-medium"></span>
                        <button id="logoutBtn" class="text-red-600 hover:text-red-700 px-3 py-2 rounded-md text-sm font-medium">Logout</button>
                    </div>
                </div>
            </div>
        </div>
    </nav>

    <!-- Main Content -->
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
        
        <!-- Home Page -->
        <div id="homePage" class="fade-in">
            <div class="text-center mb-12">
                <h1 class="text-5xl font-bold text-gray-900 mb-4">Welcome to QuizMaster</h1>
                <p class="text-xl text-gray-600 mb-8">Create engaging quizzes or test your knowledge with our interactive platform</p>
                <div class="flex flex-col sm:flex-row gap-4 justify-center">
                    <button id="createQuizBtn" class="bg-indigo-600 hover:bg-indigo-700 text-white px-8 py-4 rounded-lg text-lg font-semibold shadow-lg hover:shadow-xl transition-all">
                        🎯 Create a Quiz
                    </button>
                    <button id="browseQuizzesBtn" class="bg-green-600 hover:bg-green-700 text-white px-8 py-4 rounded-lg text-lg font-semibold shadow-lg hover:shadow-xl transition-all">
                        📚 Browse Quizzes
                    </button>
                </div>
            </div>

            <!-- Featured Stats -->
            <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mb-12">
                <div class="bg-white rounded-xl p-6 shadow-lg text-center">
                    <div class="text-3xl font-bold text-indigo-600" id="totalQuizzes">0</div>
                    <div class="text-gray-600">Total Quizzes</div>
                </div>
                <div class="bg-white rounded-xl p-6 shadow-lg text-center">
                    <div class="text-3xl font-bold text-green-600" id="totalUsers">0</div>
                    <div class="text-gray-600">Registered Users</div>
                </div>
                <div class="bg-white rounded-xl p-6 shadow-lg text-center">
                    <div class="text-3xl font-bold text-purple-600" id="totalAttempts">0</div>
                    <div class="text-gray-600">Quiz Attempts</div>
                </div>
            </div>
        </div>

        <!-- Login/Register Modal -->
        <div id="authModal" class="hidden fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50">
            <div class="bg-white rounded-xl p-8 max-w-md w-full mx-4 fade-in">
                <div id="loginForm">
                    <h2 class="text-2xl font-bold mb-6 text-center">Login to QuizMaster</h2>
                    <form id="loginFormElement">
                        <div class="mb-4">
                            <label class="block text-gray-700 text-sm font-bold mb-2">Username</label>
                            <input type="text" id="loginUsername" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500" required>
                        </div>
                        <div class="mb-6">
                            <label class="block text-gray-700 text-sm font-bold mb-2">Password</label>
                            <input type="password" id="loginPassword" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500" required>
                        </div>
                        <button type="submit" class="w-full bg-indigo-600 hover:bg-indigo-700 text-white font-bold py-2 px-4 rounded-md">Login</button>
                    </form>
                    <p class="text-center mt-4 text-gray-600">Don't have an account? <button id="switchToRegister" class="text-indigo-600 hover:underline">Register here</button></p>
                </div>

                <div id="registerForm" class="hidden">
                    <h2 class="text-2xl font-bold mb-6 text-center">Register for QuizMaster</h2>
                    <form id="registerFormElement">
                        <div class="mb-4">
                            <label class="block text-gray-700 text-sm font-bold mb-2">Username</label>
                            <input type="text" id="registerUsername" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500" required>
                        </div>
                        <div class="mb-4">
                            <label class="block text-gray-700 text-sm font-bold mb-2">Email</label>
                            <input type="email" id="registerEmail" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500" required>
                        </div>
                        <div class="mb-6">
                            <label class="block text-gray-700 text-sm font-bold mb-2">Password</label>
                            <input type="password" id="registerPassword" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500" required>
                        </div>
                        <button type="submit" class="w-full bg-green-600 hover:bg-green-700 text-white font-bold py-2 px-4 rounded-md">Register</button>
                    </form>
                    <p class="text-center mt-4 text-gray-600">Already have an account? <button id="switchToLogin" class="text-indigo-600 hover:underline">Login here</button></p>
                </div>
                <button id="closeModal" class="absolute top-4 right-4 text-gray-500 hover:text-gray-700 text-2xl">&times;</button>
            </div>
        </div>

        <!-- Quiz Creation Page -->
        <div id="quizCreationPage" class="hidden fade-in">
            <div class="max-w-4xl mx-auto">
                <div class="flex items-center mb-8">
                    <button id="backToHome" class="text-indigo-600 hover:text-indigo-800 mr-4">← Back to Home</button>
                    <h1 class="text-3xl font-bold text-gray-900">Create New Quiz</h1>
                </div>

                <div class="bg-white rounded-xl shadow-lg p-8">
                    <form id="quizForm">
                        <div class="mb-6">
                            <label class="block text-gray-700 text-sm font-bold mb-2">Quiz Title</label>
                            <input type="text" id="quizTitle" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-indigo-500" placeholder="Enter quiz title" required>
                        </div>
                        
                        <div class="mb-6">
                            <label class="block text-gray-700 text-sm font-bold mb-2">Quiz Description</label>
                            <textarea id="quizDescription" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-indigo-500" rows="3" placeholder="Brief description of your quiz"></textarea>
                        </div>

                        <div class="mb-6">
                            <div class="flex justify-between items-center mb-4">
                                <h3 class="text-lg font-semibold text-gray-900">Questions</h3>
                                <button type="button" id="addQuestionBtn" class="bg-green-600 hover:bg-green-700 text-white px-4 py-2 rounded-lg font-medium">+ Add Question</button>
                            </div>
                            <div id="questionsContainer"></div>
                        </div>

                        <div class="flex gap-4">
                            <button type="submit" class="bg-indigo-600 hover:bg-indigo-700 text-white px-8 py-3 rounded-lg font-semibold">Create Quiz</button>
                            <button type="button" id="cancelQuizCreation" class="bg-gray-500 hover:bg-gray-600 text-white px-8 py-3 rounded-lg font-semibold">Cancel</button>
                        </div>
                    </form>
                </div>
            </div>
        </div>

        <!-- Quiz Listing Page -->
        <div id="quizListingPage" class="hidden fade-in">
            <div class="flex items-center justify-between mb-8">
                <div class="flex items-center">
                    <button id="backToHomeFromList" class="text-indigo-600 hover:text-indigo-800 mr-4">← Back to Home</button>
                    <h1 class="text-3xl font-bold text-gray-900">Available Quizzes</h1>
                </div>
                <div class="flex gap-4">
                    <input type="text" id="searchQuizzes" class="px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-indigo-500" placeholder="Search quizzes...">
                    <select id="filterCategory" class="px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-indigo-500">
                        <option value="">All Categories</option>
                        <option value="science">Science</option>
                        <option value="history">History</option>
                        <option value="sports">Sports</option>
                        <option value="general">General Knowledge</option>
                    </select>
                </div>
            </div>
            <div id="quizzesGrid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6"></div>
        </div>

        <!-- Quiz Taking Page -->
        <div id="quizTakingPage" class="hidden fade-in">
            <div class="max-w-4xl mx-auto">
                <div class="flex items-center justify-between mb-8">
                    <button id="backToQuizList" class="text-indigo-600 hover:text-indigo-800">← Back to Quizzes</button>
                    <div class="flex items-center space-x-4">
                        <div class="text-sm text-gray-600">Question <span id="currentQuestionNum">1</span> of <span id="totalQuestions">1</span></div>
                        <div class="bg-gray-200 rounded-full h-2 w-32">
                            <div id="progressBar" class="bg-indigo-600 h-2 rounded-full transition-all duration-300" style="width: 0%"></div>
                        </div>
                    </div>
                </div>

                <div class="bg-white rounded-xl shadow-lg p-8">
                    <h2 id="quizTakingTitle" class="text-2xl font-bold text-gray-900 mb-6"></h2>
                    <div id="questionContainer">
                        <h3 id="questionText" class="text-xl font-semibold text-gray-800 mb-6"></h3>
                        <div id="answersContainer" class="space-y-3"></div>
                    </div>
                    <div class="flex justify-between mt-8">
                        <button id="prevQuestionBtn" class="bg-gray-500 hover:bg-gray-600 text-white px-6 py-3 rounded-lg font-medium disabled:opacity-50 disabled:cursor-not-allowed">Previous</button>
                        <button id="nextQuestionBtn" class="bg-indigo-600 hover:bg-indigo-700 text-white px-6 py-3 rounded-lg font-medium">Next Question</button>
                        <button id="submitQuizBtn" class="hidden bg-green-600 hover:bg-green-700 text-white px-6 py-3 rounded-lg font-medium">Submit Quiz</button>
                    </div>
                </div>
            </div>
        </div>

        <!-- Quiz Results Page -->
        <div id="quizResultsPage" class="hidden fade-in">
            <div class="max-w-4xl mx-auto">
                <div class="text-center mb-8">
                    <h1 class="text-4xl font-bold text-gray-900 mb-4">Quiz Complete! 🎉</h1>
                    <div class="bg-white rounded-xl shadow-lg p-8 mb-8">
                        <div class="text-6xl font-bold mb-4" id="finalScore">0%</div>
                        <div class="text-xl text-gray-600 mb-4">Your Score</div>
                        <div class="text-lg text-gray-700" id="scoreDetails">You got 0 out of 0 questions correct</div>
                    </div>
                </div>

                <div class="bg-white rounded-xl shadow-lg p-8 mb-8">
                    <h2 class="text-2xl font-bold text-gray-900 mb-6">Review Answers</h2>
                    <div id="reviewContainer"></div>
                </div>

                <div class="text-center">
                    <button id="retakeQuizBtn" class="bg-indigo-600 hover:bg-indigo-700 text-white px-8 py-3 rounded-lg font-semibold mr-4">Retake Quiz</button>
                    <button id="backToQuizzesFromResults" class="bg-gray-500 hover:bg-gray-600 text-white px-8 py-3 rounded-lg font-semibold">Browse More Quizzes</button>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Application State
        let currentUser = null;
        let quizzes = [];
        let users = [];
        let currentQuiz = null;
        let currentQuestionIndex = 0;
        let userAnswers = [];
        let questionCount = 0;

        // Initialize app
        document.addEventListener('DOMContentLoaded', function() {
            loadData();
            updateStats();
            setupEventListeners();
            checkAuthState();
        });

        // Data Management
        function loadData() {
            const savedQuizzes = localStorage.getItem('quizzes');
            const savedUsers = localStorage.getItem('users');
            const savedCurrentUser = localStorage.getItem('currentUser');
            
            if (savedQuizzes) quizzes = JSON.parse(savedQuizzes);
            if (savedUsers) users = JSON.parse(savedUsers);
            if (savedCurrentUser) currentUser = JSON.parse(savedCurrentUser);
        }

        function saveData() {
            localStorage.setItem('quizzes', JSON.stringify(quizzes));
            localStorage.setItem('users', JSON.stringify(users));
            localStorage.setItem('currentUser', JSON.stringify(currentUser));
        }

        function updateStats() {
            document.getElementById('totalQuizzes').textContent = quizzes.length;
            document.getElementById('totalUsers').textContent = users.length;
            const totalAttempts = quizzes.reduce((sum, quiz) => sum + (quiz.attempts || 0), 0);
            document.getElementById('totalAttempts').textContent = totalAttempts;
        }

        // Event Listeners
        function setupEventListeners() {
            // Navigation
            document.getElementById('loginBtn').addEventListener('click', () => showAuthModal('login'));
            document.getElementById('registerBtn').addEventListener('click', () => showAuthModal('register'));
            document.getElementById('logoutBtn').addEventListener('click', logout);
            document.getElementById('closeModal').addEventListener('click', hideAuthModal);
            
            // Auth forms
            document.getElementById('switchToRegister').addEventListener('click', () => switchAuthForm('register'));
            document.getElementById('switchToLogin').addEventListener('click', () => switchAuthForm('login'));
            document.getElementById('loginFormElement').addEventListener('submit', handleLogin);
            document.getElementById('registerFormElement').addEventListener('submit', handleRegister);
            
            // Home page
            document.getElementById('createQuizBtn').addEventListener('click', showQuizCreation);
            document.getElementById('browseQuizzesBtn').addEventListener('click', showQuizListing);
            
            // Quiz creation
            document.getElementById('backToHome').addEventListener('click', showHomePage);
            document.getElementById('cancelQuizCreation').addEventListener('click', showHomePage);
            document.getElementById('addQuestionBtn').addEventListener('click', addQuestion);
            document.getElementById('quizForm').addEventListener('submit', handleQuizCreation);
            
            // Quiz listing
            document.getElementById('backToHomeFromList').addEventListener('click', showHomePage);
            document.getElementById('searchQuizzes').addEventListener('input', filterQuizzes);
            document.getElementById('filterCategory').addEventListener('change', filterQuizzes);
            
            // Quiz taking
            document.getElementById('backToQuizList').addEventListener('click', showQuizListing);
            document.getElementById('prevQuestionBtn').addEventListener('click', previousQuestion);
            document.getElementById('nextQuestionBtn').addEventListener('click', nextQuestion);
            document.getElementById('submitQuizBtn').addEventListener('click', submitQuiz);
            
            // Quiz results
            document.getElementById('retakeQuizBtn').addEventListener('click', retakeQuiz);
            document.getElementById('backToQuizzesFromResults').addEventListener('click', showQuizListing);
        }

        // Authentication
        function checkAuthState() {
            if (currentUser) {
                showUserMenu();
            } else {
                showGuestMenu();
            }
        }

        function showUserMenu() {
            document.getElementById('loginBtn').classList.add('hidden');
            document.getElementById('registerBtn').classList.add('hidden');
            document.getElementById('userMenu').classList.remove('hidden');
            document.getElementById('welcomeUser').textContent = `Welcome, ${currentUser.username}!`;
        }

        function showGuestMenu() {
            document.getElementById('loginBtn').classList.remove('hidden');
            document.getElementById('registerBtn').classList.remove('hidden');
            document.getElementById('userMenu').classList.add('hidden');
        }

        function showAuthModal(type) {
            document.getElementById('authModal').classList.remove('hidden');
            switchAuthForm(type);
        }

        function hideAuthModal() {
            document.getElementById('authModal').classList.add('hidden');
        }

        function switchAuthForm(type) {
            if (type === 'login') {
                document.getElementById('loginForm').classList.remove('hidden');
                document.getElementById('registerForm').classList.add('hidden');
            } else {
                document.getElementById('loginForm').classList.add('hidden');
                document.getElementById('registerForm').classList.remove('hidden');
            }
        }

        function handleLogin(e) {
            e.preventDefault();
            const username = document.getElementById('loginUsername').value;
            const password = document.getElementById('loginPassword').value;
            
            const user = users.find(u => u.username === username && u.password === password);
            if (user) {
                currentUser = user;
                saveData();
                checkAuthState();
                hideAuthModal();
                alert('Login successful!');
            } else {
                alert('Invalid username or password');
            }
        }

        function handleRegister(e) {
            e.preventDefault();
            const username = document.getElementById('registerUsername').value;
            const email = document.getElementById('registerEmail').value;
            const password = document.getElementById('registerPassword').value;
            
            if (users.find(u => u.username === username)) {
                alert('Username already exists');
                return;
            }
            
            const newUser = {
                id: Date.now(),
                username,
                email,
                password,
                createdAt: new Date().toISOString()
            };
            
            users.push(newUser);
            currentUser = newUser;
            saveData();
            checkAuthState();
            hideAuthModal();
            updateStats();
            alert('Registration successful!');
        }

        function logout() {
            currentUser = null;
            localStorage.removeItem('currentUser');
            checkAuthState();
            showHomePage();
        }

        // Page Navigation
        function showPage(pageId) {
            const pages = ['homePage', 'quizCreationPage', 'quizListingPage', 'quizTakingPage', 'quizResultsPage'];
            pages.forEach(page => {
                document.getElementById(page).classList.add('hidden');
            });
            document.getElementById(pageId).classList.remove('hidden');
        }

        function showHomePage() {
            showPage('homePage');
            updateStats();
        }

        function showQuizCreation() {
            if (!currentUser) {
                showAuthModal('login');
                return;
            }
            showPage('quizCreationPage');
            resetQuizForm();
        }

        function showQuizListing() {
            showPage('quizListingPage');
            displayQuizzes();
        }

        // Quiz Creation
        function resetQuizForm() {
            document.getElementById('quizForm').reset();
            document.getElementById('questionsContainer').innerHTML = '';
            questionCount = 0;
            addQuestion(); // Add first question
        }

        function addQuestion() {
            questionCount++;
            const container = document.getElementById('questionsContainer');
            const questionDiv = document.createElement('div');
            questionDiv.className = 'border border-gray-200 rounded-lg p-6 mb-4 slide-in';
            questionDiv.innerHTML = `
                <div class="flex justify-between items-center mb-4">
                    <h4 class="text-lg font-semibold text-gray-800">Question ${questionCount}</h4>
                    <button type="button" class="text-red-600 hover:text-red-800 font-medium" onclick="removeQuestion(this)">Remove</button>
                </div>
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-bold mb-2">Question Text</label>
                    <input type="text" class="question-text w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500" placeholder="Enter your question" required>
                </div>
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-bold mb-2">Answer Options</label>
                    <div class="space-y-2">
                        <div class="flex items-center space-x-2">
                            <input type="radio" name="correct-${questionCount}" value="0" class="correct-answer">
                            <input type="text" class="answer-option flex-1 px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500" placeholder="Option A" required>
                        </div>
                        <div class="flex items-center space-x-2">
                            <input type="radio" name="correct-${questionCount}" value="1" class="correct-answer">
                            <input type="text" class="answer-option flex-1 px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500" placeholder="Option B" required>
                        </div>
                        <div class="flex items-center space-x-2">
                            <input type="radio" name="correct-${questionCount}" value="2" class="correct-answer">
                            <input type="text" class="answer-option flex-1 px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500" placeholder="Option C" required>
                        </div>
                        <div class="flex items-center space-x-2">
                            <input type="radio" name="correct-${questionCount}" value="3" class="correct-answer">
                            <input type="text" class="answer-option flex-1 px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500" placeholder="Option D" required>
                        </div>
                    </div>
                    <p class="text-sm text-gray-600 mt-2">Select the radio button next to the correct answer</p>
                </div>
            `;
            container.appendChild(questionDiv);
        }

        function removeQuestion(button) {
            if (document.querySelectorAll('#questionsContainer > div').length > 1) {
                button.closest('div').remove();
                updateQuestionNumbers();
            } else {
                alert('You must have at least one question');
            }
        }

        function updateQuestionNumbers() {
            const questions = document.querySelectorAll('#questionsContainer > div');
            questions.forEach((question, index) => {
                question.querySelector('h4').textContent = `Question ${index + 1}`;
            });
        }

        function handleQuizCreation(e) {
            e.preventDefault();
            
            const title = document.getElementById('quizTitle').value;
            const description = document.getElementById('quizDescription').value;
            const questionElements = document.querySelectorAll('#questionsContainer > div');
            
            const questions = [];
            let isValid = true;
            
            questionElements.forEach((questionEl, index) => {
                const questionText = questionEl.querySelector('.question-text').value;
                const answerOptions = Array.from(questionEl.querySelectorAll('.answer-option')).map(input => input.value);
                const correctAnswerRadio = questionEl.querySelector('input[type="radio"]:checked');
                
                if (!correctAnswerRadio) {
                    alert(`Please select the correct answer for Question ${index + 1}`);
                    isValid = false;
                    return;
                }
                
                const correctAnswer = parseInt(correctAnswerRadio.value);
                
                questions.push({
                    text: questionText,
                    options: answerOptions,
                    correctAnswer: correctAnswer
                });
            });
            
            if (!isValid) return;
            
            const newQuiz = {
                id: Date.now(),
                title,
                description,
                questions,
                createdBy: currentUser.username,
                createdAt: new Date().toISOString(),
                attempts: 0
            };
            
            quizzes.push(newQuiz);
            saveData();
            updateStats();
            alert('Quiz created successfully!');
            showQuizListing();
        }

        // Quiz Listing
        function displayQuizzes(filteredQuizzes = null) {
            const container = document.getElementById('quizzesGrid');
            const quizzesToShow = filteredQuizzes || quizzes;
            
            if (quizzesToShow.length === 0) {
                container.innerHTML = '<div class="col-span-full text-center text-gray-500 py-12">No quizzes found. Create the first one!</div>';
                return;
            }
            
            container.innerHTML = quizzesToShow.map(quiz => `
                <div class="quiz-card bg-white rounded-xl shadow-lg p-6 cursor-pointer" onclick="startQuiz(${quiz.id})">
                    <h3 class="text-xl font-bold text-gray-900 mb-2">${quiz.title}</h3>
                    <p class="text-gray-600 mb-4">${quiz.description || 'No description available'}</p>
                    <div class="flex justify-between items-center text-sm text-gray-500">
                        <span>By ${quiz.createdBy}</span>
                        <span>${quiz.questions.length} questions</span>
                    </div>
                    <div class="flex justify-between items-center mt-4">
                        <span class="text-sm text-gray-500">${quiz.attempts || 0} attempts</span>
                        <button class="bg-indigo-600 hover:bg-indigo-700 text-white px-4 py-2 rounded-lg font-medium">Take Quiz</button>
                    </div>
                </div>
            `).join('');
        }

        function filterQuizzes() {
            const searchTerm = document.getElementById('searchQuizzes').value.toLowerCase();
            const category = document.getElementById('filterCategory').value;
            
            let filtered = quizzes.filter(quiz => {
                const matchesSearch = quiz.title.toLowerCase().includes(searchTerm) || 
                                    quiz.description.toLowerCase().includes(searchTerm);
                const matchesCategory = !category || quiz.category === category;
                return matchesSearch && matchesCategory;
            });
            
            displayQuizzes(filtered);
        }

        // Quiz Taking
        function startQuiz(quizId) {
            currentQuiz = quizzes.find(q => q.id === quizId);
            if (!currentQuiz) return;
            
            currentQuestionIndex = 0;
            userAnswers = new Array(currentQuiz.questions.length).fill(null);
            
            showPage('quizTakingPage');
            document.getElementById('quizTakingTitle').textContent = currentQuiz.title;
            document.getElementById('totalQuestions').textContent = currentQuiz.questions.length;
            
            displayQuestion();
        }

        function displayQuestion() {
            const question = currentQuiz.questions[currentQuestionIndex];
            const progress = ((currentQuestionIndex + 1) / currentQuiz.questions.length) * 100;
            
            document.getElementById('currentQuestionNum').textContent = currentQuestionIndex + 1;
            document.getElementById('progressBar').style.width = `${progress}%`;
            document.getElementById('questionText').textContent = question.text;
            
            const answersContainer = document.getElementById('answersContainer');
            answersContainer.innerHTML = question.options.map((option, index) => `
                <label class="flex items-center p-4 border border-gray-200 rounded-lg cursor-pointer hover:bg-gray-50 ${userAnswers[currentQuestionIndex] === index ? 'bg-indigo-50 border-indigo-500' : ''}">
                    <input type="radio" name="answer" value="${index}" class="mr-3" ${userAnswers[currentQuestionIndex] === index ? 'checked' : ''}>
                    <span class="text-gray-800">${option}</span>
                </label>
            `).join('');
            
            // Add event listeners to radio buttons
            answersContainer.querySelectorAll('input[type="radio"]').forEach(radio => {
                radio.addEventListener('change', (e) => {
                    userAnswers[currentQuestionIndex] = parseInt(e.target.value);
                    displayQuestion(); // Refresh to show selection
                });
            });
            
            // Update navigation buttons
            document.getElementById('prevQuestionBtn').disabled = currentQuestionIndex === 0;
            
            if (currentQuestionIndex === currentQuiz.questions.length - 1) {
                document.getElementById('nextQuestionBtn').classList.add('hidden');
                document.getElementById('submitQuizBtn').classList.remove('hidden');
            } else {
                document.getElementById('nextQuestionBtn').classList.remove('hidden');
                document.getElementById('submitQuizBtn').classList.add('hidden');
            }
        }

        function previousQuestion() {
            if (currentQuestionIndex > 0) {
                currentQuestionIndex--;
                displayQuestion();
            }
        }

        function nextQuestion() {
            if (currentQuestionIndex < currentQuiz.questions.length - 1) {
                currentQuestionIndex++;
                displayQuestion();
            }
        }

        function submitQuiz() {
            // Update quiz attempts
            currentQuiz.attempts = (currentQuiz.attempts || 0) + 1;
            saveData();
            
            showQuizResults();
        }

        // Quiz Results
        function showQuizResults() {
            showPage('quizResultsPage');
            
            let correctAnswers = 0;
            const totalQuestions = currentQuiz.questions.length;
            
            currentQuiz.questions.forEach((question, index) => {
                if (userAnswers[index] === question.correctAnswer) {
                    correctAnswers++;
                }
            });
            
            const percentage = Math.round((correctAnswers / totalQuestions) * 100);
            
            document.getElementById('finalScore').textContent = `${percentage}%`;
            document.getElementById('scoreDetails').textContent = `You got ${correctAnswers} out of ${totalQuestions} questions correct`;
            
            // Display review
            const reviewContainer = document.getElementById('reviewContainer');
            reviewContainer.innerHTML = currentQuiz.questions.map((question, index) => {
                const userAnswer = userAnswers[index];
                const isCorrect = userAnswer === question.correctAnswer;
                
                return `
                    <div class="mb-6 p-4 border rounded-lg ${isCorrect ? 'border-green-200 bg-green-50' : 'border-red-200 bg-red-50'}">
                        <h4 class="font-semibold text-gray-900 mb-2">Question ${index + 1}: ${question.text}</h4>
                        <div class="space-y-2">
                            ${question.options.map((option, optIndex) => {
                                let classes = 'p-2 rounded';
                                if (optIndex === question.correctAnswer) {
                                    classes += ' bg-green-200 text-green-800';
                                } else if (optIndex === userAnswer && userAnswer !== question.correctAnswer) {
                                    classes += ' bg-red-200 text-red-800';
                                } else {
                                    classes += ' bg-gray-100';
                                }
                                
                                return `<div class="${classes}">${option} ${optIndex === question.correctAnswer ? '✓' : ''} ${optIndex === userAnswer && userAnswer !== question.correctAnswer ? '✗' : ''}</div>`;
                            }).join('')}
                        </div>
                    </div>
                `;
            }).join('');
        }

        function retakeQuiz() {
            startQuiz(currentQuiz.id);
        }
    </script>
<script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'97d6245791ad8fb2',t:'MTc1NzU4Mjk4MC4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>

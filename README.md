<html....>
<html lang="th">
 <head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Kimi-wa-Melody - MelodyCat</title>
  <script src="/_sdk/data_sdk.js"></script>
  <script src="/_sdk/element_sdk.js"></script>
  <style>
    body {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: 'Kanit', 'Sarabun', Arial, sans-serif;
      background: linear-gradient(135deg, #d4c5a9 0%, #b8a58a 100%);
      min-height: 100%;
      width: 100%;
    }

    * {
      box-sizing: border-box;
    }

    .app-container {
      width: 100%;
      min-height: 100%;
      padding: 20px;
      display: flex;
      flex-direction: column;
      align-items: center;
    }

    .card {
      background: #f5ede0;
      border-radius: 20px;
      box-shadow: 0 8px 24px rgba(0,0,0,0.15);
      padding: 30px;
      margin: 15px 0;
      width: 100%;
      max-width: 900px;
    }

    h1 {
      color: #5c4a3a;
      text-align: center;
      font-size: 2.5rem;
      margin: 0 0 10px 0;
    }

    .mascot-tag {
      text-align: center;
      color: #8b7355;
      font-size: 1.1rem;
      margin-bottom: 20px;
    }

    .form-group {
      margin: 15px 0;
    }

    label {
      display: block;
      color: #5c4a3a;
      font-weight: 600;
      margin-bottom: 8px;
      font-size: 1rem;
    }

    input, select {
      width: 100%;
      padding: 12px 15px;
      border: 2px solid #c4b5a0;
      border-radius: 10px;
      font-size: 1rem;
      background: white;
      transition: all 0.3s;
    }

    input:focus, select:focus {
      outline: none;
      border-color: #8b7355;
      box-shadow: 0 0 0 3px rgba(139, 115, 85, 0.1);
    }

    .btn {
      padding: 14px 28px;
      border: none;
      border-radius: 12px;
      font-size: 1.1rem;
      font-weight: 600;
      cursor: pointer;
      transition: all 0.3s;
      box-shadow: 0 4px 12px rgba(0,0,0,0.15);
      font-family: inherit;
    }

    .btn:hover {
      transform: translateY(-2px);
      box-shadow: 0 6px 16px rgba(0,0,0,0.2);
    }

    .btn:active {
      transform: translateY(0);
    }

    .btn:disabled {
      opacity: 0.6;
      cursor: not-allowed;
      transform: none;
    }

    .btn-primary {
      background: linear-gradient(135deg, #8b7355 0%, #6d5a45 100%);
      color: white;
    }

    .btn-success {
      background: linear-gradient(135deg, #7a9b6f 0%, #5d7a52 100%);
      color: white;
    }

    .btn-info {
      background: linear-gradient(135deg, #9bb3c4 0%, #7a96aa 100%);
      color: white;
    }

    .btn-warning {
      background: linear-gradient(135deg, #c4a569 0%, #a68a52 100%);
      color: white;
    }

    .btn-secondary {
      background: linear-gradient(135deg, #a89f91 0%, #8a8175 100%);
      color: white;
    }

    .staff-container {
      background: white;
      border-radius: 15px;
      padding: 40px 20px;
      margin: 20px 0;
      box-shadow: inset 0 2px 8px rgba(0,0,0,0.05);
      overflow-x: auto;
    }

    #musicStaff {
      display: block;
      margin: 0 auto;
      max-width: 100%;
      height: auto;
    }

    .controls {
      display: flex;
      gap: 12px;
      flex-wrap: wrap;
      justify-content: center;
      margin: 20px 0;
    }

    .info-bar {
      display: flex;
      justify-content: space-between;
      align-items: center;
      background: linear-gradient(135deg, #8b7355 0%, #6d5a45 100%);
      color: white;
      padding: 15px 25px;
      border-radius: 12px;
      font-size: 1.2rem;
      font-weight: 600;
      margin: 15px 0;
    }

    .choices-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
      gap: 15px;
      margin: 20px 0;
    }

    .choice-btn {
      padding: 20px;
      background: white;
      border: 3px solid #c4b5a0;
      border-radius: 12px;
      font-size: 1.3rem;
      font-weight: 600;
      color: #5c4a3a;
      cursor: pointer;
      transition: all 0.3s;
    }

    .choice-btn:hover {
      background: #f0e8d8;
      border-color: #8b7355;
      transform: scale(1.05);
    }

    .choice-btn.correct {
      background: #7a9b6f;
      color: white;
      border-color: #5d7a52;
    }

    .choice-btn.incorrect {
      background: #c47a6f;
      color: white;
      border-color: #a65d52;
    }

    .feedback {
      text-align: center;
      font-size: 1.3rem;
      font-weight: 600;
      padding: 15px;
      border-radius: 10px;
      margin: 15px 0;
      display: none;
    }

    .feedback.show {
      display: block;
    }

    .feedback.correct {
      background: #e8f5e4;
      color: #5d7a52;
      border: 2px solid #7a9b6f;
    }

    .feedback.incorrect {
      background: #f5e4e4;
      color: #a65d52;
      border: 2px solid #c47a6f;
    }

    .level-select {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(80px, 1fr));
      gap: 10px;
      margin: 20px 0;
    }

    .level-btn {
      padding: 15px;
      background: white;
      border: 2px solid #c4b5a0;
      border-radius: 10px;
      font-size: 1rem;
      font-weight: 600;
      color: #5c4a3a;
      cursor: pointer;
      transition: all 0.3s;
    }

    .level-btn:hover {
      background: #f0e8d8;
      transform: scale(1.05);
    }

    .level-btn.completed {
      background: #7a9b6f;
      color: white;
      border-color: #5d7a52;
    }

    .hidden {
      display: none !important;
    }

    .leaderboard-table {
      width: 100%;
      border-collapse: collapse;
      margin: 20px 0;
    }

    .leaderboard-table th {
      background: #8b7355;
      color: white;
      padding: 12px;
      text-align: left;
      font-weight: 600;
    }

    .leaderboard-table td {
      padding: 10px 12px;
      border-bottom: 1px solid #c4b5a0;
    }

    .leaderboard-table tr:nth-child(even) {
      background: #f9f6f0;
    }

    .leaderboard-table tr:hover {
      background: #f0e8d8;
    }

    .modal-backdrop {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0,0,0,0.6);
      justify-content: center;
      align-items: center;
      z-index: 1000;
    }

    .modal-backdrop.show {
      display: flex;
    }

    .modal {
      background: #f5ede0;
      border-radius: 20px;
      padding: 30px;
      max-width: 500px;
      width: 90%;
      box-shadow: 0 12px 40px rgba(0,0,0,0.3);
    }

    .modal h2 {
      color: #5c4a3a;
      margin-top: 0;
    }

    .timer-display {
      font-size: 2rem;
      font-weight: bold;
      color: #5c4a3a;
    }

    .timer-display.warning {
      color: #c47a6f;
      animation: pulse 1s infinite;
    }

    @keyframes pulse {
      0%, 100% { opacity: 1; }
      50% { opacity: 0.6; }
    }

    .back-btn {
      position: fixed;
      top: 20px;
      left: 20px;
      background: rgba(139, 115, 85, 0.9);
      color: white;
      border: none;
      border-radius: 50%;
      width: 50px;
      height: 50px;
      font-size: 1.5rem;
      cursor: pointer;
      box-shadow: 0 4px 12px rgba(0,0,0,0.2);
      transition: all 0.3s;
      z-index: 100;
    }

    .back-btn:hover {
      background: rgba(109, 90, 69, 0.9);
      transform: scale(1.1);
    }

    @media (max-width: 768px) {
      h1 {
        font-size: 1.8rem;
      }

      .btn {
        padding: 12px 20px;
        font-size: 1rem;
      }

      .controls {
        flex-direction: column;
      }

      .info-bar {
        flex-direction: column;
        gap: 10px;
        text-align: center;
      }

      .choices-grid {
        grid-template-columns: 1fr 1fr;
      }
    }
  </style>
  <style>@view-transition { navigation: auto; }</style>
  <script src="https://cdn.tailwindcss.com" type="text/javascript"></script>
 </head>
 <body>
  <div class="app-container"><!-- Landing Page -->
   <div id="landingPage" class="card">
    <h1 id="appTitle">Kimi-wa-Melody</h1>
    <div class="mascot-tag" id="mascotTag">
     🐱 MelodyCat 🎵
    </div>
    <div class="form-group"><label for="studentName">Name (or Group Name)</label> <input type="text" id="studentName" placeholder="Enter your name" required>
    </div>
    <div class="form-group"><label for="studentNo">Student Number</label> <input type="text" id="studentNo" placeholder="Enter student number" required>
    </div>
    <div class="form-group"><label for="studentClass">Class</label> <input type="text" id="studentClass" placeholder="Enter class" required>
    </div>
    <div class="form-group"><label for="gameMode">Select Mode</label> <select id="gameMode"> <option value="practice">Practice Mode</option> <option value="time_challenge">Time Challenge Mode (60 seconds)</option> </select>
    </div>
    <div class="controls"><button class="btn btn-primary" onclick="startGame()">Start Game</button> <button class="btn btn-info" onclick="showLeaderboard()">View Leaderboard</button> <button class="btn btn-warning" onclick="showExportModal()">Export Data (Teacher)</button>
    </div>
   </div><!-- Level Selection Page -->
   <div id="levelPage" class="card hidden"><button class="back-btn" onclick="backToLanding()">←</button>
    <h1>Select Level</h1>
    <p style="text-align: center; color: #5c4a3a; font-size: 1.1rem;" id="instructionText">Listen to the notes and choose the correct answer</p>
    <div class="level-select" id="levelSelect"></div>
   </div><!-- Game Page -->
   <div id="gamePage" class="card hidden"><button class="back-btn" onclick="backToLevelSelect()">←</button>
    <div class="info-bar">
     <div>
      <span id="levelDisplay">Level 1</span>
     </div>
     <div>
      <span id="questionDisplay">Question 1/10</span>
     </div>
     <div>
      <span id="scoreDisplay">Score: 0/0</span>
     </div>
     <div id="timerContainer" class="hidden"><span class="timer-display" id="timerDisplay">60</span>
     </div>
    </div>
    <div class="staff-container">
     <svg id="musicStaff" viewbox="0 0 900 250" xmlns="http://www.w3.org/2000/svg"><!-- Staff and notes will be drawn here -->
     </svg>
    </div>
    <div class="controls"><button class="btn btn-info" onclick="playQuestion()" id="playBtn">🔊 ฟัง</button> <button class="btn btn-warning" onclick="showAnswer()" id="answerBtn">👁️ ดูคำตอบ</button> <button class="btn btn-success hidden" onclick="nextQuestion()" id="nextBtn">➡️ ต่อไป</button>
    </div>
    <div id="feedback" class="feedback"></div>
    <div id="choicesContainer" class="choices-grid"></div>
    <div class="controls"><button class="btn btn-primary" onclick="saveScore()" id="saveScoreBtn">💾 บันทึกคะแนน</button>
    </div>
   </div><!-- Leaderboard Page -->
   <div id="leaderboardPage" class="card hidden"><button class="back-btn" onclick="backToLanding()">←</button>
    <h1>🏆 Time Challenge Leaderboard</h1>
    <table class="leaderboard-table">
     <thead>
      <tr>
       <th>Rank</th>
       <th>Name</th>
       <th>Class</th>
       <th>Number</th>
       <th>Score</th>
       <th>Date</th>
      </tr>
     </thead>
     <tbody id="leaderboardBody"></tbody>
    </table>
    <div class="controls"><button class="btn btn-secondary" onclick="backToLanding()">Back</button>
    </div>
   </div>
  </div><!-- PIN Modal -->
  <div id="pinModal" class="modal-backdrop">
   <div class="modal">
    <h2>🔒 กรอกรหัส PIN ครู</h2>
    <div class="form-group"><label for="pinInput">รหัส PIN</label> <input type="password" id="pinInput" placeholder="กรอกรหัส PIN">
    </div>
    <div class="controls"><button class="btn btn-primary" onclick="verifyPIN()">ยืนยัน</button> <button class="btn btn-secondary" onclick="closePINModal()">ยกเลิก</button>
    </div>
    <div id="pinError" style="color: #c47a6f; text-align: center; margin-top: 10px; display: none;">
     รหัส PIN ไม่ถูกต้อง
    </div>
   </div>
  </div>
  <script>
    // ========== Configuration ==========
    const defaultConfig = {
      app_title: "Kimi-wa-Melody",
      mascot_name: "MelodyCat",
      teacher_pin: "Teacherversion5791",
      instruction_text: "Listen to the notes and choose the correct answer"
    };

    // ========== Note Configuration ==========
    const NOTES = ['C', 'D', 'E', 'F', 'G', 'A', 'B'];
    const NOTE_NAMES_TH = {
      'C': 'Do', 'D': 'Re', 'E': 'Mi', 'F': 'Fa',
      'G': 'Sol', 'A': 'La', 'B': 'Ti'
    };

    const NOTE_FREQUENCIES = {
      'C': 261.63, 'D': 293.66, 'E': 329.63, 'F': 349.23,
      'G': 392.00, 'A': 440.00, 'B': 493.88
    };

    // Staff positions (y-coordinate) - Treble Clef Standard
    const NOTE_POSITIONS = {
      'C': 190, // Middle C - Below staff with leger line
      'D': 180, // Below line 1 (space below staff)
      'E': 170, // On line 1 (bottom staff line)
      'F': 160, // Space between line 1 and 2
      'G': 150, // On line 2
      'A': 140, // Space between line 2 and 3
      'B': 130  // On line 3 (middle line)
    };

    // Staff configuration
    const STAFF_CONFIG = {
      left: 300,
      right: 600,
      bottomY: 170,
      gap: 20,
      strokeWidth: 3
    };

    // Note rendering
    const NOTE_CONFIG = {
      startX: 380,
      stepX: 48,
      headRx: 16,
      headRy: 12,
      stemWidth: 3.8,
      stemHeight: 60
    };

    // ========== Game State ==========
    let currentStudent = null;
    let currentMode = 'practice';
    let currentLevel = 1;
    let currentQuestion = 1;
    let currentScore = 0;
    let totalAnswered = 0;
    let currentSequence = [];
    let currentChoices = [];
    let answered = false;
    let audioContext = null;
    let timerInterval = null;
    let timeRemaining = 60;
    let dataSdkReady = false;

    // ========== Audio Context ==========
    function initAudio() {
      if (!audioContext) {
        audioContext = new (window.AudioContext || window.webkitAudioContext)();
      }
    }

    function playTone(frequency, duration = 0.5) {
      initAudio();
      const oscillator = audioContext.createOscillator();
      const gainNode = audioContext.createGain();
      
      oscillator.connect(gainNode);
      gainNode.connect(audioContext.destination);
      
      oscillator.frequency.value = frequency;
      oscillator.type = 'sine';
      
      gainNode.gain.setValueAtTime(0.3, audioContext.currentTime);
      gainNode.gain.exponentialRampToValueAtTime(0.01, audioContext.currentTime + duration);
      
      oscillator.start(audioContext.currentTime);
      oscillator.stop(audioContext.currentTime + duration);
    }

    function playSequence(frequencies) {
      let delay = 0;
      frequencies.forEach(freq => {
        setTimeout(() => playTone(freq, 0.5), delay);
        delay += 600;
      });
    }

    function playCorrect() {
      playSequence([523.25, 659.25, 783.99]);
    }

    function playWrong() {
      playSequence([392, 349.23, 329.63]);
    }

    // ========== SVG Drawing Functions ==========
    function drawNote(note, index) {
      const svg = document.getElementById('musicStaff');
      const x = NOTE_CONFIG.startX + (index * NOTE_CONFIG.stepX);
      const y = NOTE_POSITIONS[note];
      
      // Draw leger line for Middle C (note C below the staff)
      if (note === 'C') {
        const legerLine = document.createElementNS('http://www.w3.org/2000/svg', 'line');
        legerLine.setAttribute('x1', x - 24);
        legerLine.setAttribute('y1', y);
        legerLine.setAttribute('x2', x + 24);
        legerLine.setAttribute('y2', y);
        legerLine.setAttribute('stroke', '#5c4a3a');
        legerLine.setAttribute('stroke-width', STAFF_CONFIG.strokeWidth);
        legerLine.setAttribute('stroke-linecap', 'round');
        svg.appendChild(legerLine);
      }
      
      // Draw note head (ellipse)
      const noteHead = document.createElementNS('http://www.w3.org/2000/svg', 'ellipse');
      noteHead.setAttribute('cx', x);
      noteHead.setAttribute('cy', y);
      noteHead.setAttribute('rx', NOTE_CONFIG.headRx);
      noteHead.setAttribute('ry', NOTE_CONFIG.headRy);
      noteHead.setAttribute('fill', '#5c4a3a');
      noteHead.setAttribute('transform', `rotate(-12 ${x} ${y})`);
      svg.appendChild(noteHead);
      
      // Draw stem
      const stem = document.createElementNS('http://www.w3.org/2000/svg', 'rect');
      stem.setAttribute('x', x + NOTE_CONFIG.headRx - 2);
      stem.setAttribute('y', y - NOTE_CONFIG.stemHeight);
      stem.setAttribute('width', NOTE_CONFIG.stemWidth);
      stem.setAttribute('height', NOTE_CONFIG.stemHeight);
      stem.setAttribute('fill', '#5c4a3a');
      svg.appendChild(stem);
    }

    function drawSequence(sequence) {
      const svg = document.getElementById('musicStaff');
      // Clear everything and redraw from scratch
      svg.innerHTML = '';
      
      // Redraw staff lines
      for (let i = 0; i < 5; i++) {
        const y = STAFF_CONFIG.bottomY - (i * STAFF_CONFIG.gap);
        const line = document.createElementNS('http://www.w3.org/2000/svg', 'line');
        line.setAttribute('x1', STAFF_CONFIG.left);
        line.setAttribute('y1', y);
        line.setAttribute('x2', STAFF_CONFIG.right);
        line.setAttribute('y2', y);
        line.setAttribute('stroke', '#5c4a3a');
        line.setAttribute('stroke-width', STAFF_CONFIG.strokeWidth);
        line.setAttribute('stroke-linecap', 'round');
        svg.appendChild(line);
      }
      
      // Redraw clef text
      const clefText = document.createElementNS('http://www.w3.org/2000/svg', 'text');
      clefText.setAttribute('x', '450');
      clefText.setAttribute('y', '30');
      clefText.setAttribute('fill', '#5c4a3a');
      clefText.setAttribute('font-size', '18');
      clefText.setAttribute('font-weight', '600');
      clefText.setAttribute('text-anchor', 'middle');
      clefText.setAttribute('font-family', 'Kanit, Sarabun, Arial, sans-serif');
      clefText.textContent = 'Treble Clef (G Clef)';
      svg.appendChild(clefText);
      
      // Draw new notes
      sequence.forEach((note, index) => {
        drawNote(note, index);
      });
    }

    // ========== Game Logic ==========
    function getNotesPerQuestion(level) {
      if (level <= 7) return 1;
      if (level <= 14) return 2;
      return 3;
    }

    function generateRandomSequence(length) {
      const sequence = [];
      for (let i = 0; i < length; i++) {
        sequence.push(NOTES[Math.floor(Math.random() * NOTES.length)]);
      }
      return sequence;
    }

    function seqToLabel(seq) {
      return seq.map(note => `${note}(${NOTE_NAMES_TH[note]})`).join(' ');
    }

    function generateChoices(correctSeq) {
      const notesPerQ = correctSeq.length;
      
      if (notesPerQ === 1) {
        // Show all 7 notes
        const choices = NOTES.map(note => [note]);
        return shuffleArray(choices);
      } else {
        // Generate 4 choices including correct answer
        const choices = [correctSeq];
        const seqStrings = new Set([JSON.stringify(correctSeq)]);
        
        while (choices.length < 4) {
          const randomSeq = generateRandomSequence(notesPerQ);
          const seqStr = JSON.stringify(randomSeq);
          if (!seqStrings.has(seqStr)) {
            choices.push(randomSeq);
            seqStrings.add(seqStr);
          }
        }
        
        return shuffleArray(choices);
      }
    }

    function shuffleArray(array) {
      const newArray = [...array];
      for (let i = newArray.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [newArray[i], newArray[j]] = [newArray[j], newArray[i]];
      }
      return newArray;
    }

    function generateQuestion() {
      const notesPerQ = getNotesPerQuestion(currentLevel);
      currentSequence = generateRandomSequence(notesPerQ);
      currentChoices = generateChoices(currentSequence);
      answered = false;
      
      drawSequence(currentSequence);
      renderChoices();
      
      document.getElementById('questionDisplay').textContent = `Question ${currentQuestion}/10`;
      document.getElementById('answerBtn').disabled = false;
      document.getElementById('nextBtn').classList.add('hidden');
      document.getElementById('feedback').classList.remove('show');
    }

    function renderChoices() {
      const container = document.getElementById('choicesContainer');
      container.innerHTML = '';
      
      currentChoices.forEach(choice => {
        const btn = document.createElement('button');
        btn.className = 'choice-btn';
        btn.textContent = seqToLabel(choice);
        btn.onclick = () => checkAnswer(choice, btn);
        container.appendChild(btn);
      });
    }

    function playQuestion() {
      const frequencies = currentSequence.map(note => NOTE_FREQUENCIES[note]);
      playSequence(frequencies);
    }

    function showAnswer() {
      if (answered) return;
      
      const feedback = document.getElementById('feedback');
      feedback.textContent = `Correct Answer: ${seqToLabel(currentSequence)}`;
      feedback.className = 'feedback show incorrect';
      
      document.getElementById('answerBtn').disabled = true;
      document.getElementById('nextBtn').classList.remove('hidden');
      
      // Disable all choice buttons
      document.querySelectorAll('.choice-btn').forEach(btn => {
        btn.disabled = true;
        if (btn.textContent === seqToLabel(currentSequence)) {
          btn.classList.add('correct');
        }
      });
      
      answered = true;
      totalAnswered++;
      updateScore();
    }

    function checkAnswer(selectedSeq, btn) {
      if (answered) return;
      
      answered = true;
      totalAnswered++;
      
      const isCorrect = JSON.stringify(selectedSeq) === JSON.stringify(currentSequence);
      const feedback = document.getElementById('feedback');
      
      if (isCorrect) {
        currentScore++;
        btn.classList.add('correct');
        feedback.textContent = '✅ Correct!';
        feedback.className = 'feedback show correct';
        playCorrect();
      } else {
        btn.classList.add('incorrect');
        feedback.textContent = `❌ ผิด! คำตอบที่ถูกต้องคือ: ${seqToLabel(currentSequence)}`;
        feedback.className = 'feedback show incorrect';
        playWrong();
        
        // Highlight correct answer
        document.querySelectorAll('.choice-btn').forEach(choiceBtn => {
          if (choiceBtn.textContent === seqToLabel(currentSequence)) {
            choiceBtn.classList.add('correct');
          }
        });
      }
      
      updateScore();
      document.getElementById('answerBtn').disabled = true;
      document.getElementById('nextBtn').classList.remove('hidden');
      
      // Disable all choice buttons
      document.querySelectorAll('.choice-btn').forEach(choiceBtn => {
        choiceBtn.disabled = true;
      });
    }

    function updateScore() {
      document.getElementById('scoreDisplay').textContent = `Score: ${currentScore}/${totalAnswered}`;
    }

    function nextQuestion() {
      if (currentMode === 'time_challenge') {
        // Time challenge mode - continuous play
        currentQuestion++;
        generateQuestion();
        playQuestion();
      } else {
        // Practice mode
        if (currentQuestion >= 10) {
          endLevel();
        } else {
          currentQuestion++;
          generateQuestion();
        }
      }
    }

    function endLevel() {
      const feedback = document.getElementById('feedback');
      feedback.textContent = `Level ${currentLevel} Complete! Score: ${currentScore}/${totalAnswered}`;
      feedback.className = 'feedback show correct';
      
      document.getElementById('nextBtn').classList.add('hidden');
      document.getElementById('choicesContainer').innerHTML = '';
      
      // Mark level as completed
      updateLevelCompletion(currentLevel);
    }

    function updateLevelCompletion(level) {
      const completed = JSON.parse(localStorage.getItem('kimi_completed_levels') || '[]');
      if (!completed.includes(level)) {
        completed.push(level);
        localStorage.setItem('kimi_completed_levels', JSON.stringify(completed));
      }
    }

    // ========== Timer Functions ==========
    function startTimer() {
      timeRemaining = 60;
      document.getElementById('timerContainer').classList.remove('hidden');
      updateTimerDisplay();
      
      timerInterval = setInterval(() => {
        timeRemaining--;
        updateTimerDisplay();
        
        if (timeRemaining <= 10) {
          document.getElementById('timerDisplay').classList.add('warning');
        }
        
        if (timeRemaining <= 0) {
          endTimeChallenge();
        }
      }, 1000);
    }

    function updateTimerDisplay() {
      document.getElementById('timerDisplay').textContent = timeRemaining;
    }

    function stopTimer() {
      if (timerInterval) {
        clearInterval(timerInterval);
        timerInterval = null;
      }
    }

    function endTimeChallenge() {
      stopTimer();
      
      const feedback = document.getElementById('feedback');
      feedback.textContent = `⏰ Time's Up! Your Score: ${currentScore}/${totalAnswered}`;
      feedback.className = 'feedback show correct';
      
      document.getElementById('nextBtn').classList.add('hidden');
      document.getElementById('choicesContainer').innerHTML = '';
      document.querySelectorAll('.choice-btn').forEach(btn => btn.disabled = true);
      
      // Save to leaderboard
      saveToLeaderboard();
    }

    function saveToLeaderboard() {
      const leaderboard = JSON.parse(localStorage.getItem('kimi_time_leaderboard') || '[]');
      
      leaderboard.push({
        name: currentStudent.name,
        class: currentStudent.class,
        no: currentStudent.no,
        score: currentScore,
        total: totalAnswered,
        date: new Date().toLocaleDateString('th-TH')
      });
      
      // Sort by score (descending) and keep top 50
      leaderboard.sort((a, b) => {
        const scoreA = a.total > 0 ? (a.score / a.total) : 0;
        const scoreB = b.total > 0 ? (b.score / b.total) : 0;
        if (scoreB !== scoreA) return scoreB - scoreA;
        return b.score - a.score;
      });
      
      localStorage.setItem('kimi_time_leaderboard', JSON.stringify(leaderboard.slice(0, 50)));
    }

    // ========== Feedback Helper ==========
    function showFeedbackMessage(message, isSuccess) {
      const feedback = document.createElement('div');
      feedback.className = `feedback show ${isSuccess ? 'correct' : 'incorrect'}`;
      feedback.textContent = message;
      
      const gamePage = document.getElementById('gamePage');
      const choicesContainer = document.getElementById('choicesContainer');
      gamePage.insertBefore(feedback, choicesContainer);
      
      setTimeout(() => feedback.remove(), 3000);
    }

    // ========== Navigation Functions ==========
    function startGame() {
      const name = document.getElementById('studentName').value.trim();
      const no = document.getElementById('studentNo').value.trim();
      const classRoom = document.getElementById('studentClass').value.trim();
      const mode = document.getElementById('gameMode').value;
      
      if (!name || !no || !classRoom) {
        const msg = document.createElement('div');
        msg.className = 'feedback show incorrect';
        msg.textContent = 'Please fill in all fields';
        document.getElementById('landingPage').appendChild(msg);
        setTimeout(() => msg.remove(), 3000);
        return;
      }
      
      currentStudent = { name, no, class: classRoom };
      currentMode = mode;
      localStorage.setItem('kimi_student', JSON.stringify(currentStudent));
      
      if (mode === 'time_challenge') {
        // Go directly to game
        currentLevel = 1;
        currentQuestion = 1;
        currentScore = 0;
        totalAnswered = 0;
        
        document.getElementById('landingPage').classList.add('hidden');
        document.getElementById('gamePage').classList.remove('hidden');
        document.getElementById('levelDisplay').textContent = 'Time Challenge';
        
        drawSequence([]);
        generateQuestion();
        startTimer();
        playQuestion();
      } else {
        // Show level selection
        document.getElementById('landingPage').classList.add('hidden');
        document.getElementById('levelPage').classList.remove('hidden');
        renderLevelSelect();
      }
    }

    function renderLevelSelect() {
      const container = document.getElementById('levelSelect');
      container.innerHTML = '';
      
      const completed = JSON.parse(localStorage.getItem('kimi_completed_levels') || '[]');
      
      for (let i = 1; i <= 20; i++) {
        const btn = document.createElement('button');
        btn.className = 'level-btn';
        if (completed.includes(i)) {
          btn.classList.add('completed');
        }
        btn.textContent = `Level ${i}`;
        btn.onclick = () => startLevel(i);
        container.appendChild(btn);
      }
    }

    function startLevel(level) {
      currentLevel = level;
      currentQuestion = 1;
      currentScore = 0;
      totalAnswered = 0;
      
      document.getElementById('levelPage').classList.add('hidden');
      document.getElementById('gamePage').classList.remove('hidden');
      document.getElementById('levelDisplay').textContent = `Level ${level}`;
      document.getElementById('timerContainer').classList.add('hidden');
      
      drawSequence([]);
      generateQuestion();
    }

    function backToLanding() {
      stopTimer();
      document.getElementById('levelPage').classList.add('hidden');
      document.getElementById('gamePage').classList.add('hidden');
      document.getElementById('leaderboardPage').classList.add('hidden');
      document.getElementById('landingPage').classList.remove('hidden');
    }

    function backToLevelSelect() {
      stopTimer();
      document.getElementById('gamePage').classList.add('hidden');
      document.getElementById('levelPage').classList.remove('hidden');
      renderLevelSelect();
    }

    function showLeaderboard() {
      document.getElementById('landingPage').classList.add('hidden');
      document.getElementById('leaderboardPage').classList.remove('hidden');
      
      const leaderboard = JSON.parse(localStorage.getItem('kimi_time_leaderboard') || '[]');
      const tbody = document.getElementById('leaderboardBody');
      tbody.innerHTML = '';
      
      if (leaderboard.length === 0) {
        const row = tbody.insertRow();
        const cell = row.insertCell();
        cell.colSpan = 6;
        cell.textContent = 'No scores yet';
        cell.style.textAlign = 'center';
        cell.style.color = '#8b7355';
        return;
      }
      
      leaderboard.slice(0, 10).forEach((entry, index) => {
        const row = tbody.insertRow();
        row.insertCell().textContent = index + 1;
        row.insertCell().textContent = entry.name;
        row.insertCell().textContent = entry.class;
        row.insertCell().textContent = entry.no;
        row.insertCell().textContent = `${entry.score}/${entry.total}`;
        row.insertCell().textContent = entry.date;
      });
    }

    // ========== Data Persistence ==========
async function saveScore() {
  // If student data missing -> warn
  if (!currentStudent) {
    showFeedbackMessage('Student information not found', false);
    return;
  }

  const saveBtn = document.getElementById('saveScoreBtn');
  saveBtn.disabled = true;
  const origText = saveBtn.textContent;
  saveBtn.textContent = '⏳ Saving...';

  // Build record
  const record = {
    student_name: currentStudent.name,
    class_room: currentStudent.class,
    student_no: currentStudent.no,
    mode: currentMode,
    level: currentLevel,
    score: currentScore,
    total: totalAnswered,
    timestamp: new Date().toISOString()
  };

  try {
    // Prefer server Data SDK if available & ready
    if (window.dataSdk && typeof window.dataSdk.create === 'function' && (typeof dataSdkReady === 'undefined' || dataSdkReady)) {
      const result = await window.dataSdk.create(record);
      if (result && result.isOk) {
        showFeedbackMessage('✅ Score saved successfully!', true);
        // also append to local export store for safety
        const store = JSON.parse(localStorage.getItem('kimi_records_all') || '[]');
        store.push(record);
        localStorage.setItem('kimi_records_all', JSON.stringify(store));
      } else {
        // If Data SDK returned an error, fallback to local store
        const errMsg = (result && result.error && result.error.message) ? result.error.message : 'Unable to save to server';
        console.warn('Data SDK error, falling back to local store:', errMsg);
        const store = JSON.parse(localStorage.getItem('kimi_records_all') || '[]');
        store.push(record);
        localStorage.setItem('kimi_records_all', JSON.stringify(store));
        showFeedbackMessage('⚠️ Saved locally (server failed).', false);
      }
    } else {
      // No Data SDK or not ready -> save locally
      const store = JSON.parse(localStorage.getItem('kimi_records_all') || '[]');
      store.push(record);
      localStorage.setItem('kimi_records_all', JSON.stringify(store));
      showFeedbackMessage('✅ Score saved locally!', true);
    }
  } catch (err) {
    console.error('saveScore error:', err);
    // Ensure local fallback
    try {
      const store = JSON.parse(localStorage.getItem('kimi_records_all') || '[]');
      store.push(record);
      localStorage.setItem('kimi_records_all', JSON.stringify(store));
      showFeedbackMessage('⚠️ Error saving to server — saved locally.', false);
    } catch (e) {
      showFeedbackMessage('❌ Failed to save score.', false);
    }
  } finally {
    saveBtn.disabled = false;
    saveBtn.textContent = origText;
  }
}

    // ========== Export Functions ==========
    function showExportModal() {
      document.getElementById('pinModal').classList.add('show');
      document.getElementById('pinInput').value = '';
      document.getElementById('pinError').style.display = 'none';
    }

    function closePINModal() {
      document.getElementById('pinModal').classList.remove('show');
    }

    function verifyPIN() {
      const config = window.elementSdk?.config || defaultConfig;
      const enteredPIN = document.getElementById('pinInput').value;
      const correctPIN = config.teacher_pin || defaultConfig.teacher_pin;
      
      if (enteredPIN === correctPIN) {
        closePINModal();
        exportToCSV();
      } else {
        document.getElementById('pinError').style.display = 'block';
      }
    }

    function exportToCSV() {
  // Prefer records from window.kimiRecords (Data SDK) then local storage
  let records = window.kimiRecords;
  if (!records || !Array.isArray(records) || records.length === 0) {
    // fallback to local store
    records = JSON.parse(localStorage.getItem('kimi_records_all') || '[]');
  }
  if (!records || records.length === 0) {
    const msg = document.createElement('div');
    msg.className = 'feedback show incorrect';
    msg.textContent = 'No data to export';
    document.getElementById('landingPage').appendChild(msg);
    setTimeout(() => msg.remove(), 3000);
    return;
  }

  // Build CSV (escape quotes)
  let csv = 'Name,Class,Number,Mode,Level,Score,Total,Date\n';
  records.forEach(record => {
    const date = record.timestamp ? new Date(record.timestamp).toLocaleString('en-US') : '';
    const name = (record.student_name || '').replace(/"/g, '""');
    const classRoom = (record.class_room || '').replace(/"/g, '""');
    const studentNo = (record.student_no || '').replace(/"/g, '""');
    const mode = (record.mode || '').replace(/"/g, '""');
    csv += `"${name}","${classRoom}","${studentNo}","${mode}",${record.level || ''},${record.score || 0},${record.total || 0},"${date}"\n`;
  });

  // Add BOM for Excel UTF-8 compatibility
  const BOM = '\uFEFF';
  const blob = new Blob([BOM + csv], { type: 'text/csv;charset=utf-8;' });

  // Create download link and click it in a user-gesture-safe way
  const url = URL.createObjectURL(blob);
  const link = document.createElement('a');
  link.href = url;
  link.download = `kimi-melody-records-${new Date().toISOString().split('T')[0]}.csv`;
  // ensure it's not visible and added to DOM
  link.style.display = 'none';
  document.body.appendChild(link);

  // Try to trigger click; use MouseEvent for compatibility
  try {
    const evt = new MouseEvent('click', { view: window, bubbles: true, cancelable: true });
    link.dispatchEvent(evt);
  } catch (e) {
    // fallback
    link.click();
  }

  // cleanup after a short delay to ensure download started
  setTimeout(() => {
    document.body.removeChild(link);
    URL.revokeObjectURL(url);
  }, 500);

  // show success message in UI
  const msg = document.createElement('div');
  msg.className = 'feedback show correct';
  msg.textContent = '✅ Data exported successfully!';
  document.getElementById('landingPage').appendChild(msg);
  setTimeout(() => msg.remove(), 3000);
}

    // ========== Data SDK Integration ==========
    const dataHandler = {
      onDataChanged(data) {
        window.kimiRecords = data;
      }
    };

    // ========== Element SDK Integration ==========
    async function onConfigChange(config) {
      const appTitle = config.app_title || defaultConfig.app_title;
      const mascotName = config.mascot_name || defaultConfig.mascot_name;
      const instructionText = config.instruction_text || defaultConfig.instruction_text;

      document.getElementById('appTitle').textContent = appTitle;
      document.getElementById('mascotTag').textContent = `🐱 ${mascotName} 🎵`;
      document.getElementById('instructionText').textContent = instructionText;
    }

    // ========== Initialization ==========
    async function init() {
      // Initialize Element SDK
      if (window.elementSdk) {
        await window.elementSdk.init({
          defaultConfig,
          onConfigChange,
          mapToCapabilities: (config) => ({
            recolorables: [],
            borderables: [],
            fontEditable: undefined,
            fontSizeable: undefined
          }),
          mapToEditPanelValues: (config) => new Map([
            ['app_title', config.app_title || defaultConfig.app_title],
            ['mascot_name', config.mascot_name || defaultConfig.mascot_name],
            ['teacher_pin', config.teacher_pin || defaultConfig.teacher_pin],
            ['instruction_text', config.instruction_text || defaultConfig.instruction_text]
          ])
        });

        await onConfigChange(window.elementSdk.config);
      }

      // Initialize Data SDK
      if (window.dataSdk) {
        const result = await window.dataSdk.init(dataHandler);
        if (result.isOk) {
          dataSdkReady = true;
        } else {
          console.error('Failed to initialize Data SDK:', result.error);
        }
      }

      // Load saved student data
      const savedStudent = localStorage.getItem('kimi_student');
      if (savedStudent) {
        const student = JSON.parse(savedStudent);
        document.getElementById('studentName').value = student.name;
        document.getElementById('studentNo').value = student.no;
        document.getElementById('studentClass').value = student.class;
      }
    }

    // Start initialization
    init();
  </script>
 <script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'9a526d1f2035d02f',t:'MTc2NDI1NDkwNC4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>

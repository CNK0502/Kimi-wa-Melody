<html....>
<html lang="en">
 <head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Kimi-wa-Melody - MelodyCat</title>
  <script src="/_sdk/data_sdk.js"></script>
  <script src="/_sdk/element_sdk.js"></script>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Niconne&family=Montserrat:wght@300;400;600;700&display=swap');

    body {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: 'Montserrat', sans-serif;
      background: linear-gradient(135deg, #ffc9d9 0%, #ffe5b8 35%, #fff9cc 50%, #e8f5d8 70%, #c8f0d8 100%);
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
      background: linear-gradient(135deg, #ffffff 0%, #fffbfc 100%);
      border-radius: 20px;
      box-shadow: 0 8px 24px rgba(201, 124, 157, 0.2);
      border: 2px solid #e8d5dd;
      padding: 30px;
      margin: 15px 0;
      width: 100%;
      max-width: 1000px;
    }

    .landing-container {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 30px;
      margin-top: 20px;
    }

    .landing-left, .landing-right {
      display: flex;
      flex-direction: column;
    }

    .mode-grid {
      display: flex;
      flex-direction: column;
      gap: 15px;
    }

    .mode-card {
      background: white;
      border: 2px solid #e8d5dd;
      border-radius: 15px;
      padding: 20px;
      cursor: pointer;
      transition: all 0.3s;
      text-align: center;
      font-family: inherit;
    }

    .mode-card:hover {
      background: #fef8fa;
      border-color: #c97c9d;
      transform: translateX(5px);
      box-shadow: 0 4px 12px rgba(201, 124, 157, 0.3);
    }

    .mode-card.selected {
      background: linear-gradient(135deg, #d4a5b8 0%, #c97c9d 100%);
      border-color: #c97c9d;
      color: white;
    }

    .mode-card.selected .mode-icon {
      transform: scale(1.2);
    }

    .mode-icon {
      font-size: 2.5rem;
      margin-bottom: 10px;
      transition: transform 0.3s;
    }

    .mode-title {
      font-size: 1.2rem;
      font-weight: 700;
      margin-bottom: 5px;
    }

    .mode-desc {
      font-size: 0.9rem;
      opacity: 0.8;
    }

    .mode-card.selected .mode-desc {
      opacity: 0.95;
    }

    h1 {
      color: #c97c9d;
      text-align: center;
      font-size: 10rem;
      margin: 0 0 10px 0;
      font-family: 'Niconne', cursive;
      font-weight: 400;
      text-shadow: 2px 2px 8px rgba(201, 124, 157, 0.3);
      line-height: 1.2;
    }
    
    #landingPage h1 {
      font-size: 3rem;
    }

    h2 {
      color: #c97c9d;
      font-size: 1.5rem;
      margin: 0 0 15px 0;
      font-weight: 600;
    }

    .mascot-tag {
      text-align: center;
      color: #b08ba4;
      font-size: 1.1rem;
      margin-bottom: 20px;
      font-weight: 300;
    }

    .form-group {
      margin: 15px 0;
    }

    label {
      display: block;
      color: #b08ba4;
      font-weight: 600;
      margin-bottom: 8px;
      font-size: 0.95rem;
    }

    input, select {
      width: 100%;
      padding: 12px 15px;
      border: 2px solid #e8d5dd;
      border-radius: 10px;
      font-size: 1rem;
      background: white;
      transition: all 0.3s;
      font-family: 'Montserrat', sans-serif;
    }

    input:focus, select:focus {
      outline: none;
      border-color: #c97c9d;
      box-shadow: 0 0 0 3px rgba(201, 124, 157, 0.1);
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
      background: linear-gradient(135deg, #d4a5b8 0%, #c97c9d 100%);
      color: white;
    }

    .btn-success {
      background: linear-gradient(135deg, #a8d5a3 0%, #8bc985 100%);
      color: white;
    }

    .btn-info {
      background: linear-gradient(135deg, #c5a3d8 0%, #b08bc4 100%);
      color: white;
    }

    .btn-warning {
      background: linear-gradient(135deg, #f5c89a 0%, #f0b880 100%);
      color: white;
    }

    .btn-secondary {
      background: linear-gradient(135deg, #d4a5b8 0%, #c97c9d 100%);
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
      background: linear-gradient(135deg, #d4a5b8 0%, #c97c9d 100%);
      color: white;
      padding: 15px 25px;
      border-radius: 12px;
      font-size: 1.2rem;
      font-weight: 400;
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
      border: 2px solid #e8d5dd;
      border-radius: 12px;
      font-size: 1.3rem;
      font-weight: 400;
      color: #b08ba4;
      cursor: pointer;
      transition: all 0.3s;
    }

    .choice-btn:hover {
      background: #fef8fa;
      border-color: #c97c9d;
      transform: scale(1.05);
    }

    .choice-btn.correct {
      background: #a8d5a3;
      color: white;
      border-color: #8bc985;
    }

    .choice-btn.incorrect {
      background: #f5b3b3;
      color: white;
      border-color: #f09d9d;
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
      background: #f0f9ef;
      color: #6fa869;
      border: 2px solid #a8d5a3;
    }

    .feedback.incorrect {
      background: #fef5f5;
      color: #d88888;
      border: 2px solid #f5b3b3;
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
      border: 2px solid #e8d5dd;
      border-radius: 10px;
      font-size: 1rem;
      font-weight: 400;
      color: #b08ba4;
      cursor: pointer;
      transition: all 0.3s;
    }

    .level-btn:hover {
      background: #fef8fa;
      transform: scale(1.05);
    }

    .level-btn.completed {
      background: #a8d5a3;
      color: white;
      border-color: #8bc985;
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
      background: #d4a5b8;
      color: white;
      padding: 12px;
      text-align: center;
      font-weight: 600;
    }

    .leaderboard-table td {
      padding: 10px 12px;
      border-bottom: 1px solid #e8d5dd;
      text-align: center;
    }

    .leaderboard-table tr:nth-child(even) {
      background: #fffbfc;
    }

    .leaderboard-table tr:hover {
      background: #fef8fa;
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
      background: linear-gradient(135deg, #ffffff 0%, #fffbfc 100%);
      border-radius: 20px;
      border: 2px solid #e8d5dd;
      padding: 30px;
      max-width: 500px;
      width: 90%;
      box-shadow: 0 12px 40px rgba(201, 124, 157, 0.3);
    }

    .modal h2 {
      color: #c97c9d;
      margin-top: 0;
    }

    .timer-display {
      font-size: 2rem;
      font-weight: 700;
      color: #ffffff;
      background: linear-gradient(135deg, #c97c9d 0%, #b06888 100%);
      padding: 8px 20px;
      border-radius: 10px;
      box-shadow: 0 4px 12px rgba(201, 124, 157, 0.4);
    }

    .timer-display.warning {
      background: linear-gradient(135deg, #f44336 0%, #d32f2f 100%);
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
      background: rgba(212, 165, 184, 0.9);
      color: white;
      border: none;
      border-radius: 50%;
      width: 50px;
      height: 50px;
      font-size: 1.5rem;
      cursor: pointer;
      box-shadow: 0 4px 12px rgba(201, 124, 157, 0.3);
      transition: all 0.3s;
      z-index: 100;
    }

    .back-btn:hover {
      background: rgba(201, 124, 157, 0.9);
      transform: scale(1.1);
    }

    .matching-grid {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 15px;
      margin: 20px 0;
      max-width: 600px;
      margin-left: auto;
      margin-right: auto;
    }

    .matching-card {
      aspect-ratio: 1;
      background: white;
      border: 2px solid #e8d5dd;
      border-radius: 15px;
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 1.5rem;
      font-weight: 400;
      color: #b08ba4;
      transition: all 0.3s;
      position: relative;
      overflow: hidden;
    }

    .matching-card:hover {
      transform: scale(1.05);
      border-color: #c97c9d;
      box-shadow: 0 4px 12px rgba(201, 124, 157, 0.3);
    }

    .matching-card.flipped {
      background: linear-gradient(135deg, #fef8fa 0%, #ffffff 100%);
    }

    .matching-card.matched {
      background: linear-gradient(135deg, #a8d5a3 0%, #8bc985 100%);
      color: white;
      border-color: #8bc985;
      cursor: default;
      pointer-events: none;
    }

    .matching-card.wrong {
      background: linear-gradient(135deg, #f5b3b3 0%, #f09d9d 100%);
      color: white;
      border-color: #f09d9d;
      animation: shake 0.5s;
    }

    .matching-card .card-back {
      position: absolute;
      width: 100%;
      height: 100%;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 2.5rem;
    }

    .matching-card .card-front {
      display: none;
    }

    .matching-card.flipped .card-back {
      display: none;
    }

    .matching-card.flipped .card-front {
      display: flex;
      align-items: center;
      justify-content: center;
      width: 100%;
      height: 100%;
    }

    .matching-card svg {
      max-width: 90%;
      max-height: 90%;
    }

    @keyframes shake {
      0%, 100% { transform: translateX(0); }
      25% { transform: translateX(-10px); }
      75% { transform: translateX(10px); }
    }

    /* Tablet Styles (iPad and similar) */
    @media (max-width: 1024px) {
      .card {
        padding: 25px;
        max-width: 95%;
      }

      #landingPage h1 {
        font-size: 2.5rem;
      }

      h2 {
        font-size: 1.3rem;
      }

      .landing-container {
        gap: 20px;
      }

      .mode-icon {
        font-size: 2.2rem;
      }

      .mode-title {
        font-size: 1.1rem;
      }

      .matching-grid {
        max-width: 500px;
        gap: 12px;
      }

      .staff-container {
        padding: 30px 15px;
      }

      .back-btn {
        width: 45px;
        height: 45px;
        font-size: 1.3rem;
      }
    }

    /* Mobile Landscape and Small Tablets */
    @media (max-width: 768px) {
      .app-container {
        padding: 15px;
      }

      .card {
        padding: 20px;
        margin: 10px 0;
        border-radius: 15px;
      }

      #landingPage h1 {
        font-size: 2rem;
        margin-bottom: 8px;
      }

      h1 {
        font-size: 1.8rem;
      }

      h2 {
        font-size: 1.2rem;
        margin-bottom: 12px;
      }

      .mascot-tag {
        font-size: 1rem;
        margin-bottom: 15px;
      }

      .landing-container {
        grid-template-columns: 1fr;
        gap: 20px;
      }

      .mode-card {
        padding: 15px;
      }

      .mode-icon {
        font-size: 2rem;
        margin-bottom: 8px;
      }

      .mode-title {
        font-size: 1.1rem;
      }

      .mode-desc {
        font-size: 0.85rem;
      }

      .form-group {
        margin: 12px 0;
      }

      label {
        font-size: 0.9rem;
        margin-bottom: 6px;
      }

      input, select {
        padding: 10px 12px;
        font-size: 0.95rem;
      }

      .btn {
        padding: 12px 20px;
        font-size: 1rem;
      }

      .controls {
        gap: 10px;
      }

      .info-bar {
        flex-direction: column;
        gap: 8px;
        text-align: center;
        padding: 12px 20px;
        font-size: 1rem;
      }

      .timer-display {
        font-size: 1.5rem;
      }

      .staff-container {
        padding: 20px 10px;
        margin: 15px 0;
      }

      .choices-grid {
        grid-template-columns: 1fr 1fr;
        gap: 10px;
      }

      .choice-btn {
        padding: 15px 10px;
        font-size: 1.1rem;
      }

      .feedback {
        font-size: 1.1rem;
        padding: 12px;
      }

      .level-select {
        grid-template-columns: repeat(auto-fill, minmax(70px, 1fr));
        gap: 8px;
      }

      .level-btn {
        padding: 12px;
        font-size: 0.9rem;
      }

      .matching-grid {
        grid-template-columns: repeat(4, 1fr);
        gap: 10px;
        max-width: 100%;
      }

      .matching-card {
        font-size: 1.2rem;
      }

      .matching-card .card-back {
        font-size: 2rem;
      }

      .matching-card.flipped .card-front {
        font-size: 0.9rem;
      }

      .leaderboard-table {
        font-size: 0.85rem;
      }

      .leaderboard-table th,
      .leaderboard-table td {
        padding: 8px 6px;
      }

      .modal {
        padding: 25px;
        width: 92%;
      }

      .modal h2 {
        font-size: 1.3rem;
      }

      .back-btn {
        width: 45px;
        height: 45px;
        font-size: 1.3rem;
        top: 15px;
        left: 15px;
      }
    }

    /* Mobile Portrait - Standard Phones */
    @media (max-width: 480px) {
      .app-container {
        padding: 10px;
      }

      .card {
        padding: 15px;
        border-radius: 12px;
      }

      #landingPage h1 {
        font-size: 1.6rem;
        margin-bottom: 5px;
      }

      h1 {
        font-size: 1.5rem;
      }

      h2 {
        font-size: 1.1rem;
        margin-bottom: 10px;
      }

      .mascot-tag {
        font-size: 0.9rem;
        margin-bottom: 12px;
      }

      .landing-container {
        gap: 15px;
        margin-top: 15px;
      }

      .mode-card {
        padding: 12px;
      }

      .mode-icon {
        font-size: 1.8rem;
        margin-bottom: 6px;
      }

      .mode-title {
        font-size: 1rem;
        margin-bottom: 3px;
      }

      .mode-desc {
        font-size: 0.8rem;
      }

      .form-group {
        margin: 10px 0;
      }

      label {
        font-size: 0.85rem;
        margin-bottom: 5px;
      }

      input, select {
        padding: 9px 10px;
        font-size: 0.9rem;
      }

      .btn {
        padding: 10px 16px;
        font-size: 0.95rem;
      }

      .controls {
        gap: 8px;
        margin: 15px 0;
      }

      .info-bar {
        padding: 10px 15px;
        font-size: 0.9rem;
        gap: 6px;
      }

      .timer-display {
        font-size: 1.3rem;
      }

      .staff-container {
        padding: 15px 8px;
        margin: 12px 0;
      }

      .choices-grid {
        grid-template-columns: 1fr;
        gap: 8px;
        margin: 15px 0;
      }

      .choice-btn {
        padding: 12px;
        font-size: 1rem;
      }

      .feedback {
        font-size: 1rem;
        padding: 10px;
        margin: 12px 0;
      }

      .level-select {
        grid-template-columns: repeat(auto-fill, minmax(60px, 1fr));
        gap: 6px;
        margin: 15px 0;
      }

      .level-btn {
        padding: 10px;
        font-size: 0.85rem;
      }

      .matching-grid {
        grid-template-columns: repeat(4, 1fr);
        gap: 6px;
      }

      .matching-card {
        font-size: 1rem;
        border-radius: 10px;
      }

      .matching-card .card-back {
        font-size: 1.5rem;
      }

      .matching-card.flipped .card-front {
        font-size: 0.8rem;
      }

      .leaderboard-table {
        font-size: 0.75rem;
      }

      .leaderboard-table th,
      .leaderboard-table td {
        padding: 6px 4px;
      }

      .modal {
        padding: 20px;
        width: 95%;
      }

      .modal h2 {
        font-size: 1.2rem;
      }

      .back-btn {
        width: 40px;
        height: 40px;
        font-size: 1.2rem;
        top: 10px;
        left: 10px;
      }
    }

    /* Very Small Phones */
    @media (max-width: 360px) {
      #landingPage h1 {
        font-size: 1.4rem;
      }

      .mode-icon {
        font-size: 1.5rem;
      }

      .mode-title {
        font-size: 0.95rem;
      }

      .mode-desc {
        font-size: 0.75rem;
      }

      .matching-grid {
        gap: 5px;
      }

      .matching-card {
        font-size: 0.9rem;
      }

      .matching-card .card-back {
        font-size: 1.3rem;
      }

      .leaderboard-table {
        font-size: 0.7rem;
      }

      .leaderboard-table th,
      .leaderboard-table td {
        padding: 5px 3px;
      }
    }

    /* Large Desktop Screens */
    @media (min-width: 1440px) {
      .card {
        max-width: 1200px;
      }

      #landingPage h1 {
        font-size: 3.5rem;
      }

      .landing-container {
        gap: 40px;
      }

      .matching-grid {
        max-width: 700px;
        gap: 20px;
      }
    }
  </style>
  <style>@view-transition { navigation: auto; }</style>
  <script src="https://cdn.tailwindcss.com" type="text/javascript"></script>
 </head>
 <body>
  <div class="app-container"><!-- Landing Page -->
   <div id="landingPage" class="card">
    <h1 id="appTitle">🌸 Kimi-wa-melody 🌸</h1>
    <div class="mascot-tag" id="mascotTag">
     🐱 MelodyCat 🎵
    </div>
    <div class="landing-container"><!-- Left Side - Mode Selection (1x3) -->
     <div class="landing-left">
      <h2 style="text-align: center;">Select Mode</h2>
      <div class="mode-grid"><button class="mode-card selected" id="modeBtn-practice" onclick="selectMode('practice')">
        <div class="mode-icon">
         📚
        </div>
        <div class="mode-title">
         Practice Mode
        </div>
        <div class="mode-desc">
         Practice without time limit
        </div></button> <button class="mode-card" id="modeBtn-time_challenge" onclick="selectMode('time_challenge')">
        <div class="mode-icon">
         ⏰
        </div>
        <div class="mode-title">
         Time Challenge
        </div>
        <div class="mode-desc">
         60 second challenge
        </div></button> <button class="mode-card" id="modeBtn-matching" onclick="selectMode('matching')">
        <div class="mode-icon">
         🎴
        </div>
        <div class="mode-title">
         Matching Mode
        </div>
        <div class="mode-desc">
         Match musical notes game
        </div></button>
      </div>
     </div><!-- Right Side - Student Info Form -->
     <div class="landing-right">
      <h2 style="text-align: center;">Student Information</h2>
      <div class="form-group"><label for="studentName">Name (or Group Name)</label> <input type="text" id="studentName" placeholder="Enter name" required>
      </div>
      <div class="form-group"><label for="studentNo">Number</label> <input type="text" id="studentNo" placeholder="Enter number" required>
      </div>
      <div class="form-group"><label for="studentClass">Class</label> <input type="text" id="studentClass" placeholder="Enter class" required>
      </div>
      <div class="controls" style="margin-top: 20px; justify-content: stretch;"><button class="btn btn-primary" onclick="startGame()" style="width: 100%; font-size: 1.2rem;">Start Game 🎮</button>
      </div>
     </div>
    </div>
    <div class="controls" style="margin-top: 20px;"><button class="btn btn-info" onclick="showLeaderboard()">View Leaderboard</button> <button class="btn btn-warning" onclick="showExportModal()">Export Data (Teacher)</button>
    </div>
   </div><!-- Level Selection Page -->
   <div id="levelPage" class="card hidden"><button class="back-btn" onclick="backToLanding()">←</button>
    <h1>Select Level</h1>
    <p style="text-align: center; color: #d81b60; font-size: 1.1rem;" id="instructionText">Listen to the notes and choose the correct answer</p>
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
    <div class="controls"><button class="btn btn-info" onclick="playQuestion()" id="playBtn">🔊 Play</button> <button class="btn btn-warning" onclick="showAnswer()" id="answerBtn">👁️ Show Answer</button> <button class="btn btn-success hidden" onclick="nextQuestion()" id="nextBtn">➡️ Next</button>
    </div>
    <div id="feedback" class="feedback"></div>
    <div id="choicesContainer" class="choices-grid"></div>
    <div class="controls"><button class="btn btn-primary" onclick="saveScore()" id="saveScoreBtn">💾 Save Score</button>
    </div>
   </div><!-- Matching Game Page -->
   <div id="matchingPage" class="card hidden"><button class="back-btn" onclick="backToLanding()">←</button>
    <h1>🌸 Matching Mode 🌸</h1>
    <div class="info-bar">
     <div>
      <span id="matchingMoves">Moves: 0</span>
     </div>
     <div>
      <span id="matchingMatched">Matched: 0/8</span>
     </div>
     <div id="matchingTimerContainer"><span class="timer-display" id="matchingTimer">0:00</span>
     </div>
    </div>
    <p style="text-align: center; color: #d81b60; font-size: 1.1rem; margin: 15px 0;">Match note names with their positions on the staff! 🎵</p>
    <div class="matching-grid" id="matchingGrid"></div>
    <div class="controls"><button class="btn btn-warning" onclick="resetMatching()">🔄 Reset Game</button> <button class="btn btn-primary hidden" onclick="saveMatchingScore()" id="saveMatchingBtn">💾 Save Score</button>
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
    <h2>�� Enter Teacher PIN</h2>
    <div class="form-group"><label for="pinInput">PIN Code</label> <input type="password" id="pinInput" placeholder="Enter PIN">
    </div>
    <div class="controls"><button class="btn btn-primary" onclick="verifyPIN()">Confirm</button> <button class="btn btn-secondary" onclick="closePINModal()">Cancel</button>
    </div>
    <div id="pinError" style="color: #ef5350; text-align: center; margin-top: 10px; display: none;">
     Incorrect PIN
    </div>
   </div>
  </div>
  <script>
    // ========== Configuration ==========
    const defaultConfig = {
      app_title: "Kimi-wa-melody",
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
    
    // Matching mode state
    let matchingMoves = 0;
    let matchingMatched = 0;
    let matchingStartTime = 0;
    let matchingTimerInterval = null;
    let matchingFlippedCards = [];
    let matchingCards = [];

    // Selected mode on landing page
    let selectedMode = 'practice';

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
        legerLine.setAttribute('stroke', '#c97c9d');
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
      noteHead.setAttribute('fill', '#c97c9d');
      noteHead.setAttribute('transform', `rotate(-12 ${x} ${y})`);
      svg.appendChild(noteHead);
      
      // Draw stem
      const stem = document.createElementNS('http://www.w3.org/2000/svg', 'rect');
      stem.setAttribute('x', x + NOTE_CONFIG.headRx - 2);
      stem.setAttribute('y', y - NOTE_CONFIG.stemHeight);
      stem.setAttribute('width', NOTE_CONFIG.stemWidth);
      stem.setAttribute('height', NOTE_CONFIG.stemHeight);
      stem.setAttribute('fill', '#c97c9d');
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
        line.setAttribute('stroke', '#c97c9d');
        line.setAttribute('stroke-width', STAFF_CONFIG.strokeWidth);
        line.setAttribute('stroke-linecap', 'round');
        svg.appendChild(line);
      }
      
      // Redraw clef text
      const clefText = document.createElementNS('http://www.w3.org/2000/svg', 'text');
      clefText.setAttribute('x', '450');
      clefText.setAttribute('y', '30');
      clefText.setAttribute('fill', '#c97c9d');
      clefText.setAttribute('font-size', '18');
      clefText.setAttribute('font-weight', '600');
      clefText.setAttribute('text-anchor', 'middle');
      clefText.setAttribute('font-family', 'Arial, sans-serif');
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
        feedback.textContent = `❌ Wrong! Correct Answer: ${seqToLabel(currentSequence)}`;
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
        date: new Date().toLocaleDateString('en-US')
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
    function selectMode(mode) {
      selectedMode = mode;
      
      // Remove selected class from all mode cards
      document.querySelectorAll('.mode-card').forEach(card => {
        card.classList.remove('selected');
      });
      
      // Add selected class to clicked card
      document.getElementById(`modeBtn-${mode}`).classList.add('selected');
    }

    function startGame() {
      const name = document.getElementById('studentName').value.trim();
      const no = document.getElementById('studentNo').value.trim();
      const classRoom = document.getElementById('studentClass').value.trim();
      const mode = selectedMode;
      
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
      
      if (mode === 'matching') {
        // Start matching mode
        document.getElementById('landingPage').classList.add('hidden');
        document.getElementById('matchingPage').classList.remove('hidden');
        initMatchingGame();
      } else if (mode === 'time_challenge') {
        // Go directly to game without level selection
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
        // Show level selection for practice mode
        document.getElementById('landingPage').classList.add('hidden');
        document.getElementById('levelPage').classList.remove('hidden');
        renderLevelSelect();
      }
    }

    // ========== Matching Mode Functions ==========
    function initMatchingGame() {
      matchingMoves = 0;
      matchingMatched = 0;
      matchingFlippedCards = [];
      matchingStartTime = Date.now();
      
      // Start timer
      if (matchingTimerInterval) clearInterval(matchingTimerInterval);
      matchingTimerInterval = setInterval(updateMatchingTimer, 1000);
      
      // Create card pairs - 8 pairs = 16 cards
      const notes = ['C', 'D', 'E', 'F', 'G', 'A', 'B', 'C'];
      matchingCards = [];
      
      notes.forEach((note, index) => {
        // Text card
        matchingCards.push({
          id: `text-${index}`,
          type: 'text',
          note: note,
          matched: false
        });
        
        // Visual card (staff notation)
        matchingCards.push({
          id: `visual-${index}`,
          type: 'visual',
          note: note,
          matched: false
        });
      });
      
      // Shuffle cards
      matchingCards = shuffleArray(matchingCards);
      
      renderMatchingGrid();
      updateMatchingStats();
      document.getElementById('saveMatchingBtn').classList.add('hidden');
    }

    function renderMatchingGrid() {
      const grid = document.getElementById('matchingGrid');
      grid.innerHTML = '';
      
      matchingCards.forEach((card, index) => {
        const cardElement = document.createElement('div');
        cardElement.className = 'matching-card';
        cardElement.dataset.index = index;
        
        if (card.matched) {
          cardElement.classList.add('matched');
        }
        
        // Card back (flower emoji)
        const cardBack = document.createElement('div');
        cardBack.className = 'card-back';
        cardBack.textContent = '🌸';
        cardElement.appendChild(cardBack);
        
        // Card front (content)
        const cardFront = document.createElement('div');
        cardFront.className = 'card-front';
        
        if (card.type === 'text') {
          // Show note name with Thai name
          cardFront.innerHTML = `<div style="text-align: center;"><div style="font-size: 2rem;">${card.note}</div><div style="font-size: 1rem;">(${NOTE_NAMES_TH[card.note]})</div></div>`;
        } else {
          // Show staff notation
          const svg = createMiniStaff(card.note);
          cardFront.appendChild(svg);
        }
        
        cardElement.appendChild(cardFront);
        
        if (!card.matched) {
          cardElement.onclick = () => flipCard(index);
        }
        
        grid.appendChild(cardElement);
      });
    }

    function createMiniStaff(note) {
      const svg = document.createElementNS('http://www.w3.org/2000/svg', 'svg');
      svg.setAttribute('viewBox', '0 0 120 100');
      svg.setAttribute('width', '100%');
      svg.setAttribute('height', '100%');
      
      // Draw staff lines
      for (let i = 0; i < 5; i++) {
        const y = 70 - (i * 10);
        const line = document.createElementNS('http://www.w3.org/2000/svg', 'line');
        line.setAttribute('x1', '10');
        line.setAttribute('y1', y);
        line.setAttribute('x2', '110');
        line.setAttribute('y2', y);
        line.setAttribute('stroke', '#c97c9d');
        line.setAttribute('stroke-width', '2');
        svg.appendChild(line);
      }
      
      // Draw leger line for Middle C if needed
      const noteY = getNoteYPosition(note);
      if (note === 'C') {
        const legerLine = document.createElementNS('http://www.w3.org/2000/svg', 'line');
        legerLine.setAttribute('x1', '40');
        legerLine.setAttribute('y1', noteY);
        legerLine.setAttribute('x2', '80');
        legerLine.setAttribute('y2', noteY);
        legerLine.setAttribute('stroke', '#c97c9d');
        legerLine.setAttribute('stroke-width', '2');
        svg.appendChild(legerLine);
      }
      
      // Draw note
      const noteHead = document.createElementNS('http://www.w3.org/2000/svg', 'ellipse');
      noteHead.setAttribute('cx', '60');
      noteHead.setAttribute('cy', noteY);
      noteHead.setAttribute('rx', '8');
      noteHead.setAttribute('ry', '6');
      noteHead.setAttribute('fill', '#c97c9d');
      noteHead.setAttribute('transform', `rotate(-12 60 ${noteY})`);
      svg.appendChild(noteHead);
      
      // Draw stem
      const stem = document.createElementNS('http://www.w3.org/2000/svg', 'rect');
      stem.setAttribute('x', '67');
      stem.setAttribute('y', noteY - 30);
      stem.setAttribute('width', '2');
      stem.setAttribute('height', '30');
      stem.setAttribute('fill', '#c97c9d');
      svg.appendChild(stem);
      
      return svg;
    }

    function getNoteYPosition(note) {
      const positions = {
        'C': 80,  // Below staff
        'D': 75,  // Below line 1
        'E': 70,  // On line 1
        'F': 65,  // Space
        'G': 60,  // On line 2
        'A': 55,  // Space
        'B': 50   // On line 3
      };
      return positions[note];
    }

    function flipCard(index) {
      const card = matchingCards[index];
      
      if (card.matched || matchingFlippedCards.length >= 2) return;
      
      // Check if card is already flipped
      if (matchingFlippedCards.some(fc => fc.index === index)) return;
      
      // Flip the card
      const cardElement = document.querySelector(`.matching-card[data-index="${index}"]`);
      cardElement.classList.add('flipped');
      
      matchingFlippedCards.push({ index, card });
      
      if (matchingFlippedCards.length === 2) {
        matchingMoves++;
        updateMatchingStats();
        
        setTimeout(() => checkMatch(), 800);
      }
    }

    function checkMatch() {
      const [first, second] = matchingFlippedCards;
      
      if (first.card.note === second.card.note && first.card.type !== second.card.type) {
        // Match!
        matchingCards[first.index].matched = true;
        matchingCards[second.index].matched = true;
        matchingMatched++;
        
        const firstElement = document.querySelector(`.matching-card[data-index="${first.index}"]`);
        const secondElement = document.querySelector(`.matching-card[data-index="${second.index}"]`);
        
        firstElement.classList.add('matched');
        secondElement.classList.add('matched');
        firstElement.onclick = null;
        secondElement.onclick = null;
        
        playCorrect();
        
        // Check if game complete
        if (matchingMatched === 8) {
          setTimeout(() => {
            clearInterval(matchingTimerInterval);
            const elapsed = Math.floor((Date.now() - matchingStartTime) / 1000);
            
            const msg = document.createElement('div');
            msg.className = 'feedback show correct';
            msg.textContent = `�������� Congratulations! Completed in ${matchingMoves} moves and ${formatTime(elapsed)}! 🌸`;
            document.getElementById('matchingPage').insertBefore(msg, document.getElementById('matchingGrid'));
            
            document.getElementById('saveMatchingBtn').classList.remove('hidden');
          }, 500);
        }
      } else {
        // No match
        const firstElement = document.querySelector(`.matching-card[data-index="${first.index}"]`);
        const secondElement = document.querySelector(`.matching-card[data-index="${second.index}"]`);
        
        firstElement.classList.add('wrong');
        secondElement.classList.add('wrong');
        
        playWrong();
        
        setTimeout(() => {
          firstElement.classList.remove('flipped', 'wrong');
          secondElement.classList.remove('flipped', 'wrong');
        }, 1000);
      }
      
      matchingFlippedCards = [];
      updateMatchingStats();
    }

    function updateMatchingStats() {
      document.getElementById('matchingMoves').textContent = `Moves: ${matchingMoves}`;
      document.getElementById('matchingMatched').textContent = `Matched: ${matchingMatched}/8`;
    }

    function updateMatchingTimer() {
      const elapsed = Math.floor((Date.now() - matchingStartTime) / 1000);
      document.getElementById('matchingTimer').textContent = formatTime(elapsed);
    }

    function formatTime(seconds) {
      const mins = Math.floor(seconds / 60);
      const secs = seconds % 60;
      return `${mins}:${secs.toString().padStart(2, '0')}`;
    }

    function resetMatching() {
      if (matchingTimerInterval) clearInterval(matchingTimerInterval);
      
      // Remove any feedback messages
      document.querySelectorAll('#matchingPage .feedback').forEach(el => el.remove());
      
      initMatchingGame();
    }

    async function saveMatchingScore() {
      if (!currentStudent) {
        showFeedbackMessage('Student information not found', false);
        return;
      }

      if (!dataSdkReady) {
        const msg = document.createElement('div');
        msg.className = 'feedback show incorrect';
        msg.textContent = '❌ System not ready, please wait';
        document.getElementById('matchingPage').appendChild(msg);
        setTimeout(() => msg.remove(), 3000);
        return;
      }

      const saveBtn = document.getElementById('saveMatchingBtn');
      saveBtn.disabled = true;
      saveBtn.textContent = '⏳ Saving...';

      try {
        const elapsed = Math.floor((Date.now() - matchingStartTime) / 1000);
        
        const record = {
          student_name: currentStudent.name,
          class_room: currentStudent.class,
          student_no: currentStudent.no,
          mode: 'matching',
          level: matchingMoves,
          score: elapsed,
          total: 8,
          timestamp: new Date().toISOString()
        };

        const result = await window.dataSdk.create(record);

        if (result.isOk) {
          const msg = document.createElement('div');
          msg.className = 'feedback show correct';
          msg.textContent = '✅ Score saved successfully!';
          document.getElementById('matchingPage').appendChild(msg);
          setTimeout(() => msg.remove(), 3000);
        } else {
          const msg = document.createElement('div');
          msg.className = 'feedback show incorrect';
          msg.textContent = `❌ Error: ${result.error?.message || 'Could not save'}`;
          document.getElementById('matchingPage').appendChild(msg);
          setTimeout(() => msg.remove(), 3000);
        }
      } catch (error) {
        const msg = document.createElement('div');
        msg.className = 'feedback show incorrect';
        msg.textContent = `��� Error: ${error.message}`;
        document.getElementById('matchingPage').appendChild(msg);
        setTimeout(() => msg.remove(), 3000);
      } finally {
        saveBtn.disabled = false;
        saveBtn.textContent = '💾 Save Score';
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
      if (matchingTimerInterval) clearInterval(matchingTimerInterval);
      document.getElementById('levelPage').classList.add('hidden');
      document.getElementById('gamePage').classList.add('hidden');
      document.getElementById('matchingPage').classList.add('hidden');
      document.getElementById('leaderboardPage').classList.add('hidden');
      document.getElementById('landingPage').classList.remove('hidden');
    }

    function backToLevelSelect() {
      stopTimer();
      document.getElementById('gamePage').classList.add('hidden');
      
      // If in time challenge mode, go back to landing
      if (currentMode === 'time_challenge') {
        document.getElementById('landingPage').classList.remove('hidden');
      } else {
        // Practice mode - go to level selection
        document.getElementById('levelPage').classList.remove('hidden');
        renderLevelSelect();
      }
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
        cell.style.color = '#ec407a';
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
      if (!currentStudent) {
        showFeedbackMessage('Student information not found', false);
        return;
      }

      if (!dataSdkReady) {
        showFeedbackMessage('❌ System not ready, please wait', false);
        return;
      }

      const saveBtn = document.getElementById('saveScoreBtn');
      saveBtn.disabled = true;
      saveBtn.textContent = '⏳ Saving...';

      try {
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

        const result = await window.dataSdk.create(record);

        if (result.isOk) {
          showFeedbackMessage('✅ Score saved successfully!', true);
        } else {
          showFeedbackMessage(`❌ Error: ${result.error?.message || 'Could not save'}`, false);
        }
      } catch (error) {
        showFeedbackMessage(`❌ Error: ${error.message}`, false);
      } finally {
        saveBtn.disabled = false;
        saveBtn.textContent = '💾 Save Score';
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
      const records = window.kimiRecords || [];
      
      if (records.length === 0) {
        const msg = document.createElement('div');
        msg.className = 'feedback show incorrect';
        msg.textContent = 'No data to export';
        document.getElementById('landingPage').appendChild(msg);
        setTimeout(() => msg.remove(), 3000);
        return;
      }
      
      // Create CSV with proper headers
      let csv = 'Name,Class,Number,Mode,Level,Score,Total,Date\n';
      
      records.forEach(record => {
        const date = new Date(record.timestamp).toLocaleDateString('en-US');
        const name = (record.student_name || '').replace(/"/g, '""');
        const classRoom = (record.class_room || '').replace(/"/g, '""');
        const studentNo = (record.student_no || '').replace(/"/g, '""');
        const mode = (record.mode || '').replace(/"/g, '""');
        csv += `"${name}","${classRoom}","${studentNo}","${mode}",${record.level},${record.score},${record.total},"${date}"\n`;
      });
      
      // Add BOM for UTF-8 Excel compatibility
      const BOM = '\uFEFF';
      const blob = new Blob([BOM + csv], { type: 'text/csv;charset=utf-8;' });
      const url = URL.createObjectURL(blob);
      
      // Create download link
      const link = document.createElement('a');
      link.setAttribute('href', url);
      link.setAttribute('download', `kimi-melody-records-${new Date().toISOString().split('T')[0]}.csv`);
      link.style.display = 'none';
      document.body.appendChild(link);
      
      // Trigger download
      link.click();
      
      // Cleanup
      setTimeout(() => {
        document.body.removeChild(link);
        URL.revokeObjectURL(url);
      }, 100);
      
      // Show success message
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

      document.getElementById('appTitle').textContent = `🌸 ${appTitle} 🌸`;
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

      // Set default mode selection
      selectMode('practice');
    }

    // Start initialization
    init();
  </script>
 <script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'9a833fa02312d036',t:'MTc2NDc2Njg0My4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>

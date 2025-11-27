<html....>
<html lang="th">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Kimi-wa-Melody — Final</title>
<link href="https://fonts.googleapis.com/css2?family=Kanit:wght@300;400;600&display=swap" rel="stylesheet">
<style>
:root{
  --bg:#efe7d7; --card:#fff7ee; --accent:#7C5A3A; --muted:#765b44; --good:#2E8B57; --bad:#C03B3B;
  --timegreen-start:#E6F7ED; --timegreen-accent:#4B8A5A;
}
*{box-sizing:border-box}
body{margin:0;font-family:'Kanit',system-ui,Segoe UI,Roboto,'Noto Sans',Arial;color:#2b2b2b;background:linear-gradient(135deg,#d4c5a9 0%,#b8a58a 100%)}
.app-container{max-width:1100px;margin:22px auto;padding:18px}
.card{background:var(--card);border-radius:18px;padding:18px;margin-bottom:14px;box-shadow:0 12px 36px rgba(0,0,0,0.12)}
.header{display:flex;align-items:center;gap:12px}
.header h1{margin:0;font-size:26px;color:var(--muted)}
.mascot{font-size:34px}
.form-row{display:flex;gap:12px;flex-wrap:wrap}
.input,select,button{font-family:inherit}
.input{padding:10px;border-radius:10px;border:1px solid rgba(0,0,0,0.08);width:100%}
.controls{display:flex;gap:10px;flex-wrap:wrap;align-items:center}
.btn{padding:10px 14px;border-radius:10px;border:none;cursor:pointer;font-weight:700}
.btn-primary{background:var(--accent);color:white;box-shadow:0 8px 20px rgba(124,90,58,0.15)}
.btn-info{background:linear-gradient(135deg,#9bb3c4,#7a96aa);color:white}
.btn-success{background:linear-gradient(135deg,#7a9b6f,#5d7a52);color:white}
.small{color:var(--muted);font-size:13px}
.staff-card{padding:12px;border-radius:12px;background:white;box-shadow:0 10px 30px rgba(0,0,0,0.06)}
#staffSVG{width:100%;height:auto;display:block}
.choices{display:grid;grid-template-columns:repeat(auto-fit,minmax(140px,1fr));gap:10px;margin-top:12px}
.choice{padding:12px;border-radius:10px;background:#fff;border:1px solid rgba(0,0,0,0.06);cursor:pointer;font-weight:700;text-align:center}
.choice.correct{background:var(--good);color:white;border-color:rgba(46,139,87,0.9)}
.choice.wrong{background:var(--bad);color:white}
.feedback{margin-top:12px;padding:10px;border-radius:10px;display:none}
.feedback.show{display:block}
.feedback.correct{background:#e8f6ea;color:var(--good);border:1px solid rgba(46,139,87,0.12)}
.feedback.incorrect{background:#fff0f0;color:var(--bad);border:1px solid rgba(192,59,59,0.12)}
.level-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(80px,1fr));gap:8px}
.level-btn{padding:10px;border-radius:8px;background:#fff;border:1px solid #e6d9c7;cursor:pointer}
.level-btn.completed{background:var(--good);color:#fff}
.modal-backdrop{position:fixed;inset:0;background:rgba(0,0,0,0.45);display:none;align-items:center;justify-content:center;z-index:60}
.modal{background:var(--card);padding:16px;border-radius:12px;min-width:320px}
.leaderboard{max-height:320px;overflow:auto}
.timer{font-weight:900;color:var(--muted)}
@media(max-width:720px){.form-row{flex-direction:column}}
</style>
</head>
<body>
<div class="app-container">
  <div class="card header">
    <div class="mascot">🐱</div>
    <div>
      <h1>Kimi-wa-Melody</h1>
      <div class="small">โปรโตไทป์ฝึกอ่านโน้ต — MelodyCat</div>
    </div>
    <div style="margin-left:auto" class="small">PIN ครู: <span style="font-weight:800">Teacherversion5791</span></div>
  </div>

  <!-- Landing -->
  <div id="landing" class="card">
    <div style="display:flex;gap:12px;align-items:center;justify-content:space-between">
      <div>
        <h2 style="margin:0">เริ่มต้น</h2>
        <div class="small">กรอกข้อมูลนักเรียนก่อนเริ่ม</div>
      </div>
    </div>
    <div style="margin-top:12px" class="form-row">
      <div style="flex:1">
        <label class="small">ชื่อ-สกุล / ชื่อกลุ่ม</label>
        <input id="landingName" class="input" placeholder="เช่น นุ่น / กลุ่ม 1">
      </div>
      <div style="width:120px">
        <label class="small">เลขที่</label>
        <input id="landingNo" class="input" placeholder="เลขที่">
      </div>
      <div style="width:140px">
        <label class="small">ห้อง</label>
        <input id="landingClass" class="input" placeholder="เช่น ป.4/1">
      </div>
      <div style="width:220px">
        <label class="small">โหมด</label>
        <select id="landingMode" class="input">
          <option value="practice">Practice — แบบฝึก</option>
          <option value="time">Time Challenge — 60 วินาที</option>
        </select>
      </div>
    </div>
    <div style="margin-top:12px" class="controls">
      <button class="btn btn-primary" id="startBtn">เริ่มเลย</button>
      <button class="btn btn-info" id="showLeaderboardBtn">ดูกระดานคะแนน</button>
      <button class="btn btn-success" id="showExportBtn">ส่งออกข้อมูล (ครู)</button>
    </div>
  </div>

  <!-- Level select -->
  <div id="levelPanel" class="card" style="display:none">
    <h2 style="margin:0">เลือกด่าน</h2>
    <div class="small" id="levelHint" style="margin-top:6px">ด่าน 1–7 : 1 โน้ต / ข้อ · ด่าน 8–14 : 2 โน้ต / ข้อ · ด่าน 15–20 : 3 โน้ต / ข้อ</div>
    <div style="margin-top:12px" id="levelGrid" class="level-grid"></div>
    <div style="margin-top:12px" class="controls">
      <button class="btn" id="backToLanding">กลับ</button>
    </div>
  </div>

  <!-- Game -->
  <div id="gamePanel" class="card" style="display:none">
    <div style="display:flex;gap:12px;align-items:center;justify-content:space-between">
      <div>
        <div class="small">ด่าน <span id="levelDisplay">1</span></div>
        <div class="small">ข้อ <span id="qDisplay">1</span>/10</div>
      </div>
      <div class="small">คะแนน: <span id="scoreDisplay">0</span></div>
      <div class="small timer" id="timerDisplay" style="display:none">60</div>
    </div>

    <div style="margin-top:12px" class="staff-card">
      <svg id="staffSVG" viewBox="0 0 900 300" xmlns="http://www.w3.org/2000/svg" aria-label="staff"></svg>
    </div>

    <div style="margin-top:12px" class="controls">
      <button class="btn btn-info" id="playBtn">🔊 ฟัง</button>
      <button class="btn btn-primary" id="showAnswerBtn">ดูคำตอบ</button>
      <button class="btn btn-success" id="nextBtn" style="display:none">ถัดไป</button>
    </div>

    <div id="choices" class="choices"></div>

    <div id="feedback" class="feedback"></div>

    <div style="margin-top:12px" class="controls">
      <button class="btn btn-success" id="saveScoreBtn">💾 บันทึกคะแนน</button>
      <button class="btn" id="backToLevels">กลับ</button>
    </div>
  </div>

  <!-- Leaderboard -->
  <div id="leaderboardPanel" class="card" style="display:none">
    <h2>กระดานคะแนน Time Challenge</h2>
    <div class="leaderboard" id="leaderboardList"></div>
    <div style="margin-top:12px" class="controls">
      <button class="btn" id="lbBack">กลับ</button>
    </div>
  </div>

  <!-- Export modal -->
  <div id="pinModal" class="modal-backdrop">
    <div class="modal">
      <h3>ยืนยันรหัสครู</h3>
      <div style="margin-top:8px">
        <label class="small">รหัส PIN</label>
        <input id="pinInput" class="input" type="password" placeholder="รหัสครู">
      </div>
      <div style="margin-top:12px" class="controls">
        <button class="btn btn-primary" id="pinOk">ยืนยัน</button>
        <button class="btn" id="pinCancel">ยกเลิก</button>
      </div>
      <div id="pinError" class="small" style="color:var(--bad);display:none;margin-top:8px">รหัสไม่ถูกต้อง</div>
    </div>
  </div>

</div>

<script>
/* ================= CONFIG ================= */
const TEACHER_PIN = "Teacherversion5791";
const TOTAL_LEVELS = 20;
const QUESTIONS_PER_LEVEL = 10;

const NOTES = ['C','D','E','F','G','A','B'];
const NOTE_NAMES_TH = {C:'โด',D:'เร',E:'มี',F:'ฟา',G:'ซอล',A:'ลา',B:'ที'};
const NOTE_FREQ = {C:261.63,D:293.66,E:329.63,F:349.23,G:392.00,A:440.00,B:493.88};

/* Staff geometry */
const STAFF = { left:110, right:760, bottomY:170, gap:20, strokeWidth:4 };

/* Note rendering */
const NOTE_CFG = { startX:360, stepX:48, rx:16, ry:12, stemW:3.8, stemH:60 };

/* Clef SVG path (clean, high-fidelity) */
const CLEF_PATH = `
M115.9,19.6c-3.1,1.6-6.8,4.8-9.9,8.6c-6.0,7.6-8.5,16.8-6.3,24.0c2.1,6.9,8.5,11.8,16.3,13.4c5.8,1.1,11.6,0.7,16.3-1.3
c8.6-3.6,13.8-11.3,14.9-20.3c1.2-9.9-2.9-20.6-12.2-30.9c-2.9-3.0-6.0-5.6-9.3-7.7c-4.1-2.6-8.0-4.6-11.8-6.1z
M111.4,46.8c2.6-0.9,5.9-0.6,9.4,0.8c6.1,2.4,9.6,6.7,10.0,11.0c0.6,6.7-3.7,13.3-11.8,17.4c-4.5,2.4-9.6,3.4-14.8,2.9
c-6.2-0.6-11.3-3.7-14.6-8.4c-3.0-4.2-3.8-9.5-2.2-14.1c1.1-3.1,3.5-6.0,6.6-8.4C98.1,50.9,104.6,48.3,111.4,46.8z
M121.0,95.3c-0.3,1.3-0.7,2.5-1.3,3.7c-2.8,6.4-8.9,11.6-17.6,15.0c-3.9,1.5-8.0,2.5-12.0,3.2c-6.6,1.0-12.2,2.6-16.1,4.6
c-6.2,3.2-9.6,7.6-9.7,12.9c-0.2,6.2,4.0,11.8,12.4,16.5c7.8,4.3,17.9,6.5,28.7,6.5c9.6,0,19.1-1.9,26.5-6.4
c6.2-3.8,9.7-8.5,10.6-13.2c0.9-4.8-0.6-9.5-4.1-13.4c-3.8-4.2-9.9-6.8-18.0-7.9c-1.9-0.2-4.0-0.2-6.1,0.0c-4.3,0.4-7.9,1.3-10.6,2.7
c-2.6,1.3-4.5,3.0-5.6,5.1c-1.2,2.3-1.5,5.0-0.6,7.9c1.3,4.1,5.0,7.6,10.8,10.8c5.6,3.0,12.0,4.5,18.6,4.5c5.6,0,11.2-0.9,15.7-2.6
c3.5-1.3,6.6-3.0,9.2-5.1c2.5-2.0,4.6-4.4,6.1-7.1c1.5-2.8,2.3-5.7,2.4-8.6c0.1-3.3-0.9-6.6-2.9-9.9c-3.3-5.3-9.5-9.3-18.4-11.6
c-3.9-1.0-8.3-1.8-13.1-2.2c-0.6-0.0-1.1-0.0-1.7-0.0C123.3,94.9,122.1,95.1,121.0,95.3z
`;

/* Clef transform: change these to fine-tune x/y/scale */
const CLEF_TRANSFORM = { tx:52, ty:-68, s:0.21 };

/* =============== State =============== */
let state = {
  student: {name:'', no:'', class:''},
  mode: 'practice',
  level: 1,
  qIndex: 0,
  score: 0,
  current: null,
  running: false,
  timeTimer: null,
  timeLeft: 60
};

/* =============== Helpers: Audio =============== */
let audioCtx = null;
function ensureAudio(){ if(!audioCtx) audioCtx = new (window.AudioContext || window.webkitAudioContext)(); }
function playTone(freq, t=0.45){
  ensureAudio();
  const o = audioCtx.createOscillator();
  const g = audioCtx.createGain();
  o.type = 'sine'; o.frequency.value = freq;
  o.connect(g); g.connect(audioCtx.destination);
  g.gain.setValueAtTime(0.0001,audioCtx.currentTime);
  g.gain.exponentialRampToValueAtTime(0.18,audioCtx.currentTime+0.01);
  o.start(); g.gain.exponentialRampToValueAtTime(0.001,audioCtx.currentTime+t);
  setTimeout(()=>o.stop(), (t+0.05)*1000);
}
function playSeq(seq, interval=380){
  seq.forEach((n,i)=> setTimeout(()=> playTone(NOTE_FREQ[n]), i*interval));
}
function playCorrect(){ playSeq(['C','E','G'],200); }
function playWrong(){ playSeq(['G','F','E'],180); }

/* =============== SVG draw =============== */
const svgNS = 'http://www.w3.org/2000/svg';
function drawStaffAndClef(){
  const svg = document.getElementById('staffSVG');
  svg.innerHTML = '';

  // staff lines
  for(let i=0;i<5;i++){
    const y = STAFF.bottomY - i*STAFF.gap;
    const line = document.createElementNS(svgNS,'line');
    line.setAttribute('x1', STAFF.left);
    line.setAttribute('y1', y);
    line.setAttribute('x2', STAFF.right);
    line.setAttribute('y2', y);
    line.setAttribute('stroke', '#000');
    line.setAttribute('stroke-width', STAFF.strokeWidth);
    line.setAttribute('stroke-linecap','round');
    svg.appendChild(line);
  }

  // add clef group with path
  const g = document.createElementNS(svgNS,'g');
  g.setAttribute('transform', `translate(${CLEF_TRANSFORM.tx}, ${CLEF_TRANSFORM.ty}) scale(${CLEF_TRANSFORM.s})`);
  const p = document.createElementNS(svgNS,'path');
  p.setAttribute('d', CLEF_PATH);
  p.setAttribute('fill', '#000');
  g.appendChild(p);
  svg.appendChild(g);

  // store for notes rendering
  svg.dataset.bottomY = STAFF.bottomY;
  svg.dataset.gap = STAFF.gap;
}

/* Map note to Y position (Treble clef mapping; bottom staff line is E) */
function getY(note){
  const svg = document.getElementById('staffSVG');
  const bottomY = parseFloat(svg.dataset.bottomY || STAFF.bottomY);
  const gap = parseFloat(svg.dataset.gap || STAFF.gap);
  const map = {
    C: bottomY + gap, // middle C (ledger)
    D: bottomY + gap/2,
    E: bottomY,
    F: bottomY - gap/2,
    G: bottomY - gap,
    A: bottomY - gap*1.5,
    B: bottomY - gap*2
  };
  return map[note];
}

function renderSequence(seq){
  const svg = document.getElementById('staffSVG');

  // preserve staff & clef (first two children likely staff lines + clef)
  const preserved = [];
  const children = Array.from(svg.childNodes);
  // Keep lines and clef group (we assume lines are first 5 and clef is next)
  for(let i=0;i<svg.childNodes.length;i++){
    const node = svg.childNodes[i];
    if(node.tagName === 'line' || (node.tagName === 'g' && node.querySelector('path'))) preserved.push(node.cloneNode(true));
  }
  svg.innerHTML = '';
  preserved.forEach(n => svg.appendChild(n));

  // draw notes
  seq.forEach((note,i)=>{
    const x = NOTE_CFG.startX + i*NOTE_CFG.stepX;
    const y = getY(note);
    // ledger for C
    if(note === 'C'){
      const ledger = document.createElementNS(svgNS,'line');
      ledger.setAttribute('x1', x-22); ledger.setAttribute('y1', y); ledger.setAttribute('x2', x+22); ledger.setAttribute('y2', y);
      ledger.setAttribute('stroke','#000'); ledger.setAttribute('stroke-width',3);
      svg.appendChild(ledger);
    }
    // head
    const head = document.createElementNS(svgNS,'ellipse');
    head.setAttribute('cx', x); head.setAttribute('cy', y); head.setAttribute('rx', NOTE_CFG.rx); head.setAttribute('ry', NOTE_CFG.ry);
    head.setAttribute('fill','#000'); head.setAttribute('transform', `rotate(-12 ${x} ${y})`);
    svg.appendChild(head);
    // stem
    const stem = document.createElementNS(svgNS,'rect');
    stem.setAttribute('x', x + NOTE_CFG.rx - 2); stem.setAttribute('y', y - NOTE_CFG.stemH); stem.setAttribute('width', NOTE_CFG.stemW); stem.setAttribute('height', NOTE_CFG.stemH);
    stem.setAttribute('fill','#000');
    svg.appendChild(stem);
  });
}

/* =============== Questions & choices =============== */
function notesPerQuestion(level){ if(level<=7) return 1; if(level<=14) return 2; return 3; }
function randomSeq(k){ return Array.from({length:k},()=> NOTES[Math.floor(Math.random()*NOTES.length)]); }
function seqLabel(seq){ return seq.map(n=> `${n}(${NOTE_NAMES_TH[n]})`).join(' '); }

function makeChoices(correct){
  const k = correct.length;
  if(k===1){
    // all 7 single notes
    const arr = NOTES.map(n=> [n]);
    return shuffle(arr);
  } else {
    const set = new Set([JSON.stringify(correct)]);
    const choices = [correct];
    while(choices.length<4){
      const cand = randomSeq(k);
      const s = JSON.stringify(cand);
      if(!set.has(s)){ set.add(s); choices.push(cand); }
    }
    return shuffle(choices);
  }
}
function shuffle(a){ const arr=a.slice(); for(let i=arr.length-1;i>0;i--){ const j=Math.floor(Math.random()*(i+1)); [arr[i],arr[j]]=[arr[j],arr[i]] } return arr; }

function generateQuestion(){
  const k = notesPerQuestion(state.level);
  const seq = randomSeq(k);
  const choices = makeChoices(seq);
  state.current = { seq, choices, answer: JSON.stringify(seq) };
  renderSequence(seq);
  renderChoices(choices);
  document.getElementById('qDisplay').textContent = (state.qIndex+1);
  document.getElementById('feedback').className = 'feedback';
  document.getElementById('nextBtn').style.display = 'none';
}

/* render choices */
function renderChoices(choices){
  const ctn = document.getElementById('choices');
  ctn.innerHTML = '';
  choices.forEach(ch=>{
    const btn = document.createElement('button');
    btn.className = 'choice';
    btn.textContent = seqLabel(ch);
    btn.onclick = ()=> onChoice(ch, btn);
    ctn.appendChild(btn);
  });
}

/* handle answer */
function onChoice(ch, btn){
  if(state.answered) return;
  state.answered = true;
  const correct = JSON.stringify(ch) === state.current.answer;
  if(correct){
    btn.classList.add('correct');
    document.getElementById('feedback').textContent = 'ถูกต้อง!';
    document.getElementById('feedback').className = 'feedback show correct';
    playCorrect();
    state.score++;
  } else {
    btn.classList.add('wrong');
    document.getElementById('feedback').textContent = 'ผิด! คำตอบ: ' + seqLabel(JSON.parse(state.current.answer));
    document.getElementById('feedback').className = 'feedback show incorrect';
    playWrong();
    // highlight correct
    Array.from(document.querySelectorAll('.choice')).forEach(b=>{
      if(b.textContent === seqLabel(JSON.parse(state.current.answer))) b.classList.add('correct');
    });
  }
  // disable choices
  Array.from(document.querySelectorAll('.choice')).forEach(b=> b.disabled=true);
  document.getElementById('scoreDisplay').textContent = state.score;
  document.getElementById('nextBtn').style.display = 'inline-block';
}

/* =============== Flow control =============== */
function startPractice(level){
  state.mode='practice'; state.level=level; state.qIndex=0; state.score=0; state.answered=false;
  document.getElementById('landing').style.display='none';
  document.getElementById('levelPanel').style.display='none';
  document.getElementById('gamePanel').style.display='block';
  document.getElementById('levelDisplay').textContent = level;
  drawStaffAndClef(); generateQuestion();
}
function startTimeChallenge(){
  state.mode='time'; state.level=1; state.score=0; state.qIndex=0; state.answered=false; state.timeLeft=60;
  document.getElementById('landing').style.display='none';
  document.getElementById('gamePanel').style.display='block';
  document.getElementById('levelDisplay').textContent = 'Time Challenge';
  document.getElementById('timerDisplay').style.display='block';
  drawStaffAndClef(); generateQuestion(); startTimer();
}

function next(){
  state.answered=false;
  if(state.mode==='practice'){
    state.qIndex++;
    if(state.qIndex >= QUESTIONS_PER_LEVEL){ endLevel(); return; }
    generateQuestion();
  } else {
    // time mode continuous
    state.qIndex++;
    generateQuestion(); playSeq(state.current.seq);
  }
}

function endLevel(){
  document.getElementById('feedback').textContent = `จบด่าน ${state.level} คะแนน ${state.score}`;
  document.getElementById('feedback').className = 'feedback show correct';
  document.getElementById('nextBtn').style.display='none';
  // mark completed
  const done = JSON.parse(localStorage.getItem('kimi_done')||'[]');
  if(!done.includes(state.level)){ done.push(state.level); localStorage.setItem('kimi_done', JSON.stringify(done)); }
}

/* =============== Timer for Time Challenge =============== */
function startTimer(){
  stopTimer();
  document.getElementById('timerDisplay').textContent = state.timeLeft;
  state.timeTimer = setInterval(()=>{
    state.timeLeft--;
    document.getElementById('timerDisplay').textContent = state.timeLeft;
    if(state.timeLeft<=0){ stopTimer(); endTime(); }
  },1000);
}
function stopTimer(){ if(state.timeTimer){ clearInterval(state.timeTimer); state.timeTimer=null; } }
function endTime(){
  document.getElementById('feedback').textContent = `หมดเวลา! คะแนน ${state.score}`;
  document.getElementById('feedback').className = 'feedback show correct';
  // save leaderboard
  saveLeaderboard();
  // disable choices
  Array.from(document.querySelectorAll('.choice')).forEach(b=> b.disabled=true);
  document.getElementById('nextBtn').style.display='none';
}

/* =============== Leaderboard & Storage =============== */
function saveLeaderboard(){
  const lb = JSON.parse(localStorage.getItem('kimi_time_leaderboard')||'[]');
  lb.push({name: state.student.name, class: state.student.class, no: state.student.no, score: state.score, total: state.qIndex+1, date: new Date().toLocaleString()});
  // sort by score desc
  lb.sort((a,b)=> b.score - a.score);
  localStorage.setItem('kimi_time_leaderboard', JSON.stringify(lb.slice(0,50)));
}

function renderLeaderboard(){
  const lb = JSON.parse(localStorage.getItem('kimi_time_leaderboard')||'[]');
  const el = document.getElementById('leaderboardList');
  if(lb.length===0){ el.innerHTML='<div class="small">ยังไม่มีคะแนน</div>'; return; }
  el.innerHTML = lb.slice(0,20).map((r,i)=> `<div style="padding:8px;border-bottom:1px solid #eee">${i+1}. ${r.name} (${r.class} ${r.no}) — ${r.score}/${r.total} — ${r.date}</div>`).join('');
}

/* =============== UI wiring =============== */
document.getElementById('startBtn').addEventListener('click', ()=>{
  const name=document.getElementById('landingName').value.trim();
  const no=document.getElementById('landingNo').value.trim();
  const cls=document.getElementById('landingClass').value.trim();
  const mode=document.getElementById('landingMode').value;
  if(!name || !no || !cls){ alert('กรุณากรอกข้อมูลให้ครบ'); return; }
  state.student={name, no, class:cls};
  // save locally
  localStorage.setItem('kimi_student', JSON.stringify(state.student));
  if(mode==='time'){ startTimeChallenge(); } else {
    // show level selection
    document.getElementById('landing').style.display='none';
    document.getElementById('levelPanel').style.display='block';
    renderLevels();
  }
});

function renderLevels(){
  const container = document.getElementById('levelGrid');
  container.innerHTML='';
  const done = JSON.parse(localStorage.getItem('kimi_done')||'[]');
  for(let i=1;i<=TOTAL_LEVELS;i++){
    const btn = document.createElement('button');
    btn.className = 'level-btn' + (done.includes(i)? ' completed':'');
    btn.textContent = 'ด่าน '+i;
    btn.onclick = ()=> { state.level=i; startPractice(i); };
    container.appendChild(btn);
  }
}

document.getElementById('backToLanding').addEventListener('click', ()=>{
  document.getElementById('levelPanel').style.display='none';
  document.getElementById('landing').style.display='block';
});
document.getElementById('backToLevels').addEventListener('click', ()=>{
  stopTimer();
  document.getElementById('gamePanel').style.display='none';
  document.getElementById('levelPanel').style.display='block';
  renderLevels();
});
document.getElementById('showLeaderboardBtn').addEventListener('click', ()=>{
  renderLeaderboard();
  document.getElementById('landing').style.display='none';
  document.getElementById('leaderboardPanel').style.display='block';
});
document.getElementById('lbBack').addEventListener('click', ()=>{
  document.getElementById('leaderboardPanel').style.display='none';
  document.getElementById('landing').style.display='block';
});
document.getElementById('playBtn').addEventListener('click', ()=> { if(state.current) playSeq(state.current.seq); });
document.getElementById('showAnswerBtn').addEventListener('click', ()=>{
  if(!state.current) return;
  document.getElementById('feedback').textContent = 'คำตอบ: ' + seqLabel(JSON.parse(state.current.answer));
  document.getElementById('feedback').className = 'feedback show incorrect';
  Array.from(document.querySelectorAll('.choice')).forEach(b=>{
    if(b.textContent === seqLabel(JSON.parse(state.current.answer))) b.classList.add('correct');
    b.disabled = true;
  });
  document.getElementById('nextBtn').style.display='inline-block';
});
document.getElementById('nextBtn').addEventListener('click', ()=> next());
document.getElementById('saveScoreBtn').addEventListener('click', saveScoreLocal);

function saveScoreLocal(){
  // Save a record to localStorage (for teacher export)
  const recs = JSON.parse(localStorage.getItem('kimi_records_all')||'[]');
  recs.push({
    student_name: state.student.name,
    class_room: state.student.class,
    student_no: state.student.no,
    mode: state.mode,
    level: state.level,
    score: state.score,
    total: state.qIndex+1,
    timestamp: new Date().toISOString()
  });
  localStorage.setItem('kimi_records_all', JSON.stringify(recs));
  alert('บันทึกคะแนนเรียบร้อย');
}

/* =============== Export (PIN modal) =============== */
document.getElementById('showExportBtn').addEventListener('click', ()=> {
  document.getElementById('pinModal').style.display = 'flex';
});
document.getElementById('pinCancel').addEventListener('click', ()=> {
  document.getElementById('pinModal').style.display = 'none';
});
document.getElementById('pinOk').addEventListener('click', ()=> {
  const val = document.getElementById('pinInput').value;
  if(val === TEACHER_PIN){
    document.getElementById('pinModal').style.display = 'none';
    exportCSVLocal();
  } else {
    document.getElementById('pinError').style.display = 'block';
  }
});

function exportCSVLocal(){
  const recs = JSON.parse(localStorage.getItem('kimi_records_all')||'[]');
  if(recs.length===0){ alert('ไม่มีข้อมูลให้ส่งออก'); return; }
  let csv = 'name,class,no,mode,level,score,total,date\n';
  recs.forEach(r=>{
    csv += `"${r.student_name}","${r.class_room}","${r.student_no}","${r.mode}",${r.level},${r.score},${r.total},"${new Date(r.timestamp).toLocaleString('th-TH')}"\n`;
  });
  const blob = new Blob([csv], {type: 'text/csv;charset=utf-8;'});
  const link = document.createElement('a'); link.href = URL.createObjectURL(blob);
  link.download = `kimi_records_${new Date().toISOString().split('T')[0]}.csv`; link.click();
  alert('ส่งออก CSV เรียบร้อย');
}

/* =============== Init =============== */
(function init(){
  // restore saved student fields
  const s = JSON.parse(localStorage.getItem('kimi_student')||'null');
  if(s){ document.getElementById('landingName').value = s.name; document.getElementById('landingNo').value = s.no; document.getElementById('landingClass').value = s.class; state.student=s; }

  // initial draw staff & clef
  drawStaffAndClef();
})();
</script>
</body>
</html>
